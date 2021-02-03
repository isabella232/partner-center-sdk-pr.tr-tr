---
title: İş ortağı lisans dağıtım bilgilerini alma
description: Tüm müşterileri kapsayacak şekilde toplanmış iş ortağı lisansları dağıtım bilgileri alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 229f63d4df4f59cd0fde2bd0fc5e3f10cf6b25c0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769838"
---
# <a name="get-partner-licenses-deployment-information"></a><span data-ttu-id="1df6b-103">İş ortağı lisans dağıtım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="1df6b-103">Get partner licenses deployment information</span></span>

<span data-ttu-id="1df6b-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="1df6b-104">**Applies To**</span></span>

- <span data-ttu-id="1df6b-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1df6b-105">Partner Center</span></span>

<span data-ttu-id="1df6b-106">Tüm müşterileri kapsayacak şekilde toplanmış iş ortağı lisansları dağıtım bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="1df6b-106">How to get partner licenses deployment information aggregated to include all customers.</span></span>

> [!NOTE]
> <span data-ttu-id="1df6b-107">Bu senaryo, [lisans dağıtımı bilgilerini alır](get-licenses-deployment-information.md).</span><span class="sxs-lookup"><span data-stu-id="1df6b-107">This scenario is superceded by [Get licenses deployment information](get-licenses-deployment-information.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1df6b-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1df6b-108">Prerequisites</span></span>

<span data-ttu-id="1df6b-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1df6b-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1df6b-110">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1df6b-110">This scenario supports authentication with App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="1df6b-111">C\#</span><span class="sxs-lookup"><span data-stu-id="1df6b-111">C\#</span></span>

<span data-ttu-id="1df6b-112">Lisans dağıtımında toplanmış verileri almak için ilk olarak [**ıaggregatepartner. Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) özelliğinden iş ortağı düzeyi Analizi toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="1df6b-112">To retrieve aggregated data on licenses deployment, first get an interface to partner level analytics collection operations from the [**IAggregatePartner.Analytics**](/dotnet/api/microsoft.store.partnercenter.ipartner.analytics) property.</span></span> <span data-ttu-id="1df6b-113">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) özelliğinden iş ortağı düzeyi lisans Analizi koleksiyonuna bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="1df6b-113">Then retrieve an interface to the partner level licenses analytics collection from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.analytics.ipartneranalyticscollection.licenses) property.</span></span> <span data-ttu-id="1df6b-114">Son olarak, lisans dağıtımında toplanan verileri almak için [**Deployment. Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1df6b-114">Finally, call the [**Deployment.Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) method to get the aggregated data on licenses deployment.</span></span> <span data-ttu-id="1df6b-115">Yöntem başarılı olursa, [**Partnerlicensesdeploymenınsıghts**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) nesnelerinin bir koleksiyonunu alırsınız.</span><span class="sxs-lookup"><span data-stu-id="1df6b-115">If the method succeeds you'll get a collection of [**PartnerLicensesDeploymentInsights**](/dotnet/api/microsoft.store.partnercenter.models.analytics.partnerlicensesdeploymentinsights) objects.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var partnerLicensesDeploymentAnalytics = partnerOperations.Analytics.Licenses.Deployment.Get();
```

## <a name="rest-request"></a><span data-ttu-id="1df6b-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1df6b-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1df6b-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1df6b-117">Request syntax</span></span>

| <span data-ttu-id="1df6b-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1df6b-118">Method</span></span>  | <span data-ttu-id="1df6b-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1df6b-119">Request URI</span></span>                                                                           |
|---------|---------------------------------------------------------------------------------------|
| <span data-ttu-id="1df6b-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="1df6b-120">**GET**</span></span> | <span data-ttu-id="1df6b-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/analiz Tics/licenses/Deployment http/1.1</span><span class="sxs-lookup"><span data-stu-id="1df6b-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/licenses/deployment HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1df6b-122">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1df6b-122">Request headers</span></span>

<span data-ttu-id="1df6b-123">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1df6b-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1df6b-124">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1df6b-124">Request body</span></span>

<span data-ttu-id="1df6b-125">Yok.</span><span class="sxs-lookup"><span data-stu-id="1df6b-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1df6b-126">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1df6b-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/analytics/licenses/deployment HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 25b6edd5-1f53-456b-b48c-c64f60ec2dda
MS-CorrelationId: 6492b9d6-5629-429b-934c-040b1946e760
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1df6b-127">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1df6b-127">REST response</span></span>

<span data-ttu-id="1df6b-128">Başarılı olursa, yanıt gövdesi, dağıtılan lisanslar hakkında bilgi sağlayan bir [Partnerlicensesdeploymentinsıghts](analytics-resources.md#partnerlicensesdeploymentinsights) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="1df6b-128">If successful, the response body contains a collection of [PartnerLicensesDeploymentInsights](analytics-resources.md#partnerlicensesdeploymentinsights) resources that provide information about the licenses deployed.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1df6b-129">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1df6b-129">Response success and error codes</span></span>

<span data-ttu-id="1df6b-130">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1df6b-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1df6b-131">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1df6b-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1df6b-132">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1df6b-132">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1df6b-133">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1df6b-133">Response example</span></span>

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
