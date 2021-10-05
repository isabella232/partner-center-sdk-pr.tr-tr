---
title: Yeni bir ticari abonelik geçişi alın
description: Yeni bir ticari abonelik geçişi edinme
ms.date: 10/04/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69c34f015d418437f080eb9d2f22a02c1f373b4f
ms.sourcegitcommit: 856b0baa4824960e13ee9672817a2d2e713fdf43
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/05/2021
ms.locfileid: "129528730"
---
#  <a name="get-a-new-commerce-subscription-migration"></a>Yeni bir ticari abonelik geçişi alın

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Geçiş durumunu denetlemek için bir aboneliğin yeni bir ticari deneyime geçişini alma

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Geçerli bir abonelik KIMLIĞI

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                           |
|---------|---------------------------------------------------------------------------------------------------------------------------------------|
| **AL** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Migrations/newcommerce/{Migration-id} http/1.1           |

### <a name="uri-parameter"></a>URI parametresi

Bu tabloda yeni bir ticari geçiş oluşturmak için gereken sorgu parametreleri listelenmektedir.

| Ad               | Tür   | Gerekli | Açıklama                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| Müşteri-Kiracı kimliği | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |
| geçiş kimliği       | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir [abonelik](subscription-resources.md) kaynakları koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-examples"></a>Yanıt örnekleri

```http
{
    "id": "d3a0ef43-a208-4c32-8b10-f15e99d4e782",
    "currentSubscriptionId": "9beb6319-6889-4d28-a155-68ca9c783842",
    "status": "Processing",
    "customerTenantId": "a836f6d8-1b17-44af-aaf1-1e5511c5d4e1",
    "partnerTenantId": "7828d7ba-f17b-45c3-a1ce-8b6c3e3a26c0",
    "catalogItemId": "CFQ7TTC0LF8S:0002:CFQ7TTC0KSVV",
    "subscriptionEndDate": "2022-09-06T00:00:00Z",
    "quantity": 1,
    "termDuration": "P1Y",
    "billingCycle": "Monthly"
}
```
