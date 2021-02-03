---
title: Kimliğe göre bir self servis ilkesi alma
description: Belirtilen self servis ilkesini KIMLIĞINI kullanarak alır.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ec01d0d9b7c3858cdacf1dbaad3b2b0bb7b6a1a4
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769088"
---
# <a name="get-a-self-serve-policy-by-id"></a><span data-ttu-id="89dcb-103">Kimliğe göre bir self servis ilkesi alma</span><span class="sxs-lookup"><span data-stu-id="89dcb-103">Get a self serve policy by ID</span></span>

<span data-ttu-id="89dcb-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="89dcb-104">**Applies To**</span></span>

- <span data-ttu-id="89dcb-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="89dcb-105">Partner Center</span></span>

<span data-ttu-id="89dcb-106">Belirtilen self servis ilkesini KIMLIĞINI kullanarak alır.</span><span class="sxs-lookup"><span data-stu-id="89dcb-106">Gets the specified self serve policy using its ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89dcb-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="89dcb-107">Prerequisites</span></span>

- <span data-ttu-id="89dcb-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="89dcb-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="89dcb-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="89dcb-109">This scenario supports authentication with App+User credentials.</span></span>
- <span data-ttu-id="89dcb-110">Self Servis ilke KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="89dcb-110">A self serve policy ID.</span></span>

## <a name="examples"></a><span data-ttu-id="89dcb-111">Örnekler</span><span class="sxs-lookup"><span data-stu-id="89dcb-111">Examples</span></span>


## <a name="span-idrest_requestspan-idrest_requestspan-idrest_requestrest-request"></a><span data-ttu-id="89dcb-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Isteği</span><span class="sxs-lookup"><span data-stu-id="89dcb-112"><span id="REST_Request"/><span id="rest_request"/><span id="REST_REQUEST"/>REST Request</span></span>

<span data-ttu-id="89dcb-113">**İstek sözdizimi**</span><span class="sxs-lookup"><span data-stu-id="89dcb-113">**Request syntax**</span></span>

| <span data-ttu-id="89dcb-114">Yöntem</span><span class="sxs-lookup"><span data-stu-id="89dcb-114">Method</span></span>  | <span data-ttu-id="89dcb-115">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="89dcb-115">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="89dcb-116">**Al**</span><span class="sxs-lookup"><span data-stu-id="89dcb-116">**GET**</span></span> | <span data-ttu-id="89dcb-117">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="89dcb-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/SelfServePolicy/{id} HTTP/1.1</span></span> |

<span data-ttu-id="89dcb-118">**URI parametresi**</span><span class="sxs-lookup"><span data-stu-id="89dcb-118">**URI parameter**</span></span>

<span data-ttu-id="89dcb-119">Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="89dcb-119">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="89dcb-120">Ad</span><span class="sxs-lookup"><span data-stu-id="89dcb-120">Name</span></span>                       | <span data-ttu-id="89dcb-121">Tür</span><span class="sxs-lookup"><span data-stu-id="89dcb-121">Type</span></span>         | <span data-ttu-id="89dcb-122">Gerekli</span><span class="sxs-lookup"><span data-stu-id="89dcb-122">Required</span></span> | <span data-ttu-id="89dcb-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89dcb-123">Description</span></span>                                                     |
|----------------------------|--------------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="89dcb-124">**SelfServePolicy kimliği**</span><span class="sxs-lookup"><span data-stu-id="89dcb-124">**SelfServePolicy-id**</span></span>     | <span data-ttu-id="89dcb-125">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="89dcb-125">**string**</span></span>   | <span data-ttu-id="89dcb-126">Yes</span><span class="sxs-lookup"><span data-stu-id="89dcb-126">Yes</span></span>      | <span data-ttu-id="89dcb-127">Self Servis ilkesini tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="89dcb-127">A string that identifies the self serve policy.</span></span>                 |

<span data-ttu-id="89dcb-128">**İstek üst bilgileri**</span><span class="sxs-lookup"><span data-stu-id="89dcb-128">**Request headers**</span></span>

- <span data-ttu-id="89dcb-129">Daha fazla bilgi için bkz. [üst](headers.md) bilgiler.</span><span class="sxs-lookup"><span data-stu-id="89dcb-129">See [Headers](headers.md) for more information.</span></span>

<span data-ttu-id="89dcb-130">**İstek gövdesi**</span><span class="sxs-lookup"><span data-stu-id="89dcb-130">**Request body**</span></span>

<span data-ttu-id="89dcb-131">Yok.</span><span class="sxs-lookup"><span data-stu-id="89dcb-131">None.</span></span>

<span data-ttu-id="89dcb-132">**İstek örneği**</span><span class="sxs-lookup"><span data-stu-id="89dcb-132">**Request example**</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/SelfServePolicy/634f6379-ad54-449b-9821-564f737158ab_0431a72c-7d8a-4393-b25e-ef63f5efb415 HTTP/1.1
Authorization: Bearer  <token>
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="89dcb-133">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="89dcb-133">REST response</span></span>

<span data-ttu-id="89dcb-134">Başarılı olursa, yanıt gövdesi bir [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="89dcb-134">If successful, the response body contains a [SelfServePolicy](self-serve-policy-resources.md#selfservepolicy) resource.</span></span>

<span data-ttu-id="89dcb-135">**Yanıt başarısı ve hata kodları**</span><span class="sxs-lookup"><span data-stu-id="89dcb-135">**Response success and error codes**</span></span>

<span data-ttu-id="89dcb-136">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="89dcb-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89dcb-137">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="89dcb-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89dcb-138">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="89dcb-138">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="89dcb-139">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="89dcb-139">This method returns the following error codes:</span></span>

| <span data-ttu-id="89dcb-140">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="89dcb-140">HTTP Status Code</span></span>     | <span data-ttu-id="89dcb-141">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="89dcb-141">Error code</span></span>   | <span data-ttu-id="89dcb-142">Description</span><span class="sxs-lookup"><span data-stu-id="89dcb-142">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="89dcb-143">404</span><span class="sxs-lookup"><span data-stu-id="89dcb-143">404</span></span>                  | <span data-ttu-id="89dcb-144">600039</span><span class="sxs-lookup"><span data-stu-id="89dcb-144">600039</span></span>       | <span data-ttu-id="89dcb-145">Self Servis ilkesi bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="89dcb-145">Self serve policy not found.</span></span>                                                     |

<span data-ttu-id="89dcb-146">**Yanıt örneği**</span><span class="sxs-lookup"><span data-stu-id="89dcb-146">**Response example**</span></span>

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