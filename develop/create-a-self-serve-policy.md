---
title: Self servis ilkesi oluşturma
description: Yeni bir self servis ilkesi oluşturma.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 14f46e22fbd294c765b745204cf62474250cbfbd
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973698"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="ec7a3-103">SelfServePolicy oluşturma</span><span class="sxs-lookup"><span data-stu-id="ec7a3-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="ec7a3-104">Bu makalede yeni bir self servis ilkesi oluşturma açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-104">This article explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ec7a3-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ec7a3-105">Prerequisites</span></span>

- <span data-ttu-id="ec7a3-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="ec7a3-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ec7a3-107">Bu senaryo, Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="ec7a3-108">C\#</span><span class="sxs-lookup"><span data-stu-id="ec7a3-108">C\#</span></span>

<span data-ttu-id="ec7a3-109">Self servis ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="ec7a3-109">Create a self-serve policy:</span></span>

1. <span data-ttu-id="ec7a3-110">Self servis [**ilke bilgileriyle IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) veya [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-110">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string customerIdAsEntity;

var selfServePolicy = new SelfServePolicy
{
    SelfServeEntity = new SelfServeEntity
    {
        SelfServeEntityType = "customer",
        TenantID = customerIdAsEntity,
    },
    Grantor = new Grantor
    {
        GrantorType = "billToPartner",
        TenantID = partnerIdAsGrantor,
    },
    Permissions = new Permission[]
    {
        new Permission
        {
        Action = "Purchase",
        Resource = "AzureReservedInstances",
        },
    },
};

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// creates the self-serve policy
SelfServePolicy createdSelfServePolicy = scopedPartnerOperations.selfServePolicies.Create(selfServePolicy);
```

<span data-ttu-id="ec7a3-111">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="ec7a3-111">For an example, see the following:</span></span>

- <span data-ttu-id="ec7a3-112">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ec7a3-112">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ec7a3-113">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="ec7a3-113">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="ec7a3-114">Sınıf: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="ec7a3-114">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="ec7a3-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="ec7a3-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ec7a3-116">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="ec7a3-116">Request syntax</span></span>

| <span data-ttu-id="ec7a3-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="ec7a3-117">Method</span></span>   | <span data-ttu-id="ec7a3-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="ec7a3-118">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="ec7a3-119">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="ec7a3-119">**POST**</span></span> | <span data-ttu-id="ec7a3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="ec7a3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ec7a3-121">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="ec7a3-121">Request headers</span></span>

- <span data-ttu-id="ec7a3-122">İstek kimliği ve bağıntı kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-122">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="ec7a3-123">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="ec7a3-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ec7a3-124">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="ec7a3-124">Request body</span></span>

<span data-ttu-id="ec7a3-125">Bu tablo, istek gövdesinde gerekli özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-125">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="ec7a3-126">Ad</span><span class="sxs-lookup"><span data-stu-id="ec7a3-126">Name</span></span>                              | <span data-ttu-id="ec7a3-127">Tür</span><span class="sxs-lookup"><span data-stu-id="ec7a3-127">Type</span></span>   | <span data-ttu-id="ec7a3-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ec7a3-128">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="ec7a3-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ec7a3-129">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="ec7a3-130">object</span><span class="sxs-lookup"><span data-stu-id="ec7a3-130">object</span></span> | <span data-ttu-id="ec7a3-131">Self servis ilke bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-131">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="ec7a3-132">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="ec7a3-132">SelfServePolicy</span></span>

<span data-ttu-id="ec7a3-133">Bu tablo, yeni bir self servis ilkesi oluşturmak için [gereken SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağından gereken minimum alanları açıklar.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-133">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="ec7a3-134">Özellik</span><span class="sxs-lookup"><span data-stu-id="ec7a3-134">Property</span></span>              | <span data-ttu-id="ec7a3-135">Tür</span><span class="sxs-lookup"><span data-stu-id="ec7a3-135">Type</span></span>             | <span data-ttu-id="ec7a3-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ec7a3-136">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ec7a3-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="ec7a3-137">SelfServeEntity</span></span>       | <span data-ttu-id="ec7a3-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="ec7a3-138">SelfServeEntity</span></span>  | <span data-ttu-id="ec7a3-139">Erişim verilen self servis varlık.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="ec7a3-140">Grantor</span><span class="sxs-lookup"><span data-stu-id="ec7a3-140">Grantor</span></span>               | <span data-ttu-id="ec7a3-141">Grantor</span><span class="sxs-lookup"><span data-stu-id="ec7a3-141">Grantor</span></span>          | <span data-ttu-id="ec7a3-142">Erişim iznini vermekte olan grantor.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="ec7a3-143">İzinler</span><span class="sxs-lookup"><span data-stu-id="ec7a3-143">Permissions</span></span>           | <span data-ttu-id="ec7a3-144">İzin Dizisi</span><span class="sxs-lookup"><span data-stu-id="ec7a3-144">Array of Permission</span></span>| <span data-ttu-id="ec7a3-145">İzin [kaynakları](self-serve-policy-resources.md#permission) dizisi.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="ec7a3-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="ec7a3-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/SelfServePolicy HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
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
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="ec7a3-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="ec7a3-147">REST response</span></span>

<span data-ttu-id="ec7a3-148">Başarılı olursa, bu API yeni self servis ilkesi için bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-148">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ec7a3-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ec7a3-149">Response success and error codes</span></span>

<span data-ttu-id="ec7a3-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ec7a3-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ec7a3-152">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ec7a3-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="ec7a3-153">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="ec7a3-153">This method returns the following error codes:</span></span>

| <span data-ttu-id="ec7a3-154">HTTP Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="ec7a3-154">HTTP Status Code</span></span>     | <span data-ttu-id="ec7a3-155">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="ec7a3-155">Error code</span></span>   | <span data-ttu-id="ec7a3-156">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ec7a3-156">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="ec7a3-157">409</span><span class="sxs-lookup"><span data-stu-id="ec7a3-157">409</span></span>                  | <span data-ttu-id="ec7a3-158">600041</span><span class="sxs-lookup"><span data-stu-id="ec7a3-158">600041</span></span>       | <span data-ttu-id="ec7a3-159">Self servis ilkesi zaten var.</span><span class="sxs-lookup"><span data-stu-id="ec7a3-159">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="ec7a3-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="ec7a3-160">Response example</span></span>

```http
HTTP/1.1 201 Created
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
        "etag": "\"933523d1-3f63-4fc3-8789-5e21c02cdaed\"",
        "objectType": "SelfServePolicy"
    }
}
```
