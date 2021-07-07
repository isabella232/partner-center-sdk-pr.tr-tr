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
# <a name="update-a-selfservepolicy"></a><span data-ttu-id="de91f-103">SelfServePolicy güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="de91f-103">Update a SelfServePolicy</span></span>

<span data-ttu-id="de91f-104">Bu makalede bir self servis ilkesinin nasıl güncelleştirilmesi açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="de91f-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="de91f-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="de91f-105">Prerequisites</span></span>

- <span data-ttu-id="de91f-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="de91f-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="de91f-107">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="de91f-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="de91f-108">C\#</span><span class="sxs-lookup"><span data-stu-id="de91f-108">C\#</span></span>

<span data-ttu-id="de91f-109">Self Servis ilkesini silmek için:</span><span class="sxs-lookup"><span data-stu-id="de91f-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="de91f-110">İlkelerdeki işlemlere bir arabirim almak için, varlık tanımlayıcısıyla [**ıaggregatepartner. SelfServePolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="de91f-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="de91f-111">Self Servis ilkesini güncelleştirmek için [**PUT**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) veya [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="de91f-111">Call the [**Put**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.put) or [**PutAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.putasync) method to update the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
SelfServePolicy policy;

// All the operations executed on this partner operation instance will share the same correlation identifier but will differ in request identifier
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// updates the self-serve policies
partnerOperations.SelfServePolicies.ById(policy.id).Put(policy);
```

## <a name="rest-request"></a><span data-ttu-id="de91f-112">REST isteği</span><span class="sxs-lookup"><span data-stu-id="de91f-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="de91f-113">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="de91f-113">Request syntax</span></span>

| <span data-ttu-id="de91f-114">Yöntem</span><span class="sxs-lookup"><span data-stu-id="de91f-114">Method</span></span>   | <span data-ttu-id="de91f-115">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="de91f-115">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="de91f-116">**PUT**</span><span class="sxs-lookup"><span data-stu-id="de91f-116">**PUT**</span></span> | <span data-ttu-id="de91f-117">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy http/1.1</span><span class="sxs-lookup"><span data-stu-id="de91f-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="de91f-118">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="de91f-118">Request headers</span></span>

- <span data-ttu-id="de91f-119">İstek tanımlayıcısı ve bağıntı tanımlayıcısı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="de91f-119">A request identifier and correlation identifier are required.</span></span>
- <span data-ttu-id="de91f-120">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="de91f-120">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="de91f-121">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="de91f-121">Request body</span></span>

<span data-ttu-id="de91f-122">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="de91f-122">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="de91f-123">Ad</span><span class="sxs-lookup"><span data-stu-id="de91f-123">Name</span></span>                              | <span data-ttu-id="de91f-124">Tür</span><span class="sxs-lookup"><span data-stu-id="de91f-124">Type</span></span>   | <span data-ttu-id="de91f-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="de91f-125">Description</span></span>                                 |
|------------------------------------------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="de91f-126">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="de91f-126">SelfServePolicy</span></span>](self-serve-policy-resources.md#selfservepolicy)| <span data-ttu-id="de91f-127">object</span><span class="sxs-lookup"><span data-stu-id="de91f-127">object</span></span> | <span data-ttu-id="de91f-128">Self Servis ilke bilgileri.</span><span class="sxs-lookup"><span data-stu-id="de91f-128">The self-serve policy information.</span></span> |

#### <a name="selfservepolicy"></a><span data-ttu-id="de91f-129">SelfServePolicy</span><span class="sxs-lookup"><span data-stu-id="de91f-129">SelfServePolicy</span></span>

<span data-ttu-id="de91f-130">Bu tabloda, yeni bir self servis ilkesi oluşturmak için gereken [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağından gerekli en düşük alan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="de91f-130">This table describes the minimum required fields from the [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource needed to create a new self-serve policy.</span></span>

| <span data-ttu-id="de91f-131">Özellik</span><span class="sxs-lookup"><span data-stu-id="de91f-131">Property</span></span>              | <span data-ttu-id="de91f-132">Tür</span><span class="sxs-lookup"><span data-stu-id="de91f-132">Type</span></span>             | <span data-ttu-id="de91f-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="de91f-133">Description</span></span>                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="de91f-134">kimlik</span><span class="sxs-lookup"><span data-stu-id="de91f-134">id</span></span>                    | <span data-ttu-id="de91f-135">string</span><span class="sxs-lookup"><span data-stu-id="de91f-135">string</span></span>           | <span data-ttu-id="de91f-136">Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan kendi kendine bir ilke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="de91f-136">A self-serve policy identifier that is supplied upon successful creation of the self-serve policy.</span></span>     |
| <span data-ttu-id="de91f-137">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="de91f-137">SelfServeEntity</span></span>       | <span data-ttu-id="de91f-138">SelfServeEntity</span><span class="sxs-lookup"><span data-stu-id="de91f-138">SelfServeEntity</span></span>  | <span data-ttu-id="de91f-139">Erişim izni verilen self servis varlığı.</span><span class="sxs-lookup"><span data-stu-id="de91f-139">The self-serve entity that is being granted access.</span></span>                                                     |
| <span data-ttu-id="de91f-140">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="de91f-140">Grantor</span></span>               | <span data-ttu-id="de91f-141">Verenin Grant izni</span><span class="sxs-lookup"><span data-stu-id="de91f-141">Grantor</span></span>          | <span data-ttu-id="de91f-142">Erişim veren granör.</span><span class="sxs-lookup"><span data-stu-id="de91f-142">The grantor that is granting access.</span></span>                                                                    |
| <span data-ttu-id="de91f-143">İzinler</span><span class="sxs-lookup"><span data-stu-id="de91f-143">Permissions</span></span>           | <span data-ttu-id="de91f-144">Izin dizisi</span><span class="sxs-lookup"><span data-stu-id="de91f-144">Array of Permission</span></span>| <span data-ttu-id="de91f-145">[İzin](self-serve-policy-resources.md#permission) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="de91f-145">An Array of [Permission](self-serve-policy-resources.md#permission) resources.</span></span>                                                      |
| <span data-ttu-id="de91f-146">Özelliği</span><span class="sxs-lookup"><span data-stu-id="de91f-146">Etag</span></span>                  | <span data-ttu-id="de91f-147">string</span><span class="sxs-lookup"><span data-stu-id="de91f-147">string</span></span>           | <span data-ttu-id="de91f-148">ETag.</span><span class="sxs-lookup"><span data-stu-id="de91f-148">The Etag.</span></span>                                                                                               |


### <a name="request-example"></a><span data-ttu-id="de91f-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="de91f-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="de91f-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="de91f-150">REST response</span></span>

<span data-ttu-id="de91f-151">Başarılı olursa, bu API güncelleştirilmiş self servis ilkesi için bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="de91f-151">If successful, this API returns a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource for the updated self-serve policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="de91f-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="de91f-152">Response success and error codes</span></span>

<span data-ttu-id="de91f-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="de91f-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="de91f-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="de91f-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="de91f-155">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="de91f-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

<span data-ttu-id="de91f-156">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="de91f-156">This method returns the following error codes:</span></span>

| <span data-ttu-id="de91f-157">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="de91f-157">HTTP Status Code</span></span>     | <span data-ttu-id="de91f-158">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="de91f-158">Error code</span></span>   | <span data-ttu-id="de91f-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="de91f-159">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="de91f-160">404</span><span class="sxs-lookup"><span data-stu-id="de91f-160">404</span></span>                  | <span data-ttu-id="de91f-161">600039</span><span class="sxs-lookup"><span data-stu-id="de91f-161">600039</span></span>       | <span data-ttu-id="de91f-162">Self Servis ilkesi bulunamadı</span><span class="sxs-lookup"><span data-stu-id="de91f-162">Self-serve policy was not found</span></span>                                            |
| <span data-ttu-id="de91f-163">404</span><span class="sxs-lookup"><span data-stu-id="de91f-163">404</span></span>                  | <span data-ttu-id="de91f-164">600040</span><span class="sxs-lookup"><span data-stu-id="de91f-164">600040</span></span>       | <span data-ttu-id="de91f-165">Self Servis ilke tanımlayıcısı yanlış</span><span class="sxs-lookup"><span data-stu-id="de91f-165">Self-serve policy identifier is incorrect</span></span>                                  |


### <a name="response-example"></a><span data-ttu-id="de91f-166">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="de91f-166">Response example</span></span>

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
