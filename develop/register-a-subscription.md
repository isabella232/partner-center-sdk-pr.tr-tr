---
title: Bir aboneliğe kaydolma
description: Azure rezervasyonlarını sipariş etmek için etkinleştirilmesi için mevcut bir aboneliği kaydetme.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d26a7c77f60e6ef817cde80b9e97c88bd8bdc786
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446624"
---
# <a name="register-a-subscription"></a>Bir aboneliğe kaydolma

Azure [rezervasyonlarını sipariş](subscription-resources.md) etmek için etkinleştirilmesi için mevcut bir Aboneliği kaydetme.

Azure rezervasyonu satın almak için en az bir CSP Azure aboneliğinizin olması gerekir. Bu yöntem, mevcut CSP Azure aboneliğinizi kaydederek Azure rezervasyonları satın almak için etkinleştirmenize olanak sağlar.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Abonelik kimliği.

## <a name="c"></a>C\#

Müşterinin aboneliğini kaydetmek için müşteri kimliğini kullanarak [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim alın. Ardından, kaydetmekte olduğunu aboneliği tanımlamak için [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemini abonelik kimliğiyle birlikte çağırabilirsiniz.

Son olarak, aboneliği kaydetmek ve abonelik kayıt durumunu almak için uri'yi almak için **Registration.Register()** yöntemini arayın. Daha fazla bilgi için [bkz. Abonelik kayıt durumunu alma.](get-subscription-registration-status.md)

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem    | İstek URI'si                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Yayınla**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad                    | Tür       | Gerekli | Açıklama                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| customer-id             | string     | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize.         |
| subscription-id         | string     | Yes      | Aboneliği tanımlayan GUID biçimli bir dize.     |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt, abonelik **kayıt durumunu** almak için URI'ye sahip bir Konum üst bilgisi içerir. Bu URI'yi diğer ilgili REST API'leriyle kullanmak üzere kaydedin. Durumu alma örneği için bkz. [Abonelik kayıt durumunu alma.](get-subscription-registration-status.md)

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
