---
title: Tüm müşteriler için kullanım kayıtları al
description: Belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin kullanım kayıtlarını almak için CustomerMonthlyUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: da829a6de3690a9b1117ce9dfa58fbe381cafd81
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769160"
---
# <a name="get-usage-records-for-all-customers"></a><span data-ttu-id="7dd84-103">Tüm müşteriler için kullanım kayıtları al</span><span class="sxs-lookup"><span data-stu-id="7dd84-103">Get usage records for all customers</span></span>

<span data-ttu-id="7dd84-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="7dd84-104">**Applies to:**</span></span>

- <span data-ttu-id="7dd84-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7dd84-105">Partner Center</span></span>
- <span data-ttu-id="7dd84-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7dd84-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7dd84-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7dd84-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7dd84-108">İş ortakları, tüm müşterileri için kullanım kayıtları almak üzere **CustomerMonthlyUsageRecord** kaynak koleksiyonunu kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="7dd84-108">Partners can use the **CustomerMonthlyUsageRecord** resource collection to get usage records for all their customers.</span></span> <span data-ttu-id="7dd84-109">Bu kaynak, tüm müşteriler için kullanım kayıtlarını temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7dd84-109">This resource represents usage records for all customers.</span></span> <span data-ttu-id="7dd84-110">Bu müşterileri bir Microsoft Azure (MS-AZR-0145P) aboneliği veya bir Azure planına dahil eder.</span><span class="sxs-lookup"><span data-stu-id="7dd84-110">That includes those customers with a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dd84-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7dd84-111">Prerequisites</span></span>

- <span data-ttu-id="7dd84-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7dd84-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7dd84-113">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7dd84-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7dd84-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7dd84-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7dd84-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dd84-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7dd84-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7dd84-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7dd84-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7dd84-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7dd84-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="7dd84-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7dd84-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="7dd84-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7dd84-120">C\#</span><span class="sxs-lookup"><span data-stu-id="7dd84-120">C\#</span></span>

<span data-ttu-id="7dd84-121">Geçerli faturalandırma döneminde belirli bir Azure hizmetini veya kaynağını satın alan tüm müşterilerin kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="7dd84-121">To get all the usage records for all customers who purchased a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="7dd84-122">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7dd84-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="7dd84-123">**UsageRecords** özelliğini çağırın, sonra **Get ()** veya **GetAsync ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7dd84-123">Call **UsageRecords** property, then call the **Get()** or **GetAsync()** method.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    var usageRecords = partnerOperations.Customers.UsageRecords.Get();
    ```

<span data-ttu-id="7dd84-124">Bir örnek için aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="7dd84-124">For an example, see the following sample:</span></span>

- <span data-ttu-id="7dd84-125">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7dd84-125">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7dd84-126">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="7dd84-126">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="7dd84-127">Sınıf: **GetCustomerUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="7dd84-127">Class: **GetCustomerUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7dd84-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7dd84-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7dd84-129">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7dd84-129">Request syntax</span></span>

| <span data-ttu-id="7dd84-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7dd84-130">Method</span></span>  | <span data-ttu-id="7dd84-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7dd84-131">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="7dd84-132">**Al**</span><span class="sxs-lookup"><span data-stu-id="7dd84-132">**GET**</span></span> | <span data-ttu-id="7dd84-133">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="7dd84-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/usagerecords HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7dd84-134">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7dd84-134">Request headers</span></span>

<span data-ttu-id="7dd84-135">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7dd84-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7dd84-136">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7dd84-136">Request body</span></span>

<span data-ttu-id="7dd84-137">Yok.</span><span class="sxs-lookup"><span data-stu-id="7dd84-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7dd84-138">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7dd84-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="7dd84-139">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7dd84-139">REST response</span></span>

<span data-ttu-id="7dd84-140">Başarılı olursa, bu yöntem yanıt gövdesinde bir **CustomerMonthlyUsageRecord** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="7dd84-140">If successful, this method returns a **CustomerMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7dd84-141">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7dd84-141">Response success and error codes</span></span>

<span data-ttu-id="7dd84-142">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7dd84-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7dd84-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7dd84-143">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="7dd84-144">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7dd84-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7dd84-145">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7dd84-145">Response example</span></span>

<span data-ttu-id="7dd84-146">**Ispyükseltilen** özelliğini kullanarak bir Azure planına sahip olan müşterileri tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7dd84-146">You can use the **isUpgraded** property to identify customers who have an Azure plan.</span></span> <span data-ttu-id="7dd84-147">**Isyükseltilen** değeri **true** ise, müşterilerin Azure planlarına sahip olduğu anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="7dd84-147">If the value for **isUpgraded** is **true**, it means the customers have Azure plans.</span></span>

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
