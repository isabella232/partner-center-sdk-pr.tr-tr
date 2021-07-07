---
title: Self Servis ilkelerinin bir listesini alın
description: Müşterinin self servis ilkelerini temsil eden kaynakların koleksiyonunu alma.
ms.date: 07/06/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b18fde8a11d3ed3dd31e50fdba746dd6b0bf3f97
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025743"
---
# <a name="get-a-list-of-self-serve-policies"></a><span data-ttu-id="d1363-103">Self Servis ilkelerinin bir listesini alın</span><span class="sxs-lookup"><span data-stu-id="d1363-103">Get a list of self-serve policies</span></span>

<span data-ttu-id="d1363-104">Bir varlık için self servis ilkelerini temsil eden kaynakların bir koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="d1363-104">Gets a collection of resources that represents self-serve policies for an entity.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d1363-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d1363-105">Prerequisites</span></span>

- <span data-ttu-id="d1363-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d1363-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d1363-107">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d1363-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d1363-108">C\#</span><span class="sxs-lookup"><span data-stu-id="d1363-108">C\#</span></span>

<span data-ttu-id="d1363-109">Tüm self servis ilkelerinin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="d1363-109">To get a list of all self-serve policies:</span></span>

1. <span data-ttu-id="d1363-110">İlkelerdeki işlemlere bir arabirim almak için, varlık tanımlayıcısıyla [**ıaggregatepartner. SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d1363-110">Call the [**IAggregatePartner.SelfServePolicies**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// gets the self-serve policies
var SelfServePolicies = scopedPartnerOperations.SelfServePolicies.Get(customerIdAsEntity);
```

<span data-ttu-id="d1363-111">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="d1363-111">For an example, see the following:</span></span>

- <span data-ttu-id="d1363-112">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d1363-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d1363-113">Project: **partnersdk. featuresamples**</span><span class="sxs-lookup"><span data-stu-id="d1363-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="d1363-114">Sınıf: **GetSelfServePolicies. cs**</span><span class="sxs-lookup"><span data-stu-id="d1363-114">Class: **GetSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d1363-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d1363-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d1363-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d1363-116">Request syntax</span></span>

| <span data-ttu-id="d1363-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d1363-117">Method</span></span>  | <span data-ttu-id="d1363-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d1363-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="d1363-119">**Al**</span><span class="sxs-lookup"><span data-stu-id="d1363-119">**GET**</span></span> | <span data-ttu-id="d1363-120">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy? entity_id = {ENTITY_ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d1363-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy?entity_id={entity_id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d1363-121">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d1363-121">URI parameter</span></span>

<span data-ttu-id="d1363-122">Müşterilerin bir listesini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d1363-122">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="d1363-123">Ad</span><span class="sxs-lookup"><span data-stu-id="d1363-123">Name</span></span>          | <span data-ttu-id="d1363-124">Tür</span><span class="sxs-lookup"><span data-stu-id="d1363-124">Type</span></span>       | <span data-ttu-id="d1363-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d1363-125">Required</span></span> | <span data-ttu-id="d1363-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d1363-126">Description</span></span>                                        |
|---------------|------------|----------|----------------------------------------------------|
| <span data-ttu-id="d1363-127">**entity_id**</span><span class="sxs-lookup"><span data-stu-id="d1363-127">**entity_id**</span></span> | <span data-ttu-id="d1363-128">**string**</span><span class="sxs-lookup"><span data-stu-id="d1363-128">**string**</span></span> | <span data-ttu-id="d1363-129">Y</span><span class="sxs-lookup"><span data-stu-id="d1363-129">Y</span></span>        | <span data-ttu-id="d1363-130">İçin erişim isteyen varlık tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d1363-130">The entity identifier requesting access for.</span></span> <span data-ttu-id="d1363-131">Bu, müşterinin kiracı KIMLIĞI olacaktır.</span><span class="sxs-lookup"><span data-stu-id="d1363-131">This will be the customer's tenant ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d1363-132">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d1363-132">Request headers</span></span>

<span data-ttu-id="d1363-133">Daha fazla bilgi için bkz. [üstbilgiler](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d1363-133">For more information, see [Headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d1363-134">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d1363-134">Request body</span></span>

<span data-ttu-id="d1363-135">Yok.</span><span class="sxs-lookup"><span data-stu-id="d1363-135">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d1363-136">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d1363-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy?entity_id=0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="d1363-137">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d1363-137">REST response</span></span>

<span data-ttu-id="d1363-138">Başarılı olursa, bu yöntem yanıt gövdesinde bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="d1363-138">If successful, this method returns a collection of [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d1363-139">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d1363-139">Response success and error codes</span></span>

<span data-ttu-id="d1363-140">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="d1363-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d1363-141">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d1363-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d1363-142">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d1363-142">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d1363-143">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d1363-143">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 1,
    "items": [{
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
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
