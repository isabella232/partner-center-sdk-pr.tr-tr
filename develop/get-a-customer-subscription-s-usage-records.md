---
title: Müşteri için tüm abonelik kullanım kayıtlarını alma
description: Geçerli faturalandırma döneminde belirli bir Azure hizmeti veya kaynağı müşterisi için abonelik kullanım kayıtları almak üzere SubscriptionMonthlyUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 765ea16ff58b462d83ae3b8764b8b34c3ef804dc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769143"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="9da4a-103">Bir müşteri için abonelik kullanım kayıtlarını al</span><span class="sxs-lookup"><span data-stu-id="9da4a-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="9da4a-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="9da4a-104">**Applies to:**</span></span>

- <span data-ttu-id="9da4a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9da4a-105">Partner Center</span></span>
- <span data-ttu-id="9da4a-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9da4a-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9da4a-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9da4a-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9da4a-108">Geçerli faturalandırma döneminde belirli bir Azure hizmeti veya kaynağı müşterisi için abonelik kullanım kayıtları almak üzere **SubscriptionMonthlyUsageRecord** kaynak koleksiyonunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9da4a-108">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="9da4a-109">Bu kaynak müşterinin tüm aboneliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9da4a-109">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="9da4a-110">Azure planına sahip bir müşteri için bu kaynak, bu planların bir listesini döndürür (bireysel Azure abonelikleri değil).</span><span class="sxs-lookup"><span data-stu-id="9da4a-110">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9da4a-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9da4a-111">Prerequisites</span></span>

- <span data-ttu-id="9da4a-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9da4a-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9da4a-113">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9da4a-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9da4a-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9da4a-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9da4a-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9da4a-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9da4a-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9da4a-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9da4a-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9da4a-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9da4a-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="9da4a-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9da4a-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="9da4a-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9da4a-120">C\#</span><span class="sxs-lookup"><span data-stu-id="9da4a-120">C\#</span></span>

<span data-ttu-id="9da4a-121">Geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı müşterisi için abonelik kullanım kayıtları almak için:</span><span class="sxs-lookup"><span data-stu-id="9da4a-121">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period.:</span></span>

1. <span data-ttu-id="9da4a-122">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9da4a-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="9da4a-123">Ardından, **UsageRecords** özelliğini ve ayrıca **abonelikler** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9da4a-123">Then call the **Subscriptions** property, as well as **UsageRecords** property.</span></span> <span data-ttu-id="9da4a-124">Get () veya GetAsync () yöntemlerini çağırarak son ' a erişin.</span><span class="sxs-lookup"><span data-stu-id="9da4a-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="9da4a-125">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="9da4a-125">For an example, see the following:</span></span>

- <span data-ttu-id="9da4a-126">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="9da4a-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="9da4a-127">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="9da4a-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="9da4a-128">Sınıf: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="9da4a-128">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="9da4a-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9da4a-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9da4a-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9da4a-130">Request syntax</span></span>

| <span data-ttu-id="9da4a-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9da4a-131">Method</span></span>  | <span data-ttu-id="9da4a-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9da4a-132">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9da4a-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="9da4a-133">**GET**</span></span> | <span data-ttu-id="9da4a-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Subscriptions/usagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="9da4a-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="9da4a-135">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="9da4a-135">URI parameter</span></span>

<span data-ttu-id="9da4a-136">Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="9da4a-136">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="9da4a-137">Ad</span><span class="sxs-lookup"><span data-stu-id="9da4a-137">Name</span></span>                   | <span data-ttu-id="9da4a-138">Tür</span><span class="sxs-lookup"><span data-stu-id="9da4a-138">Type</span></span>     | <span data-ttu-id="9da4a-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9da4a-139">Required</span></span> | <span data-ttu-id="9da4a-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9da4a-140">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="9da4a-141">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="9da4a-141">**customer-tenant-id**</span></span> | <span data-ttu-id="9da4a-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="9da4a-142">**guid**</span></span> | <span data-ttu-id="9da4a-143">Y</span><span class="sxs-lookup"><span data-stu-id="9da4a-143">Y</span></span>        | <span data-ttu-id="9da4a-144">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="9da4a-144">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9da4a-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9da4a-145">Request headers</span></span>

<span data-ttu-id="9da4a-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9da4a-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9da4a-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9da4a-147">Request body</span></span>

<span data-ttu-id="9da4a-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="9da4a-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9da4a-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9da4a-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="9da4a-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9da4a-150">REST response</span></span>

<span data-ttu-id="9da4a-151">Başarılı olursa, bu yöntem yanıt gövdesinde bir **SubscriptionMonthlyUsageRecord** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="9da4a-151">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9da4a-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9da4a-152">Response success and error codes</span></span>

<span data-ttu-id="9da4a-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9da4a-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9da4a-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9da4a-154">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="9da4a-155">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9da4a-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="9da4a-156">Microsoft Azure (MS-AZR-0145P) abonelikleri için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9da4a-156">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="9da4a-157">Bu örnekte, müşteri bir **145P Azure PayG** teklifi satın almıştır.</span><span class="sxs-lookup"><span data-stu-id="9da4a-157">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="9da4a-158">*Microsoft Azure (MS-AZR-0145P) aboneliklerine sahip müşteriler için API yanıtında hiçbir değişiklik olmayacaktır.*</span><span class="sxs-lookup"><span data-stu-id="9da4a-158">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="9da4a-159">Azure planına REST yanıtı örneği</span><span class="sxs-lookup"><span data-stu-id="9da4a-159">REST response example for Azure plan</span></span>

<span data-ttu-id="9da4a-160">Bu örnekte, müşteri bir Azure planı satın almış.</span><span class="sxs-lookup"><span data-stu-id="9da4a-160">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="9da4a-161">*Azure planlarına sahip müşteriler için API yanıtında aşağıdaki değişiklikler vardır:*</span><span class="sxs-lookup"><span data-stu-id="9da4a-161">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="9da4a-162">**Currencylocale** , **CurrencyCode** ile değiştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="9da4a-162">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="9da4a-163">**Usdtotalcost** yeni bir alandır</span><span class="sxs-lookup"><span data-stu-id="9da4a-163">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 2,
    "items": [
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-7d58-6654-69fa-0797198155d3",
            "id": "11111111-7d58-6654-69fa-0797198155d3",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        },
        {
            "status": "active",
            "partnerOnRecord": "some-id",
            "offerId": "DZH318Z0BPS6:0001:DZH318Z0BML6",
            "resourceId": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "id": "11111111-25aa-ebb8-2bb4-fb406307babd",
            "resourceName": "Azure plan",
            "name": "Azure plan",
            "totalCost": 0,
            "currencyCode": "GBP",
            "usdTotalCost": 0,
            "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
            "attributes": {
                "objectType": "SubscriptionMonthlyUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/usagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
