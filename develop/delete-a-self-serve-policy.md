---
title: Self Servis ilkesini silme
description: Self Servis ilkesini silme.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3450145d6daf2ffca5e2886245e592406cb0886d
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770226"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="1ed4b-103">Bir SelfServePolicy silme</span><span class="sxs-lookup"><span data-stu-id="1ed4b-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="1ed4b-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="1ed4b-104">**Applies to:**</span></span>

- <span data-ttu-id="1ed4b-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1ed4b-105">Partner Center</span></span>

<span data-ttu-id="1ed4b-106">Bu konu, bir self servis ilkesinin nasıl güncelleştireceğinizi açıklar.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-106">This topic explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1ed4b-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1ed4b-107">Prerequisites</span></span>

- <span data-ttu-id="1ed4b-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1ed4b-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-109">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="1ed4b-110">C\#</span><span class="sxs-lookup"><span data-stu-id="1ed4b-110">C\#</span></span>

<span data-ttu-id="1ed4b-111">Self Servis ilkesini silmek için:</span><span class="sxs-lookup"><span data-stu-id="1ed4b-111">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="1ed4b-112">İlkelerdeki işlemlere bir arabirim almak için, varlık tanımlayıcısıyla [**ıaggregatepartner. SelfServePolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-112">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="1ed4b-113">Self Servis ilkesini silmek için [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) veya [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-113">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="1ed4b-114">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="1ed4b-114">For an example, see the following:</span></span>

- <span data-ttu-id="1ed4b-115">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1ed4b-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1ed4b-116">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="1ed4b-116">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="1ed4b-117">Sınıf: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="1ed4b-117">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1ed4b-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1ed4b-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1ed4b-119">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1ed4b-119">Request syntax</span></span>

| <span data-ttu-id="1ed4b-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1ed4b-120">Method</span></span>  | <span data-ttu-id="1ed4b-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1ed4b-121">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="1ed4b-122">**SILMELI**</span><span class="sxs-lookup"><span data-stu-id="1ed4b-122">**DELETE**</span></span> | <span data-ttu-id="1ed4b-123">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="1ed4b-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="1ed4b-124">**URI parametresi**</span><span class="sxs-lookup"><span data-stu-id="1ed4b-124">**URI parameter**</span></span>

<span data-ttu-id="1ed4b-125">Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="1ed4b-126">Ad</span><span class="sxs-lookup"><span data-stu-id="1ed4b-126">Name</span></span>                       | <span data-ttu-id="1ed4b-127">Tür</span><span class="sxs-lookup"><span data-stu-id="1ed4b-127">Type</span></span>         | <span data-ttu-id="1ed4b-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1ed4b-128">Required</span></span> | <span data-ttu-id="1ed4b-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1ed4b-129">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="1ed4b-130">**SelfServePolicy kimliği**</span><span class="sxs-lookup"><span data-stu-id="1ed4b-130">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="1ed4b-131">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="1ed4b-131">**string**</span></span>   | <span data-ttu-id="1ed4b-132">Yes</span><span class="sxs-lookup"><span data-stu-id="1ed4b-132">Yes</span></span>      | <span data-ttu-id="1ed4b-133">Self Servis ilkesini tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-133">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="1ed4b-134">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1ed4b-134">Request headers</span></span>

- <span data-ttu-id="1ed4b-135">İstek KIMLIĞI ve bağıntı KIMLIĞI gereklidir.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-135">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="1ed4b-136">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="1ed4b-136">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="1ed4b-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1ed4b-137">Request body</span></span>

<span data-ttu-id="1ed4b-138">Yok.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-138">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1ed4b-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1ed4b-139">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 789
Connection: Keep-Alive

```

## <a name="rest-response"></a><span data-ttu-id="1ed4b-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1ed4b-140">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1ed4b-141">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1ed4b-141">Response success and error codes</span></span>

<span data-ttu-id="1ed4b-142">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1ed4b-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1ed4b-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1ed4b-144">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1ed4b-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1ed4b-145">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1ed4b-145">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
