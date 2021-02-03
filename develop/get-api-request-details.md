---
title: Tüm iş ortağı kullanıcı isteklerinin bir listesini alın
description: Iş ortağı REST API kullanarak tüm iş ortağı kullanıcı isteklerinin bir listesini alın.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
author: cychua
ms.author: cychua
ms.openlocfilehash: 43b1e3d4a6220ac8adba8eed0389395113072288
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768752"
---
# <a name="get-app-and-user-api-requests"></a><span data-ttu-id="c3108-103">Uygulama ve Kullanıcı API 'SI isteklerini al</span><span class="sxs-lookup"><span data-stu-id="c3108-103">Get App and User API requests</span></span>

<span data-ttu-id="c3108-104">Aşağıdakiler cihazlar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="c3108-104">Applies to:</span></span>

- <span data-ttu-id="c3108-105">İş Ortağı Merkezi API’si</span><span class="sxs-lookup"><span data-stu-id="c3108-105">Partner Center API</span></span>

<span data-ttu-id="c3108-106">Bu makalede REST API 'Leri kullanarak bir kiracının içindeki tüm iş ortağı kullanıcı isteklerinin listesinin nasıl alınacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c3108-106">This article explains how to obtain a list of all partner user requests within a tenant using REST APIs.</span></span>

 > [!NOTE]
 > <span data-ttu-id="c3108-107">Bu API yalnızca en fazla 10.000 sınırı olan APP + Kullanıcı kimlik bilgileri tarafından yapılan en son API isteklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="c3108-107">This API only returns the most recent API requests made by APP + User credential with maximum 10K limit.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3108-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c3108-108">Prerequisites</span></span>

- <span data-ttu-id="c3108-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c3108-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c3108-110">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="c3108-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="c3108-111">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c3108-111">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c3108-112">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c3108-112">Request syntax</span></span>

| <span data-ttu-id="c3108-113">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c3108-113">Method</span></span>  | <span data-ttu-id="c3108-114">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c3108-114">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="c3108-115">**Al**</span><span class="sxs-lookup"><span data-stu-id="c3108-115">**GET**</span></span> | <span data-ttu-id="c3108-116">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/partnerrequests</span><span class="sxs-lookup"><span data-stu-id="c3108-116">[*{baseURL}*](partner-center-rest-urls.md)/v1/partnerRequests</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c3108-117">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c3108-117">Request headers</span></span>

- <span data-ttu-id="c3108-118">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üst bilgileri](headers.md) .</span><span class="sxs-lookup"><span data-stu-id="c3108-118">See [Partner Center REST headers](headers.md) for more information.</span></span>

### <a name="request-body"></a><span data-ttu-id="c3108-119">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c3108-119">Request body</span></span>

<span data-ttu-id="c3108-120">Yok.</span><span class="sxs-lookup"><span data-stu-id="c3108-120">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c3108-121">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c3108-121">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/partnerRequests HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Type: application/json
```

## <a name="rest-response"></a><span data-ttu-id="c3108-122">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c3108-122">REST response</span></span>

<span data-ttu-id="c3108-123">Başarılı olursa, bu yöntem yanıt gövdesinde bir [API isteği ayrıntıları](mfa-resources.md#api-request-details) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="c3108-123">If successful, this method returns a collection of [API request details](mfa-resources.md#api-request-details) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c3108-124">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c3108-124">Response success and error codes</span></span>

<span data-ttu-id="c3108-125">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c3108-125">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c3108-126">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c3108-126">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c3108-127">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c3108-127">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c3108-128">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c3108-128">Response example</span></span>

``` http
HTTP/1.1 200 OK
Content-Length: 2960
Content-Type: application/json
MS-CorrelationId: 4cb80cbe-566b-4d8b-8b8f-af1454b73089
MS-RequestId: 566330a7-1e4b-4848-9c23-f135c70fd810
Date: Thu, 21 May 2020 22:29:17 GMT
{
    "totalCount": 2,
    "items": [
        {
            "requestId": "6c583d8d-46cd-420c-ae3d-35b6dfdcdb21",
            "correlationId": "",
            "operationName": "Get /v{version}/nonMfaCompliantPartnerPrincipals",
            "requestDateTime": "2020-05-21T21:02:10.31",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "c69854fe-5fb4-4527-a28f-f24f1acaffd6",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "admin@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": true
        },
        {
            "requestId": "09f8e434-a9ce-43ea-a9ac-270fbb22371a",
            "correlationId": "",
            "operationName": "Get /v{version}/customers/{customer_id}/subscriptions?order_id={order_id_value}&mpn_id={mpn_id_value}",
            "requestDateTime": "2020-05-21T22:18:35.73",
            "sourceIpAddress": "13.88.20.150",
            "objectId": "adc77aa5-7968-4c57-9f48-361018265c1a",
            "tenantId": "6e6aef4a-4ca9-40a8-b5bf-b53a1923c540",
            "upn": "portalnonmfa@yourdomain.onmicrosoft.com",
            "applicationId": "60a00bf2-0644-4279-83b3-87ddf96f2509",
            "mfaCompliant": false
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
