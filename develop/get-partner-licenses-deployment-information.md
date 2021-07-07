---
title: İş ortağı lisans dağıtım bilgilerini alma
description: Tüm müşterileri kapsayacak şekilde toplanmış iş ortağı lisansları dağıtım bilgileri alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2464242fc6dc4e7464511eac5d4197630e22fac0
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445994"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="2033b-103">İş ortağı lisans dağıtım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="2033b-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="2033b-104">Tüm müşterileri kapsayacak şekilde toplanmış iş ortağı lisansları dağıtım bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="2033b-104">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="2033b-105">Bu senaryo, [lisans dağıtımı bilgilerini alır](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="2033b-105">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2033b-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2033b-106">Prerequisites</span></span>

<span data-ttu-id="2033b-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2033b-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2033b-108">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="2033b-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2033b-109">C\#</span><span class="sxs-lookup"><span data-stu-id="2033b-109">C\#</span></span>

<span data-ttu-id="2033b-110">Lisans dağıtımında toplanmış verileri almak için ilk olarak [**ıaggregatepartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) özelliğinden iş ortağı düzeyi Analizi toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="2033b-110">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="2033b-111">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) özelliğinden iş ortağı düzeyi lisans Analizi koleksiyonuna bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="2033b-111">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="2033b-112">Son olarak, lisans dağıtımında toplanan verileri almak için [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2033b-112">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="2033b-113">Yöntem başarılı olursa, [**Partnerlicensesdeploymentinsıghts**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) nesnelerinin bir koleksiyonunu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="2033b-113">If the method succeeds, you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="2033b-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2033b-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2033b-115">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2033b-115">Request syntax</span></span>

| <span data-ttu-id="2033b-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2033b-116">Method</span></span>  | <span data-ttu-id="2033b-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2033b-117">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="2033b-118">**Al**</span><span class="sxs-lookup"><span data-stu-id="2033b-118">**GET**</span></span> | <span data-ttu-id="2033b-119">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/analiz Tics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="2033b-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2033b-120">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2033b-120">Request headers</span></span>

<span data-ttu-id="2033b-121">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2033b-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2033b-122">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2033b-122">Request body</span></span>

<span data-ttu-id="2033b-123">Yok.</span><span class="sxs-lookup"><span data-stu-id="2033b-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2033b-124">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2033b-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="2033b-125">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2033b-125">REST response</span></span>

<span data-ttu-id="2033b-126">Başarılı olursa, yanıt gövdesi, dağıtılan lisanslar hakkında bilgi sağlayan bir [Partnerlicensesdeploymentinsıghts](analytics-resources.md#partnerlicensesdeploymentinsights) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="2033b-126">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2033b-127">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2033b-127">Response success and error codes</span></span>

<span data-ttu-id="2033b-128">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2033b-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2033b-129">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2033b-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2033b-130">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2033b-130">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2033b-131">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2033b-131">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 102030524
Date: Tue, 14 Mar 2017 17:55:01 GMT

{
    "totalCount": 2,
    "items": [{
            "proratedDeploymentPercent": 0.0,
            "licensesSold": 343,
            "processedDateTime": "2017-03-10T00:00:00+00:00",
            "serviceName": "crm",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }, {
            "proratedDeploymentPercent": 1.0,
            "licensesSold": 4464,
            "processedDateTime": "2017-03-14T03:25:16.36+00:00",
            "serviceName": "o365",
            "channel": "reseller",
            "attributes": {
                "objectType": "PartnerLicensesDeploymentInsights"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
