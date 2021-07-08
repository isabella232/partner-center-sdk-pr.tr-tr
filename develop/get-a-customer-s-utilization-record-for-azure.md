---
title: Müşterinin Azure kullanım kayıtlarını alma
description: Belirli bir süre boyunca bir müşterinin Azure aboneliğinin kullanım kayıtlarını almak için Azure kullanım API 'sini kullanabilirsiniz.
ms.date: 04/19/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7024bc65976a9b43a62b66c529d271519181ab23
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874933"
---
# <a name="get-a-customers-utilization-records-for-azure"></a>Müşterinin Azure kullanım kayıtlarını alma

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Azure kullanım API 'sini kullanarak belirli bir süre için müşterinin Azure aboneliğinin kullanım kayıtlarını alabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik tanımlayıcısı.

Bu API, rastgele bir zaman aralığı için günlük ve saatlik derecelendirilmemiş tüketim döndürür. Ancak, *Bu API Azure planları için desteklenmez*. Bir Azure planınız varsa, [Fatura faturalandırılmamış tüketim satırı öğelerini Al](get-invoice-unbilled-consumption-lineitems.md) ve [Fatura için faturalandırılan tüketim satırı öğelerini](get-invoice-billed-consumption-lineitems.md) al makalelerine bakın. Bu makalelerde, kaynak başına ölçüm başına her gün bir derecelendirmeden derecelendirilen tüketimin nasıl alınacağı açıklanır. Bu hız tüketimi, Azure kullanım API 'SI tarafından belirtilen günlük gren verilere eşdeğerdir. Fatura tanımlayıcısını, faturalandırılan kullanım verilerini almak için kullanmanız gerekir. Ya da, faturalandırılmamış kullanım tahminleri almak için geçerli ve önceki dönemleri de kullanabilirsiniz. *Saatlik gren veri ve rastgele tarih aralığı filtreleri şu anda Azure plan aboneliği kaynakları için desteklenmiyor*.

## <a name="azure-utilization-api"></a>Azure kullanım API 'SI

Bu Azure kullanım API 'SI, kullanımın faturalandırma sisteminde ne zaman raporlanacağı temsil eden bir döneme ait kullanım kayıtlarına erişim sağlar. Bu, mutabakat dosyası oluşturmak ve hesaplamak için kullanılan kullanım verilerine erişim sağlar. Ancak fatura sistem mutabakatı dosya mantığı hakkında bilgi sahibi değildir. Aynı zaman dilimi için bu API 'den alınan sonuçla eşleşen dosya Özeti sonuçlarının mutabakatını beklememelisiniz.

Örneğin, faturalandırma sistemi aynı kullanım verilerini alır ve bir mutabakat dosyasında nelerin hesaba katılmaz belirlemek için değer kuralları uygular. Bir faturalandırma dönemi kapandığında, fatura döneminin sona ereceği günün sonuna kadar tüm kullanımlar mutabakat dosyasına dahil edilir. Fatura dönemi bittikten sonra 24 saat içinde raporlanan ödeme dönemi içinde herhangi bir geç kullanım, bir sonraki mutabakat dosyasında hesaba katılmaz. Ortağın faturalandırılma şekli için bkz. [Azure aboneliği için tüketim verilerini alma](/previous-versions/azure/reference/mt219001(v=azure.100)).

Bu REST API disk belleğine alınmış. Yanıt yükü tek bir sayfadan fazlaysa, kullanım kayıtlarının sonraki sayfasını almak için sonraki bağlantıyı izlemeniz gerekir.

### <a name="scenario-partner-a-has-transferred-billing-ownership-of-azure-legacy-subscription-145p-to-partner-b"></a>Senaryo: Iş ortağı A, Azure eski aboneliğinin (145P) faturalama sahipliğini B ortağına aktardı

Bir iş ortağı, Azure eski aboneliğinin faturalandırma sahipliğini başka bir ortağa aktarıyorsa yeni iş ortağı aktarılan abonelik için kullanım API 'sini çağırdığında, Azure Yetkilendirme KIMLIĞI yerine ticari abonelik KIMLIĞI (Iş Ortağı Merkezi hesabında gösterilir) kullanmaları gerekir. Azure Yetkilendirme KIMLIĞI, Iş ortağı B yalnızca müşterinin Azure portal (AOBO) adına yönetici olduklarında görüntülenir. 

Aktarılan abonelik için kullanım API 'sini başarılı bir şekilde çağırmak için, yeni iş ortağının ticaret abonelik KIMLIĞINI kullanması gerekir.

## <a name="c"></a>C\#

Azure kullanım kayıtlarını almak için:

1. Müşteri KIMLIĞINI ve abonelik KIMLIĞINI alın.

2. Kullanım kayıtlarını içeren bir [**Resourcecollection**](/dotnet/api/microsoft.store.partnercenter.models.resourcecollection-1) döndürmek için [**IAzureUtilizationCollection. Query**](/dotnet/api/microsoft.store.partnercenter.utilization.iazureutilizationcollection.query) yöntemini çağırın.

3. Kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı elde edin. Kaynak koleksiyonu disk belleğine alındığından bu adım gereklidir.

- **Örnek**: [konsol test uygulaması](console-test-app.md)
- **Project**: iş ortağı merkezi SDK örnekleri
- **Sınıf**: GetAzureSubscriptionUtilization. cs

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

IPartner partner = PartnerService.Instance.CreatePartnerOperations(credentials);

// Retrieve the utilization records for the last year in pages of 100 records.
var utilizationRecords = partner.Customers[customerId].Subscriptions[subscriptionId].Utilization.Azure.Query(
    DateTimeOffset.Now.AddYears(-1),
    DateTimeOffset.Now,
    size: 100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages.
var utilizationRecordEnumerator = partner.Enumerators.Utilization.Azure.Create(utilizationRecords);

while (utilizationRecordEnumerator.HasValue)
{
    //
    // Insert code here to work with this page.
    //

    // Get the next page.
    utilizationRecordEnumerator.Next();
}
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır. Daha sonra, kullanım kayıtlarını içeren bir **Resourcecollection** döndürmek için **IAzureUtilizationCollection. Query** işlevini çağırabilirsiniz. Kaynak koleksiyonu disk belleğine alındığından, kullanım sayfalarında geçiş yapmak için bir Azure kullanım kaydı numaralandırıcısı edinmeniz gerekir.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;

ResourceCollection<AzureUtilizationRecord> utilizationRecords = partnerOperations.getCustomers()
  .byId(customerId).getSubscriptions().byId(subscriptionId)
  .getUtilization().getAzure().query(
      new DateTime().minusYears(1),
      new DateTime(),
      AzureUtilizationGranularity.Daily,
      true,
      100);

// Create an Azure utilization enumerator which will aid us in traversing the utilization pages
IResourceCollectionEnumerator<ResourceCollection<AzureUtilizationRecord>> utilizationRecordEnumerator =
    partnerOperations.getEnumerators().getUtilization().getAzure().create(utilizationRecords);

while (utilizationRecordEnumerator.hasValue())
{
    //
    // Insert code here to work with this page.
    //

    // get the next page
    utilizationRecordEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Azure kullanım kayıtlarını almak için öncelikle bir müşteri tanımlayıcısına ve bir abonelik tanımlayıcısına ihtiyacınız vardır. Daha sonra [**Get-Partnercustomersubscriptionkullanımı**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscriptionUtilization.md)' nı çağırabilirsiniz. Bu komut, belirtilen süre boyunca kullanılabilir olan tüm kayıtları döndürür.

```powershell
# $customerId
# $subscriptionId

Get-PartnerCustomerSubscriptionUtilization -CustomerId $customerId -SubscriptionId $subscriptionId -StartDate (Get-Date).AddDays(-2).ToUniversalTime() -Granularity Hourly -ShowDetails
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si |
|------- | ----------- |
| **Al** | *{BaseUrl}*/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-id}/gurzations/Azure? başlangıç \_ zamanı = {başlangıç zamanı} &bitiş \_ zamanı = {bitiş zamanı} &ayrıntı düzeyi = {ayrıntı düzeyi} &\_ Ayrıntıları göster = {true} |

#### <a name="uri-parameters"></a>URI parametreleri

Kullanım kayıtlarını almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad | Tür | Gerekli | Açıklama |
| ---- | ---- | -------- | ----------- |
| Müşteri-Kiracı kimliği | string | Yes | Müşteriyi tanımlayan GUID biçimli bir dize. |
| abonelik kimliği | string | Yes | Aboneliği tanımlayan GUID biçimli bir dize. |
| start_time | UTC Tarih-saat fark biçiminde dize | Yes | Kullanım faturalandırma sisteminde ne zaman bildirileceğini temsil eden zaman aralığının başlangıcı. |
| end_time | UTC Tarih-saat fark biçiminde dize | Yes | Kullanım faturalandırma sisteminde bildirilme zamanını temsil eden zaman aralığının sonu. |
| boyutu | dize | No | Kullanım toplamalarının ayrıntı düzeyini tanımlar. Kullanılabilir seçenekler şunlardır: `daily` (varsayılan) ve `hourly` .
| show_details | boolean | Hayır | Örnek düzeyinde kullanım ayrıntılarının kullanılıp kullanılmayacağını belirtir. Varsayılan değer: `true`. |
| boyut | sayı | Hayır | Tek bir API çağrısıyla döndürülen toplama sayısını belirtir. Varsayılan değer 1000’dir. Maksimum değer 1000 ' dir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

Aşağıdaki örnek istek, karşılaştırma dosyasının 7/2-8/1 dönemi için göstereceği şeydir benzer sonuçlar üretir. Bu sonuçlar, tam olarak eşleşmeyebilir (Ayrıntılar için bkz. [Azure kullanım API 'si](#azure-utilization-api) ).

Bu örnek istek, faturalama sisteminde 7/2 (UTC) ve 8/2 (UTC) ile arasında raporlanan kullanım verilerini döndürür.

```http
GET https://api.partnercenter.microsoft.com/v1/customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-07-02T00:00:00-08:00&end_time=2017-08-02T00:00:00-08:00 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde [Azure kullanım kaydı](azure-utilization-record-resources.md) kaynaklarının bir koleksiyonunu döndürür. Azure kullanım verileri henüz bağımlı bir sistemde kullanıma yoksa, bu yöntem Retry-After bir üst bilgiyle 204 HTTP durum kodunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. HTTP durum kodunu, [hata kodu türünü](error-codes.md)ve ek parametreleri okumak için bir ağ izleme aracı kullanın.

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 2630
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: PjuGoYrw806o6A3Y.0
MS-ServerId: 030020525
Date: Fri, 04 Aug 2017 23:48:28 GMT

{
  "totalCount": 2,
  "items": [
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        }
      },
      "attributes": {
        "objectType": "AzureUtilizationRecord"
      }
    },
    {
      "usageStartTime": "2017-06-07T17:00:00-07:00",
      "usageEndTime": "2017-06-08T17:00:00-07:00",
      "resource": {
        "id": "8767aeb3-6909-4db2-9927-3f51e9a9085e",
        "name": "Storage Admin",
        "category": "Storage",
        "subcategory": "Block Blob",
        "region": "Azure Stack"
      },
      "quantity": 0.217790327034891,
      "unit": "1 GB/Hr",
      "infoFields": {},
      "instanceData": {
        "resourceUri": "/subscriptions/ab7e2384-eeee-489a-a14f-1eb41ddd261d/resourcegroups/system.local/providers/Microsoft.Storage/storageaccounts/srphealthaccount",
        "location": "azurestack",
        "partNumber": "",
        "orderNumber": "",
        "additionalInfo": {
          "azureStack.MeterId": "09F8879E-87E9-4305-A572-4B7BE209F857",
          "azureStack.SubscriptionId": "dbd1aa30-e40d-4436-b465-3a8bc11df027",
          "azureStack.Location": "local",
          "azureStack.EventDateTime": "06/05/2017 06:00:00"
        },
        "attributes": {
          "objectType": "AzureUtilizationRecord"
        }
      },

      "links": {
        "self": {
          "uri": "customers/E499C962-9218-4DBA-8B83-8ADC94F47B9F/subscriptions/FC8F8908-F918-4406-AF13-D5BC0FE41865/utilizations/azure?start_time=2017-06-10T00:00:00Z&end_time=2017-07-09T00:00:00Z&granularity=Daily&show_details=True&size=1000",
          "method": "GET",
          "headers": []
        }
      },
      "attributes": {
        "objectType": "Collection"
      }
    }
  ]
}
```
