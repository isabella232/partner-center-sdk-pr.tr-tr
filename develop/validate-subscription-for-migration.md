---
title: Geçiş için bir abonelik doğrulama
description: Bir aboneliğin geçişe uygun olup olmadığını doğrulama.
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8d2ae596901a45a794230c79cfb54815963e300
ms.sourcegitcommit: 856b0baa4824960e13ee9672817a2d2e713fdf43
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/05/2021
ms.locfileid: "129528729"
---
# <a name="validate-a-subscription-for-migration"></a>Geçiş için bir abonelik doğrulama

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Yeni ticaret deneyimine geçiş için bir aboneliği doğrulama

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Geçerli bir abonelik KIMLIĞI

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
|**YAYINLA** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Migrations/newcommerce/Validate http/1.1  |

### <a name="uri-parameter"></a>URI parametresi

Bu tablo, geçiş için bir aboneliği doğrulamak üzere gerekli sorgu parametrelerini listeler.

| Ad               | Tür   | Gerekli | Açıklama                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| Müşteri-Kiracı kimliği | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde [abonelik](subscription-resources.md) özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| Currentsubscriptionıd | string           | Yes             | Hangi aboneliğin geçiş için doğrulama gerektirdiğini belirten bir abonelik tanımlayıcısı.            |

### <a name="request-example"></a>İstek örneği

```http
"currentSubscriptionId" : "9beb6319-6889-4d28-a155-68ca9c783842"
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde "ıdilinli" Boole değeri döndürür. Bu, geçerli aboneliğin yeni ticarete geçişe uygun olup olmadığını gösterir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-examples"></a>Yanıt örnekleri

```http
1. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": false,
        "errors": [
            {
                "code": 5,
                "description": "Subscription cannot be migrated to New Commerce because the equivalent offer is not yet available in New Commerce",
            }
        ]
    }

2. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": true,
    "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV",
    }
```
