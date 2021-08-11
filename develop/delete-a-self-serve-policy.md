---
title: Self Servis ilkesini silme
description: Self Servis ilkesini silme.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c638054e7d2b2eb6083c771bc6bdbee56af206907213c9b389176144d5230199
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995008"
---
# <a name="delete-a-selfservepolicy"></a>Bir SelfServePolicy silme

Bu makalede bir self servis ilkesinin nasıl güncelleştirilmesi açıklanmaktadır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="c"></a>C\#

Self Servis ilkesini silmek için:

1. İlkelerdeki işlemlere bir arabirim almak için, varlık tanımlayıcısıyla [**ıaggregatepartner. SelfServePolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metodunu çağırın.

2. Self Servis ilkesini silmek için [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) veya [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

Bir örnek için aşağıdakilere bakın:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Project: **partnersdk. featuresamples**
- Sınıf: **DeleteSelfServePolicies. cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                   |
|---------|-------------------------------------------------------------------------------|
| **SILMELI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} http/1.1 |

**URI parametresi**

Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.

| Ad                       | Tür         | Gerekli | Açıklama                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy kimliği**     | **string**   | Yes      | Self Servis ilkesini tanımlayan bir dize.                 |

### <a name="request-headers"></a>İstek üst bilgileri

- İstek KIMLIĞI ve bağıntı KIMLIĞI gereklidir.
- Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a>REST yanıtı

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
