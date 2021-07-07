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
# <a name="create-a-subscription-for-commercial-marketplace-products"></a>Ticari market ürünleri için abonelik oluşturma

Api'leri kullanarak ticari market ürünleri için İş Ortağı Merkezi oluşturabilirsiniz. Bir pazara [yönelik tekliflerin listesini alısınız,](#get-a-list-of-offers-for-a-market) [ticari](#create-and-submit-an-order) market aboneliği için sipariş oluşturmanız ve göndermeniz ve ardından etkinleştirme bağlantısını [alasınız.](#get-activation-link)

Ayrıca bu [abonelikler için yaşam döngüsü](#lifecycle-management) yönetimi [gerçekleştirebilirsiniz ve](#invoice-and-reconciliation) faturaları yönetebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

* [İş Ortağı Merkezi kimlik doğrulaması](partner-center-authentication.md) kimlik bilgileri. Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
* Müşteri tanımlayıcısı. Müşteri tanımlayıcısına sahip değilsanız Müşteri listesini alma [adımlarını izleyin.](get-a-list-of-customers.md) Alternatif olarak, İş Ortağı Merkezi oturum açın, müşteri listesinden müşteriyi seçin, Hesap'ı **seçin** ve microsoft kimliğini **kaydedin.**

## <a name="get-a-list-of-offers-for-a-market"></a>Pazara yönelik tekliflerin bir listesini alma

Aşağıdaki API modellerini kullanarak pazar için kullanılabilir teklifleri İş Ortağı Merkezi edinebilirsiniz:

* **[Ürün:](product-resources.md#product)** Satınlanabilir ürünler veya hizmetler için bir gruplama yapısı. Ürünün kendisi satınlanabilir bir öğe değildir.
* **[SKU:](product-resources.md#sku)** Ürün altında satın alınabilir bir Stok Tutma Birimi (SKU). Bunlar ürünün farklı şekillerini temsil ediyor.
* **[Kullanılabilirlik:](product-resources.md#availability)** SKU'nun satın alınabilir olduğu yapılandırma (ülke, para birimi veya sektör segmenti gibi).

Azure rezervasyonu satın almadan önce aşağıdaki adımları tamamlayın:

1. Satın almak istediğiniz ürünü ve SKU'ları belirleyin ve alın. Ürün Kimliği ve SKU Kimliğini zaten biliyorsanız bunları seçin.

    * [Ürünlerin listesini al](get-a-list-of-products.md)
    * [Ürün kimliğini kullanarak ürün al](get-a-product-by-id.md)
    * [Bir ürün için SKUS listesini al](get-a-list-of-skus-for-a-product.md)
    * [SKU Kimliğini kullanarak SKU'ya sahip olmak](get-a-sku-by-id.md)

    > [!NOTE]
    > Ticari market ürünlerini **ProductType** özelliğine ve **"SaaS"** **subType** **özelliğine göre tanımlayabilirsiniz.**

2. SKU'lar **InventoryCheck** önkoşulları ile etiketlenmişse, [SKU envanterini kontrol edin.](check-inventory.md)

    > [!NOTE]
    > Şu anda envanter denetimi destekleyen veya **InventoryCheck** önkolu ile etiketlenen ticari market ürünleri yoktur.

3. SKU için kullanılabilirliği alın. Siparişinizi sağlarken **kullanılabilirlik CatalogItemId'ye** ihtiyacınız olacak ve bu bilgileri aşağıdaki API'ler aracılığıyla edinebilirsiniz:

    * [SKU için kullanılabilirlik listesini al](get-a-list-of-availabilities-for-a-sku.md)
    * [Kullanılabilirlik kimliğini kullanarak kullanılabilirlik elde edin](get-an-availability-by-id.md)

## <a name="create-and-submit-an-order"></a>Sipariş oluşturma ve gönderme

Azure rezervasyon siparişinizi göndermek için şu adımları izleyin:

1. [Satın almayı istediğiniz](create-a-cart.md) katalog öğelerinin koleksiyonunu tutmak için bir sepet oluşturun. Bir sepet [oluşturma](cart-resources.md#cart)sırasında, [sepet satır](cart-resources.md#cartlineitem) öğeleri aynı sırayla birlikte satın alınarak otomatik olarak [gruplanır.](order-resources.md#order) (Bir sepeti [de güncelleştirin.)](update-a-cart.md)
2. [Siparişin oluşturulmasıyla](checkout-a-cart.md)sonuçlandıran sepetine [göz at.](order-resources.md#order)

### <a name="get-order-details"></a>Sipariş ayrıntılarını al

Sipariş [kimliğini kullanarak tek bir siparişin ayrıntılarını alın.](get-an-order-by-id.md) Belirli bir [müşteriye yönelik tüm siparişlerin listesini de almak için kullanabilirsiniz.](get-all-of-a-customer-s-orders.md)

> [!NOTE]
> Bir sipariş gönderildikten sonra, siparişin müşterinin sipariş listesinde görünürken 15 dakika kadar gecikme olur.

## <a name="get-activation-link"></a>Etkinleştirme bağlantısını al

İş ortağının veya müşterinin abonelikleri ürün Azure Market gerekir. Sipariş satırı [öğesine göre etkinleştirme bağlantısı edinebilirsiniz.](get-activation-link-by-order-line-item.md) Ayrıca, [kimliğine göre bir abonelik edinebilirsiniz,](get-a-subscription-by-id.md)ardından etkinleştirme bağlantısı oluşturmak için **Links** özelliğini numaralandırabilirsiniz.

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

Ticari market ürünlerine aboneliklerinizi yaşam döngüsünü yönetmek için aşağıdaki yöntemleri kullanabilirsiniz:

* [Ticari market aboneliğini iptal etme](cancel-an-azure-marketplace-subscription.md)
* [Ticari market aboneliği için otomatik yenilemeyi etkinleştirme veya devre dışı bırakma](update-autorenew-for-an-azure-marketplace-subscription.md)

## <a name="quantity-management"></a>Miktar yönetimi

Ticari market aboneliğinin miktarı, ilişkili [SKU'su](product-resources.md#sku) tarafından tanımlanan sınırlar içinde yer almalı **(bkz. minimumQuantity** ve **maximumQuantity** öznitelikleri). Ticari market aboneliğinin miktarını güncelleştirmek için aşağıdaki yöntemi kullanın:

* [Bir aboneliğin miktarını değiştirme](change-the-quantity-of-a-subscription.md)

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki yöntemleri kullanarak [müşteri faturalarını](invoice-resources.md) (ticari market ürünlerine abonelik ücretleri dahil) yönetebilirsiniz:

* [Faturalandırmış ticari market tüketim satırı öğelerini alma](get-invoice-billed-consumption-lineitems.md)
* [Fatura tahmini bağlantılarını alma](get-invoice-estimate-links.md)
* [Faturalanmamış ticari market tüketim satırı öğelerini alma](get-invoice-unbilled-consumption-lineitems.md)
* [Faturalanmamış mutabakat satırı öğelerini alın](get-invoice-unbilled-recon-lineitems.md)

## <a name="test-using-integration-sandbox-account"></a>Tümleştirme korumalı alan hesabını kullanarak test

Üretimde, ticari market SaaS ürünlerine abonelik oluşturduktan sonra, kurulum işlemini tamamlamak için İş Ortağı Merkezi'dan kişiselleştirilmiş etkinleştirme bağlantısını alı ve yayımcının sitesini ziyaret edin. Abonelik faturalaması ancak kurulum tamamlandıktan sonra başlar.

CSP korumalı alanı ortamında ISV'lerle tümleştirme yoktur. İş Ortağı Merkezi'dan etkinleştirme bağlantısını almaya İş Ortağı Merkezi, sahte bir bağlantı döndürülür. Yayımcının sitesinde kurulum işlemini tamamlamak için bu sahte bağlantıyı kullanılamaz. Ticari market SaaS ürünlerine aboneliklerin faturalarını test etmek üzere tümleştirme korumalı alanı hesabını kullanmak için aşağıdaki yöntemi kullanarak aboneliği etkinleştirin. Abonelik faturalaması, etkinleştirme başarılı olduktan sonra başlar:

* [Ticari market ürünleri için korumalı alan aboneliğini etkinleştirme](activate-sandbox-subscription-azure-marketplace-products.md)

