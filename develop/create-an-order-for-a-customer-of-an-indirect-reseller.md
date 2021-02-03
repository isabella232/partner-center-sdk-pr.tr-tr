---
title: Dolaylı satıcı için müşteri siparişi oluştur
description: Dolaylı bir satıcının müşterisi için sipariş oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makale önkoşulları, adımları ve Exmaples 'leri içerir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770154"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="4e13c-104">Dolaylı satıcı müşterisi için bir sipariş oluşturma</span><span class="sxs-lookup"><span data-stu-id="4e13c-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="4e13c-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="4e13c-105">**Applies to:**</span></span>

- <span data-ttu-id="4e13c-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4e13c-106">Partner Center</span></span>

<span data-ttu-id="4e13c-107">Dolaylı bir satıcı müşterisi için sipariş oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4e13c-107">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e13c-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4e13c-108">Prerequisites</span></span>

- <span data-ttu-id="4e13c-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4e13c-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4e13c-110">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4e13c-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4e13c-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4e13c-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4e13c-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e13c-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4e13c-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="4e13c-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4e13c-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4e13c-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4e13c-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4e13c-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="4e13c-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4e13c-117">Satın alınacak öğenin teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-117">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="4e13c-118">Dolaylı Bayi kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-118">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="4e13c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="4e13c-119">C\#</span></span>

<span data-ttu-id="4e13c-120">Dolaylı bir satıcının müşterisi için sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="4e13c-120">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="4e13c-121">Oturum açmış iş ortağıyla ilişkisi olan dolaylı satıcıların bir koleksiyonunu alın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-121">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="4e13c-122">Koleksiyonda dolaylı satıcı KIMLIĞIYLE eşleşen öğeye yerel bir değişken alın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-122">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="4e13c-123">Bu adım, siparişi oluştururken satıcının [**Mpnıd**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) özelliğine erişmenize yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4e13c-123">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="4e13c-124">Bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği oluşturun ve müşteriyi kaydetmek Için [**Referencecustomerıd**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) özelliğini müşteri tanımlayıcısı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-124">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="4e13c-125">[**Orderlineıtem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) nesnelerinin bir listesini oluşturun ve listeyi Order 's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) özelliğine atayın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-125">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="4e13c-126">Her sipariş satırı öğesi, bir teklifin satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="4e13c-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="4e13c-127">Her bir satır öğesinde [**Partneridonrecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) özelliğini dolaylı satıcının MPN kimliğiyle doldurduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="4e13c-127">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="4e13c-128">En az bir sipariş satırı öğesine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="4e13c-128">You must have at least one order line item.</span></span>

5. <span data-ttu-id="4e13c-129">Müşteriyi tanımlamak için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak işlemleri sipariş etmek için bir arabirim edinin ve ardından [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğinden arabirimi alın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-129">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="4e13c-130">Siparişi oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-130">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="4e13c-131">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="4e13c-131">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="4e13c-132">**Örnek**: [konsol test uygulaması](console-test-app.md)**PROJESI**: iş ortağı Merkezi SDK örnekleri **sınıfı**: PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="4e13c-132">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4e13c-133">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4e13c-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4e13c-134">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4e13c-134">Request syntax</span></span>

| <span data-ttu-id="4e13c-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4e13c-135">Method</span></span>   | <span data-ttu-id="4e13c-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4e13c-136">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="4e13c-137">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="4e13c-137">**POST**</span></span> | <span data-ttu-id="4e13c-138">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="4e13c-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4e13c-139">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="4e13c-139">URI parameters</span></span>

<span data-ttu-id="4e13c-140">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-140">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="4e13c-141">Ad</span><span class="sxs-lookup"><span data-stu-id="4e13c-141">Name</span></span>        | <span data-ttu-id="4e13c-142">Tür</span><span class="sxs-lookup"><span data-stu-id="4e13c-142">Type</span></span>   | <span data-ttu-id="4e13c-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e13c-143">Required</span></span> | <span data-ttu-id="4e13c-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e13c-144">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="4e13c-145">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="4e13c-145">customer-id</span></span> | <span data-ttu-id="4e13c-146">string</span><span class="sxs-lookup"><span data-stu-id="4e13c-146">string</span></span> | <span data-ttu-id="4e13c-147">Yes</span><span class="sxs-lookup"><span data-stu-id="4e13c-147">Yes</span></span>      | <span data-ttu-id="4e13c-148">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="4e13c-148">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4e13c-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4e13c-149">Request headers</span></span>

<span data-ttu-id="4e13c-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4e13c-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4e13c-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4e13c-151">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="4e13c-152">Sipariş</span><span class="sxs-lookup"><span data-stu-id="4e13c-152">Order</span></span>

<span data-ttu-id="4e13c-153">Bu tablo, istek gövdesindeki **sıra** özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4e13c-153">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="4e13c-154">Ad</span><span class="sxs-lookup"><span data-stu-id="4e13c-154">Name</span></span> | <span data-ttu-id="4e13c-155">Tür</span><span class="sxs-lookup"><span data-stu-id="4e13c-155">Type</span></span> | <span data-ttu-id="4e13c-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e13c-156">Required</span></span> | <span data-ttu-id="4e13c-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e13c-157">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="4e13c-158">kimlik</span><span class="sxs-lookup"><span data-stu-id="4e13c-158">id</span></span> | <span data-ttu-id="4e13c-159">dize</span><span class="sxs-lookup"><span data-stu-id="4e13c-159">string</span></span> | <span data-ttu-id="4e13c-160">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-160">No</span></span> | <span data-ttu-id="4e13c-161">Siparişin başarıyla oluşturulması sırasında sağlanan bir sipariş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-161">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="4e13c-162">Referencecustomerıd</span><span class="sxs-lookup"><span data-stu-id="4e13c-162">referenceCustomerId</span></span> | <span data-ttu-id="4e13c-163">string</span><span class="sxs-lookup"><span data-stu-id="4e13c-163">string</span></span> | <span data-ttu-id="4e13c-164">Yes</span><span class="sxs-lookup"><span data-stu-id="4e13c-164">Yes</span></span> | <span data-ttu-id="4e13c-165">Müşteri tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-165">The customer identifier.</span></span> |
| <span data-ttu-id="4e13c-166">Bilimlingcycle</span><span class="sxs-lookup"><span data-stu-id="4e13c-166">billingCycle</span></span> | <span data-ttu-id="4e13c-167">dize</span><span class="sxs-lookup"><span data-stu-id="4e13c-167">string</span></span> | <span data-ttu-id="4e13c-168">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-168">No</span></span> | <span data-ttu-id="4e13c-169">Bu sipariş için ortağın faturalandırılma sıklığı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-169">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="4e13c-170">Varsayılan değer &quot; aylık &quot; ' dır ve siparişin başarıyla oluşturulması üzerine uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4e13c-170">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="4e13c-171">Desteklenen değerler, [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)içinde bulunan üye adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="4e13c-171">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="4e13c-172">Note: yıllık faturalandırma özelliği henüz genel kullanıma sunulmamıştır.</span><span class="sxs-lookup"><span data-stu-id="4e13c-172">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="4e13c-173">Yıllık faturalandırmaya yönelik destek yakında kullanıma sunulacak.</span><span class="sxs-lookup"><span data-stu-id="4e13c-173">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="4e13c-174">LineItems</span><span class="sxs-lookup"><span data-stu-id="4e13c-174">lineItems</span></span> | <span data-ttu-id="4e13c-175">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="4e13c-175">array of objects</span></span> | <span data-ttu-id="4e13c-176">Yes</span><span class="sxs-lookup"><span data-stu-id="4e13c-176">Yes</span></span> | <span data-ttu-id="4e13c-177">[**Orderlineıtem**](#orderlineitem) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="4e13c-177">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="4e13c-178">creationDate</span><span class="sxs-lookup"><span data-stu-id="4e13c-178">creationDate</span></span> | <span data-ttu-id="4e13c-179">dize</span><span class="sxs-lookup"><span data-stu-id="4e13c-179">string</span></span> | <span data-ttu-id="4e13c-180">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-180">No</span></span> | <span data-ttu-id="4e13c-181">Siparişin oluşturulduğu tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="4e13c-181">The date the order was created, in date-time format.</span></span> <span data-ttu-id="4e13c-182">Siparişin başarıyla oluşturulmasından sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-182">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="4e13c-183">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="4e13c-183">attributes</span></span> | <span data-ttu-id="4e13c-184">object</span><span class="sxs-lookup"><span data-stu-id="4e13c-184">object</span></span> | <span data-ttu-id="4e13c-185">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-185">No</span></span> | <span data-ttu-id="4e13c-186">"ObjectType": "Order" içerir.</span><span class="sxs-lookup"><span data-stu-id="4e13c-186">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="4e13c-187">Orderlineıtem</span><span class="sxs-lookup"><span data-stu-id="4e13c-187">OrderLineItem</span></span>

<span data-ttu-id="4e13c-188">Bu tablo, istek gövdesinde **Orderlineıtem** özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4e13c-188">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="4e13c-189">Ad</span><span class="sxs-lookup"><span data-stu-id="4e13c-189">Name</span></span> | <span data-ttu-id="4e13c-190">Tür</span><span class="sxs-lookup"><span data-stu-id="4e13c-190">Type</span></span> | <span data-ttu-id="4e13c-191">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e13c-191">Required</span></span> | <span data-ttu-id="4e13c-192">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e13c-192">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="4e13c-193">Lineıtemnumber</span><span class="sxs-lookup"><span data-stu-id="4e13c-193">lineItemNumber</span></span> | <span data-ttu-id="4e13c-194">int</span><span class="sxs-lookup"><span data-stu-id="4e13c-194">int</span></span> | <span data-ttu-id="4e13c-195">Yes</span><span class="sxs-lookup"><span data-stu-id="4e13c-195">Yes</span></span> | <span data-ttu-id="4e13c-196">Koleksiyondaki her bir satır öğesi, 0 ' dan say-1 ' e kadar sayarak benzersiz bir satır numarası alır.</span><span class="sxs-lookup"><span data-stu-id="4e13c-196">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="4e13c-197">OfferId</span><span class="sxs-lookup"><span data-stu-id="4e13c-197">offerId</span></span> | <span data-ttu-id="4e13c-198">string</span><span class="sxs-lookup"><span data-stu-id="4e13c-198">string</span></span> | <span data-ttu-id="4e13c-199">Yes</span><span class="sxs-lookup"><span data-stu-id="4e13c-199">Yes</span></span> | <span data-ttu-id="4e13c-200">Teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-200">The offer identifier.</span></span> |
| <span data-ttu-id="4e13c-201">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4e13c-201">subscriptionId</span></span> | <span data-ttu-id="4e13c-202">dize</span><span class="sxs-lookup"><span data-stu-id="4e13c-202">string</span></span> | <span data-ttu-id="4e13c-203">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-203">No</span></span> | <span data-ttu-id="4e13c-204">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-204">The subscription identifier.</span></span> |
| <span data-ttu-id="4e13c-205">Parentsubscriptionıd</span><span class="sxs-lookup"><span data-stu-id="4e13c-205">parentSubscriptionId</span></span> | <span data-ttu-id="4e13c-206">dize</span><span class="sxs-lookup"><span data-stu-id="4e13c-206">string</span></span> | <span data-ttu-id="4e13c-207">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-207">No</span></span> | <span data-ttu-id="4e13c-208">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-208">Optional.</span></span> <span data-ttu-id="4e13c-209">Bir eklenti teklifinde üst aboneliğin KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="4e13c-209">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="4e13c-210">Yalnızca düzeltme eki için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4e13c-210">Applies to PATCH only.</span></span> |
| <span data-ttu-id="4e13c-211">friendlyName</span><span class="sxs-lookup"><span data-stu-id="4e13c-211">friendlyName</span></span> | <span data-ttu-id="4e13c-212">dize</span><span class="sxs-lookup"><span data-stu-id="4e13c-212">string</span></span> | <span data-ttu-id="4e13c-213">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-213">No</span></span> | <span data-ttu-id="4e13c-214">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-214">Optional.</span></span> <span data-ttu-id="4e13c-215">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-215">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="4e13c-216">miktar</span><span class="sxs-lookup"><span data-stu-id="4e13c-216">quantity</span></span> | <span data-ttu-id="4e13c-217">int</span><span class="sxs-lookup"><span data-stu-id="4e13c-217">int</span></span> | <span data-ttu-id="4e13c-218">Yes</span><span class="sxs-lookup"><span data-stu-id="4e13c-218">Yes</span></span> | <span data-ttu-id="4e13c-219">Lisans tabanlı abonelik için lisans sayısı.</span><span class="sxs-lookup"><span data-stu-id="4e13c-219">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="4e13c-220">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="4e13c-220">partnerIdOnRecord</span></span> | <span data-ttu-id="4e13c-221">dize</span><span class="sxs-lookup"><span data-stu-id="4e13c-221">string</span></span> | <span data-ttu-id="4e13c-222">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-222">No</span></span> | <span data-ttu-id="4e13c-223">Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir).</span><span class="sxs-lookup"><span data-stu-id="4e13c-223">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="4e13c-224">Bu, teşvikleri için doğru hesaplamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4e13c-224">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="4e13c-225">**Satıcı MPN KIMLIĞI sağlama hatası, siparişin başarısız olmasına neden olmaz. Ancak, satıcı kaydedilmez ve bir sonuç olarak hesaplamalar satışı içermez.**</span><span class="sxs-lookup"><span data-stu-id="4e13c-225">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="4e13c-226">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="4e13c-226">attributes</span></span> | <span data-ttu-id="4e13c-227">object</span><span class="sxs-lookup"><span data-stu-id="4e13c-227">object</span></span> | <span data-ttu-id="4e13c-228">No</span><span class="sxs-lookup"><span data-stu-id="4e13c-228">No</span></span> | <span data-ttu-id="4e13c-229">"ObjectType": "Orderlineıtem" içerir.</span><span class="sxs-lookup"><span data-stu-id="4e13c-229">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="4e13c-230">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4e13c-230">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

## <a name="rest-response"></a><span data-ttu-id="4e13c-231">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4e13c-231">REST response</span></span>

<span data-ttu-id="4e13c-232">Başarılı olursa, yanıt gövdesi doldurulmuş [sipariş](order-resources.md) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="4e13c-232">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4e13c-233">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4e13c-233">Response success and error codes</span></span>

<span data-ttu-id="4e13c-234">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4e13c-234">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4e13c-235">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e13c-235">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4e13c-236">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4e13c-236">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4e13c-237">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4e13c-237">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
