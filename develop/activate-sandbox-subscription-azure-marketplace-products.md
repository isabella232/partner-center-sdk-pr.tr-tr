---
title: Ticari market ürünleri için korumalı alan aboneliğini etkinleştirme
description: Ticari market ürünleri için korumalı alan aboneliğini etkinleştirmek İş Ortağı Merkezi C/# ve rest API'leri kullanmayı öğrenin.
ms.date: 09/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1ea581695e4328f02d08486c91b7b90a78e75a50985279d78cc54ef8b35fa715
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990503"
---
# <a name="activate-a-sandbox-subscription-for-commercial-marketplace-saas-products-to-enable-billing"></a>Faturalamayı etkinleştirmek için ticari market SaaS ürünleri için korumalı alan aboneliğini etkinleştirme

Faturalamayı etkinleştirmek için tümleştirme korumalı alan hesaplarından ticari market Hizmet Olarak Yazılım (SaaS) ürünleri için aboneliği etkinleştirme.

> [!NOTE]
> Ticari market SaaS ürünleri için aboneliği yalnızca tümleştirme korumalı alan hesaplarından etkinleştirmek mümkündür. Üretim aboneliğiniz varsa, kurulum işlemini tamamlamak için yayımcının sitesini ziyaret edin. Abonelik faturalaması ancak kurulum tamamlandıktan sonra başlar.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Ticari market SaaS ürünleri için etkin bir aboneliğe sahip olan bir müşteriyle tümleştirme korumalı alan iş ortağı hesabı.

- .NET SDK İş Ortağı Merkezi kullanan iş ortakları için bu özelliğe erişmek için SDK sürüm 1.14.0 veya daha yüksek bir sürümünü kullansanız gerekir.

## <a name="c"></a>C\#

Ticari market SaaS ürünleri için aboneliği etkinleştirmek üzere aşağıdaki adımları kullanın:

1. Abonelik işlemleri için bir arabirim kullanılabilir hale getirildi. Müşteriyi tanımlamanız ve deneme aboneliğinin abonelik tanımlayıcısını belirtmeniz gerekir.

   ```csharp
   var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
   ```

2. Etkinleştir işlemi kullanarak aboneliği **etkinleştirin.**

   ```csharp
   var subscriptionActivationResult = subscriptionOperations.Activate();
   ```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem     | İstek URI'si                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/activate HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y | Değer, müşteri belirtmenize olanak sağlayan GUID biçimli bir müşteri kiracı tanımlayıcısıdır (**customer-tenant-id).** |
| **subscription-id** | **guid** | Y | Değer, bir abonelik belirtmenize olanak sağlayan GUID biçimli bir abonelik tanımlayıcısıdır (**subscription-id).** |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Bu yöntem **subscription-id ve status** **özelliklerini** döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
