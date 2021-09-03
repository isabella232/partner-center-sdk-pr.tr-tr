---
title: Yeni ticaret lisansı tabanlı hizmetler satın alın
description: Geliştiriciler, Iş Ortağı Merkezi API 'Lerini kullanarak yeni ticaret lisansı tabanlı hizmetler satın alabilir, oluşturabilir ve yönetebilir.
ms.date: 02/24/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: dd3aebdb0a670449d3a39f67fc2ad6c7ef8df8e5
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457336"
---
# <a name="purchasing-new-commerce-license-based-services"></a>Yeni ticaret lisansı tabanlı hizmetler satın alma

**Uygulama hedefi:**

* İş Ortağı Merkezi

> [!Note] 
> Yeni ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinin parçası olan iş ortakları tarafından kullanılabilir.

Iş Ortağı Merkezi API 'Lerini kullanarak yeni ticari deneyim lisans tabanlı hizmetler satın alabilir, oluşturabilir ve yönetebilirsiniz. İşlem, Azure planı ve Market teklifleri gibi benzerdir.

## <a name="prerequisites"></a>Önkoşullar

* [Iş ortağı merkezi kimlik doğrulama](partner-center-authentication.md) bilgileri. Yeni ticaret deneyimi hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.
* Müşteri tanımlayıcısı. Müşterinin tanımlayıcısı yoksa, [müşterilerin listesini al](get-a-list-of-customers.md)bölümündeki adımları izleyin. Alternatif olarak, Iş Ortağı Merkezi ' nde oturum açın, müşteri listesinden müşteriyi seçin, **Hesap**' ı seçin ve **Microsoft kimliklerini** kaydedin.
* [Müşterinin Microsoft Müşteri sözleşmesinin kabul edilmesine yönelik onay](/partner-center/confirm-customer-agreement).

## <a name="get-the-catalog-item-for-new-commerce-license-based-services"></a>Yeni ticaret lisansı tabanlı hizmetler için Katalog öğesini al

Yeni ticari lisans tabanlı hizmetler katalog öğelerini almanız gerekir. Aşağıdaki kaynak modelleriyle mevcut Iş Ortağı Merkezi katalog API 'Lerini kullanarak katalog öğelerini alın:

* **[Ürün](product-resources.md#product)**: satın alınabilir alınırken mallar veya hizmetler için gruplama yapısı. Ürünün kendisi bir satın alınabilir alınırken öğesi değil.
* **[SKU](product-resources.md#sku)**: bir ürün altındaki satın alınabilir alınırken stok tutma BIRIMI (SKU). SKU 'Lar ürünün farklı şekillerini temsil eder.
* **[Kullanılabilirlik](product-resources.md#availability)**: BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi veya sektör segmenti gibi).

Yeni ticaret lisansı tabanlı hizmetler için katalog öğelerini almak üzere:

1. Ürünlerin [ürünlerin listesini alın](get-a-list-of-products.md) ve **Targetview** 'ı **OnlineServices** olarak belirtin. (Satın almak istediğiniz teklifin ürün tanımlayıcısını zaten biliyorsanız, bunun yerine [ürün kimliği kullanarak ürün alma](get-a-product-by-id.md) bölümündeki adımları izleyebilirsiniz.)

2. Aradığınız teklifin ürün **SKU** 'sunu alın. [Bir ürün Için SKU 'ların listesini alın](get-a-list-of-skus-for-a-product.md)bölümündeki adımları izleyin. (İstediğiniz teklif için SKU kimliğini zaten biliyorsanız, bunun yerine SKU [kimliğini kullanarak SKU al](get-a-sku-by-id.md) bölümündeki adımları izleyebilirsiniz.)

3. Teklif için SKU 'dan **kullanılabilirliği** alın. Farklı teklifler, belirli koşulları destekler. Bazı SKU 'Ların birden fazla kullanılabilirliği vardır. [SKU 'nun kullanılabilirliği listesini al](get-a-list-of-availabilities-for-a-sku.md)bölümündeki adımları izleyin. (İhtiyacınız olan kullanılabilirlik için tanımlayıcıyı zaten biliyorsanız, bunun yerine [KULLANıLABILIRLIK kimliğini kullanarak kullanılabilirlik al](get-an-availability-by-id.md) ' daki adımları izleyebilirsiniz.) *Teklifin kullanılabilirliğine ait **catalogıtemıd** özelliğinin değerini aklınızda olduğunuzdan emin olun. Sipariş oluşturmak için bu değere ihtiyacınız olacaktır*.

## <a name="create-and-submit-an-order"></a>Sipariş oluşturma ve gönderme

Bir Azure planına yönelik siparişinizi (yeni ticaret siparişleri dahil) göndermek için şu adımları izleyin:

1. Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için [bir sepet oluşturun](create-a-cart.md) . Bir [sepet](cart-resources.md#cart)oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md#order)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır. ( [Bir sepet de güncelleştirebilirsiniz](update-a-cart.md).)

2. Bir [sipariş](order-resources.md#order)oluşturulmasına neden olan [sepete](checkout-a-cart.md)göz atın.

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

[SIPARIŞ kimliğini kullanarak tek bir siparişin ayrıntılarını alabilirsiniz](get-an-order-by-id.md). Ayrıca, [belirli bir müşterinin tüm siparişlerinin listesini alabilirsiniz](get-all-of-a-customer-s-orders.md).

>[!NOTE]
>Sipariş gönderdikten sonra, bu müşterinin sıra listesinde görüntülenmeden önce 15 dakikaya kadar bir gecikme olur. Şu anda, AB iş ortakları yalnızca yeni ticari teklifler satın alabilir: 1. Yeni müşteriler 2. Önceden var olan bir Azure planına, Market 'e, yazılım aboneliğine veya kalıcı yazılıma, iş ortağının ülke para biriminden başka bir para birimiyle sahip olmayan mevcut müşteriler.

## <a name="manage-new-commerce-subscriptions"></a>Yeni ticari abonelikleri yönetme

Sipariş başarıyla işlendikten sonra Azure planı için bir Iş Ortağı Merkezi **abonelik** kaynağı oluşturulur. Azure planını yönetmek üzere Iş Ortağı Merkezi **abonelik** kaynaklarını yönetmek için aşağıdaki yöntemleri kullanabilirsiniz:

* [Müşterinin aboneliğini alma](get-all-of-a-customer-s-subscriptions.md)
* [Siparişe göre aboneliklerin bir listesini alma](get-a-list-of-subscriptions-by-order.md)

Yeni ticarete özgü farklar ve yeni yetenekler vardır.

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
