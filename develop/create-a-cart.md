---
title: Sepet oluşturma
description: Sepette bir İş Ortağı Merkezi sipariş eklemek için api'leri kullanmayı öğrenin. Konu, sepet oluşturma ve önkoşullar hakkında bilgi içerir.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: dba54d4f6b97f3d0a51e2f87b32edca686466b89
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973783"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="3146e-104">Müşteri siparişiyle sepet oluşturma</span><span class="sxs-lookup"><span data-stu-id="3146e-104">Create a cart with a customer order</span></span>

<span data-ttu-id="3146e-105">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="3146e-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3146e-106">Sepette bir müşteri için sipariş eklemek de gerekir.</span><span class="sxs-lookup"><span data-stu-id="3146e-106">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="3146e-107">Şu anda satış için kullanılabilenler hakkında daha fazla bilgi için bkz. [Bulut Çözümü Sağlayıcısı programda iş ortağı teklifleri.](/partner-center/csp-offers)</span><span class="sxs-lookup"><span data-stu-id="3146e-107">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3146e-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3146e-108">Prerequisites</span></span>

- <span data-ttu-id="3146e-109">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="3146e-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3146e-110">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3146e-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="3146e-111">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3146e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3146e-112">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="3146e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3146e-113">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="3146e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3146e-114">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="3146e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3146e-115">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="3146e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3146e-116">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="3146e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="3146e-117">C\#</span><span class="sxs-lookup"><span data-stu-id="3146e-117">C\#</span></span>

<span data-ttu-id="3146e-118">Bir müşteriye sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="3146e-118">To create an order for a customer:</span></span>

1. <span data-ttu-id="3146e-119">Bir Sepet nesnesi örneği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="3146e-119">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="3146e-120">**CartLineItem nesnelerinin** listesini oluşturun ve listeyi sepetin LineItems özelliğine attayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3146e-120">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="3146e-121">Her sepet satır öğesi, bir ürün için satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3146e-121">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="3146e-122">En az bir sepet satır öğeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3146e-122">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="3146e-123">Müşteriyi tanımlamak için müşteri kimliğiyle **IAggregatePartner.Customers.ById** yöntemini çağırarak ve ardından Cart özelliğinden arabirimi alarak sepet işlemleri için bir **arabirim** elde edin.</span><span class="sxs-lookup"><span data-stu-id="3146e-123">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="3146e-124">Sepeti oluşturmak **için Create** **veya CreateAsync** yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="3146e-124">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="3146e-125">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="3146e-125">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a><span data-ttu-id="3146e-126">Java</span><span class="sxs-lookup"><span data-stu-id="3146e-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="3146e-127">Bir müşteriye sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="3146e-127">To create an order for a customer:</span></span>

1. <span data-ttu-id="3146e-128">Bir Sepet nesnesi örneği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="3146e-128">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="3146e-129">**CartLineItem nesnelerinin** listesini oluşturun ve listeyi sepetin satır öğelerine attayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3146e-129">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="3146e-130">Her sepet satır öğesi, bir ürün için satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3146e-130">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="3146e-131">En az bir sepet satır öğeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3146e-131">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="3146e-132">Müşteriyi tanımlamak için müşteri kimliğiyle **IAggregatePartner.getCustomers().byId** işlevini çağırarak ve **ardından getCart** işlevinden arabirimi alarak işlemleri sepetine almak için bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="3146e-132">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="3146e-133">Sepeti **oluşturmak için create** işlevini çağırma.</span><span class="sxs-lookup"><span data-stu-id="3146e-133">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="3146e-134">Java örneği</span><span class="sxs-lookup"><span data-stu-id="3146e-134">Java example</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a><span data-ttu-id="3146e-135">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3146e-135">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="3146e-136">Bir müşteriye sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="3146e-136">To create an order for a customer:</span></span>

1. <span data-ttu-id="3146e-137">Bir Sepet nesnesi örneği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="3146e-137">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="3146e-138">**CartLineItem nesnelerinin** listesini oluşturun ve listeyi sepetin satır öğelerine attayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3146e-138">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="3146e-139">Her sepet satır öğesi, bir ürün için satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="3146e-139">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="3146e-140">En az bir sepet satır öğeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="3146e-140">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="3146e-141">Sepeti oluşturmak [**için New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="3146e-141">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a><span data-ttu-id="3146e-142">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3146e-142">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3146e-143">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="3146e-143">Request syntax</span></span>

| <span data-ttu-id="3146e-144">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3146e-144">Method</span></span>   | <span data-ttu-id="3146e-145">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3146e-145">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3146e-146">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="3146e-146">**POST**</span></span> | <span data-ttu-id="3146e-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="3146e-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="3146e-148">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="3146e-148">URI parameter</span></span>

<span data-ttu-id="3146e-149">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3146e-149">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="3146e-150">Ad</span><span class="sxs-lookup"><span data-stu-id="3146e-150">Name</span></span>            | <span data-ttu-id="3146e-151">Tür</span><span class="sxs-lookup"><span data-stu-id="3146e-151">Type</span></span>     | <span data-ttu-id="3146e-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3146e-152">Required</span></span> | <span data-ttu-id="3146e-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3146e-153">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="3146e-154">**customer-id**</span><span class="sxs-lookup"><span data-stu-id="3146e-154">**customer-id**</span></span> | <span data-ttu-id="3146e-155">string</span><span class="sxs-lookup"><span data-stu-id="3146e-155">string</span></span>   | <span data-ttu-id="3146e-156">Yes</span><span class="sxs-lookup"><span data-stu-id="3146e-156">Yes</span></span>      | <span data-ttu-id="3146e-157">Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id.</span><span class="sxs-lookup"><span data-stu-id="3146e-157">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="3146e-158">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3146e-158">Request headers</span></span>

<span data-ttu-id="3146e-159">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="3146e-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3146e-160">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3146e-160">Request body</span></span>

<span data-ttu-id="3146e-161">Bu tablo, istek [gövdesinin](cart-resources.md) Sepet özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="3146e-161">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="3146e-162">Özellik</span><span class="sxs-lookup"><span data-stu-id="3146e-162">Property</span></span>              | <span data-ttu-id="3146e-163">Tür</span><span class="sxs-lookup"><span data-stu-id="3146e-163">Type</span></span>             | <span data-ttu-id="3146e-164">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3146e-164">Required</span></span>        | <span data-ttu-id="3146e-165">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3146e-165">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3146e-166">kimlik</span><span class="sxs-lookup"><span data-stu-id="3146e-166">id</span></span>                    | <span data-ttu-id="3146e-167">dize</span><span class="sxs-lookup"><span data-stu-id="3146e-167">string</span></span>           | <span data-ttu-id="3146e-168">No</span><span class="sxs-lookup"><span data-stu-id="3146e-168">No</span></span>              | <span data-ttu-id="3146e-169">Sepetin başarıyla oluşturulmasının ardından sağlanan bir sepet tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3146e-169">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="3146e-170">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="3146e-170">creationTimeStamp</span></span>     | <span data-ttu-id="3146e-171">DateTime</span><span class="sxs-lookup"><span data-stu-id="3146e-171">DateTime</span></span>         | <span data-ttu-id="3146e-172">Hayır</span><span class="sxs-lookup"><span data-stu-id="3146e-172">No</span></span>              | <span data-ttu-id="3146e-173">Sepetin tarih-saat biçiminde oluşturulma tarihi.</span><span class="sxs-lookup"><span data-stu-id="3146e-173">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="3146e-174">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3146e-174">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="3146e-175">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="3146e-175">lastModifiedTimeStamp</span></span> | <span data-ttu-id="3146e-176">DateTime</span><span class="sxs-lookup"><span data-stu-id="3146e-176">DateTime</span></span>         | <span data-ttu-id="3146e-177">Hayır</span><span class="sxs-lookup"><span data-stu-id="3146e-177">No</span></span>              | <span data-ttu-id="3146e-178">Sepetin en son güncelleştirilen tarih-saat biçiminde olduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="3146e-178">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="3146e-179">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3146e-179">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="3146e-180">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="3146e-180">expirationTimeStamp</span></span>   | <span data-ttu-id="3146e-181">DateTime</span><span class="sxs-lookup"><span data-stu-id="3146e-181">DateTime</span></span>         | <span data-ttu-id="3146e-182">Hayır</span><span class="sxs-lookup"><span data-stu-id="3146e-182">No</span></span>              | <span data-ttu-id="3146e-183">Sepet tarih-saat biçiminde sona erer.</span><span class="sxs-lookup"><span data-stu-id="3146e-183">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="3146e-184">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3146e-184">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="3146e-185">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="3146e-185">lastModifiedUser</span></span>      | <span data-ttu-id="3146e-186">dize</span><span class="sxs-lookup"><span data-stu-id="3146e-186">string</span></span>           | <span data-ttu-id="3146e-187">No</span><span class="sxs-lookup"><span data-stu-id="3146e-187">No</span></span>              | <span data-ttu-id="3146e-188">Sepeti en son güncelleştirilen kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="3146e-188">The user who last updated the cart.</span></span> <span data-ttu-id="3146e-189">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3146e-189">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="3146e-190">lineItems</span><span class="sxs-lookup"><span data-stu-id="3146e-190">lineItems</span></span>             | <span data-ttu-id="3146e-191">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="3146e-191">Array of objects</span></span> | <span data-ttu-id="3146e-192">Yes</span><span class="sxs-lookup"><span data-stu-id="3146e-192">Yes</span></span>             | <span data-ttu-id="3146e-193">[Bir CartLineItem kaynakları](cart-resources.md#cartlineitem) dizisi.</span><span class="sxs-lookup"><span data-stu-id="3146e-193">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="3146e-194">Bu tablo, istek [gövdesinin CartLineItem](cart-resources.md#cartlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="3146e-194">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="3146e-195">Özellik</span><span class="sxs-lookup"><span data-stu-id="3146e-195">Property</span></span>       |            <span data-ttu-id="3146e-196">Tür</span><span class="sxs-lookup"><span data-stu-id="3146e-196">Type</span></span>             | <span data-ttu-id="3146e-197">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3146e-197">Required</span></span> |                                                                                         <span data-ttu-id="3146e-198">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3146e-198">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="3146e-199">kimlik</span><span class="sxs-lookup"><span data-stu-id="3146e-199">id</span></span>          |           <span data-ttu-id="3146e-200">dize</span><span class="sxs-lookup"><span data-stu-id="3146e-200">string</span></span>            |    <span data-ttu-id="3146e-201">No</span><span class="sxs-lookup"><span data-stu-id="3146e-201">No</span></span>    |                                                     <span data-ttu-id="3146e-202">Sepet satır öğesi için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="3146e-202">A unique identifier for a cart line item.</span></span> <span data-ttu-id="3146e-203">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3146e-203">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="3146e-204">catalogId</span><span class="sxs-lookup"><span data-stu-id="3146e-204">catalogId</span></span>      |           <span data-ttu-id="3146e-205">string</span><span class="sxs-lookup"><span data-stu-id="3146e-205">string</span></span>            |   <span data-ttu-id="3146e-206">Yes</span><span class="sxs-lookup"><span data-stu-id="3146e-206">Yes</span></span>    |                                                                                <span data-ttu-id="3146e-207">Katalog öğesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="3146e-207">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="3146e-208">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="3146e-208">friendlyName</span></span>     |           <span data-ttu-id="3146e-209">dize</span><span class="sxs-lookup"><span data-stu-id="3146e-209">string</span></span>            |    <span data-ttu-id="3146e-210">No</span><span class="sxs-lookup"><span data-stu-id="3146e-210">No</span></span>    |                                                    <span data-ttu-id="3146e-211">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="3146e-211">Optional.</span></span> <span data-ttu-id="3146e-212">Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="3146e-212">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="3146e-213">miktar</span><span class="sxs-lookup"><span data-stu-id="3146e-213">quantity</span></span>       |             <span data-ttu-id="3146e-214">int</span><span class="sxs-lookup"><span data-stu-id="3146e-214">int</span></span>             |   <span data-ttu-id="3146e-215">Yes</span><span class="sxs-lookup"><span data-stu-id="3146e-215">Yes</span></span>    |                                                                            <span data-ttu-id="3146e-216">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="3146e-216">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="3146e-217">currencyCode</span><span class="sxs-lookup"><span data-stu-id="3146e-217">currencyCode</span></span>     |           <span data-ttu-id="3146e-218">dize</span><span class="sxs-lookup"><span data-stu-id="3146e-218">string</span></span>            |    <span data-ttu-id="3146e-219">No</span><span class="sxs-lookup"><span data-stu-id="3146e-219">No</span></span>    |                                                                                     <span data-ttu-id="3146e-220">Para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="3146e-220">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="3146e-221">billingCycle</span><span class="sxs-lookup"><span data-stu-id="3146e-221">billingCycle</span></span>     |           <span data-ttu-id="3146e-222">Nesne</span><span class="sxs-lookup"><span data-stu-id="3146e-222">Object</span></span>            |   <span data-ttu-id="3146e-223">Yes</span><span class="sxs-lookup"><span data-stu-id="3146e-223">Yes</span></span>    |                                                                    <span data-ttu-id="3146e-224">Geçerli dönem için ayarlanmış faturalama dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="3146e-224">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="3146e-225">Katılımcılar</span><span class="sxs-lookup"><span data-stu-id="3146e-225">participants</span></span>     | <span data-ttu-id="3146e-226">Nesne Dizesi çiftlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="3146e-226">List of Object String pairs</span></span> |    <span data-ttu-id="3146e-227">Hayır</span><span class="sxs-lookup"><span data-stu-id="3146e-227">No</span></span>    |                                                                <span data-ttu-id="3146e-228">Satın almada Kayıt üzerinde PartnerId (MPNID) koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="3146e-228">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="3146e-229">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="3146e-229">provisioningContext</span></span> | <span data-ttu-id="3146e-230">Sözlük<dizesi, dize></span><span class="sxs-lookup"><span data-stu-id="3146e-230">Dictionary<string, string></span></span>  |    <span data-ttu-id="3146e-231">Hayır</span><span class="sxs-lookup"><span data-stu-id="3146e-231">No</span></span>    | <span data-ttu-id="3146e-232">Katalogdaki bazı öğeler için sağlama için gereken bilgiler.</span><span class="sxs-lookup"><span data-stu-id="3146e-232">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="3146e-233">SKU'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="3146e-233">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="3146e-234">orderGroup</span><span class="sxs-lookup"><span data-stu-id="3146e-234">orderGroup</span></span>      |           <span data-ttu-id="3146e-235">dize</span><span class="sxs-lookup"><span data-stu-id="3146e-235">string</span></span>            |    <span data-ttu-id="3146e-236">No</span><span class="sxs-lookup"><span data-stu-id="3146e-236">No</span></span>    |                                                                   <span data-ttu-id="3146e-237">Hangi öğelerin bir araya yerleştiril olduğunu belirten bir grup.</span><span class="sxs-lookup"><span data-stu-id="3146e-237">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="3146e-238">error</span><span class="sxs-lookup"><span data-stu-id="3146e-238">error</span></span>        |           <span data-ttu-id="3146e-239">Nesne</span><span class="sxs-lookup"><span data-stu-id="3146e-239">Object</span></span>            |    <span data-ttu-id="3146e-240">Hayır</span><span class="sxs-lookup"><span data-stu-id="3146e-240">No</span></span>    |                                                                     <span data-ttu-id="3146e-241">Bir hata varsa sepet oluşturulduktan sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="3146e-241">Applied after cart is created if there is an error.</span></span>                                                                      |
|     <span data-ttu-id="3146e-242">renewsTo</span><span class="sxs-lookup"><span data-stu-id="3146e-242">renewsTo</span></span>        | <span data-ttu-id="3146e-243">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="3146e-243">Array of objects</span></span>            |    <span data-ttu-id="3146e-244">Hayır</span><span class="sxs-lookup"><span data-stu-id="3146e-244">No</span></span>    |                                                    <span data-ttu-id="3146e-245">[RenewsTo kaynakları dizisi.](cart-resources.md#renewsto)</span><span class="sxs-lookup"><span data-stu-id="3146e-245">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="3146e-246">Bu tabloda istek [gövdesinin RenewsTo](cart-resources.md#renewsto) özellikleri açık edilmektedir.</span><span class="sxs-lookup"><span data-stu-id="3146e-246">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="3146e-247">Özellik</span><span class="sxs-lookup"><span data-stu-id="3146e-247">Property</span></span>              | <span data-ttu-id="3146e-248">Tür</span><span class="sxs-lookup"><span data-stu-id="3146e-248">Type</span></span>             | <span data-ttu-id="3146e-249">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3146e-249">Required</span></span>        | <span data-ttu-id="3146e-250">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3146e-250">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3146e-251">termDuration</span><span class="sxs-lookup"><span data-stu-id="3146e-251">termDuration</span></span>          | <span data-ttu-id="3146e-252">dize</span><span class="sxs-lookup"><span data-stu-id="3146e-252">string</span></span>           | <span data-ttu-id="3146e-253">No</span><span class="sxs-lookup"><span data-stu-id="3146e-253">No</span></span>              | <span data-ttu-id="3146e-254">Yenileme süresinin ISO 8601 gösterimi.</span><span class="sxs-lookup"><span data-stu-id="3146e-254">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="3146e-255">Desteklenen geçerli değerler **P1M (1** ay) ve **P1Y (1** yıl) değerleridir.</span><span class="sxs-lookup"><span data-stu-id="3146e-255">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="3146e-256">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3146e-256">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="3146e-257">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3146e-257">REST response</span></span>

<span data-ttu-id="3146e-258">Başarılı olursa, bu yöntem yanıt [gövdesinde](cart-resources.md) doldurulmuş Sepet kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="3146e-258">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3146e-259">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3146e-259">Response success and error codes</span></span>

<span data-ttu-id="3146e-260">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="3146e-260">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3146e-261">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3146e-261">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3146e-262">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="3146e-262">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3146e-263">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3146e-263">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
