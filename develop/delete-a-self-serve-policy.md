---
title: Self servis ilkesi silme
description: Self servis ilkesi silme.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 063cf98d4c78e82622e486427baeb1a5721715e5
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973103"
---
# <a name="delete-a-selfservepolicy"></a><span data-ttu-id="33251-103">SelfServePolicy silme</span><span class="sxs-lookup"><span data-stu-id="33251-103">Delete a SelfServePolicy</span></span>

<span data-ttu-id="33251-104">Bu makalede self servis ilkesi güncelleştirme işlemi açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="33251-104">This article explains how to update a self-serve policy.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="33251-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="33251-105">Prerequisites</span></span>

- <span data-ttu-id="33251-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="33251-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="33251-107">Bu senaryo, Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="33251-107">This scenario supports authentication with Application+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="33251-108">C\#</span><span class="sxs-lookup"><span data-stu-id="33251-108">C\#</span></span>

<span data-ttu-id="33251-109">Self servis ilkesi silmek için:</span><span class="sxs-lookup"><span data-stu-id="33251-109">To delete a self-serve policy:</span></span>

1. <span data-ttu-id="33251-110">İlkeler üzerinde işlemlere bir arabirim almak için varlık tanımlayıcısıyla [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="33251-110">Call the [**IAggregatePartner.SelfServePolicies.ById**](/dotnet/api/microsoft.store.partnercenter.iselfservepoliciescollection.byid) method with the entity identifier to retrieve an interface to operations on the policies.</span></span>

2. <span data-ttu-id="33251-111">Self servis [**ilkeyi**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) silmek için Delete veya [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="33251-111">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.SelfServePolicies.deleteasync) method to delete the self-serve policy.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
string policyId;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// deletes the self-serve policies
partnerOperations.SelfServePolicies.ById(policyId).Delete();
```

<span data-ttu-id="33251-112">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="33251-112">For an example, see the following:</span></span>

- <span data-ttu-id="33251-113">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="33251-113">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="33251-114">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="33251-114">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="33251-115">Sınıf: **DeleteSelfServePolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="33251-115">Class: **DeleteSelfServePolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="33251-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="33251-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="33251-117">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="33251-117">Request syntax</span></span>

| <span data-ttu-id="33251-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="33251-118">Method</span></span>  | <span data-ttu-id="33251-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="33251-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="33251-120">**Silmek**</span><span class="sxs-lookup"><span data-stu-id="33251-120">**DELETE**</span></span> | <span data-ttu-id="33251-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="33251-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="33251-122">**URI parametresi**</span><span class="sxs-lookup"><span data-stu-id="33251-122">**URI parameter**</span></span>

<span data-ttu-id="33251-123">Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="33251-123">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="33251-124">Ad</span><span class="sxs-lookup"><span data-stu-id="33251-124">Name</span></span>                       | <span data-ttu-id="33251-125">Tür</span><span class="sxs-lookup"><span data-stu-id="33251-125">Type</span></span>         | <span data-ttu-id="33251-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="33251-126">Required</span></span> | <span data-ttu-id="33251-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="33251-127">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="33251-128">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="33251-128">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="33251-129">**string**</span><span class="sxs-lookup"><span data-stu-id="33251-129">**string**</span></span>   | <span data-ttu-id="33251-130">Yes</span><span class="sxs-lookup"><span data-stu-id="33251-130">Yes</span></span>      | <span data-ttu-id="33251-131">Self servis ilkesi tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="33251-131">A string that identifies the self-serve policy.</span></span>                 |

### <a name="request-headers"></a><span data-ttu-id="33251-132">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="33251-132">Request headers</span></span>

- <span data-ttu-id="33251-133">İstek kimliği ve bağıntı kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="33251-133">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="33251-134">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="33251-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="33251-135">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="33251-135">Request body</span></span>

<span data-ttu-id="33251-136">Yok.</span><span class="sxs-lookup"><span data-stu-id="33251-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="33251-137">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="33251-137">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="33251-138">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="33251-138">REST response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="33251-139">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="33251-139">Response success and error codes</span></span>

<span data-ttu-id="33251-140">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="33251-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="33251-141">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="33251-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="33251-142">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="33251-142">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="33251-143">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="33251-143">Response example</span></span>

```http
HTTP/1.1 204 deleted
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
Date: Tue, 14 Feb 2017 20:06:02 GMT

```
