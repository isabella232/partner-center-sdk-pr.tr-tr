---
title: Müşterinin aboneliği için Kullanım Özeti al
description: Geçerli fatura döneminde belirli bir Azure hizmetinin veya kaynağının abonelik kullanım özetini almak için SubscriptionUsageSummary kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 30334b6f08829eccf0693b566c11f94cb3ece976
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769137"
---
# <a name="get-usage-summary-for-customers-subscription"></a><span data-ttu-id="9fa64-103">Müşterinin aboneliği için Kullanım Özeti al</span><span class="sxs-lookup"><span data-stu-id="9fa64-103">Get usage summary for customer's subscription</span></span>

<span data-ttu-id="9fa64-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="9fa64-104">**Applies to:**</span></span>

- <span data-ttu-id="9fa64-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9fa64-105">Partner Center</span></span>
- <span data-ttu-id="9fa64-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9fa64-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9fa64-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9fa64-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9fa64-108">Bir müşteri için abonelik Kullanım Özeti almak üzere **Subscriptionusagesummary** kaynağını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fa64-108">You can use the **SubscriptionUsageSummary** resource to get a subscription usage summary for a customer.</span></span> <span data-ttu-id="9fa64-109">Bu kaynak, geçerli fatura döneminde belirli bir Azure hizmetinin veya kaynağının abonelik kullanım özetini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="9fa64-109">This resource represents the subscription usage summary of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9fa64-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9fa64-110">Prerequisites</span></span>

- <span data-ttu-id="9fa64-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9fa64-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9fa64-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9fa64-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9fa64-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9fa64-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9fa64-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9fa64-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9fa64-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9fa64-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9fa64-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9fa64-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9fa64-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="9fa64-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9fa64-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="9fa64-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9fa64-119">Abonelik tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="9fa64-119">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="9fa64-120">C\#</span><span class="sxs-lookup"><span data-stu-id="9fa64-120">C\#</span></span>

<span data-ttu-id="9fa64-121">Bir müşterinin aboneliğine abonelik Kullanım Özeti almak için:</span><span class="sxs-lookup"><span data-stu-id="9fa64-121">To get a subscription usage summary for a customer's subscription:</span></span>

1. <span data-ttu-id="9fa64-122">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9fa64-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="9fa64-123">Ardından,, ve için de, **Usagesummary** özelliği Ile birlikte abonelikler özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9fa64-123">Then call the Subscriptions property, as well as **UsageSummary** property.</span></span> <span data-ttu-id="9fa64-124">Get () veya GetAsync () yöntemlerini çağırarak son ' a erişin.</span><span class="sxs-lookup"><span data-stu-id="9fa64-124">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var subscriptionUsageSummary = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageSummary.Get();
    ```

<span data-ttu-id="9fa64-125">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="9fa64-125">For an example, see the following:</span></span>

- <span data-ttu-id="9fa64-126">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="9fa64-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="9fa64-127">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="9fa64-127">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="9fa64-128">Sınıf: **GetSubscriptionUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="9fa64-128">Class: **GetSubscriptionUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="9fa64-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9fa64-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9fa64-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9fa64-130">Request syntax</span></span>

| <span data-ttu-id="9fa64-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9fa64-131">Method</span></span>  | <span data-ttu-id="9fa64-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9fa64-132">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9fa64-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="9fa64-133">**GET**</span></span> | <span data-ttu-id="9fa64-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{Subscription-id}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="9fa64-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="9fa64-135">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="9fa64-135">URI parameters</span></span>

<span data-ttu-id="9fa64-136">Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametreleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="9fa64-136">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="9fa64-137">Ad</span><span class="sxs-lookup"><span data-stu-id="9fa64-137">Name</span></span>                   | <span data-ttu-id="9fa64-138">Tür</span><span class="sxs-lookup"><span data-stu-id="9fa64-138">Type</span></span>     | <span data-ttu-id="9fa64-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9fa64-139">Required</span></span> | <span data-ttu-id="9fa64-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9fa64-140">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="9fa64-141">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="9fa64-141">**customer-tenant-id**</span></span> | <span data-ttu-id="9fa64-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="9fa64-142">**guid**</span></span> | <span data-ttu-id="9fa64-143">Y</span><span class="sxs-lookup"><span data-stu-id="9fa64-143">Y</span></span>        | <span data-ttu-id="9fa64-144">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="9fa64-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="9fa64-145">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="9fa64-145">**subscription-id**</span></span>    | <span data-ttu-id="9fa64-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="9fa64-146">**guid**</span></span> | <span data-ttu-id="9fa64-147">Y</span><span class="sxs-lookup"><span data-stu-id="9fa64-147">Y</span></span>        | <span data-ttu-id="9fa64-148">Bir aboneliğin tanımlayıcısına karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="9fa64-148">A GUID corresponding to the identifier of a subscription.</span></span> <span data-ttu-id="9fa64-149">Azure planı için, bu, Azure planını temsil eden karşılık gelen Iş Ortağı Merkezi [abonelik kaynağının](subscription-resources.md#subscription)tanıtıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="9fa64-149">For an Azure plan, this is the identifier of the corresponding Partner Center [subscription resource](subscription-resources.md#subscription), which represents the Azure plan.</span></span> <span data-ttu-id="9fa64-150">*Azure planı abonelik kaynakları için, bu rotada **abonelik kimliği** olarak **plan kimliği** sağlayın.*</span><span class="sxs-lookup"><span data-stu-id="9fa64-150">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9fa64-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9fa64-151">Request headers</span></span>

<span data-ttu-id="9fa64-152">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9fa64-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9fa64-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9fa64-153">Request body</span></span>

<span data-ttu-id="9fa64-154">Yok.</span><span class="sxs-lookup"><span data-stu-id="9fa64-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9fa64-155">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9fa64-155">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="9fa64-156">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9fa64-156">REST response</span></span>

<span data-ttu-id="9fa64-157">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Subscriptionusagesummary** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="9fa64-157">If successful, this method returns a **SubscriptionUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9fa64-158">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9fa64-158">Response success and error codes</span></span>

<span data-ttu-id="9fa64-159">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9fa64-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9fa64-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9fa64-160">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="9fa64-161">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9fa64-161">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="9fa64-162">Microsoft Azure (MS-AZR-0145P) abonelikleri için yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9fa64-162">Response example for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="9fa64-163">Bu örnekte, müşteri bir **145P Azure PayG** teklifi satın almıştır.</span><span class="sxs-lookup"><span data-stu-id="9fa64-163">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="9fa64-164">*Microsoft Azure (MS-AZR-0145P) aboneliklerine sahip müşteriler için API yanıtında hiçbir değişiklik olmayacaktır.*</span><span class="sxs-lookup"><span data-stu-id="9fa64-164">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "id": "ABCDEFGH-F347-41B6-B02C-187B1B778A43",
    "resourceName": "Microsoft Azure",
    "name": "Microsoft Azure",
    "billingStartDate": "2019-08-28T00:00:00-07:00",
    "billingEndDate": "2019-09-27T00:00:00-07:00",
    "totalCost": 22.861172,
    "currencyLocale": "fr-FR",
    "lastModifiedDate": "2019-09-01T23:04:41.193+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```

## <a name="rest-response-example-for-azure-plan"></a><span data-ttu-id="9fa64-165">Azure planına REST yanıtı örneği</span><span class="sxs-lookup"><span data-stu-id="9fa64-165">REST response example for Azure plan</span></span>

<span data-ttu-id="9fa64-166">Bu örnekte, müşteri bir Azure planı satın almış.</span><span class="sxs-lookup"><span data-stu-id="9fa64-166">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="9fa64-167">*Azure planlarına sahip müşteriler için aşağıdaki API yanıtı değişiklikleri vardır:*</span><span class="sxs-lookup"><span data-stu-id="9fa64-167">*For customers with Azure plans, there are the following API response changes:*</span></span>

- <span data-ttu-id="9fa64-168">**Currencylocale** , **CurrencyCode** ile değiştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="9fa64-168">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="9fa64-169">**Usdtotalcost** yeni bir alandır</span><span class="sxs-lookup"><span data-stu-id="9fa64-169">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac1
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "resourceId": "11111111-dca5-6f31-d3a6-dbbfad9be0fc",
    "resourceName": "Azure plan",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/usagesummary",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SubscriptionUsageSummary"
    }
}
```
