---
title: Müşteri lisans dağıtım bilgilerini alma
description: Belirli bir müşteri için lisans dağıtımı öngörülerini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 83a27b49054f0cb33531dfd8a028ab2d3d4d7bee23be4e99c45a0b383880c5d4
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992526"
---
# <a name="get-customer-licenses-deployment-information"></a>Müşteri lisans dağıtım bilgilerini alma

Belirli bir müşteri için lisans dağıtımı öngörülerini alma.

> [!NOTE]
> Bu senaryo, [lisans dağıtımı bilgilerini alır](get-licenses-deployment-information.md).

## <a name="prerequisites"></a>Önkoşullar

[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="c"></a>C\#

Belirtilen bir müşteri için dağıtımda toplanan verileri almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından [**analiz**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) özelliğinden müşteri düzeyi Analizi toplama işlemlerine yönelik bir arabirim alın. Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) özelliğinden müşteri düzeyi lisans Analizi koleksiyonuna bir arabirim alın. Son olarak, lisans dağıtımında toplanan verileri almak için [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırın. Yöntem başarılı olursa [**Customerlicensesdeploymenınsıghts**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) nesnelerinin bir koleksiyonunu alırsınız.

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Analtics/licenses/Deployment http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad        | Tür | Gerekli | Açıklama                                                |
|-------------|------|----------|------------------------------------------------------------|
| müşteri kimliği | guid | Yes      | Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi, dağıtılan lisanslar hakkında bilgi sağlayan bir [Customerlicensesdeploymentinsıghts](analytics-resources.md#customerlicensesdeploymentinsights) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1012
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CV: deEp2Wy6DUitMCYA.0
MS-ServerId: 102030524
Date: Wed, 15 Mar 2017 01:19:18 GMT

{
    "totalCount": 3,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 1,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 5,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 2,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
