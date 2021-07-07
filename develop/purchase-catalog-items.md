---
title: Katalog öğeleri satın alma
description: İş Ortağı Merkezi API'sini kullanarak katalog İş Ortağı Merkezi satın alma.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d3e0deedff194b1c836d9266c2201a2b3a52cc1b
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445366"
---
# <a name="purchase-catalog-items"></a><span data-ttu-id="27ea3-103">Katalog öğeleri satın alma</span><span class="sxs-lookup"><span data-stu-id="27ea3-103">Purchase catalog items</span></span>

<span data-ttu-id="27ea3-104">Aşağıdaki senaryo, İş Ortağı Merkezi API'sini kullanarak katalogdan ürün satın alma işlemini gösterir.</span><span class="sxs-lookup"><span data-stu-id="27ea3-104">The following scenario demonstrates the generic process for purchasing items from the catalog by using the Partner Center API.</span></span>

## <a name="discovery"></a><span data-ttu-id="27ea3-105">Bulma</span><span class="sxs-lookup"><span data-stu-id="27ea3-105">Discovery</span></span>

<span data-ttu-id="27ea3-106">Ürünleri ve Stok Tutma Birimlerini (SKU) seçin ve api modellerinde aşağıdaki İş Ortağı Merkezi kullanılabilirliklerini kontrol edin:</span><span class="sxs-lookup"><span data-stu-id="27ea3-106">Select products and Stock Keeping Units (SKUs) and check their availability using the following Partner Center API models:</span></span>

- <span data-ttu-id="27ea3-107">[Ürün](product-resources.md#product) - Satınlanabilir ürünler veya hizmetler için bir gruplama yapısı.</span><span class="sxs-lookup"><span data-stu-id="27ea3-107">[Product](product-resources.md#product) - A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="27ea3-108">Tek başına ürün, satın edilebilir bir öğe değildir.</span><span class="sxs-lookup"><span data-stu-id="27ea3-108">A product by itself isn't a purchasable item.</span></span>
- <span data-ttu-id="27ea3-109">[SKU](product-resources.md#sku) - Ürün altında satınlanabilir bir SKU.</span><span class="sxs-lookup"><span data-stu-id="27ea3-109">[SKU](product-resources.md#sku) - A purchasable SKU under a product.</span></span> <span data-ttu-id="27ea3-110">Bunlar ürünün farklı şekillerini temsil ediyor.</span><span class="sxs-lookup"><span data-stu-id="27ea3-110">These represent the different shapes of the product.</span></span>
- <span data-ttu-id="27ea3-111">[Kullanılabilirlik:](product-resources.md#availability) SKU'nun satın alına hazır olduğu yapılandırma (ülke, para birimi ve sektör segmenti gibi).</span><span class="sxs-lookup"><span data-stu-id="27ea3-111">[Availability](product-resources.md#availability) - A configuration in which a SKU is available for purchase (such as country, currency, and industry segment).</span></span>

<span data-ttu-id="27ea3-112">Katalogdan bir öğe satın almak için aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="27ea3-112">To purchase an item from the catalog, complete the following steps:</span></span>

1. <span data-ttu-id="27ea3-113">Satın almak istediğiniz Ürün ve SKU'ları belirleyin ve alın.</span><span class="sxs-lookup"><span data-stu-id="27ea3-113">Identify and retrieve the Product and SKU that you want to purchase.</span></span>

   - [<span data-ttu-id="27ea3-114">Ürünlerin listesini al</span><span class="sxs-lookup"><span data-stu-id="27ea3-114">Get a list of products</span></span>](get-a-list-of-products.md)
   - [<span data-ttu-id="27ea3-115">Ürün kimliğini kullanarak ürün al</span><span class="sxs-lookup"><span data-stu-id="27ea3-115">Get a product using the product ID</span></span>](get-a-product-by-id.md)
   - [<span data-ttu-id="27ea3-116">Bir ürün için SKUS listesini al</span><span class="sxs-lookup"><span data-stu-id="27ea3-116">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
   - [<span data-ttu-id="27ea3-117">SKU Kimliğini kullanarak SKU'ya sahip olmak</span><span class="sxs-lookup"><span data-stu-id="27ea3-117">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

2. <span data-ttu-id="27ea3-118">SKU envanterini denetleme.</span><span class="sxs-lookup"><span data-stu-id="27ea3-118">Check the inventory for a SKU.</span></span> <span data-ttu-id="27ea3-119">Bu adım yalnızca [purchasePrerequisites](product-resources.md#sku) özelliğinde **InventoryCheck** değeriyle etiketlenen SKU'lar için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="27ea3-119">This step is only needed for SKUs that are tagged with an **InventoryCheck** value in the [purchasePrerequisites](product-resources.md#sku) property.</span></span>

   - [<span data-ttu-id="27ea3-120">Envanter denetleme</span><span class="sxs-lookup"><span data-stu-id="27ea3-120">Check Inventory</span></span>](check-inventory.md)

3. <span data-ttu-id="27ea3-121">SKU [için](product-resources.md#availability) [kullanılabilirliği alın.](product-resources.md#sku)</span><span class="sxs-lookup"><span data-stu-id="27ea3-121">Retrieve the [availability](product-resources.md#availability) for the [SKU](product-resources.md#sku).</span></span> <span data-ttu-id="27ea3-122">Siparişi sağlarken **kullanılabilirlik CatalogItemId'ye** ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="27ea3-122">You will need the **CatalogItemId** of the availability when placing the order.</span></span> <span data-ttu-id="27ea3-123">Bu değeri almak için aşağıdaki API'lerden birini kullanın:</span><span class="sxs-lookup"><span data-stu-id="27ea3-123">To get this value, use one of the following APIs:</span></span>

   - [<span data-ttu-id="27ea3-124">SKU için kullanılabilirlik listesini al</span><span class="sxs-lookup"><span data-stu-id="27ea3-124">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
   - [<span data-ttu-id="27ea3-125">Kullanılabilirlik kimliğini kullanarak kullanılabilirlik elde edin</span><span class="sxs-lookup"><span data-stu-id="27ea3-125">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="order-submission"></a><span data-ttu-id="27ea3-126">Sipariş gönderimi</span><span class="sxs-lookup"><span data-stu-id="27ea3-126">Order submission</span></span>

<span data-ttu-id="27ea3-127">Katalog öğesi siparişinizi göndermek için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="27ea3-127">To submit your catalog item order, do the following:</span></span>

1. <span data-ttu-id="27ea3-128">Satın almayı [istediğiniz](cart-resources.md) katalog öğelerinin koleksiyonunu tutmak için bir Sepet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="27ea3-128">Create a [Cart](cart-resources.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="27ea3-129">Bir sepet oluşturma sırasında, [sepet satır öğeleri](cart-resources.md#cartlineitem) aynı Sipariş içinde birlikte satın alınarak nelerin satın alınarak otomatik olarak [gruplanır.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-129">When you create a cart, the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="27ea3-130">Alışveriş sepeti oluşturma</span><span class="sxs-lookup"><span data-stu-id="27ea3-130">Create a shopping cart</span></span>](create-a-cart.md)
   - [<span data-ttu-id="27ea3-131">Alışveriş sepetini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="27ea3-131">Update a shopping cart</span></span>](update-a-cart.md)

2. <span data-ttu-id="27ea3-132">Sepete göz at.</span><span class="sxs-lookup"><span data-stu-id="27ea3-132">Check out the cart.</span></span> <span data-ttu-id="27ea3-133">Sepete göz atarak Sipariş oluşturulmasına neden [olur.](order-resources.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-133">Checking out a cart results in the creation of an [Order](order-resources.md).</span></span>

   - [<span data-ttu-id="27ea3-134">Sepete göz at</span><span class="sxs-lookup"><span data-stu-id="27ea3-134">Checkout the cart</span></span>](checkout-a-cart.md)

## <a name="get-order-details"></a><span data-ttu-id="27ea3-135">Sipariş ayrıntılarını al</span><span class="sxs-lookup"><span data-stu-id="27ea3-135">Get order details</span></span>

<span data-ttu-id="27ea3-136">Sipariş kimliğini kullanarak tek bir siparişin ayrıntılarını alabilir veya müşteri için siparişlerin listesini edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27ea3-136">You can retrieve the details of an individual order using the order ID, or get a list of orders for a customer.</span></span> <span data-ttu-id="27ea3-137">Bir siparişin gönderilme zamanı ile müşterinin sipariş listesinde görünmesi arasında 15 dakikaya kadar bir gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="27ea3-137">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a list of a customer's orders.</span></span>

- <span data-ttu-id="27ea3-138">Sipariş [kimliklerini kullanarak tek bir](get-an-order-by-id.md) siparişin ayrıntılarını almak için bkz. Kimliklere göre sipariş al.</span><span class="sxs-lookup"><span data-stu-id="27ea3-138">See [Get an order by ID](get-an-order-by-id.md) to get the details of an individual order using the order IDs.</span></span>

- <span data-ttu-id="27ea3-139">Müşteri [kimliğini kullanarak bir müşterinin sipariş listesini](get-all-of-a-customer-s-orders.md) almak için bkz. Müşterinin tüm siparişlerini alma.</span><span class="sxs-lookup"><span data-stu-id="27ea3-139">See [Get all of a customer's orders](get-all-of-a-customer-s-orders.md) to get a list of orders for a customer using the customer ID.</span></span>

- <span data-ttu-id="27ea3-140">Katalog [öğesi siparişlerini](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) (tek defalık ücretler) ve yıllık veya [](product-resources.md#billingcycletype) aylık faturalandırılabilir siparişleri ayrı olarak listeleyebilirsiniz. Faturalama döngüsü türüne göre bir müşteriye yönelik siparişlerin listesini almak için bkz. Müşteriye ve faturalama döngüsü türüne göre siparişlerin listesini alma.</span><span class="sxs-lookup"><span data-stu-id="27ea3-140">See [Get a list of orders by customer and billing cycle type](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) to get a list of orders for a customer by [billing cycle type](product-resources.md#billingcycletype) allowing you to list catalog item orders (one-time charges) and annual or monthly billed orders separately.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="27ea3-141">Yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="27ea3-141">Lifecycle management</span></span>

<span data-ttu-id="27ea3-142">İş Ortağı Merkezi'de katalog öğelerinizin yaşam döngüsünün yönetilmesinin bir parçası olarak, katalog [](entitlement-resources.md)öğesi Yetkilendirmeleri hakkında bilgi alabilir ve rezervasyon sipariş kimliğini kullanarak rezervasyon ayrıntılarını edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27ea3-142">As part of managing the lifecycle of your catalog items in Partner Center, you can retrieve information about your catalog item [Entitlements](entitlement-resources.md), and get reservation details using the reservation order ID.</span></span> <span data-ttu-id="27ea3-143">Bunu yapma örnekleri için bkz. [Yetkilendirmeleri al.](get-a-collection-of-entitlements.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-143">For examples of how to do this, see [Get entitlements](get-a-collection-of-entitlements.md).</span></span>   

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="27ea3-144">Fatura ve mutabakat</span><span class="sxs-lookup"><span data-stu-id="27ea3-144">Invoice and reconciliation</span></span>

<span data-ttu-id="27ea3-145">Aşağıdaki senaryolar, müşterinizin faturalarını program aracılığıyla [](invoice-resources.md)görüntülemeyi ve katalog öğeleri için tek sefer ücretleri içeren hesap bakiyelerinizi ve özetlerinizi nasıl alasınız?</span><span class="sxs-lookup"><span data-stu-id="27ea3-145">The following scenarios show you how to programmatically view your customer's [invoices](invoice-resources.md), and get your account balances and summaries that include one-time charges for catalog items.</span></span>

### <a name="balance-and-payment"></a><span data-ttu-id="27ea3-146">Bakiye ve ödeme</span><span class="sxs-lookup"><span data-stu-id="27ea3-146">Balance and payment</span></span>

<span data-ttu-id="27ea3-147">Hem yinelenen hem de bir defalık (katalog öğesi) ücretlerinin bakiyesi olan varsayılan para birimi türünüz için geçerli hesap bakiyenizi almak için bkz. [Geçerli hesap bakiyenizi al.](get-the-reseller-s-current-account-balance.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-147">To get current account balance in your default currency type that is a balance of both recurring and one-time (catalog item) charges, see [Get your current account balance](get-the-reseller-s-current-account-balance.md).</span></span>

### <a name="multi-currency-balance-and-payment"></a><span data-ttu-id="27ea3-148">Çoklu para birimi bakiyesi ve ödeme</span><span class="sxs-lookup"><span data-stu-id="27ea3-148">Multi-currency balance and payment</span></span>

<span data-ttu-id="27ea3-149">Geçerli hesap bakiyenizi ve her müşterinizin para birimi türleri için hem yinelenen hem de tek defalık ücretleri içeren bir fatura özeti içeren fatura özetleri koleksiyonunu almak için [bkz. Fatura özetlerini alın.](get-invoice-summaries.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-149">To get your current account balance and a collection of invoice summaries containing an invoice summary with both recurring and one-time charges for each of your customer's currency types, see [Get invoice summaries](get-invoice-summaries.md).</span></span>

### <a name="invoices"></a><span data-ttu-id="27ea3-150">Faturalar</span><span class="sxs-lookup"><span data-stu-id="27ea3-150">Invoices</span></span>

<span data-ttu-id="27ea3-151">Hem yinelenen hem de tek seferlik ücretlerin yer alan bir fatura koleksiyonunu almak için bkz. Fatura [koleksiyonu alın.](get-a-collection-of-invoices.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-151">To get a collection of invoices that show both recurring and one-time charges, see [Get a collection of invoices](get-a-collection-of-invoices.md).</span></span> 

### <a name="single-invoice"></a><span data-ttu-id="27ea3-152">Tek Fatura</span><span class="sxs-lookup"><span data-stu-id="27ea3-152">Single Invoice</span></span>

<span data-ttu-id="27ea3-153">Fatura kimliğini kullanarak belirli bir faturayı almak için [bkz. Kimliğine göre fatura alma.](get-invoice-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-153">To retrieve a specific invoice using the invoice ID, see [Get an invoice by ID](get-invoice-by-id.md).</span></span>  

### <a name="reconciliation"></a><span data-ttu-id="27ea3-154">Uzlaşma</span><span class="sxs-lookup"><span data-stu-id="27ea3-154">Reconciliation</span></span>

<span data-ttu-id="27ea3-155">Belirli bir fatura kimliğine ilişkin fatura satırı öğesi ayrıntılarının (Mutabakat satır öğeleri) koleksiyonunu almak için [bkz. Fatura satırı öğelerini al.](get-invoiceline-items.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-155">To get a collection of invoice line item details (Reconciliation line items) for a specific invoice ID, see [Get invoice line items](get-invoiceline-items.md).</span></span>  

### <a name="download-an-invoice-as-a-pdf"></a><span data-ttu-id="27ea3-156">Faturayı PDF olarak indirme</span><span class="sxs-lookup"><span data-stu-id="27ea3-156">Download an invoice as a PDF</span></span>

<span data-ttu-id="27ea3-157">Fatura kimliği kullanarak PDF formunda fatura deyimi almak için bkz. [Fatura deyimi alma.](get-invoice-statement.md)</span><span class="sxs-lookup"><span data-stu-id="27ea3-157">To retrieve an invoice statement in PDF form using an invoice ID, see [Get an invoice statement](get-invoice-statement.md).</span></span>
