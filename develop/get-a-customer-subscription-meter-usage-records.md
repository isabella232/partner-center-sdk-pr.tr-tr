---
title: Ölçüme göre abonelik için kullanım verilerini alma
description: Geçerli faturalandırma döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak üzere MeterUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df981eae8d2caee2dcb7f36696725ec011ead75b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769148"
---
# <a name="get-usage-data-for-subscription-by-meter"></a><span data-ttu-id="83d25-103">Ölçüme göre abonelik için kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="83d25-103">Get usage data for subscription by meter</span></span>

<span data-ttu-id="83d25-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="83d25-104">**Applies to:**</span></span>

- <span data-ttu-id="83d25-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="83d25-105">Partner Center</span></span>
- <span data-ttu-id="83d25-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="83d25-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="83d25-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="83d25-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="83d25-108">Geçerli faturalandırma döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin ölçüm kullanım kayıtlarını almak üzere **MeterUsageRecord** kaynak koleksiyonunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d25-108">You can use the **MeterUsageRecord** resource collection to get meter usage records of a customer for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="83d25-109">Bu kaynak koleksiyonu, tüm Azure planınız genelinde geçerli faturalandırma döngüsünün her bir ölçümü için toplam toplu toplamı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="83d25-109">This resource collection represents an aggregated total for each meter for the current billing cycle, across your entire Azure plan.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="83d25-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="83d25-110">Prerequisites</span></span>

- <span data-ttu-id="83d25-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="83d25-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="83d25-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="83d25-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="83d25-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="83d25-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="83d25-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="83d25-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="83d25-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="83d25-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="83d25-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="83d25-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="83d25-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="83d25-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="83d25-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="83d25-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="83d25-119">Abonelik KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="83d25-119">A subscription ID</span></span>

<span data-ttu-id="83d25-120">*Bu yeni yol ile eşdeğerdir `subscriptions/{subscription-id}/usagerecords/resources` , ancak yalnızca Microsoft Azure (MS-azr-0145P) abonelikleri için çalışmaya devam edecektir.*</span><span class="sxs-lookup"><span data-stu-id="83d25-120">*This new route is equivalent to `subscriptions/{subscription-id}/usagerecords/resources`, which will continue to function only for Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span> <span data-ttu-id="83d25-121">Bu yeni rota hem Microsoft Azure (MS-AZR-0145P) aboneliklerini ve Azure planlarını destekleyecektir.</span><span class="sxs-lookup"><span data-stu-id="83d25-121">This new route will support both Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span> <span data-ttu-id="83d25-122">Azure planınızla ilgili bu bilgileri almak için bu yeni yola geçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="83d25-122">In order to get this information for your Azure plan, you need to switch to this new route.</span></span> <span data-ttu-id="83d25-123">Aşağıdaki bölümlerde bahsedilen özellikler dışında, yanıt eski rotayla aynıdır.</span><span class="sxs-lookup"><span data-stu-id="83d25-123">Other than the properties mentioned in the following sections, the response is the same as the old route.</span></span>

## <a name="c"></a><span data-ttu-id="83d25-124">C\#</span><span class="sxs-lookup"><span data-stu-id="83d25-124">C\#</span></span>

<span data-ttu-id="83d25-125">Geçerli faturalandırma döneminde belirli bir Azure hizmeti veya kaynağı için bir müşterinin ölçüm kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="83d25-125">To get meter usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="83d25-126">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="83d25-126">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="83d25-127">Abonelikler özelliğini ve **UsageRecords** ve ardından **ölçümler özelliğini çağırın** .</span><span class="sxs-lookup"><span data-stu-id="83d25-127">Call the Subscriptions property, and **UsageRecords**, then the **Meters** property.</span></span> <span data-ttu-id="83d25-128">Get () veya GetAsync () yöntemlerini çağırarak son ' a erişin.</span><span class="sxs-lookup"><span data-stu-id="83d25-128">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Meters.Get();
    ```

<span data-ttu-id="83d25-129">Bir örnek için aşağıdaki örneğe bakın:</span><span class="sxs-lookup"><span data-stu-id="83d25-129">For an example, see the following sample:</span></span>

- <span data-ttu-id="83d25-130">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="83d25-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="83d25-131">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="83d25-131">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="83d25-132">Sınıf: **GetSubscriptionUsageRecordsByMeter.cs**</span><span class="sxs-lookup"><span data-stu-id="83d25-132">Class: **GetSubscriptionUsageRecordsByMeter.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="83d25-133">REST isteği</span><span class="sxs-lookup"><span data-stu-id="83d25-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="83d25-134">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="83d25-134">Request syntax</span></span>

| <span data-ttu-id="83d25-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="83d25-135">Method</span></span>  | <span data-ttu-id="83d25-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="83d25-136">Request URI</span></span>                                                                                                                             |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="83d25-137">**Al**</span><span class="sxs-lookup"><span data-stu-id="83d25-137">**GET**</span></span> | <span data-ttu-id="83d25-138">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Subscriptions/{Subscription-id}/meterusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="83d25-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="83d25-139">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="83d25-139">URI parameters</span></span>

<span data-ttu-id="83d25-140">Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametreleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="83d25-140">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="83d25-141">Ad</span><span class="sxs-lookup"><span data-stu-id="83d25-141">Name</span></span>                   | <span data-ttu-id="83d25-142">Tür</span><span class="sxs-lookup"><span data-stu-id="83d25-142">Type</span></span>     | <span data-ttu-id="83d25-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="83d25-143">Required</span></span> | <span data-ttu-id="83d25-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="83d25-144">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="83d25-145">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="83d25-145">**customer-tenant-id**</span></span> | <span data-ttu-id="83d25-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="83d25-146">**guid**</span></span> | <span data-ttu-id="83d25-147">Y</span><span class="sxs-lookup"><span data-stu-id="83d25-147">Y</span></span>        | <span data-ttu-id="83d25-148">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="83d25-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="83d25-149">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="83d25-149">**subscription-id**</span></span>    | <span data-ttu-id="83d25-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="83d25-150">**guid**</span></span> | <span data-ttu-id="83d25-151">Y</span><span class="sxs-lookup"><span data-stu-id="83d25-151">Y</span></span>        | <span data-ttu-id="83d25-152">Bir Microsoft Azure (MS-AZR-0145P) aboneliğini veya bir Azure planını temsil eden bir Iş Ortağı Merkezi [abonelik kaynağının](subscription-resources.md#subscription)tanımlayıcısına karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="83d25-152">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="83d25-153">*Azure planı abonelik kaynakları için, bu rotada **abonelik kimliği** olarak **plan kimliği** sağlayın.*</span><span class="sxs-lookup"><span data-stu-id="83d25-153">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="83d25-154">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="83d25-154">Request headers</span></span>

<span data-ttu-id="83d25-155">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="83d25-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="83d25-156">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="83d25-156">Request body</span></span>

<span data-ttu-id="83d25-157">Yok.</span><span class="sxs-lookup"><span data-stu-id="83d25-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="83d25-158">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="83d25-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/meterusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="83d25-159">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="83d25-159">REST response</span></span>

<span data-ttu-id="83d25-160">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Pagedresourcecollection \<MeterUsageRecord>** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="83d25-160">If successful, this method returns a **PagedResourceCollection\<MeterUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="83d25-161">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="83d25-161">Response success and error codes</span></span>

<span data-ttu-id="83d25-162">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="83d25-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="83d25-163">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="83d25-163">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="83d25-164">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="83d25-164">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="83d25-165">Microsoft Azure (MS-AZR-0145P) abonelikleri için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="83d25-165">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="83d25-166">Bu örnekte, müşteri **145P Azure PayG** satın almıştır.</span><span class="sxs-lookup"><span data-stu-id="83d25-166">In this example, the customer purchased **145P Azure PayG**.</span></span>

<span data-ttu-id="83d25-167">*Microsoft Azure (MS-AZR-0145P) aboneliği olan müşteriler için, API yanıtında hiçbir değişiklik olmaz.*</span><span class="sxs-lookup"><span data-stu-id="83d25-167">*For customers with a Microsoft Azure (MS-AZR-0145P) subscription, there will be no change to API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="83d25-168">Azure planına REST yanıtı örneği</span><span class="sxs-lookup"><span data-stu-id="83d25-168">REST response example for Azure plan</span></span>

<span data-ttu-id="83d25-169">Bu örnekte, müşteri bir Azure planı satın almış.</span><span class="sxs-lookup"><span data-stu-id="83d25-169">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="83d25-170">*Azure planlarına sahip müşteriler için API yanıtında aşağıdaki değişiklikler vardır:*</span><span class="sxs-lookup"><span data-stu-id="83d25-170">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="83d25-171">**Currencylocale** , **CurrencyCode** ile değiştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="83d25-171">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="83d25-172">**Usdtotalcost** yeni bir alandır</span><span class="sxs-lookup"><span data-stu-id="83d25-172">**usdTotalCost** is a new field</span></span>

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
