---
title: Bir abonelik için tüm aylık kullanım kayıtlarını alma
description: AzureResourceMonthlyUsageRecord kaynak koleksiyonunu kullanarak müşterinin aboneliği içindeki hizmetlerin listesini ve ilişkili derecelendirilmiş kullanım bilgilerini edinebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: ee4bd413eec7d5a2dddbe3803df8839589ab7504
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760292"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="47182-103">Bir abonelik için tüm aylık kullanım kayıtlarını alma</span><span class="sxs-lookup"><span data-stu-id="47182-103">Get all monthly usage records for a subscription</span></span>

<span data-ttu-id="47182-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="47182-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="47182-105">[**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) kaynak koleksiyonunu kullanarak müşterinin aboneliği içindeki hizmetlerin listesini ve ilişkili derecelendirilmiş kullanım bilgilerini edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="47182-105">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="47182-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="47182-106">Prerequisites</span></span>

- <span data-ttu-id="47182-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="47182-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="47182-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="47182-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="47182-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="47182-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="47182-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="47182-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="47182-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="47182-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="47182-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="47182-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="47182-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="47182-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="47182-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="47182-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="47182-115">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="47182-115">A subscription identifier.</span></span>

<span data-ttu-id="47182-116">*Bu API yalnızca Microsoft Azure (MS-AZR-0145P) aboneliklerini destekler. Azure planı kullanıyorsanız bkz. [Ölçüme göre abonelik için kullanım verilerini](get-a-customer-subscription-meter-usage-records.md) alma.*</span><span class="sxs-lookup"><span data-stu-id="47182-116">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="47182-117">C\#</span><span class="sxs-lookup"><span data-stu-id="47182-117">C\#</span></span>

<span data-ttu-id="47182-118">Aboneliğin kaynak kullanım bilgilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="47182-118">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="47182-119">**ById()** **yöntemini çağırarak IAggregatePartner.Customers** koleksiyonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="47182-119">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="47182-120">Subscriptions **özelliğini** ve **UsageRecords'ı,** ardından **Resources özelliğini** arayın.</span><span class="sxs-lookup"><span data-stu-id="47182-120">Call the **Subscriptions** property, and **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="47182-121">**Get() veya** **GetAsync() yöntemlerini** çağırma.</span><span class="sxs-lookup"><span data-stu-id="47182-121">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="47182-122">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="47182-122">For an example, see the following:</span></span>

- <span data-ttu-id="47182-123">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="47182-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="47182-124">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="47182-124">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="47182-125">Sınıf: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="47182-125">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="47182-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="47182-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="47182-127">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="47182-127">Request syntax</span></span>

| <span data-ttu-id="47182-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="47182-128">Method</span></span>  | <span data-ttu-id="47182-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="47182-129">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="47182-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="47182-130">**GET**</span></span> | <span data-ttu-id="47182-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="47182-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="47182-132">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="47182-132">URI parameters</span></span>

<span data-ttu-id="47182-133">Bu tabloda, derecelendirilmiş kullanım bilgilerini almak için gerekli sorgu parametreleri listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="47182-133">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="47182-134">Ad</span><span class="sxs-lookup"><span data-stu-id="47182-134">Name</span></span>                    | <span data-ttu-id="47182-135">Tür</span><span class="sxs-lookup"><span data-stu-id="47182-135">Type</span></span>     | <span data-ttu-id="47182-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="47182-136">Required</span></span> | <span data-ttu-id="47182-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="47182-137">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="47182-138">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="47182-138">**customer-tenant-id**</span></span>  | <span data-ttu-id="47182-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="47182-139">**guid**</span></span> | <span data-ttu-id="47182-140">Y</span><span class="sxs-lookup"><span data-stu-id="47182-140">Y</span></span>        | <span data-ttu-id="47182-141">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="47182-141">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="47182-142">**subscription-id**</span><span class="sxs-lookup"><span data-stu-id="47182-142">**subscription-id**</span></span> | <span data-ttu-id="47182-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="47182-143">**guid**</span></span> | <span data-ttu-id="47182-144">Y</span><span class="sxs-lookup"><span data-stu-id="47182-144">Y</span></span>        | <span data-ttu-id="47182-145">Aboneliğe karşılık gelen BIR GUID.</span><span class="sxs-lookup"><span data-stu-id="47182-145">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="47182-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="47182-146">Request headers</span></span>

<span data-ttu-id="47182-147">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="47182-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="47182-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="47182-148">Request body</span></span>

<span data-ttu-id="47182-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="47182-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="47182-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="47182-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="47182-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="47182-151">REST response</span></span>

<span data-ttu-id="47182-152">Başarılı olursa, bu yöntem yanıt gövdesinde **AzureResourceMonthlyUsageRecord** kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="47182-152">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="47182-153">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="47182-153">Response success and error codes</span></span>

<span data-ttu-id="47182-154">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="47182-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="47182-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="47182-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="47182-156">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="47182-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="47182-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="47182-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 648a26a4-a63e-459f-844b-4f29d7913353
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

{
    "totalCount":20,
    "items":[{
        "category":"Storage",
        "subcategory":"LOCALLY REDUNDANT",
        "quantityUsed":0.151287527825352,
        "unit":"GB",
        "id":"2a2419c0-cefe-46b2-8004-8eb002ad606c",
        "name":"Azure Resource 1",
        "totalCost":0.195779159290613,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    },
    {
        "category":"Remote App",
        "subcategory":"Remote App",
        "quantityUsed":0.932546524299563,
        "unit":"GB",
        "id":"7e4099c8-2b3d-41a6-a1bd-d5cf315989b2",
        "name":"Azure Resource 2",
        "totalCost":0.920983775016379,
        "currencyLocale":"en-US",
        "attributes":{
            "objectType":"AzureResourceMonthlyUsageRecord"
        }
    }],
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>%20/usagerecords",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
