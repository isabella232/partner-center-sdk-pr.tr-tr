---
title: Müşteri lisans dağıtım bilgilerini alma
description: Belirli bir müşteri için lisans dağıtımı öngörülerini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 3a39c6c908048305ff2dabf85a29d7ddc3628500
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769856"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="076f2-103">Müşteri lisans dağıtım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="076f2-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="076f2-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="076f2-104">**Applies To**</span></span>

- <span data-ttu-id="076f2-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="076f2-105">Partner Center</span></span>

<span data-ttu-id="076f2-106">Belirli bir müşteri için lisans dağıtımı öngörülerini alma.</span><span class="sxs-lookup"><span data-stu-id="076f2-106">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="076f2-107">Bu senaryo, [lisans dağıtımı bilgilerini alır](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="076f2-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="076f2-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="076f2-108">Prerequisites</span></span>

<span data-ttu-id="076f2-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="076f2-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="076f2-110">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="076f2-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="076f2-111">C\#</span><span class="sxs-lookup"><span data-stu-id="076f2-111">C\#</span></span>

<span data-ttu-id="076f2-112">Belirtilen bir müşteri için dağıtımda toplanan verileri almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="076f2-112">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="076f2-113">Ardından [**analiz**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) özelliğinden müşteri düzeyi Analizi toplama işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="076f2-113">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="076f2-114">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) özelliğinden müşteri düzeyi lisans Analizi koleksiyonuna bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="076f2-114">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="076f2-115">Son olarak, lisans dağıtımında toplanan verileri almak için [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="076f2-115">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="076f2-116">Yöntem başarılı olursa [**Customerlicensesdeploymenınsıghts**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) nesnelerinin bir koleksiyonunu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="076f2-116">If the method succeeds you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="076f2-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="076f2-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="076f2-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="076f2-118">Request syntax</span></span>

| <span data-ttu-id="076f2-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="076f2-119">Method</span></span>  | <span data-ttu-id="076f2-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="076f2-120">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="076f2-121">**Al**</span><span class="sxs-lookup"><span data-stu-id="076f2-121">**GET**</span></span> | <span data-ttu-id="076f2-122">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Analtics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="076f2-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="076f2-123">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="076f2-123">URI parameter</span></span>

<span data-ttu-id="076f2-124">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="076f2-124">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="076f2-125">Ad</span><span class="sxs-lookup"><span data-stu-id="076f2-125">Name</span></span>        | <span data-ttu-id="076f2-126">Tür</span><span class="sxs-lookup"><span data-stu-id="076f2-126">Type</span></span> | <span data-ttu-id="076f2-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="076f2-127">Required</span></span> | <span data-ttu-id="076f2-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="076f2-128">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="076f2-129">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="076f2-129">customer-id</span></span> | <span data-ttu-id="076f2-130">guid</span><span class="sxs-lookup"><span data-stu-id="076f2-130">guid</span></span> | <span data-ttu-id="076f2-131">Yes</span><span class="sxs-lookup"><span data-stu-id="076f2-131">Yes</span></span>      | <span data-ttu-id="076f2-132">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="076f2-132">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="076f2-133">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="076f2-133">Request headers</span></span>

<span data-ttu-id="076f2-134">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="076f2-134">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="076f2-135">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="076f2-135">Request body</span></span>

<span data-ttu-id="076f2-136">Yok.</span><span class="sxs-lookup"><span data-stu-id="076f2-136">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="076f2-137">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="076f2-137">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="076f2-138">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="076f2-138">REST response</span></span>

<span data-ttu-id="076f2-139">Başarılı olursa, yanıt gövdesi, dağıtılan lisanslar hakkında bilgi sağlayan bir [Customerlicensesdeploymentinsıghts](analytics-resources.md#customerlicensesdeploymentinsights) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="076f2-139">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="076f2-140">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="076f2-140">Response success and error codes</span></span>

<span data-ttu-id="076f2-141">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="076f2-141">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="076f2-142">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="076f2-142">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="076f2-143">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="076f2-143">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="076f2-144">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="076f2-144">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1012
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CV: deEp2Wy6DUitMCYA.0
MS-ServerId: 102030524
Date: Wed, 15 Mar 2017 01:19:18 GMT

{
    "totalCount": 3,
    "items": [{
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "OFFICE 365 BUSINESS ESSENTIALS",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 1,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE (PLAN 1)",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 5,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }, {
            "customerName": "DT DEMO CSP CUSTOMER 005",
            "productName": "EXCHANGE ONLINE ARCHIVING FOR EXCHANGE ONLINE",
            "licensesDeployed": 0,
            "deploymentPercent": 0.0,
            "licensesSold": 2,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "CustomerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
