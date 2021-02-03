---
title: Kaynağa göre abonelik için kullanım verilerini alma
description: Geçerli fatura döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin kaynak kullanım kayıtlarını almak üzere ResourceUsageRecord kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e815430730dd7182380e9efd1fea80f9e84d2ce7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769142"
---
# <a name="get-usage-data-for-subscription-by-resource"></a><span data-ttu-id="3b983-103">Kaynağa göre abonelik için kullanım verilerini alma</span><span class="sxs-lookup"><span data-stu-id="3b983-103">Get usage data for subscription by resource</span></span>

<span data-ttu-id="3b983-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="3b983-104">**Applies to:**</span></span>

- <span data-ttu-id="3b983-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b983-105">Partner Center</span></span>
- <span data-ttu-id="3b983-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b983-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3b983-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b983-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3b983-108">Bu makalede **ResourceUsageRecord** kaynağını alma açıklanır.</span><span class="sxs-lookup"><span data-stu-id="3b983-108">This article describes how to get the **ResourceUsageRecord** resource.</span></span> <span data-ttu-id="3b983-109">Bu kaynak, Azure planınızda sağlanan bireysel kaynaklar için aylık toplam toplu toplamı temsil eder.</span><span class="sxs-lookup"><span data-stu-id="3b983-109">This resource represents an aggregated total for the month for individual resources provisioned in your Azure plan.</span></span> <span data-ttu-id="3b983-110">Bu kaynağı, geçerli fatura döneminde belirli Azure hizmetleri veya kaynakları için bir müşterinin kaynak kullanım kayıtlarını almak üzere kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b983-110">You can use this resource to get a customer's resource usage records for specific Azure services or resources during the current billing period.</span></span> <span data-ttu-id="3b983-111">Bu API, daha önce Azure harcama API 'Leri aracılığıyla kullanılamayan verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3b983-111">This API returns data that was not available previously through Azure spending APIs.</span></span>

<span data-ttu-id="3b983-112">*Bu yol Microsoft Azure (MS-AZR-0145P) aboneliklerini desteklemez.*</span><span class="sxs-lookup"><span data-stu-id="3b983-112">*This route does not support Microsoft Azure (MS-AZR-0145P) subscriptions.*</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b983-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3b983-113">Prerequisites</span></span>

- <span data-ttu-id="3b983-114">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3b983-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3b983-115">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3b983-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3b983-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3b983-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3b983-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3b983-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3b983-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="3b983-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3b983-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3b983-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3b983-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="3b983-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3b983-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="3b983-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3b983-122">Abonelik tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="3b983-122">A subscription identifier</span></span>

## <a name="c"></a><span data-ttu-id="3b983-123">C\#</span><span class="sxs-lookup"><span data-stu-id="3b983-123">C\#</span></span>

<span data-ttu-id="3b983-124">Geçerli fatura döneminde belirli bir Azure hizmeti veya kaynağı için bir müşterinin kaynak kullanım kayıtlarını almak için:</span><span class="sxs-lookup"><span data-stu-id="3b983-124">To get resource usage records of a customer for a specific Azure service or resource during the current billing period:</span></span>

1. <span data-ttu-id="3b983-125">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b983-125">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="3b983-126">**UsageRecords** ve ardından **Resources** özelliği ile birlikte abonelikler özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="3b983-126">Call the Subscriptions property, as well as **UsageRecords**, then the **Resources** property.</span></span> <span data-ttu-id="3b983-127">Get () veya GetAsync () yöntemlerini çağırarak son ' a erişin.</span><span class="sxs-lookup"><span data-stu-id="3b983-127">Finish by calling the Get() or GetAsync() methods.</span></span>

    ``` csharp
    // IAggregatePartner partnerOperations;
    // var selectedCustomerId as string;
    // var selectedSubscriptionId as string;

    var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
    ```

<span data-ttu-id="3b983-128">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="3b983-128">For an example, see the following:</span></span>

- <span data-ttu-id="3b983-129">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3b983-129">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3b983-130">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="3b983-130">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="3b983-131">Sınıf: **GetSubscriptionUsageRecordsByResource.cs**</span><span class="sxs-lookup"><span data-stu-id="3b983-131">Class: **GetSubscriptionUsageRecordsByResource.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3b983-132">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3b983-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3b983-133">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3b983-133">Request syntax</span></span>

| <span data-ttu-id="3b983-134">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3b983-134">Method</span></span>  | <span data-ttu-id="3b983-135">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3b983-135">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3b983-136">**Al**</span><span class="sxs-lookup"><span data-stu-id="3b983-136">**GET**</span></span> | <span data-ttu-id="3b983-137">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Subscriptions/{Subscription-id}/resourceusagerecords http/1.1</span><span class="sxs-lookup"><span data-stu-id="3b983-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3b983-138">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="3b983-138">URI parameters</span></span>

<span data-ttu-id="3b983-139">Bu tabloda, müşterinin derecelendirildi kullanım bilgilerini almak için gerekli sorgu parametreleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="3b983-139">This table lists the required query parameters to get the customer's rated usage information.</span></span>

| <span data-ttu-id="3b983-140">Ad</span><span class="sxs-lookup"><span data-stu-id="3b983-140">Name</span></span>                   | <span data-ttu-id="3b983-141">Tür</span><span class="sxs-lookup"><span data-stu-id="3b983-141">Type</span></span>     | <span data-ttu-id="3b983-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3b983-142">Required</span></span> | <span data-ttu-id="3b983-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3b983-143">Description</span></span>                               |
|------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="3b983-144">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="3b983-144">**customer-tenant-id**</span></span> | <span data-ttu-id="3b983-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="3b983-145">**guid**</span></span> | <span data-ttu-id="3b983-146">Y</span><span class="sxs-lookup"><span data-stu-id="3b983-146">Y</span></span>        | <span data-ttu-id="3b983-147">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="3b983-147">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="3b983-148">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="3b983-148">**subscription-id**</span></span>    | <span data-ttu-id="3b983-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="3b983-149">**guid**</span></span> | <span data-ttu-id="3b983-150">Y</span><span class="sxs-lookup"><span data-stu-id="3b983-150">Y</span></span>        | <span data-ttu-id="3b983-151">Bir Microsoft Azure (MS-AZR-0145P) aboneliğini veya bir Azure planını temsil eden bir Iş Ortağı Merkezi [abonelik kaynağının](subscription-resources.md#subscription)tanımlayıcısına karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="3b983-151">A GUID corresponding to the identifier of a Partner Center [subscription resource](subscription-resources.md#subscription), which represents a Microsoft Azure (MS-AZR-0145P) subscription or an Azure plan.</span></span> <span data-ttu-id="3b983-152">*Azure planı abonelik kaynakları için, bu rotada **abonelik kimliği** olarak **plan kimliği** sağlayın.*</span><span class="sxs-lookup"><span data-stu-id="3b983-152">*For Azure plan subscription resources, provide the **plan-id** as the **subscription-id** in this route.*</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3b983-153">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3b983-153">Request headers</span></span>

<span data-ttu-id="3b983-154">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3b983-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3b983-155">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3b983-155">Request body</span></span>

<span data-ttu-id="3b983-156">Yok.</span><span class="sxs-lookup"><span data-stu-id="3b983-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3b983-157">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3b983-157">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-id}/resourceusagerecords HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="3b983-158">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3b983-158">REST response</span></span>

<span data-ttu-id="3b983-159">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Pagedresourcecollection \<ResourceUsageRecord>** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3b983-159">If successful, this method returns a **PagedResourceCollection\<ResourceUsageRecord>** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3b983-160">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3b983-160">Response success and error codes</span></span>

<span data-ttu-id="3b983-161">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3b983-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3b983-162">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b983-162">Use a network trace tool to read this code, the error type, and additional parameters.</span></span> <span data-ttu-id="3b983-163">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3b983-163">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3b983-164">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3b983-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1120
Content-Type: application/json
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
MS-RequestId: e128c8e2-4c33-4940-a3e2-2e59b0abdc67
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    "totalCount": 3,
    "items": [
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/disks/testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "resourceName": "testVM1_OsDisk_1_531d3c99534b4649ae025d485370143e",
            "totalCost": 2.0211938955034572,
            "currencyCode": "GBP",
            "usdTotalCost": 2.4700000000000001,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/TESTRG1/providers/Microsoft.Compute/virtualMachines/testVM1",
            "resourceType": "Microsoft.Compute",
            "entitlementId": "{entitlement-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "TESTRG1",
            "name": "testVM1",
            "resourceName": "testVM1",
            "totalCost": 80.3322286322163563,
            "currencyCode": "GBP",
            "usdTotalCost": 98.1699999999999985,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        },
        {
            "subscriptionId": "{subscription-id}",
            "resourceUri": "/subscriptions/{subscription-id}/resourceGroups/testrg1/providers/Microsoft.Storage/storageAccounts/testrg1diag153",
            "resourceType": "Microsoft.Storage",
            "entitlementId": "{entitlemen-id}",
            "entitlementName": "Partner Subscription",
            "resourceGroupName": "testrg1",
            "name": "testrg1diag153",
            "resourceName": "testrg1diag153",
            "totalCost": 0.0081829712368561032,
            "currencyCode": "GBP",
            "usdTotalCost": 0.0099999999999999997,
            "lastModifiedDate": "2019-09-17T21:08:44.2566667+00:00",
            "attributes": {
                "objectType": "ResourceUsageRecord"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/<customer-tenant-id>/subscriptions/<subscription-id>/resourceusagerecords",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
