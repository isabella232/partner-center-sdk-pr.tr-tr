---
title: İlişki isteği URL’sini alma
description: Bir müşteriye göndermek için bir ilişki isteği URL 'SI alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 07804b36dfe0892cf8b531e0731188260c014f49
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547470"
---
# <a name="retrieve-a-relationship-request-url"></a>İlişki isteği URL’sini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi

Bir müşteriye göndermek için bir ilişki isteği URL 'SI alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

İlişki isteği URL 'sini almak için, önce iş ortağının müşteri işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ' ı kullanın. Ardından, bir Kullanıcı ilişki isteği işlemlerine bir arabirim almak için [**Relationshiprequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) özelliğini kullanın. Son olarak, URL 'YI almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getcustomerrelationshiprequest. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                            |
|---------|----------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/relationshiprequests http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt [Relationshiprequest](relationships-resources.md#relationshiprequest) nesnesini içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
