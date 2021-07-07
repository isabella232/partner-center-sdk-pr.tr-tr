---
title: Dolaylı satıcıların bir listesini alma
description: Oturum açmış ortağın dolaylı satıcıların listesini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 58f5c3378b5b941fdc9dafcf28f5efbc58c29c7c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446573"
---
# <a name="retrieve-a-list-of-indirect-resellers"></a>Dolaylı satıcıların bir listesini alma

Oturum açmış ortağın dolaylı satıcıların listesini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

Oturum açmış iş ortağının ilişkiye sahip olduğu dolaylı satıcıların bir listesini almak için, ilk olarak [**partneroperations. relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) özelliğinden ilişki toplama işlemlerine bir arabirim alın. Ardından, ilişki türünü tanımlamak için [**Partnerrelationshiptype**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) numaralandırmasının bir üyesini geçirerek [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) veya [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) yöntemini çağırın. Dolaylı satıcıları almak için ısındirectcloudsolutionproviderof kullanmanız gerekir.

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

**örnek**: [konsol test uygulaması](console-test-app.md)**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getındirectsatıcıları. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Relationships? ilişki \_ türü = ısındirectcloudsolutionproviderof http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İlişki türünü tanımlamak için aşağıdaki sorgu parametresini kullanın.

| Ad               | Tür    | Gerekli  | Açıklama                         |
|--------------------|---------|-----------|-------------------------------------|
| relationship_type  | string  | Yes       | Değer, [Partnerrelationshiptype](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)içinde bulunan üye adlarından birinin dize gösterimidir.<br/><br/> İş ortağı bir sağlayıcı olarak oturum açmışsa ve ilişki kurdukları dolaylı satıcıların bir listesini almak istiyorsanız, ısındirectcloudsolutionproviderof kullanın.<br/><br/> İş ortağı bir satıcı olarak oturum açmışsa ve ilişki kurdukları dolaylı sağlayıcıların bir listesini almak istiyorsanız, ısındirectresellerkullanın.    |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

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

Başarılı olursa, yanıt gövdesi satıcıları tanımlamak için bir [Iş ortağı ilişki](relationships-resources.md) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

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