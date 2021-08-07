---
title: KIMLIĞE göre Self Servis İlkesi al
description: Belirtilen self servis ilkesini KIMLIĞINI kullanarak alır.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 7ad763dd6d586a58b73d0a3abb2b2fc399a0f35e7b842f5d1dd2e4c5006c3b30
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989755"
---
# <a name="get-a-self-serve-policy-by-id"></a>KIMLIĞE göre Self Servis İlkesi al

Belirtilen self servis ilkesini KIMLIĞINI kullanarak alır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
- Self Servis ilke KIMLIĞI.

## <a name="examples"></a>Örnekler


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Isteği

**İstek sözdizimi**

| Yöntem  | İstek URI'si                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} http/1.1 |

**URI parametresi**

Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.

| Ad                       | Tür         | Gerekli | Açıklama                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy kimliği**     | **string**   | Yes      | Self Servis ilkesini tanımlayan bir dize.                 |

**İstek üst bilgileri**

- Daha fazla bilgi için bkz. [üstbilgiler](headers.md).

**İstek gövdesi**

Yok.

**İstek örneği**

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağı içerir.

**Yanıt başarısı ve hata kodları**

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP durum kodu     | Hata kodu   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Self Servis ilkesi bulunamadı.                                                     |

**Yanıt örneği**

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415",
    "selfServeEntity": {
        "selfServeEntityType": "customer",
        "tenantID": "0431a72c-7d8a-4393-b25e-ef63f5efb415"
    },
    "grantor": {
        "grantorType": "billToPartner",
        "tenantID": "634f6379-ad54-449b-9821-564f737158ab"
    },
    "permissions": [{
        "resource": "AzureReservedInstances",
        "action": "Purchase"
    }],
    "attributes": {
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```