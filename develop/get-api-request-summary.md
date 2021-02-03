---
title: MFA benimseme durumunu al
description: Iş ortağı REST API kullanarak her iş ortağı için Multi-Factor Authentication benimseme durumunun bir listesini alın.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: f82d163b704323c81e2948b78eb9b9d1a14ddc52
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769022"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="500b6-103">MFA benimseme durumunu al</span><span class="sxs-lookup"><span data-stu-id="500b6-103">Get MFA adoption status</span></span>

<span data-ttu-id="500b6-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="500b6-104">Applies to:</span></span>

- <span data-ttu-id="500b6-105">İş Ortağı Merkezi API’si</span><span class="sxs-lookup"><span data-stu-id="500b6-105">Partner Center API</span></span>

<span data-ttu-id="500b6-106">Bu makalede, bir kiracının içindeki her ortağın Multi-Factor Authentication (MFA) benimseme durumunun nasıl alınacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="500b6-106">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="500b6-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="500b6-107">Prerequisites</span></span>

- <span data-ttu-id="500b6-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="500b6-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="500b6-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="500b6-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="500b6-110">REST isteği</span><span class="sxs-lookup"><span data-stu-id="500b6-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="500b6-111">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="500b6-111">Request syntax</span></span>

| <span data-ttu-id="500b6-112">Yöntem</span><span class="sxs-lookup"><span data-stu-id="500b6-112">Method</span></span>  | <span data-ttu-id="500b6-113">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="500b6-113">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="500b6-114">**Al**</span><span class="sxs-lookup"><span data-stu-id="500b6-114">**GET**</span></span> | <span data-ttu-id="500b6-115">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/applicationmfabenimsetionstatus></span><span class="sxs-lookup"><span data-stu-id="500b6-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="500b6-116">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="500b6-116">Request headers</span></span>

- <span data-ttu-id="500b6-117">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="500b6-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="500b6-118">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="500b6-118">Request body</span></span>

<span data-ttu-id="500b6-119">Yok.</span><span class="sxs-lookup"><span data-stu-id="500b6-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="500b6-120">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="500b6-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="500b6-121">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="500b6-121">REST response</span></span>

<span data-ttu-id="500b6-122">Başarılı olursa, bu yöntem yanıt gövdesinde uygulama kaynakları [tarafından özetlenen bir API isteği](mfa-resources.md#api-request-summarized-by-application) koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="500b6-122">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="500b6-123">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="500b6-123">Response success and error codes</span></span>

<span data-ttu-id="500b6-124">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="500b6-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="500b6-125">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="500b6-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="500b6-126">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="500b6-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="500b6-127">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="500b6-127">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 313
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
[
    {
        "loginDate": "2020-05-20",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 7,
        "applicationId": "14f38d7d-c4fc-448a-b2df-0fc60e75465a",
        "applicationName": ""
    },
    {
        "loginDate": "2020-05-19",
        "mfaCompliantRequestCount": 7,
        "totalRequestCount": 14,
        "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
        "applicationName": ""
    }
]
```
