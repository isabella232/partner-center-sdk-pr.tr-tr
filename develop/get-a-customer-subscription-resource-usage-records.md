---
title: Kaynağa göre abonelik için kullanım verilerini alma
description: ResourceUsageRecord kaynağını kullanarak müşterinin geçerli faturalama döneminde belirli Azure hizmetleri veya kaynaklarına yönelik kaynak kullanım kayıtlarını edinebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 81c8fcb868f7d4d50e23d69579138a6c03e9ea4ae93058d141a029c103489dcb
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992849"
---
# <a name="get-usage-data-for-subscription-by-resource"></a>Kaynağa göre abonelik için kullanım verilerini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu makalede **ResourceUsageRecord kaynağının nasıl elde edildikleri açıklanmıştır.** Bu kaynak, Azure planınıza sağlanan tek tek kaynaklar için ay için toplu bir toplamı temsil eder. Geçerli faturalama döneminde belirli Azure hizmetlerinin veya kaynaklarının müşteri kaynak kullanım kayıtlarını almak için bu kaynağı kullanabilirsiniz. Bu API, daha önce Azure harcama API'leri aracılığıyla kullanılabilir durumda olan verileri döndürür.

*Bu yol, Microsoft Azure (MS-AZR-0145P) aboneliklerini desteklemez.*

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Abonelik tanımlayıcısı

## <a name="c"></a>C\#

Geçerli faturalama döneminde belirli bir Azure hizmetine veya kaynağına yönelik bir müşterinin kaynak kullanım kayıtlarını almak için:

1. **ById()** **yöntemini çağırarak IAggregatePartner.Customers** koleksiyonu kullanın.

2. Subscriptions özelliğini ve **UsageRecords'ı** ve ardından **Resources özelliğini** çağırma. Get() veya GetAsync() yöntemlerini çağırarak son.

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

Bir örnek için aşağıdakilere bakın:

- Örnek: [Konsol test uygulaması](console-test-app.md)
- Project: **PartnerSDK.FeatureSamples**
- Sınıf: **GetSubscriptionUsageRecordsByResource.cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt **gövdesinde \<ResourceUsageRecord> bir PagedResourceCollection** kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
