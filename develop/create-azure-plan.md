---
title: Azure planı oluşturma
description: Geliştiriciler Azure planlarını program aracılığıyla satın alma, oluşturma ve yönetme İş Ortağı Merkezi kullanabilir.
ms.date: 07/21/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 5083f7aa8ea274b5210d88085d26376dadbc0c4d1a0dd6e1babe59c94d7a6f9c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991489"
---
# <a name="create-an-azure-plan"></a>Azure planı oluşturma

Azure planı satın almak, oluşturmak ve yönetmek için api'leri İş Ortağı Merkezi kullanabilirsiniz. İşlem, bir Microsoft Azure ([MS-AZR-0145P](https://go.microsoft.com/fwlink/p/?linkid=2164140)) aboneliği oluşturmaya benzer. Azure [planı için katalog öğesini alıp bir](#get-the-catalog-item-for-azure-plan)sipariş [oluşturmanız ve göndermeniz gerekir.](#create-and-submit-an-order)

## <a name="prerequisites"></a>Önkoşullar

* [İş Ortağı Merkezi kimlik doğrulaması](partner-center-authentication.md) kimlik bilgileri. Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
* Müşteri tanımlayıcısı. Müşteri tanımlayıcısına sahip değilsanız Müşteri listesini alma [adımlarını izleyin.](get-a-list-of-customers.md) Alternatif olarak, İş Ortağı Merkezi oturum açın, müşteri listesinden müşteriyi seçin, Hesap'ı **seçin** ve microsoft kimliğini **kaydedin.**
* [Müşterinin tarafından kabulü onaylandı ve Microsoft Müşteri Sözleşmesi.](/partner-center/confirm-customer-agreement)

## <a name="get-the-catalog-item-for-azure-plan"></a>Azure planı için katalog öğesini edinin

Müşteri için bir Azure planı oluşturamadan önce ilgili katalog öğesini alasiniz. Katalog öğesini, aşağıdaki kaynak modelleriyle İş Ortağı Merkezi katalog API'lerini kullanarak alın.

* **[Ürün:](product-resources.md#product)** Satınlanabilir ürünler veya hizmetler için bir gruplama yapısı. Ürünün kendisi satınlanabilir bir öğe değildir.
* **[SKU:](product-resources.md#sku)** Ürün altında satın alınabilir bir Stok Tutma Birimi (SKU). SKUS'lar ürünün farklı şekillerini temsil ediyor.
* **[Kullanılabilirlik:](product-resources.md#availability)** SKU'nun satın alınabilir olduğu yapılandırma (ülke, para birimi veya sektör segmenti gibi).

Bir Azure planının katalog öğesini almak için aşağıdaki adımları tamamlayın:

1. Azure planının *ürün tanımlayıcısını* belirleme ve alma. Ürünlerin listesini alma [ve targetView'u](get-a-list-of-products.md) **MicrosoftAzure olarak belirtme adımlarını izleyin.**  (Azure planının ürün *tanımlayıcısını* zaten biliyorsanız bunun yerine Ürün kimliğini kullanarak ürün alma [adımlarını takip](get-a-product-by-id.md) edin.)

2. Azure **planı için** üründen SKU'ları alın. Bir ürün için [SKUS listesini al'daki adımları izleyin.](get-a-list-of-skus-for-a-product.md) Azure planının SKU tanımlayıcısını zaten biliyorsanız, bunun yerine SKU kimliğini kullanarak SKU alma [adımlarını takip](get-a-sku-by-id.md) edin.

3. Azure **planı için** SKU'dan kullanılabilirliği alın. SKU için [kullanılabilirlik listesini al'daki adımları izleyin.](get-a-list-of-availabilities-for-a-sku.md) Ihtiyacınız olan kullanılabilirlik için tanımlayıcıyı zaten biliyorsanız Kullanılabilirlik kimliğini kullanarak kullanılabilirlik [alma adımlarını takip](get-an-availability-by-id.md) edin. *Azure planı için kullanılabilirlik **özelliğinin CatalogItemId** özelliğinin değerini not edin. Sipariş oluşturmak için bu değere ihtiyacınız olacak.*

## <a name="create-and-submit-an-order"></a>Sipariş oluşturma ve gönderme

Azure planı siparişinizi göndermek için şu adımları izleyin:

1. [Satın almayı istediğiniz](create-a-cart.md) katalog öğelerinin koleksiyonunu tutmak için bir sepet oluşturun. Bir sepet [oluşturma](cart-resources.md#cart)sırasında, [sepet satır](cart-resources.md#cartlineitem) öğeleri aynı sırayla birlikte satın alınarak otomatik olarak [gruplanır.](order-resources.md#order) (Bir sepeti [de güncelleştirin.)](update-a-cart.md)

2. [Siparişin oluşturulmasıyla](checkout-a-cart.md)sonuçlandıran sepetine [göz at.](order-resources.md#order)

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

Sipariş [kimliğini kullanarak tek bir siparişin ayrıntılarını alın.](get-an-order-by-id.md) Belirli bir [müşteriye yönelik tüm siparişlerin listesini de almak için kullanabilirsiniz.](get-all-of-a-customer-s-orders.md)

>[!NOTE]
>Bir sipariş gönderildikten sonra, siparişin müşterinin sipariş listesinde görünürken 15 dakika kadar gecikme olur.

## <a name="manage-azure-plans"></a>Azure planlarını yönetme

Sipariş başarıyla işlendikten sonra, Azure İş Ortağı Merkezi **abonelik** kaynağı oluşturulur. Azure planını yönetmek için abonelik kaynaklarını İş Ortağı Merkezi **aşağıdaki** yöntemleri kullanabilirsiniz:

* [Müşterinin aboneliğini alma](get-all-of-a-customer-s-subscriptions.md)
* [Siparişe göre aboneliklerin bir listesini alma](get-a-list-of-subscriptions-by-order.md)

Azure'da bir Azure planı İş Ortağı Merkezi azure'da karşılık gelen bir Azure kullanım aboneliği de oluşturulur. Azure api'lerini ve Azure API'lerini kullanarak aynı Azure planı altında Azure portal Azure kullanım abonelikleri de oluşturabilirsiniz. Bir Azure planıyla ilişkili tüm Azure kullanım aboneliklerinin tanımlayıcılarını almak için Azure aboneliği için Azure yetkilendirmelerinin [listesini alma](get-a-list-of-azure-entitlements-for-subscription.md) İş Ortağı Merkezi alabilirsiniz

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

Aboneliği askıya alma 'daki adımları takip edin ve mevcut Bir Azure planını [askıya almak için askıya alın.](suspend-a-subscription.md)

*Mevcut Bir Azure planını askıya almak için azure kullanım abonelikleri ve Azure rezervasyonları dahil olmak üzere artık ilişkili etkin kullanım varlıkları yoksa askıya alabilirsiniz.*

Azure kullanım aboneliklerini devre dışı bırakma hakkında ayrıntılı bilgi için bkz. [Abonelik yaşam döngüsü yönetiminde Azure API.](/rest/api/resources/subscriptions)

Mevcut Azure rezervasyonlarını kaldırmak için rezervasyonları [iptal etmeniz gerekir.](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation)
Bir Azure planını askıya aldırdikten sonra yeniden etkinleştirilebilir.

Azure planını yeniden etkinleştirme hakkında ayrıntılı bilgi için bkz. [Askıya alınmış aboneliği yeniden etkinleştirme](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Mevcut CSP tekliflerini Azure planına geçirme 

Microsoft Azure (MS-AZR-0145P) aboneliğine sahip mevcut müşteriler için Azure planı oluşturamazsınız. Bununla birlikte, İş Ortağı Merkezi'nin içinde yer alan CSP programındaki yeni ticaret deneyiminde [müşteriyi mevcut CSP Azure tekliflerinden Azure planı kapsamındaki Azure hizmetlerine geçirebilirsiniz](/partner-center/azure-plan-transition). Mevcut müşteriyi geçirmek için ürün yükseltme API'lerini kullanarak şu adımları izleyin:

* [Müşterinin Azure planına geçişe uygun olup olmadığını denetleme](get-eligibility-for-product-upgrade.md)
* [Müşteri için ürün yükseltmesi başlatma](create-product-upgrade-entity.md)
* [Ürün yükseltmesinin durumunu denetleme](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Azure harcaması

Aşağıdaki yöntemleri [kullanarak kullanım](azure-spending.md) özetini ve ayrıntılı kullanım kayıtlarını sorgularken Azure harcamalarını izleyebilirsiniz:

* [İş ortağı kullanım özeti alma](get-a-partner-usage-summary.md)
* [İş ortağı için tüm müşteri kullanım kayıtlarını alma](get-a-customer-s-usage-records.md)
* [Müşteri kullanım özeti alma](get-a-customer-usage-summary.md)
* [Müşteri için tüm abonelik kullanım kayıtlarını alma](get-a-customer-subscription-s-usage-records.md)
* [Abonelik kullanım özeti alma](get-a-customer-subscription-usage-summary.md)
* [Kaynağa göre abonelik için kullanım verilerini alma](get-a-customer-subscription-resource-usage-records.md)
* [Ölçüme göre abonelik için kullanım verilerini alma](get-a-customer-subscription-meter-usage-records.md)
* [Ölçüm kullanım kaydı kaynaklarını alma](meter-usage-resources.md)
* [Kaynak kullanım kaydı kaynaklarını alma](resource-usage-resources.md)

Ayrıca aşağıdaki yöntemleri kullanarak müşteri kullanım bütçesini de ayarp yönetebilirsiniz:

* [Müşteri kullanım bütçesi alma](get-a-customer-s-usage-spending-budget.md)
* [Müşteri kullanım bütçesi güncelleştirme](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Faturaları ve mutabakat verilerini yönetmek için aşağıdaki yöntemleri kullanabilirsiniz:

* [Faturaların koleksiyonunu alma](get-a-collection-of-invoices.md)
* [Fatura tahmini bağlantılarını alma](get-invoice-estimate-links.md)
* [Kimliğine göre fatura al](get-invoice-by-id.md)
* [Fatura ekstresini alma](get-invoice-statement.md)
* [Fatura özetlerini alma](get-invoice-summaries.md)
* [Faturalandırılan tüketim satırı öğelerini alma](get-invoice-billed-consumption-lineitems.md)
* [Faturalanmamış tüketim satırı öğelerini alma](get-invoice-unbilled-consumption-lineitems.md)
* [Faturalanmış mutabakat satırı öğelerini alın](get-invoiceline-items.md)
* [Faturalanmamış keşif satırı öğelerini alma](get-invoice-unbilled-recon-lineitems.md)
