---
title: Ölçüme göre abonelik için kullanım verilerini alma
description: Geçerli faturalama döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak için MeterUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0bd6143c80059bd140a4c4332ab4ec19c54d99f1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874865"
---
# <a name="get-usage-data-for-subscription-by-meter"></a>Ölçüme göre abonelik için kullanım verilerini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Geçerli faturalama döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak için **MeterUsageRecord** kaynak koleksiyonunu kullanabilirsiniz. Bu kaynak koleksiyonu, Tüm Azure planınız genelinde geçerli faturalama dönemi için her ölçüm için toplu bir toplamı temsil eder.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Abonelik kimliği

*Bu yeni yol, yalnızca Microsoft Azure (MS-AZR-0145P) abonelikleri için çalışmaya devam edecek olan ile `subscriptions/{subscription-id}/usagerecords/resources` eşdeğerdir.* Bu yeni yol hem Microsoft Azure (MS-AZR-0145P) aboneliklerini hem de Azure planlarını destekleyecektir. Azure planınıza ilişkin bu bilgileri almak için bu yeni rotaya geçmeniz gerekir. Aşağıdaki bölümlerde belirtilen özellikler dışında, yanıt eski yol ile aynıdır.

## <a name="c"></a>C\#

Geçerli faturalama döneminde belirli bir Azure hizmetine veya kaynağına yönelik müşterinin ölçüm kullanım kayıtlarını almak için:

1. **ById()** **yöntemini çağırarak IAggregatePartner.Customers** koleksiyonu kullanın.

2. Subscriptions özelliğini ve **UsageRecords'ı** ve ardından **Meters özelliğini** çağırma. Get() veya GetAsync() yöntemlerini çağırarak son.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

Bir örnek için aşağıdaki örneğine bakın:

- Örnek: [Konsol test uygulaması](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Sınıf: **GetSubscriptionUsageRecordsByMeter.cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Bu tabloda müşterinin derecelendirilmiş kullanım bilgilerini almak için gereken sorgu parametreleri listelemektedir.

| Ad                   | Tür     | Gerekli | Açıklama                               |
|------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Müşteriye karşılık gelen bir GUID.     |
| **subscription-id**    | **guid** | Y        | Microsoft Azure (MS-AZR-0145P) aboneliğini veya bir Azure planını temsil eden bir İş Ortağı Merkezi aboneliği kaynağının tanımlayıcısına karşılık gelen GUID. [](subscription-resources.md#subscription) *Azure planı abonelik kaynakları için bu yolda **subscription-id** olarak **plan-id** girin.* |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, bu yöntem yanıt **gövdesinde \<MeterUsageRecord> bir PagedResourceCollection** kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-AZR-0145P) abonelikleri için yanıt örneği

Bu örnekte müşteri **145P Azure PayG satın alır.**

*Microsoft Azure (MS-AZR-0145P) aboneliğine sahip müşteriler için API yanıtta değişiklik olmaz.*

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

## <a name="rest-response-example-for-azure-plan"></a>Azure planı için REST yanıtı örneği

Bu örnekte müşteri bir Azure planı satın alır.

*Azure planları olan müşteriler için API yanıtta aşağıdaki değişiklikler vardır:*

- **currencyLocale,** **currencyCode ile değiştirildi**
- **usdTotalCost** yeni bir alandır

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
