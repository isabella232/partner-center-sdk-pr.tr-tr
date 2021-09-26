---
title: Yükseltme uygunluğunu doğrulama
description: Müşteri işlemlerinin verilen promosyon için uygun olup olmadığını doğrular.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: ad3346ddca0438c0011e2c6fd03c3ec00b1a1fe3
ms.sourcegitcommit: 7be22de808a10fa2d05577d6497086c8ca3f678a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/24/2021
ms.locfileid: "128716008"
---
# <a name="verify-promotion-eligibility"></a>Yükseltme uygunluğunu doğrulama

**Uygulandığı Yer**

- İş Ortağı Merkezi

**Uygun roller**

- Genel yönetici
- Yönetici aracısı

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca Microsoft 365 ve Dynamics 365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortakları tarafından kullanılabilir.

Parters, müşteri işlemlerinin verilen promosyon için uygun olup olmadığını doğrular. Müşteri işlemi belirli bir yükseltme için uygunsa bu yöntem *True* döndürür. İş ortakları, yükseltmenin uygulandığını doğrulamak için bir işlem göndermeden önce uygunluğu doğrular.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Uygunluk, satın alınan ürün sku kullanılabilirliğini, değerlendirilen yükseltme kimliğini, miktarı, süreyi ve işlem faturalama döngüsünü içerir.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **YAYINLA**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/promotionEligibilities HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Kullanılabilir yükseltmeleri geri dönmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                    | Tür     | Gerekli | Açıklama                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Customerıd**  | **string** | Y        | Değer, müşteri belirtmenize olanak sağlayan bir tanımlayıcı olan GUID biçimli customer-tenant-id değeridir.          |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Gövde, PromotionEligibilitiesRequestItems koleksiyonu içerir. Bu tabloda Bir [PromotionEligibilitiesRequestItem için özellikler açıkmektedir.](promotion-resources.md#promotioneligibilitiesrequestitem)

| Özellik        | Tür             | Gerekli        | Açıklama                                                                                               |
|-----------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| catalogItemId   | string           | Yes             | Katalog öğesi tanımlayıcısı.                         |
| miktar        | int | Yes        | Lisans veya örnek sayısı.                 |
| termDuration    | DateTime         | Yes             | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler P1M (bir ay), P1Y (bir yıl) ve P3Y (üç yıl) değerleridir.   |
| billingCycle    | string | Yes     | Faturalama döngüsünün türünü gösteren değer.   |
| promotionId     | string           | Yes             | Yükseltme öğesi tanımlayıcısı.                       | 

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/46632f71-f052-4384-8f84-4cdb6c12c2a1/promotionEligibilities HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "promotionId": " CFQ7TTC0HL8W:0001:CFQ7TTC0K59M"
        }
    ]
}

```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem uygunluk sonuçlarının bir koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve daha fazla hata ayıklama bilgisi ile birlikte gelir. Bu kodu, hata türünü ve daha fazla parametreyi okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "totalCount": 1,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
            "quantity": 1,
            "termDuration": "P1Y",
            "billingCycle": "Monthly",
            "eligibilities": [
                {
                    "promotionId": "CFQ9TTC0HH4R:0001:CFQ8HGC0K77G",
                    "isEligible": false,
                    "errors": [
                        {
                            "type": "SeatCount",
                            "minRequiredSeats": 25,
                            "maxRequiredSeats": 500
                        },
                        {
                            "type": "Term",
                            "eligibleTerms": [
                                {
                                    "duration": "P3Y",
                                    "billingCycle": "Monthly"
                                }
                            ]
                        },
                        {
                            "type": "FirstPurchase"
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "PromotionEligibilities"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

