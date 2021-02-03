---
title: Bir aboneliğe kaydolma
description: Mevcut bir aboneliği Azure ayırmalarını sıralamak için etkin olacak şekilde kaydettirin.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769652"
---
# <a name="register-a-subscription"></a>Bir aboneliğe kaydolma

**Uygulama hedefi**

- İş Ortağı Merkezi

Mevcut bir [aboneliği](subscription-resources.md) Azure ayırmalarını sıralamak için etkin olacak şekilde kaydettirin.

Bir Azure ayırması satın almak için, en az bir tane mevcut CSP Azure aboneliğiniz olması gerekir. Bu yöntem, mevcut CSP Azure aboneliğinizi kaydetmenizi sağlar ve bunu Azure ayırmaları satın almak üzere etkinleştirir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik KIMLIĞI.

## <a name="c"></a>C\#

Müşterinin aboneliğini kaydetmek için, müşteriyi tanımlamak üzere [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) YÖNTEMINI Müşteri kimliğiyle çağırarak abonelik işlemlerine bir arabirim alın. Ardından, kaydolduğunuz aboneliği tanımlamak için abonelik KIMLIĞIYLE birlikte [**Subscription. Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemini çağırın.

Son olarak, aboneliği kaydetmek ve abonelik kayıt durumunu almak için kullanılabilecek bir URI almak için **kayıt. Register ()** yöntemini çağırın. Daha fazla bilgi için bkz. [abonelik kayıt durumunu Al](get-subscription-registration-status.md).

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem    | İstek URI'si                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Yayınla**  | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/kayıtlar http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad                    | Tür       | Gerekli | Açıklama                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| müşteri kimliği             | string     | Yes      | Müşteriyi tanımlayan GUID biçimli dize.         |
| abonelik kimliği         | string     | Yes      | Aboneliği tanımlayan GUID biçimli dize.     |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

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

Başarılı olursa, yanıt, abonelik kayıt durumunu almak için kullanılabilecek bir URI içeren bir **konum** üst bilgisi içerir. Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin. Durumu alma hakkında bir örnek için bkz. [abonelik kayıt durumunu alma](get-subscription-registration-status.md).

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

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
