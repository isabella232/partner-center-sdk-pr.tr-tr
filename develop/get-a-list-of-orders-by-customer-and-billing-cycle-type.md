---
title: Müşteri ve faturalandırma dönem türüne göre siparişlerin bir listesini alma
description: Belirtilen müşteri ve faturalandırma dönem türü için sipariş kaynakları koleksiyonunu alır.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 43fe08b0791851f915e2b39a25394db5ffd022ca
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769538"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="e42d4-103">Müşteri ve faturalandırma dönem türüne göre siparişlerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="e42d4-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="e42d4-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="e42d4-104">**Applies to:**</span></span>

- <span data-ttu-id="e42d4-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e42d4-105">Partner Center</span></span>
- <span data-ttu-id="e42d4-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e42d4-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="e42d4-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e42d4-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="e42d4-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e42d4-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e42d4-109">Belirli bir müşteriye ve faturalandırma dönem türüne karşılık gelen sipariş kaynakları koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="e42d4-109">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="e42d4-110">Bir siparişin gönderildiği ve müşterinin siparişlerinin koleksiyonunda görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="e42d4-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e42d4-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e42d4-111">Prerequisites</span></span>

- <span data-ttu-id="e42d4-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e42d4-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e42d4-113">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="e42d4-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e42d4-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e42d4-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e42d4-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e42d4-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e42d4-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="e42d4-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e42d4-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="e42d4-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e42d4-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="e42d4-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e42d4-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="e42d4-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="e42d4-120">C\#</span><span class="sxs-lookup"><span data-stu-id="e42d4-120">C\#</span></span>

<span data-ttu-id="e42d4-121">Müşterinin siparişlerinin bir koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="e42d4-121">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="e42d4-122">[**Iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini seçilen Müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="e42d4-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="e42d4-123">[**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğini ve **ByBillingCycleType ()** yöntemini belirtilen [**BillingCycleType**](product-resources.md#billingcycletype)ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="e42d4-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="e42d4-124">[**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="e42d4-124">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="e42d4-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e42d4-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e42d4-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e42d4-126">Request syntax</span></span>

| <span data-ttu-id="e42d4-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e42d4-127">Method</span></span>  | <span data-ttu-id="e42d4-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e42d4-128">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e42d4-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="e42d4-129">**GET**</span></span> | <span data-ttu-id="e42d4-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders? billingType = {faturalandırma-Cycle-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e42d4-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="e42d4-131">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="e42d4-131">URI parameters</span></span>

<span data-ttu-id="e42d4-132">Bu tabloda, müşteri KIMLIĞINE ve fatura çevrimi türüne göre siparişlerin koleksiyonunu almak için gerekli sorgu parametreleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="e42d4-132">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="e42d4-133">Ad</span><span class="sxs-lookup"><span data-stu-id="e42d4-133">Name</span></span>                   | <span data-ttu-id="e42d4-134">Tür</span><span class="sxs-lookup"><span data-stu-id="e42d4-134">Type</span></span>     | <span data-ttu-id="e42d4-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e42d4-135">Required</span></span> | <span data-ttu-id="e42d4-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e42d4-136">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="e42d4-137">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="e42d4-137">customer-tenant-id</span></span>     | <span data-ttu-id="e42d4-138">string</span><span class="sxs-lookup"><span data-stu-id="e42d4-138">string</span></span>   | <span data-ttu-id="e42d4-139">Yes</span><span class="sxs-lookup"><span data-stu-id="e42d4-139">Yes</span></span>      | <span data-ttu-id="e42d4-140">Müşteriye karşılık gelen GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="e42d4-140">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="e42d4-141">Faturalandırma-geçiş türü</span><span class="sxs-lookup"><span data-stu-id="e42d4-141">billing-cycle-type</span></span>     | <span data-ttu-id="e42d4-142">dize</span><span class="sxs-lookup"><span data-stu-id="e42d4-142">string</span></span>   | <span data-ttu-id="e42d4-143">No</span><span class="sxs-lookup"><span data-stu-id="e42d4-143">No</span></span>       | <span data-ttu-id="e42d4-144">Fatura çevrimi türüne karşılık gelen bir dize.</span><span class="sxs-lookup"><span data-stu-id="e42d4-144">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="e42d4-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e42d4-145">Request headers</span></span>

<span data-ttu-id="e42d4-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e42d4-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e42d4-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e42d4-147">Request body</span></span>

<span data-ttu-id="e42d4-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="e42d4-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e42d4-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e42d4-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e42d4-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e42d4-150">REST response</span></span>

<span data-ttu-id="e42d4-151">Başarılı olursa, bu yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="e42d4-151">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e42d4-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e42d4-152">Response success and error codes</span></span>

<span data-ttu-id="e42d4-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e42d4-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e42d4-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e42d4-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e42d4-155">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e42d4-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e42d4-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e42d4-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 97fa8b4f-6576-4cd9-dd19-ac7c97a023a7
MS-RequestId: 3c6a034c-82ee-4095-d50f-9b530a415f1f
MS-CV: nb4/b3Yl2keY0eYR.0
MS-ServerId: 202010607
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Order"
            }
        },
        {
            "id": "s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4Z:002P:DZH318Z0CL2D",
                    "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_3_Years",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4Z/skus/002P?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T01:42:36.8440279Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/s-BZlr_TeGksPNT61SsWRL-sqMaKbyVa1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": { "objectType": "Order" }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType":
        "Collection"
    }
}
```
