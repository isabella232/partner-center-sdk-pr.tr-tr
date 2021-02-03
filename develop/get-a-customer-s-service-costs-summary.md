---
title: Müşterinin hizmet maliyetleri özetini alma
description: Belirtilen fatura dönemi için müşterinin hizmet maliyetlerini alır.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 635e61342e13c3676120ec0df02f1e8bffda64ac
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769347"
---
# <a name="get-a-customers-service-costs-summary"></a><span data-ttu-id="0f20d-103">Müşterinin hizmet maliyetleri özetini alma</span><span class="sxs-lookup"><span data-stu-id="0f20d-103">Get a customer's service costs summary</span></span>

<span data-ttu-id="0f20d-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="0f20d-104">**Applies to:**</span></span>

- <span data-ttu-id="0f20d-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0f20d-105">Partner Center</span></span>

<span data-ttu-id="0f20d-106">Belirtilen fatura dönemi için müşterinin hizmet maliyetlerini alır.</span><span class="sxs-lookup"><span data-stu-id="0f20d-106">Gets a customer's service costs for the specified billing period.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f20d-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0f20d-107">Prerequisites</span></span>

- <span data-ttu-id="0f20d-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0f20d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0f20d-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="0f20d-109">This scenario supports authentication with App+User credentials.</span></span>

- <span data-ttu-id="0f20d-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f20d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0f20d-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f20d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0f20d-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="0f20d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0f20d-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0f20d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0f20d-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="0f20d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0f20d-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="0f20d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0f20d-116">Bir fatura dönemi göstergesi ( **`mostrecent`** ).</span><span class="sxs-lookup"><span data-stu-id="0f20d-116">A billing period indicator (**`mostrecent`**).</span></span>

## <a name="c"></a><span data-ttu-id="0f20d-117">C\#</span><span class="sxs-lookup"><span data-stu-id="0f20d-117">C\#</span></span>

<span data-ttu-id="0f20d-118">Belirtilen müşteriye yönelik bir hizmet maliyetleri Özeti almak için:</span><span class="sxs-lookup"><span data-stu-id="0f20d-118">To retrieve a service costs summary for the specified customer:</span></span>

1. <span data-ttu-id="0f20d-119">Müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0f20d-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="0f20d-120">Müşteri Hizmetleri maliyet toplama işlemlerine yönelik bir arabirim almak için [**Servicemaliyetler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f20d-120">Use the [**ServiceCosts**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicecosts) property to get an interface to customer service costs collection operations.</span></span>

3. <span data-ttu-id="0f20d-121">Bir [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection)döndürmek Için [**Servicecostsbillingperiod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) numaralandırmasının bir üyesiyle [**bybillingperiod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="0f20d-121">Call the [**ByBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.icustomerservicecostscollection.bybillingperiod) method with a member of the [**ServiceCostsBillingPeriod**](/dotnet/api/microsoft.store.partnercenter.models.servicecosts.servicecostsbillingperiod) enumeration to return an [**IServiceCostsCollection**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostscollection).</span></span>

4. <span data-ttu-id="0f20d-122">Müşterinin hizmet maliyetleri özetini almak için [**IServiceCostsCollection. Summary. Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f20d-122">Use the [**IServiceCostsCollection.Summary.Get**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customers.servicecosts.iservicecostsummary.getasync) method to get the customer's service costs summary.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var serviceCostsSummary = partnerOperations.Customers.ById(selectedCustomerId).ServiceCosts.ByBillingPeriod(ServiceCostsBillingPeriod.MostRecent).Summary.Get();
```

## <a name="rest-request"></a><span data-ttu-id="0f20d-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0f20d-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0f20d-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0f20d-124">Request syntax</span></span>

| <span data-ttu-id="0f20d-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0f20d-125">Method</span></span>  | <span data-ttu-id="0f20d-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0f20d-126">Request URI</span></span>                                                                                                   |
|---------|---------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0f20d-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="0f20d-127">**GET**</span></span> | <span data-ttu-id="0f20d-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/servicecosts/{Billing-period} http/1.1</span><span class="sxs-lookup"><span data-stu-id="0f20d-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/servicecosts/{billing-period} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="0f20d-129">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="0f20d-129">URI parameters</span></span>

<span data-ttu-id="0f20d-130">Müşteriyi ve fatura dönemini tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f20d-130">Use the following path parameters to identify the customer and the billing period.</span></span>

| <span data-ttu-id="0f20d-131">Ad</span><span class="sxs-lookup"><span data-stu-id="0f20d-131">Name</span></span>           | <span data-ttu-id="0f20d-132">Tür</span><span class="sxs-lookup"><span data-stu-id="0f20d-132">Type</span></span>   | <span data-ttu-id="0f20d-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0f20d-133">Required</span></span> | <span data-ttu-id="0f20d-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f20d-134">Description</span></span>                                                                                                                      |
|----------------|--------|----------|----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0f20d-135">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="0f20d-135">customer-id</span></span>    | <span data-ttu-id="0f20d-136">guid</span><span class="sxs-lookup"><span data-stu-id="0f20d-136">guid</span></span>   | <span data-ttu-id="0f20d-137">Yes</span><span class="sxs-lookup"><span data-stu-id="0f20d-137">Yes</span></span>      | <span data-ttu-id="0f20d-138">Müşteriyi tanımlayan bir GUID biçimli müşteri KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="0f20d-138">A GUID formatted customer ID that identifies the customer.</span></span>                                                                       |
| <span data-ttu-id="0f20d-139">Faturalandırma dönemi</span><span class="sxs-lookup"><span data-stu-id="0f20d-139">billing-period</span></span> | <span data-ttu-id="0f20d-140">string</span><span class="sxs-lookup"><span data-stu-id="0f20d-140">string</span></span> | <span data-ttu-id="0f20d-141">Yes</span><span class="sxs-lookup"><span data-stu-id="0f20d-141">Yes</span></span>      | <span data-ttu-id="0f20d-142">Fatura dönemini temsil eden bir gösterge.</span><span class="sxs-lookup"><span data-stu-id="0f20d-142">An indicator that represents the billing period.</span></span> <span data-ttu-id="0f20d-143">Yalnızca Mostson değeri desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0f20d-143">The only supported value is MostRecent.</span></span> <span data-ttu-id="0f20d-144">Dizenin büyük küçük bir önemi yoktur.</span><span class="sxs-lookup"><span data-stu-id="0f20d-144">The case of the string does not matter.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0f20d-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0f20d-145">Request headers</span></span>

<span data-ttu-id="0f20d-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0f20d-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0f20d-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0f20d-147">Request body</span></span>

<span data-ttu-id="0f20d-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="0f20d-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0f20d-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0f20d-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65726577-c208-40fd-9735-8c85ac9cac68/servicecosts/mostrecent HTTP/1.1
Authorization: Bearer <authorization token>
Accept: application/json
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="0f20d-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0f20d-150">REST response</span></span>

<span data-ttu-id="0f20d-151">Başarılı olursa, yanıt gövdesi hizmet maliyetleri hakkında bilgi sağlayan bir [Servicecostssummary](service-costs-resources.md) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="0f20d-151">If successful, the response body contains a [ServiceCostsSummary](service-costs-resources.md) resource that provides information about the service costs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0f20d-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0f20d-152">Response success and error codes</span></span>

<span data-ttu-id="0f20d-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="0f20d-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0f20d-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f20d-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0f20d-155">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0f20d-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0f20d-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0f20d-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 766
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
MS-RequestId: e6a3b6b2-230a-4813-999d-57f883b60d38
MS-CV: gPPoyNX1X0asAAcw.0
MS-ServerId: 101112202
Date: Fri, 02 Dec 2016 18: 54: 38 GMT

{
    "billingStartDate": "2015-12-12T00:00:00Z",
    "billingEndDate": "2016-01-11T00:00:00Z",
    "pretaxTotal": 17.22,
    "tax": 0.0,
    "afterTaxTotal": 17.22,
    "currencySymbol": "$",
    "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
    "details":
     [
        {
            "invoiceType": "Recurring",
            "summary": {
                "billingStartDate": "2015-12-12T00:00:00Z",
                "billingEndDate": "2016-01-11T00:00:00Z",
                "pretaxTotal": 17.22,
                "tax": 0.0,
                "afterTaxTotal": 17.22,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        },
        {
            "invoiceType": "OneTime",
            "summary": {
                "billingStartDate": "2019-04-01T00:00:00Z",
                "billingEndDate": "2019-04-30T23:59:59.9999999Z",
                "pretaxTotal": 2,
                "tax": 0.2,
                "afterTaxTotal": 2.2,
                "currencyCode": "USD",
                "currencySymbol": "$",
                "customerId": "ae1d5b32-f9ff-4252-b2bf-40e21937a51a",
                "links": {},
                "attributes": {
                    "objectType": "ServiceCostsSummary"
                }
            }
        }
    ],
    "links": {
        "serviceCostLineItems": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent/lineitems",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/ae1d5b32-f9ff-4252-b2bf-40e21937a51a/servicecosts/MostRecent",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "ServiceCostsSummary"
    }
}
```
