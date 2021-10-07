---
title: Geçiş için aboneliği doğrulama
description: Bir aboneliğin geçiş için uygun olup olduğunu doğrulama.
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d085093b8adc3750d1b8d95963fc9d74c4209e00
ms.sourcegitcommit: 53980dc43fb2277878bf61a15a86013b8b1c2574
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/06/2021
ms.locfileid: "129610005"
---
# <a name="validate-a-subscription-for-migration"></a>Geçiş için aboneliği doğrulama

**Için geçerlidir:** İş Ortağı Merkezi | 21Vianet İş Ortağı Merkezi tarafından çalıştırılan | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Yeni Ticaret Deneyimi'ne geçiş için aboneliği doğrulama

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bunu panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi menüsünden **CSP'yi** ve ardından Müşteriler'i **seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Geçerli abonelik kimliği

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
|**YAYINLA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/migrations/newcommerce/validate HTTP/1.1  |

### <a name="uri-parameter"></a>URI parametresi

Bu tabloda, geçiş için bir aboneliği doğrulamak için gerekli sorgu parametreleri listeleniyor.

| Ad               | Tür   | Gerekli | Açıklama                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| customer-tenant-id | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek [gövdesinin](subscription-resources.md) Abonelik özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| currentSubscriptionId | string           | Yes             | Hangi aboneliğin geçiş için doğrulama gerektirdiğini gösteren bir abonelik tanımlayıcısı.            |

### <a name="request-example"></a>İstek örneği

```http
"currentSubscriptionId" : "9beb6319-6889-4d28-a155-68ca9c783842"
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde geçerli aboneliğin yeni ticarete geçiş için uygun olup olmadığını belirten bir "isEligible" boole döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
```

```http
2. 
    {
        "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
        "isEligible": true,
        "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV"
    }
```
