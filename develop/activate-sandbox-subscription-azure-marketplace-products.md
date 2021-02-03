---
title: Ticari Market ürünleri için bir korumalı alan aboneliğini etkinleştirin
description: Ticari Market ürünleri için bir korumalı alan aboneliğini etkinleştirmek üzere C/# ve Iş Ortağı Merkezi REST API 'Lerini nasıl kullanacağınızı öğrenin.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a78b2c84368b29f1378f46971c4814929094e299
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769952"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Faturalandırmayı etkinleştirmek için ticari Market SaaS ürünleri için bir korumalı alan aboneliği etkinleştirin

**Uygulama hedefi:**

- İş Ortağı Merkezi

Faturalandırmayı etkinleştirmek için tümleştirme korumalı alanı hesaplarından hizmet olarak satılan ticari Market yazılım (SaaS) ürünleri için bir abonelik etkinleştirme.

> [!NOTE]
> Yalnızca tümleştirme korumalı alanı hesaplarından ticari Market SaaS ürünleri için bir abonelik etkinleştirmek mümkündür. Üretim aboneliğiniz varsa, kurulum işlemini gerçekleştirmek için yayımcının sitesini ziyaret etmeniz gerekir. Abonelik faturalandırması, yalnızca kurulum tamamlandıktan sonra başlayacaktır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Ticari Market SaaS ürünleri için etkin aboneliğe sahip bir müşterinin bulunduğu tümleştirme korumalı alan iş ortağı hesabı.

- Iş ortağı merkezi .NET SDK kullanan iş ortakları için, bu özelliğe erişmek için SDK sürüm 1.14.0 veya üstünü kullanmanız gerekir.

## <a name="c"></a>C\#

Ticari Market SaaS ürünleri için bir aboneliği etkinleştirmek üzere aşağıdaki adımları kullanın:

1. Kullanılabilir abonelik işlemlerine bir arabirim oluşturun. Müşteriyi tanımlamalısınız ve deneme aboneliğinin abonelik tanımlayıcısını belirtmeniz gerekir.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. **Etkinleştirme** işlemini kullanarak aboneliği etkinleştirin.

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem     | İstek URI'si                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-id}/Activate http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y | Değer, bir müşteri belirtmenize olanak tanıyan, GUID biçimli bir müşteri kiracı tanımlayıcısıdır (**Müşteri Kiracı kimliği**). |
| **abonelik kimliği** | **guid** | Y | Değer, bir abonelik belirtmenizi sağlayan GUID biçimli bir abonelik tanımlayıcısıdır (**abonelik kimliği**). |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/42b5f772-5c5c-4bce-b9d7-bdadeecca411/subscriptions/87363db7-39ab-dd25-d371-94340aaa2f97/activate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

```

## <a name="rest-response"></a>REST yanıtı

Bu yöntem, **abonelik kimliği** ve **durum** özelliklerini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 79
Content-Type: application/json
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "subscriptionId":"87363db7-39ab-dd25-d371-94340aaa2f97",
    "status":"Success"
}
```
