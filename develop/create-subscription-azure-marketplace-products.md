---
title: Ticari Market ürünleri için abonelik oluşturma
description: Geliştiriciler, Iş Ortağı Merkezi API 'Lerini kullanarak ticari Market ürünleri için bir abonelik oluşturabilir ve yönetebilir.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: df2a3707e00ba36a11c404b102304c08d105244e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768812"
---
# <a name="create-a-subscription-for-commercial-marketplace-products"></a><span data-ttu-id="6e856-103">Ticari Market ürünleri için abonelik oluşturma</span><span class="sxs-lookup"><span data-stu-id="6e856-103">Create a subscription for commercial marketplace products</span></span>

<span data-ttu-id="6e856-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="6e856-104">**Applies to:**</span></span>

* <span data-ttu-id="6e856-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6e856-105">Partner Center</span></span>

<span data-ttu-id="6e856-106">Iş Ortağı Merkezi API 'Lerini kullanarak ticari Market ürünleri için bir abonelik oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e856-106">You can create a subscription for commercial marketplace products using Partner Center APIs.</span></span> <span data-ttu-id="6e856-107">[Pazara yönelik tekliflerin bir listesini almanız](#get-a-list-of-offers-for-a-market), ticari Market aboneliğine yönelik bir [sipariş oluşturup göndermeniz ve](#create-and-submit-an-order) ardından [bir etkinleştirme bağlantısı almanız](#get-activation-link)gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e856-107">You must [get a list of offers for a market](#get-a-list-of-offers-for-a-market), [create and submit an order](#create-and-submit-an-order) for a commercial marketplace subscription, then [retrieve an activation link](#get-activation-link).</span></span>

<span data-ttu-id="6e856-108">Ayrıca, [yaşam döngüsü yönetimi gerçekleştirebilir](#lifecycle-management) ve bu abonelikler için [faturaları yönetebilirsiniz](#invoice-and-reconciliation) .</span><span class="sxs-lookup"><span data-stu-id="6e856-108">You can also [perform lifecycle management](#lifecycle-management) and [manage invoices](#invoice-and-reconciliation) for these subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6e856-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6e856-109">Prerequisites</span></span>

* <span data-ttu-id="6e856-110">[Iş ortağı merkezi kimlik doğrulama](partner-center-authentication.md) bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6e856-110">[Partner Center authentication](partner-center-authentication.md) credentials.</span></span> <span data-ttu-id="6e856-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="6e856-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>
* <span data-ttu-id="6e856-112">Müşteri tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="6e856-112">The customer identifier.</span></span> <span data-ttu-id="6e856-113">Müşterinin tanımlayıcısı yoksa, [müşterilerin listesini al](get-a-list-of-customers.md)bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="6e856-113">If you don't have a customer's identifier, follow the steps in [Get a list of customers](get-a-list-of-customers.md).</span></span> <span data-ttu-id="6e856-114">Alternatif olarak, Iş Ortağı Merkezi ' nde oturum açın, müşteri listesinden müşteriyi seçin, **Hesap**' ı seçin ve **Microsoft kimliklerini** kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6e856-114">Alternatively, sign in to Partner Center, choose the customer from the list of customers, select **Account**, then save their **Microsoft ID**.</span></span>

## <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="6e856-115">Pazara yönelik tekliflerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="6e856-115">Get a list of offers for a market</span></span>

<span data-ttu-id="6e856-116">Aşağıdaki Iş Ortağı Merkezi API modellerini kullanarak bir pazar için kullanılabilir teklifleri kontrol edebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e856-116">You can check the available offers for a market using the following Partner Center API models:</span></span>

* <span data-ttu-id="6e856-117">**[Ürün](product-resources.md#product)**: satın alınabilir alınırken mallar veya hizmetler için gruplama yapısı.</span><span class="sxs-lookup"><span data-stu-id="6e856-117">**[Product](product-resources.md#product)**: A grouping construct for purchasable goods or services.</span></span> <span data-ttu-id="6e856-118">Ürünün kendisi bir satın alınabilir alınırken öğesi değil.</span><span class="sxs-lookup"><span data-stu-id="6e856-118">A product itself isn't a purchasable item.</span></span>
* <span data-ttu-id="6e856-119">**[SKU](product-resources.md#sku)**: bir ürün altındaki satın alınabilir alınırken stok tutma BIRIMI (SKU).</span><span class="sxs-lookup"><span data-stu-id="6e856-119">**[SKU](product-resources.md#sku)**: A purchasable Stock Keeping Unit (SKU) under a product.</span></span> <span data-ttu-id="6e856-120">Bunlar, ürünün farklı şekillerini temsil eder.</span><span class="sxs-lookup"><span data-stu-id="6e856-120">These represent the different shapes of the product.</span></span>
* <span data-ttu-id="6e856-121">**[Kullanılabilirlik](product-resources.md#availability)**: BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi veya sektör segmenti gibi).</span><span class="sxs-lookup"><span data-stu-id="6e856-121">**[Availability](product-resources.md#availability)**: A configuration in which a SKU is available for purchase (such as country, currency, or industry segment).</span></span>

<span data-ttu-id="6e856-122">Bir Azure ayırması satın almadan önce, aşağıdaki adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6e856-122">Before you purchase an Azure reservation, complete the following steps:</span></span>

1. <span data-ttu-id="6e856-123">Satın almak istediğiniz ürün ve SKU 'YU belirleyip alın.</span><span class="sxs-lookup"><span data-stu-id="6e856-123">Identify and retrieve the product and SKU that you want to purchase.</span></span> <span data-ttu-id="6e856-124">Ürün KIMLIĞI ve SKU KIMLIĞINI zaten biliyorsanız, bunları seçin.</span><span class="sxs-lookup"><span data-stu-id="6e856-124">If you already know the Product ID and SKU ID, select them.</span></span>

    * [<span data-ttu-id="6e856-125">Ürünlerin bir listesini alın</span><span class="sxs-lookup"><span data-stu-id="6e856-125">Get a list of products</span></span>](get-a-list-of-products.md)
    * [<span data-ttu-id="6e856-126">Ürün KIMLIĞINI kullanarak bir ürün alın</span><span class="sxs-lookup"><span data-stu-id="6e856-126">Get a product using the product ID</span></span>](get-a-product-by-id.md)
    * [<span data-ttu-id="6e856-127">Ürün için SKU 'ların listesini alın</span><span class="sxs-lookup"><span data-stu-id="6e856-127">Get a list of SKUs for a product</span></span>](get-a-list-of-skus-for-a-product.md)
    * [<span data-ttu-id="6e856-128">SKU KIMLIĞI kullanarak bir SKU al</span><span class="sxs-lookup"><span data-stu-id="6e856-128">Get a SKU using the SKU ID</span></span>](get-a-sku-by-id.md)

    > [!NOTE]
    > <span data-ttu-id="6e856-129">Ticari Market ürünlerini, **ProductType** özelliği olan **"Azure"** ve onların **Subtype** özelliği olan **"SaaS"** olarak tanımlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e856-129">You can identify commercial marketplace products by their **ProductType** property of **"Azure"** and their **SubType** property of **"SaaS"**.</span></span>

2. <span data-ttu-id="6e856-130">SKU 'Lar bir **ınventorycheck** önkoşulu ile ETIKETLENMIŞSE, [SKU 'nun envanterini kontrol](check-inventory.md)edin.</span><span class="sxs-lookup"><span data-stu-id="6e856-130">If the SKUs are tagged with an **InventoryCheck** prerequisite, [check the inventory for a SKU](check-inventory.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="6e856-131">Şu anda, envanter denetimini destekleyen bir ticari Market ürünü yoktur veya bir **ınventorycheck** önkoşulu ile etiketlenebilir.</span><span class="sxs-lookup"><span data-stu-id="6e856-131">At this time, there are no commercial marketplace products that support inventory check or are tagged with an **InventoryCheck** prerequisite.</span></span>

3. <span data-ttu-id="6e856-132">SKU için kullanılabilirliği alın.</span><span class="sxs-lookup"><span data-stu-id="6e856-132">Retrieve the availability for the SKU.</span></span> <span data-ttu-id="6e856-133">Siparişi yerleştirirken, aşağıdaki API 'Ler aracılığıyla alabileceğiniz, kullanılabilir olan **Catalogıtemıd** öğesine ihtiyacınız olacaktır:</span><span class="sxs-lookup"><span data-stu-id="6e856-133">You will need the **CatalogItemId** of the availability when placing the order, which you can retrieve through the following APIs:</span></span>

    * [<span data-ttu-id="6e856-134">SKU 'nun kullanılabilirliği listesini alın</span><span class="sxs-lookup"><span data-stu-id="6e856-134">Get a list of availabilities for a SKU</span></span>](get-a-list-of-availabilities-for-a-sku.md)
    * [<span data-ttu-id="6e856-135">Kullanılabilirlik KIMLIĞINI kullanarak bir kullanılabilirlik alın</span><span class="sxs-lookup"><span data-stu-id="6e856-135">Get an availability using the availability ID</span></span>](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a><span data-ttu-id="6e856-136">Sipariş oluşturma ve gönderme</span><span class="sxs-lookup"><span data-stu-id="6e856-136">Create and submit an order</span></span>

<span data-ttu-id="6e856-137">Azure rezervasyon siparişinizi göndermek için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="6e856-137">To submit your Azure reservation order, follow these steps:</span></span>

1. <span data-ttu-id="6e856-138">Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için [bir sepet oluşturun](create-a-cart.md) .</span><span class="sxs-lookup"><span data-stu-id="6e856-138">[Create a cart](create-a-cart.md) to hold the collection of catalog items that you intend to buy.</span></span> <span data-ttu-id="6e856-139">Bir [sepet](cart-resources.md#cart)oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md#order)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır.</span><span class="sxs-lookup"><span data-stu-id="6e856-139">When you create a [cart](cart-resources.md#cart), the [cart line items](cart-resources.md#cartlineitem) are automatically grouped based on what can be purchased together in the same [order](order-resources.md#order).</span></span> <span data-ttu-id="6e856-140">( [Bir sepet de güncelleştirebilirsiniz](update-a-cart.md).)</span><span class="sxs-lookup"><span data-stu-id="6e856-140">(You can also [update a cart](update-a-cart.md).)</span></span>
2. <span data-ttu-id="6e856-141">Bir [sipariş](order-resources.md#order)oluşturulmasına neden olan [sepete](checkout-a-cart.md)göz atın.</span><span class="sxs-lookup"><span data-stu-id="6e856-141">[Check out the cart](checkout-a-cart.md), which results in the creation of an [order](order-resources.md#order).</span></span>

### <a name="get-order-details"></a><span data-ttu-id="6e856-142">Sipariş ayrıntılarını al</span><span class="sxs-lookup"><span data-stu-id="6e856-142">Get order details</span></span>

<span data-ttu-id="6e856-143">[SIPARIŞ kimliğini kullanarak tek bir siparişin ayrıntılarını alabilirsiniz](get-an-order-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="6e856-143">You can [retrieve the details of an individual order using the order ID](get-an-order-by-id.md).</span></span> <span data-ttu-id="6e856-144">Ayrıca, [belirli bir müşterinin tüm siparişlerinin listesini alabilirsiniz](get-all-of-a-customer-s-orders.md).</span><span class="sxs-lookup"><span data-stu-id="6e856-144">You can also [retrieve a list of all orders for a specific customer](get-all-of-a-customer-s-orders.md).</span></span>

> [!NOTE]
> <span data-ttu-id="6e856-145">Bir sipariş gönderildikten sonra, bu müşterinin sıra listesinde görüntülenmeden önce 15 dakikaya kadar bir gecikme olur.</span><span class="sxs-lookup"><span data-stu-id="6e856-145">After an order is submitted, there is a delay of up to 15 minutes before the order appears in that customer's order list.</span></span>

## <a name="get-activation-link"></a><span data-ttu-id="6e856-146">Etkinleştirme bağlantısını al</span><span class="sxs-lookup"><span data-stu-id="6e856-146">Get activation link</span></span>

<span data-ttu-id="6e856-147">İş ortağı veya müşteri, abonelikleri Azure Market ürünlerine etkinleştirmelidir.</span><span class="sxs-lookup"><span data-stu-id="6e856-147">The partner or customer must activate subscriptions to Azure Marketplace products.</span></span> <span data-ttu-id="6e856-148">[Sipariş satırı öğesine göre bir etkinleştirme bağlantısı alabilirsiniz](get-activation-link-by-order-line-item.md).</span><span class="sxs-lookup"><span data-stu-id="6e856-148">You can [get an activation link by order line item](get-activation-link-by-order-line-item.md).</span></span> <span data-ttu-id="6e856-149">Ayrıca, [kimliğe göre bir abonelik alabilir](get-a-subscription-by-id.md)ve ardından bir etkinleştirme bağlantısı oluşturmak için **Links** özelliğini numaralandırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6e856-149">You can also [get a subscription by ID](get-a-subscription-by-id.md), then enumerate its **Links** property to create an activation link.</span></span>

## <a name="lifecycle-management"></a><span data-ttu-id="6e856-150">Yaşam döngüsü yönetimi</span><span class="sxs-lookup"><span data-stu-id="6e856-150">Lifecycle management</span></span>

<span data-ttu-id="6e856-151">Aşağıdaki yöntemleri kullanarak ticari Market ürünleri aboneliklerinizin yaşam döngüsünü yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e856-151">You can manage the lifecycle of your subscriptions to commercial marketplace products using the following methods:</span></span>

* [<span data-ttu-id="6e856-152">Ticari market aboneliğini iptal etme</span><span class="sxs-lookup"><span data-stu-id="6e856-152">Cancel a commercial marketplace subscription</span></span>](cancel-an-azure-marketplace-subscription.md)
* [<span data-ttu-id="6e856-153">Ticari Market aboneliği için autorenew 'i etkinleştirme veya devre dışı bırakma</span><span class="sxs-lookup"><span data-stu-id="6e856-153">Enable or disable autorenew for a commercial marketplace subscription</span></span>](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a><span data-ttu-id="6e856-154">Miktar yönetimi</span><span class="sxs-lookup"><span data-stu-id="6e856-154">Quantity management</span></span>

<span data-ttu-id="6e856-155">Bir ticari Market aboneliğinin miktarı, ilişkili [SKU 'su](product-resources.md#sku) tarafından tanımlanan sınırlar dahilinde olmalıdır (bkz. **Minimumquantity** ve **maximumquantity** öznitelikleri).</span><span class="sxs-lookup"><span data-stu-id="6e856-155">The quantity of a commercial marketplace subscription must be within the limits defined by its associated [SKU](product-resources.md#sku) (see the **minimumQuantity** and **maximumQuantity** attributes).</span></span> <span data-ttu-id="6e856-156">Bir ticari Market aboneliğinin miktarını güncelleştirmek için aşağıdaki yöntemi kullanın:</span><span class="sxs-lookup"><span data-stu-id="6e856-156">To update the quantity of a commercial marketplace subscription, use the following method:</span></span>

* [<span data-ttu-id="6e856-157">Bir aboneliğin miktarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="6e856-157">Change the quantity of a subscription</span></span>](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a><span data-ttu-id="6e856-158">Fatura ve mutabakat</span><span class="sxs-lookup"><span data-stu-id="6e856-158">Invoice and reconciliation</span></span>

<span data-ttu-id="6e856-159">Aşağıdaki yöntemleri kullanarak müşteri [faturalarını](invoice-resources.md) (ticari Market ürünlerine abonelikler için ücretler dahil olmak üzere) yönetebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6e856-159">You can manage customer [invoices](invoice-resources.md) (including charges for subscriptions to commercial marketplace products) using the following methods:</span></span>

* [<span data-ttu-id="6e856-160">Fatura faturalandırılan ticari Market tüketim satırı öğelerini Al</span><span class="sxs-lookup"><span data-stu-id="6e856-160">Get invoice billed commercial marketplace consumption line items</span></span>](get-invoice-billed-consumption-lineitems.md)
* [<span data-ttu-id="6e856-161">Fatura tahmini bağlantılarını alma</span><span class="sxs-lookup"><span data-stu-id="6e856-161">Get invoice estimate links</span></span>](get-invoice-estimate-links.md)
* [<span data-ttu-id="6e856-162">Fatura faturalanmamış ticari Market tüketim satırı öğelerini Al</span><span class="sxs-lookup"><span data-stu-id="6e856-162">Get invoice unbilled commercial marketplace consumption line items</span></span>](get-invoice-unbilled-consumption-lineitems.md)
* [<span data-ttu-id="6e856-163">Fatura faturalandırılmamış mutabakat satır öğelerini Al</span><span class="sxs-lookup"><span data-stu-id="6e856-163">Get invoice unbilled reconciliation line items</span></span>](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a><span data-ttu-id="6e856-164">Tümleştirme korumalı alanı hesabını kullanarak test etme</span><span class="sxs-lookup"><span data-stu-id="6e856-164">Test using integration sandbox account</span></span>

<span data-ttu-id="6e856-165">Üretimde, ticari Market SaaS ürünlerine bir abonelik oluşturduktan sonra, Iş Ortağı Merkezi 'nden kişiselleştirilmiş bir etkinleştirme bağlantısı almanız ve kurulum işlemini tamamlaması için yayımcının sitesini ziyaret etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="6e856-165">In production, after you have created a subscription to commercial marketplace SaaS products, you need to retrieve a personalized activation link from Partner Center and visit the publisher's site to complete the setup process.</span></span> <span data-ttu-id="6e856-166">Abonelik faturalandırması, yalnızca kurulum tamamlandıktan sonra başlayacaktır.</span><span class="sxs-lookup"><span data-stu-id="6e856-166">Subscription billing will begin only after setup is complete.</span></span>

<span data-ttu-id="6e856-167">CSP korumalı alan ortamında ISV 'Ler ile tümleştirme yoktur.</span><span class="sxs-lookup"><span data-stu-id="6e856-167">In the CSP sandbox environment, there is no integration with ISVs.</span></span> <span data-ttu-id="6e856-168">Iş Ortağı Merkezi 'nden bir etkinleştirme bağlantısı almaya çalışırsanız, bir kukla bağlantı döndürülür.</span><span class="sxs-lookup"><span data-stu-id="6e856-168">If you try to retrieve an activation link from Partner Center, a dummy link will be returned.</span></span> <span data-ttu-id="6e856-169">Bu kukla bağlantıyı, yayımcının sitesindeki kurulum işlemini tamamlayacak şekilde kullanamazsınız.</span><span class="sxs-lookup"><span data-stu-id="6e856-169">You cannot use this dummy link to complete the setup process at the publisher's site.</span></span> <span data-ttu-id="6e856-170">Ticari Market SaaS ürünlerine yönelik abonelikleri test etmek üzere tümleştirme korumalı alanı hesabını kullanmak için, bunun yerine aboneliği etkinleştirmek üzere aşağıdaki yöntemi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6e856-170">To use the integration sandbox account to test billing for subscriptions to commercial marketplace SaaS products, use the following method to activate the subscription instead.</span></span> <span data-ttu-id="6e856-171">Aboneliğin faturalandırılması, başarıyla etkinleştirilmesinden sonra başlayacak:</span><span class="sxs-lookup"><span data-stu-id="6e856-171">Subscription billing will begin after successful activation:</span></span>

* [<span data-ttu-id="6e856-172">Ticari Market ürünleri için bir korumalı alan aboneliğini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="6e856-172">Activate a sandbox subscription for commercial marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

