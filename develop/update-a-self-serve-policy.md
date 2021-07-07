---
title: Self Servis ilkesini güncelleştirme
description: Self Servis ilkesini güncelleştirme.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d94382e73fd2a79751fe5f8f8414df2befde584f
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445264"
---
# <a name="update-a-selfservepolicy"></a>SelfServePolicy güncelleştirme

Bu makalede bir self servis ilkesinin nasıl güncelleştirilmesi açıklanmaktadır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="c"></a>C\#

Self Servis ilkesini silmek için:

1. İlkelerdeki işlemlere bir arabirim almak için, varlık tanımlayıcısıyla [**ıaggregatepartner. SelfServePolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metodunu çağırın.

2. Self Servis ilkesini güncelleştirmek için [**PUT**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) veya [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) metodunu çağırın.

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                       |
|----------|-------------------------------------------------------------------|
| **PUT** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

- İstek tanımlayıcısı ve bağıntı tanımlayıcısı gereklidir.
- Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.

| Ad                              | Tür   | Açıklama                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy)| object | Self Servis ilke bilgileri. |

#### <a name="selfservepolicy"></a>SelfServePolicy

Bu tabloda, yeni bir self servis ilkesi oluşturmak için gereken [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağından gerekli en düşük alan açıklanmaktadır.

| Özellik              | Tür             | Açıklama                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan kendi kendine bir ilke tanımlayıcısı.     |
| SelfServeEntity       | SelfServeEntity  | Erişim izni verilen self servis varlığı.                                                     |
| Verenin Grant izni               | Verenin Grant izni          | Erişim veren granör.                                                                    |
| İzinler           | Izin dizisi| [İzin](self-serve-policy-resources.md#permission) kaynakları dizisi.                                                      |
| Özelliği                  | string           | ETag.                                                                                               |


### <a name="request-example"></a>İstek örneği

```http
PUT https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive

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

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu API güncelleştirilmiş self servis ilkesi için bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP durum kodu     | Hata kodu   | Açıklama                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 600039       | Self Servis ilkesi bulunamadı                                            |
| 404                  | 600040       | Self Servis ilke tanımlayıcısı yanlış                                  |


### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 Ok
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

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
        "etag": "\"1ec98034-a249-46f4-b9dd-9cd464fb5e47\"",
        "objectType": "SelfServePolicy"
    }
}
```
