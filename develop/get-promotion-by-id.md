---
title: Tek bir yükseltme alır
description: Verilen bir yükseltme kimliği ve ülke için tek bir promosyon alır.
ms.date: 09/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 9ed9171cd7bbe8a6d5202deb7cc6111bb76ec923
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716014"
---
# <a name="get-promotion-by-id"></a>Kimlikle yükseltmeyi al

**Uygulandığı Yer**

- İş Ortağı Merkezi

**Uygun roller**

- Genel yönetici
- Yönetici aracısı

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca Microsoft 365 ve Dynamics 365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortakları tarafından kullanılabilir.

İş ortakları, verilen bir yükseltme kimliği ve ülke için tek bir promosyon elde ediyor olabilir. Bu yöntem, yükseltme başlangıç ve bitiş tarihlerini yoksayarak yükseltme verilerini döndürür. Bu yöntem, yükseltme süresi dolsa bile yükseltme ayrıntılarını almak için öncelikli olarak mutabakat amacıyla kullanılır.



## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Yükseltme Kimliği, belirli bir yükseltmeyi temsil eden sınırlandırılmış dize kümesidir.

- Ülke, müşterinin ülke promosyonlarını temsil eder. Ülke, iki karakterli bir ülke koduyla temsil edildi.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **AL**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/productpromotions/{promotion-id}?country={country-code HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Kullanılabilir yükseltmeleri geri dönmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                    | Tür     | Gerekli | Açıklama                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **promotion-id**  | **string** | Y        | Alınarak yükseltmeyi tanımlayan bir dize.           |
| **Ülke** | **string** | Y        | Hangi müşteri ülke promosyonlarının kullanılabilir olduğunu belirleyen iki harfli ülke kodu. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions/CFQ7TTC0HD33:0003:CFQ7TTC0K59M?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem tek bir yükseltme döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve daha fazla hata ayıklama bilgisi ile birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 24 Sep 2021 20:42:26 GMT

 
        {
            "id": "39NFJQT1PJQB:0001:39NFJQT1Q5KN",
            "name": "Visio Plan 1",
            "description": "Visio Plan 1",
            "startDate": "2021-09-23T00:00:00+00:00",
            "endDate": "2021-10-14T23:59:59+00:00",
            "properties": {
                "isAutoApplicable": true
            },
            "requiredProducts": [
                {
                    "productId": "CFQ7TTC0HD33",
                    "skuId": "0003",
                    "term": {
                        "duration": "P1Y",
                        "billingCycle": "Annual"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.05"
                        }
                    ]
                }
            ]
        }
```
