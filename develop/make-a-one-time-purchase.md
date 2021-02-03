---
title: Tek seferlik satın alım yapma
description: Iş Ortağı Merkezi API 'sini kullanarak yazılım abonelikleri, kalıcı yazılımlar ve Azure ayrılmış sanal makine (VM) örnekleri gibi yazılım ve rezervasyon ürünlerini tek seferlik satın alma.
ms.date: 10/09/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 17a5f5c1e845ba36a94d7ce909df30e0146ba448
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768902"
---
# <a name="make-a-one-time-purchase"></a>Tek seferlik satın alım yapma

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Iş Ortağı Merkezi API 'sini kullanarak yazılım abonelikleri, kalıcı yazılımlar ve Azure ayrılmış sanal makine (VM) örnekleri gibi yazılım ve rezervasyon ürünlerini tek seferlik satın alma.

> [!NOTE]
> Yazılım abonelikleri aşağıdaki pazarlarda kullanılamaz:
>
> | Kullanılamayan pazarlar            | Kullanılamayan pazarlar (devam eden...) | Kullanılamayan pazarlar (devam eden...)      |
> |--------------------------------|-----------------------------------|------------------------------------------|
> | Bir i Adaları                  | Grönland                         | Papua Yeni Gine                         |
> | Amerikan Samoası                 | Grenada                           | Pitcairn Adaları                         |
> | Andorra                        | Guadeloupe                        | Reunion                                  |
> | Anguilla                       | Guam                              | Rusya Federasyonu                       |
> | Antarktika                     | Guernsey                          | Saba                                     |
> | Antigua ve Barbuda            | Gine                            | Saint Barthelemy                         |
> | Aruba                          | Gine-Bissau                     | Saint Lucia                              |
> | Benin                          | Guyana                            | Saint Martin                             |
> | Butan                         | Haiti                             | Saint Pierre ve Miquelon                |
> | Bonaire                        | Heard Adası ve McDonald Adaları | Saint Vincent ve Grenadinler         |
> | Bouvet Adası                  | Man Adası                       | Samoa                                    |
> | Brezilya                         | Jan Mayen                         | San Marino                               |
> | Britanya Hint Okyanusu Toprakları | Jersey                            | Sao Tome ve Principe                    |
> | Britanya Virjin Adaları         | Kiribati                          | Seyşeller                               |
> | Burkina Faso                   | Kosova                            | Sierra Leone                             |
> | Burundi                        | Laos                              | Sint Eustatius                           |
> | Kamboçya                       | Lesotho                           | Sint Maarten                             |
> | Orta Afrika Cumhuriyeti       | Liberya                           | Solomon Adaları                          |
> | Çad                           | Madagaskar                        | Somali                                  |
> | Çin                          | Malavi                            | Güney Georgia ve Güney Sandwich Adaları |
> | Christmas Adası               | Maldivler                          | Güney Sudan                              |
> | Cocos (Keeling) Adaları        | Mali                              | Saint Helena, Ascension ve Tristan da Cunha   |
> | Komorlar                        | Marshall Adaları                  | Surinam                                 |
> | Kongo Cumhuriyeti                          | Martinique                        | Svalbard                                 |
> | Kongo (KDC)                    | Moritanya                        | Svaziland                                |
> | Cook Adaları                   | Mayotte                           | Timor-Leste                              |
> | Cibuti                       | Mikronezya                        | Togo                                     |
> | Dominika                       | Montserrat                        | Tokelau                                  |
> | Ekvator Ginesi              | Mozambik                        | Tonga                                    |
> | Eritre                        | Myanmar                           | Turks ve Caicos Adaları                 |
> | Falkland Adaları               | Nauru                             | Tuvalu                                   |
> | Fransız Guyanası                  | Yeni Kaledonya                     | ABD harici Adaları                    |
> | Fransız Polinezyası               | Nijer                             | Vanuatu                                  |
> | Fransız Güney Toprakları    | Niue                              | Vatikan                             |
> | Gabon                          | Norfolk Adası                    | Wallis ve Futuna                        |
> | Gambiya                         | Kuzey Mariana Adaları          | Yemen                                    |
> | Cebelitarık                      | Palau                             | &nbsp;                                   |
>
&nbsp;
> [!NOTE]
> Kalıcı yazılım satın almak için önceden nitelenmiş olmanız gerekir. Daha fazla bilgi için desteğe başvurun.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="making-a-one-time-purchase"></a>Tek seferlik satın alma yapma

Tek seferlik satın alma yapmak için aşağıdaki adımları kullanın:

1. [Etkinleştirme](#enablement) -(yalnızca Azure ayrılmış VM örneği), herhangi bir rezervasyon ürününün satın alınmasını sağlamak için ETKIN bir CSP Azure aboneliğini kaydeder.

2. [Bulma](#discovery) -satın almak istediğiniz ürünleri ve SKU 'ları bulup seçin ve kullanılabilirliğini denetleyin.

3. [Sipariş gönderimi](#order-submission) -sıralarınızın öğeleriyle birlikte bir alışveriş sepeti oluşturun ve gönderebilirsiniz.

4. [Sipariş ayrıntılarını al](#get-order-details) -bir siparişin ayrıntılarını, bir müşteriye ait tüm siparişleri gözden geçirin veya faturalandırma dönem türüne göre siparişleri görüntüleyin.

Tek seferlik satın alımınızın ardından, aşağıdaki senaryolarda, yetkilendirmelerinizle ilgili bilgi alarak ve bilanço özetleri, faturaların ve fatura özetlerinin nasıl alınacağının yanı sıra ürünlerin yaşam döngüsünün nasıl yönetileceği gösterilmektedir.

- [Yaşam döngüsü yönetimi](#lifecycle-management)

- [Fatura ve mutabakat](#invoice-and-reconciliation)

## <a name="enablement"></a>Geçerlilik

Azure ayrılmış VM örneğini eklemek istediğiniz etkin aboneliği tanımladıktan sonra, bu aboneliği etkin hale gelecek şekilde kaydetmeniz gerekir. Mevcut bir [abonelik](subscription-resources.md) kaynağını, etkin olacak şekilde kaydetmek için bkz. [abonelik kaydetme](register-a-subscription.md).

Aboneliğinizi kaydettikten sonra kayıt durumunu denetleyerek kayıt işleminin tamamlandığını onaylamanız gerekir. Bu adımı yapmak için bkz. [abonelik kayıt durumunu Al](get-subscription-registration-status.md).

## <a name="discovery"></a>Bulma

Abonelik etkinleştirildikten sonra, ürün ve SKU 'Ları seçip aşağıdaki Iş Ortağı Merkezi API modellerini kullanarak kullanılabilirliğini kontrol etmeye hazır olursunuz:

- [Ürün](product-resources.md#product) -satın alınabilir alınırken malları veya hizmetleri için gruplama yapısı. Bir ürünün kendisi bir satın alınabilir alınırken öğesi değil.

- [SKU](product-resources.md#sku) -bir ürün altında bir satın alınabilir alınırken stok tutma BIRIMI (SKU). SKU 'Lar ürünün farklı şekillerini temsil eder.

- [Kullanılabilirlik](product-resources.md#availability) -BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi ve sektör segmenti gibi).

Bir kerelik satın alma yapmadan önce aşağıdaki adımları izleyin:

1. Satın almak istediğiniz ürün ve SKU 'YU belirleyip alın. Bu adımı, önce ürün ve SKU 'Ları listeleyerek veya ürün ve SKU 'nun kimliklerini zaten biliyorsanız, bunları seçerek yapabilirsiniz.

   - [Ürünlerin bir listesini alın](get-a-list-of-products.md)
   - [Ürün KIMLIĞINI kullanarak bir ürün alın](get-a-product-by-id.md)
   - [Ürün için SKU 'ların listesini alın](get-a-list-of-skus-for-a-product.md)
   - [SKU KIMLIĞI kullanarak bir SKU al](get-a-sku-by-id.md)

2. Bir SKU için envanteri denetleyin. Bu adım yalnızca bir **ınventorycheck** önkoşulu Ile etiketlenmiş SKU 'lar için gereklidir.

   - [Envanter denetleme](check-inventory.md)

3. [SKU](product-resources.md#sku)için [kullanılabilirliği](product-resources.md#availability) alın. Siparişi yerleştirirken kullanılabilirliğin **Catalogıtemıd** öğesine ihtiyacınız olacaktır. Bu değeri almak için aşağıdaki API 'lerden birini kullanın:

   - [SKU 'nun kullanılabilirliği listesini alın](get-a-list-of-availabilities-for-a-sku.md)
   - [Kullanılabilirlik KIMLIĞINI kullanarak bir kullanılabilirlik alın](get-an-availability-by-id.md)

## <a name="order-submission"></a>Sipariş gönderimi

Siparişinizi göndermek için şu adımları izleyin:

1. Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için bir sepet oluşturun. Bir [sepet](cart-resources.md)oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır.

   - [Alışveriş sepeti oluşturma](create-a-cart.md)
   - [Bir alışveriş sepetini güncelleştirme](update-a-cart.md)

2. Sepete göz atın. Sepetin kullanıma hazır olması, bir [sipariş](order-resources.md)oluşturulmasına neden olur.

   - [Sepetini kullanıma alın](checkout-a-cart.md)

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

Siparişinizi oluşturduktan sonra, sipariş KIMLIĞINI kullanarak tek bir siparişin ayrıntılarını alabilir veya bir müşteri siparişlerinin listesini alabilirsiniz. Bir siparişin gönderildiği ve müşterinin siparişlerinin listesinde görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.

- Sipariş KIMLIĞINI kullanarak tek bir siparişin ayrıntılarını almak için. Bkz. [bir SIPARIŞI kimliğe göre alın](get-an-order-by-id.md).

- Müşteri KIMLIĞINI kullanarak bir müşterinin siparişlerinin listesini almak için. Bkz. [bir müşterinin siparişlerinin tümünü alın](get-all-of-a-customer-s-orders.md).

- [Fatura döngüsüne](product-resources.md#billingcycletype) göre bir müşterinin siparişlerinin listesini almak için, siparişleri (tek seferlik ücretler) ve yıllık veya aylık olarak faturalandırılan siparişleri ayrı olarak listelemenize olanak sağlar. Bkz. [müşteri ve faturalandırma dönem türüne göre siparişlerin listesini alın](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

Iş Ortağı Merkezi 'nde tek seferlik satın alımlarının yaşam döngüsünü yönetmenin bir parçası olarak, [yetkilendirmelerinizi](entitlement-resources.md)hakkında bilgi alabilir ve rezervasyon siparişi kimliğini kullanarak rezervasyon ayrıntılarını alabilirsiniz. Bunun nasıl yapılacağı hakkında örnekler için bkz. [yetkilendirmeleri alma](get-a-collection-of-entitlements.md).

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki senaryolarda, müşterinizin [faturalarını](invoice-resources.md)programlamayla görüntüleme ve tek seferlik ücretler içeren Hesap bakiyeleriniz ve özetler alma işlemlerinin nasıl yapılacağı gösterilmektedir.

### <a name="balance-and-payment"></a>Bakiye ve ödeme

Yinelenen ve tek seferlik ücretler bakiyesi olan varsayılan para birimi türünde güncel hesap bakiyesini almak için, bkz. [geçerli hesap bakiyenizi edinme](get-the-reseller-s-current-account-balance.md)

### <a name="multi-currency-balance-and-payment"></a>Çoklu para birimi bakiyesi ve ödemesi

Geçerli hesap bakiyenizi ve müşterinizin para birimi türlerinden her biri için hem yinelenen hem de tek seferlik ücretler içeren bir fatura Özeti içeren bir fatura özetleri koleksiyonu ve bir fatura Özeti koleksiyonu almak için bkz. [Fatura özetlerini al](get-invoice-summaries.md).

### <a name="invoices"></a>Faturalar

Hem yinelenen hem de bir zaman ücreti gösteren faturaların bir koleksiyonunu almak için, bkz. [faturaların toplanmasını edinme](get-a-collection-of-invoices.md).

### <a name="single-invoice"></a>Tek fatura

Fatura KIMLIĞINI kullanarak belirli bir faturayı almak için bkz. [kimliğe göre fatura alma](get-invoice-by-id.md).

### <a name="reconciliation"></a>Katına

Belirli bir fatura KIMLIĞI için fatura satırı öğe ayrıntılarının (mutabakat satır öğeleri) bir koleksiyonunu almak için bkz. [fatura satırı öğelerini Al](get-invoiceline-items.md).

### <a name="download-an-invoice-as-a-pdf"></a>Bir faturayı PDF olarak indirme

Fatura KIMLIĞI kullanarak PDF formundaki fatura ekstresini almak için bkz. [Fatura alma ekstresi](get-invoice-statement.md).
