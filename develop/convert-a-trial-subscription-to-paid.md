---
title: Deneme aboneliğini ücretli aboneliğe dönüştürme
description: Deneme aboneliğini ücretli bir aboneliğe dönüştürmek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7cee9b9afddb12137bb66b57250a9487bd4902f5
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439336"
---
# <a name="convert-a-trial-subscription-to-paid-using-partner-center-apis"></a>Deneme aboneliğini Iş Ortağı Merkezi API 'Leri kullanarak ücretli olarak dönüştürme

> [!NOTE]
> Bu adımlar yeni ticaret ürünleri için geçerli değildir. Yeni ticaret deneme sürümlerini ücretli aboneliklere dönüştürmek için **Yeni bir ticari abonelik belgelerinin geçişine** bakın

Deneme aboneliğini ücretli olarak dönüştürebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Etkin deneme aboneliği için abonelik KIMLIĞI.

- Kullanılabilir bir dönüştürme teklifi.

## <a name="convert-a-trial-subscription-to-a-paid-subscription-through-code"></a>Kod aracılığıyla bir deneme aboneliğini ücretli aboneliğe dönüştürme

Deneme aboneliğini ücretli bir sürüme dönüştürmek için, önce kullanılabilir deneme dönüştürmelerinden oluşan bir koleksiyonu edinmeniz gerekir. Ardından, Satın almak istediğiniz dönüştürme teklifini seçmeniz gerekir.

Dönüştürme teklifleri, deneme aboneliğiyle aynı sayıda lisansla varsayılan olarak bir miktar belirtir. Bu miktarı, [**Miktar**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion.quantity) özelliğini satın almak istediğiniz lisansların sayısı olarak ayarlayarak değiştirebilirsiniz.

> [!NOTE]
> Satın alınan lisans sayısı ne olursa olsun, deneme sürümü abonelik KIMLIĞI satın alınan lisanslar için yeniden kullanılır. Sonuç olarak, etkin olan deneme kaybolur ve satın alma işlemi tarafından değiştirilmiştir.

Bir deneme aboneliğini kodla dönüştürmek için aşağıdaki adımları kullanın:

1. Kullanılabilir abonelik işlemlerine bir arabirim alın. Müşteriyi tanımlamalısınız ve deneme aboneliğinin abonelik tanımlayıcısını belirtmeniz gerekir.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2. Kullanılabilir dönüştürme tekliflerinin bir koleksiyonunu alın. Bu yöntem için istek/yanıt hakkında daha fazla bilgi ve Ayrıntılar için bkz. [deneme dönüştürme tekliflerinin bir listesini alın](get-a-list-of-trial-conversion-offers.md).

    ``` csharp
    var conversions = subscriptionOperations.Conversions.Get();
    ```

3. Bir dönüştürme teklifi seçin. Aşağıdaki kod, koleksiyondaki ilk dönüştürme teklifini seçer.

    ``` csharp
    var selectedConversion = conversions.Items.ToList()[0];
    ```

4. İsteğe bağlı olarak, satın alınabilecek lisansların sayısını belirtin. Varsayılan değer, deneme aboneliğindeki lisansların sayısıdır.

    ``` csharp
    selectedConversion.Quantity = 10;
    ```

5. Deneme aboneliğini ücretli olarak dönüştürmek için [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) yöntemini çağırın.

    ``` csharp
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
    ```

## <a name="c"></a>C\#

Deneme aboneliğini ücretli birine dönüştürmek için:

1. Müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.

2. Deneme aboneliği KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim alın. Yerel bir değişkende abonelik işlemleri arabirimine bir başvuru kaydedin.

3. Dönüşümlerde kullanılabilir işlemlere bir arabirim elde etmek için [**dönüşümler**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) özelliğini kullanın ve ardından kullanılabilir [**dönüştürme**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) tekliflerinin bir koleksiyonunu almak Için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) yöntemini çağırın. Birini seçmeniz gerekir. Aşağıdaki örnek varsayılan olarak kullanılabilir ilk dönüştürmeyi alır.

4. Dönüşümlerdeki kullanılabilir işlemlere bir arabirim elde etmek için yerel bir değişkende kaydettiğiniz abonelik işlemleri arabirimine yönelik başvuruyu ve [**dönüşümler**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) özelliğini kullanın.

5. Deneme dönüşümünü denemek için seçili dönüştürme teklifini nesnesini [**Create**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionupgradecollection.createasync) metoduna geçirin.

### <a name="c-example"></a>C \# örneği

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get subscription operations for the trial subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the available conversions.
var conversions = subscriptionOperations.Conversions.Get();

// If there are no conversions available, we&#39;re done.
// Otherwise, convert the trial to the first available conversion offer.
if (conversions.TotalCount <= 0)
{
    System.Console.WriteLine("This subscription has no conversions");
}
else
{
    // Default to the first conversion.
    var selectedConversion = conversions.Items.ToList()[0];

    // Convert the trial and return the result.
    var convertResult = subscriptionOperations.Conversions.Create(selectedConversion);
}
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **YAYINLA** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/dönüşümler http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşteri ve deneme aboneliğini belirlemek için aşağıdaki yol parametrelerini kullanın.

| Ad            | Tür   | Gerekli | Açıklama                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| müşteri kimliği     | string | Yes      | Müşteriyi tanımlayan GUID biçimli dize.           |
| abonelik kimliği | string | Yes      | Deneme aboneliğini tanımlayan GUID biçimli dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesine doldurulmuş bir [dönüştürme](conversions-resources.md#conversion) kaynağı eklenmelidir.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 234
Expect: 100-continue

{
    "OfferId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "TargetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "OrderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
    "Quantity": 25,
    "BillingCycle": "monthly",
    "Attributes": {
        "ObjectType": "Conversion"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [Conversionresult](conversions-resources.md#conversionresult) kaynağı içerir.

#### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

#### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 211
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: bd0cde7f-ba87-4010-8a73-1190b641f2a4
MS-CV: kW4GzmhvHEqCq1ls.0
MS-ServerId: 030020643
Date: Thu, 15 Jun 2017 23:10:40 GMT

 {
    "subscriptionId": "488745B5-2086-4912-802C-6ABB9F7C3638",
    "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
    "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "attributes": {
        "objectType": "ConversionResult"
    }
}
```
