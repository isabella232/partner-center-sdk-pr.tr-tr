---
title: Self Servis ilkesi oluşturma
description: Yeni bir self servis ilkesi oluşturma.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd1579b2775ead57a440db0d6afb3bf22164c319
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770218"
---
# <a name="create-a-selfservepolicy"></a><span data-ttu-id="78ca6-103">SelfServePolicy oluşturma</span><span class="sxs-lookup"><span data-stu-id="78ca6-103">Create a SelfServePolicy</span></span>

<span data-ttu-id="78ca6-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="78ca6-104">**Applies to:**</span></span>

- <span data-ttu-id="78ca6-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="78ca6-105">Partner Center</span></span>

<span data-ttu-id="78ca6-106">Bu konuda, yeni bir self servis ilkesinin nasıl oluşturulacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="78ca6-106">This topic explains how to create a new self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78ca6-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="78ca6-107">Prerequisites</span></span>

- <span data-ttu-id="78ca6-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="78ca6-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="78ca6-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="78ca6-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="78ca6-110">C\#</span><span class="sxs-lookup"><span data-stu-id="78ca6-110">C\#</span></span>

<span data-ttu-id="78ca6-111">Self Servis ilkesi oluşturun:</span><span class="sxs-lookup"><span data-stu-id="78ca6-111">Create a self-serve policy:</span></span>

1. <span data-ttu-id="78ca6-112">Self Servis ilke bilgileriyle [**ıaggregatepartner. SelfServePolicies. Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) veya [**ıaggregatepartner. SelfServePolicies. createasync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="78ca6-112">Call the [**IAggregatePartner.SelfServePolicies.Create**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.create) or [**IAggregatePartner.SelfServePolicies.CreateAsync**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.createasync) method with the self-serve policy info.</span></span>

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

<span data-ttu-id="78ca6-113">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="78ca6-113">For an example, see the following:</span></span>

- <span data-ttu-id="78ca6-114">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="78ca6-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="78ca6-115">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="78ca6-115">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="78ca6-116">Sınıf: **CreateSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="78ca6-116">Class: **CreateSelfServePolicies.cs**</span></span>


## <a name="rest-request"></a><span data-ttu-id="78ca6-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="78ca6-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="78ca6-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="78ca6-118">Request syntax</span></span>

| <span data-ttu-id="78ca6-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="78ca6-119">Method</span></span>   | <span data-ttu-id="78ca6-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="78ca6-120">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="78ca6-121">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="78ca6-121">**POST**</span></span> | <span data-ttu-id="78ca6-122">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="78ca6-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="78ca6-123">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="78ca6-123">Request headers</span></span>

- <span data-ttu-id="78ca6-124">İstek KIMLIĞI ve bağıntı KIMLIĞI gereklidir.</span><span class="sxs-lookup"><span data-stu-id="78ca6-124">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="78ca6-125">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="78ca6-125">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="78ca6-126">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="78ca6-126">Request body</span></span>

<span data-ttu-id="78ca6-127">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="78ca6-127">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="78ca6-128">Ad</span><span class="sxs-lookup"><span data-stu-id="78ca6-128">Name</span></span>                              | <span data-ttu-id="78ca6-129">Tür</span><span class="sxs-lookup"><span data-stu-id="78ca6-129">Type</span></span>   | <span data-ttu-id="78ca6-130">Description</span><span class="sxs-lookup"><span data-stu-id="78ca6-130">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="78ca6-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="78ca6-131">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="78ca6-132">object</span><span class="sxs-lookup"><span data-stu-id="78ca6-132">object</span></span> | <span data-ttu-id="78ca6-133">Self Servis ilke bilgileri.</span><span class="sxs-lookup"><span data-stu-id="78ca6-133">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="78ca6-134">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="78ca6-134">SelfServePolicy</span></span>

<span data-ttu-id="78ca6-135">Bu tabloda, yeni bir self servis ilkesi oluşturmak için gereken [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağından gerekli en düşük alan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="78ca6-135">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="78ca6-136">Özellik</span><span class="sxs-lookup"><span data-stu-id="78ca6-136">Property</span></span>              | <span data-ttu-id="78ca6-137">Tür</span><span class="sxs-lookup"><span data-stu-id="78ca6-137">Type</span></span>             | <span data-ttu-id="78ca6-138">Description</span><span class="sxs-lookup"><span data-stu-id="78ca6-138">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="78ca6-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="78ca6-139">SelfServeEntity</span></span>       | <span data-ttu-id="78ca6-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="78ca6-140">SelfServeEntity</span></span>  | <span data-ttu-id="78ca6-141">Erişim izni verilen self servis varlığı.</span><span class="sxs-lookup"><span data-stu-id="78ca6-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="78ca6-142">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="78ca6-142">Grantor</span></span>               | <span data-ttu-id="78ca6-143">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="78ca6-143">Grantor</span></span>          | <span data-ttu-id="78ca6-144">Erişim veren granör.</span><span class="sxs-lookup"><span data-stu-id="78ca6-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="78ca6-145">İzinler</span><span class="sxs-lookup"><span data-stu-id="78ca6-145">Permissions</span></span>           | <span data-ttu-id="78ca6-146">Izin dizisi</span><span class="sxs-lookup"><span data-stu-id="78ca6-146">Array of Permission</span></span>| <span data-ttu-id="78ca6-147">[İzin](self-serve-policy-resources.md#permission) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="78ca6-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                                     |


### <a name="request-example"></a><span data-ttu-id="78ca6-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="78ca6-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="78ca6-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="78ca6-149">REST response</span></span>

<span data-ttu-id="78ca6-150">Başarılı olursa, bu API yeni self servis ilkesi için bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="78ca6-150">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the new self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="78ca6-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="78ca6-151">Response success and error codes</span></span>

<span data-ttu-id="78ca6-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="78ca6-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="78ca6-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="78ca6-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="78ca6-154">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="78ca6-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="78ca6-155">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="78ca6-155">This method returns the following error codes:</span></span>

| <span data-ttu-id="78ca6-156">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="78ca6-156">HTTP Status Code</span></span>     | <span data-ttu-id="78ca6-157">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="78ca6-157">Error code</span></span>   | <span data-ttu-id="78ca6-158">Description</span><span class="sxs-lookup"><span data-stu-id="78ca6-158">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="78ca6-159">409</span><span class="sxs-lookup"><span data-stu-id="78ca6-159">409</span></span>                  | <span data-ttu-id="78ca6-160">600041</span><span class="sxs-lookup"><span data-stu-id="78ca6-160">600041</span></span>       | <span data-ttu-id="78ca6-161">Self Servis İlkesi zaten var.</span><span class="sxs-lookup"><span data-stu-id="78ca6-161">Self-serve policy already exists.</span></span>                                                     |


### <a name="response-example"></a><span data-ttu-id="78ca6-162">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="78ca6-162">Response example</span></span>

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
