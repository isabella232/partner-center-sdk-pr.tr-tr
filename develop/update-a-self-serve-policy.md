---
title: Self Servis ilkesini güncelleştirme
description: Self Servis ilkesini güncelleştirme.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4d53ab8e5b8ef5b7be83360a3f43ec7791b2e3b4
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770250"
---
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="e9f89-103">SelfServePolicy güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e9f89-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="e9f89-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="e9f89-104">**Applies to:**</span></span>

- <span data-ttu-id="e9f89-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e9f89-105">Partner Center</span></span>

<span data-ttu-id="e9f89-106">Bu konu, bir self servis ilkesinin nasıl güncelleştireceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="e9f89-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e9f89-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e9f89-107">Prerequisites</span></span>

- <span data-ttu-id="e9f89-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e9f89-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e9f89-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e9f89-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="e9f89-110">C\#</span><span class="sxs-lookup"><span data-stu-id="e9f89-110">C\#</span></span>

<span data-ttu-id="e9f89-111">Self Servis ilkesini silmek için:</span><span class="sxs-lookup"><span data-stu-id="e9f89-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="e9f89-112">İlkelerdeki işlemlere bir arabirim almak için, varlık tanımlayıcısıyla [**ıaggregatepartner. SelfServePolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="e9f89-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="e9f89-113">Self Servis ilkesini güncelleştirmek için [**PUT**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) veya [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="e9f89-113">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="e9f89-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e9f89-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e9f89-115">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e9f89-115">Request syntax</span></span>

| <span data-ttu-id="e9f89-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e9f89-116">Method</span></span>   | <span data-ttu-id="e9f89-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e9f89-117">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="e9f89-118">**PUT**</span><span class="sxs-lookup"><span data-stu-id="e9f89-118">**PUT**</span></span> | <span data-ttu-id="e9f89-119">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="e9f89-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e9f89-120">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e9f89-120">Request headers</span></span>

- <span data-ttu-id="e9f89-121">İstek tanımlayıcısı ve bağıntı tanımlayıcısı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e9f89-121">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="e9f89-122">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="e9f89-122">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="e9f89-123">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e9f89-123">Request body</span></span>

<span data-ttu-id="e9f89-124">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e9f89-124">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="e9f89-125">Ad</span><span class="sxs-lookup"><span data-stu-id="e9f89-125">Name</span></span>                              | <span data-ttu-id="e9f89-126">Tür</span><span class="sxs-lookup"><span data-stu-id="e9f89-126">Type</span></span>   | <span data-ttu-id="e9f89-127">Description</span><span class="sxs-lookup"><span data-stu-id="e9f89-127">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="e9f89-128">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="e9f89-128">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="e9f89-129">object</span><span class="sxs-lookup"><span data-stu-id="e9f89-129">object</span></span> | <span data-ttu-id="e9f89-130">Self Servis ilke bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e9f89-130">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="e9f89-131">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="e9f89-131">SelfServePolicy</span></span>

<span data-ttu-id="e9f89-132">Bu tabloda, yeni bir self servis ilkesi oluşturmak için gereken [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağından gerekli en düşük alan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="e9f89-132">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="e9f89-133">Özellik</span><span class="sxs-lookup"><span data-stu-id="e9f89-133">Property</span></span>              | <span data-ttu-id="e9f89-134">Tür</span><span class="sxs-lookup"><span data-stu-id="e9f89-134">Type</span></span>             | <span data-ttu-id="e9f89-135">Description</span><span class="sxs-lookup"><span data-stu-id="e9f89-135">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e9f89-136">kimlik</span><span class="sxs-lookup"><span data-stu-id="e9f89-136">id</span></span>                    | <span data-ttu-id="e9f89-137">string</span><span class="sxs-lookup"><span data-stu-id="e9f89-137">string</span></span>           | <span data-ttu-id="e9f89-138">Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan kendi kendine bir ilke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="e9f89-138">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="e9f89-139">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="e9f89-139">SelfServeEntity</span></span>       | <span data-ttu-id="e9f89-140">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="e9f89-140">SelfServeEntity</span></span>  | <span data-ttu-id="e9f89-141">Erişim izni verilen self servis varlığı.</span><span class="sxs-lookup"><span data-stu-id="e9f89-141">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="e9f89-142">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="e9f89-142">Grantor</span></span>               | <span data-ttu-id="e9f89-143">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="e9f89-143">Grantor</span></span>          | <span data-ttu-id="e9f89-144">Erişim veren granör.</span><span class="sxs-lookup"><span data-stu-id="e9f89-144">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="e9f89-145">İzinler</span><span class="sxs-lookup"><span data-stu-id="e9f89-145">Permissions</span></span>           | <span data-ttu-id="e9f89-146">Izin dizisi</span><span class="sxs-lookup"><span data-stu-id="e9f89-146">Array of Permission</span></span>| <span data-ttu-id="e9f89-147">[İzin](self-serve-policy-resources.md#permission) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="e9f89-147">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="e9f89-148">Özelliği</span><span class="sxs-lookup"><span data-stu-id="e9f89-148">Etag</span></span>                  | <span data-ttu-id="e9f89-149">string</span><span class="sxs-lookup"><span data-stu-id="e9f89-149">string</span></span>           | <span data-ttu-id="e9f89-150">ETag.</span><span class="sxs-lookup"><span data-stu-id="e9f89-150">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="e9f89-151">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e9f89-151">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="e9f89-152">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e9f89-152">REST response</span></span>

<span data-ttu-id="e9f89-153">Başarılı olursa, bu API güncelleştirilmiş self servis ilkesi için bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="e9f89-153">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e9f89-154">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e9f89-154">Response success and error codes</span></span>

<span data-ttu-id="e9f89-155">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e9f89-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e9f89-156">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e9f89-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e9f89-157">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e9f89-157">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="e9f89-158">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="e9f89-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="e9f89-159">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="e9f89-159">HTTP Status Code</span></span>     | <span data-ttu-id="e9f89-160">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="e9f89-160">Error code</span></span>   | <span data-ttu-id="e9f89-161">Description</span><span class="sxs-lookup"><span data-stu-id="e9f89-161">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="e9f89-162">404</span><span class="sxs-lookup"><span data-stu-id="e9f89-162">404</span></span>                  | <span data-ttu-id="e9f89-163">600039</span><span class="sxs-lookup"><span data-stu-id="e9f89-163">600039</span></span>       | <span data-ttu-id="e9f89-164">Self Servis ilkesi bulunamadı</span><span class="sxs-lookup"><span data-stu-id="e9f89-164">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="e9f89-165">404</span><span class="sxs-lookup"><span data-stu-id="e9f89-165">404</span></span>                  | <span data-ttu-id="e9f89-166">600040</span><span class="sxs-lookup"><span data-stu-id="e9f89-166">600040</span></span>       | <span data-ttu-id="e9f89-167">Self Servis ilke tanımlayıcısı yanlış</span><span class="sxs-lookup"><span data-stu-id="e9f89-167">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="e9f89-168">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e9f89-168">Response example</span></span>

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
