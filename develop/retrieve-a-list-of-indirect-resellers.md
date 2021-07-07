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
# <a name="retrieve-a-list-of-indirect-resellers"></a><span data-ttu-id="3f2a7-103">Dolaylı satıcıların bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="3f2a7-103">Retrieve a list of indirect resellers</span></span>

<span data-ttu-id="3f2a7-104">Oturum açmış ortağın dolaylı satıcıların listesini alma.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-104">How to retrieve a list of the signed-in partner's indirect resellers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3f2a7-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3f2a7-105">Prerequisites</span></span>

- <span data-ttu-id="3f2a7-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3f2a7-107">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-107">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="3f2a7-108">C\#</span><span class="sxs-lookup"><span data-stu-id="3f2a7-108">C\#</span></span>

<span data-ttu-id="3f2a7-109">Oturum açmış iş ortağının ilişkiye sahip olduğu dolaylı satıcıların bir listesini almak için, ilk olarak [**partneroperations. relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) özelliğinden ilişki toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-109">To retrieve a list of indirect resellers with whom the signed-in partner has a relationship, first get an interface to relationship collection operations from the [**partnerOperations.Relationships**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property.</span></span> <span data-ttu-id="3f2a7-110">Ardından, ilişki türünü tanımlamak için [**Partnerrelationshiptype**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) numaralandırmasının bir üyesini geçirerek [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) veya [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-110">Then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.irelationshipcollection.getasync) method, passing a member of the [**PartnerRelationshipType**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype) enumeration to identify the relationship type.</span></span> <span data-ttu-id="3f2a7-111">Dolaylı satıcıları almak için ısındirectcloudsolutionproviderof kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-111">To retrieve indirect resellers, you must use IsIndirectCloudSolutionProviderOf.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);
```

<span data-ttu-id="3f2a7-112">**örnek**: [konsol test uygulaması](console-test-app.md)**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getındirectsatıcıları. cs</span><span class="sxs-lookup"><span data-stu-id="3f2a7-112">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3f2a7-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3f2a7-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3f2a7-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3f2a7-114">Request syntax</span></span>

| <span data-ttu-id="3f2a7-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3f2a7-115">Method</span></span>  | <span data-ttu-id="3f2a7-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3f2a7-116">Request URI</span></span>                                                                                                                |
|---------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3f2a7-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="3f2a7-117">**GET**</span></span> | <span data-ttu-id="3f2a7-118">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Relationships? ilişki \_ türü = ısındirectcloudsolutionproviderof http/1.1</span><span class="sxs-lookup"><span data-stu-id="3f2a7-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/relationships?relationship\_type=IsIndirectCloudSolutionProviderOf HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3f2a7-119">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="3f2a7-119">URI parameter</span></span>

<span data-ttu-id="3f2a7-120">İlişki türünü tanımlamak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-120">Use the following query parameter to identify the relationship type.</span></span>

| <span data-ttu-id="3f2a7-121">Ad</span><span class="sxs-lookup"><span data-stu-id="3f2a7-121">Name</span></span>               | <span data-ttu-id="3f2a7-122">Tür</span><span class="sxs-lookup"><span data-stu-id="3f2a7-122">Type</span></span>    | <span data-ttu-id="3f2a7-123">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3f2a7-123">Required</span></span>  | <span data-ttu-id="3f2a7-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3f2a7-124">Description</span></span>                         |
|--------------------|---------|-----------|-------------------------------------|
| <span data-ttu-id="3f2a7-125">relationship_type</span><span class="sxs-lookup"><span data-stu-id="3f2a7-125">relationship_type</span></span>  | <span data-ttu-id="3f2a7-126">string</span><span class="sxs-lookup"><span data-stu-id="3f2a7-126">string</span></span>  | <span data-ttu-id="3f2a7-127">Yes</span><span class="sxs-lookup"><span data-stu-id="3f2a7-127">Yes</span></span>       | <span data-ttu-id="3f2a7-128">Değer, [Partnerrelationshiptype](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype)içinde bulunan üye adlarından birinin dize gösterimidir.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-128">The value is the string representation of one of the member names found in [PartnerRelationshipType](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationshiptype).</span></span><br/><br/> <span data-ttu-id="3f2a7-129">İş ortağı bir sağlayıcı olarak oturum açmışsa ve ilişki kurdukları dolaylı satıcıların bir listesini almak istiyorsanız, ısındirectcloudsolutionproviderof kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-129">If the partner is signed in as a provider and you want to get a list of the indirect resellers with whom they have established a relationship, use IsIndirectCloudSolutionProviderOf.</span></span><br/><br/> <span data-ttu-id="3f2a7-130">İş ortağı bir satıcı olarak oturum açmışsa ve ilişki kurdukları dolaylı sağlayıcıların bir listesini almak istiyorsanız, ısındirectresellerkullanın.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-130">If the partner is signed in as a reseller and you want to get a list of the indirect providers with whom they have established a relationship, use IsIndirectResellerOf.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="3f2a7-131">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3f2a7-131">Request headers</span></span>

<span data-ttu-id="3f2a7-132">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3f2a7-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3f2a7-133">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3f2a7-133">Request body</span></span>

<span data-ttu-id="3f2a7-134">Yok.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3f2a7-135">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3f2a7-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/relationships?relationship_type=IsIndirectCloudSolutionProviderOf HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 144391a4-fb06-41ae-b684-3308ce4706bd
MS-CorrelationId: 72524ef8-81aa-4141-a049-45a4fece5d84
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="3f2a7-136">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3f2a7-136">REST response</span></span>

<span data-ttu-id="3f2a7-137">Başarılı olursa, yanıt gövdesi satıcıları tanımlamak için bir [Iş ortağı ilişki](relationships-resources.md) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-137">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3f2a7-138">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3f2a7-138">Response success and error codes</span></span>

<span data-ttu-id="3f2a7-139">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3f2a7-140">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3f2a7-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3f2a7-141">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3f2a7-141">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3f2a7-142">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3f2a7-142">Response example</span></span>

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