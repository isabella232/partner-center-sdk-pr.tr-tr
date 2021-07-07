---
title: Bir abonelik için eklenti satın alma
description: Mevcut bir aboneliğe eklenti satın alma.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547691"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="8dfa4-103">Bir abonelik için eklenti satın alma</span><span class="sxs-lookup"><span data-stu-id="8dfa4-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="8dfa4-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="8dfa4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8dfa4-105">Mevcut bir aboneliğe eklenti satın alma.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-105">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dfa4-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8dfa4-106">Prerequisites</span></span>

- <span data-ttu-id="8dfa4-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="8dfa4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8dfa4-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="8dfa4-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8dfa4-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8dfa4-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="8dfa4-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8dfa4-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="8dfa4-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8dfa4-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="8dfa4-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8dfa4-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8dfa4-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8dfa4-115">Abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-115">A subscription ID.</span></span> <span data-ttu-id="8dfa4-116">Bu, eklenti teklifi satın alınarak satın alınan mevcut aboneliktir.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-116">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="8dfa4-117">Satın alınan eklenti teklifini tanımlayan teklif kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-117">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="8dfa4-118">Kod aracılığıyla eklenti satın alma</span><span class="sxs-lookup"><span data-stu-id="8dfa4-118">Purchasing an add-on through code</span></span>

<span data-ttu-id="8dfa4-119">Bir abonelik için eklenti satın aldığınız zaman, özgün abonelik siparişlerini eklentinin siparişiyle güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-119">When you purchase an add-on to a subscription, you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="8dfa4-120">Aşağıda customerId müşteri kimliği, subscriptionId abonelik kimliği, addOnOfferId ise eklentinin teklif kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-120">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="8dfa4-121">Adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="8dfa4-121">Here are the steps:</span></span>

1.  <span data-ttu-id="8dfa4-122">Aboneliğin işlemleri için bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-122">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="8dfa4-123">Bir abonelik nesnesi örneği için bu arabirimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-123">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="8dfa4-124">Bu, sipariş kimliği de dahil olmak üzere üst abonelik ayrıntılarını size alır.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-124">This gets you the parent subscription details, including the order ID.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="8dfa4-125">Yeni bir Order nesnesi [**örneği**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) oluşturma.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-125">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="8dfa4-126">Bu sipariş örneği, aboneliği satın almak için kullanılan özgün siparişi güncelleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-126">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="8dfa4-127">Eklentiyi temsil eden sıraya tek satırlı bir öğe ekleyin.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-127">Add a single-line item to the order that represents the add-on.</span></span>
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  <span data-ttu-id="8dfa4-128">Aboneliğin özgün siparişlerini eklentinin yeni siparişiyle güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-128">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="8dfa4-129">C\#</span><span class="sxs-lookup"><span data-stu-id="8dfa4-129">C\#</span></span>

<span data-ttu-id="8dfa4-130">Bir eklenti satın almak için, müşteriyi tanımlamak üzere müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim elde edin ve [**subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemi ile eklenti teklifinin yer alan aboneliğini tanıyın.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-130">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="8dfa4-131">[**Al'ı**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) çağırarak abonelik ayrıntılarını almak için bu arabirimi [**kullanın.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)</span><span class="sxs-lookup"><span data-stu-id="8dfa4-131">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="8dfa4-132">Abonelik ayrıntıları, abonelik siparişinin sipariş kimliğini içerir ve bu, eklentiyle güncelleştirilen sipariştir.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-132">The subscription details contain the order ID of the subscription order, which is the order to be updated with the add-on.</span></span>

<span data-ttu-id="8dfa4-133">Ardından yeni bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği ekleyin ve aşağıdaki kod parçacığında gösterildiği gibi eklentiyi tanımlamak için gereken bilgileri içeren tek [**bir LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) örneğiyle doldurmak.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-133">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="8dfa4-134">Bu yeni nesneyi kullanarak abonelik siparişlerini eklentiyle güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-134">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="8dfa4-135">Son olarak, önce [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) ile müşteriyi ve [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)ile siparişi tanımdikten sonra abonelik siparişini güncelleştirmek için [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-135">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

<span data-ttu-id="8dfa4-136">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8dfa4-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8dfa4-137">**Project:** İş Ortağı Merkezi SDK'sı **Samples Sınıfı:** AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="8dfa4-137">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8dfa4-138">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8dfa4-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8dfa4-139">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="8dfa4-139">Request syntax</span></span>

| <span data-ttu-id="8dfa4-140">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8dfa4-140">Method</span></span>    | <span data-ttu-id="8dfa4-141">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8dfa4-141">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8dfa4-142">**Yama**</span><span class="sxs-lookup"><span data-stu-id="8dfa4-142">**PATCH**</span></span> | <span data-ttu-id="8dfa4-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="8dfa4-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="8dfa4-144">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="8dfa4-144">URI parameters</span></span>

<span data-ttu-id="8dfa4-145">Müşteriyi ve siparişi belirlemek için aşağıdaki parametreleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-145">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="8dfa4-146">Ad</span><span class="sxs-lookup"><span data-stu-id="8dfa4-146">Name</span></span>                   | <span data-ttu-id="8dfa4-147">Tür</span><span class="sxs-lookup"><span data-stu-id="8dfa4-147">Type</span></span>     | <span data-ttu-id="8dfa4-148">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8dfa4-148">Required</span></span> | <span data-ttu-id="8dfa4-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8dfa4-149">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="8dfa4-150">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="8dfa4-150">**customer-tenant-id**</span></span> | <span data-ttu-id="8dfa4-151">**guid**</span><span class="sxs-lookup"><span data-stu-id="8dfa4-151">**guid**</span></span> | <span data-ttu-id="8dfa4-152">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-152">Y</span></span>        | <span data-ttu-id="8dfa4-153">Değer, müşteriyi tanımlayan GUID **biçimli bir customer-tenant-id** değeridir.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-153">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="8dfa4-154">**order-id**</span><span class="sxs-lookup"><span data-stu-id="8dfa4-154">**order-id**</span></span>           | <span data-ttu-id="8dfa4-155">**guid**</span><span class="sxs-lookup"><span data-stu-id="8dfa4-155">**guid**</span></span> | <span data-ttu-id="8dfa4-156">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-156">Y</span></span>        | <span data-ttu-id="8dfa4-157">Sipariş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-157">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="8dfa4-158">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8dfa4-158">Request headers</span></span>

<span data-ttu-id="8dfa4-159">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="8dfa4-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8dfa4-160">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="8dfa4-160">Request body</span></span>

<span data-ttu-id="8dfa4-161">Aşağıdaki tablolar istek gövdesinin özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-161">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="8dfa4-162">Sipariş</span><span class="sxs-lookup"><span data-stu-id="8dfa4-162">Order</span></span>

| <span data-ttu-id="8dfa4-163">Ad</span><span class="sxs-lookup"><span data-stu-id="8dfa4-163">Name</span></span>                | <span data-ttu-id="8dfa4-164">Tür</span><span class="sxs-lookup"><span data-stu-id="8dfa4-164">Type</span></span>             | <span data-ttu-id="8dfa4-165">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8dfa4-165">Required</span></span> | <span data-ttu-id="8dfa4-166">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8dfa4-166">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="8dfa4-167">Id</span><span class="sxs-lookup"><span data-stu-id="8dfa4-167">Id</span></span>                  | <span data-ttu-id="8dfa4-168">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-168">string</span></span>           | <span data-ttu-id="8dfa4-169">N</span><span class="sxs-lookup"><span data-stu-id="8dfa4-169">N</span></span>        | <span data-ttu-id="8dfa4-170">Sipariş kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-170">The order ID.</span></span>                                        |
| <span data-ttu-id="8dfa4-171">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="8dfa4-171">ReferenceCustomerId</span></span> | <span data-ttu-id="8dfa4-172">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-172">string</span></span>           | <span data-ttu-id="8dfa4-173">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-173">Y</span></span>        | <span data-ttu-id="8dfa4-174">Müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-174">The customer ID.</span></span>                                     |
| <span data-ttu-id="8dfa4-175">LineItems</span><span class="sxs-lookup"><span data-stu-id="8dfa4-175">LineItems</span></span>           | <span data-ttu-id="8dfa4-176">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="8dfa4-176">array of objects</span></span> | <span data-ttu-id="8dfa4-177">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-177">Y</span></span>        | <span data-ttu-id="8dfa4-178">[OrderLineItem nesneleri dizisi.](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="8dfa4-178">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="8dfa4-179">Creationdate</span><span class="sxs-lookup"><span data-stu-id="8dfa4-179">CreationDate</span></span>        | <span data-ttu-id="8dfa4-180">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-180">string</span></span>           | <span data-ttu-id="8dfa4-181">N</span><span class="sxs-lookup"><span data-stu-id="8dfa4-181">N</span></span>        | <span data-ttu-id="8dfa4-182">Siparişin tarih-saat biçiminde oluşturulma tarihi.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-182">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="8dfa4-183">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="8dfa4-183">Attributes</span></span>          | <span data-ttu-id="8dfa4-184">object</span><span class="sxs-lookup"><span data-stu-id="8dfa4-184">object</span></span>           | <span data-ttu-id="8dfa4-185">N</span><span class="sxs-lookup"><span data-stu-id="8dfa4-185">N</span></span>        | <span data-ttu-id="8dfa4-186">"ObjectType": "Order" ifadesini içerir.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-186">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="8dfa4-187">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="8dfa4-187">OrderLineItem</span></span>

| <span data-ttu-id="8dfa4-188">Ad</span><span class="sxs-lookup"><span data-stu-id="8dfa4-188">Name</span></span>                 | <span data-ttu-id="8dfa4-189">Tür</span><span class="sxs-lookup"><span data-stu-id="8dfa4-189">Type</span></span>   | <span data-ttu-id="8dfa4-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8dfa4-190">Required</span></span> | <span data-ttu-id="8dfa4-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8dfa4-191">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="8dfa4-192">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="8dfa4-192">LineItemNumber</span></span>       | <span data-ttu-id="8dfa4-193">sayı</span><span class="sxs-lookup"><span data-stu-id="8dfa4-193">number</span></span> | <span data-ttu-id="8dfa4-194">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-194">Y</span></span>        | <span data-ttu-id="8dfa4-195">0 ile başlayan satır öğesi numarası.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-195">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="8dfa4-196">OfferId</span><span class="sxs-lookup"><span data-stu-id="8dfa4-196">OfferId</span></span>              | <span data-ttu-id="8dfa4-197">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-197">string</span></span> | <span data-ttu-id="8dfa4-198">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-198">Y</span></span>        | <span data-ttu-id="8dfa4-199">Eklentinin teklif kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-199">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="8dfa4-200">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="8dfa4-200">SubscriptionId</span></span>       | <span data-ttu-id="8dfa4-201">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-201">string</span></span> | <span data-ttu-id="8dfa4-202">N</span><span class="sxs-lookup"><span data-stu-id="8dfa4-202">N</span></span>        | <span data-ttu-id="8dfa4-203">Satın alınan eklenti aboneliğinin kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-203">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="8dfa4-204">ParentSubscriptionId</span><span class="sxs-lookup"><span data-stu-id="8dfa4-204">ParentSubscriptionId</span></span> | <span data-ttu-id="8dfa4-205">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-205">string</span></span> | <span data-ttu-id="8dfa4-206">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-206">Y</span></span>        | <span data-ttu-id="8dfa4-207">Eklenti teklifine sahip üst aboneliğin kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-207">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="8dfa4-208">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="8dfa4-208">FriendlyName</span></span>         | <span data-ttu-id="8dfa4-209">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-209">string</span></span> | <span data-ttu-id="8dfa4-210">N</span><span class="sxs-lookup"><span data-stu-id="8dfa4-210">N</span></span>        | <span data-ttu-id="8dfa4-211">Bu satır öğesinin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-211">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="8dfa4-212">Miktar</span><span class="sxs-lookup"><span data-stu-id="8dfa4-212">Quantity</span></span>             | <span data-ttu-id="8dfa4-213">sayı</span><span class="sxs-lookup"><span data-stu-id="8dfa4-213">number</span></span> | <span data-ttu-id="8dfa4-214">Y</span><span class="sxs-lookup"><span data-stu-id="8dfa4-214">Y</span></span>        | <span data-ttu-id="8dfa4-215">Lisans sayısı.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-215">The number of licenses.</span></span>                                      |
| <span data-ttu-id="8dfa4-216">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="8dfa4-216">PartnerIdOnRecord</span></span>    | <span data-ttu-id="8dfa4-217">string</span><span class="sxs-lookup"><span data-stu-id="8dfa4-217">string</span></span> | <span data-ttu-id="8dfa4-218">N</span><span class="sxs-lookup"><span data-stu-id="8dfa4-218">N</span></span>        | <span data-ttu-id="8dfa4-219">Kayıt ortağının MPN kimliği.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-219">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="8dfa4-220">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="8dfa4-220">Attributes</span></span>           | <span data-ttu-id="8dfa4-221">object</span><span class="sxs-lookup"><span data-stu-id="8dfa4-221">object</span></span> | <span data-ttu-id="8dfa4-222">N</span><span class="sxs-lookup"><span data-stu-id="8dfa4-222">N</span></span>        | <span data-ttu-id="8dfa4-223">"ObjectType": "OrderLineItem" ifadesini içerir.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-223">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="8dfa4-224">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8dfa4-224">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="8dfa4-225">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8dfa4-225">REST response</span></span>

<span data-ttu-id="8dfa4-226">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş abonelik siparişlerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-226">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8dfa4-227">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8dfa4-227">Response success and error codes</span></span>

<span data-ttu-id="8dfa4-228">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8dfa4-229">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8dfa4-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8dfa4-230">Tam liste için bkz. [İş Ortağı Merkezi Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="8dfa4-230">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8dfa4-231">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="8dfa4-231">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
