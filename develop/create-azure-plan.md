---
title: Azure planı oluşturma
description: Geliştiriciler Iş Ortağı Merkezi API 'Lerini kullanarak Azure planlarını programlı bir şekilde satın alabilir, oluşturabilir ve yönetebilir.
ms.date: 01/02/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: mowrim
ms.author: mowrim
ms.openlocfilehash: 372b94ac7217899ca560cf943bf11a7e8906872d
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769316"
---
# <a name="create-an-azure-plan"></a>Azure planı oluşturma

**Uygulama hedefi:**

* İş Ortağı Merkezi

Iş Ortağı Merkezi API 'Lerini kullanarak bir Azure planı satın alabilir, oluşturabilir ve yönetebilirsiniz. İşlem, Microsoft Azure (MS-AZR-0145P) aboneliği oluşturmaya benzer. [Azure planına ait Katalog öğesini almanız](#get-the-catalog-item-for-azure-plan) [ve ardından sipariş oluşturmanız ve göndermeniz](#create-and-submit-an-order)gerekir.

## <a name="prerequisites"></a>Önkoşullar

* [Iş ortağı merkezi kimlik doğrulama](partner-center-authentication.md) bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.
* Müşteri tanımlayıcısı. Müşterinin tanımlayıcısı yoksa, [müşterilerin listesini al](get-a-list-of-customers.md)bölümündeki adımları izleyin. Alternatif olarak, Iş Ortağı Merkezi ' nde oturum açın, müşteri listesinden müşteriyi seçin, **Hesap**' ı seçin ve **Microsoft kimliklerini** kaydedin.
* [Müşterinin Microsoft Müşteri sözleşmesinin kabul edilmesine yönelik onay](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-azure-plan"></a>Azure planına yönelik Katalog öğesini al

Bir müşteri için bir Azure planı oluşturabilmeniz için önce karşılık gelen Katalog öğesini almanız gerekir. Aşağıdaki kaynak modelleriyle mevcut Iş Ortağı Merkezi kataloğu API 'Lerini kullanarak katalog öğesini alabilirsiniz.

* **[Ürün](product-resources.md#product)**: satın alınabilir alınırken mallar veya hizmetler için gruplama yapısı. Ürünün kendisi bir satın alınabilir alınırken öğesi değil.
* **[SKU](product-resources.md#sku)**: bir ürün altındaki satın alınabilir alınırken stok tutma BIRIMI (SKU). SKU 'Lar ürünün farklı şekillerini temsil eder.
* **[Kullanılabilirlik](product-resources.md#availability)**: BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi veya sektör segmenti gibi).

Bir Azure planına ait Katalog öğesini almak için aşağıdaki adımları izleyin:

1. Azure planına ait *ürün* tanımlayıcısını tanımlama ve alma. [Ürünlerin listesini al](get-a-list-of-products.md) bölümündeki adımları Izleyin ve **Targetview** öğesini **MicrosoftAzure** olarak belirtin. (Azure planına ait *ürün* tanımlayıcısını zaten biliyorsanız, bunun yerıne ürün [kimliği kullanarak ürün edinme](get-a-product-by-id.md) adımlarını izleyebilirsiniz.)

2. Azure planına ait ürünün **SKU** 'sunu alın. [Bir ürün Için SKU 'ların listesini alın](get-a-list-of-skus-for-a-product.md)bölümündeki adımları izleyin. Azure planına ait SKU tanımlayıcısını zaten biliyorsanız, SKU [kimliğini kullanarak SKU al](get-a-sku-by-id.md) bölümündeki adımları takip edebilirsiniz.

3. Azure planına ait SKU 'dan **kullanılabilirliği** alın. [SKU 'nun kullanılabilirliği listesini al](get-a-list-of-availabilities-for-a-sku.md)bölümündeki adımları izleyin. İhtiyaç duyduğunuz kullanılabilirlik için tanımlayıcıyı zaten biliyorsanız, bunun yerine [KULLANıLABILIRLIK kimliğini kullanarak kullanılabilirlik edinme](get-an-availability-by-id.md) bölümündeki adımları izleyebilirsiniz. *Azure planının kullanılabilirliğine ait **Catalogıtemıd** özelliğinin değerini aklınızda olduğunuzdan emin olun. Sipariş oluşturmak için bu değere ihtiyacınız olacaktır.*

## <a name="create-and-submit-an-order"></a>Sipariş oluşturma ve gönderme

Bir Azure planına siparişiniz göndermek için şu adımları izleyin:

1. Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için [bir sepet oluşturun](create-a-cart.md) . Bir [sepet](cart-resources.md#cart)oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md#order)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır. ( [Bir sepet de güncelleştirebilirsiniz](update-a-cart.md).)

2. Bir [sipariş](order-resources.md#order)oluşturulmasına neden olan [sepete](checkout-a-cart.md)göz atın.

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

[SIPARIŞ kimliğini kullanarak tek bir siparişin ayrıntılarını alabilirsiniz](get-an-order-by-id.md). Ayrıca, [belirli bir müşterinin tüm siparişlerinin listesini alabilirsiniz](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>Bir sipariş gönderildikten sonra, bu müşterinin sıra listesinde görüntülenmeden önce 15 dakikaya kadar bir gecikme olur.

## <a name="manage-azure-plans"></a>Azure planlarını yönetme

Sipariş başarıyla işlendikten sonra Azure planı için bir Iş Ortağı Merkezi **abonelik** kaynağı oluşturulur. Azure planını yönetmek üzere Iş Ortağı Merkezi **abonelik** kaynaklarını yönetmek için aşağıdaki yöntemleri kullanabilirsiniz:

* [Müşterinin aboneliğini alma](get-all-of-a-customer-s-subscriptions.md)
* [Siparişe göre aboneliklerin bir listesini alma](get-a-list-of-subscriptions-by-order.md)

Iş Ortağı Merkezi 'nde bir Azure planı oluşturulduğunda, Azure 'da buna karşılık gelen bir Azure kullanım aboneliği de oluşturulur. Azure Portal ve Azure API 'Leri kullanarak aynı Azure planı altında ek Azure kullanım abonelikleri de oluşturabilirsiniz. Azure planıyla ilişkili tüm Azure kullanım aboneliklerinin tanımlayıcılarını, [Iş Ortağı Merkezi aboneliğine yönelik Azure yetkilendirmeleri listesini alma](get-a-list-of-azure-entitlements-for-subscription.md) bölümündeki adımları izleyerek elde edebilirsiniz.

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

[Aboneliği askıya alma](suspend-a-subscription.md)' daki adımları izleyerek mevcut bir Azure planını askıya alabilirsiniz.

*Yalnızca mevcut bir Azure planını, Azure kullanım abonelikleri ve Azure ayırmaları dahil olmak üzere bununla ilişkili etkin kullanım varlıkları yoksa askıya alabilirsiniz.*

Azure kullanım aboneliklerini devre dışı bırakma hakkında daha fazla bilgi için bkz. [abonelik yaşam döngüsü yönetiminde Azure API](/rest/api/resources/subscriptions).

Mevcut Azure ayırmalarını kaldırmak için [ayırmaları iptal](/partner-center/azure-reservations-manage#cancel-or-exchange-a-reservation)etmeniz gerekir.
Bir Azure planını askıya aldıktan sonra yeniden etkinleştirebilirsiniz.

Bir Azure planını yeniden etkinleştirmeye ilişkin ayrıntılar için bkz. [askıya alınmış aboneliği yeniden etkinleştirme](reactivate-a-suspended-a-subscription.md)

## <a name="transition-existing-csp-offers-to-azure-plan"></a>Mevcut CSP tekliflerini Azure planına geçirme 

Microsoft Azure (MS-AZR-0145P) aboneliğine sahip mevcut müşteriler için Azure planı oluşturamazsınız. Bununla birlikte, İş Ortağı Merkezi'nin içinde yer alan CSP programındaki yeni ticaret deneyiminde [müşteriyi mevcut CSP Azure tekliflerinden Azure planı kapsamındaki Azure hizmetlerine geçirebilirsiniz](/partner-center/azure-plan-transition). Mevcut müşteriyi geçirmek için ürün yükseltme API'lerini kullanarak şu adımları izleyin:

* [Müşterinin Azure planına geçişe uygun olup olmadığını denetleme](get-eligibility-for-product-upgrade.md)
* [Müşteri için ürün yükseltmesi başlatma](create-product-upgrade-entity.md)
* [Ürün yükseltmesinin durumunu denetleme](get-product-upgrade-status.md)

## <a name="azure-spending"></a>Azure harcaması

Aşağıdaki yöntemleri kullanarak Kullanım Özeti ve ayrıntılı kullanım kayıtlarını sorgulayarak [Azure harcama](azure-spending.md) 'i izleyebilirsiniz:

* [İş ortağı kullanım özeti alma](get-a-partner-usage-summary.md)
* [İş ortağı için tüm müşteri kullanım kayıtlarını alma](get-a-customer-s-usage-records.md)
* [Müşteri kullanım özeti alma](get-a-customer-usage-summary.md)
* [Müşteri için tüm abonelik kullanım kayıtlarını alma](get-a-customer-subscription-s-usage-records.md)
* [Abonelik kullanım özeti alma](get-a-customer-subscription-usage-summary.md)
* [Kaynağa göre abonelik için kullanım verilerini alma](get-a-customer-subscription-resource-usage-records.md)
* [Ölçüme göre abonelik için kullanım verilerini alma](get-a-customer-subscription-meter-usage-records.md)
* [Ölçüm kullanım kaydı kaynaklarını alma](meter-usage-resources.md)
* [Kaynak kullanım kaydı kaynaklarını alma](resource-usage-resources.md)

Ayrıca, aşağıdaki yöntemleri kullanarak müşteri kullanım bütçesini ayarlayabilir ve yönetebilirsiniz:

* [Müşteri kullanım bütçesi alma](get-a-customer-s-usage-spending-budget.md)
* [Müşteri kullanım bütçesi güncelleştirme](update-a-customer-s-usage-spending-budget.md)

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki yöntemleri kullanarak faturaları ve mutabakat verilerini yönetebilirsiniz:

* [Faturaların koleksiyonunu alma](get-a-collection-of-invoices.md)
* [Fatura tahmini bağlantılarını alma](get-invoice-estimate-links.md)
* [Kodu kimliğe göre al](get-invoice-by-id.md)
* [Fatura ekstresini alma](get-invoice-statement.md)
* [Fatura özetlerini alma](get-invoice-summaries.md)
* [Faturalandırılan tüketim satırı öğelerini alma](get-invoice-billed-consumption-lineitems.md)
* [Faturalanmamış tüketim satırı öğelerini alma](get-invoice-unbilled-consumption-lineitems.md)
* [Fatura faturalandırılan keşfi satır öğelerini Al](get-invoiceline-items.md)
* [Faturalanmamış keşif satırı öğelerini alma](get-invoice-unbilled-recon-lineitems.md)
