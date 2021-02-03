---
title: Abonelik kayıt durumunu alma
description: Azure ayrılmış VM örnekleri ile kullanılmak üzere kaydedilmiş bir aboneliğin durumunu alın.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769850"
---
# <a name="get-subscription-registration-status"></a>Abonelik kayıt durumunu alma

**Uygulama hedefi**

- İş Ortağı Merkezi

Azure ayrılmış VM örnekleri satın alma için etkinleştirilen bir müşteri aboneliğinin abonelik kayıt durumunu alma.

Iş Ortağı Merkezi API 'sini kullanarak bir Azure ayrılmış VM örneği satın almak için, en az bir tane mevcut CSP Azure aboneliğiniz olması gerekir. [Abonelik kaydetme](register-a-subscription.md) yöntemi, mevcut CSP Azure aboneliğinizi kaydetmenizi sağlar ve bunu Azure ayrılmış VM örnekleri satın almak üzere etkinleştirir. Bu yöntem, bu kaydın durumunu almanızı sağlar.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik KIMLIĞI.

## <a name="c"></a>C\#

Bir aboneliğin kayıt durumunu almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın. Ardından, aboneliği tanımlamak için abonelik KIMLIĞIYLE birlikte Subscription [**. Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemini çağırarak abonelik işlemlerine yönelik bir arabirim elde edin. Ardından, geçerli aboneliğin kayıt durumu işlemlerine bir arabirim almak için RegistrationStatus özelliğini kullanın ve **Subscriptionregistrationstatus** nesnesini almak için **Get** veya **GetAsync** yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem    | İstek URI'si                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| **Al**  | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/registrationstatus http/1.1 |

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
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
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

Başarılı olursa, yanıt gövdesi bir [Subscriptionregistrationstatus](subscription-resources.md#subscriptionregistrationstatus) kaynağı içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
