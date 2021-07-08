---
title: Müşterinin hizmet maliyetleri satır öğelerini alma
description: Belirtilen fatura dönemi için müşterinin hizmet maliyet satırı öğelerini alır.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1bc2914d7c8d41c6d806131444fdc241aa1feb90
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874950"
---
# <a name="get-a-customers-service-costs-line-items"></a><span data-ttu-id="eecb2-103">Müşterinin hizmet maliyetleri satır öğelerini alma</span><span class="sxs-lookup"><span data-stu-id="eecb2-103">Get a customer's service costs line items</span></span>

<span data-ttu-id="eecb2-104">Belirtilen fatura dönemi için müşterinin hizmet maliyet satırı öğelerini alır.</span><span class="sxs-lookup"><span data-stu-id="eecb2-104">Gets a customer's service cost line items for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="eecb2-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="eecb2-105">Prerequisites</span></span>

- <span data-ttu-id="eecb2-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="eecb2-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="eecb2-107">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="eecb2-107">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="eecb2-108">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="eecb2-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="eecb2-109">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="eecb2-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="eecb2-110">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="eecb2-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="eecb2-111">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="eecb2-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="eecb2-112">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="eecb2-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="eecb2-113">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="eecb2-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="eecb2-114">Bir fatura dönemi göstergesi ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="eecb2-114">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="eecb2-115">C\#</span><span class="sxs-lookup"><span data-stu-id="eecb2-115">C\#</span></span>

<span data-ttu-id="eecb2-116">Belirtilen müşteriye yönelik bir hizmet maliyetleri Özeti almak için:</span><span class="sxs-lookup"><span data-stu-id="eecb2-116">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="eecb2-117">Müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="eecb2-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="eecb2-118">Müşteri Hizmetleri maliyet toplama işlemlerine yönelik bir arabirim almak için [**Servicemaliyetler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="eecb2-118">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="eecb2-119">Bir [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)döndürmek Için [**Servicecostsbillingperiod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) numaralandırmasının bir üyesiyle [**bybillingperiod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="eecb2-119">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="eecb2-120">Müşterinin hizmet maliyetleri satır öğelerini almak için [**IServiceCostsCollection. LineItems. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="eecb2-120">Use the [**IServiceCostsCollection.LineItems.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostlineitemscollection.getasync) method to get the customer's service costs line items.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).LineItems.Get();
```

## <a name="rest-request"></a><span data-ttu-id="eecb2-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="eecb2-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="eecb2-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="eecb2-122">Request syntax</span></span>

| <span data-ttu-id="eecb2-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="eecb2-123">Method</span></span>  | <span data-ttu-id="eecb2-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="eecb2-124">Request URI</span></span>                                                                                                             |
|---------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="eecb2-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="eecb2-125">**GET**</span></span> | <span data-ttu-id="eecb2-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/servicecosts/{Billing-period}/LineItems http/1.1</span><span class="sxs-lookup"><span data-stu-id="eecb2-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period}/lineitems HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="eecb2-127">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="eecb2-127">URI parameters</span></span>

<span data-ttu-id="eecb2-128">Müşteriyi ve fatura dönemini tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="eecb2-128">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="eecb2-129">Ad</span><span class="sxs-lookup"><span data-stu-id="eecb2-129">Name</span></span>           | <span data-ttu-id="eecb2-130">Tür</span><span class="sxs-lookup"><span data-stu-id="eecb2-130">Type</span></span>   | <span data-ttu-id="eecb2-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="eecb2-131">Required</span></span> | <span data-ttu-id="eecb2-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="eecb2-132">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="eecb2-133">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="eecb2-133">customer-id</span></span>    | <span data-ttu-id="eecb2-134">guid</span><span class="sxs-lookup"><span data-stu-id="eecb2-134">guid</span></span>   | <span data-ttu-id="eecb2-135">Yes</span><span class="sxs-lookup"><span data-stu-id="eecb2-135">Yes</span></span>      | <span data-ttu-id="eecb2-136">Müşteriyi tanımlayan bir GUID biçimli müşteri KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="eecb2-136">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="eecb2-137">Faturalandırma dönemi</span><span class="sxs-lookup"><span data-stu-id="eecb2-137">billing-period</span></span> | <span data-ttu-id="eecb2-138">string</span><span class="sxs-lookup"><span data-stu-id="eecb2-138">string</span></span> | <span data-ttu-id="eecb2-139">Yes</span><span class="sxs-lookup"><span data-stu-id="eecb2-139">Yes</span></span>      | <span data-ttu-id="eecb2-140">Fatura dönemini temsil eden bir gösterge.</span><span class="sxs-lookup"><span data-stu-id="eecb2-140">An indicator that represents the billing period.</span></span> <span data-ttu-id="eecb2-141">Yalnızca Mostson değeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="eecb2-141">The only supported value is MostRecent.</span></span> <span data-ttu-id="eecb2-142">Dizenin büyük küçük bir önemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="eecb2-142">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="eecb2-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="eecb2-143">Request headers</span></span>

<span data-ttu-id="eecb2-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="eecb2-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="eecb2-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="eecb2-145">Request body</span></span>

<span data-ttu-id="eecb2-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="eecb2-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="eecb2-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="eecb2-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent/lineitems HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="eecb2-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="eecb2-148">REST response</span></span>

<span data-ttu-id="eecb2-149">Başarılı olursa, yanıt gövdesi hizmet maliyetleri hakkında bilgi sağlayan bir [Servicecostlineıtem](service-costs-resources.md) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="eecb2-149">If successful, the response body contains a [ServiceCostLineItem](service-costs-resources.md) resource that provides information about the service costs.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="eecb2-150">Aşağıdaki özellikler yalnızca ürünün *bir kerelik satın alma* işlemi olduğu servis maliyeti satırı öğeleri *için geçerlidir* : **ProductID**, **ProductName**, **skuid**, **skuname**, **kullanılabilirliği bilityıd**, **publisherID**, **PublisherName**, **terdibillingcycle**, **decountdetails**.</span><span class="sxs-lookup"><span data-stu-id="eecb2-150">The following properties *only apply to* service cost line items where the product is a *one-time purchase*: **productId**, **productName**, **skuId**, **skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.</span></span> <span data-ttu-id="eecb2-151">Bu özellikler, ürünün *yinelenen satın alma* işlemi olduğu hizmet satırı öğeleri *için uygulanmaz* .</span><span class="sxs-lookup"><span data-stu-id="eecb2-151">These properties *don't apply to* service line items where the product is a *recurring purchase*.</span></span> <span data-ttu-id="eecb2-152">örneğin, bu özellikler abonelik tabanlı Office 365 ve Azure için *geçerlidir* .</span><span class="sxs-lookup"><span data-stu-id="eecb2-152">For example, these properties *don't apply* to subscription-based Office 365 and Azure.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="eecb2-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="eecb2-153">Response success and error codes</span></span>

<span data-ttu-id="eecb2-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="eecb2-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="eecb2-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="eecb2-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="eecb2-156">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="eecb2-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="eecb2-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="eecb2-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2148
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "attributes": {
        "objectType": "Collection"
    },
    "items":
    [{
            "afterTaxTotal": 0.0,
            "chargeType": "PURCHASE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-01-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 0.0,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2015-12-15T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 0.0,
            "invoiceNumber": "T000003163",
            "invoiceType": "OneTime",
            "productId": "DZH318Z0BJR6",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BMFK",
            "productName": "Azure Managed Experience",
            "skuName": "Azure Managed Experience - Optimize",
            "publisherName": "Microsoft",
            "publisherId": "01323244",
            "termAndBillingCycle": "",
            "discountDetails": "N/A"
        }, {
            "afterTaxTotal": 17.219999999999999,
            "chargeType": "CYCLE FEE",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
            "customerName": "AABB CCDD",
            "endDate": "2016-02-11T00:00:00",
            "offerId": "11E3C9A9-24A2-4CFD-9F60-A9797D68E296",
            "offerName": "Project for Office 365 (Government Pricing)",
            "orderId": "4FEB262A-FAF3-4710-B216-D563421B006F",
            "pretaxTotal": 17.219999999999999,
            "quantity": 1.0,
            "resellerMPNId": "-1",
            "startDate": "2016-01-12T00:00:00",
            "subscriptionFriendlyName": "Project Pro for Office 365 (Government Pricing)",
            "subscriptionId": "71B5BCDD-51C8-4BF2-B704-D3432EE33064",
            "tax": 0.0,
            "unitPrice": 17.219999999999999,
            "invoiceNumber": "D000003163",
            "invoiceType": "Recurring",
            "productId": "DZH318Z0BJR7",
            "skuId": "0001",
            "availabilityId": "DZH318Z0BTTTT",
            "productName": "NGINX Plus",
            "skuName": "NGINX Plus (Ubuntu 14.04)",
            "publisherName": "Nginx, Inc.",
            "publisherId": "212336222",
            "termAndBillingCycle": "30 Days Trial",
            "discountDetails": "20%"
        }
    ],
    "links": {
        "self": {
            "headers": [],
            "method": "GET",
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems"
        }
    },
    "totalCount": 2
}
```
