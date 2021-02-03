---
title: Bir abonelik için tüm aylık kullanım kayıtlarını alın.
description: Bir müşterinin aboneliği içindeki hizmetlerin listesini ve bunların ilişkili derecelendirdikleri kullanım bilgilerini almak için AzureResourceMonthlyUsageRecord kaynak koleksiyonunu kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1dd09d4976c9626e088cda02ce36669dd7121a99
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769736"
---
# <a name="get-all-monthly-usage-records-for-a-subscription"></a><span data-ttu-id="3632f-103">Bir abonelik için tüm aylık kullanım kayıtlarını alın.</span><span class="sxs-lookup"><span data-stu-id="3632f-103">Get all monthly usage records for a subscription.</span></span>

<span data-ttu-id="3632f-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="3632f-104">**Applies to:**</span></span>

- <span data-ttu-id="3632f-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3632f-105">Partner Center</span></span>
- <span data-ttu-id="3632f-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3632f-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3632f-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3632f-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3632f-108">Bir müşterinin aboneliği içindeki hizmetlerin listesini ve bunların ilişkili derecelendirdikleri kullanım bilgilerini almak için [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) kaynak koleksiyonunu kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3632f-108">You can use the [**AzureResourceMonthlyUsageRecord**](/dotnet/api/microsoft.store.partnercenter.models.usage.azureresourcemonthlyusagerecord) resource collection to get a list of services within a customer's subscription and their associated rated usage information.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3632f-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3632f-109">Prerequisites</span></span>

- <span data-ttu-id="3632f-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3632f-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3632f-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3632f-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3632f-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3632f-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3632f-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3632f-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3632f-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="3632f-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3632f-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3632f-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3632f-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="3632f-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3632f-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="3632f-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3632f-118">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3632f-118">A subscription identifier.</span></span>

<span data-ttu-id="3632f-119">*Bu API yalnızca Microsoft Azure (MS-AZR-0145P) aboneliklerini destekler. Azure planı kullanıyorsanız, bkz. bunun yerine [ölçüm için kullanım verilerini alın](get-a-customer-subscription-meter-usage-records.md) .*</span><span class="sxs-lookup"><span data-stu-id="3632f-119">*This API only supports Microsoft Azure (MS-AZR-0145P) subscriptions. If you are using an Azure plan, see [Get usage data for subscription by meter](get-a-customer-subscription-meter-usage-records.md) instead.*</span></span>

## <a name="c"></a><span data-ttu-id="3632f-120">C\#</span><span class="sxs-lookup"><span data-stu-id="3632f-120">C\#</span></span>

<span data-ttu-id="3632f-121">Bir aboneliğin kaynak kullanım bilgilerini almak için:</span><span class="sxs-lookup"><span data-stu-id="3632f-121">To get a subscription's resource usage information:</span></span>

1. <span data-ttu-id="3632f-122">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="3632f-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="3632f-123">**UsageRecords** ve ardından **Resources** özelliği ile birlikte **abonelikler** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="3632f-123">Call the **Subscriptions** property, as well as **UsageRecords**, then the **Resources** property.</span></span>
3. <span data-ttu-id="3632f-124">**Get ()** veya **GetAsync ()** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="3632f-124">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscriptionID as string;

var usageRecords = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).UsageRecords.Resources.Get();
```

<span data-ttu-id="3632f-125">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="3632f-125">For an example, see the following:</span></span>

- <span data-ttu-id="3632f-126">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="3632f-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="3632f-127">Proje: **Partnersdk. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="3632f-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="3632f-128">Sınıf: **SubscriptionResourceUsageRecords.cs**</span><span class="sxs-lookup"><span data-stu-id="3632f-128">Class: **SubscriptionResourceUsageRecords.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="3632f-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3632f-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3632f-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3632f-130">Request syntax</span></span>

| <span data-ttu-id="3632f-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3632f-131">Method</span></span>  | <span data-ttu-id="3632f-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3632f-132">Request URI</span></span>                                                                                                                                       |
|---------|---------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3632f-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="3632f-133">**GET**</span></span> | <span data-ttu-id="3632f-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Subscriptions/{id-for-Subscription}/usagerecords/Resources http/1.1</span><span class="sxs-lookup"><span data-stu-id="3632f-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="3632f-135">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="3632f-135">URI parameters</span></span>

<span data-ttu-id="3632f-136">Bu tablo, derecelendirilen kullanım bilgilerini almak için gerekli sorgu parametrelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="3632f-136">This table lists the required query parameters to get the rated usage information.</span></span>

| <span data-ttu-id="3632f-137">Ad</span><span class="sxs-lookup"><span data-stu-id="3632f-137">Name</span></span>                    | <span data-ttu-id="3632f-138">Tür</span><span class="sxs-lookup"><span data-stu-id="3632f-138">Type</span></span>     | <span data-ttu-id="3632f-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3632f-139">Required</span></span> | <span data-ttu-id="3632f-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3632f-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="3632f-141">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="3632f-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="3632f-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="3632f-142">**guid**</span></span> | <span data-ttu-id="3632f-143">Y</span><span class="sxs-lookup"><span data-stu-id="3632f-143">Y</span></span>        | <span data-ttu-id="3632f-144">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="3632f-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="3632f-145">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="3632f-145">**subscription-id**</span></span> | <span data-ttu-id="3632f-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="3632f-146">**guid**</span></span> | <span data-ttu-id="3632f-147">Y</span><span class="sxs-lookup"><span data-stu-id="3632f-147">Y</span></span>        | <span data-ttu-id="3632f-148">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="3632f-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3632f-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3632f-149">Request headers</span></span>

<span data-ttu-id="3632f-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3632f-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3632f-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3632f-151">Request body</span></span>

<span data-ttu-id="3632f-152">Yok.</span><span class="sxs-lookup"><span data-stu-id="3632f-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3632f-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3632f-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/usagerecords/resources HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 65b26053-37d0-4303-9fd1-46ad8012bcb6
MS-CorrelationId: 47c36033-af5d-4457-80a4-512c1626fac4
```

## <a name="rest-response"></a><span data-ttu-id="3632f-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3632f-154">REST response</span></span>

<span data-ttu-id="3632f-155">Başarılı olursa, bu yöntem yanıt gövdesinde bir **AzureResourceMonthlyUsageRecord** kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="3632f-155">If successful, this method returns a collection of **AzureResourceMonthlyUsageRecord** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3632f-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3632f-156">Response success and error codes</span></span>

<span data-ttu-id="3632f-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3632f-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3632f-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3632f-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3632f-159">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3632f-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3632f-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3632f-160">Response example</span></span>

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
