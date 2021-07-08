---
title: Müşteri için tüm abonelik kullanım kayıtlarını alma
description: Geçerli faturalama döneminde belirli bir Azure hizmetinin veya kaynağının müşterisi için abonelik kullanım kayıtlarını almak için SubscriptionMonthlyUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 976abd86f34c1c27184f277ffc89fbc65f16bb37
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874695"
---
# <a name="get-subscription-usage-records-for-a-customer"></a><span data-ttu-id="3abe7-103">Müşteri için abonelik kullanım kayıtlarını alma</span><span class="sxs-lookup"><span data-stu-id="3abe7-103">Get subscription usage records for a customer</span></span>

<span data-ttu-id="3abe7-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3abe7-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3abe7-105">Geçerli faturalama döneminde belirli bir Azure hizmetinin veya kaynağının müşterisi için abonelik kullanım kayıtlarını almak için **SubscriptionMonthlyUsageRecord** kaynak koleksiyonunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3abe7-105">You can use the **SubscriptionMonthlyUsageRecord** resource collection to get subscription usage records for a customer of a specific Azure service or resource during the current billing period.</span></span> <span data-ttu-id="3abe7-106">Bu kaynak, müşterinin tüm aboneliklerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3abe7-106">This resource represents all subscriptions for the customer.</span></span> <span data-ttu-id="3abe7-107">Azure planına sahip bir müşteri için bu kaynak, bu planların (tek tek Azure aboneliklerinin değil) listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3abe7-107">For a customer with an Azure plan, this resource returns a list of those plans (not individual Azure subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3abe7-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3abe7-108">Prerequisites</span></span>

- <span data-ttu-id="3abe7-109">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3abe7-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3abe7-110">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3abe7-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3abe7-111">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3abe7-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3abe7-112">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="3abe7-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3abe7-113">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="3abe7-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3abe7-114">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="3abe7-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3abe7-115">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="3abe7-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3abe7-116">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3abe7-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="3abe7-117">C\#</span><span class="sxs-lookup"><span data-stu-id="3abe7-117">C\#</span></span>

<span data-ttu-id="3abe7-118">Geçerli faturalama döneminde belirli bir Azure hizmetinin veya kaynağının müşterisi için abonelik kullanım kayıtlarını almak için aşağıdaki adımları uygulayın:</span><span class="sxs-lookup"><span data-stu-id="3abe7-118">To get subscription usage records for a customer of a specific Azure service or resource during the current billing period, do the following steps:</span></span>

1. <span data-ttu-id="3abe7-119">**ById()** **yöntemini çağırarak IAggregatePartner.Customers** koleksiyonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3abe7-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="3abe7-120">Ardından **Subscriptions özelliğini ve** **UsageRecords özelliğini** arayın.</span><span class="sxs-lookup"><span data-stu-id="3abe7-120">Then call the **Subscriptions** property and the **UsageRecords** property.</span></span> <span data-ttu-id="3abe7-121">Get() veya GetAsync() yöntemlerini çağırarak son.</span><span class="sxs-lookup"><span data-stu-id="3abe7-121">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.UsageRecords.Get();
    ```

<span data-ttu-id="3abe7-122">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="3abe7-122">For an example, see the following:</span></span>

- <span data-ttu-id="3abe7-123">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3abe7-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3abe7-124">Project: **PartnerSDK.FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="3abe7-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="3abe7-125">Sınıf: **GetSubscriptionUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="3abe7-125">Class: **GetSubscriptionUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3abe7-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3abe7-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3abe7-127">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="3abe7-127">Request syntax</span></span>

| <span data-ttu-id="3abe7-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3abe7-128">Method</span></span>  | <span data-ttu-id="3abe7-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3abe7-129">Request URI</span></span>                                                                                                      |
|---------|------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3abe7-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="3abe7-130">**GET**</span></span> | <span data-ttu-id="3abe7-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3abe7-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="3abe7-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="3abe7-132">URI parameter</span></span>

<span data-ttu-id="3abe7-133">Bu tabloda müşterinin derecelendirilmiş kullanım bilgilerini almak için gereken sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="3abe7-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="3abe7-134">Ad</span><span class="sxs-lookup"><span data-stu-id="3abe7-134">Name</span></span>                   | <span data-ttu-id="3abe7-135">Tür</span><span class="sxs-lookup"><span data-stu-id="3abe7-135">Type</span></span>     | <span data-ttu-id="3abe7-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3abe7-136">Required</span></span> | <span data-ttu-id="3abe7-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3abe7-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="3abe7-138">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="3abe7-138">**customer-tenant-id**</span></span> | <span data-ttu-id="3abe7-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="3abe7-139">**guid**</span></span> | <span data-ttu-id="3abe7-140">Y</span><span class="sxs-lookup"><span data-stu-id="3abe7-140">Y</span></span>        | <span data-ttu-id="3abe7-141">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="3abe7-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3abe7-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3abe7-142">Request headers</span></span>

<span data-ttu-id="3abe7-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3abe7-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3abe7-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3abe7-144">Request body</span></span>

<span data-ttu-id="3abe7-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="3abe7-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3abe7-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3abe7-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/usagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="3abe7-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3abe7-147">REST response</span></span>

<span data-ttu-id="3abe7-148">Bu yöntem başarılı olursa yanıt **gövdesinde SubscriptionMonthlyUsageRecord** kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3abe7-148">If successful, this method returns a **SubscriptionMonthlyUsageRecord** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3abe7-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3abe7-149">Response success and error codes</span></span>

<span data-ttu-id="3abe7-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="3abe7-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3abe7-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3abe7-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="3abe7-152">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3abe7-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="3abe7-153">Microsoft Azure (MS-AZR-0145P) abonelikleri için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3abe7-153">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="3abe7-154">Bu örnekte müşteri **145P Azure PayG teklifi satın** alır.</span><span class="sxs-lookup"><span data-stu-id="3abe7-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="3abe7-155">*Microsoft Azure (MS-AZR-0145P) abonelikleri olan müşteriler için API yanıtta değişiklik olmaz.*</span><span class="sxs-lookup"><span data-stu-id="3abe7-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="3abe7-156">Azure planı için REST yanıtı örneği</span><span class="sxs-lookup"><span data-stu-id="3abe7-156">REST response example for Azure plan</span></span>

<span data-ttu-id="3abe7-157">Bu örnekte müşteri bir Azure planı satın alır.</span><span class="sxs-lookup"><span data-stu-id="3abe7-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="3abe7-158">*Azure planları olan müşteriler için API yanıtta aşağıdaki değişiklikler vardır:*</span><span class="sxs-lookup"><span data-stu-id="3abe7-158">*For customers with Azure plans, there are the following changes in the API response:*</span></span>

- <span data-ttu-id="3abe7-159">**currencyLocale,** **currencyCode ile değiştirildi**</span><span class="sxs-lookup"><span data-stu-id="3abe7-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="3abe7-160">**usdTotalCost** yeni bir alandır</span><span class="sxs-lookup"><span data-stu-id="3abe7-160">**usdTotalCost** is a new field</span></span>

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
