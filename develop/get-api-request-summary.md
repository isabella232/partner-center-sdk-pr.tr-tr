---
title: MFA benimseme durumunu al
description: Iş ortağı REST API kullanarak her iş ortağı için Multi-Factor Authentication benimseme durumunun bir listesini alın.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9b8848c2a4531dd6609f86aae6876cec436eeea9
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760530"
---
# <a name="get-mfa-adoption-status"></a><span data-ttu-id="fa044-103">MFA benimseme durumunu al</span><span class="sxs-lookup"><span data-stu-id="fa044-103">Get MFA adoption status</span></span>

<span data-ttu-id="fa044-104">**Uygulama hedefi**: Iş Ortağı Merkezi API</span><span class="sxs-lookup"><span data-stu-id="fa044-104">**Applies to**: Partner Center API</span></span>

<span data-ttu-id="fa044-105">Bu makalede, bir kiracının içindeki her ortağın Multi-Factor Authentication (MFA) benimseme durumunun nasıl alınacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="fa044-105">This article explains how to get the multi-factor authentication (MFA) adoption status for each partner within a tenant.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fa044-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fa044-106">Prerequisites</span></span>

- <span data-ttu-id="fa044-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fa044-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fa044-108">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="fa044-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="fa044-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="fa044-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fa044-110">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="fa044-110">Request syntax</span></span>

| <span data-ttu-id="fa044-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="fa044-111">Method</span></span>  | <span data-ttu-id="fa044-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="fa044-112">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="fa044-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="fa044-113">**GET**</span></span> | <span data-ttu-id="fa044-114">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/applicationmfabenimsetionstatus></span><span class="sxs-lookup"><span data-stu-id="fa044-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/applicationmfaadoptionstatus></span></span> |

### <a name="request-headers"></a><span data-ttu-id="fa044-115">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="fa044-115">Request headers</span></span>

- <span data-ttu-id="fa044-116">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="fa044-116">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fa044-117">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="fa044-117">Request body</span></span>

<span data-ttu-id="fa044-118">Yok.</span><span class="sxs-lookup"><span data-stu-id="fa044-118">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="fa044-119">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="fa044-119">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/applicationmfaadoptionstatus HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="fa044-120">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="fa044-120">REST response</span></span>

<span data-ttu-id="fa044-121">Başarılı olursa, bu yöntem yanıt gövdesinde uygulama kaynakları [tarafından özetlenen bir API isteği](mfa-resources.md#api-request-summarized-by-application) koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="fa044-121">If successful, this method returns a collection of [API request summarized by Application](mfa-resources.md#api-request-summarized-by-application) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fa044-122">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="fa044-122">Response success and error codes</span></span>

<span data-ttu-id="fa044-123">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="fa044-123">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fa044-124">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fa044-124">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fa044-125">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="fa044-125">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fa044-126">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="fa044-126">Response example</span></span>

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
