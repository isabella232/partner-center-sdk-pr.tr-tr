---
title: MFA olmadan portal istekleri alma
description: İş Ortağı kimlik doğrulamasını kullanarak çok faktörlü kimlik doğrulaması (MFA) olmadan kullanıcı isteklerinin REST API.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 41627751d3402d7712d96c15c4281a25ed9a44a7
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445587"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="50d8f-103">MFA olmadan portal istekleri alma</span><span class="sxs-lookup"><span data-stu-id="50d8f-103">Get portal requests without MFA</span></span>

<span data-ttu-id="50d8f-104">Bu makalede, çok faktörlü kimlik doğrulamasını (MFA) tamamlamadan İş Ortağı Merkezi kullanıcılardan en son isteklerin listesini alma işlemi açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="50d8f-104">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="50d8f-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="50d8f-105">Prerequisites</span></span>

- <span data-ttu-id="50d8f-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="50d8f-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="50d8f-107">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="50d8f-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="50d8f-108">REST isteği</span><span class="sxs-lookup"><span data-stu-id="50d8f-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="50d8f-109">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="50d8f-109">Request syntax</span></span>

| <span data-ttu-id="50d8f-110">Yöntem</span><span class="sxs-lookup"><span data-stu-id="50d8f-110">Method</span></span>  | <span data-ttu-id="50d8f-111">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="50d8f-111">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="50d8f-112">**Al**</span><span class="sxs-lookup"><span data-stu-id="50d8f-112">**GET**</span></span> | <span data-ttu-id="50d8f-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span><span class="sxs-lookup"><span data-stu-id="50d8f-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="50d8f-114">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="50d8f-114">Request headers</span></span>

- <span data-ttu-id="50d8f-115">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="50d8f-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="50d8f-116">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="50d8f-116">Request body</span></span>

<span data-ttu-id="50d8f-117">Yok.</span><span class="sxs-lookup"><span data-stu-id="50d8f-117">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="50d8f-118">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="50d8f-118">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="50d8f-119">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="50d8f-119">REST response</span></span>

<span data-ttu-id="50d8f-120">Başarılı olursa, bu yöntem yanıt gövdesinde [Portal isteği](mfa-resources.md#portal-request-without-mfa) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="50d8f-120">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="50d8f-121">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="50d8f-121">Response success and error codes</span></span>

<span data-ttu-id="50d8f-122">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="50d8f-122">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="50d8f-123">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="50d8f-123">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="50d8f-124">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="50d8f-124">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="50d8f-125">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="50d8f-125">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 296
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 23 Apr 2020 22:10:30 GMT
{
    "totalCount": 1,
    "items": [
        {
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "lastNonMfaCompliantRequestDateTime": "2020-04-21T22:09:53.051"
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
