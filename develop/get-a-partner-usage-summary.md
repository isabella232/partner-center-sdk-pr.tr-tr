---
title: İş ortağı için Kullanım Özeti alın
description: Geçerli fatura döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin iş ortağı kullanım özetini almak için PartnerUsageSummary kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ba1885f46043a75274595239fe61ce3ef0998acf
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769035"
---
# <a name="get-a-usage-summary-for-a-partner"></a><span data-ttu-id="4b6f8-103">İş ortağı için Kullanım Özeti alın</span><span class="sxs-lookup"><span data-stu-id="4b6f8-103">Get a usage summary for a partner</span></span>

<span data-ttu-id="4b6f8-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="4b6f8-104">**Applies to:**</span></span>

- <span data-ttu-id="4b6f8-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4b6f8-105">Partner Center</span></span>
- <span data-ttu-id="4b6f8-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4b6f8-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4b6f8-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4b6f8-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4b6f8-108">Geçerli fatura döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin iş ortağı kullanım özetini almak için **Partnerusagesummary** kaynağını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-108">You can use the **PartnerUsageSummary** resource to get a partner usage summary of all customers that purchased a specific Azure service or resource during the current billing period.</span></span>

<span data-ttu-id="4b6f8-109">*Bu API tarafından döndürülen toplam, bir Azure planına sahip müşteriler için tüketim getirmeyecektir.*</span><span class="sxs-lookup"><span data-stu-id="4b6f8-109">*The total returned by this API will not return consumption for customers that have an Azure plan.*</span></span> <span data-ttu-id="4b6f8-110">Gelecekte kullanımdan kaldırılması planlanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-110">Planned for deprecation in the future.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4b6f8-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4b6f8-111">Prerequisites</span></span>

- <span data-ttu-id="4b6f8-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4b6f8-113">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-113">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="4b6f8-114">C\#</span><span class="sxs-lookup"><span data-stu-id="4b6f8-114">C\#</span></span>

<span data-ttu-id="4b6f8-115">Geçerli faturalandırma döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşteriler için Kullanım Özeti almak üzere:</span><span class="sxs-lookup"><span data-stu-id="4b6f8-115">To get a usage summary for all customers that purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="4b6f8-116">**Iaggregatepartner**'nizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-116">Use your **IAggregatePartner**.</span></span>

2. <span data-ttu-id="4b6f8-117">**Usagesummary** özelliğini çağırın, ardından **Get ()** veya **GetAsync ()** yöntemleri gelir:</span><span class="sxs-lookup"><span data-stu-id="4b6f8-117">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;

    var usageSummary = partnerOperations.UsageSummary.Get();
    ```

<span data-ttu-id="4b6f8-118">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="4b6f8-118">For an example, see the following:</span></span>

- <span data-ttu-id="4b6f8-119">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4b6f8-119">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4b6f8-120">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="4b6f8-120">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="4b6f8-121">Sınıf: **GetPartnerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="4b6f8-121">Class: **GetPartnerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="4b6f8-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4b6f8-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4b6f8-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4b6f8-123">Request syntax</span></span>

| <span data-ttu-id="4b6f8-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4b6f8-124">Method</span></span>  | <span data-ttu-id="4b6f8-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4b6f8-125">Request URI</span></span>                                                         |
|---------|---------------------------------------------------------------------|
| <span data-ttu-id="4b6f8-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="4b6f8-126">**GET**</span></span> | <span data-ttu-id="4b6f8-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="4b6f8-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/usagesummary HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4b6f8-128">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4b6f8-128">Request headers</span></span>

<span data-ttu-id="4b6f8-129">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4b6f8-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4b6f8-130">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4b6f8-130">Request body</span></span>

<span data-ttu-id="4b6f8-131">Yok.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4b6f8-132">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4b6f8-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="4b6f8-133">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4b6f8-133">REST response</span></span>

<span data-ttu-id="4b6f8-134">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Partnerusagesummary** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-134">If successful, this method returns a **PartnerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4b6f8-135">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4b6f8-135">Response success and error codes</span></span>

<span data-ttu-id="4b6f8-136">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4b6f8-137">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4b6f8-137">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="4b6f8-138">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4b6f8-138">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4b6f8-139">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4b6f8-139">Response example</span></span>

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
