---
title: Dolaylı kurumsal bayi için müşteri siparişi oluşturma
description: Dolaylı kurumsal bayi İş Ortağı Merkezi sipariş oluşturmak için api'leri kullanmayı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973561"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a><span data-ttu-id="4d206-104">Dolaylı satıcı müşterisi için bir sipariş oluşturma</span><span class="sxs-lookup"><span data-stu-id="4d206-104">Create an order for a customer of an indirect reseller</span></span>

<span data-ttu-id="4d206-105">Dolaylı kurumsal bayi müşterisi için sipariş oluşturma.</span><span class="sxs-lookup"><span data-stu-id="4d206-105">How to create an order for a customer of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d206-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4d206-106">Prerequisites</span></span>

- <span data-ttu-id="4d206-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4d206-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4d206-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="4d206-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="4d206-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4d206-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4d206-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4d206-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4d206-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="4d206-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4d206-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="4d206-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4d206-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="4d206-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4d206-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="4d206-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4d206-115">Satın alınan öğenin teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4d206-115">The offer identifier of the item to purchase.</span></span>

- <span data-ttu-id="4d206-116">Dolaylı kurumsal bayinin kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4d206-116">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="4d206-117">C\#</span><span class="sxs-lookup"><span data-stu-id="4d206-117">C\#</span></span>

<span data-ttu-id="4d206-118">Dolaylı kurumsal bayinin müşterisi için sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="4d206-118">To create an order for a customer of an indirect reseller:</span></span>

1. <span data-ttu-id="4d206-119">Oturum açmış iş ortağıyla ilişkisi olan dolaylı kurumsal bayilerin koleksiyonunu alın.</span><span class="sxs-lookup"><span data-stu-id="4d206-119">Get a collection of the indirect resellers that have a relationship with the signed-in partner.</span></span>

2. <span data-ttu-id="4d206-120">Koleksiyonda dolaylı kurumsal bayi kimliğiyle eşleşen öğeye bir yerel değişken alın.</span><span class="sxs-lookup"><span data-stu-id="4d206-120">Get a local variable to the item in the collection that matches the indirect reseller ID.</span></span> <span data-ttu-id="4d206-121">Bu adım, siparişi 7/2012'ye kadar olan tüm bayilerin [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) özelliğine erişmeye yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="4d206-121">This step helps you access the reseller's [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) property when you create the order.</span></span>

3. <span data-ttu-id="4d206-122">Bir Order [**nesnesinin**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) örneğini oluşturma ve müşteriyi kaydetmek için [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) özelliğini müşteri tanımlayıcısı olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="4d206-122">Instantiate an [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) object and set the [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) property to the customer identifier in order to record the customer.</span></span>

4. <span data-ttu-id="4d206-123">[**OrderLineItem nesnelerinin**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) listesini oluşturun ve listeyi siparişin [**LineItems özelliğine**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) attayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4d206-123">Create a list of [**OrderLineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) objects, and assign the list to the order's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) property.</span></span> <span data-ttu-id="4d206-124">Her sipariş satırı öğesi, bir teklif için satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="4d206-124">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="4d206-125">Her satır öğesinde [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) özelliğini dolaylı kurumsal bayinin MPN kimliğiyle doldurmak için emin olun.</span><span class="sxs-lookup"><span data-stu-id="4d206-125">Be sure to populate the [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) property in each line item with the MPN ID of the indirect reseller.</span></span> <span data-ttu-id="4d206-126">En az bir sipariş satırı öğeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="4d206-126">You must have at least one order line item.</span></span>

5. <span data-ttu-id="4d206-127">Müşteriyi tanımlamak için müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak işlemleri sıralamak için bir arabirim alın ve [**ardından Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğinden arabirimi alın.</span><span class="sxs-lookup"><span data-stu-id="4d206-127">Obtain an interface to order operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

6. <span data-ttu-id="4d206-128">Siparişi oluşturmak [**için Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) [**veya CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="4d206-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method to create the order.</span></span>

### <a name="c-example"></a><span data-ttu-id="4d206-129">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="4d206-129">C\# example</span></span>

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

<span data-ttu-id="4d206-130">**Örnek:** [Konsol test uygulaması](console-test-app.md)**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** PlaceOrderForCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="4d206-130">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: PlaceOrderForCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4d206-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4d206-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4d206-132">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="4d206-132">Request syntax</span></span>

| <span data-ttu-id="4d206-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4d206-133">Method</span></span>   | <span data-ttu-id="4d206-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4d206-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="4d206-135">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="4d206-135">**POST**</span></span> | <span data-ttu-id="4d206-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4d206-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4d206-137">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="4d206-137">URI parameters</span></span>

<span data-ttu-id="4d206-138">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d206-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="4d206-139">Ad</span><span class="sxs-lookup"><span data-stu-id="4d206-139">Name</span></span>        | <span data-ttu-id="4d206-140">Tür</span><span class="sxs-lookup"><span data-stu-id="4d206-140">Type</span></span>   | <span data-ttu-id="4d206-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4d206-141">Required</span></span> | <span data-ttu-id="4d206-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4d206-142">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="4d206-143">customer-id</span><span class="sxs-lookup"><span data-stu-id="4d206-143">customer-id</span></span> | <span data-ttu-id="4d206-144">string</span><span class="sxs-lookup"><span data-stu-id="4d206-144">string</span></span> | <span data-ttu-id="4d206-145">Yes</span><span class="sxs-lookup"><span data-stu-id="4d206-145">Yes</span></span>      | <span data-ttu-id="4d206-146">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="4d206-146">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4d206-147">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4d206-147">Request headers</span></span>

<span data-ttu-id="4d206-148">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4d206-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4d206-149">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4d206-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="4d206-150">Sipariş</span><span class="sxs-lookup"><span data-stu-id="4d206-150">Order</span></span>

<span data-ttu-id="4d206-151">Bu tablo, istek **gövdesinin** Sipariş özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4d206-151">This table describes the **Order** properties in the request body.</span></span>

| <span data-ttu-id="4d206-152">Ad</span><span class="sxs-lookup"><span data-stu-id="4d206-152">Name</span></span> | <span data-ttu-id="4d206-153">Tür</span><span class="sxs-lookup"><span data-stu-id="4d206-153">Type</span></span> | <span data-ttu-id="4d206-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4d206-154">Required</span></span> | <span data-ttu-id="4d206-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4d206-155">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="4d206-156">kimlik</span><span class="sxs-lookup"><span data-stu-id="4d206-156">id</span></span> | <span data-ttu-id="4d206-157">dize</span><span class="sxs-lookup"><span data-stu-id="4d206-157">string</span></span> | <span data-ttu-id="4d206-158">No</span><span class="sxs-lookup"><span data-stu-id="4d206-158">No</span></span> | <span data-ttu-id="4d206-159">Siparişin başarıyla oluşturulmasının ardından sağlanan bir sipariş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4d206-159">An order identifier that is supplied upon successful creation of the order.</span></span> |
| <span data-ttu-id="4d206-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="4d206-160">referenceCustomerId</span></span> | <span data-ttu-id="4d206-161">string</span><span class="sxs-lookup"><span data-stu-id="4d206-161">string</span></span> | <span data-ttu-id="4d206-162">Yes</span><span class="sxs-lookup"><span data-stu-id="4d206-162">Yes</span></span> | <span data-ttu-id="4d206-163">Müşteri tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4d206-163">The customer identifier.</span></span> |
| <span data-ttu-id="4d206-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="4d206-164">billingCycle</span></span> | <span data-ttu-id="4d206-165">dize</span><span class="sxs-lookup"><span data-stu-id="4d206-165">string</span></span> | <span data-ttu-id="4d206-166">No</span><span class="sxs-lookup"><span data-stu-id="4d206-166">No</span></span> | <span data-ttu-id="4d206-167">İş ortağının bu sipariş için faturalandırılama sıklığı.</span><span class="sxs-lookup"><span data-stu-id="4d206-167">The frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="4d206-168">Varsayılan değer &quot; Aylık'tır &quot; ve siparişin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4d206-168">The default is &quot;Monthly&quot; and is applied upon successful creation of the order.</span></span> <span data-ttu-id="4d206-169">Desteklenen değerler, [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)içinde bulunan üye adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="4d206-169">Supported values are the member names found in [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype).</span></span> <span data-ttu-id="4d206-170">Not: Yıllık faturalama özelliği henüz genel kullanıma açık değildir.</span><span class="sxs-lookup"><span data-stu-id="4d206-170">Note: the annual billing feature isn't yet generally available.</span></span> <span data-ttu-id="4d206-171">Yıllık faturalama desteği yakında gelecektir.</span><span class="sxs-lookup"><span data-stu-id="4d206-171">Support for annual billing is coming soon.</span></span> |
| <span data-ttu-id="4d206-172">lineItems</span><span class="sxs-lookup"><span data-stu-id="4d206-172">lineItems</span></span> | <span data-ttu-id="4d206-173">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="4d206-173">array of objects</span></span> | <span data-ttu-id="4d206-174">Yes</span><span class="sxs-lookup"><span data-stu-id="4d206-174">Yes</span></span> | <span data-ttu-id="4d206-175">[**OrderLineItem kaynaklarının dizisi.**](#orderlineitem)</span><span class="sxs-lookup"><span data-stu-id="4d206-175">An array of [**OrderLineItem**](#orderlineitem) resources.</span></span> |
| <span data-ttu-id="4d206-176">Creationdate</span><span class="sxs-lookup"><span data-stu-id="4d206-176">creationDate</span></span> | <span data-ttu-id="4d206-177">dize</span><span class="sxs-lookup"><span data-stu-id="4d206-177">string</span></span> | <span data-ttu-id="4d206-178">No</span><span class="sxs-lookup"><span data-stu-id="4d206-178">No</span></span> | <span data-ttu-id="4d206-179">Siparişin tarih-saat biçiminde oluşturulma tarihi.</span><span class="sxs-lookup"><span data-stu-id="4d206-179">The date the order was created, in date-time format.</span></span> <span data-ttu-id="4d206-180">Siparişin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="4d206-180">Applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="4d206-181">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="4d206-181">attributes</span></span> | <span data-ttu-id="4d206-182">object</span><span class="sxs-lookup"><span data-stu-id="4d206-182">object</span></span> | <span data-ttu-id="4d206-183">Hayır</span><span class="sxs-lookup"><span data-stu-id="4d206-183">No</span></span> | <span data-ttu-id="4d206-184">"ObjectType": "Order" ifadesini içerir.</span><span class="sxs-lookup"><span data-stu-id="4d206-184">Contains "ObjectType": "Order".</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="4d206-185">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="4d206-185">OrderLineItem</span></span>

<span data-ttu-id="4d206-186">Bu tablo, istek **gövdesinin OrderLineItem** özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4d206-186">This table describes the **OrderLineItem** properties in the request body.</span></span>

| <span data-ttu-id="4d206-187">Ad</span><span class="sxs-lookup"><span data-stu-id="4d206-187">Name</span></span> | <span data-ttu-id="4d206-188">Tür</span><span class="sxs-lookup"><span data-stu-id="4d206-188">Type</span></span> | <span data-ttu-id="4d206-189">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4d206-189">Required</span></span> | <span data-ttu-id="4d206-190">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4d206-190">Description</span></span> |
| ---- | ---- | -------- | ----------- |
| <span data-ttu-id="4d206-191">lineItemNumber</span><span class="sxs-lookup"><span data-stu-id="4d206-191">lineItemNumber</span></span> | <span data-ttu-id="4d206-192">int</span><span class="sxs-lookup"><span data-stu-id="4d206-192">int</span></span> | <span data-ttu-id="4d206-193">Yes</span><span class="sxs-lookup"><span data-stu-id="4d206-193">Yes</span></span> | <span data-ttu-id="4d206-194">Koleksiyonda yer alan her satır öğesi benzersiz bir satır numarası alır ve 0 ile 1 arasında bir sayıya kadar sayar.</span><span class="sxs-lookup"><span data-stu-id="4d206-194">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span> |
| <span data-ttu-id="4d206-195">offerId</span><span class="sxs-lookup"><span data-stu-id="4d206-195">offerId</span></span> | <span data-ttu-id="4d206-196">string</span><span class="sxs-lookup"><span data-stu-id="4d206-196">string</span></span> | <span data-ttu-id="4d206-197">Yes</span><span class="sxs-lookup"><span data-stu-id="4d206-197">Yes</span></span> | <span data-ttu-id="4d206-198">Teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4d206-198">The offer identifier.</span></span> |
| <span data-ttu-id="4d206-199">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="4d206-199">subscriptionId</span></span> | <span data-ttu-id="4d206-200">dize</span><span class="sxs-lookup"><span data-stu-id="4d206-200">string</span></span> | <span data-ttu-id="4d206-201">No</span><span class="sxs-lookup"><span data-stu-id="4d206-201">No</span></span> | <span data-ttu-id="4d206-202">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4d206-202">The subscription identifier.</span></span> |
| <span data-ttu-id="4d206-203">Parentsubscriptionıd</span><span class="sxs-lookup"><span data-stu-id="4d206-203">parentSubscriptionId</span></span> | <span data-ttu-id="4d206-204">dize</span><span class="sxs-lookup"><span data-stu-id="4d206-204">string</span></span> | <span data-ttu-id="4d206-205">No</span><span class="sxs-lookup"><span data-stu-id="4d206-205">No</span></span> | <span data-ttu-id="4d206-206">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="4d206-206">Optional.</span></span> <span data-ttu-id="4d206-207">Bir eklenti teklifinde üst aboneliğin KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="4d206-207">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="4d206-208">Yalnızca düzeltme eki için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="4d206-208">Applies to PATCH only.</span></span> |
| <span data-ttu-id="4d206-209">friendlyName</span><span class="sxs-lookup"><span data-stu-id="4d206-209">friendlyName</span></span> | <span data-ttu-id="4d206-210">dize</span><span class="sxs-lookup"><span data-stu-id="4d206-210">string</span></span> | <span data-ttu-id="4d206-211">No</span><span class="sxs-lookup"><span data-stu-id="4d206-211">No</span></span> | <span data-ttu-id="4d206-212">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="4d206-212">Optional.</span></span> <span data-ttu-id="4d206-213">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="4d206-213">The friendly name for the subscription defined by the partner to help disambiguate.</span></span> |
| <span data-ttu-id="4d206-214">miktar</span><span class="sxs-lookup"><span data-stu-id="4d206-214">quantity</span></span> | <span data-ttu-id="4d206-215">int</span><span class="sxs-lookup"><span data-stu-id="4d206-215">int</span></span> | <span data-ttu-id="4d206-216">Yes</span><span class="sxs-lookup"><span data-stu-id="4d206-216">Yes</span></span> | <span data-ttu-id="4d206-217">Lisans tabanlı abonelik için lisans sayısı.</span><span class="sxs-lookup"><span data-stu-id="4d206-217">The number of licenses for a license-based subscription.</span></span> |
| <span data-ttu-id="4d206-218">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="4d206-218">partnerIdOnRecord</span></span> | <span data-ttu-id="4d206-219">dize</span><span class="sxs-lookup"><span data-stu-id="4d206-219">string</span></span> | <span data-ttu-id="4d206-220">No</span><span class="sxs-lookup"><span data-stu-id="4d206-220">No</span></span> | <span data-ttu-id="4d206-221">Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir).</span><span class="sxs-lookup"><span data-stu-id="4d206-221">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="4d206-222">Bu, teşvikleri için doğru hesaplamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="4d206-222">This ensures proper accounting for incentives.</span></span> <span data-ttu-id="4d206-223">**Satıcı MPN KIMLIĞI sağlama hatası, siparişin başarısız olmasına neden olmaz. Ancak, satıcı kaydedilmez ve bir sonuç olarak hesaplamalar satışı içermez.**</span><span class="sxs-lookup"><span data-stu-id="4d206-223">**Failure to provide the reseller MPN ID does not cause the order to fail. However, the reseller isn't recorded and as a consequence incentive calculations may not include the sale.**</span></span> |
| <span data-ttu-id="4d206-224">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="4d206-224">attributes</span></span> | <span data-ttu-id="4d206-225">object</span><span class="sxs-lookup"><span data-stu-id="4d206-225">object</span></span> | <span data-ttu-id="4d206-226">Hayır</span><span class="sxs-lookup"><span data-stu-id="4d206-226">No</span></span> | <span data-ttu-id="4d206-227">"ObjectType": "Orderlineıtem" içerir.</span><span class="sxs-lookup"><span data-stu-id="4d206-227">Contains "ObjectType":"OrderLineItem".</span></span> |

### <a name="request-example"></a><span data-ttu-id="4d206-228">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4d206-228">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4d206-229">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4d206-229">REST response</span></span>

<span data-ttu-id="4d206-230">Başarılı olursa, yanıt gövdesi doldurulmuş [sipariş](order-resources.md) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="4d206-230">If successful, the response body contains the populated [Order](order-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4d206-231">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4d206-231">Response success and error codes</span></span>

<span data-ttu-id="4d206-232">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4d206-232">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4d206-233">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d206-233">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4d206-234">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4d206-234">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4d206-235">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4d206-235">Response example</span></span>

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
