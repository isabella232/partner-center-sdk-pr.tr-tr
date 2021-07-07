---
title: Müşteri lisans kullanım bilgilerini alma
description: Belirli bir müşteri için lisans kullanım öngörüleri alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: cfec12d37ce4f5f50baad57bfd45770388f8a2dc
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446438"
---
# <a name="get-customer-licenses-usage-information"></a><span data-ttu-id="8603b-103">Müşteri lisans kullanım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="8603b-103">Get customer licenses usage information</span></span>

<span data-ttu-id="8603b-104">Belirli bir müşteri için lisans dağıtımı öngörülerini alma.</span><span class="sxs-lookup"><span data-stu-id="8603b-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="8603b-105">Bu senaryo, [lisans kullanım bilgilerinin yerini alır](get-licenses-usage-information.md).</span><span class="sxs-lookup"><span data-stu-id="8603b-105">This scenario is superceded by [Get licenses usage information](get-licenses-usage-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8603b-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8603b-106">Prerequisites</span></span>

<span data-ttu-id="8603b-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8603b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8603b-108">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="8603b-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="8603b-109">C\#</span><span class="sxs-lookup"><span data-stu-id="8603b-109">C\#</span></span>

<span data-ttu-id="8603b-110">Belirtilen bir müşteri için dağıtımda toplanan verileri almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="8603b-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="8603b-111">Ardından [**analiz**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) özelliğinden müşteri düzeyi Analizi toplama işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="8603b-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="8603b-112">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) özelliğinden müşteri düzeyi lisans Analizi koleksiyonuna bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="8603b-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="8603b-113">Son olarak, lisansların kullanımıyla ilgili toplanan verileri almak için [**Usage. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="8603b-113">Finally, call the [**Usage.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses usage.</span></span> <span data-ttu-id="8603b-114">Yöntem başarılı olursa [**Customerlicensesusageınsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) nesnelerinin bir koleksiyonunu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="8603b-114">If the method succeeds, you'll get a collection of [**CustomerLicensesUsageInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesusageinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Usage.Get();
```

## <a name="rest-request"></a><span data-ttu-id="8603b-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8603b-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8603b-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8603b-116">Request syntax</span></span>

| <span data-ttu-id="8603b-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8603b-117">Method</span></span>  | <span data-ttu-id="8603b-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8603b-118">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8603b-119">**Al**</span><span class="sxs-lookup"><span data-stu-id="8603b-119">**GET**</span></span> | <span data-ttu-id="8603b-120">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Analtics/licenses/Usage http/1.1</span><span class="sxs-lookup"><span data-stu-id="8603b-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/usage HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="8603b-121">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="8603b-121">URI parameter</span></span>

<span data-ttu-id="8603b-122">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8603b-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="8603b-123">Ad</span><span class="sxs-lookup"><span data-stu-id="8603b-123">Name</span></span>        | <span data-ttu-id="8603b-124">Tür</span><span class="sxs-lookup"><span data-stu-id="8603b-124">Type</span></span> | <span data-ttu-id="8603b-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8603b-125">Required</span></span> | <span data-ttu-id="8603b-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8603b-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="8603b-127">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="8603b-127">customer-id</span></span> | <span data-ttu-id="8603b-128">guid</span><span class="sxs-lookup"><span data-stu-id="8603b-128">guid</span></span> | <span data-ttu-id="8603b-129">Yes</span><span class="sxs-lookup"><span data-stu-id="8603b-129">Yes</span></span>      | <span data-ttu-id="8603b-130">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="8603b-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8603b-131">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8603b-131">Request headers</span></span>

<span data-ttu-id="8603b-132">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8603b-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8603b-133">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="8603b-133">Request body</span></span>

<span data-ttu-id="8603b-134">Yok.</span><span class="sxs-lookup"><span data-stu-id="8603b-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8603b-135">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8603b-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/usage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8603b-136">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8603b-136">REST response</span></span>

<span data-ttu-id="8603b-137">Başarılı olursa, yanıt gövdesi, lisans kullanımı hakkında bilgi sağlayan bir [Customerlicensesusageınsights](analytics-resources.md#customerlicensesusageinsights) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="8603b-137">If successful, the response body contains a collection of [CustomerLicensesUsageInsights](analytics-resources.md#customerlicensesusageinsights) resources that provide information about licenses usage.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8603b-138">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8603b-138">Response success and error codes</span></span>

<span data-ttu-id="8603b-139">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="8603b-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8603b-140">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8603b-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8603b-141">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8603b-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8603b-142">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="8603b-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1726
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: f657d2a8-9ed6-41b4-abfc-3cf4abebd62f
MS-CV: 0mufM0K1kEOoR7oI.0
MS-ServerId: 030020525
Date: Wed, 15 Mar 2017 01:19:58 GMT

{
    "totalCount": 5,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "SharePoint",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesActive": 0,
            "licensesQualified": 1,
            "usagePercent": 0.0,
            "workloadName": "Skype For Business",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesActive": 0,
            "licensesQualified": 5,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesActive": 0,
            "licensesQualified": 2,
            "usagePercent": 0.0,
            "workloadName": "Exchange",
            "processedDateTime": "2017-03-09T00:00:00+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesUsageInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
