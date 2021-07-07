---
title: Fatura döngüsünü değiştirme
description: Api'leri kullanarak müşteri aboneliğini aylık veya yıllık faturalamaya İş Ortağı Merkezi öğrenin. Bunu panodan da İş Ortağı Merkezi.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 435309229e2cb038c936028943f4c2cf27b032a7
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974123"
---
# <a name="change-a-customer-subscription-billing-cycle"></a><span data-ttu-id="4e735-104">Müşteri aboneliği faturalama döngüsünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="4e735-104">Change a customer subscription billing cycle</span></span>

<span data-ttu-id="4e735-105">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="4e735-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4e735-106">Bir Siparişi [aylık](order-resources.md) faturalamadan yıllık faturalamaya veya yıllık faturalamadan aylık faturalamaya doğru güncelleştirmeler.</span><span class="sxs-lookup"><span data-stu-id="4e735-106">Updates an [Order](order-resources.md) from monthly to annual billing or from annual to monthly billing.</span></span>

<span data-ttu-id="4e735-107">Bu İş Ortağı Merkezi, müşterinin abonelik ayrıntıları sayfasına giderek bu işlemi gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4e735-107">In the Partner Center dashboard, this operation can be performed by navigating to a customer's subscription details page.</span></span> <span data-ttu-id="4e735-108">Bu seçenek, abonelik için geçerli faturalama döngüsünü tanımlayarak değişiklik ve gönderme olanağına sahip olur.</span><span class="sxs-lookup"><span data-stu-id="4e735-108">Once there, you will see an option defining the current billing cycle for the subscription with the ability to change and submit it.</span></span>

<span data-ttu-id="4e735-109">**Bu makalenin** kapsamı dışında:</span><span class="sxs-lookup"><span data-stu-id="4e735-109">**Out of scope** for this article:</span></span>

- <span data-ttu-id="4e735-110">Denemeler için faturalama döngüsünü değiştirme</span><span class="sxs-lookup"><span data-stu-id="4e735-110">Changing the billing cycle for trials</span></span>
- <span data-ttu-id="4e735-111">Azure abonelikleri için yıllık olmayan dönem tekliflerinin (aylık, altı yıllık) faturalama & değiştirme</span><span class="sxs-lookup"><span data-stu-id="4e735-111">Changing the billing cycles for any non-annual term offers (monthly, six-year) & Azure subscriptions</span></span>
- <span data-ttu-id="4e735-112">Etkin olmayan abonelikler için faturalama döngülerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="4e735-112">Changing the billing cycles for inactive subscriptions</span></span>
- <span data-ttu-id="4e735-113">Microsoft çevrimiçi hizmetler tabanlı abonelikler için faturalama döngülerini değiştirme</span><span class="sxs-lookup"><span data-stu-id="4e735-113">Changing billing cycles for Microsoft online services license-based subscriptions</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e735-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4e735-114">Prerequisites</span></span>

- <span data-ttu-id="4e735-115">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="4e735-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4e735-116">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="4e735-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4e735-117">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4e735-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4e735-118">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="4e735-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4e735-119">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="4e735-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4e735-120">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="4e735-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4e735-121">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="4e735-121">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4e735-122">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="4e735-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4e735-123">Sipariş kimliği.</span><span class="sxs-lookup"><span data-stu-id="4e735-123">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="4e735-124">C\#</span><span class="sxs-lookup"><span data-stu-id="4e735-124">C\#</span></span>

<span data-ttu-id="4e735-125">Faturalama döngüsünün sıklığını değiştirmek için [**Order.BillingCycle özelliğini güncelleştirin.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)</span><span class="sxs-lookup"><span data-stu-id="4e735-125">To change the frequency of the billing cycle, update the [**Order.BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) property.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="4e735-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4e735-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4e735-127">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="4e735-127">Request syntax</span></span>

| <span data-ttu-id="4e735-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4e735-128">Method</span></span>    | <span data-ttu-id="4e735-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4e735-129">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4e735-130">**Yama**</span><span class="sxs-lookup"><span data-stu-id="4e735-130">**PATCH**</span></span> | <span data-ttu-id="4e735-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="4e735-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4e735-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="4e735-132">URI parameter</span></span>

<span data-ttu-id="4e735-133">Bu tabloda aboneliğin miktarını değiştirmek için gerekli sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="4e735-133">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="4e735-134">Ad</span><span class="sxs-lookup"><span data-stu-id="4e735-134">Name</span></span>                   | <span data-ttu-id="4e735-135">Tür</span><span class="sxs-lookup"><span data-stu-id="4e735-135">Type</span></span> | <span data-ttu-id="4e735-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e735-136">Required</span></span> | <span data-ttu-id="4e735-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e735-137">Description</span></span>                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| <span data-ttu-id="4e735-138">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="4e735-138">**customer-tenant-id**</span></span> | <span data-ttu-id="4e735-139">GUID</span><span class="sxs-lookup"><span data-stu-id="4e735-139">GUID</span></span> |    <span data-ttu-id="4e735-140">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-140">Y</span></span>     | <span data-ttu-id="4e735-141">Müşteriyi tanımlayan **GUID biçimlendirilmiş customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="4e735-141">A GUID formatted **customer-tenant-id** that identifies the customer</span></span> |
| <span data-ttu-id="4e735-142">**order-id**</span><span class="sxs-lookup"><span data-stu-id="4e735-142">**order-id**</span></span>           | <span data-ttu-id="4e735-143">GUID</span><span class="sxs-lookup"><span data-stu-id="4e735-143">GUID</span></span> |    <span data-ttu-id="4e735-144">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-144">Y</span></span>     | <span data-ttu-id="4e735-145">Sipariş tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="4e735-145">The order identifier</span></span>                                                 |

### <a name="request-headers"></a><span data-ttu-id="4e735-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4e735-146">Request headers</span></span>

<span data-ttu-id="4e735-147">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="4e735-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4e735-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4e735-148">Request body</span></span>

<span data-ttu-id="4e735-149">Aşağıdaki tablolar istek gövdesinin özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="4e735-149">The following tables describe the properties in the request body.</span></span>

### <a name="order"></a><span data-ttu-id="4e735-150">Sipariş</span><span class="sxs-lookup"><span data-stu-id="4e735-150">Order</span></span>

| <span data-ttu-id="4e735-151">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e735-151">Property</span></span>           | <span data-ttu-id="4e735-152">Tür</span><span class="sxs-lookup"><span data-stu-id="4e735-152">Type</span></span>             | <span data-ttu-id="4e735-153">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e735-153">Required</span></span> | <span data-ttu-id="4e735-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e735-154">Description</span></span>                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| <span data-ttu-id="4e735-155">Id</span><span class="sxs-lookup"><span data-stu-id="4e735-155">Id</span></span>                 | <span data-ttu-id="4e735-156">string</span><span class="sxs-lookup"><span data-stu-id="4e735-156">string</span></span>           |    <span data-ttu-id="4e735-157">N</span><span class="sxs-lookup"><span data-stu-id="4e735-157">N</span></span>     | <span data-ttu-id="4e735-158">Siparişin başarıyla oluşturulmasının ardından sağlanan sipariş tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="4e735-158">An order identifier that is supplied upon successful creation of the order</span></span> |
|<span data-ttu-id="4e735-159">ReferenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="4e735-159">ReferenceCustomerId</span></span> | <span data-ttu-id="4e735-160">string</span><span class="sxs-lookup"><span data-stu-id="4e735-160">string</span></span>           |    <span data-ttu-id="4e735-161">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-161">Y</span></span>     | <span data-ttu-id="4e735-162">Müşteri tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="4e735-162">The customer identifier</span></span>                                                    |
| <span data-ttu-id="4e735-163">BillingCycle</span><span class="sxs-lookup"><span data-stu-id="4e735-163">BillingCycle</span></span>       | <span data-ttu-id="4e735-164">string</span><span class="sxs-lookup"><span data-stu-id="4e735-164">string</span></span>           |    <span data-ttu-id="4e735-165">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-165">Y</span></span>     | <span data-ttu-id="4e735-166">İş ortağının bu sipariş için faturalandırılama sıklığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="4e735-166">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="4e735-167">Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="4e735-167">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> |
| <span data-ttu-id="4e735-168">LineItems</span><span class="sxs-lookup"><span data-stu-id="4e735-168">LineItems</span></span>          | <span data-ttu-id="4e735-169">nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="4e735-169">array of objects</span></span> |    <span data-ttu-id="4e735-170">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-170">Y</span></span>     | <span data-ttu-id="4e735-171">[OrderLineItem kaynakları](#orderlineitem) dizisi</span><span class="sxs-lookup"><span data-stu-id="4e735-171">An array of [OrderLineItem](#orderlineitem) resources</span></span>                      |
| <span data-ttu-id="4e735-172">Creationdate</span><span class="sxs-lookup"><span data-stu-id="4e735-172">CreationDate</span></span>       | <span data-ttu-id="4e735-173">datetime</span><span class="sxs-lookup"><span data-stu-id="4e735-173">datetime</span></span>         |    <span data-ttu-id="4e735-174">N</span><span class="sxs-lookup"><span data-stu-id="4e735-174">N</span></span>     | <span data-ttu-id="4e735-175">Siparişin tarih-saat biçiminde oluşturulma tarihi</span><span class="sxs-lookup"><span data-stu-id="4e735-175">The date the order was created, in date-time format</span></span>                        |
| <span data-ttu-id="4e735-176">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="4e735-176">Attributes</span></span>         | <span data-ttu-id="4e735-177">Nesne</span><span class="sxs-lookup"><span data-stu-id="4e735-177">Object</span></span>           |    <span data-ttu-id="4e735-178">N</span><span class="sxs-lookup"><span data-stu-id="4e735-178">N</span></span>     | <span data-ttu-id="4e735-179">"ObjectType": "OrderLineItem" içerir</span><span class="sxs-lookup"><span data-stu-id="4e735-179">Contains "ObjectType": "OrderLineItem"</span></span>                                     |

### <a name="orderlineitem"></a><span data-ttu-id="4e735-180">OrderLineItem</span><span class="sxs-lookup"><span data-stu-id="4e735-180">OrderLineItem</span></span>

| <span data-ttu-id="4e735-181">Özellik</span><span class="sxs-lookup"><span data-stu-id="4e735-181">Property</span></span>             | <span data-ttu-id="4e735-182">Tür</span><span class="sxs-lookup"><span data-stu-id="4e735-182">Type</span></span>   | <span data-ttu-id="4e735-183">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e735-183">Required</span></span> | <span data-ttu-id="4e735-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e735-184">Description</span></span>                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="4e735-185">LineItemNumber</span><span class="sxs-lookup"><span data-stu-id="4e735-185">LineItemNumber</span></span>       | <span data-ttu-id="4e735-186">sayı</span><span class="sxs-lookup"><span data-stu-id="4e735-186">number</span></span> |    <span data-ttu-id="4e735-187">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-187">Y</span></span>     | <span data-ttu-id="4e735-188">0 ile başlayan satır öğesi numarası</span><span class="sxs-lookup"><span data-stu-id="4e735-188">The line item number, starting with 0</span></span>                                              |
| <span data-ttu-id="4e735-189">OfferId</span><span class="sxs-lookup"><span data-stu-id="4e735-189">OfferId</span></span>              | <span data-ttu-id="4e735-190">string</span><span class="sxs-lookup"><span data-stu-id="4e735-190">string</span></span> |    <span data-ttu-id="4e735-191">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-191">Y</span></span>     | <span data-ttu-id="4e735-192">Teklifin kimliği</span><span class="sxs-lookup"><span data-stu-id="4e735-192">The ID of the offer</span></span>                                                                |
| <span data-ttu-id="4e735-193">SubscriptionId</span><span class="sxs-lookup"><span data-stu-id="4e735-193">SubscriptionId</span></span>       | <span data-ttu-id="4e735-194">string</span><span class="sxs-lookup"><span data-stu-id="4e735-194">string</span></span> |    <span data-ttu-id="4e735-195">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-195">Y</span></span>     | <span data-ttu-id="4e735-196">Aboneliğin kimliği</span><span class="sxs-lookup"><span data-stu-id="4e735-196">The ID of the subscription</span></span>                                                         |
| <span data-ttu-id="4e735-197">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="4e735-197">FriendlyName</span></span>         | <span data-ttu-id="4e735-198">string</span><span class="sxs-lookup"><span data-stu-id="4e735-198">string</span></span> |    <span data-ttu-id="4e735-199">N</span><span class="sxs-lookup"><span data-stu-id="4e735-199">N</span></span>     | <span data-ttu-id="4e735-200">Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı</span><span class="sxs-lookup"><span data-stu-id="4e735-200">The friendly name for the subscription defined by the partner to help disambiguate</span></span> |
| <span data-ttu-id="4e735-201">Miktar</span><span class="sxs-lookup"><span data-stu-id="4e735-201">Quantity</span></span>             | <span data-ttu-id="4e735-202">sayı</span><span class="sxs-lookup"><span data-stu-id="4e735-202">number</span></span> |    <span data-ttu-id="4e735-203">Y</span><span class="sxs-lookup"><span data-stu-id="4e735-203">Y</span></span>     | <span data-ttu-id="4e735-204">Lisans veya örnek sayısı</span><span class="sxs-lookup"><span data-stu-id="4e735-204">The number of licenses or instances</span></span>                                                |
| <span data-ttu-id="4e735-205">PartnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="4e735-205">PartnerIdOnRecord</span></span>    | <span data-ttu-id="4e735-206">string</span><span class="sxs-lookup"><span data-stu-id="4e735-206">string</span></span> |    <span data-ttu-id="4e735-207">N</span><span class="sxs-lookup"><span data-stu-id="4e735-207">N</span></span>     | <span data-ttu-id="4e735-208">Kayıt ortağının MPN KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="4e735-208">The MPN ID of the partner of record</span></span>                                                |
| <span data-ttu-id="4e735-209">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="4e735-209">Attributes</span></span>           | <span data-ttu-id="4e735-210">Nesne</span><span class="sxs-lookup"><span data-stu-id="4e735-210">Object</span></span> |    <span data-ttu-id="4e735-211">N</span><span class="sxs-lookup"><span data-stu-id="4e735-211">N</span></span>     | <span data-ttu-id="4e735-212">"ObjectType" içerir: "Orderlineıtem"</span><span class="sxs-lookup"><span data-stu-id="4e735-212">Contains "ObjectType": "OrderLineItem"</span></span>                                             |

### <a name="request-example"></a><span data-ttu-id="4e735-213">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4e735-213">Request example</span></span>

<span data-ttu-id="4e735-214">Yıllık faturalandırmaya Güncelleştir</span><span class="sxs-lookup"><span data-stu-id="4e735-214">Update to annual billing</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="4e735-215">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4e735-215">REST response</span></span>

<span data-ttu-id="4e735-216">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş abonelik sırasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="4e735-216">If successful, this method returns the updated subscription order in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4e735-217">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4e735-217">Response success and error codes</span></span>

<span data-ttu-id="4e735-218">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4e735-218">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4e735-219">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e735-219">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4e735-220">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4e735-220">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4e735-221">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4e735-221">Response example</span></span>

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