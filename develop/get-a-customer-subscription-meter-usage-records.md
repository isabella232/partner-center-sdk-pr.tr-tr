---
title: Ölçüme göre abonelik için kullanım verilerini alma
description: Geçerli faturalandırma döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak üzere MeterUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2d2f13c9f944a0a5297c61c70606517c4426957f86066fe4469a7543b14d3bf9
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992832"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>Ölçüme göre abonelik için kullanım verilerini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Geçerli faturalandırma döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak üzere **MeterUsageRecord** kaynak koleksiyonunu kullanabilirsiniz. Bu kaynak koleksiyonu, tüm Azure planınız genelinde geçerli faturalandırma döngüsünün her bir ölçümü için toplam toplu toplamı temsil eder.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik KIMLIĞI

*bu yeni yol ile eşdeğerdir `subscriptions/{subscription-id}/usagerecords/resources` , ancak yalnızca Microsoft Azure (MS-azr-0145p) abonelikleri için çalışmaya devam edecektir.* bu yeni rota hem Microsoft Azure (MS-azr-0145p) aboneliklerini ve Azure planlarını destekleyecektir. Azure planınızla ilgili bu bilgileri almak için bu yeni yola geçmeniz gerekir. Aşağıdaki bölümlerde bahsedilen özellikler dışında, yanıt eski rotayla aynıdır.

## <a name="c"></a>C\#

Geçerli faturalandırma döneminde belirli bir Azure hizmeti veya kaynağı için bir müşterinin ölçüm kullanım kayıtlarını almak için:

1. **Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.

2. Abonelikler özelliğini ve **UsageRecords** ve ardından **ölçümler özelliğini çağırın** . Get () veya GetAsync () yöntemlerini çağırarak son ' a erişin.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

Bir örnek için aşağıdaki örneğe bakın:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Project: **partnersdk. featuresamples**
- Sınıf: **GetSubscriptionUsageRecordsByMeter. cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Subscriptions/{Subscription-id}/meterusagerecords http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametreleri listelenmektedir.

| Ad                   | Tür     | Gerekli | Açıklama                               |
|------------------------|----------|----------|-------------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y        | Müşteriye karşılık gelen bir GUID.     |
| **abonelik kimliği**    | **guid** | Y        | bir Microsoft Azure (MS-azr-0145p) aboneliğini veya bir Azure planını temsil eden bir iş ortağı merkezi [abonelik kaynağının](subscription-resources.md#subscription)tanımlayıcısına karşılık gelen bir guıd. *Azure planı abonelik kaynakları için, bu rotada **abonelik kimliği** olarak **plan kimliği** sağlayın.* |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir **Pagedresourcecollection \<MeterUsageRecord>** kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-azr-0145p) abonelikleri için yanıt örneği

Bu örnekte, müşteri **145P Azure PayG** satın almıştır.

*Microsoft Azure (MS-azr-0145p) aboneliği olan müşteriler için, apı yanıtında hiçbir değişiklik olmaz.*

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a>Azure planına REST yanıtı örneği

Bu örnekte, müşteri bir Azure planı satın almış.

*Azure planlarına sahip müşteriler için API yanıtında aşağıdaki değişiklikler vardır:*

- **Currencylocale** , **CurrencyCode** ile değiştirilmiştir
- **Usdtotalcost** yeni bir alandır

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
