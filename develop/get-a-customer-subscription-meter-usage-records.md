---
title: Ölçüme göre abonelik için kullanım verilerini alma
description: Geçerli faturalama döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak için MeterUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0bd6143c80059bd140a4c4332ab4ec19c54d99f1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874865"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="aee61-103">Ölçüme göre abonelik için kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="aee61-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="aee61-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="aee61-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="aee61-105">Geçerli faturalama döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak için **MeterUsageRecord** kaynak koleksiyonunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aee61-105">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="aee61-106">Bu kaynak koleksiyonu, Tüm Azure planınız genelinde geçerli faturalama dönemi için her ölçüm için toplu bir toplamı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="aee61-106">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aee61-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="aee61-107">Prerequisites</span></span>

- <span data-ttu-id="aee61-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="aee61-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="aee61-109">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="aee61-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="aee61-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="aee61-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="aee61-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="aee61-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="aee61-112">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="aee61-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="aee61-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="aee61-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="aee61-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="aee61-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="aee61-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="aee61-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="aee61-116">Abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="aee61-116">A subscription ID</span></span>

<span data-ttu-id="aee61-117">*Bu yeni yol, yalnızca Microsoft Azure (MS-AZR-0145P) abonelikleri için çalışmaya devam edecek olan ile `subscriptions/{subscription-id}/usagerecords/resources` eşdeğerdir.*</span><span class="sxs-lookup"><span data-stu-id="aee61-117">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="aee61-118">Bu yeni yol hem Microsoft Azure (MS-AZR-0145P) aboneliklerini hem de Azure planlarını destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="aee61-118">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="aee61-119">Azure planınıza ilişkin bu bilgileri almak için bu yeni rotaya geçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="aee61-119">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="aee61-120">Aşağıdaki bölümlerde belirtilen özellikler dışında, yanıt eski yol ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="aee61-120">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="aee61-121">C\#</span><span class="sxs-lookup"><span data-stu-id="aee61-121">C\#</span></span>

<span data-ttu-id="aee61-122">Geçerli faturalama döneminde belirli bir Azure hizmetine veya kaynağına yönelik müşterinin ölçüm kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="aee61-122">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="aee61-123">**ById()** **yöntemini çağırarak IAggregatePartner.Customers** koleksiyonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="aee61-123">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="aee61-124">Subscriptions özelliğini ve **UsageRecords'ı** ve ardından **Meters özelliğini** çağırma.</span><span class="sxs-lookup"><span data-stu-id="aee61-124">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="aee61-125">Get() veya GetAsync() yöntemlerini çağırarak son.</span><span class="sxs-lookup"><span data-stu-id="aee61-125">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="aee61-126">Bir örnek için aşağıdaki örneğine bakın:</span><span class="sxs-lookup"><span data-stu-id="aee61-126">For an example, see the following sample:</span></span>

- <span data-ttu-id="aee61-127">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="aee61-127">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="aee61-128">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="aee61-128">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="aee61-129">Sınıf: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="aee61-129">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="aee61-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="aee61-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="aee61-131">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="aee61-131">Request syntax</span></span>

| <span data-ttu-id="aee61-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="aee61-132">Method</span></span>  | <span data-ttu-id="aee61-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="aee61-133">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="aee61-134">**Al**</span><span class="sxs-lookup"><span data-stu-id="aee61-134">**GET**</span></span> | <span data-ttu-id="aee61-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="aee61-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="aee61-136">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="aee61-136">URI parameters</span></span>

<span data-ttu-id="aee61-137">Bu tabloda müşterinin derecelendirilmiş kullanım bilgilerini almak için gereken sorgu parametreleri listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="aee61-137">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="aee61-138">Ad</span><span class="sxs-lookup"><span data-stu-id="aee61-138">Name</span></span>                   | <span data-ttu-id="aee61-139">Tür</span><span class="sxs-lookup"><span data-stu-id="aee61-139">Type</span></span>     | <span data-ttu-id="aee61-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="aee61-140">Required</span></span> | <span data-ttu-id="aee61-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aee61-141">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="aee61-142">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="aee61-142">**customer-tenant-id**</span></span> | <span data-ttu-id="aee61-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="aee61-143">**guid**</span></span> | <span data-ttu-id="aee61-144">Y</span><span class="sxs-lookup"><span data-stu-id="aee61-144">Y</span></span>        | <span data-ttu-id="aee61-145">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="aee61-145">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="aee61-146">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="aee61-146">**subscription-id**</span></span>    | <span data-ttu-id="aee61-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="aee61-147">**guid**</span></span> | <span data-ttu-id="aee61-148">Y</span><span class="sxs-lookup"><span data-stu-id="aee61-148">Y</span></span>        | <span data-ttu-id="aee61-149">Microsoft Azure (MS-AZR-0145P) aboneliğini veya bir Azure planını temsil eden bir İş Ortağı Merkezi aboneliği kaynağının tanımlayıcısına karşılık gelen GUID. [](subscription-resources.md#subscription)</span><span class="sxs-lookup"><span data-stu-id="aee61-149">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="aee61-150">*Azure planı abonelik kaynakları için bu yolda **subscription-id** olarak **plan-id** girin.*</span><span class="sxs-lookup"><span data-stu-id="aee61-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="aee61-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="aee61-151">Request headers</span></span>

<span data-ttu-id="aee61-152">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="aee61-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="aee61-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="aee61-153">Request body</span></span>

<span data-ttu-id="aee61-154">Yok.</span><span class="sxs-lookup"><span data-stu-id="aee61-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="aee61-155">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="aee61-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="aee61-156">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="aee61-156">REST response</span></span>

<span data-ttu-id="aee61-157">Başarılı olursa, bu yöntem yanıt **gövdesinde \<MeterUsageRecord> bir PagedResourceCollection** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="aee61-157">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="aee61-158">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="aee61-158">Response success and error codes</span></span>

<span data-ttu-id="aee61-159">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="aee61-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="aee61-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="aee61-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="aee61-161">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="aee61-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="aee61-162">Microsoft Azure (MS-AZR-0145P) abonelikleri için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="aee61-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="aee61-163">Bu örnekte müşteri **145P Azure PayG satın alır.**</span><span class="sxs-lookup"><span data-stu-id="aee61-163">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="aee61-164">*Microsoft Azure (MS-AZR-0145P) aboneliğine sahip müşteriler için API yanıtta değişiklik olmaz.*</span><span class="sxs-lookup"><span data-stu-id="aee61-164">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 1,
    "items": [
        {
            "status": "active",
            "offerId": "MS-AZR-0145P",
            "resourceId": "11111111-F347-41B6-B02C-187B1B778A43",
            "id": "11111111-F347-41B6-B02C-187B1B778A43",
            "resourceName": "Microsoft Azure",
            "name": "Microsoft Azure",
            "totalCost": 22.861172,
            "currencyLocale": "fr-FR",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/{customer-tenant-id}/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="aee61-165">Azure planı için REST yanıtı örneği</span><span class="sxs-lookup"><span data-stu-id="aee61-165">REST response example for Azure plan</span></span>

<span data-ttu-id="aee61-166">Bu örnekte müşteri bir Azure planı satın alır.</span><span class="sxs-lookup"><span data-stu-id="aee61-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="aee61-167">*Azure planları olan müşteriler için API yanıtta aşağıdaki değişiklikler vardır:*</span><span class="sxs-lookup"><span data-stu-id="aee61-167">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="aee61-168">**currencyLocale,** **currencyCode ile değiştirildi**</span><span class="sxs-lookup"><span data-stu-id="aee61-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="aee61-169">**usdTotalCost** yeni bir alandır</span><span class="sxs-lookup"><span data-stu-id="aee61-169">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Fri, 26 Feb 2016 20:31:45 GMT

{
    "totalCount": 4,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer In (GB)",
            "meterName": "Data Transfer In",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.01129,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNVX-005J-Data Transfer Out (GB)",
            "meterName": "Data Transfer Out",
            "category": "Bandwidth",
            "subcategory": "Bandwidth",
            "quantityUsed": 0.000224,
            "unit": "1 GB",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-10K Batch Write Operations",
            "meterName": "Batch Write Operations",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.2462,
            "unit": "10K",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "meterId": "DZH318Z0BNZ5-006G-Data Stored (GB/Month)",
            "meterName": "LRS Data Stored",
            "category": "Storage",
            "subcategory": "Tables",
            "quantityUsed": 0.002632,
            "unit": "1 GB/Month",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "MeterUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/meterusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
