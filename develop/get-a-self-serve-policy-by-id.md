---
title: Kimlikle self servis ilkesi elde etme
description: Kimliğini kullanarak belirtilen self servis ilkesi alır.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 074d7ba65c7aab91687a67f50e871cee913fc2bb
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873845"
---
# <a name="get-a-self-serve-policy-by-id"></a>Kimlikle self servis ilkesi elde etme

Kimliğini kullanarak belirtilen self servis ilkesi alır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.
- Self servis ilke kimliği.

## <a name="examples"></a>Örnekler


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST İsteği

**İstek söz dizimi**

| Yöntem  | İstek URI'si                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1 |

**URI parametresi**

Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.

| Ad                       | Tür         | Gerekli | Açıklama                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| **SelfServePolicy-id**     | **string**   | Yes      | Self servis ilkesi tanımlayan bir dize.                 |

**İstek üst bilgileri**

- Daha fazla bilgi için [bkz. Üst Bilgiler.](headers.md)

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

Başarılı olursa, yanıt gövdesi bir [SelfServePolicy kaynağı](self-serve-policy-resources.md#selfservepolicy) içerir.

**Yanıt başarı ve hata kodları**

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP Durum Kodu     | Hata kodu   | Açıklama                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Self servis ilkesi bulunamadı.                                                     |

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