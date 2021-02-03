---
title: Eklentilerle bir sepet oluşturma
description: Bir sepet aracılığıyla eklentilere bir müşteri siparişi eklemek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makalesinde, eklentilerle bir sepet oluşturmak için önkoşulları ve adımları paylaşır.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770132"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="2cfc0-104">Eklentiler ile müşteri siparişi arasında bir sepet oluşturma</span><span class="sxs-lookup"><span data-stu-id="2cfc0-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="2cfc0-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="2cfc0-105">**Applies to:**</span></span>

- <span data-ttu-id="2cfc0-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2cfc0-106">Partner Center</span></span>

<span data-ttu-id="2cfc0-107">Eklentileri bir sepet aracılığıyla satın alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-107">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="2cfc0-108">Şu anda Satım için kullanılabilir olanlar hakkında daha fazla bilgi için bkz. [Cloud Solution Provider programındaki Iş ortağı teklifleri](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="2cfc0-108">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2cfc0-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2cfc0-109">Prerequisites</span></span>

- <span data-ttu-id="2cfc0-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2cfc0-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2cfc0-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2cfc0-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2cfc0-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2cfc0-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2cfc0-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2cfc0-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2cfc0-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="2cfc0-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2cfc0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="2cfc0-118">C\#</span></span>

<span data-ttu-id="2cfc0-119">Bir sepet, temel teklifin ve bunlara karşılık gelen eklentilerin satın alınmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-119">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="2cfc0-120">Bir sepet oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2cfc0-120">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="2cfc0-121">Bir [**sepet**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-121">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="2cfc0-122">Taban teklifleri temsil eden [**Cartlineıtem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) nesnelerinin bir listesini oluşturun ve listeyi sepetinin [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) özelliğine atayın.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-122">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects which represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="2cfc0-123">Her temel teklifin sepet çizgisi öğesi altında, **Addonıtems** listesini her biri temel teklifte satın alınacak eklentiyi temsil eden diğer **Cartlineıtem** nesneleriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-123">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="2cfc0-124">[**Iaggregatepartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) kullanarak, müşteriyi tanımlamak üzere [**ıustomercollection. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırmak ve sonra da bu arabirimi **sepet** özelliğinden almak için bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-124">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="2cfc0-125">Son olarak, sepet oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-125">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="2cfc0-126">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="2cfc0-126">C\# example</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

<span data-ttu-id="2cfc0-127">Eklentilerin mevcut temel abonelikler için satın alınmasını sağlayacak bir sepet oluşturmak için bu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="2cfc0-127">Follow these steps to create a cart which will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="2cfc0-128">"Parentsubscriptionıd" anahtarıyla **Provisioningcontext** ÖZELLIĞINDEKI abonelik kimliğini içeren yeni bir **Cartlineıtem** içeren bir **sepet** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-128">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="2cfc0-129">**Create** veya **createasync** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-129">Call the **Create** or **CreateAsync** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a><span data-ttu-id="2cfc0-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2cfc0-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2cfc0-131">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2cfc0-131">Request syntax</span></span>

| <span data-ttu-id="2cfc0-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2cfc0-132">Method</span></span>   | <span data-ttu-id="2cfc0-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2cfc0-133">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2cfc0-134">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="2cfc0-134">**POST**</span></span> | <span data-ttu-id="2cfc0-135">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="2cfc0-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="2cfc0-136">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="2cfc0-136">URI parameter</span></span>

<span data-ttu-id="2cfc0-137">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-137">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="2cfc0-138">Ad</span><span class="sxs-lookup"><span data-stu-id="2cfc0-138">Name</span></span>            | <span data-ttu-id="2cfc0-139">Tür</span><span class="sxs-lookup"><span data-stu-id="2cfc0-139">Type</span></span>     | <span data-ttu-id="2cfc0-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2cfc0-140">Required</span></span> | <span data-ttu-id="2cfc0-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2cfc0-141">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="2cfc0-142">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="2cfc0-142">**customer-id**</span></span> | <span data-ttu-id="2cfc0-143">string</span><span class="sxs-lookup"><span data-stu-id="2cfc0-143">string</span></span>   | <span data-ttu-id="2cfc0-144">Yes</span><span class="sxs-lookup"><span data-stu-id="2cfc0-144">Yes</span></span>      | <span data-ttu-id="2cfc0-145">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-145">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="2cfc0-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2cfc0-146">Request headers</span></span>

<span data-ttu-id="2cfc0-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2cfc0-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2cfc0-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2cfc0-148">Request body</span></span>

<span data-ttu-id="2cfc0-149">Bu tablo, istek gövdesinde [sepet](cart-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-149">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="2cfc0-150">Özellik</span><span class="sxs-lookup"><span data-stu-id="2cfc0-150">Property</span></span>              | <span data-ttu-id="2cfc0-151">Tür</span><span class="sxs-lookup"><span data-stu-id="2cfc0-151">Type</span></span>             | <span data-ttu-id="2cfc0-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2cfc0-152">Required</span></span>        | <span data-ttu-id="2cfc0-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2cfc0-153">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2cfc0-154">kimlik</span><span class="sxs-lookup"><span data-stu-id="2cfc0-154">id</span></span>                    | <span data-ttu-id="2cfc0-155">dize</span><span class="sxs-lookup"><span data-stu-id="2cfc0-155">string</span></span>           | <span data-ttu-id="2cfc0-156">No</span><span class="sxs-lookup"><span data-stu-id="2cfc0-156">No</span></span>              | <span data-ttu-id="2cfc0-157">Sepet başarıyla oluşturulduktan sonra sağlanan bir sepet tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-157">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="2cfc0-158">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="2cfc0-158">creationTimeStamp</span></span>     | <span data-ttu-id="2cfc0-159">DateTime</span><span class="sxs-lookup"><span data-stu-id="2cfc0-159">DateTime</span></span>         | <span data-ttu-id="2cfc0-160">No</span><span class="sxs-lookup"><span data-stu-id="2cfc0-160">No</span></span>              | <span data-ttu-id="2cfc0-161">Sepetin oluşturulduğu tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-161">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="2cfc0-162">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-162">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="2cfc0-163">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="2cfc0-163">lastModifiedTimeStamp</span></span> | <span data-ttu-id="2cfc0-164">DateTime</span><span class="sxs-lookup"><span data-stu-id="2cfc0-164">DateTime</span></span>         | <span data-ttu-id="2cfc0-165">No</span><span class="sxs-lookup"><span data-stu-id="2cfc0-165">No</span></span>              | <span data-ttu-id="2cfc0-166">Sepetin son güncelleştirildiği tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-166">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="2cfc0-167">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-167">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="2cfc0-168">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="2cfc0-168">expirationTimeStamp</span></span>   | <span data-ttu-id="2cfc0-169">DateTime</span><span class="sxs-lookup"><span data-stu-id="2cfc0-169">DateTime</span></span>         | <span data-ttu-id="2cfc0-170">No</span><span class="sxs-lookup"><span data-stu-id="2cfc0-170">No</span></span>              | <span data-ttu-id="2cfc0-171">Sepetin süresinin dolacağı tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-171">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="2cfc0-172">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-172">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="2cfc0-173">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="2cfc0-173">lastModifiedUser</span></span>      | <span data-ttu-id="2cfc0-174">dize</span><span class="sxs-lookup"><span data-stu-id="2cfc0-174">string</span></span>           | <span data-ttu-id="2cfc0-175">No</span><span class="sxs-lookup"><span data-stu-id="2cfc0-175">No</span></span>              | <span data-ttu-id="2cfc0-176">Sepetini son güncelleştiren Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-176">The user who last updated the cart.</span></span> <span data-ttu-id="2cfc0-177">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-177">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="2cfc0-178">LineItems</span><span class="sxs-lookup"><span data-stu-id="2cfc0-178">lineItems</span></span>             | <span data-ttu-id="2cfc0-179">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="2cfc0-179">Array of objects</span></span> | <span data-ttu-id="2cfc0-180">Yes</span><span class="sxs-lookup"><span data-stu-id="2cfc0-180">Yes</span></span>             | <span data-ttu-id="2cfc0-181">Bir [Cartlineıtem](cart-resources.md#cartlineitem) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-181">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="2cfc0-182">Bu tablo, istek gövdesinde [Cartlineıtem](cart-resources.md#cartlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-182">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="2cfc0-183">Özellik</span><span class="sxs-lookup"><span data-stu-id="2cfc0-183">Property</span></span>             | <span data-ttu-id="2cfc0-184">Tür</span><span class="sxs-lookup"><span data-stu-id="2cfc0-184">Type</span></span>                             | <span data-ttu-id="2cfc0-185">Description</span><span class="sxs-lookup"><span data-stu-id="2cfc0-185">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2cfc0-186">kimlik</span><span class="sxs-lookup"><span data-stu-id="2cfc0-186">id</span></span>                   | <span data-ttu-id="2cfc0-187">string</span><span class="sxs-lookup"><span data-stu-id="2cfc0-187">string</span></span>                           | <span data-ttu-id="2cfc0-188">Sepet çizgisi öğesi için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-188">A unique identifier for a cart line item.</span></span> <span data-ttu-id="2cfc0-189">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-189">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="2cfc0-190">catalogId</span><span class="sxs-lookup"><span data-stu-id="2cfc0-190">catalogId</span></span>            | <span data-ttu-id="2cfc0-191">string</span><span class="sxs-lookup"><span data-stu-id="2cfc0-191">string</span></span>                           | <span data-ttu-id="2cfc0-192">Katalog öğesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-192">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="2cfc0-193">friendlyName</span><span class="sxs-lookup"><span data-stu-id="2cfc0-193">friendlyName</span></span>         | <span data-ttu-id="2cfc0-194">string</span><span class="sxs-lookup"><span data-stu-id="2cfc0-194">string</span></span>                           | <span data-ttu-id="2cfc0-195">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-195">Optional.</span></span> <span data-ttu-id="2cfc0-196">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="2cfc0-197">miktar</span><span class="sxs-lookup"><span data-stu-id="2cfc0-197">quantity</span></span>             | <span data-ttu-id="2cfc0-198">int</span><span class="sxs-lookup"><span data-stu-id="2cfc0-198">int</span></span>                              | <span data-ttu-id="2cfc0-199">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-199">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="2cfc0-200">currencyCode</span><span class="sxs-lookup"><span data-stu-id="2cfc0-200">currencyCode</span></span>         | <span data-ttu-id="2cfc0-201">string</span><span class="sxs-lookup"><span data-stu-id="2cfc0-201">string</span></span>                           | <span data-ttu-id="2cfc0-202">Para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-202">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="2cfc0-203">Bilimlingcycle</span><span class="sxs-lookup"><span data-stu-id="2cfc0-203">billingCycle</span></span>         | <span data-ttu-id="2cfc0-204">Nesne</span><span class="sxs-lookup"><span data-stu-id="2cfc0-204">Object</span></span>                           | <span data-ttu-id="2cfc0-205">Geçerli dönem için ayarlanan faturalandırma dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-205">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="2cfc0-206">Katılımcılar</span><span class="sxs-lookup"><span data-stu-id="2cfc0-206">participants</span></span>         | <span data-ttu-id="2cfc0-207">Nesne dizesi çiftlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="2cfc0-207">List of Object String pairs</span></span>      | <span data-ttu-id="2cfc0-208">Satınalmada iş ortağı kimliği koleksiyonu (MPNıD).</span><span class="sxs-lookup"><span data-stu-id="2cfc0-208">A collection of PartnerId on Record (MPNID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="2cfc0-209">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="2cfc0-209">provisioningContext</span></span>  | <span data-ttu-id="2cfc0-210">Sözlük<dize, dize></span><span class="sxs-lookup"><span data-stu-id="2cfc0-210">Dictionary<string, string></span></span>       | <span data-ttu-id="2cfc0-211">Teklifin sağlanması için kullanılan bir bağlam.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-211">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="2cfc0-212">orderGroup</span><span class="sxs-lookup"><span data-stu-id="2cfc0-212">orderGroup</span></span>           | <span data-ttu-id="2cfc0-213">string</span><span class="sxs-lookup"><span data-stu-id="2cfc0-213">string</span></span>                           | <span data-ttu-id="2cfc0-214">Hangi öğelerin birlikte yerleştirilebileceğini belirten bir grup.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-214">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="2cfc0-215">Addonıtems</span><span class="sxs-lookup"><span data-stu-id="2cfc0-215">addonItems</span></span>           | <span data-ttu-id="2cfc0-216">**Cartlineıtem** nesnelerinin listesi</span><span class="sxs-lookup"><span data-stu-id="2cfc0-216">List of **CartLineItem** objects</span></span> | <span data-ttu-id="2cfc0-217">Ana sepet çizgisi öğesinin satın alma işleminden kaynaklanan temel aboneliğe yönelik olarak satın alınacak eklentiler için sepet çizgisi öğeleri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-217">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="2cfc0-218">error</span><span class="sxs-lookup"><span data-stu-id="2cfc0-218">error</span></span>                | <span data-ttu-id="2cfc0-219">Nesne</span><span class="sxs-lookup"><span data-stu-id="2cfc0-219">Object</span></span>                           | <span data-ttu-id="2cfc0-220">Bir hata durumunda sepet oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-220">Applied after cart is created in case of an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="2cfc0-221">İstek örneği (yeni temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="2cfc0-221">Request example (new base subscription)</span></span>

<span data-ttu-id="2cfc0-222">Aşağıdaki REST örneği, yeni bir temel abonelik için eklenti öğelerine sahip bir sepet oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-222">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="2cfc0-223">İstek örneği (varolan temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="2cfc0-223">Request example (existing base subscription)</span></span>

<span data-ttu-id="2cfc0-224">Aşağıdaki REST örneği, mevcut bir temel aboneliğe eklentilerin nasıl ekleneceğini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-224">The following REST example show how to append add-ons to an existing base subscription.</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="2cfc0-225">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2cfc0-225">REST response</span></span>

<span data-ttu-id="2cfc0-226">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [sepet](cart-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-226">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="2cfc0-227">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2cfc0-227">Response success and error codes</span></span>

<span data-ttu-id="2cfc0-228">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-228">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2cfc0-229">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2cfc0-229">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2cfc0-230">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2cfc0-230">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="2cfc0-231">Yanıt örneği (yeni temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="2cfc0-231">Response example (new base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="2cfc0-232">Yanıt örneği (varolan temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="2cfc0-232">Response example (existing base subscription)</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
