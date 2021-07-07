---
title: Eklentilerle bir sepet oluşturma
description: Bir sepet aracılığıyla eklentilere bir müşteri siparişi eklemek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makalesinde, eklentilerle bir sepet oluşturmak için önkoşulları ve adımları paylaşır.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 513a9607b9194c36253630c91de9622325317c3a
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973766"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a><span data-ttu-id="7802e-104">Eklentiler ile müşteri siparişi arasında bir sepet oluşturma</span><span class="sxs-lookup"><span data-stu-id="7802e-104">Create a cart with add-ons to a customer order</span></span>

<span data-ttu-id="7802e-105">Eklentileri bir sepet aracılığıyla satın alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7802e-105">You can purchase add-ons through a cart.</span></span> <span data-ttu-id="7802e-106">şu anda satım için kullanılabilir olanlar hakkında daha fazla bilgi için [Bulut Çözümü Sağlayıcısı programındaki iş ortağı teklifleri](/partner-center/csp-offers)konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="7802e-106">For more information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7802e-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7802e-107">Prerequisites</span></span>

- <span data-ttu-id="7802e-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7802e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7802e-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7802e-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7802e-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7802e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7802e-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7802e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7802e-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7802e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7802e-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7802e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7802e-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="7802e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7802e-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="7802e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7802e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="7802e-116">C\#</span></span>

<span data-ttu-id="7802e-117">Bir sepet, temel teklifin ve bunlara karşılık gelen eklentilerin satın alınmasını sağlar.</span><span class="sxs-lookup"><span data-stu-id="7802e-117">A cart enables the purchase of a base offer and its corresponding add-ons.</span></span> <span data-ttu-id="7802e-118">Bir sepet oluşturmak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7802e-118">Follow these steps to create a cart:</span></span>

1. <span data-ttu-id="7802e-119">Bir [**sepet**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7802e-119">Instantiate a [**Cart**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) object.</span></span>

2. <span data-ttu-id="7802e-120">Taban teklifleri temsil eden [**Cartlineıtem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) nesnelerinin bir listesini oluşturun ve listeyi sepetinin [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) özelliğine atayın.</span><span class="sxs-lookup"><span data-stu-id="7802e-120">Create a list of [**CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) objects that represent the base offer(s), and assign the list to the cart's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) property.</span></span>

3. <span data-ttu-id="7802e-121">Her temel teklifin sepet çizgisi öğesi altında, **Addonıtems** listesini her biri temel teklifte satın alınacak eklentiyi temsil eden diğer **Cartlineıtem** nesneleriyle doldurun.</span><span class="sxs-lookup"><span data-stu-id="7802e-121">Under each base offer's cart line item, populate the list of **AddOnItems** with other **CartLineItem** objects that each represent an add-on that will be purchased against that base offer.</span></span>

4. <span data-ttu-id="7802e-122">[**Iaggregatepartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) kullanarak, müşteriyi tanımlamak üzere [**ıustomercollection. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırmak ve sonra da bu arabirimi **sepet** özelliğinden almak için bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="7802e-122">Obtain an interface to cart operations by using [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) to call the [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and then retrieving the interface from the **Cart** property.</span></span>

5. <span data-ttu-id="7802e-123">Son olarak, sepet oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="7802e-123">Finally, call the [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) method to create the cart.</span></span>

### <a name="c-example"></a><span data-ttu-id="7802e-124">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="7802e-124">C\# example</span></span>

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

<span data-ttu-id="7802e-125">Eklentilerin mevcut temel abonelikler için satın alınmasını sağlayacak bir sepet oluşturmak için bu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7802e-125">Follow these steps to create a cart that will enable the purchase of add-on(s) against existing base subscription(s):</span></span>

1. <span data-ttu-id="7802e-126">"Parentsubscriptionıd" anahtarıyla **Provisioningcontext** ÖZELLIĞINDEKI abonelik kimliğini içeren yeni bir **Cartlineıtem** içeren bir **sepet** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7802e-126">Create a **Cart** with a new **CartLineItem** containing the subscription ID in the **ProvisioningContext** property with key "ParentSubscriptionId".</span></span>

2. <span data-ttu-id="7802e-127">**Create** veya **createasync** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="7802e-127">Call the **Create** or **CreateAsync** method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="7802e-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7802e-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7802e-129">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7802e-129">Request syntax</span></span>

| <span data-ttu-id="7802e-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7802e-130">Method</span></span>   | <span data-ttu-id="7802e-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7802e-131">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7802e-132">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="7802e-132">**POST**</span></span> | <span data-ttu-id="7802e-133">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts http/1.1</span><span class="sxs-lookup"><span data-stu-id="7802e-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1</span></span>                        |

#### <a name="uri-parameter"></a><span data-ttu-id="7802e-134">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="7802e-134">URI parameter</span></span>

<span data-ttu-id="7802e-135">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7802e-135">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="7802e-136">Ad</span><span class="sxs-lookup"><span data-stu-id="7802e-136">Name</span></span>            | <span data-ttu-id="7802e-137">Tür</span><span class="sxs-lookup"><span data-stu-id="7802e-137">Type</span></span>     | <span data-ttu-id="7802e-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7802e-138">Required</span></span> | <span data-ttu-id="7802e-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7802e-139">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="7802e-140">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="7802e-140">**customer-id**</span></span> | <span data-ttu-id="7802e-141">string</span><span class="sxs-lookup"><span data-stu-id="7802e-141">string</span></span>   | <span data-ttu-id="7802e-142">Yes</span><span class="sxs-lookup"><span data-stu-id="7802e-142">Yes</span></span>      | <span data-ttu-id="7802e-143">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="7802e-143">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="7802e-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7802e-144">Request headers</span></span>

<span data-ttu-id="7802e-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7802e-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7802e-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7802e-146">Request body</span></span>

<span data-ttu-id="7802e-147">Bu tablo, istek gövdesinde [sepet](cart-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="7802e-147">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="7802e-148">Özellik</span><span class="sxs-lookup"><span data-stu-id="7802e-148">Property</span></span>              | <span data-ttu-id="7802e-149">Tür</span><span class="sxs-lookup"><span data-stu-id="7802e-149">Type</span></span>             | <span data-ttu-id="7802e-150">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7802e-150">Required</span></span>        | <span data-ttu-id="7802e-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7802e-151">Description</span></span> |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7802e-152">kimlik</span><span class="sxs-lookup"><span data-stu-id="7802e-152">id</span></span>                    | <span data-ttu-id="7802e-153">dize</span><span class="sxs-lookup"><span data-stu-id="7802e-153">string</span></span>           | <span data-ttu-id="7802e-154">No</span><span class="sxs-lookup"><span data-stu-id="7802e-154">No</span></span>              | <span data-ttu-id="7802e-155">Sepet başarıyla oluşturulduktan sonra sağlanan bir sepet tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7802e-155">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="7802e-156">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="7802e-156">creationTimeStamp</span></span>     | <span data-ttu-id="7802e-157">DateTime</span><span class="sxs-lookup"><span data-stu-id="7802e-157">DateTime</span></span>         | <span data-ttu-id="7802e-158">Hayır</span><span class="sxs-lookup"><span data-stu-id="7802e-158">No</span></span>              | <span data-ttu-id="7802e-159">Sepetin oluşturulduğu tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="7802e-159">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="7802e-160">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="7802e-160">Applied upon successful creation of the cart.</span></span>         |
| <span data-ttu-id="7802e-161">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="7802e-161">lastModifiedTimeStamp</span></span> | <span data-ttu-id="7802e-162">DateTime</span><span class="sxs-lookup"><span data-stu-id="7802e-162">DateTime</span></span>         | <span data-ttu-id="7802e-163">Hayır</span><span class="sxs-lookup"><span data-stu-id="7802e-163">No</span></span>              | <span data-ttu-id="7802e-164">Sepetin son güncelleştirildiği tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="7802e-164">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="7802e-165">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="7802e-165">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="7802e-166">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="7802e-166">expirationTimeStamp</span></span>   | <span data-ttu-id="7802e-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="7802e-167">DateTime</span></span>         | <span data-ttu-id="7802e-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="7802e-168">No</span></span>              | <span data-ttu-id="7802e-169">Sepetin süresinin dolacağı tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="7802e-169">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="7802e-170">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="7802e-170">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="7802e-171">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="7802e-171">lastModifiedUser</span></span>      | <span data-ttu-id="7802e-172">dize</span><span class="sxs-lookup"><span data-stu-id="7802e-172">string</span></span>           | <span data-ttu-id="7802e-173">No</span><span class="sxs-lookup"><span data-stu-id="7802e-173">No</span></span>              | <span data-ttu-id="7802e-174">Sepetini son güncelleştiren Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="7802e-174">The user who last updated the cart.</span></span> <span data-ttu-id="7802e-175">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="7802e-175">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="7802e-176">LineItems</span><span class="sxs-lookup"><span data-stu-id="7802e-176">lineItems</span></span>             | <span data-ttu-id="7802e-177">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="7802e-177">Array of objects</span></span> | <span data-ttu-id="7802e-178">Yes</span><span class="sxs-lookup"><span data-stu-id="7802e-178">Yes</span></span>             | <span data-ttu-id="7802e-179">Bir [Cartlineıtem](cart-resources.md#cartlineitem) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="7802e-179">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                             |

<span data-ttu-id="7802e-180">Bu tablo, istek gövdesinde [Cartlineıtem](cart-resources.md#cartlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="7802e-180">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="7802e-181">Özellik</span><span class="sxs-lookup"><span data-stu-id="7802e-181">Property</span></span>             | <span data-ttu-id="7802e-182">Tür</span><span class="sxs-lookup"><span data-stu-id="7802e-182">Type</span></span>                             | <span data-ttu-id="7802e-183">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7802e-183">Description</span></span>                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7802e-184">kimlik</span><span class="sxs-lookup"><span data-stu-id="7802e-184">id</span></span>                   | <span data-ttu-id="7802e-185">string</span><span class="sxs-lookup"><span data-stu-id="7802e-185">string</span></span>                           | <span data-ttu-id="7802e-186">Sepet çizgisi öğesi için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="7802e-186">A unique identifier for a cart line item.</span></span> <span data-ttu-id="7802e-187">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="7802e-187">Applied upon successful creation of cart.</span></span>                                                                   |
| <span data-ttu-id="7802e-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="7802e-188">catalogId</span></span>            | <span data-ttu-id="7802e-189">string</span><span class="sxs-lookup"><span data-stu-id="7802e-189">string</span></span>                           | <span data-ttu-id="7802e-190">Katalog öğesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7802e-190">The catalog item identifier.</span></span>                                                                                                                          |
| <span data-ttu-id="7802e-191">friendlyName</span><span class="sxs-lookup"><span data-stu-id="7802e-191">friendlyName</span></span>         | <span data-ttu-id="7802e-192">string</span><span class="sxs-lookup"><span data-stu-id="7802e-192">string</span></span>                           | <span data-ttu-id="7802e-193">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="7802e-193">Optional.</span></span> <span data-ttu-id="7802e-194">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="7802e-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>                                                                 |
| <span data-ttu-id="7802e-195">miktar</span><span class="sxs-lookup"><span data-stu-id="7802e-195">quantity</span></span>             | <span data-ttu-id="7802e-196">int</span><span class="sxs-lookup"><span data-stu-id="7802e-196">int</span></span>                              | <span data-ttu-id="7802e-197">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="7802e-197">The number of licenses or instances.</span></span>                                                                                                                  |
| <span data-ttu-id="7802e-198">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7802e-198">currencyCode</span></span>         | <span data-ttu-id="7802e-199">string</span><span class="sxs-lookup"><span data-stu-id="7802e-199">string</span></span>                           | <span data-ttu-id="7802e-200">Para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="7802e-200">The currency code.</span></span>                                                                                                                                    |
| <span data-ttu-id="7802e-201">billingCycle</span><span class="sxs-lookup"><span data-stu-id="7802e-201">billingCycle</span></span>         | <span data-ttu-id="7802e-202">Nesne</span><span class="sxs-lookup"><span data-stu-id="7802e-202">Object</span></span>                           | <span data-ttu-id="7802e-203">Geçerli dönem için ayarlanmış faturalama dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="7802e-203">The type of billing cycle set for the current period.</span></span>                                                                                                 |
| <span data-ttu-id="7802e-204">Katılımcılar</span><span class="sxs-lookup"><span data-stu-id="7802e-204">participants</span></span>         | <span data-ttu-id="7802e-205">Nesne Dizesi çiftlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="7802e-205">List of Object String pairs</span></span>      | <span data-ttu-id="7802e-206">Satın almada Kayıtta PartnerId (MPN KIMLIĞI) koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="7802e-206">A collection of PartnerId on Record (MPN ID) on the purchase.</span></span>                                                                                          |
| <span data-ttu-id="7802e-207">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="7802e-207">provisioningContext</span></span>  | <span data-ttu-id="7802e-208">Sözlük<dizesi, dize></span><span class="sxs-lookup"><span data-stu-id="7802e-208">Dictionary<string, string></span></span>       | <span data-ttu-id="7802e-209">Teklifin sağlanması için kullanılan bağlam.</span><span class="sxs-lookup"><span data-stu-id="7802e-209">A context used for provisioning of offer.</span></span>                                                                                                             |
| <span data-ttu-id="7802e-210">orderGroup</span><span class="sxs-lookup"><span data-stu-id="7802e-210">orderGroup</span></span>           | <span data-ttu-id="7802e-211">string</span><span class="sxs-lookup"><span data-stu-id="7802e-211">string</span></span>                           | <span data-ttu-id="7802e-212">Hangi öğelerin bir araya yerleştiril olduğunu belirten bir grup.</span><span class="sxs-lookup"><span data-stu-id="7802e-212">A group to indicate which items can be placed together.</span></span>                                                                                               |
| <span data-ttu-id="7802e-213">addonItems</span><span class="sxs-lookup"><span data-stu-id="7802e-213">addonItems</span></span>           | <span data-ttu-id="7802e-214">**CartLineItem nesnelerinin** listesi</span><span class="sxs-lookup"><span data-stu-id="7802e-214">List of **CartLineItem** objects</span></span> | <span data-ttu-id="7802e-215">Üst sepet satır öğesinin satın alımından sonuç olarak temel aboneliğe doğru satın alınacak eklentiler için sepet satırı öğeleri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="7802e-215">A collection of cart line items for add-ons that will be purchased towards the base subscription that results from the parent cart line item's purchase.</span></span> |
| <span data-ttu-id="7802e-216">error</span><span class="sxs-lookup"><span data-stu-id="7802e-216">error</span></span>                | <span data-ttu-id="7802e-217">Nesne</span><span class="sxs-lookup"><span data-stu-id="7802e-217">Object</span></span>                           | <span data-ttu-id="7802e-218">Bir hata varsa sepet oluşturulduktan sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7802e-218">Applied after cart is created if there is an error.</span></span>                                                                                                    |

### <a name="request-example-new-base-subscription"></a><span data-ttu-id="7802e-219">İstek örneği (yeni temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="7802e-219">Request example (new base subscription)</span></span>

<span data-ttu-id="7802e-220">Aşağıdaki REST örneği, yeni bir temel abonelik için eklenti öğeleriyle bir sepet oluşturmayı gösterir.</span><span class="sxs-lookup"><span data-stu-id="7802e-220">The following REST example shows how to create a cart with add-on items for a new base subscription.</span></span>

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

#### <a name="request-example-existing-base-subscription"></a><span data-ttu-id="7802e-221">İstek örneği (mevcut temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="7802e-221">Request example (existing base subscription)</span></span>

<span data-ttu-id="7802e-222">Aşağıdaki REST örneği, mevcut bir temel aboneliğe eklenti eklemeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="7802e-222">The following REST example shows how to append add-ons to an existing base subscription.</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="7802e-223">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7802e-223">REST response</span></span>

<span data-ttu-id="7802e-224">Başarılı olursa, bu yöntem yanıt [gövdesinde](cart-resources.md) doldurulmuş Sepet kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="7802e-224">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="7802e-225">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7802e-225">Response success and error codes</span></span>

<span data-ttu-id="7802e-226">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="7802e-226">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7802e-227">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7802e-227">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7802e-228">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7802e-228">For the full list, see [Error Codes](error-codes.md).</span></span>

#### <a name="response-example-new-base-subscription"></a><span data-ttu-id="7802e-229">Yanıt örneği (yeni temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="7802e-229">Response example (new base subscription)</span></span>

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

#### <a name="response-example-existing-base-subscription"></a><span data-ttu-id="7802e-230">Yanıt örneği (mevcut temel abonelik)</span><span class="sxs-lookup"><span data-stu-id="7802e-230">Response example (existing base subscription)</span></span>

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
