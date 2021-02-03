---
title: Kimliğe göre bir sipariş alma
description: Müşteri ve sipariş KIMLIĞIYLE eşleşen bir sipariş kaynağı alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 0a39d7142e5bf97f9fb345416964d4ed6bb935ad
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769869"
---
# <a name="get-an-order-by-id"></a><span data-ttu-id="a30bb-103">Kimliğe göre bir sipariş alma</span><span class="sxs-lookup"><span data-stu-id="a30bb-103">Get an order by ID</span></span>

<span data-ttu-id="a30bb-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="a30bb-104">**Applies to:**</span></span>

- <span data-ttu-id="a30bb-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a30bb-105">Partner Center</span></span>
- <span data-ttu-id="a30bb-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a30bb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a30bb-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a30bb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a30bb-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a30bb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a30bb-109">Müşteri ve sipariş KIMLIĞIYLE eşleşen bir [sipariş](order-resources.md) kaynağı alır.</span><span class="sxs-lookup"><span data-stu-id="a30bb-109">Gets an [Order](order-resources.md) resource that matches the customer and order ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a30bb-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a30bb-110">Prerequisites</span></span>

- <span data-ttu-id="a30bb-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a30bb-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a30bb-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="a30bb-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a30bb-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="a30bb-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="a30bb-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a30bb-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="a30bb-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="a30bb-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="a30bb-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="a30bb-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="a30bb-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="a30bb-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="a30bb-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="a30bb-119">Bir sipariş KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="a30bb-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="a30bb-120">C\#</span><span class="sxs-lookup"><span data-stu-id="a30bb-120">C\#</span></span>

<span data-ttu-id="a30bb-121">Müşterinin sırasını KIMLIĞE göre almak için:</span><span class="sxs-lookup"><span data-stu-id="a30bb-121">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="a30bb-122">**Iaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-122">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="a30bb-123">[**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğini çağırın ve ardından [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) yöntemini daha sonra bir kez daha yapın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method once more.</span></span>
3. <span data-ttu-id="a30bb-124">[**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync)öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-124">Call [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.getasync).</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedOrderId;

var order = partnerOperations.Customers.ById(selectedCustomerId).Orders.ById(selectedOrderId).Get();
```

<span data-ttu-id="a30bb-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a30bb-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a30bb-126">**Proje**: Partnersdk. Featuresample **sınıfı**: GetOrder.cs</span><span class="sxs-lookup"><span data-stu-id="a30bb-126">**Project**: PartnerSDK.FeatureSample **Class**: GetOrder.cs</span></span>

## <a name="java"></a><span data-ttu-id="a30bb-127">Java</span><span class="sxs-lookup"><span data-stu-id="a30bb-127">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a30bb-128">Müşterinin sırasını KIMLIĞE göre almak için:</span><span class="sxs-lookup"><span data-stu-id="a30bb-128">To get a customer's order by ID:</span></span>

1. <span data-ttu-id="a30bb-129">**Iaggregatepartner. getCustomers** işlevinizi kullanın ve **byıd ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-129">Use your **IAggregatePartner.getCustomers** function and call the **byId()** function.</span></span>

2. <span data-ttu-id="a30bb-130">**GetOrders** işlevini çağırın ve ardından **byıd ()** işlevini daha sonra bir kez daha yapın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-130">Call the **getOrders** function, followed by the **byID()** function once more.</span></span>
3. <span data-ttu-id="a30bb-131">**Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-131">Call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String selectedCustomerId;
// String selectedOrderId;

Order order = partnerOperations.getCustomers().byId(selectedCustomerId).getOrders().byId(selectedOrderId).get();
```

## <a name="powershell"></a><span data-ttu-id="a30bb-132">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a30bb-132">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a30bb-133">Müşterinin sırasını KIMLIĞE göre almak için [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) komutunu yürütün ve **CustomerID** ve **OrderID** parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a30bb-133">To get a customer's order by ID, execute the [**Get-PartnerCustomerOrder**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerOrder.md) command, and specify the **CustomerId** and **OrderId** parameters.</span></span>

```powershell
# $selectedCustomerId
# $selectedOrderId

Get-PartnerCustomerOrder -CustomerId $selectedCustomerId -OrderId $selectedOrderId
```

## <a name="rest-request"></a><span data-ttu-id="a30bb-134">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a30bb-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a30bb-135">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a30bb-135">Request syntax</span></span>

| <span data-ttu-id="a30bb-136">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a30bb-136">Method</span></span>  | <span data-ttu-id="a30bb-137">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a30bb-137">Request URI</span></span>                                                                                                  |
|---------|--------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a30bb-138">**Al**</span><span class="sxs-lookup"><span data-stu-id="a30bb-138">**GET**</span></span> | <span data-ttu-id="a30bb-139">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{ID-for-Order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a30bb-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{id-for-order} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="a30bb-140">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a30bb-140">URI parameters</span></span>

<span data-ttu-id="a30bb-141">Bu tablo, bir order by ID almak için gerekli sorgu parametrelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="a30bb-141">This table lists the required query parameters to get an order by ID.</span></span>

| <span data-ttu-id="a30bb-142">Ad</span><span class="sxs-lookup"><span data-stu-id="a30bb-142">Name</span></span>                   | <span data-ttu-id="a30bb-143">Tür</span><span class="sxs-lookup"><span data-stu-id="a30bb-143">Type</span></span>     | <span data-ttu-id="a30bb-144">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a30bb-144">Required</span></span> | <span data-ttu-id="a30bb-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a30bb-145">Description</span></span>                                            |
|------------------------|----------|----------|--------------------------------------------------------|
| <span data-ttu-id="a30bb-146">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="a30bb-146">customer-tenant-id</span></span>     | <span data-ttu-id="a30bb-147">string</span><span class="sxs-lookup"><span data-stu-id="a30bb-147">string</span></span>   | <span data-ttu-id="a30bb-148">Yes</span><span class="sxs-lookup"><span data-stu-id="a30bb-148">Yes</span></span>      | <span data-ttu-id="a30bb-149">Müşteriye karşılık gelen GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="a30bb-149">A GUID formatted string corresponding to the customer.</span></span> |
| <span data-ttu-id="a30bb-150">sıra kimliği</span><span class="sxs-lookup"><span data-stu-id="a30bb-150">id-for-order</span></span>           | <span data-ttu-id="a30bb-151">string</span><span class="sxs-lookup"><span data-stu-id="a30bb-151">string</span></span>   | <span data-ttu-id="a30bb-152">Yes</span><span class="sxs-lookup"><span data-stu-id="a30bb-152">Yes</span></span>      | <span data-ttu-id="a30bb-153">Sipariş KIMLIĞINE karşılık gelen bir dize.</span><span class="sxs-lookup"><span data-stu-id="a30bb-153">A string corresponding to the order ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="a30bb-154">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a30bb-154">Request headers</span></span>

<span data-ttu-id="a30bb-155">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a30bb-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a30bb-156">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a30bb-156">Request body</span></span>

<span data-ttu-id="a30bb-157">Yok.</span><span class="sxs-lookup"><span data-stu-id="a30bb-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a30bb-158">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a30bb-158">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<id-for-order> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a30bb-159">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a30bb-159">REST response</span></span>

<span data-ttu-id="a30bb-160">Başarılı olursa, bu yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="a30bb-160">If successful, this method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a30bb-161">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a30bb-161">Response success and error codes</span></span>

<span data-ttu-id="a30bb-162">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a30bb-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a30bb-163">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a30bb-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a30bb-164">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a30bb-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a30bb-165">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a30bb-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 823
Content-Type: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 22:05:30 GMT

{
    "id": "YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
    "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol" : "$",
    "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "DZH318Z0BQ4Z:002L:DZH318Z0CMNP",
        "friendlyName": "Reserved_VM_Instance_Standard_NC12_AU_East_1_Year",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4Z/skus/002L?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
    ],
    "creationDate": "2018-03-13T22:49:54.3396949Z",
    "status": "completed",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/YxH1q4KScfvfkJQjgRI8QY1DznnUWZTH1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
