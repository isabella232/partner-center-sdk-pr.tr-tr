---
title: İş ortağı lisans kullanım bilgilerini alma
description: Tüm müşterileri dahil etmek için iş ortağı lisansları kullanım bilgilerini toplama.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f3d05d61ac4f2c90b0d8a4bfd93fe24e94bd5c1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445604"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="f17d4-103">İş ortağı lisans kullanım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="f17d4-103">Get partner licenses usage information</span></span>

<span data-ttu-id="f17d4-104">Tüm müşterileri dahil etmek için iş ortağı lisansları kullanım bilgilerini toplama.</span><span class="sxs-lookup"><span data-stu-id="f17d4-104">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="f17d4-105">Bu senaryo, Get licenses usage information ( Lisans kullanım [bilgilerini al) ile yenisi kullanılır.](get-licenses-usage-information.md)</span><span class="sxs-lookup"><span data-stu-id="f17d4-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f17d4-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f17d4-106">Prerequisites</span></span>

<span data-ttu-id="f17d4-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f17d4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f17d4-108">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="f17d4-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="f17d4-109">C\#</span><span class="sxs-lookup"><span data-stu-id="f17d4-109">C\#</span></span>

<span data-ttu-id="f17d4-110">Lisans dağıtımında toplu verileri almak için, önce [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) özelliğinden iş ortağı düzeyinde analiz toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="f17d4-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="f17d4-111">Ardından Lisanslar özelliğinden iş ortağı düzeyinde lisanslar analiz koleksiyonuna [**bir arabirim**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) alın.</span><span class="sxs-lookup"><span data-stu-id="f17d4-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="f17d4-112">Son olarak, lisans kullanımıyla ilgili toplu verileri almak için [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f17d4-112">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="f17d4-113">Yöntem başarılı olursa [**PartnerLicensesUsageInsights nesnelerinin bir koleksiyonunu elde**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) edersiniz.</span><span class="sxs-lookup"><span data-stu-id="f17d4-113">If the method succeeds, you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="f17d4-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f17d4-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f17d4-115">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="f17d4-115">Request syntax</span></span>

| <span data-ttu-id="f17d4-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f17d4-116">Method</span></span>  | <span data-ttu-id="f17d4-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f17d4-117">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="f17d4-118">**Al**</span><span class="sxs-lookup"><span data-stu-id="f17d4-118">**GET**</span></span> | <span data-ttu-id="f17d4-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f17d4-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f17d4-120">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f17d4-120">Request headers</span></span>

<span data-ttu-id="f17d4-121">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f17d4-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f17d4-122">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f17d4-122">Request body</span></span>

<span data-ttu-id="f17d4-123">Yok.</span><span class="sxs-lookup"><span data-stu-id="f17d4-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f17d4-124">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f17d4-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f17d4-125">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f17d4-125">REST response</span></span>

<span data-ttu-id="f17d4-126">Başarılı olursa yanıt gövdesi, kullanılan lisanslar hakkında bilgi sağlayan [partnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) kaynaklarının bir koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f17d4-126">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f17d4-127">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f17d4-127">Response success and error codes</span></span>

<span data-ttu-id="f17d4-128">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="f17d4-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f17d4-129">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f17d4-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f17d4-130">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f17d4-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f17d4-131">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f17d4-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1156
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CV: wk0/vjugzEe0Z9cv.0
MS-ServerId: 101112012
Date: Wed, 15 Mar 2017 01:18:26 GMT

{
    "totalCount": 5,
    "items": [{
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Microsoft Dynamics CRM",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }, {
            "proratedLicensesUsagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
