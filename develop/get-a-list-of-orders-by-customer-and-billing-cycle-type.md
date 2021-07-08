---
title: Müşteri ve faturalandırma dönem türüne göre siparişlerin bir listesini alma
description: Belirtilen müşteri ve faturalandırma dönem türü için sipariş kaynakları koleksiyonunu alır.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c52a556887dba065c4ccd1a82d6223624d0ad1f2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874236"
---
# <a name="get-a-list-of-orders-by-customer-and-billing-cycle-type"></a><span data-ttu-id="53fd6-103">Müşteri ve faturalandırma dönem türüne göre siparişlerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="53fd6-103">Get a list of orders by customer and billing cycle type</span></span>

<span data-ttu-id="53fd6-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="53fd6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="53fd6-105">Belirli bir müşteriye ve faturalandırma dönem türüne karşılık gelen sipariş kaynakları koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="53fd6-105">Gets a collection of Order resources that correspond to a given customer and billing cycle type.</span></span> <span data-ttu-id="53fd6-106">Bir siparişin gönderildiği ve müşterinin siparişlerinin koleksiyonunda görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="53fd6-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53fd6-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="53fd6-107">Prerequisites</span></span>

- <span data-ttu-id="53fd6-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="53fd6-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="53fd6-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="53fd6-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="53fd6-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="53fd6-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="53fd6-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53fd6-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="53fd6-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="53fd6-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="53fd6-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="53fd6-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="53fd6-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="53fd6-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="53fd6-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="53fd6-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="53fd6-116">C\#</span><span class="sxs-lookup"><span data-stu-id="53fd6-116">C\#</span></span>

<span data-ttu-id="53fd6-117">Müşterinin siparişlerinin bir koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="53fd6-117">To get a collection of a customer's orders:</span></span>

1. <span data-ttu-id="53fd6-118">[**Iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini seçilen Müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="53fd6-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span>

2. <span data-ttu-id="53fd6-119">[**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğini ve **ByBillingCycleType ()** yöntemini belirtilen [**BillingCycleType**](product-resources.md#billingcycletype)ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="53fd6-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the **ByBillingCycleType()** method with your specified  [**BillingCycleType**](product-resources.md#billingcycletype).</span></span>
3. <span data-ttu-id="53fd6-120">[**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="53fd6-120">Call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// BillingCycleType selectedBillingCycleType;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.ByBillingCycleType(selectedBillingCycleType).Get();
```

## <a name="rest-request"></a><span data-ttu-id="53fd6-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="53fd6-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="53fd6-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="53fd6-122">Request syntax</span></span>

| <span data-ttu-id="53fd6-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="53fd6-123">Method</span></span>  | <span data-ttu-id="53fd6-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="53fd6-124">Request URI</span></span>                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="53fd6-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="53fd6-125">**GET**</span></span> | <span data-ttu-id="53fd6-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Orders? billingType = {faturalandırma-Cycle-Type} http/1.1</span><span class="sxs-lookup"><span data-stu-id="53fd6-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders?billingType={billing-cycle-type} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="53fd6-127">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="53fd6-127">URI parameters</span></span>

<span data-ttu-id="53fd6-128">Bu tabloda, müşteri KIMLIĞINE ve fatura çevrimi türüne göre siparişlerin koleksiyonunu almak için gerekli sorgu parametreleri listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="53fd6-128">This table lists the required query parameters to get a collection of orders by customer ID and billing cycle type.</span></span>

| <span data-ttu-id="53fd6-129">Ad</span><span class="sxs-lookup"><span data-stu-id="53fd6-129">Name</span></span>                   | <span data-ttu-id="53fd6-130">Tür</span><span class="sxs-lookup"><span data-stu-id="53fd6-130">Type</span></span>     | <span data-ttu-id="53fd6-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="53fd6-131">Required</span></span> | <span data-ttu-id="53fd6-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="53fd6-132">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="53fd6-133">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="53fd6-133">customer-tenant-id</span></span>     | <span data-ttu-id="53fd6-134">string</span><span class="sxs-lookup"><span data-stu-id="53fd6-134">string</span></span>   | <span data-ttu-id="53fd6-135">Yes</span><span class="sxs-lookup"><span data-stu-id="53fd6-135">Yes</span></span>      | <span data-ttu-id="53fd6-136">Müşteriye karşılık gelen GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="53fd6-136">A GUID formatted string corresponding to the customer.</span></span>    |
| <span data-ttu-id="53fd6-137">Faturalandırma-geçiş türü</span><span class="sxs-lookup"><span data-stu-id="53fd6-137">billing-cycle-type</span></span>     | <span data-ttu-id="53fd6-138">dize</span><span class="sxs-lookup"><span data-stu-id="53fd6-138">string</span></span>   | <span data-ttu-id="53fd6-139">No</span><span class="sxs-lookup"><span data-stu-id="53fd6-139">No</span></span>       | <span data-ttu-id="53fd6-140">Fatura çevrimi türüne karşılık gelen bir dize.</span><span class="sxs-lookup"><span data-stu-id="53fd6-140">A string corresponding to the billing cycle type.</span></span>         |

### <a name="request-headers"></a><span data-ttu-id="53fd6-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="53fd6-141">Request headers</span></span>

<span data-ttu-id="53fd6-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="53fd6-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="53fd6-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="53fd6-143">Request body</span></span>

<span data-ttu-id="53fd6-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="53fd6-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="53fd6-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="53fd6-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders?billingType=onetime HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="53fd6-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="53fd6-146">REST response</span></span>

<span data-ttu-id="53fd6-147">Başarılı olursa, bu yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="53fd6-147">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="53fd6-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="53fd6-148">Response success and error codes</span></span>

<span data-ttu-id="53fd6-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="53fd6-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="53fd6-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="53fd6-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="53fd6-151">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="53fd6-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="53fd6-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="53fd6-152">Response example</span></span>

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
