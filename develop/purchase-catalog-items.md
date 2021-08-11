---
title: Katalog öğeleri satın alma
description: Iş Ortağı Merkezi API 'sini kullanarak katalog öğeleri satın alma.
ms.date: 07/12/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 34560ceff2721a805d50cd4bf0702f6e7cf6f473db3f38ee52ea439b7355b786
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997353"
---
# <a name="purchase-catalog-items"></a>Katalog öğeleri satın alma

Aşağıdaki senaryoda, Iş Ortağı Merkezi API 'sini kullanarak katalogdan öğe satın alma genel işlemi gösterilmektedir.

## <a name="discovery"></a>Bulma

Ürünleri ve stok tutma birimlerini (SKU 'Lar) seçin ve aşağıdaki Iş Ortağı Merkezi API modellerini kullanarak kullanılabilirliğini kontrol edin:

- [Ürün](product-resources.md#product) -satın alınabilir alınırken malları veya hizmetleri için gruplama yapısı. Bir ürünün kendisi bir satın alınabilir alınırken öğesi değil.
- [SKU](product-resources.md#sku) -bir ürün altında bir satın alınabilir alınırken SKU 'su. Bunlar, ürünün farklı şekillerini temsil eder.
- [Kullanılabilirlik](product-resources.md#availability) -BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi ve sektör segmenti gibi).

Katalogdan bir öğe satın almak için aşağıdaki adımları izleyin:

1. Satın almak istediğiniz ürün ve SKU 'YU belirleyip alın.

   - [Ürünlerin bir listesini alın](get-a-list-of-products.md)
   - [Ürün KIMLIĞINI kullanarak bir ürün alın](get-a-product-by-id.md)
   - [Ürün için SKU 'ların listesini alın](get-a-list-of-skus-for-a-product.md)
   - [SKU KIMLIĞI kullanarak bir SKU al](get-a-sku-by-id.md)

2. Bir SKU için envanteri denetleyin. Bu adım yalnızca [purchasePrerequisites](product-resources.md#sku) özelliğindeki bir **ınventorycheck** değeri ile etiketlenmiş SKU 'lar için gereklidir.

   - [Envanter denetleme](check-inventory.md)

3. [SKU](product-resources.md#sku)için [kullanılabilirliği](product-resources.md#availability) alın. Siparişi yerleştirirken kullanılabilirliğin **Catalogıtemıd** öğesine ihtiyacınız olacaktır. Bu değeri almak için aşağıdaki API 'lerden birini kullanın:

   - [SKU 'nun kullanılabilirliği listesini alın](get-a-list-of-availabilities-for-a-sku.md)
   - [Kullanılabilirlik KIMLIĞINI kullanarak bir kullanılabilirlik alın](get-an-availability-by-id.md)

## <a name="order-submission"></a>Sipariş gönderimi

Katalog öğesi siparişinizi göndermek için aşağıdakileri yapın:

1. Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için bir [sepet](cart-resources.md) oluşturun. Bir sepet oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır.

   - [Alışveriş sepeti oluşturma](create-a-cart.md)
   - [Bir alışveriş sepetini güncelleştirme](update-a-cart.md)

2. Sepete göz atın. Sepetin kullanıma hazır olması, bir [sipariş](order-resources.md)oluşturulmasına neden olur.

   - [Sepetini kullanıma alın](checkout-a-cart.md)

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

Sipariş KIMLIĞINI kullanarak tek bir siparişin ayrıntılarını alabilir veya bir müşteri siparişlerinin listesini alabilirsiniz. Bir siparişin gönderildiği ve müşterinin siparişlerinin listesinde görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.

- Sipariş kimliklerini kullanarak tek bir siparişin ayrıntılarını almak için bkz. [order by ID Get](get-an-order-by-id.md) .

- Müşteri KIMLIĞINI kullanarak müşterinin siparişlerinin listesini almak için [müşterinin siparişlerinin tümünü alın](get-all-of-a-customer-s-orders.md) konusuna bakın.

- Bir müşteri siparişlerinin listesini almak için bkz. [müşteri ve faturalandırma](get-a-list-of-orders-by-customer-and-billing-cycle-type.md) döngüsüne göre siparişlerin listesini almak için, katalog öğesi siparişlerini (tek seferlik ücretler) ve yıllık veya aylık faturalandırılan siparişleri ayrı olarak [listelemenize olanak](product-resources.md#billingcycletype) tanır.

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

Iş Ortağı Merkezi 'nde Katalog öğelerinizin yaşam döngüsünü yönetmenin bir parçası olarak, katalog öğesi [yetkilendirmelerinizin](entitlement-resources.md)bilgilerini alabilir ve rezervasyon siparişi kimliğini kullanarak rezervasyon ayrıntılarını alabilirsiniz. Bunun nasıl yapılacağı hakkında örnekler için bkz. [yetkilendirmeleri alma](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki senaryolarda, müşterinizin [faturalarını](invoice-resources.md)programlamayla görüntüleme ve katalog öğeleri için tek seferlik ücretler içeren Hesap bakiyeleriniz ve özetler alma işlemlerinin nasıl yapılacağı gösterilmektedir.

### <a name="balance-and-payment"></a>Bakiye ve ödeme

Hem yinelenen hem de tek seferlik (katalog öğesi) ücretlerine ait bir bakiye olan varsayılan para birimi türünde güncel hesap bakiyesini almak için, bkz. [geçerli hesap bakiyenizi alın](get-the-reseller-s-current-account-balance.md).

### <a name="multi-currency-balance-and-payment"></a>Çoklu para birimi bakiyesi ve ödemesi

Geçerli hesap bakiyenizi ve müşterinizin para birimi türlerinden her biri için hem yinelenen hem de tek seferlik ücretler içeren bir fatura Özeti içeren bir fatura özetleri koleksiyonu ve bir fatura Özeti koleksiyonu almak için bkz. [Fatura özetlerini al](get-invoice-summaries.md).

### <a name="invoices"></a>Faturalar

Yinelenen ve tek seferlik ücretleri gösteren faturaların bir koleksiyonunu almak için, bkz. [faturaların toplanmasını edinme](get-a-collection-of-invoices.md). 

### <a name="single-invoice"></a>Tek fatura

Fatura KIMLIĞINI kullanarak belirli bir faturayı almak için bkz. [kimliğe göre fatura alma](get-invoice-by-id.md).  

### <a name="reconciliation"></a>Katına

Belirli bir fatura KIMLIĞI için fatura satırı öğe ayrıntılarının (mutabakat satır öğeleri) bir koleksiyonunu almak için bkz. [fatura satırı öğelerini Al](get-invoiceline-items.md).  

### <a name="download-an-invoice-as-a-pdf"></a>Bir faturayı PDF olarak indirme

Fatura KIMLIĞI kullanarak PDF formundaki fatura ekstresini almak için bkz. [Fatura alma ekstresi](get-invoice-statement.md).
