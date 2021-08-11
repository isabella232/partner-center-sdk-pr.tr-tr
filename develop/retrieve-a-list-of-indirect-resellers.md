---
title: Dolaylı satıcıların bir listesini alma
description: Oturum açmış iş ortağının dolaylı kurumsal bayilerinin listesini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 901bf045d1de29744114bb58ed445f9eb17f70a4744786fd4617da9697e7c683
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996929"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Dolaylı satıcıların bir listesini alma

Oturum açmış iş ortağının dolaylı kurumsal bayilerinin listesini alma.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="c"></a>C\#

Oturum açmış olan iş ortağının ilişkisi olan dolaylı kurumsal bayilerin listesini almak için ilk olarak [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) özelliğinden ilişki toplama işlemlerine yönelik bir arabirim alın. Ardından, [**ilişki türünü**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) tanımlamak için [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) numaralarının bir üyesini geçerek Get veya [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) yöntemini çağırın. Dolaylı kurumsal bayileri almak için IsIndirectCloudSolutionProviderOf kullansanız gerekir.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md)**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** GetIndirectResellers.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship \_ type=IsIndirectCloudSolutionProviderOf HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İlişki türünü tanımlamak için aşağıdaki sorgu parametresini kullanın.

| Ad               | Tür    | Gerekli  | Açıklama                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | string  | Yes       | değeri, [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)içinde bulunan üye adlarından birinin dize gösterimidir.<br/><br/> İş ortağı sağlayıcı olarak oturum açmışsa ve ilişki kurduğu dolaylı kurumsal bayilerin listesini almak için IsIndirectCloudSolutionProviderOf kullanın.<br/><br/> İş ortağı kurumsal bayi olarak oturum açmışsa ve ilişki kuracakları dolaylı sağlayıcıların listesini almak için IsIndirectResellerOf kullanın.    |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi kurumsal bayileri tanımlamak için [bir PartnerRelationship](relationships-resources.md) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 298
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CV: b21Ll1miM0yFMPQQ.0
MS-ServerId: 030020643
Date: Wed, 05 Apr 2017 21:08:44 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847383",
            "location": "US",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }, {
            "id": "b01b1487-b36e-4e6d-9b5e-0b58974c4b28",
            "name": "ReleCloud",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "state": "Active",
            "mpnId": "4847433",
            "location": "BR",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```