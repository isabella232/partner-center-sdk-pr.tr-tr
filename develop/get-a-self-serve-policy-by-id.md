---
title: Kimlikle self servis ilkesi elde etme
description: Kimliğini kullanarak belirtilen self servis ilkesi alır.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 074d7ba65c7aab91687a67f50e871cee913fc2bb
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873845"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="e97ec-103">Kimlikle self servis ilkesi elde etme</span><span class="sxs-lookup"><span data-stu-id="e97ec-103">Get a self-serve policy by ID</span></span>

<span data-ttu-id="e97ec-104">Kimliğini kullanarak belirtilen self servis ilkesi alır.</span><span class="sxs-lookup"><span data-stu-id="e97ec-104">Gets the specified self-serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e97ec-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e97ec-105">Prerequisites</span></span>

- <span data-ttu-id="e97ec-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e97ec-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e97ec-107">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e97ec-107">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="e97ec-108">Self servis ilke kimliği.</span><span class="sxs-lookup"><span data-stu-id="e97ec-108">A self-serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="e97ec-109">Örnekler</span><span class="sxs-lookup"><span data-stu-id="e97ec-109">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="e97ec-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST İsteği</span><span class="sxs-lookup"><span data-stu-id="e97ec-110"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="e97ec-111">**İstek söz dizimi**</span><span class="sxs-lookup"><span data-stu-id="e97ec-111">**Request syntax**</span></span>

| <span data-ttu-id="e97ec-112">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e97ec-112">Method</span></span>  | <span data-ttu-id="e97ec-113">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e97ec-113">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="e97ec-114">**Al**</span><span class="sxs-lookup"><span data-stu-id="e97ec-114">**GET**</span></span> | <span data-ttu-id="e97ec-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e97ec-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="e97ec-116">**URI parametresi**</span><span class="sxs-lookup"><span data-stu-id="e97ec-116">**URI parameter**</span></span>

<span data-ttu-id="e97ec-117">Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e97ec-117">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="e97ec-118">Ad</span><span class="sxs-lookup"><span data-stu-id="e97ec-118">Name</span></span>                       | <span data-ttu-id="e97ec-119">Tür</span><span class="sxs-lookup"><span data-stu-id="e97ec-119">Type</span></span>         | <span data-ttu-id="e97ec-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e97ec-120">Required</span></span> | <span data-ttu-id="e97ec-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e97ec-121">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="e97ec-122">**SelfServePolicy-id**</span><span class="sxs-lookup"><span data-stu-id="e97ec-122">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="e97ec-123">**string**</span><span class="sxs-lookup"><span data-stu-id="e97ec-123">**string**</span></span>   | <span data-ttu-id="e97ec-124">Yes</span><span class="sxs-lookup"><span data-stu-id="e97ec-124">Yes</span></span>      | <span data-ttu-id="e97ec-125">Self servis ilkesi tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="e97ec-125">A string that identifies the self-serve policy.</span></span>                 |

<span data-ttu-id="e97ec-126">**İstek üst bilgileri**</span><span class="sxs-lookup"><span data-stu-id="e97ec-126">**Request headers**</span></span>

- <span data-ttu-id="e97ec-127">Daha fazla bilgi için [bkz. Üst Bilgiler.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e97ec-127">For more information, see [Headers](headers.md).</span></span>

<span data-ttu-id="e97ec-128">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="e97ec-128">**Request body**</span></span>

<span data-ttu-id="e97ec-129">Yok.</span><span class="sxs-lookup"><span data-stu-id="e97ec-129">None.</span></span>

<span data-ttu-id="e97ec-130">**İstek örneği**</span><span class="sxs-lookup"><span data-stu-id="e97ec-130">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="e97ec-131">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e97ec-131">REST response</span></span>

<span data-ttu-id="e97ec-132">Başarılı olursa, yanıt gövdesi bir [SelfServePolicy kaynağı](self-serve-policy-resources.md#selfservepolicy) içerir.</span><span class="sxs-lookup"><span data-stu-id="e97ec-132">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="e97ec-133">**Yanıt başarı ve hata kodları**</span><span class="sxs-lookup"><span data-stu-id="e97ec-133">**Response success and error codes**</span></span>

<span data-ttu-id="e97ec-134">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="e97ec-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e97ec-135">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e97ec-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e97ec-136">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e97ec-136">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="e97ec-137">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="e97ec-137">This method returns the following error codes:</span></span>

| <span data-ttu-id="e97ec-138">HTTP Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="e97ec-138">HTTP Status Code</span></span>     | <span data-ttu-id="e97ec-139">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="e97ec-139">Error code</span></span>   | <span data-ttu-id="e97ec-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e97ec-140">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="e97ec-141">404</span><span class="sxs-lookup"><span data-stu-id="e97ec-141">404</span></span>                  | <span data-ttu-id="e97ec-142">600039</span><span class="sxs-lookup"><span data-stu-id="e97ec-142">600039</span></span>       | <span data-ttu-id="e97ec-143">Self servis ilkesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="e97ec-143">Self-serve policy not found.</span></span>                                                     |

<span data-ttu-id="e97ec-144">**Yanıt örneği**</span><span class="sxs-lookup"><span data-stu-id="e97ec-144">**Response example**</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

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