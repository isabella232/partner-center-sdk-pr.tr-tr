---
title: İş ortağı lisans kullanım bilgilerini alma
description: Tüm müşterileri dahil etmek için toplanan iş ortağı lisansları kullanım bilgilerini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d003fb269a3421b8efd8cebe8f396f97599a10
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769904"
---
# <a name="get-partner-licenses-usage-information"></a><span data-ttu-id="44a61-103">İş ortağı lisans kullanım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="44a61-103">Get partner licenses usage information</span></span>

<span data-ttu-id="44a61-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="44a61-104">**Applies To**</span></span>

- <span data-ttu-id="44a61-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="44a61-105">Partner Center</span></span>

<span data-ttu-id="44a61-106">Tüm müşterileri dahil etmek için toplanan iş ortağı lisansları kullanım bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="44a61-106">How to get partner licenses usage information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="44a61-107">Bu senaryo, [lisans kullanım bilgilerinin yerini alır](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="44a61-107">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44a61-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="44a61-108">Prerequisites</span></span>

<span data-ttu-id="44a61-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="44a61-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44a61-110">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="44a61-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="44a61-111">C\#</span><span class="sxs-lookup"><span data-stu-id="44a61-111">C\#</span></span>

<span data-ttu-id="44a61-112">Lisans dağıtımında toplanmış verileri almak için ilk olarak [**ıaggregatepartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) özelliğinden iş ortağı düzeyi Analizi toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="44a61-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="44a61-113">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) özelliğinden iş ortağı düzeyi lisans Analizi koleksiyonuna bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="44a61-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="44a61-114">Son olarak, lisansların kullanımıyla ilgili toplanan verileri almak için [**Usage. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="44a61-114">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="44a61-115">Yöntem başarılı olursa, [**Partnerlicensesusageınsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) nesnelerinin bir koleksiyonunu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="44a61-115">If the method succeeds you'll get a collection of [**PartnerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesUsageAnalytics = partnerOperations.Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="44a61-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="44a61-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44a61-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="44a61-117">Request syntax</span></span>

| <span data-ttu-id="44a61-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="44a61-118">Method</span></span>  | <span data-ttu-id="44a61-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="44a61-119">Request URI</span></span>                                                                      |
|---------|----------------------------------------------------------------------------------|
| <span data-ttu-id="44a61-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="44a61-120">**GET**</span></span> | <span data-ttu-id="44a61-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/analiz Tics/licenses/Usage http/1.1</span><span class="sxs-lookup"><span data-stu-id="44a61-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="44a61-122">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="44a61-122">Request headers</span></span>

<span data-ttu-id="44a61-123">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="44a61-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44a61-124">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="44a61-124">Request body</span></span>

<span data-ttu-id="44a61-125">Yok.</span><span class="sxs-lookup"><span data-stu-id="44a61-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="44a61-126">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="44a61-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6b588e9b-1d02-471a-bce2-79374497c24e
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="44a61-127">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="44a61-127">REST response</span></span>

<span data-ttu-id="44a61-128">Başarılı olursa, yanıt gövdesi, kullanılan lisanslar hakkında bilgi sağlayan bir iş [ortağı lisans](analytics-resources.md#partnerlicensesusageinsights) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="44a61-128">If successful, the response body contains a collection of [PartnerLicensesUsageInsights](analytics-resources.md#partnerlicensesusageinsights) resources that provide information about the licenses used.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44a61-129">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="44a61-129">Response success and error codes</span></span>

<span data-ttu-id="44a61-130">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="44a61-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44a61-131">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="44a61-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44a61-132">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="44a61-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44a61-133">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="44a61-133">Response example</span></span>

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
