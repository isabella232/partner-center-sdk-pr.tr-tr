---
title: Azure rezervasyonları satın alma
description: mevcut Microsoft Azure aboneliğiniz (MS-azr-0145p) veya Azure planı aracılığıyla iş ortağı merkezi apı 'sini kullanarak bir müşteri için Azure ayırmaları satın alabilirsiniz.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b9ce4a808ac12c32bd67888fc92808baeb0e575
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547776"
---
# <a name="purchase-azure-reservations"></a>Azure rezervasyonları satın alma

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

iş ortağı merkezi apı 'sini kullanarak bir müşterinin Azure ayırmasını satın almak için, mevcut bir Microsoft Azure (**MS-azr-0145p**) aboneliğine veya azure planına sahip olmanız gerekir.

> [!NOTE]
> Azure ayırmaları aşağıdaki pazarlarda kullanılamaz:
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

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Etkin bir CSP Azure aboneliğine veya bir Azure planına yönelik abonelik KIMLIĞI.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Microsoft Azure ayırmaları satın alma

Azure ayırması eklemek istediğiniz etkin CSP Azure aboneliğini tanımladıktan sonra satın almak için aşağıdaki adımları kullanın:

1. [Etkinleştirme](#enablement) -Azure ayırmaları satın almak üzere etkinleştirmek için ETKIN bir CSP Azure aboneliğini kaydedin.

2. [Bulma](#discovery) -satın almak istediğiniz Azure rezervasyon ürünlerini ve stok tutma birimlerini (SKU 'lar) bulun ve seçin ve bunların kullanılabilirliğini kontrol edin.

3. [Sipariş gönderimi](#order-submission) -sıralarınızın öğeleriyle birlikte bir alışveriş sepeti oluşturun ve gönderebilirsiniz.

4. [Sipariş ayrıntılarını al](#get-order-details) -bir siparişin ayrıntılarını, bir müşteriye ait tüm siparişleri gözden geçirin veya faturalandırma dönem türüne göre siparişleri görüntüleyin.

Azure ayırmaları satın aldıktan sonra, aşağıdaki senaryolarda Azure rezervasyon yetkilendirmelerinizi ve bilanço özetlerini, faturaları ve fatura özetlerini alma hakkında bilgi alarak yaşam döngüsünü nasıl yöneteceğiniz gösterilmektedir.

- [Yaşam döngüsü yönetimi](#lifecycle-management)
- [Fatura ve mutabakat](#invoice-and-reconciliation)

## <a name="enablement"></a>Geçerlilik

etkinleştirme, aboneliği azure ayırmaları için etkinleştirilecek şekilde kaydederek mevcut bir Microsoft Azure (**MS-azr-0145p**) aboneliğini bir azure ayrılmış VM örneğine ilişkilendirme anlamına gelir. Kayıt, Azure ayrılmış VM örnekleri satın almak için bir önkoşuldur.

Aşağıdaki görevleri desteklemek için bir abonelik gereklidir:

1. Müşterinin kaynakları dağıtmaya uygun olup olmadığını ve bu nedenle Azure ayrılmış VM örneklerini bir bölgede satın alıp almadığından emin olun.

2. Bir abonelikteki dağıtımlar için kapasite önceliği sağlamak üzere. Bu, yalnızca **Kapasite önceliği** seçeneği belirlenmiş olan Azure ayrılmış sanal makine örneklerine yönelik tek kapsam için geçerlidir.

Azure ayırmasını eklemek istediğiniz etkin aboneliği tanımladıktan sonra, aboneliği Azure ayırmaları için etkinleştirilecek şekilde kaydetmeniz gerekir. Mevcut bir [abonelik](subscription-resources.md) kaynağını Azure ayırmalarını sıralamak üzere etkinleştirilecek şekilde kaydetmek için bkz. [bir aboneliği kaydetme](register-a-subscription.md).

Aboneliğinizi kaydettikten sonra kayıt durumunu denetleyerek kayıt işleminin tamamlandığını onaylamanız gerekir. Bunu yapmak için bkz. [abonelik kayıt durumunu Al](get-subscription-registration-status.md).

> [!NOTE]
> azure planına sahip bir müşterinin Microsoft Azure ayırmasını satın alırken önce azure planını kaydetmeniz gerekir. bir Microsoft Azure (**MS-azr-0145p**) aboneliğine benzer şekilde, bir Azure planı bir iş ortağı merkezi [abonelik](subscription-resources.md) kaynağıyla temsil edilir. Bu nedenle, bir Azure planını kaydetmek için aynı [aboneliği kaydet](register-a-subscription.md) yöntemini kullanabilirsiniz.

## <a name="discovery"></a>Bulma

Abonelik, Azure ayırmaları satın alma için etkinleştirildikten sonra, ürün ve SKU 'Ları seçip aşağıdaki Iş Ortağı Merkezi API modellerini kullanarak kullanılabilirliğini kontrol etmeye hazır olursunuz:

- [Ürün](product-resources.md#product) -satın alınabilir alınırken malları veya hizmetleri için gruplama yapısı. Bir ürünün kendisi bir satın alınabilir alınırken öğesi değil.

- [SKU](product-resources.md#sku) -bir ürün altında bir satın alınabilir alınırken SKU 'su. Bunlar, ürünün farklı şekillerini temsil eder.

- [Kullanılabilirlik](product-resources.md#availability) -BIR SKU 'nun satın alma için kullanılabildiği bir yapılandırma (ülke, para birimi ve sektör segmenti gibi).

Bir Azure ayırması satın almadan önce, aşağıdaki adımları izleyin:

1. Satın almak istediğiniz ürün ve SKU 'YU belirleyip alın. Bunu, önce ürün ve SKU 'Ları listeleyerek ya da ürün ve SKU kimliklerini zaten biliyorsanız, seçerek yapabilirsiniz.

   - [Ürünlerin bir listesini alma (ülkeye göre)](get-a-list-of-products.md)
   - [Ürün KIMLIĞINI kullanarak bir ürün alın](get-a-product-by-id.md)
   - [Bir ürüne ait SKU’ların listesini alma (ülkeye göre)](get-a-list-of-skus-for-a-product.md)
   - [SKU KIMLIĞI kullanarak bir SKU al](get-a-sku-by-id.md)

2. Bir SKU için envanteri denetleyin. Bu adım yalnızca bir **ınventorycheck** önkoşulu Ile etiketlenmiş SKU 'lar için gereklidir.

   - [Envanter denetleme](check-inventory.md)

3. [SKU](product-resources.md#sku)için [kullanılabilirliği](product-resources.md#availability) alın. Siparişi yerleştirirken kullanılabilirliğin **Catalogıtemıd** öğesine ihtiyacınız olacaktır. Bu değeri almak için aşağıdaki API 'lerden birini kullanın:

   - [Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma](get-a-list-of-availabilities-for-a-sku.md)
   - [Kullanılabilirlik KIMLIĞINI kullanarak bir kullanılabilirlik alın](get-an-availability-by-id.md)

> [!IMPORTANT]
> her bir Microsoft Azure rezervasyon ürününde Microsoft Azure (**MS-azr-0145p**) aboneliği ve Azure planına ait farklı kullanılabilirlik vardır. [Ürünlerin bir listesini (ülkeye göre](get-a-list-of-products.md)) veya bir [ürüne ait SKU](get-a-list-of-skus-for-a-product.md)'ların bir listesini alın (ülkeye göre) veya yalnızca Azure planına uygulanabilen [bir SKU (ülkeye göre) için kullanılabilirlik](get-a-list-of-availabilities-for-a-sku.md) listesi alın, "rezervationscope = azuplan" parametresini belirtin.

## <a name="order-submission"></a>Sipariş gönderimi

Azure rezervasyon siparişinizi göndermek için aşağıdaki görevleri yapın:

1. Satın almayı planladığınız Katalog öğelerinin koleksiyonunu tutmak için bir sepet oluşturun. Bir [sepet](cart-resources.md)oluşturduğunuzda, [sepet çizgisi öğeleri](cart-resources.md#cartlineitem) aynı [sırada](order-resources.md)birlikte satın alınabilecek öğelere göre otomatik olarak gruplandırılır.

   - [Alışveriş sepeti oluşturma](create-a-cart.md)
   - [Bir alışveriş sepetini güncelleştirme](update-a-cart.md)

2. Sepete göz atın. Sepetin kullanıma hazır olması, bir [sipariş](order-resources.md)oluşturulmasına neden olur.

   - [Sepetini kullanıma alın](checkout-a-cart.md)

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

Azure rezervasyon siparişinizi oluşturduktan sonra, sipariş KIMLIĞINI kullanarak tek bir siparişin ayrıntılarını alabilir veya bir müşteri siparişlerinin listesini alabilirsiniz. Bir siparişin gönderildiği ve müşterinin siparişlerinin listesinde görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.

- Sipariş KIMLIĞINI kullanarak tek bir siparişin ayrıntılarını almak için. Bkz. [bir SIPARIŞI kimliğe göre alın](get-an-order-by-id.md).

- Müşteri KIMLIĞINI kullanarak bir müşterinin siparişlerinin listesini almak için. Bkz. [bir müşterinin siparişlerinin tümünü alın](get-all-of-a-customer-s-orders.md).

- [Fatura döngüsüne](product-resources.md#billingcycletype) göre müşterinin siparişlerinin bir listesini almak Için, Azure rezervasyon emirlerini (tek seferlik ücretler) ve yıllık veya aylık olarak faturalandırılan siparişleri ayrı olarak listelemenize olanak tanır. Bkz. [müşteri ve faturalandırma dönem türüne göre siparişlerin listesini alın](get-a-list-of-orders-by-customer-and-billing-cycle-type.md).

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

Iş Ortağı Merkezi 'nde Azure ayırmaların yaşam döngüsünü yönetmenin bir parçası olarak, Azure ayırma [yetkilendirmelerinizin](entitlement-resources.md)bilgilerini alabilir ve rezervasyon siparişi kimliğini kullanarak rezervasyon ayrıntılarını alabilirsiniz. Bunun nasıl yapılacağı hakkında örnekler için bkz. [yetkilendirmeleri alma](get-a-collection-of-entitlements.md).   

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki senaryolarda, müşterinizin [faturalarını](invoice-resources.md)programlı bir şekilde görüntüleme ve Azure ayırmaları için tek seferlik ücretler içeren Hesap bakiyeleriniz ve özetler alma işlemleri gösterilmektedir.

### <a name="balance-and-payment"></a>Bakiye ve ödeme

Hem yinelenen hem de tek seferlik (Azure rezervasyon) ücretlerine yönelik bir bakiye olan varsayılan para birimi türünde güncel hesap bakiyesini almak için bkz. [geçerli hesap bakiyenizi edinme](get-the-reseller-s-current-account-balance.md)

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
