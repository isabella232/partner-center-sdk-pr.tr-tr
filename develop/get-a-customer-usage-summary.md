---
title: Müşterinin aboneliklerinin tümü için Kullanım Özeti alın
description: Müşteri 'nin geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı kullanımını almak için CustomerUsageSummary kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c918434367a3514e6a6ad6034b4897c33f51025
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769130"
---
# <a name="get-a-usage-summary-for-all-of-a-customers-subscriptions"></a><span data-ttu-id="21569-103">Müşterinin aboneliklerinin tümü için Kullanım Özeti alın</span><span class="sxs-lookup"><span data-stu-id="21569-103">Get a usage summary for all of a customer's subscriptions</span></span>

<span data-ttu-id="21569-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="21569-104">**Applies to:**</span></span>

- <span data-ttu-id="21569-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="21569-105">Partner Center</span></span>
- <span data-ttu-id="21569-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="21569-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="21569-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="21569-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="21569-108">Müşteri 'nin geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı kullanımını almak için **Customerusagesummary** kaynağını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21569-108">You can use the **CustomerUsageSummary** resource to get a customer's usage of a specific Azure service or resource during the current billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21569-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="21569-109">Prerequisites</span></span>

- <span data-ttu-id="21569-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="21569-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="21569-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="21569-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="21569-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="21569-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="21569-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21569-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="21569-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="21569-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="21569-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="21569-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="21569-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="21569-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="21569-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="21569-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="21569-118">C\#</span><span class="sxs-lookup"><span data-stu-id="21569-118">C\#</span></span>

<span data-ttu-id="21569-119">Müşterinin aboneliklerinin tümü için Kullanım Özeti almak üzere:</span><span class="sxs-lookup"><span data-stu-id="21569-119">To get a usage summary for all of a customer's subscriptions:</span></span>

1. <span data-ttu-id="21569-120">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="21569-120">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="21569-121">**Usagesummary** özelliğini çağırın, ardından **Get ()** veya **GetAsync ()** yöntemleri gelir:</span><span class="sxs-lookup"><span data-stu-id="21569-121">Call the **UsageSummary** property, followed by the **Get()** or **GetAsync()** methods:</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;

    var usageSummary = partnerOperations.Customers.ById(selectedCustomerId).UsageSummary.Get();
    ```

<span data-ttu-id="21569-122">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="21569-122">For an example, see the following:</span></span>

- <span data-ttu-id="21569-123">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="21569-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="21569-124">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="21569-124">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="21569-125">Sınıf: **GetCustomerUsageSummary.cs**</span><span class="sxs-lookup"><span data-stu-id="21569-125">Class: **GetCustomerUsageSummary.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="21569-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="21569-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="21569-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="21569-127">Request syntax</span></span>

| <span data-ttu-id="21569-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="21569-128">Method</span></span>  | <span data-ttu-id="21569-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="21569-129">Request URI</span></span>                                                                                         |
|---------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="21569-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="21569-130">**GET**</span></span> | <span data-ttu-id="21569-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagesummary http/1.1</span><span class="sxs-lookup"><span data-stu-id="21569-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="21569-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="21569-132">URI parameter</span></span>

<span data-ttu-id="21569-133">Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="21569-133">This table lists the required query parameter to get the customer's rated usage information.</span></span>

| <span data-ttu-id="21569-134">Ad</span><span class="sxs-lookup"><span data-stu-id="21569-134">Name</span></span>                   | <span data-ttu-id="21569-135">Tür</span><span class="sxs-lookup"><span data-stu-id="21569-135">Type</span></span>     | <span data-ttu-id="21569-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21569-136">Required</span></span> | <span data-ttu-id="21569-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21569-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="21569-138">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="21569-138">**customer-tenant-id**</span></span> | <span data-ttu-id="21569-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="21569-139">**guid**</span></span> | <span data-ttu-id="21569-140">Y</span><span class="sxs-lookup"><span data-stu-id="21569-140">Y</span></span>        | <span data-ttu-id="21569-141">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="21569-141">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="21569-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="21569-142">Request headers</span></span>

<span data-ttu-id="21569-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="21569-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="21569-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="21569-144">Request body</span></span>

<span data-ttu-id="21569-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="21569-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="21569-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="21569-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/usagesummary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="21569-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="21569-147">REST response</span></span>

<span data-ttu-id="21569-148">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Customerusagesummary** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="21569-148">If successful, this method returns a **CustomerUsageSummary** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="21569-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="21569-149">Response success and error codes</span></span>

<span data-ttu-id="21569-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="21569-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="21569-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="21569-151">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="21569-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="21569-152">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example-for-microsoft-azure-ms-azr-0145p-subscription"></a><span data-ttu-id="21569-153">Microsoft Azure için yanıt örneği (MS-AZR-0145P) aboneliği</span><span class="sxs-lookup"><span data-stu-id="21569-153">Response example for Microsoft Azure (MS-AZR-0145P) subscription</span></span>

<span data-ttu-id="21569-154">Bu örnekte, müşteri bir **145P Azure PayG** teklifi satın almıştır.</span><span class="sxs-lookup"><span data-stu-id="21569-154">In this example, the customer purchased a **145P Azure PayG** offer.</span></span>

<span data-ttu-id="21569-155">*Microsoft Azure (MS-AZR-0145P) aboneliklerine sahip müşteriler için API yanıtında hiçbir değişiklik olmayacaktır.*</span><span class="sxs-lookup"><span data-stu-id="21569-155">*For customers with Microsoft Azure (MS-AZR-0145P) subscriptions, there will be no change to the API response.*</span></span>

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

### <a name="response-example-for-azure-plan"></a><span data-ttu-id="21569-156">Azure planına yönelik yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="21569-156">Response example for Azure plan</span></span>

<span data-ttu-id="21569-157">Bu örnekte, müşteri bir Azure planı satın almış.</span><span class="sxs-lookup"><span data-stu-id="21569-157">In this example, the customer purchased an Azure plan.</span></span>

<span data-ttu-id="21569-158">*Azure planlarına sahip müşteriler için API yanıtında aşağıdaki değişiklikler vardır:*</span><span class="sxs-lookup"><span data-stu-id="21569-158">*For customers with Azure plans, there are the following changes to the API response:*</span></span>

- <span data-ttu-id="21569-159">**Currencylocale** , **CurrencyCode** ile değiştirilmiştir</span><span class="sxs-lookup"><span data-stu-id="21569-159">**currencyLocale** is replaced with **currencyCode**</span></span>
- <span data-ttu-id="21569-160">**Usdtotalcost** yeni bir alandır</span><span class="sxs-lookup"><span data-stu-id="21569-160">**usdTotalCost** is a new field</span></span>

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
