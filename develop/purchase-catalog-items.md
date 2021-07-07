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
# <a name="purchase-catalog-items"></a>Katalog öğeleri satın alma

Aşağıdaki senaryo, İş Ortağı Merkezi API'sini kullanarak katalogdan ürün satın alma işlemini gösterir.

## <a name="discovery"></a>Bulma

Ürünleri ve Stok Tutma Birimlerini (SKU) seçin ve api modellerinde aşağıdaki İş Ortağı Merkezi kullanılabilirliklerini kontrol edin:

- [Ürün](product-resources.md#product) - Satınlanabilir ürünler veya hizmetler için bir gruplama yapısı. Tek başına ürün, satın edilebilir bir öğe değildir.
- [SKU](product-resources.md#sku) - Ürün altında satınlanabilir bir SKU. Bunlar ürünün farklı şekillerini temsil ediyor.
- [Kullanılabilirlik:](product-resources.md#availability) SKU'nun satın alına hazır olduğu yapılandırma (ülke, para birimi ve sektör segmenti gibi).

Katalogdan bir öğe satın almak için aşağıdaki adımları tamamlayın:

1. Satın almak istediğiniz Ürün ve SKU'ları belirleyin ve alın.

   - [Ürünlerin listesini al](get-a-list-of-products.md)
   - [Ürün kimliğini kullanarak ürün al](get-a-product-by-id.md)
   - [Bir ürün için SKUS listesini al](get-a-list-of-skus-for-a-product.md)
   - [SKU Kimliğini kullanarak SKU'ya sahip olmak](get-a-sku-by-id.md)

2. SKU envanterini denetleme. Bu adım yalnızca [purchasePrerequisites](product-resources.md#sku) özelliğinde **InventoryCheck** değeriyle etiketlenen SKU'lar için gereklidir.

   - [Envanter denetleme](check-inventory.md)

3. SKU [için](product-resources.md#availability) [kullanılabilirliği alın.](product-resources.md#sku) Siparişi sağlarken **kullanılabilirlik CatalogItemId'ye** ihtiyacınız olacak. Bu değeri almak için aşağıdaki API'lerden birini kullanın:

   - [SKU için kullanılabilirlik listesini al](get-a-list-of-availabilities-for-a-sku.md)
   - [Kullanılabilirlik kimliğini kullanarak kullanılabilirlik elde edin](get-an-availability-by-id.md)

## <a name="order-submission"></a>Sipariş gönderimi

Katalog öğesi siparişinizi göndermek için şunları yapın:

1. Satın almayı [istediğiniz](cart-resources.md) katalog öğelerinin koleksiyonunu tutmak için bir Sepet oluşturun. Bir sepet oluşturma sırasında, [sepet satır öğeleri](cart-resources.md#cartlineitem) aynı Sipariş içinde birlikte satın alınarak nelerin satın alınarak otomatik olarak [gruplanır.](order-resources.md)

   - [Alışveriş sepeti oluşturma](create-a-cart.md)
   - [Alışveriş sepetini güncelleştirme](update-a-cart.md)

2. Sepete göz at. Sepete göz atarak Sipariş oluşturulmasına neden [olur.](order-resources.md)

   - [Sepete göz at](checkout-a-cart.md)

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

Sipariş kimliğini kullanarak tek bir siparişin ayrıntılarını alabilir veya müşteri için siparişlerin listesini edinebilirsiniz. Bir siparişin gönderilme zamanı ile müşterinin sipariş listesinde görünmesi arasında 15 dakikaya kadar bir gecikme olur.

- Sipariş [kimliklerini kullanarak tek bir](get-an-order-by-id.md) siparişin ayrıntılarını almak için bkz. Kimliklere göre sipariş al.

- Müşteri [kimliğini kullanarak bir müşterinin sipariş listesini](get-all-of-a-customer-s-orders.md) almak için bkz. Müşterinin tüm siparişlerini alma.

- Katalog [öğesi siparişlerini](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) (tek defalık ücretler) ve yıllık veya [](product-resources.md#billingcycletype) aylık faturalandırılabilir siparişleri ayrı olarak listeleyebilirsiniz. Faturalama döngüsü türüne göre bir müşteriye yönelik siparişlerin listesini almak için bkz. Müşteriye ve faturalama döngüsü türüne göre siparişlerin listesini alma.

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

İş Ortağı Merkezi'de katalog öğelerinizin yaşam döngüsünün yönetilmesinin bir parçası olarak, katalog [](entitlement-resources.md)öğesi Yetkilendirmeleri hakkında bilgi alabilir ve rezervasyon sipariş kimliğini kullanarak rezervasyon ayrıntılarını edinebilirsiniz. Bunu yapma örnekleri için bkz. [Yetkilendirmeleri al.](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki senaryolar, müşterinizin faturalarını program aracılığıyla [](invoice-resources.md)görüntülemeyi ve katalog öğeleri için tek sefer ücretleri içeren hesap bakiyelerinizi ve özetlerinizi nasıl alasınız?

### <a name="balance-and-payment"></a>Bakiye ve ödeme

Hem yinelenen hem de bir defalık (katalog öğesi) ücretlerinin bakiyesi olan varsayılan para birimi türünüz için geçerli hesap bakiyenizi almak için bkz. [Geçerli hesap bakiyenizi al.](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Çoklu para birimi bakiyesi ve ödeme

Geçerli hesap bakiyenizi ve her müşterinizin para birimi türleri için hem yinelenen hem de tek defalık ücretleri içeren bir fatura özeti içeren fatura özetleri koleksiyonunu almak için [bkz. Fatura özetlerini alın.](get-invoice-summaries.md)

### <a name="invoices"></a>Faturalar

Hem yinelenen hem de tek seferlik ücretlerin yer alan bir fatura koleksiyonunu almak için bkz. Fatura [koleksiyonu alın.](get-a-collection-of-invoices.md) 

### <a name="single-invoice"></a>Tek Fatura

Fatura kimliğini kullanarak belirli bir faturayı almak için [bkz. Kimliğine göre fatura alma.](get-invoice-by-id.md)  

### <a name="reconciliation"></a>Uzlaşma

Belirli bir fatura kimliğine ilişkin fatura satırı öğesi ayrıntılarının (Mutabakat satır öğeleri) koleksiyonunu almak için [bkz. Fatura satırı öğelerini al.](get-invoiceline-items.md)  

### <a name="download-an-invoice-as-a-pdf"></a>Faturayı PDF olarak indirme

Fatura kimliği kullanarak PDF formunda fatura deyimi almak için bkz. [Fatura deyimi alma.](get-invoice-statement.md)
