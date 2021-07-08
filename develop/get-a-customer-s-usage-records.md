---
title: Tüm müşteriler için kullanım kayıtları al
description: Belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin kullanım kayıtlarını almak için CustomerMonthlyUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6b3fb0e1989336810f2afcc2a5bfc3a1d2849b7f
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874899"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="adfde-103">Tüm müşteriler için kullanım kayıtları al</span><span class="sxs-lookup"><span data-stu-id="adfde-103">Get usage records for all customers</span></span>

<span data-ttu-id="adfde-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="adfde-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="adfde-105">İş ortakları, tüm müşterileri için kullanım kayıtları almak üzere **CustomerMonthlyUsageRecord** kaynak koleksiyonunu kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="adfde-105">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="adfde-106">Bu kaynak, tüm müşteriler için kullanım kayıtlarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="adfde-106">This resource represents usage records for all customers.</span></span> <span data-ttu-id="adfde-107">bu müşterileri bir Microsoft Azure (MS-azr-0145p) aboneliği veya bir Azure planına dahil eder.</span><span class="sxs-lookup"><span data-stu-id="adfde-107">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="adfde-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="adfde-108">Prerequisites</span></span>

- <span data-ttu-id="adfde-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="adfde-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="adfde-110">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="adfde-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="adfde-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="adfde-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="adfde-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adfde-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="adfde-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="adfde-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="adfde-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="adfde-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="adfde-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="adfde-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="adfde-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="adfde-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="adfde-117">C\#</span><span class="sxs-lookup"><span data-stu-id="adfde-117">C\#</span></span>

<span data-ttu-id="adfde-118">Geçerli faturalandırma döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="adfde-118">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="adfde-119">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="adfde-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="adfde-120">**UsageRecords** özelliğini çağırın, sonra **Get ()** veya **GetAsync ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="adfde-120">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="adfde-121">Bir örnek için aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="adfde-121">For an example, see the following sample:</span></span>

- <span data-ttu-id="adfde-122">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="adfde-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="adfde-123">Project: **partnersdk. featuresamples**</span><span class="sxs-lookup"><span data-stu-id="adfde-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="adfde-124">Sınıf: **GetCustomerUsageRecords. cs**</span><span class="sxs-lookup"><span data-stu-id="adfde-124">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="adfde-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="adfde-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="adfde-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="adfde-126">Request syntax</span></span>

| <span data-ttu-id="adfde-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="adfde-127">Method</span></span>  | <span data-ttu-id="adfde-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="adfde-128">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="adfde-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="adfde-129">**GET**</span></span> | <span data-ttu-id="adfde-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="adfde-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="adfde-131">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="adfde-131">Request headers</span></span>

<span data-ttu-id="adfde-132">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="adfde-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="adfde-133">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="adfde-133">Request body</span></span>

<span data-ttu-id="adfde-134">Yok.</span><span class="sxs-lookup"><span data-stu-id="adfde-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="adfde-135">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="adfde-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="adfde-136">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="adfde-136">REST response</span></span>

<span data-ttu-id="adfde-137">Başarılı olursa, bu yöntem yanıt gövdesinde bir **CustomerMonthlyUsageRecord** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="adfde-137">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="adfde-138">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="adfde-138">Response success and error codes</span></span>

<span data-ttu-id="adfde-139">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="adfde-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="adfde-140">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="adfde-140">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="adfde-141">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="adfde-141">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="adfde-142">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="adfde-142">Response example</span></span>

<span data-ttu-id="adfde-143">**Ispyükseltilen** özelliğini kullanarak bir Azure planına sahip olan müşterileri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="adfde-143">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="adfde-144">**Isyükseltilen** değeri **true** ise, müşterilerin Azure planlarına sahip olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="adfde-144">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 25,
    "items": [
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "customerSpendingBudget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": false,
            "resourceId": "11111111-1843-4b3b-872f-206e08a08e51",
            "id": "11111111-1843-4b3b-872f-206e08a08e51",
            "resourceName": "LEGACY AZURE CUSTOMER SE",
            "name": "LEGACY AZURE CUSTOMER SE",
            "totalCost": 0,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-08-01T23:00:16.57+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "amount": 20,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 602.84,
            "isUpgraded": true,
            "resourceId": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "id": "11111111-6fb9-4b05-8f15-b3d72e0596e6",
            "resourceName": "Modern Azure Customer SE",
            "name": "Modern Azure Customer SE",
            "totalCost": 120.5682999999995904716,
            "currencyCode": "SEK",
            "usdTotalCost": 12.39999999999999985235,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
        {
            "budget": {
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 0,
            "isUpgraded": true,
            "resourceId": "11111111-5892-4326-8541-9da1fdb233fb",
            "id": "11111111-5892-4326-8541-9da1fdb233fb",
            "resourceName": "Test_Test_MA20190829_14",
            "name": "Test_Test_MA20190829_14",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        },
           {
            "budget": {
                "amount": 97,
                "attributes": {
                    "objectType": "SpendingBudget"
                }
            },
            "percentUsed": 28.08,
            "isUpgraded": true,
            "resourceId": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "id": "11111111-641b-4c53-b7fc-0f2bfca8a581",
            "resourceName": "Modern Azure Customer UK",
            "name": "Modern Azure Customer UK",
            "totalCost": 27.23292827625710931604,
            "currencyCode": "GBP",
            "usdTotalCost": 33.280000000000001044,
            "lastModifiedDate": "2019-09-17T17:08:11.1433333+00:00",
            "attributes": {
                "objectType": "CustomerMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
