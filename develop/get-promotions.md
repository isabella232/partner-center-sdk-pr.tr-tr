---
title: Bir segment ve Pazar için geçerli promosyonların bir listesini alır
description: Bir segment ve Pazar için geçerli promosyonların bir listesini alır.
ms.date: 09/24/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 0b9cc6ccdebbd641ab8b7dcd6cc5932c191d85ad
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716007"
---
# <a name="get-promotions"></a>Yükseltmeleri al

**Uygulama hedefi**

- İş Ortağı Merkezi

**Uygun roller**

- Genel yönetici
- Yönetim Aracısı

> [!Note] 
> yeni ticaret değişiklikleri şu anda yalnızca Microsoft 365 ve Dynamics 365 yeni ticaret deneyimi technical preview sürümü olan iş ortakları tarafından kullanılabilir.

İş ortakları, belirli bir Pazar (ülke) ve segment için etkin yeni ticaret promosyonları listesini alabilir. Bu yöntem, geçerli promosyonları kullanılabilir başlangıç ve bitiş tarihlerine göre döndürür.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Segment, promosyonların etkinleştirildiği müşterinin türünü temsil eder. Şu anda yalnızca ticari destekleniyor.

- Ülke, için sunulan müşteri ülkesi promosyonları temsil eder. Ülke iki karakterli bir ülke koduyla temsil edilir.

## <a name="rest-request"></a>REST isteği
[GET]/v1/productpromosyonları? ülke = {Country-Code} &segment = {segment}

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **AL**  | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/productpromosyonları? ülke = {Country-code} &segment = {segment} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Kullanılabilir yükseltmeleri döndürmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                    | Tür     | Gerekli | Açıklama                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **deki**  | **string** | Y        | Belirli bir segment için hangi promosyonların kullanılabildiğini belirleyen bir dize.           |
| **ülke** | **string** | Y        | Hangi müşteri ülke promosyonları için kullanılabilir olduğunu belirleyen iki harfli ülke kodu. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/productpromotions?country=US&segment=commercial HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem promosyon listesini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt, başarı veya başarısızlık ve daha fazla hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve daha fazla parametreyi okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT


{
    "totalCount": 2,
    "items": [
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
        },
        {
            "id": "39NFJQT1PJQC:0001:39NFJQT1Q5KM",
            "name": "Vision Plan 1",
            "description": "Vision Plan 1",
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
                        "billingCycle": "Monthly"
                    },
                    "pricingPolicies": [
                        {
                            "policyType": "PercentDiscount",
                            "value": "0.167"
                        }
                    ]
                }
            ]
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
