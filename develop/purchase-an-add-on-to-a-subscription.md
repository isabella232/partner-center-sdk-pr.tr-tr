---
title: Bir abonelik için eklenti satın alma
description: Mevcut bir aboneliğe eklenti satın alma.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769658"
---
# <a name="purchase-an-add-on-to-a-subscription"></a><span data-ttu-id="70cc7-103">Bir abonelik için eklenti satın alma</span><span class="sxs-lookup"><span data-stu-id="70cc7-103">Purchase an add-on to a subscription</span></span>

<span data-ttu-id="70cc7-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="70cc7-104">**Applies To**</span></span>

- <span data-ttu-id="70cc7-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="70cc7-105">Partner Center</span></span>
- <span data-ttu-id="70cc7-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="70cc7-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="70cc7-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="70cc7-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="70cc7-108">Mevcut bir aboneliğe eklenti satın alma.</span><span class="sxs-lookup"><span data-stu-id="70cc7-108">How to purchase an add-on to an existing subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70cc7-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="70cc7-109">Prerequisites</span></span>

- <span data-ttu-id="70cc7-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="70cc7-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="70cc7-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="70cc7-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="70cc7-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="70cc7-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="70cc7-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70cc7-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="70cc7-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="70cc7-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="70cc7-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="70cc7-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="70cc7-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="70cc7-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="70cc7-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="70cc7-118">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-118">A subscription ID.</span></span> <span data-ttu-id="70cc7-119">Bu, eklenti teklifinin satın alınacağı mevcut bir aboneliğiniz.</span><span class="sxs-lookup"><span data-stu-id="70cc7-119">This is the existing subscription for which to purchase an add-on offer.</span></span>

- <span data-ttu-id="70cc7-120">Satın almaya yönelik eklenti teklifini tanımlayan bir teklif KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-120">An offer ID that identifies the add-on offer to purchase.</span></span>

## <a name="purchasing-an-add-on-through-code"></a><span data-ttu-id="70cc7-121">Kod üzerinden eklenti satın alma</span><span class="sxs-lookup"><span data-stu-id="70cc7-121">Purchasing an add-on through code</span></span>

<span data-ttu-id="70cc7-122">Bir aboneliğe eklenti satın aldığınızda, özgün abonelik sırasını eklentinin sırasıyla güncelliyor olursunuz.</span><span class="sxs-lookup"><span data-stu-id="70cc7-122">When you purchase an add-on to a subscription you are updating the original subscription order with the order for the add-on.</span></span> <span data-ttu-id="70cc7-123">Aşağıda, CustomerID müşteri KIMLIĞI, SubscriptionID abonelik KIMLIĞI, Addonofferıd ise eklentinin teklif KIMLIĞIDIR.</span><span class="sxs-lookup"><span data-stu-id="70cc7-123">In the following, customerId is the customer ID, subscriptionId is the subscription ID, and addOnOfferId is the offer ID for the add-on.</span></span>

<span data-ttu-id="70cc7-124">Adımlar aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="70cc7-124">Here are the steps:</span></span>

1.  <span data-ttu-id="70cc7-125">Abonelik işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-125">Get an interface to the operations for the subscription.</span></span>

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  <span data-ttu-id="70cc7-126">Bir abonelik nesnesi oluşturmak için bu arabirimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-126">Use that interface to instantiate a subscription object.</span></span> <span data-ttu-id="70cc7-127">Bu, sipariş kimliği de dahil olmak üzere üst abonelik ayrıntılarını alır.</span><span class="sxs-lookup"><span data-stu-id="70cc7-127">This gets you the parent subscription details, including the order id.</span></span>

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  <span data-ttu-id="70cc7-128">Yeni bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="70cc7-128">Instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object.</span></span> <span data-ttu-id="70cc7-129">Bu sipariş örneği, aboneliği satın almak için kullanılan orijinal sırayı güncelleştirmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="70cc7-129">This order instance is used to update the original order used to purchase the subscription.</span></span> <span data-ttu-id="70cc7-130">Eklentiyi temsil eden sıraya tek satırlık bir öğe ekleyin.</span><span class="sxs-lookup"><span data-stu-id="70cc7-130">Add a single line item to the order that represents the add-on.</span></span>
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

4.  <span data-ttu-id="70cc7-131">Eklenti için yeni siparişle abonelik için orijinal sırayı güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="70cc7-131">Update the original order for the subscription with the new order for the add-on.</span></span>
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a><span data-ttu-id="70cc7-132">C\#</span><span class="sxs-lookup"><span data-stu-id="70cc7-132">C\#</span></span>

<span data-ttu-id="70cc7-133">Bir eklenti satın almak için, müşteriyi belirlemek için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak ve eklenti teklifini içeren aboneliği belirlemek için [**abonelikler. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim edinerek başlayın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-133">To purchase an add-on, begin by obtaining an interface to the subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the subscription that has the add-on offer.</span></span> <span data-ttu-id="70cc7-134">[**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)yöntemini çağırarak abonelik ayrıntılarını almak için bu [**arabirimi**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) kullanın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-134">Use that [**interface**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) to retrieve the subscription details by calling [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get).</span></span> <span data-ttu-id="70cc7-135">Abonelik ayrıntılarına neden ihtiyacınız var?</span><span class="sxs-lookup"><span data-stu-id="70cc7-135">Why do you need the subscription details?</span></span> <span data-ttu-id="70cc7-136">Abonelik siparişinin sipariş kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="70cc7-136">Because you need the order id of the subscription order.</span></span> <span data-ttu-id="70cc7-137">Bu, eklenti ile güncelleştirilme sıraatalım.</span><span class="sxs-lookup"><span data-stu-id="70cc7-137">That's the order to be updated with the add-on.</span></span>

<span data-ttu-id="70cc7-138">Ardından, yeni bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği oluşturun ve aşağıdaki kod parçacığında gösterildiği gibi, eklentiyi tanımlayan bilgileri içeren tek bir [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) örneğiyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="70cc7-138">Next, instantiate a new [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and populate it with a single [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) instance that contains the information to identify the add-on, as shown in the following code snippet.</span></span> <span data-ttu-id="70cc7-139">Bu yeni nesneyi, eklenti ile abonelik sırasını güncelleştirmek için kullanacaksınız.</span><span class="sxs-lookup"><span data-stu-id="70cc7-139">You'll use this new object to update the subscription order with the add-on.</span></span> <span data-ttu-id="70cc7-140">Son olarak, ilk olarak, bir müşteriyi [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) ve [**Orders. byıd**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)ile sipariş olarak tanımladıktan sonra, abonelik sırasını güncelleştirmek için [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-140">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) method to update the subscription order, after first identifying the customer with [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) and the order with [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid).</span></span>

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

<span data-ttu-id="70cc7-141">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="70cc7-141">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="70cc7-142">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: AddSubscriptionAddOn.cs</span><span class="sxs-lookup"><span data-stu-id="70cc7-142">**Project**: Partner Center SDK Samples **Class**: AddSubscriptionAddOn.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="70cc7-143">REST isteği</span><span class="sxs-lookup"><span data-stu-id="70cc7-143">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="70cc7-144">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="70cc7-144">Request syntax</span></span>

| <span data-ttu-id="70cc7-145">Yöntem</span><span class="sxs-lookup"><span data-stu-id="70cc7-145">Method</span></span>    | <span data-ttu-id="70cc7-146">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="70cc7-146">Request URI</span></span>                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="70cc7-147">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="70cc7-147">**PATCH**</span></span> | <span data-ttu-id="70cc7-148">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="70cc7-148">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="70cc7-149">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="70cc7-149">URI parameters</span></span>

<span data-ttu-id="70cc7-150">Müşteriyi ve siparişi tanımlamak için aşağıdaki parametreleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-150">Use the following parameters to identify the customer and order.</span></span>

| <span data-ttu-id="70cc7-151">Ad</span><span class="sxs-lookup"><span data-stu-id="70cc7-151">Name</span></span>                   | <span data-ttu-id="70cc7-152">Tür</span><span class="sxs-lookup"><span data-stu-id="70cc7-152">Type</span></span>     | <span data-ttu-id="70cc7-153">Gerekli</span><span class="sxs-lookup"><span data-stu-id="70cc7-153">Required</span></span> | <span data-ttu-id="70cc7-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="70cc7-154">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="70cc7-155">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="70cc7-155">**customer-tenant-id**</span></span> | <span data-ttu-id="70cc7-156">**guid**</span><span class="sxs-lookup"><span data-stu-id="70cc7-156">**guid**</span></span> | <span data-ttu-id="70cc7-157">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-157">Y</span></span>        | <span data-ttu-id="70cc7-158">Değer, müşteriyi tanımlayan bir GUID biçimli **Müşteri-Kiracı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="70cc7-158">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="70cc7-159">**sıra kimliği**</span><span class="sxs-lookup"><span data-stu-id="70cc7-159">**order-id**</span></span>           | <span data-ttu-id="70cc7-160">**guid**</span><span class="sxs-lookup"><span data-stu-id="70cc7-160">**guid**</span></span> | <span data-ttu-id="70cc7-161">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-161">Y</span></span>        | <span data-ttu-id="70cc7-162">Sıra tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="70cc7-162">The order identifier.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="70cc7-163">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="70cc7-163">Request headers</span></span>

<span data-ttu-id="70cc7-164">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="70cc7-164">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="70cc7-165">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="70cc7-165">Request body</span></span>

<span data-ttu-id="70cc7-166">Aşağıdaki tablolarda, istek gövdesindeki özellikler açıklanır.</span><span class="sxs-lookup"><span data-stu-id="70cc7-166">The following tables describe the properties in the request body.</span></span>

## <a name="order"></a><span data-ttu-id="70cc7-167">Sipariş</span><span class="sxs-lookup"><span data-stu-id="70cc7-167">Order</span></span>

| <span data-ttu-id="70cc7-168">Ad</span><span class="sxs-lookup"><span data-stu-id="70cc7-168">Name</span></span>                | <span data-ttu-id="70cc7-169">Tür</span><span class="sxs-lookup"><span data-stu-id="70cc7-169">Type</span></span>             | <span data-ttu-id="70cc7-170">Gerekli</span><span class="sxs-lookup"><span data-stu-id="70cc7-170">Required</span></span> | <span data-ttu-id="70cc7-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="70cc7-171">Description</span></span>                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| <span data-ttu-id="70cc7-172">Id</span><span class="sxs-lookup"><span data-stu-id="70cc7-172">Id</span></span>                  | <span data-ttu-id="70cc7-173">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-173">string</span></span>           | <span data-ttu-id="70cc7-174">N</span><span class="sxs-lookup"><span data-stu-id="70cc7-174">N</span></span>        | <span data-ttu-id="70cc7-175">Sipariş KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-175">The order ID.</span></span>                                        |
| <span data-ttu-id="70cc7-176">Referencecustomerıd</span><span class="sxs-lookup"><span data-stu-id="70cc7-176">ReferenceCustomerId</span></span> | <span data-ttu-id="70cc7-177">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-177">string</span></span>           | <span data-ttu-id="70cc7-178">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-178">Y</span></span>        | <span data-ttu-id="70cc7-179">Müşteri KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-179">The customer ID.</span></span>                                     |
| <span data-ttu-id="70cc7-180">LineItems</span><span class="sxs-lookup"><span data-stu-id="70cc7-180">LineItems</span></span>           | <span data-ttu-id="70cc7-181">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="70cc7-181">array of objects</span></span> | <span data-ttu-id="70cc7-182">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-182">Y</span></span>        | <span data-ttu-id="70cc7-183">[Orderlineıtem](#orderlineitem) nesneleri dizisi.</span><span class="sxs-lookup"><span data-stu-id="70cc7-183">An array of [OrderLineItem](#orderlineitem) objects.</span></span> |
| <span data-ttu-id="70cc7-184">CreationDate</span><span class="sxs-lookup"><span data-stu-id="70cc7-184">CreationDate</span></span>        | <span data-ttu-id="70cc7-185">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-185">string</span></span>           | <span data-ttu-id="70cc7-186">N</span><span class="sxs-lookup"><span data-stu-id="70cc7-186">N</span></span>        | <span data-ttu-id="70cc7-187">Siparişin oluşturulduğu tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="70cc7-187">The date the order was created, in date-time format.</span></span> |
| <span data-ttu-id="70cc7-188">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="70cc7-188">Attributes</span></span>          | <span data-ttu-id="70cc7-189">object</span><span class="sxs-lookup"><span data-stu-id="70cc7-189">object</span></span>           | <span data-ttu-id="70cc7-190">N</span><span class="sxs-lookup"><span data-stu-id="70cc7-190">N</span></span>        | <span data-ttu-id="70cc7-191">"ObjectType": "Order" içerir.</span><span class="sxs-lookup"><span data-stu-id="70cc7-191">Contains "ObjectType": "Order".</span></span>                      |

## <a name="orderlineitem"></a><span data-ttu-id="70cc7-192">Orderlineıtem</span><span class="sxs-lookup"><span data-stu-id="70cc7-192">OrderLineItem</span></span>

| <span data-ttu-id="70cc7-193">Ad</span><span class="sxs-lookup"><span data-stu-id="70cc7-193">Name</span></span>                 | <span data-ttu-id="70cc7-194">Tür</span><span class="sxs-lookup"><span data-stu-id="70cc7-194">Type</span></span>   | <span data-ttu-id="70cc7-195">Gerekli</span><span class="sxs-lookup"><span data-stu-id="70cc7-195">Required</span></span> | <span data-ttu-id="70cc7-196">Açıklama</span><span class="sxs-lookup"><span data-stu-id="70cc7-196">Description</span></span>                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="70cc7-197">Lineıtemnumber</span><span class="sxs-lookup"><span data-stu-id="70cc7-197">LineItemNumber</span></span>       | <span data-ttu-id="70cc7-198">sayı</span><span class="sxs-lookup"><span data-stu-id="70cc7-198">number</span></span> | <span data-ttu-id="70cc7-199">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-199">Y</span></span>        | <span data-ttu-id="70cc7-200">Satır öğe numarası, 0 ile başlar.</span><span class="sxs-lookup"><span data-stu-id="70cc7-200">The line item number, starting with 0.</span></span>                       |
| <span data-ttu-id="70cc7-201">OfferId</span><span class="sxs-lookup"><span data-stu-id="70cc7-201">OfferId</span></span>              | <span data-ttu-id="70cc7-202">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-202">string</span></span> | <span data-ttu-id="70cc7-203">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-203">Y</span></span>        | <span data-ttu-id="70cc7-204">Eklentinin teklif KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-204">The offer ID of the add-on.</span></span>                                  |
| <span data-ttu-id="70cc7-205">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="70cc7-205">SubscriptionId</span></span>       | <span data-ttu-id="70cc7-206">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-206">string</span></span> | <span data-ttu-id="70cc7-207">N</span><span class="sxs-lookup"><span data-stu-id="70cc7-207">N</span></span>        | <span data-ttu-id="70cc7-208">Satın alınan eklenti aboneliğinin KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-208">The ID of the add-on subscription purchased.</span></span>                 |
| <span data-ttu-id="70cc7-209">Parentsubscriptionıd</span><span class="sxs-lookup"><span data-stu-id="70cc7-209">ParentSubscriptionId</span></span> | <span data-ttu-id="70cc7-210">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-210">string</span></span> | <span data-ttu-id="70cc7-211">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-211">Y</span></span>        | <span data-ttu-id="70cc7-212">Eklenti teklifine sahip olan üst aboneliğin KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-212">The ID of the parent subscription that has the add-on offer.</span></span> |
| <span data-ttu-id="70cc7-213">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="70cc7-213">FriendlyName</span></span>         | <span data-ttu-id="70cc7-214">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-214">string</span></span> | <span data-ttu-id="70cc7-215">N</span><span class="sxs-lookup"><span data-stu-id="70cc7-215">N</span></span>        | <span data-ttu-id="70cc7-216">Bu satır öğesi için kolay ad.</span><span class="sxs-lookup"><span data-stu-id="70cc7-216">The friendly name for this line item.</span></span>                        |
| <span data-ttu-id="70cc7-217">Miktar</span><span class="sxs-lookup"><span data-stu-id="70cc7-217">Quantity</span></span>             | <span data-ttu-id="70cc7-218">sayı</span><span class="sxs-lookup"><span data-stu-id="70cc7-218">number</span></span> | <span data-ttu-id="70cc7-219">Y</span><span class="sxs-lookup"><span data-stu-id="70cc7-219">Y</span></span>        | <span data-ttu-id="70cc7-220">Lisans sayısı.</span><span class="sxs-lookup"><span data-stu-id="70cc7-220">The number of licenses.</span></span>                                      |
| <span data-ttu-id="70cc7-221">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="70cc7-221">PartnerIdOnRecord</span></span>    | <span data-ttu-id="70cc7-222">string</span><span class="sxs-lookup"><span data-stu-id="70cc7-222">string</span></span> | <span data-ttu-id="70cc7-223">N</span><span class="sxs-lookup"><span data-stu-id="70cc7-223">N</span></span>        | <span data-ttu-id="70cc7-224">Kayıt ortağının MPN KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="70cc7-224">The MPN ID of the partner of record.</span></span>                         |
| <span data-ttu-id="70cc7-225">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="70cc7-225">Attributes</span></span>           | <span data-ttu-id="70cc7-226">object</span><span class="sxs-lookup"><span data-stu-id="70cc7-226">object</span></span> | <span data-ttu-id="70cc7-227">N</span><span class="sxs-lookup"><span data-stu-id="70cc7-227">N</span></span>        | <span data-ttu-id="70cc7-228">"ObjectType": "Orderlineıtem" içerir.</span><span class="sxs-lookup"><span data-stu-id="70cc7-228">Contains "ObjectType": "OrderLineItem".</span></span>                      |

### <a name="request-example"></a><span data-ttu-id="70cc7-229">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="70cc7-229">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="70cc7-230">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="70cc7-230">REST response</span></span>

<span data-ttu-id="70cc7-231">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş abonelik sırasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="70cc7-231">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="70cc7-232">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="70cc7-232">Response success and error codes</span></span>

<span data-ttu-id="70cc7-233">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="70cc7-233">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="70cc7-234">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="70cc7-234">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="70cc7-235">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="70cc7-235">For the full list, see [Partner Center Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="70cc7-236">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="70cc7-236">Response example</span></span>

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
