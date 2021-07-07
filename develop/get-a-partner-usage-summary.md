---
title: İş ortağı için Kullanım Özeti alın
description: Geçerli fatura döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin iş ortağı kullanım özetini almak için PartnerUsageSummary kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: f003980f1b521ad0ac26dbfd0d4821b9096fdd27
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873913"
---
# <a name="get-a-usage-summary-for-a-partner"></a>İş ortağı için Kullanım Özeti alın

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Geçerli fatura döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin iş ortağı kullanım özetini almak için **Partnerusagesummary** kaynağını kullanabilirsiniz.

*Bu API tarafından döndürülen toplam, bir Azure planına sahip müşteriler için tüketim getirmeyecektir.* Gelecekte kullanımdan kaldırılması planlanmaktadır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

Geçerli faturalandırma döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşteriler için Kullanım Özeti almak üzere:

1. **Iaggregatepartner**'nizi kullanın.

2. **Usagesummary** özelliğini çağırın, ardından **Get ()** veya **GetAsync ()** yöntemleri gelir:

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

Bir örnek için aşağıdakilere bakın:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Project: **partnersdk. featuresamples**
- Sınıf: **Getpartnerusagesummary. cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                         |
|---------|---------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/usagesummary http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir **Partnerusagesummary** kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```
