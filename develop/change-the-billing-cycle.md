---
title: Fatura döngüsünü değiştirme
description: Iş Ortağı Merkezi API 'Lerini kullanarak aylık veya yıllık faturalandırma için bir müşteri aboneliğini güncelleştirme hakkında bilgi edinin. Bunu Iş Ortağı Merkezi panosundan de yapabilirsiniz.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770090"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="44835-104">Müşteri aboneliği fatura döngüsünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="44835-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="44835-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="44835-105">**Applies to:**</span></span>

- <span data-ttu-id="44835-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="44835-106">Partner Center</span></span>
- <span data-ttu-id="44835-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="44835-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="44835-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="44835-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="44835-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="44835-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="44835-110">Bir [siparişi](order-resources.md) aylık faturalandırmaya veya yıllık faturalandırmaya aylık faturalandırma olarak güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="44835-110">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="44835-111">Iş Ortağı Merkezi panosunda, bu işlem bir müşterinin abonelik ayrıntıları sayfasına gidilerek gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="44835-111">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="44835-112">Bu işlem tamamlandıktan sonra, abonelik için geçerli faturalandırma döngüsünü tanımlama ve gönderme yeteneğine sahip bir seçenek görürsünüz.</span><span class="sxs-lookup"><span data-stu-id="44835-112">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="44835-113">Bu makalenin **kapsam dışı** :</span><span class="sxs-lookup"><span data-stu-id="44835-113">**Out of scope** for this article:</span></span>

- <span data-ttu-id="44835-114">Deneme için faturalandırma döngüsünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="44835-114">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="44835-115">Yıllık olmayan dönem teklifleri (aylık, 6 yıl) & Azure abonelikleri için fatura döngülerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="44835-115">Changing the billing cycles for any non-annual term offers (monthly, 6-year) & Azure subscriptions</span></span>
- <span data-ttu-id="44835-116">Etkin olmayan abonelikler için faturalandırma döngülerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="44835-116">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="44835-117">Microsoft çevrimiçi hizmetler lisans tabanlı abonelikler için faturalandırma döngülerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="44835-117">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="44835-118">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="44835-118">Prerequisites</span></span>

- <span data-ttu-id="44835-119">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="44835-119">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="44835-120">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="44835-120">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="44835-121">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="44835-121">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="44835-122">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="44835-122">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="44835-123">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="44835-123">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="44835-124">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="44835-124">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="44835-125">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="44835-125">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="44835-126">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="44835-126">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="44835-127">Bir sipariş KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="44835-127">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="44835-128">C\#</span><span class="sxs-lookup"><span data-stu-id="44835-128">C\#</span></span>

<span data-ttu-id="44835-129">Faturalandırma döngüsünün sıklığını değiştirmek için [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) özelliğini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="44835-129">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a><span data-ttu-id="44835-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="44835-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="44835-131">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="44835-131">Request syntax</span></span>

| <span data-ttu-id="44835-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="44835-132">Method</span></span>    | <span data-ttu-id="44835-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="44835-133">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="44835-134">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="44835-134">**PATCH**</span></span> | <span data-ttu-id="44835-135">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="44835-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="44835-136">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="44835-136">URI parameter</span></span>

<span data-ttu-id="44835-137">Bu tabloda, abonelik miktarını değiştirmek için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="44835-137">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="44835-138">Ad</span><span class="sxs-lookup"><span data-stu-id="44835-138">Name</span></span>                   | <span data-ttu-id="44835-139">Tür</span><span class="sxs-lookup"><span data-stu-id="44835-139">Type</span></span> | <span data-ttu-id="44835-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44835-140">Required</span></span> | <span data-ttu-id="44835-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44835-141">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="44835-142">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="44835-142">**customer-tenant-id**</span></span> | <span data-ttu-id="44835-143">GUID</span><span class="sxs-lookup"><span data-stu-id="44835-143">GUID</span></span> |    <span data-ttu-id="44835-144">Y</span><span class="sxs-lookup"><span data-stu-id="44835-144">Y</span></span>     | <span data-ttu-id="44835-145">Müşteriyi tanımlayan bir GUID biçimli **Müşteri Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="44835-145">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="44835-146">**sıra kimliği**</span><span class="sxs-lookup"><span data-stu-id="44835-146">**order-id**</span></span>           | <span data-ttu-id="44835-147">GUID</span><span class="sxs-lookup"><span data-stu-id="44835-147">GUID</span></span> |    <span data-ttu-id="44835-148">Y</span><span class="sxs-lookup"><span data-stu-id="44835-148">Y</span></span>     | <span data-ttu-id="44835-149">Sıra tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="44835-149">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="44835-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="44835-150">Request headers</span></span>

<span data-ttu-id="44835-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="44835-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="44835-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="44835-152">Request body</span></span>

<span data-ttu-id="44835-153">Aşağıdaki tablolarda, istek gövdesindeki özellikler açıklanır.</span><span class="sxs-lookup"><span data-stu-id="44835-153">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="44835-154">Sipariş</span><span class="sxs-lookup"><span data-stu-id="44835-154">Order</span></span>

| <span data-ttu-id="44835-155">Özellik</span><span class="sxs-lookup"><span data-stu-id="44835-155">Property</span></span>           | <span data-ttu-id="44835-156">Tür</span><span class="sxs-lookup"><span data-stu-id="44835-156">Type</span></span>             | <span data-ttu-id="44835-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44835-157">Required</span></span> | <span data-ttu-id="44835-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44835-158">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="44835-159">Id</span><span class="sxs-lookup"><span data-stu-id="44835-159">Id</span></span>                 | <span data-ttu-id="44835-160">string</span><span class="sxs-lookup"><span data-stu-id="44835-160">string</span></span>           |    <span data-ttu-id="44835-161">N</span><span class="sxs-lookup"><span data-stu-id="44835-161">N</span></span>     | <span data-ttu-id="44835-162">Sıranın başarıyla oluşturulması sırasında sağlanan bir sipariş tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="44835-162">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="44835-163">Referencecustomerıd</span><span class="sxs-lookup"><span data-stu-id="44835-163">ReferenceCustomerId</span></span> | <span data-ttu-id="44835-164">string</span><span class="sxs-lookup"><span data-stu-id="44835-164">string</span></span>           |    <span data-ttu-id="44835-165">Y</span><span class="sxs-lookup"><span data-stu-id="44835-165">Y</span></span>     | <span data-ttu-id="44835-166">Müşteri tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="44835-166">The customer identifier</span></span>                                                    |
| <span data-ttu-id="44835-167">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="44835-167">BillingCycle</span></span>       | <span data-ttu-id="44835-168">string</span><span class="sxs-lookup"><span data-stu-id="44835-168">string</span></span>           |    <span data-ttu-id="44835-169">Y</span><span class="sxs-lookup"><span data-stu-id="44835-169">Y</span></span>     | <span data-ttu-id="44835-170">Ortağın bu sipariş için faturalandırılabileceği sıklığı belirtir.</span><span class="sxs-lookup"><span data-stu-id="44835-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="44835-171">Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="44835-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="44835-172">LineItems</span><span class="sxs-lookup"><span data-stu-id="44835-172">LineItems</span></span>          | <span data-ttu-id="44835-173">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="44835-173">array of objects</span></span> |    <span data-ttu-id="44835-174">Y</span><span class="sxs-lookup"><span data-stu-id="44835-174">Y</span></span>     | <span data-ttu-id="44835-175">[Orderlineıtem](#orderlineitem) kaynakları dizisi</span><span class="sxs-lookup"><span data-stu-id="44835-175">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="44835-176">CreationDate</span><span class="sxs-lookup"><span data-stu-id="44835-176">CreationDate</span></span>       | <span data-ttu-id="44835-177">datetime</span><span class="sxs-lookup"><span data-stu-id="44835-177">datetime</span></span>         |    <span data-ttu-id="44835-178">N</span><span class="sxs-lookup"><span data-stu-id="44835-178">N</span></span>     | <span data-ttu-id="44835-179">Siparişin oluşturulduğu tarih ve tarih-saat biçiminde</span><span class="sxs-lookup"><span data-stu-id="44835-179">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="44835-180">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="44835-180">Attributes</span></span>         | <span data-ttu-id="44835-181">Nesne</span><span class="sxs-lookup"><span data-stu-id="44835-181">Object</span></span>           |    <span data-ttu-id="44835-182">N</span><span class="sxs-lookup"><span data-stu-id="44835-182">N</span></span>     | <span data-ttu-id="44835-183">"ObjectType" içerir: "Orderlineıtem"</span><span class="sxs-lookup"><span data-stu-id="44835-183">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="44835-184">Orderlineıtem</span><span class="sxs-lookup"><span data-stu-id="44835-184">OrderLineItem</span></span>

| <span data-ttu-id="44835-185">Özellik</span><span class="sxs-lookup"><span data-stu-id="44835-185">Property</span></span>             | <span data-ttu-id="44835-186">Tür</span><span class="sxs-lookup"><span data-stu-id="44835-186">Type</span></span>   | <span data-ttu-id="44835-187">Gerekli</span><span class="sxs-lookup"><span data-stu-id="44835-187">Required</span></span> | <span data-ttu-id="44835-188">Açıklama</span><span class="sxs-lookup"><span data-stu-id="44835-188">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="44835-189">Lineıtemnumber</span><span class="sxs-lookup"><span data-stu-id="44835-189">LineItemNumber</span></span>       | <span data-ttu-id="44835-190">sayı</span><span class="sxs-lookup"><span data-stu-id="44835-190">number</span></span> |    <span data-ttu-id="44835-191">Y</span><span class="sxs-lookup"><span data-stu-id="44835-191">Y</span></span>     | <span data-ttu-id="44835-192">Satır öğe numarası, 0 ile başlar</span><span class="sxs-lookup"><span data-stu-id="44835-192">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="44835-193">OfferId</span><span class="sxs-lookup"><span data-stu-id="44835-193">OfferId</span></span>              | <span data-ttu-id="44835-194">string</span><span class="sxs-lookup"><span data-stu-id="44835-194">string</span></span> |    <span data-ttu-id="44835-195">Y</span><span class="sxs-lookup"><span data-stu-id="44835-195">Y</span></span>     | <span data-ttu-id="44835-196">Teklifin KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="44835-196">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="44835-197">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="44835-197">SubscriptionId</span></span>       | <span data-ttu-id="44835-198">string</span><span class="sxs-lookup"><span data-stu-id="44835-198">string</span></span> |    <span data-ttu-id="44835-199">Y</span><span class="sxs-lookup"><span data-stu-id="44835-199">Y</span></span>     | <span data-ttu-id="44835-200">Aboneliğin KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="44835-200">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="44835-201">FriendlyName</span><span class="sxs-lookup"><span data-stu-id="44835-201">FriendlyName</span></span>         | <span data-ttu-id="44835-202">string</span><span class="sxs-lookup"><span data-stu-id="44835-202">string</span></span> |    <span data-ttu-id="44835-203">N</span><span class="sxs-lookup"><span data-stu-id="44835-203">N</span></span>     | <span data-ttu-id="44835-204">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı</span><span class="sxs-lookup"><span data-stu-id="44835-204">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="44835-205">Miktar</span><span class="sxs-lookup"><span data-stu-id="44835-205">Quantity</span></span>             | <span data-ttu-id="44835-206">sayı</span><span class="sxs-lookup"><span data-stu-id="44835-206">number</span></span> |    <span data-ttu-id="44835-207">Y</span><span class="sxs-lookup"><span data-stu-id="44835-207">Y</span></span>     | <span data-ttu-id="44835-208">Lisans veya örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="44835-208">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="44835-209">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="44835-209">PartnerIdOnRecord</span></span>    | <span data-ttu-id="44835-210">string</span><span class="sxs-lookup"><span data-stu-id="44835-210">string</span></span> |    <span data-ttu-id="44835-211">N</span><span class="sxs-lookup"><span data-stu-id="44835-211">N</span></span>     | <span data-ttu-id="44835-212">Kayıt ortağının MPN KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="44835-212">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="44835-213">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="44835-213">Attributes</span></span>           | <span data-ttu-id="44835-214">Nesne</span><span class="sxs-lookup"><span data-stu-id="44835-214">Object</span></span> |    <span data-ttu-id="44835-215">N</span><span class="sxs-lookup"><span data-stu-id="44835-215">N</span></span>     | <span data-ttu-id="44835-216">"ObjectType" içerir: "Orderlineıtem"</span><span class="sxs-lookup"><span data-stu-id="44835-216">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="44835-217">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="44835-217">Request example</span></span>

<span data-ttu-id="44835-218">Yıllık faturalandırmaya Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="44835-218">Update to annual billing</span></span>

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
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
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

## <a name="rest-response"></a><span data-ttu-id="44835-219">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="44835-219">REST response</span></span>

<span data-ttu-id="44835-220">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş abonelik sırasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="44835-220">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="44835-221">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="44835-221">Response success and error codes</span></span>

<span data-ttu-id="44835-222">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="44835-222">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="44835-223">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="44835-223">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="44835-224">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="44835-224">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="44835-225">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="44835-225">Response example</span></span>

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
    "billingCycle": "Annual",
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
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
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