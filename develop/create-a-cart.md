---
title: Sepet oluşturma
description: Iş Ortağı Merkezi API 'Lerini kullanarak bir sepette müşteri için sipariş ekleme hakkında bilgi edinin. Konu başlığı, bir sepet ve Önkoşullar oluşturma hakkında bilgiler içerir.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770127"
---
# <a name="create-a-cart-with-a-customer-order"></a><span data-ttu-id="72558-104">Müşteri siparişi içeren bir sepet oluşturma</span><span class="sxs-lookup"><span data-stu-id="72558-104">Create a cart with a customer order</span></span>

<span data-ttu-id="72558-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="72558-105">**Applies to:**</span></span>

- <span data-ttu-id="72558-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="72558-106">Partner Center</span></span>
- <span data-ttu-id="72558-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="72558-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="72558-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="72558-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="72558-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="72558-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="72558-110">Bir sepetteki bir müşteri için sipariş ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72558-110">You can add an order for a customer in a cart.</span></span> <span data-ttu-id="72558-111">Şu anda Satım için kullanılabilir olanlar hakkında daha fazla bilgi için bkz. [Cloud Solution Provider programındaki Iş ortağı teklifleri](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="72558-111">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="72558-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="72558-112">Prerequisites</span></span>

- <span data-ttu-id="72558-113">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="72558-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="72558-114">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="72558-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="72558-115">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="72558-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="72558-116">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="72558-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="72558-117">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="72558-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="72558-118">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="72558-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="72558-119">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="72558-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="72558-120">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="72558-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="72558-121">C\#</span><span class="sxs-lookup"><span data-stu-id="72558-121">C\#</span></span>

<span data-ttu-id="72558-122">Bir müşteri için sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="72558-122">To create an order for a customer:</span></span>

1. <span data-ttu-id="72558-123">Bir sepet nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72558-123">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="72558-124">**Cartlineıtem** nesnelerinin bir listesini oluşturun ve listeyi sepetin LineItems özelliğine atayın.</span><span class="sxs-lookup"><span data-stu-id="72558-124">Create a list of **CartLineItem** objects, and assign the list to the cart's LineItems property.</span></span> <span data-ttu-id="72558-125">Her sepet çizgisi öğesi, bir ürünün satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="72558-125">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="72558-126">En az bir sepet çizgisi öğesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="72558-126">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="72558-127">Müşteriyi belirlemek için müşteri KIMLIĞI ile **ıaggregatepartner. Customers. Byıd** yöntemini çağırarak ve sonra da **sepet** özelliğinden arabirimi almak için bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="72558-127">Obtain an interface to cart operations by calling the **IAggregatePartner.Customers.ById** method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

4. <span data-ttu-id="72558-128">Sepetini oluşturmak için **Create** veya **createasync** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="72558-128">Call the **Create** or **CreateAsync** method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="72558-129">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="72558-129">C\# example</span></span>

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

## <a name="java"></a><span data-ttu-id="72558-130">Java</span><span class="sxs-lookup"><span data-stu-id="72558-130">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="72558-131">Bir müşteri için sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="72558-131">To create an order for a customer:</span></span>

1. <span data-ttu-id="72558-132">Bir sepet nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72558-132">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="72558-133">**Cartlineıtem** nesnelerinin bir listesini oluşturun ve listeyi sepetinin çizgi öğelerine atayın.</span><span class="sxs-lookup"><span data-stu-id="72558-133">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="72558-134">Her sepet çizgisi öğesi, bir ürünün satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="72558-134">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="72558-135">En az bir sepet çizgisi öğesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="72558-135">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="72558-136">Müşteriyi belirlemek için müşteri KIMLIĞIYLE **ıaggregatepartner. getCustomers (). Byıd** işlevini çağırarak ve sonra **getcart** işlevinden arabirimi alarak, işlem yapmak için bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="72558-136">Obtain an interface to cart operations by calling the **IAggregatePartner.getCustomers().byId** function with the customer ID to identify the customer, and then retrieving the interface from the **getCart** function.</span></span>

4. <span data-ttu-id="72558-137">Sepetini oluşturmak için **Oluştur** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="72558-137">Call the **create** function to create the cart.</span></span>

## <a name="java-example"></a><span data-ttu-id="72558-138">Java örneği</span><span class="sxs-lookup"><span data-stu-id="72558-138">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="72558-139">PowerShell</span><span class="sxs-lookup"><span data-stu-id="72558-139">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="72558-140">Bir müşteri için sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="72558-140">To create an order for a customer:</span></span>

1. <span data-ttu-id="72558-141">Bir sepet nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="72558-141">Instantiate a Cart object.</span></span>

2. <span data-ttu-id="72558-142">**Cartlineıtem** nesnelerinin bir listesini oluşturun ve listeyi sepetinin çizgi öğelerine atayın.</span><span class="sxs-lookup"><span data-stu-id="72558-142">Create a list of **CartLineItem** objects, and assign the list to the cart's line items.</span></span> <span data-ttu-id="72558-143">Her sepet çizgisi öğesi, bir ürünün satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="72558-143">Each cart line item contains the purchase information for one product.</span></span> <span data-ttu-id="72558-144">En az bir sepet çizgisi öğesi olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="72558-144">You must have at least one cart line item.</span></span>

3. <span data-ttu-id="72558-145">Sepetini oluşturmak için [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="72558-145">Execute the [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) command to create the cart.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="72558-146">REST isteği</span><span class="sxs-lookup"><span data-stu-id="72558-146">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="72558-147">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="72558-147">Request syntax</span></span>

| <span data-ttu-id="72558-148">Yöntem</span><span class="sxs-lookup"><span data-stu-id="72558-148">Method</span></span>   | <span data-ttu-id="72558-149">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="72558-149">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72558-150">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="72558-150">**POST**</span></span> | <span data-ttu-id="72558-151">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="72558-151">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="72558-152">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="72558-152">URI parameter</span></span>

<span data-ttu-id="72558-153">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="72558-153">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="72558-154">Ad</span><span class="sxs-lookup"><span data-stu-id="72558-154">Name</span></span>            | <span data-ttu-id="72558-155">Tür</span><span class="sxs-lookup"><span data-stu-id="72558-155">Type</span></span>     | <span data-ttu-id="72558-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="72558-156">Required</span></span> | <span data-ttu-id="72558-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="72558-157">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="72558-158">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="72558-158">**customer-id**</span></span> | <span data-ttu-id="72558-159">string</span><span class="sxs-lookup"><span data-stu-id="72558-159">string</span></span>   | <span data-ttu-id="72558-160">Yes</span><span class="sxs-lookup"><span data-stu-id="72558-160">Yes</span></span>      | <span data-ttu-id="72558-161">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="72558-161">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="72558-162">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="72558-162">Request headers</span></span>

<span data-ttu-id="72558-163">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="72558-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="72558-164">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="72558-164">Request body</span></span>

<span data-ttu-id="72558-165">Bu tablo, istek gövdesinde [sepet](cart-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="72558-165">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="72558-166">Özellik</span><span class="sxs-lookup"><span data-stu-id="72558-166">Property</span></span>              | <span data-ttu-id="72558-167">Tür</span><span class="sxs-lookup"><span data-stu-id="72558-167">Type</span></span>             | <span data-ttu-id="72558-168">Gerekli</span><span class="sxs-lookup"><span data-stu-id="72558-168">Required</span></span>        | <span data-ttu-id="72558-169">Açıklama</span><span class="sxs-lookup"><span data-stu-id="72558-169">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72558-170">kimlik</span><span class="sxs-lookup"><span data-stu-id="72558-170">id</span></span>                    | <span data-ttu-id="72558-171">dize</span><span class="sxs-lookup"><span data-stu-id="72558-171">string</span></span>           | <span data-ttu-id="72558-172">No</span><span class="sxs-lookup"><span data-stu-id="72558-172">No</span></span>              | <span data-ttu-id="72558-173">Sepet başarıyla oluşturulduktan sonra sağlanan bir sepet tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="72558-173">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="72558-174">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="72558-174">creationTimeStamp</span></span>     | <span data-ttu-id="72558-175">DateTime</span><span class="sxs-lookup"><span data-stu-id="72558-175">DateTime</span></span>         | <span data-ttu-id="72558-176">No</span><span class="sxs-lookup"><span data-stu-id="72558-176">No</span></span>              | <span data-ttu-id="72558-177">Sepetin oluşturulduğu tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="72558-177">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="72558-178">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="72558-178">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="72558-179">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="72558-179">lastModifiedTimeStamp</span></span> | <span data-ttu-id="72558-180">DateTime</span><span class="sxs-lookup"><span data-stu-id="72558-180">DateTime</span></span>         | <span data-ttu-id="72558-181">No</span><span class="sxs-lookup"><span data-stu-id="72558-181">No</span></span>              | <span data-ttu-id="72558-182">Sepetin son güncelleştirildiği tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="72558-182">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="72558-183">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="72558-183">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="72558-184">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="72558-184">expirationTimeStamp</span></span>   | <span data-ttu-id="72558-185">DateTime</span><span class="sxs-lookup"><span data-stu-id="72558-185">DateTime</span></span>         | <span data-ttu-id="72558-186">No</span><span class="sxs-lookup"><span data-stu-id="72558-186">No</span></span>              | <span data-ttu-id="72558-187">Sepetin süresinin dolacağı tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="72558-187">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="72558-188">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="72558-188">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="72558-189">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="72558-189">lastModifiedUser</span></span>      | <span data-ttu-id="72558-190">dize</span><span class="sxs-lookup"><span data-stu-id="72558-190">string</span></span>           | <span data-ttu-id="72558-191">No</span><span class="sxs-lookup"><span data-stu-id="72558-191">No</span></span>              | <span data-ttu-id="72558-192">Sepetini son güncelleştiren Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="72558-192">The user who last updated the cart.</span></span> <span data-ttu-id="72558-193">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="72558-193">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="72558-194">LineItems</span><span class="sxs-lookup"><span data-stu-id="72558-194">lineItems</span></span>             | <span data-ttu-id="72558-195">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="72558-195">Array of objects</span></span> | <span data-ttu-id="72558-196">Yes</span><span class="sxs-lookup"><span data-stu-id="72558-196">Yes</span></span>             | <span data-ttu-id="72558-197">Bir [Cartlineıtem](cart-resources.md#cartlineitem) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="72558-197">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                     |

<span data-ttu-id="72558-198">Bu tablo, istek gövdesinde [Cartlineıtem](cart-resources.md#cartlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="72558-198">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="72558-199">Özellik</span><span class="sxs-lookup"><span data-stu-id="72558-199">Property</span></span>       |            <span data-ttu-id="72558-200">Tür</span><span class="sxs-lookup"><span data-stu-id="72558-200">Type</span></span>             | <span data-ttu-id="72558-201">Gerekli</span><span class="sxs-lookup"><span data-stu-id="72558-201">Required</span></span> |                                                                                         <span data-ttu-id="72558-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="72558-202">Description</span></span>                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         <span data-ttu-id="72558-203">kimlik</span><span class="sxs-lookup"><span data-stu-id="72558-203">id</span></span>          |           <span data-ttu-id="72558-204">dize</span><span class="sxs-lookup"><span data-stu-id="72558-204">string</span></span>            |    <span data-ttu-id="72558-205">No</span><span class="sxs-lookup"><span data-stu-id="72558-205">No</span></span>    |                                                     <span data-ttu-id="72558-206">Sepet çizgisi öğesi için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="72558-206">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="72558-207">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="72558-207">Applied upon successful creation of cart.</span></span>                                                     |
|      <span data-ttu-id="72558-208">catalogId</span><span class="sxs-lookup"><span data-stu-id="72558-208">catalogId</span></span>      |           <span data-ttu-id="72558-209">string</span><span class="sxs-lookup"><span data-stu-id="72558-209">string</span></span>            |   <span data-ttu-id="72558-210">Yes</span><span class="sxs-lookup"><span data-stu-id="72558-210">Yes</span></span>    |                                                                                <span data-ttu-id="72558-211">Katalog öğesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="72558-211">The catalog item identifier.</span></span>                                                                                 |
|    <span data-ttu-id="72558-212">friendlyName</span><span class="sxs-lookup"><span data-stu-id="72558-212">friendlyName</span></span>     |           <span data-ttu-id="72558-213">dize</span><span class="sxs-lookup"><span data-stu-id="72558-213">string</span></span>            |    <span data-ttu-id="72558-214">No</span><span class="sxs-lookup"><span data-stu-id="72558-214">No</span></span>    |                                                    <span data-ttu-id="72558-215">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="72558-215">Optional.</span></span> <span data-ttu-id="72558-216">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="72558-216">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                    |
|      <span data-ttu-id="72558-217">miktar</span><span class="sxs-lookup"><span data-stu-id="72558-217">quantity</span></span>       |             <span data-ttu-id="72558-218">int</span><span class="sxs-lookup"><span data-stu-id="72558-218">int</span></span>             |   <span data-ttu-id="72558-219">Yes</span><span class="sxs-lookup"><span data-stu-id="72558-219">Yes</span></span>    |                                                                            <span data-ttu-id="72558-220">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="72558-220">The number of licenses or instances.</span></span>                                                                             |
|    <span data-ttu-id="72558-221">currencyCode</span><span class="sxs-lookup"><span data-stu-id="72558-221">currencyCode</span></span>     |           <span data-ttu-id="72558-222">dize</span><span class="sxs-lookup"><span data-stu-id="72558-222">string</span></span>            |    <span data-ttu-id="72558-223">No</span><span class="sxs-lookup"><span data-stu-id="72558-223">No</span></span>    |                                                                                     <span data-ttu-id="72558-224">Para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="72558-224">The currency code.</span></span>                                                                                      |
|    <span data-ttu-id="72558-225">Bilimlingcycle</span><span class="sxs-lookup"><span data-stu-id="72558-225">billingCycle</span></span>     |           <span data-ttu-id="72558-226">Nesne</span><span class="sxs-lookup"><span data-stu-id="72558-226">Object</span></span>            |   <span data-ttu-id="72558-227">Yes</span><span class="sxs-lookup"><span data-stu-id="72558-227">Yes</span></span>    |                                                                    <span data-ttu-id="72558-228">Geçerli dönem için ayarlanan faturalandırma dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="72558-228">The type of billing cycle set for the current period.</span></span>                                                                    |
|    <span data-ttu-id="72558-229">Katılımcılar</span><span class="sxs-lookup"><span data-stu-id="72558-229">participants</span></span>     | <span data-ttu-id="72558-230">Nesne dizesi çiftlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="72558-230">List of Object String pairs</span></span> |    <span data-ttu-id="72558-231">No</span><span class="sxs-lookup"><span data-stu-id="72558-231">No</span></span>    |                                                                <span data-ttu-id="72558-232">Satınalmada iş ortağı kimliği koleksiyonu (MPNıD).</span><span class="sxs-lookup"><span data-stu-id="72558-232">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                 |
| <span data-ttu-id="72558-233">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="72558-233">provisioningContext</span></span> | <span data-ttu-id="72558-234">Sözlük<dize, dize></span><span class="sxs-lookup"><span data-stu-id="72558-234">Dictionary<string, string></span></span>  |    <span data-ttu-id="72558-235">No</span><span class="sxs-lookup"><span data-stu-id="72558-235">No</span></span>    | <span data-ttu-id="72558-236">Katalogdaki bazı öğelerin sağlanması için gereken bilgiler.</span><span class="sxs-lookup"><span data-stu-id="72558-236">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="72558-237">SKU 'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="72558-237">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span> |
|     <span data-ttu-id="72558-238">orderGroup</span><span class="sxs-lookup"><span data-stu-id="72558-238">orderGroup</span></span>      |           <span data-ttu-id="72558-239">dize</span><span class="sxs-lookup"><span data-stu-id="72558-239">string</span></span>            |    <span data-ttu-id="72558-240">No</span><span class="sxs-lookup"><span data-stu-id="72558-240">No</span></span>    |                                                                   <span data-ttu-id="72558-241">Hangi öğelerin birlikte yerleştirilebileceğini belirten bir grup.</span><span class="sxs-lookup"><span data-stu-id="72558-241">A group to indicate which items can be placed together.</span></span>                                                                   |
|        <span data-ttu-id="72558-242">error</span><span class="sxs-lookup"><span data-stu-id="72558-242">error</span></span>        |           <span data-ttu-id="72558-243">Nesne</span><span class="sxs-lookup"><span data-stu-id="72558-243">Object</span></span>            |    <span data-ttu-id="72558-244">No</span><span class="sxs-lookup"><span data-stu-id="72558-244">No</span></span>    |                                                                     <span data-ttu-id="72558-245">Bir hata durumunda sepet oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="72558-245">Applied after cart is created in case of an error.</span></span>                                                                      |
|     <span data-ttu-id="72558-246">renewsTo</span><span class="sxs-lookup"><span data-stu-id="72558-246">renewsTo</span></span>        | <span data-ttu-id="72558-247">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="72558-247">Array of objects</span></span>            |    <span data-ttu-id="72558-248">No</span><span class="sxs-lookup"><span data-stu-id="72558-248">No</span></span>    |                                                    <span data-ttu-id="72558-249">[RenewsTo](cart-resources.md#renewsto) kaynaklarından oluşan bir dizi.</span><span class="sxs-lookup"><span data-stu-id="72558-249">An array of [RenewsTo](cart-resources.md#renewsto) resources.</span></span>                                                                            |

<span data-ttu-id="72558-250">Bu tablo, istek gövdesinde [RenewsTo](cart-resources.md#renewsto) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="72558-250">This table describes the [RenewsTo](cart-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="72558-251">Özellik</span><span class="sxs-lookup"><span data-stu-id="72558-251">Property</span></span>              | <span data-ttu-id="72558-252">Tür</span><span class="sxs-lookup"><span data-stu-id="72558-252">Type</span></span>             | <span data-ttu-id="72558-253">Gerekli</span><span class="sxs-lookup"><span data-stu-id="72558-253">Required</span></span>        | <span data-ttu-id="72558-254">Açıklama</span><span class="sxs-lookup"><span data-stu-id="72558-254">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="72558-255">termDuration</span><span class="sxs-lookup"><span data-stu-id="72558-255">termDuration</span></span>          | <span data-ttu-id="72558-256">dize</span><span class="sxs-lookup"><span data-stu-id="72558-256">string</span></span>           | <span data-ttu-id="72558-257">No</span><span class="sxs-lookup"><span data-stu-id="72558-257">No</span></span>              | <span data-ttu-id="72558-258">Yenileme teriminin süresinin ISO 8601 temsili.</span><span class="sxs-lookup"><span data-stu-id="72558-258">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="72558-259">Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl).</span><span class="sxs-lookup"><span data-stu-id="72558-259">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="72558-260">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="72558-260">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="72558-261">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="72558-261">REST response</span></span>

<span data-ttu-id="72558-262">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [sepet](cart-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="72558-262">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="72558-263">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="72558-263">Response success and error codes</span></span>

<span data-ttu-id="72558-264">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="72558-264">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="72558-265">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="72558-265">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="72558-266">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="72558-266">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="72558-267">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="72558-267">Response example</span></span>

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
