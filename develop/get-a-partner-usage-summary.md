---
title: İş ortağı için Kullanım Özeti alın
description: Geçerli fatura döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin iş ortağı kullanım özetini almak için PartnerUsageSummary kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: f003980f1b521ad0ac26dbfd0d4821b9096fdd27
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873913"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="46424-103">İş ortağı için Kullanım Özeti alın</span><span class="sxs-lookup"><span data-stu-id="46424-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="46424-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="46424-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="46424-105">Geçerli fatura döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin iş ortağı kullanım özetini almak için **Partnerusagesummary** kaynağını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="46424-105">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="46424-106">*Bu API tarafından döndürülen toplam, bir Azure planına sahip müşteriler için tüketim getirmeyecektir.*</span><span class="sxs-lookup"><span data-stu-id="46424-106">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="46424-107">Gelecekte kullanımdan kaldırılması planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="46424-107">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="46424-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="46424-108">Prerequisites</span></span>

- <span data-ttu-id="46424-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="46424-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="46424-110">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="46424-110">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="46424-111">C\#</span><span class="sxs-lookup"><span data-stu-id="46424-111">C\#</span></span>

<span data-ttu-id="46424-112">Geçerli faturalandırma döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşteriler için Kullanım Özeti almak üzere:</span><span class="sxs-lookup"><span data-stu-id="46424-112">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="46424-113">**Iaggregatepartner**'nizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="46424-113">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="46424-114">**Usagesummary** özelliğini çağırın, ardından **Get ()** veya **GetAsync ()** yöntemleri gelir:</span><span class="sxs-lookup"><span data-stu-id="46424-114">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="46424-115">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="46424-115">For an example, see the following:</span></span>

- <span data-ttu-id="46424-116">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="46424-116">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="46424-117">Project: **partnersdk. featuresamples**</span><span class="sxs-lookup"><span data-stu-id="46424-117">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="46424-118">Sınıf: **Getpartnerusagesummary. cs**</span><span class="sxs-lookup"><span data-stu-id="46424-118">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="46424-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="46424-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="46424-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="46424-120">Request syntax</span></span>

| <span data-ttu-id="46424-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="46424-121">Method</span></span>  | <span data-ttu-id="46424-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="46424-122">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="46424-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="46424-123">**GET**</span></span> | <span data-ttu-id="46424-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="46424-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="46424-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="46424-125">Request headers</span></span>

<span data-ttu-id="46424-126">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="46424-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="46424-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="46424-127">Request body</span></span>

<span data-ttu-id="46424-128">Yok.</span><span class="sxs-lookup"><span data-stu-id="46424-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="46424-129">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="46424-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="46424-130">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="46424-130">REST response</span></span>

<span data-ttu-id="46424-131">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Partnerusagesummary** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="46424-131">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="46424-132">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="46424-132">Response success and error codes</span></span>

<span data-ttu-id="46424-133">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="46424-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="46424-134">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="46424-134">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="46424-135">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="46424-135">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="46424-136">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="46424-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "customersOverBudget": 1,
    "customersTrendingOver": 0,
    "customersWithUsageBasedSubscription": 11,
    "resourceId": "11111111-4574-4539-bc42-0e539b9684c0",
    "id": "11111111-4574-4539-bc42-0e539b9684c0",
    "resourceName": "PLAMUATT2NETNEW",
    "name": "PLAMUATT2NETNEW",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerUsageSummary"
    }
}
```
