---
title: Katalog öğeleri satın alma
description: Iş Ortağı Merkezi API 'sini kullanarak katalog öğeleri satın alma.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f2b3a34cdb6b29cb7eaaf5d977e4588f538fff09
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768884"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="7e543-103">Katalog öğeleri satın alma</span><span class="sxs-lookup"><span data-stu-id="7e543-103">Purchase catalog items</span></span>

<span data-ttu-id="7e543-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="7e543-104">**Applies To**</span></span>

- <span data-ttu-id="7e543-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7e543-105">Partner Center</span></span>

<span data-ttu-id="7e543-106">Aşağıdaki senaryoda, Iş Ortağı Merkezi API 'sini kullanarak katalogdan öğe satın alma genel işlemi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7e543-106">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="7e543-107">Bulma</span><span class="sxs-lookup"><span data-stu-id="7e543-107">Discovery</span></span>

<span data-ttu-id="7e543-108">Ürünler ve SKU 'Lar ' ı seçin ve aşağıdaki Iş Ortağı Merkezi API modellerini kullanarak kullanılabilirliğini kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="7e543-108">Select products and SKUs and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="7e543-109">[Ürün](product-resources.md#product) -satın alınabilir alınırken malları veya hizmetleri için gruplama yapısı.</span><span class="sxs-lookup"><span data-stu-id="7e543-109">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="7e543-110">Bir ürünün kendisi bir satın alınabilir alınırken öğesi değil.</span><span class="sxs-lookup"><span data-stu-id="7e543-110">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="7e543-111">[SKU](product-resources.md#sku) -bir ürün altında bir satın alınabilir alınırken stok tutma BIRIMI (SKU).</span><span class="sxs-lookup"><span data-stu-id="7e543-111">[SKU](product-resources.md#sku) - A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="7e543-112">Bunlar, ürünün farklı şekillerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="7e543-112">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="7e543-113">[Kullanılabilirlik](product-resources.md#availability) -BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi ve sektör segmenti gibi).</span><span class="sxs-lookup"><span data-stu-id="7e543-113">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency and industry segment).</span></span>

<span data-ttu-id="7e543-114">Katalogdan bir öğe satın almak için aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7e543-114">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="7e543-115">Satın almak istediğiniz ürün ve SKU 'YU belirleyip alın.</span><span class="sxs-lookup"><span data-stu-id="7e543-115">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="7e543-116">Ürünlerin bir listesini alın</span><span class="sxs-lookup"><span data-stu-id="7e543-116">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="7e543-117">Ürün KIMLIĞINI kullanarak bir ürün alın</span><span class="sxs-lookup"><span data-stu-id="7e543-117">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="7e543-118">Ürün için SKU 'ların listesini alın</span><span class="sxs-lookup"><span data-stu-id="7e543-118">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="7e543-119">SKU KIMLIĞI kullanarak bir SKU al</span><span class="sxs-lookup"><span data-stu-id="7e543-119">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="7e543-120">Bir SKU için envanteri denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7e543-120">Check the inventory for a SKU.</span></span> <span data-ttu-id="7e543-121">Bu adım yalnızca [purchasePrerequisites](product-resources.md#sku) özelliğindeki bir **ınventorycheck** değeri ile etiketlenmiş SKU 'lar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="7e543-121">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="7e543-122">Envanter denetleme</span><span class="sxs-lookup"><span data-stu-id="7e543-122">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="7e543-123">[SKU](product-resources.md#sku)için [kullanılabilirliği](product-resources.md#availability) alın.</span><span class="sxs-lookup"><span data-stu-id="7e543-123">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="7e543-124">Siparişi yerleştirirken kullanılabilirliğin **Catalogıtemıd** öğesine ihtiyacınız olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7e543-124">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="7e543-125">Bu değeri almak için aşağıdaki API 'lerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="7e543-125">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="7e543-126">SKU 'nun kullanılabilirliği listesini alın</span><span class="sxs-lookup"><span data-stu-id="7e543-126">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="7e543-127">Kullanılabilirlik KIMLIĞINI kullanarak bir kullanılabilirlik alın</span><span class="sxs-lookup"><span data-stu-id="7e543-127">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="7e543-128">Sipariş gönderimi</span><span class="sxs-lookup"><span data-stu-id="7e543-128">Order submission</span></span>

<span data-ttu-id="7e543-129">Katalog öğesi siparişinizi göndermek için aşağıdakileri yapın:</span><span class="sxs-lookup"><span data-stu-id="7e543-129">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="7e543-130">Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için bir [sepet](cart-resources.md) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7e543-130">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="7e543-131">Bir sepet oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="7e543-131">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="7e543-132">Alışveriş sepeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e543-132">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="7e543-133">Bir alışveriş sepetini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7e543-133">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="7e543-134">Sepete göz atın.</span><span class="sxs-lookup"><span data-stu-id="7e543-134">Check out the cart.</span></span> <span data-ttu-id="7e543-135">Sepetin kullanıma hazır olması, bir [sipariş](order-resources.md)oluşturulmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="7e543-135">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="7e543-136">Sepetini kullanıma alın</span><span class="sxs-lookup"><span data-stu-id="7e543-136">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="7e543-137">Sipariş ayrıntılarını al</span><span class="sxs-lookup"><span data-stu-id="7e543-137">Get order details</span></span>

<span data-ttu-id="7e543-138">Sipariş KIMLIĞINI kullanarak tek bir siparişin ayrıntılarını alabilir veya bir müşteri siparişlerinin listesini alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e543-138">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="7e543-139">Bir siparişin gönderildiği ve müşterinin siparişlerinin listesinde görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="7e543-139">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="7e543-140">Sipariş kimliklerini kullanarak tek bir siparişin ayrıntılarını almak için bkz. [order by ID Get](get-an-order-by-id.md) .</span><span class="sxs-lookup"><span data-stu-id="7e543-140">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="7e543-141">Müşteri KIMLIĞINI kullanarak müşterinin siparişlerinin listesini almak için [müşterinin siparişlerinin tümünü alın](get-all-of-a-customer-s-orders.md) konusuna bakın.</span><span class="sxs-lookup"><span data-stu-id="7e543-141">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="7e543-142">Bir müşteri siparişlerinin listesini almak için bkz. [müşteri ve faturalandırma](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) döngüsüne göre siparişlerin listesini almak için, katalog öğesi siparişlerini (tek seferlik ücretler) ve yıllık veya aylık faturalandırılan siparişleri ayrı olarak [listelemenize olanak](product-resources.md#billingcycletype) tanır.</span><span class="sxs-lookup"><span data-stu-id="7e543-142">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="7e543-143">Yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="7e543-143">Lifecycle management</span></span>

<span data-ttu-id="7e543-144">Iş Ortağı Merkezi 'nde Katalog öğelerinizin yaşam döngüsünü yönetmenin bir parçası olarak, katalog öğesi [yetkilendirmelerinizin](entitlement-resources.md)bilgilerini alabilir ve rezervasyon siparişi kimliğini kullanarak rezervasyon ayrıntılarını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e543-144">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="7e543-145">Bunun nasıl yapılacağı hakkında örnekler için bkz. [yetkilendirmeleri alma](get-a-collection-of-entitlements.md).</span><span class="sxs-lookup"><span data-stu-id="7e543-145">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="7e543-146">Fatura ve mutabakat</span><span class="sxs-lookup"><span data-stu-id="7e543-146">Invoice and reconciliation</span></span>

<span data-ttu-id="7e543-147">Aşağıdaki senaryolarda, müşterinizin [faturalarını](invoice-resources.md)programlamayla görüntüleme ve katalog öğeleri için tek seferlik ücretler içeren Hesap bakiyeleriniz ve özetler alma işlemlerinin nasıl yapılacağı gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7e543-147">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="7e543-148">Bakiye ve ödeme</span><span class="sxs-lookup"><span data-stu-id="7e543-148">Balance and payment</span></span>

<span data-ttu-id="7e543-149">Hem yinelenen hem de tek seferlik (katalog öğesi) ücretlerine ait bir bakiye olan varsayılan para birimi türünde güncel hesap bakiyesini almak için, bkz. [geçerli hesap bakiyenizi alın](get-the-reseller-s-current-account-balance.md).</span><span class="sxs-lookup"><span data-stu-id="7e543-149">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="7e543-150">Çoklu para birimi bakiyesi ve ödemesi</span><span class="sxs-lookup"><span data-stu-id="7e543-150">Multi-currency balance and payment</span></span>

<span data-ttu-id="7e543-151">Geçerli hesap bakiyenizi ve müşterinizin para birimi türlerinden her biri için hem yinelenen hem de tek seferlik ücretler içeren bir fatura Özeti içeren bir fatura özetleri koleksiyonu ve bir fatura Özeti koleksiyonu almak için bkz. [Fatura özetlerini al](get-invoice-summaries.md).</span><span class="sxs-lookup"><span data-stu-id="7e543-151">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="7e543-152">Faturalar</span><span class="sxs-lookup"><span data-stu-id="7e543-152">Invoices</span></span>

<span data-ttu-id="7e543-153">Yinelenen ve tek seferlik ücretleri gösteren faturaların bir koleksiyonunu almak için, bkz. [faturaların toplanmasını edinme](get-a-collection-of-invoices.md).</span><span class="sxs-lookup"><span data-stu-id="7e543-153">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="7e543-154">Tek fatura</span><span class="sxs-lookup"><span data-stu-id="7e543-154">Single Invoice</span></span>

<span data-ttu-id="7e543-155">Fatura KIMLIĞINI kullanarak belirli bir faturayı almak için bkz. [kimliğe göre fatura alma](get-invoice-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="7e543-155">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="7e543-156">Katına</span><span class="sxs-lookup"><span data-stu-id="7e543-156">Reconciliation</span></span>

<span data-ttu-id="7e543-157">Belirli bir fatura KIMLIĞI için fatura satırı öğe ayrıntılarının (mutabakat satır öğeleri) bir koleksiyonunu almak için bkz. [fatura satırı öğelerini Al](get-invoiceline-items.md).</span><span class="sxs-lookup"><span data-stu-id="7e543-157">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="7e543-158">Bir faturayı PDF olarak indirme</span><span class="sxs-lookup"><span data-stu-id="7e543-158">Download an invoice as a PDF</span></span>

<span data-ttu-id="7e543-159">Fatura KIMLIĞI kullanarak PDF formundaki fatura ekstresini almak için bkz. [Fatura alma ekstresi](get-invoice-statement.md).</span><span class="sxs-lookup"><span data-stu-id="7e543-159">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
