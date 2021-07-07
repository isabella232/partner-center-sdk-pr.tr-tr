---
title: Ticari market ürünleri için abonelik oluşturma
description: Geliştiriciler, farklı API'leri kullanarak ticari market ürünleri için İş Ortağı Merkezi oluşturabilir ve yönetebilir.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ae2e4b0a1ffa2e63e68864887093673e32079d9f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973375"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a><span data-ttu-id="f79ea-103">Ticari market ürünleri için abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="f79ea-103">Create a subscription for commercial marketplace products</span></span>

<span data-ttu-id="f79ea-104">Api'leri kullanarak ticari market ürünleri için İş Ortağı Merkezi oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f79ea-104">You can create a subscription for commercial marketplace products using Partner Center APIs.</span></span> <span data-ttu-id="f79ea-105">Bir pazara [yönelik tekliflerin listesini alısınız,](#get-a-list-of-offers-for-a-market) [ticari](#create-and-submit-an-order) market aboneliği için sipariş oluşturmanız ve göndermeniz ve ardından etkinleştirme bağlantısını [alasınız.](#get-activation-link)</span><span class="sxs-lookup"><span data-stu-id="f79ea-105">You must [get a list of offers for a market](#get-a-list-of-offers-for-a-market), [create and submit an order](#create-and-submit-an-order) for a commercial marketplace subscription, then [retrieve an activation link](#get-activation-link).</span></span>

<span data-ttu-id="f79ea-106">Ayrıca bu [abonelikler için yaşam döngüsü](#lifecycle-management) yönetimi [gerçekleştirebilirsiniz ve](#invoice-and-reconciliation) faturaları yönetebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f79ea-106">You can also [perform lifecycle management](#lifecycle-management) and [manage invoices](#invoice-and-reconciliation) for these subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f79ea-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f79ea-107">Prerequisites</span></span>

* <span data-ttu-id="f79ea-108">[İş Ortağı Merkezi kimlik doğrulaması](partner-center-authentication.md) kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f79ea-108">[Partner Center authentication](partner-center-authentication.md) credentials.</span></span> <span data-ttu-id="f79ea-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="f79ea-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>
* <span data-ttu-id="f79ea-110">Müşteri tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="f79ea-110">The customer identifier.</span></span> <span data-ttu-id="f79ea-111">Müşteri tanımlayıcısına sahip değilsanız Müşteri listesini alma [adımlarını izleyin.](get-a-list-of-customers.md)</span><span class="sxs-lookup"><span data-stu-id="f79ea-111">If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md).</span></span> <span data-ttu-id="f79ea-112">Alternatif olarak, İş Ortağı Merkezi oturum açın, müşteri listesinden müşteriyi seçin, Hesap'ı **seçin** ve microsoft kimliğini **kaydedin.**</span><span class="sxs-lookup"><span data-stu-id="f79ea-112">Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.</span></span>

## <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="f79ea-113">Pazara yönelik tekliflerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="f79ea-113">Get a list of offers for a market</span></span>

<span data-ttu-id="f79ea-114">Aşağıdaki API modellerini kullanarak pazar için kullanılabilir teklifleri İş Ortağı Merkezi edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f79ea-114">You can check the available offers for a market using the following Partner Center API models:</span></span>

* <span data-ttu-id="f79ea-115">**[Ürün:](product-resources.md#product)** Satınlanabilir ürünler veya hizmetler için bir gruplama yapısı.</span><span class="sxs-lookup"><span data-stu-id="f79ea-115">**[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="f79ea-116">Ürünün kendisi satınlanabilir bir öğe değildir.</span><span class="sxs-lookup"><span data-stu-id="f79ea-116">A product itself isn't a purchasable item.</span></span>
* <span data-ttu-id="f79ea-117">**[SKU:](product-resources.md#sku)** Ürün altında satın alınabilir bir Stok Tutma Birimi (SKU).</span><span class="sxs-lookup"><span data-stu-id="f79ea-117">**[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="f79ea-118">Bunlar ürünün farklı şekillerini temsil ediyor.</span><span class="sxs-lookup"><span data-stu-id="f79ea-118">These represent the different shapes of the product.</span></span>
* <span data-ttu-id="f79ea-119">**[Kullanılabilirlik:](product-resources.md#availability)** SKU'nun satın alınabilir olduğu yapılandırma (ülke, para birimi veya sektör segmenti gibi).</span><span class="sxs-lookup"><span data-stu-id="f79ea-119">**[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).</span></span>

<span data-ttu-id="f79ea-120">Azure rezervasyonu satın almadan önce aşağıdaki adımları tamamlayın:</span><span class="sxs-lookup"><span data-stu-id="f79ea-120">Before you purchase an Azure reservation, complete the following steps:</span></span>

1. <span data-ttu-id="f79ea-121">Satın almak istediğiniz ürünü ve SKU'ları belirleyin ve alın.</span><span class="sxs-lookup"><span data-stu-id="f79ea-121">Identify and retrieve the product and SKU that you want to purchase.</span></span> <span data-ttu-id="f79ea-122">Ürün Kimliği ve SKU Kimliğini zaten biliyorsanız bunları seçin.</span><span class="sxs-lookup"><span data-stu-id="f79ea-122">If you already know the Product ID and SKU ID, select them.</span></span>

    * [<span data-ttu-id="f79ea-123">Ürünlerin listesini al</span><span class="sxs-lookup"><span data-stu-id="f79ea-123">Get a list of products</span></span>](get-a-list-of-products.md)
    * [<span data-ttu-id="f79ea-124">Ürün kimliğini kullanarak ürün al</span><span class="sxs-lookup"><span data-stu-id="f79ea-124">Get a product using the product ID</span></span>](get-a-product-by-id.md)
    * [<span data-ttu-id="f79ea-125">Bir ürün için SKUS listesini al</span><span class="sxs-lookup"><span data-stu-id="f79ea-125">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
    * [<span data-ttu-id="f79ea-126">SKU Kimliğini kullanarak SKU'ya sahip olmak</span><span class="sxs-lookup"><span data-stu-id="f79ea-126">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

    > [!NOTE]
    > <span data-ttu-id="f79ea-127">Ticari market ürünlerini **ProductType** özelliğine ve **"SaaS"** **subType** **özelliğine göre tanımlayabilirsiniz.**</span><span class="sxs-lookup"><span data-stu-id="f79ea-127">You can identify commercial marketplace products by their **ProductType** property of **"Azure"** and their **SubType** property of **"SaaS"**.</span></span>

2. <span data-ttu-id="f79ea-128">SKU'lar **InventoryCheck** önkoşulları ile etiketlenmişse, [SKU envanterini kontrol edin.](check-inventory.md)</span><span class="sxs-lookup"><span data-stu-id="f79ea-128">If the SKUs are tagged with an **InventoryCheck** prerequisite, [check the inventory for a SKU](check-inventory.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="f79ea-129">Şu anda envanter denetimi destekleyen veya **InventoryCheck** önkolu ile etiketlenen ticari market ürünleri yoktur.</span><span class="sxs-lookup"><span data-stu-id="f79ea-129">At this time, there are no commercial marketplace products that support inventory check or are tagged with an **InventoryCheck** prerequisite.</span></span>

3. <span data-ttu-id="f79ea-130">SKU için kullanılabilirliği alın.</span><span class="sxs-lookup"><span data-stu-id="f79ea-130">Retrieve the availability for the SKU.</span></span> <span data-ttu-id="f79ea-131">Siparişinizi sağlarken **kullanılabilirlik CatalogItemId'ye** ihtiyacınız olacak ve bu bilgileri aşağıdaki API'ler aracılığıyla edinebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f79ea-131">You will need the **CatalogItemId** of the availability when placing the order, which you can retrieve through the following APIs:</span></span>

    * [<span data-ttu-id="f79ea-132">SKU için kullanılabilirlik listesini al</span><span class="sxs-lookup"><span data-stu-id="f79ea-132">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
    * [<span data-ttu-id="f79ea-133">Kullanılabilirlik kimliğini kullanarak kullanılabilirlik elde edin</span><span class="sxs-lookup"><span data-stu-id="f79ea-133">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a><span data-ttu-id="f79ea-134">Sipariş oluşturma ve gönderme</span><span class="sxs-lookup"><span data-stu-id="f79ea-134">Create and submit an order</span></span>

<span data-ttu-id="f79ea-135">Azure rezervasyon siparişinizi göndermek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="f79ea-135">To submit your Azure reservation order, follow these steps:</span></span>

1. <span data-ttu-id="f79ea-136">[Satın almayı istediğiniz](create-a-cart.md) katalog öğelerinin koleksiyonunu tutmak için bir sepet oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f79ea-136">[Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="f79ea-137">Bir sepet [oluşturma](cart-resources.md#cart)sırasında, [sepet satır](cart-resources.md#cartlineitem) öğeleri aynı sırayla birlikte satın alınarak otomatik olarak [gruplanır.](order-resources.md#order)</span><span class="sxs-lookup"><span data-stu-id="f79ea-137">When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order).</span></span> <span data-ttu-id="f79ea-138">(Bir sepeti [de güncelleştirin.)](update-a-cart.md)</span><span class="sxs-lookup"><span data-stu-id="f79ea-138">(You can also [update a cart](update-a-cart.md).)</span></span>
2. <span data-ttu-id="f79ea-139">[Siparişin oluşturulmasıyla](checkout-a-cart.md)sonuçlandıran sepetine [göz at.](order-resources.md#order)</span><span class="sxs-lookup"><span data-stu-id="f79ea-139">[Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).</span></span>

### <a name="get-order-details"></a><span data-ttu-id="f79ea-140">Sipariş ayrıntılarını al</span><span class="sxs-lookup"><span data-stu-id="f79ea-140">Get order details</span></span>

<span data-ttu-id="f79ea-141">Sipariş [kimliğini kullanarak tek bir siparişin ayrıntılarını alın.](get-an-order-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="f79ea-141">You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md).</span></span> <span data-ttu-id="f79ea-142">Belirli bir [müşteriye yönelik tüm siparişlerin listesini de almak için kullanabilirsiniz.](get-all-of-a-customer-s-orders.md)</span><span class="sxs-lookup"><span data-stu-id="f79ea-142">You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).</span></span>

> [!NOTE]
> <span data-ttu-id="f79ea-143">Bir sipariş gönderildikten sonra, siparişin müşterinin sipariş listesinde görünürken 15 dakika kadar gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="f79ea-143">After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list.</span></span>

## <a name="get-activation-link"></a><span data-ttu-id="f79ea-144">Etkinleştirme bağlantısını al</span><span class="sxs-lookup"><span data-stu-id="f79ea-144">Get activation link</span></span>

<span data-ttu-id="f79ea-145">İş ortağının veya müşterinin abonelikleri ürün Azure Market gerekir.</span><span class="sxs-lookup"><span data-stu-id="f79ea-145">The partner or customer must activate subscriptions to Azure Marketplace products.</span></span> <span data-ttu-id="f79ea-146">Sipariş satırı [öğesine göre etkinleştirme bağlantısı edinebilirsiniz.](get-activation-link-by-order-line-item.md)</span><span class="sxs-lookup"><span data-stu-id="f79ea-146">You can [get an activation link by order line item](get-activation-link-by-order-line-item.md).</span></span> <span data-ttu-id="f79ea-147">Ayrıca, [kimliğine göre bir abonelik edinebilirsiniz,](get-a-subscription-by-id.md)ardından etkinleştirme bağlantısı oluşturmak için **Links** özelliğini numaralandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f79ea-147">You can also [get a subscription by ID](get-a-subscription-by-id.md), then enumerate its **Links** property to create an activation link.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="f79ea-148">Yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="f79ea-148">Lifecycle management</span></span>

<span data-ttu-id="f79ea-149">Ticari market ürünlerine aboneliklerinizi yaşam döngüsünü yönetmek için aşağıdaki yöntemleri kullanabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f79ea-149">You can manage the lifecycle of your subscriptions to commercial marketplace products using the following methods:</span></span>

* [<span data-ttu-id="f79ea-150">Ticari market aboneliğini iptal etme</span><span class="sxs-lookup"><span data-stu-id="f79ea-150">Cancel a commercial marketplace subscription</span></span>](cancel-an-azure-marketplace-subscription.md)
* [<span data-ttu-id="f79ea-151">Ticari market aboneliği için otomatik yenilemeyi etkinleştirme veya devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="f79ea-151">Enable or disable autorenew for a commercial marketplace subscription</span></span>](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a><span data-ttu-id="f79ea-152">Miktar yönetimi</span><span class="sxs-lookup"><span data-stu-id="f79ea-152">Quantity management</span></span>

<span data-ttu-id="f79ea-153">Ticari market aboneliğinin miktarı, ilişkili [SKU'su](product-resources.md#sku) tarafından tanımlanan sınırlar içinde yer almalı **(bkz. minimumQuantity** ve **maximumQuantity** öznitelikleri).</span><span class="sxs-lookup"><span data-stu-id="f79ea-153">The quantity of a commercial marketplace subscription must be within the limits defined by its associated [SKU](product-resources.md#sku) (see the **minimumQuantity** and **maximumQuantity** attributes).</span></span> <span data-ttu-id="f79ea-154">Ticari market aboneliğinin miktarını güncelleştirmek için aşağıdaki yöntemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="f79ea-154">To update the quantity of a commercial marketplace subscription, use the following method:</span></span>

* [<span data-ttu-id="f79ea-155">Bir aboneliğin miktarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="f79ea-155">Change the quantity of a subscription</span></span>](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="f79ea-156">Fatura ve mutabakat</span><span class="sxs-lookup"><span data-stu-id="f79ea-156">Invoice and reconciliation</span></span>

<span data-ttu-id="f79ea-157">Aşağıdaki yöntemleri kullanarak [müşteri faturalarını](invoice-resources.md) (ticari market ürünlerine abonelik ücretleri dahil) yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="f79ea-157">You can manage customer [invoices](invoice-resources.md) (including charges for subscriptions to commercial marketplace products) using the following methods:</span></span>

* [<span data-ttu-id="f79ea-158">Faturalandırmış ticari market tüketim satırı öğelerini alma</span><span class="sxs-lookup"><span data-stu-id="f79ea-158">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
* [<span data-ttu-id="f79ea-159">Fatura tahmini bağlantılarını alma</span><span class="sxs-lookup"><span data-stu-id="f79ea-159">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
* [<span data-ttu-id="f79ea-160">Faturalanmamış ticari market tüketim satırı öğelerini alma</span><span class="sxs-lookup"><span data-stu-id="f79ea-160">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
* [<span data-ttu-id="f79ea-161">Faturalanmamış mutabakat satırı öğelerini alın</span><span class="sxs-lookup"><span data-stu-id="f79ea-161">Get invoice unbilled reconciliation line items</span></span>](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a><span data-ttu-id="f79ea-162">Tümleştirme korumalı alan hesabını kullanarak test</span><span class="sxs-lookup"><span data-stu-id="f79ea-162">Test using integration sandbox account</span></span>

<span data-ttu-id="f79ea-163">Üretimde, ticari market SaaS ürünlerine abonelik oluşturduktan sonra, kurulum işlemini tamamlamak için İş Ortağı Merkezi'dan kişiselleştirilmiş etkinleştirme bağlantısını alı ve yayımcının sitesini ziyaret edin.</span><span class="sxs-lookup"><span data-stu-id="f79ea-163">In production, after you have created a subscription to commercial marketplace SaaS products, you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="f79ea-164">Abonelik faturalaması ancak kurulum tamamlandıktan sonra başlar.</span><span class="sxs-lookup"><span data-stu-id="f79ea-164">Subscription billing will begin only after setup is complete.</span></span>

<span data-ttu-id="f79ea-165">CSP korumalı alanı ortamında ISV'lerle tümleştirme yoktur.</span><span class="sxs-lookup"><span data-stu-id="f79ea-165">In the CSP sandbox environment, there is no integration with ISVs.</span></span> <span data-ttu-id="f79ea-166">İş Ortağı Merkezi'dan etkinleştirme bağlantısını almaya İş Ortağı Merkezi, sahte bir bağlantı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="f79ea-166">If you try to retrieve an activation link from Partner Center, a dummy link will be returned.</span></span> <span data-ttu-id="f79ea-167">Yayımcının sitesinde kurulum işlemini tamamlamak için bu sahte bağlantıyı kullanılamaz.</span><span class="sxs-lookup"><span data-stu-id="f79ea-167">You cannot use this dummy link to complete the setup process at the publisher's site.</span></span> <span data-ttu-id="f79ea-168">Ticari market SaaS ürünlerine aboneliklerin faturalarını test etmek üzere tümleştirme korumalı alanı hesabını kullanmak için aşağıdaki yöntemi kullanarak aboneliği etkinleştirin.</span><span class="sxs-lookup"><span data-stu-id="f79ea-168">To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, use the following method to activate the subscription instead.</span></span> <span data-ttu-id="f79ea-169">Abonelik faturalaması, etkinleştirme başarılı olduktan sonra başlar:</span><span class="sxs-lookup"><span data-stu-id="f79ea-169">Subscription billing will begin after successful activation:</span></span>

* [<span data-ttu-id="f79ea-170">Ticari market ürünleri için korumalı alan aboneliğini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="f79ea-170">Activate a sandbox subscription for commercial marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

