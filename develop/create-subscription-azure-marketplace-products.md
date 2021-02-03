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
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Ticari Market ürünleri için abonelik oluşturma

**Uygulama hedefi:**

* İş Ortağı Merkezi

Iş Ortağı Merkezi API 'Lerini kullanarak ticari Market ürünleri için bir abonelik oluşturabilirsiniz. [Pazara yönelik tekliflerin bir listesini almanız](#get-a-list-of-offers-for-a-market), ticari Market aboneliğine yönelik bir [sipariş oluşturup göndermeniz ve](#create-and-submit-an-order) ardından [bir etkinleştirme bağlantısı almanız](#get-activation-link)gerekir.

Ayrıca, [yaşam döngüsü yönetimi gerçekleştirebilir](#lifecycle-management) ve bu abonelikler için [faturaları yönetebilirsiniz](#invoice-and-reconciliation) .

## <a name="prerequisites"></a>Önkoşullar

* [Iş ortağı merkezi kimlik doğrulama](partner-center-authentication.md) bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.
* Müşteri tanımlayıcısı. Müşterinin tanımlayıcısı yoksa, [müşterilerin listesini al](get-a-list-of-customers.md)bölümündeki adımları izleyin. Alternatif olarak, Iş Ortağı Merkezi ' nde oturum açın, müşteri listesinden müşteriyi seçin, **Hesap**' ı seçin ve **Microsoft kimliklerini** kaydedin.

## <a name="get-a-list-of-offers-for-a-market"></a>Pazara yönelik tekliflerin bir listesini alma

Aşağıdaki Iş Ortağı Merkezi API modellerini kullanarak bir pazar için kullanılabilir teklifleri kontrol edebilirsiniz:

* **[Ürün](product-resources.md#product)**: satın alınabilir alınırken mallar veya hizmetler için gruplama yapısı. Ürünün kendisi bir satın alınabilir alınırken öğesi değil.
* **[SKU](product-resources.md#sku)**: bir ürün altındaki satın alınabilir alınırken stok tutma BIRIMI (SKU). Bunlar, ürünün farklı şekillerini temsil eder.
* **[Kullanılabilirlik](product-resources.md#availability)**: BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi veya sektör segmenti gibi).

Bir Azure ayırması satın almadan önce, aşağıdaki adımları izleyin:

1. Satın almak istediğiniz ürün ve SKU 'YU belirleyip alın. Ürün KIMLIĞI ve SKU KIMLIĞINI zaten biliyorsanız, bunları seçin.

    * [Ürünlerin bir listesini alın](get-a-list-of-products.md)
    * [Ürün KIMLIĞINI kullanarak bir ürün alın](get-a-product-by-id.md)
    * [Ürün için SKU 'ların listesini alın](get-a-list-of-skus-for-a-product.md)
    * [SKU KIMLIĞI kullanarak bir SKU al](get-a-sku-by-id.md)

    > [!NOTE]
    > Ticari Market ürünlerini, **ProductType** özelliği olan **"Azure"** ve onların **Subtype** özelliği olan **"SaaS"** olarak tanımlayabilirsiniz.

2. SKU 'Lar bir **ınventorycheck** önkoşulu ile ETIKETLENMIŞSE, [SKU 'nun envanterini kontrol](check-inventory.md)edin.

    > [!NOTE]
    > Şu anda, envanter denetimini destekleyen bir ticari Market ürünü yoktur veya bir **ınventorycheck** önkoşulu ile etiketlenebilir.

3. SKU için kullanılabilirliği alın. Siparişi yerleştirirken, aşağıdaki API 'Ler aracılığıyla alabileceğiniz, kullanılabilir olan **Catalogıtemıd** öğesine ihtiyacınız olacaktır:

    * [SKU 'nun kullanılabilirliği listesini alın](get-a-list-of-availabilities-for-a-sku.md)
    * [Kullanılabilirlik KIMLIĞINI kullanarak bir kullanılabilirlik alın](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Sipariş oluşturma ve gönderme

Azure rezervasyon siparişinizi göndermek için şu adımları izleyin:

1. Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için [bir sepet oluşturun](create-a-cart.md) . Bir [sepet](cart-resources.md#cart)oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md#order)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır. ( [Bir sepet de güncelleştirebilirsiniz](update-a-cart.md).)
2. Bir [sipariş](order-resources.md#order)oluşturulmasına neden olan [sepete](checkout-a-cart.md)göz atın.

### <a name="get-order-details"></a>Sipariş ayrıntılarını al

[SIPARIŞ kimliğini kullanarak tek bir siparişin ayrıntılarını alabilirsiniz](get-an-order-by-id.md). Ayrıca, [belirli bir müşterinin tüm siparişlerinin listesini alabilirsiniz](get-all-of-a-customer-s-orders.md).

> [!NOTE]
> Bir sipariş gönderildikten sonra, bu müşterinin sıra listesinde görüntülenmeden önce 15 dakikaya kadar bir gecikme olur.

## <a name="get-activation-link"></a>Etkinleştirme bağlantısını al

İş ortağı veya müşteri, abonelikleri Azure Market ürünlerine etkinleştirmelidir. [Sipariş satırı öğesine göre bir etkinleştirme bağlantısı alabilirsiniz](get-activation-link-by-order-line-item.md). Ayrıca, [kimliğe göre bir abonelik alabilir](get-a-subscription-by-id.md)ve ardından bir etkinleştirme bağlantısı oluşturmak için **Links** özelliğini numaralandırabilirsiniz.

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

Aşağıdaki yöntemleri kullanarak ticari Market ürünleri aboneliklerinizin yaşam döngüsünü yönetebilirsiniz:

* [Ticari market aboneliğini iptal etme](cancel-an-azure-marketplace-subscription.md)
* [Ticari Market aboneliği için autorenew 'i etkinleştirme veya devre dışı bırakma](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Miktar yönetimi

Bir ticari Market aboneliğinin miktarı, ilişkili [SKU 'su](product-resources.md#sku) tarafından tanımlanan sınırlar dahilinde olmalıdır (bkz. **Minimumquantity** ve **maximumquantity** öznitelikleri). Bir ticari Market aboneliğinin miktarını güncelleştirmek için aşağıdaki yöntemi kullanın:

* [Bir aboneliğin miktarını değiştirme](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki yöntemleri kullanarak müşteri [faturalarını](invoice-resources.md) (ticari Market ürünlerine abonelikler için ücretler dahil olmak üzere) yönetebilirsiniz:

* [Fatura faturalandırılan ticari Market tüketim satırı öğelerini Al](get-invoice-billed-consumption-lineitems.md)
* [Fatura tahmini bağlantılarını alma](get-invoice-estimate-links.md)
* [Fatura faturalanmamış ticari Market tüketim satırı öğelerini Al](get-invoice-unbilled-consumption-lineitems.md)
* [Fatura faturalandırılmamış mutabakat satır öğelerini Al](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Tümleştirme korumalı alanı hesabını kullanarak test etme

Üretimde, ticari Market SaaS ürünlerine bir abonelik oluşturduktan sonra, Iş Ortağı Merkezi 'nden kişiselleştirilmiş bir etkinleştirme bağlantısı almanız ve kurulum işlemini tamamlaması için yayımcının sitesini ziyaret etmeniz gerekir. Abonelik faturalandırması, yalnızca kurulum tamamlandıktan sonra başlayacaktır.

CSP korumalı alan ortamında ISV 'Ler ile tümleştirme yoktur. Iş Ortağı Merkezi 'nden bir etkinleştirme bağlantısı almaya çalışırsanız, bir kukla bağlantı döndürülür. Bu kukla bağlantıyı, yayımcının sitesindeki kurulum işlemini tamamlayacak şekilde kullanamazsınız. Ticari Market SaaS ürünlerine yönelik abonelikleri test etmek üzere tümleştirme korumalı alanı hesabını kullanmak için, bunun yerine aboneliği etkinleştirmek üzere aşağıdaki yöntemi kullanın. Aboneliğin faturalandırılması, başarıyla etkinleştirilmesinden sonra başlayacak:

* [Ticari Market ürünleri için bir korumalı alan aboneliğini etkinleştirin](activate-sandbox-subscription-azure-marketplace-products.md)

