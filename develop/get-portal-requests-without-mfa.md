---
title: MFA olmadan portal istekleri alma
description: Iş ortağı REST API kullanarak Multi-Factor Authentication (MFA) olmadan kullanıcı isteklerinin bir listesini alın.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: fd350aa3301f00926942ae6c6af359b0d0edc423
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769076"
---
# <a name="get-portal-requests-without-mfa"></a><span data-ttu-id="319a2-103">MFA olmadan portal istekleri alma</span><span class="sxs-lookup"><span data-stu-id="319a2-103">Get portal requests without MFA</span></span>

<span data-ttu-id="319a2-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="319a2-104">Applies to:</span></span>

- <span data-ttu-id="319a2-105">İş Ortağı Merkezi API’si</span><span class="sxs-lookup"><span data-stu-id="319a2-105">Partner Center API</span></span>

<span data-ttu-id="319a2-106">Bu makalede, çok faktörlü kimlik doğrulamasını (MFA) tamamlamadan Iş Ortağı Merkezi portalına erişen kullanıcılardan gelen en son isteklerin listesinin nasıl alınacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="319a2-106">This article explains how to obtain a list of the most recent requests from users who access Partner Center portal without completing multi-factor authentication (MFA).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="319a2-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="319a2-107">Prerequisites</span></span>

- <span data-ttu-id="319a2-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="319a2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="319a2-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="319a2-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="319a2-110">REST isteği</span><span class="sxs-lookup"><span data-stu-id="319a2-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="319a2-111">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="319a2-111">Request syntax</span></span>

| <span data-ttu-id="319a2-112">Yöntem</span><span class="sxs-lookup"><span data-stu-id="319a2-112">Method</span></span>  | <span data-ttu-id="319a2-113">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="319a2-113">Request URI</span></span>                                                  |
|---------|--------------------------------------------------------------|
| <span data-ttu-id="319a2-114">**Al**</span><span class="sxs-lookup"><span data-stu-id="319a2-114">**GET**</span></span> | <span data-ttu-id="319a2-115">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/nonmfakarmaşıkantpartnerpartnersorumluları</span><span class="sxs-lookup"><span data-stu-id="319a2-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/nonMfaCompliantPartnerPrincipals</span></span> |

### <a name="request-headers"></a><span data-ttu-id="319a2-116">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="319a2-116">Request headers</span></span>

- <span data-ttu-id="319a2-117">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="319a2-117">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="319a2-118">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="319a2-118">Request body</span></span>

<span data-ttu-id="319a2-119">Yok.</span><span class="sxs-lookup"><span data-stu-id="319a2-119">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="319a2-120">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="319a2-120">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/nonMfaCompliantPartnerPrincipals HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Accept: application/json
MS-RequestId: 8f489776-a3f3-47cb-91c3-538e1f70f560
MS-CorrelationId: e72e1dc3-4abd-4ce0-908b-d23fdaedcb28
Connection: keep-alive

```

## <a name="rest-response"></a><span data-ttu-id="319a2-121">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="319a2-121">REST response</span></span>

<span data-ttu-id="319a2-122">Başarılı olursa, bu yöntem yanıt gövdesinde [Portal istek](mfa-resources.md#portal-request-without-mfa) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="319a2-122">If successful, this method returns a collection of [Portal request](mfa-resources.md#portal-request-without-mfa) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="319a2-123">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="319a2-123">Response success and error codes</span></span>

<span data-ttu-id="319a2-124">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="319a2-124">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="319a2-125">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="319a2-125">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="319a2-126">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="319a2-126">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="319a2-127">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="319a2-127">Response example</span></span>

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
