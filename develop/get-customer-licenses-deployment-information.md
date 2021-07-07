---
title: Müşteri lisans dağıtım bilgilerini alma
description: Belirli bir müşteri için lisans dağıtım içgörüleri elde edin.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 91fe9da185aa59025d4dc8263257b207edb4a5be
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446471"
---
# <a name="get-customer-licenses-deployment-information"></a><span data-ttu-id="a22a6-103">Müşteri lisans dağıtım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="a22a6-103">Get customer licenses deployment information</span></span>

<span data-ttu-id="a22a6-104">Belirli bir müşteri için lisans dağıtım içgörüleri elde edin.</span><span class="sxs-lookup"><span data-stu-id="a22a6-104">How to get licenses deployment insights for a specific customer.</span></span>

> [!NOTE]
> <span data-ttu-id="a22a6-105">Bu senaryo, Get licenses deployment information ( Lisans dağıtım [bilgilerini al) ile 1000'den fazla lisansa sahip olur.](get-licenses-deployment-information.md)</span><span class="sxs-lookup"><span data-stu-id="a22a6-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a22a6-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a22a6-106">Prerequisites</span></span>

<span data-ttu-id="a22a6-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a22a6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a22a6-108">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a22a6-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a22a6-109">C\#</span><span class="sxs-lookup"><span data-stu-id="a22a6-109">C\#</span></span>

<span data-ttu-id="a22a6-110">Belirtilen bir müşteri için dağıtımda toplanan verileri almak için önce müşteri kimliğini kullanarak [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak müşteriyi tanıyın.</span><span class="sxs-lookup"><span data-stu-id="a22a6-110">To retrieve aggregated data on deployment for a specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="a22a6-111">Ardından Analytics özelliğinden müşteri düzeyinde analiz toplama işlemlerine bir [**arabirim**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) elde edin.</span><span class="sxs-lookup"><span data-stu-id="a22a6-111">Then get an interface to customer level analytics collection operations from the [**Analytics**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.analytics) property.</span></span> <span data-ttu-id="a22a6-112">Ardından, Lisanslar özelliğinden müşteri düzeyinde lisans analizi koleksiyonuna [**bir arabirim**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) alın.</span><span class="sxs-lookup"><span data-stu-id="a22a6-112">Next, retrieve an interface to the customer level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.icustomeranalyticscollection.licenses) property.</span></span> <span data-ttu-id="a22a6-113">Son olarak, lisans dağıtımında toplanan verileri almak için [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a22a6-113">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="a22a6-114">Yöntem başarılı olursa [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) nesnelerinin bir koleksiyonunu elde edersiniz.</span><span class="sxs-lookup"><span data-stu-id="a22a6-114">If the method succeeds, you'll get a collection of [**CustomerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.customerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerIdToRetrieve;

var customerLicensesDeploymentAnalytics = partnerOperations.Customers.ById(customerIdToRetrieve).Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="a22a6-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a22a6-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a22a6-116">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="a22a6-116">Request syntax</span></span>

| <span data-ttu-id="a22a6-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a22a6-117">Method</span></span>  | <span data-ttu-id="a22a6-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a22a6-118">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a22a6-119">**Al**</span><span class="sxs-lookup"><span data-stu-id="a22a6-119">**GET**</span></span> | <span data-ttu-id="a22a6-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a22a6-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a22a6-121">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="a22a6-121">URI parameter</span></span>

<span data-ttu-id="a22a6-122">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a22a6-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="a22a6-123">Ad</span><span class="sxs-lookup"><span data-stu-id="a22a6-123">Name</span></span>        | <span data-ttu-id="a22a6-124">Tür</span><span class="sxs-lookup"><span data-stu-id="a22a6-124">Type</span></span> | <span data-ttu-id="a22a6-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a22a6-125">Required</span></span> | <span data-ttu-id="a22a6-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a22a6-126">Description</span></span>                                                |
|-------------|------|----------|------------------------------------------------------------|
| <span data-ttu-id="a22a6-127">customer-id</span><span class="sxs-lookup"><span data-stu-id="a22a6-127">customer-id</span></span> | <span data-ttu-id="a22a6-128">guid</span><span class="sxs-lookup"><span data-stu-id="a22a6-128">guid</span></span> | <span data-ttu-id="a22a6-129">Yes</span><span class="sxs-lookup"><span data-stu-id="a22a6-129">Yes</span></span>      | <span data-ttu-id="a22a6-130">Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id.</span><span class="sxs-lookup"><span data-stu-id="a22a6-130">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a22a6-131">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a22a6-131">Request headers</span></span>

<span data-ttu-id="a22a6-132">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a22a6-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a22a6-133">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a22a6-133">Request body</span></span>

<span data-ttu-id="a22a6-134">Yok.</span><span class="sxs-lookup"><span data-stu-id="a22a6-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a22a6-135">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a22a6-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b01b8759-4dbe-4605-adb7-e5839a796c33
MS-CorrelationId: ae3b8c36-348b-46bc-9a60-398f973153ff
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="a22a6-136">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a22a6-136">REST response</span></span>

<span data-ttu-id="a22a6-137">Başarılı olursa yanıt gövdesi, dağıtılan lisanslar hakkında bilgi sağlayan [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) kaynaklarının bir koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="a22a6-137">If successful, the response body contains a collection of [CustomerLicensesDeploymentInsights](analytics-resources.md#customerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a22a6-138">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a22a6-138">Response success and error codes</span></span>

<span data-ttu-id="a22a6-139">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a22a6-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a22a6-140">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a22a6-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a22a6-141">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a22a6-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a22a6-142">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a22a6-142">Response example</span></span>

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
