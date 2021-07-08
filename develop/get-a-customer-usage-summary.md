---
title: Müşterinin aboneliklerinin tümü için Kullanım Özeti alın
description: Müşteri 'nin geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı kullanımını almak için CustomerUsageSummary kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 88c69637c94b9263ede6924cf2dd09513aa00f70
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874627"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="1b8da-103">Müşterinin aboneliklerinin tümü için Kullanım Özeti alın</span><span class="sxs-lookup"><span data-stu-id="1b8da-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="1b8da-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1b8da-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1b8da-105">Müşteri 'nin geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı kullanımını almak için **Customerusagesummary** kaynağını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b8da-105">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b8da-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1b8da-106">Prerequisites</span></span>

- <span data-ttu-id="1b8da-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1b8da-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1b8da-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="1b8da-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1b8da-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1b8da-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1b8da-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b8da-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1b8da-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1b8da-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1b8da-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1b8da-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1b8da-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="1b8da-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1b8da-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="1b8da-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1b8da-115">C\#</span><span class="sxs-lookup"><span data-stu-id="1b8da-115">C\#</span></span>

<span data-ttu-id="1b8da-116">Müşterinin aboneliklerinin tümü için Kullanım Özeti almak üzere:</span><span class="sxs-lookup"><span data-stu-id="1b8da-116">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="1b8da-117">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b8da-117">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="1b8da-118">**Usagesummary** özelliğini çağırın, ardından **Get ()** veya **GetAsync ()** yöntemleri gelir:</span><span class="sxs-lookup"><span data-stu-id="1b8da-118">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="1b8da-119">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="1b8da-119">For an example, see the following:</span></span>

- <span data-ttu-id="1b8da-120">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1b8da-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1b8da-121">Project: **partnersdk. featuresamples**</span><span class="sxs-lookup"><span data-stu-id="1b8da-121">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="1b8da-122">Sınıf: **Getcustomerusagesummary. cs**</span><span class="sxs-lookup"><span data-stu-id="1b8da-122">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1b8da-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1b8da-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1b8da-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1b8da-124">Request syntax</span></span>

| <span data-ttu-id="1b8da-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1b8da-125">Method</span></span>  | <span data-ttu-id="1b8da-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1b8da-126">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1b8da-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="1b8da-127">**GET**</span></span> | <span data-ttu-id="1b8da-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="1b8da-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="1b8da-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1b8da-129">URI parameter</span></span>

<span data-ttu-id="1b8da-130">Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="1b8da-130">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="1b8da-131">Ad</span><span class="sxs-lookup"><span data-stu-id="1b8da-131">Name</span></span>                   | <span data-ttu-id="1b8da-132">Tür</span><span class="sxs-lookup"><span data-stu-id="1b8da-132">Type</span></span>     | <span data-ttu-id="1b8da-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1b8da-133">Required</span></span> | <span data-ttu-id="1b8da-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1b8da-134">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="1b8da-135">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="1b8da-135">**customer-tenant-id**</span></span> | <span data-ttu-id="1b8da-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="1b8da-136">**guid**</span></span> | <span data-ttu-id="1b8da-137">Y</span><span class="sxs-lookup"><span data-stu-id="1b8da-137">Y</span></span>        | <span data-ttu-id="1b8da-138">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="1b8da-138">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1b8da-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1b8da-139">Request headers</span></span>

<span data-ttu-id="1b8da-140">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1b8da-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1b8da-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1b8da-141">Request body</span></span>

<span data-ttu-id="1b8da-142">Yok.</span><span class="sxs-lookup"><span data-stu-id="1b8da-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1b8da-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1b8da-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="1b8da-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1b8da-144">REST response</span></span>

<span data-ttu-id="1b8da-145">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Customerusagesummary** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b8da-145">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1b8da-146">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1b8da-146">Response success and error codes</span></span>

<span data-ttu-id="1b8da-147">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1b8da-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1b8da-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b8da-148">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="1b8da-149">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1b8da-149">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="1b8da-150">Microsoft Azure için yanıt örneği (MS-azr-0145p) aboneliği</span><span class="sxs-lookup"><span data-stu-id="1b8da-150">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="1b8da-151">Bu örnekte, müşteri bir **145P Azure PayG** teklifi satın almıştır.</span><span class="sxs-lookup"><span data-stu-id="1b8da-151">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="1b8da-152">*Microsoft Azure (MS-azr-0145p) aboneliklerine sahip müşteriler için apı yanıtında hiçbir değişiklik olmayacaktır.*</span><span class="sxs-lookup"><span data-stu-id="1b8da-152">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget":{
        "ammount":300.000000,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "id":"65726577-C208-40FD-9735-8C85AC9CAC68",
    "name":"600 test",
    "billingStartDate":"2016-02-06T00:00:00-08:00",
    "billingEndDate":"2016-03-05T00:00:00-08:00",
    "totalCost":0.0,
    "currencyLocale":"en-US",
    "lastModifiedDate":"2016-02-26T09:42:54.5130558+00:00",
    "links":{
        "self":{
            "uri":"/customers/{customer-tenant-id}/usagesummary",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"CustomerUsageSummary"
    }
}
```

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="1b8da-153">Azure planına yönelik yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1b8da-153">Response example for Azure plan</span></span>

<span data-ttu-id="1b8da-154">Bu örnekte, müşteri bir Azure planı satın almış.</span><span class="sxs-lookup"><span data-stu-id="1b8da-154">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="1b8da-155">*Azure planlarına sahip müşteriler için API yanıtında aşağıdaki değişiklikler vardır:*</span><span class="sxs-lookup"><span data-stu-id="1b8da-155">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="1b8da-156">**Currencylocale** , **CurrencyCode** ile değiştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="1b8da-156">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="1b8da-157">**Usdtotalcost** yeni bir alandır</span><span class="sxs-lookup"><span data-stu-id="1b8da-157">**usdTotalCost** is a new field</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "budget": {
        "amount": 97,
        "attributes": {
            "objectType": "SpendingBudget"
        }
    },
    "resourceId": "44908a11-641b-4c53-b7fc-0f2bfca8a581",
    "resourceName": "Modern Azure Customer UK",
    "billingStartDate": "2019-09-01T00:00:00+00:00",
    "billingEndDate": "2019-10-01T00:00:00+00:00",
    "totalCost": 28.82860766744404945074,
    "currencyCode": "GBP",
    "usdTotalCost": 35.23000000000000362337,
    "lastModifiedDate": "2019-09-18T17:09:26.16+00:00",
    "attributes": {
        "objectType": "CustomerUsageSummary"
    }
}
```
