---
title: Azure rezervasyonları satın alma
description: mevcut Microsoft Azure aboneliğiniz (MS-azr-0145p) veya Azure planı aracılığıyla iş ortağı merkezi apı 'sini kullanarak bir müşteri için Azure ayırmaları satın alabilirsiniz.
ms.date: 11/01/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ed8aa12117e9f13f84f39c97fc87e2c8844b223bd913cbaebf870d7022959dbd
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997303"
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
> | Fransız Guyanası                  | Yeni Kaledonya                     | ABD'de Outlying Adaları                    |
> | Fransız Polinezyası               | Nijer                             | Vanuatu                                  |
> | Fransız Güney Toprakları    | Niue                              | Vatikan                             |
> | Gabon                          | Norfolk Adası                    | Wallis veUçsuzuna                        |
> | Gambiya                         | Kuzey Mariana Adaları          | Yemen                                    |
> | Cebelitarık                      | Palau                             | &nbsp;                                   |
>

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Etkin bir CSP Azure aboneliği veya Azure planı için abonelik kimliği.

## <a name="how-to-purchase-microsoft-azure-reservations"></a>Microsoft Azure rezervasyonları satın alma

Azure rezervasyonu eklemek istediğiniz etkin CSP Azure aboneliğini belirlediktan sonra satın almak için aşağıdaki adımları kullanın:

1. [Etkinleştirme -](#enablement) Azure rezervasyonları satın almak için etkin bir CSP Azure aboneliğini kaydetme.

2. [Bulma](#discovery) - Satın almak istediğiniz Azure rezervasyon ürünlerini ve Stok Tutma Birimlerini (SKU) bulup seçin ve bunların kullanılabilirliğini kontrol edin.

3. [Sipariş gönderimi](#order-submission) - Siparişinizde bulunan öğelerle bir alışveriş sepeti oluşturun ve gönderin.

4. [Sipariş ayrıntılarını alma](#get-order-details) - Siparişin ayrıntılarını, bir müşterinin tüm siparişlerini gözden geçirme veya faturalama döngüsü türüne göre siparişleri görüntüleme.

Azure rezervasyonları satın alındıktan sonra, aşağıdaki senaryolarda Azure rezervasyon yetkilendirmeleri hakkında bilgi edinerek yaşam döngülerini yönetme ve bakiye deyimleri, faturalar ve fatura özetlerini alma adımları açıklanıyor.

- [Yaşam döngüsü yönetimi](#lifecycle-management)
- [Fatura ve mutabakat](#invoice-and-reconciliation)

## <a name="enablement"></a>Geçerlilik

Etkinleştirme, mevcut bir Microsoft Azure (**MS-AZR-0145P**) aboneliğini Azure Ayrılmış SANAL Makine Örneği ile azure rezervasyonları için etkinleştirilmesi için kaydederek bir Azure Ayrılmış SANAL Makine Örneği ile ilerler. Kayıt, kayıt satın almak için önkoşul Azure Ayrılmış VM Örnekleri.

Aşağıdaki görevleri desteklemek için bir abonelik gereklidir:

1. Müşterinin kaynakları dağıtmaya uygun olup olmadığını ve bu nedenle bir bölgede Azure Ayrılmış VM Örnekleri satın almak için.

2. Bir abonelikte dağıtımlara kapasite önceliği sağlamak için. Bu yalnızca kapasite önceliği seçeneği Azure Ayrılmış VM Örnekleri tek **bir kapsam için** geçerlidir.

Azure rezervasyonlarını eklemek istediğiniz etkin aboneliği belirlediktan sonra, Azure rezervasyonları için etkinleştirilmesi için aboneliği kaydetmeniz gerekir. Azure rezervasyonlarını [sipariş etme](subscription-resources.md) amacıyla etkinleştirilmesi için mevcut bir Abonelik kaynağını kaydetmek için [bkz. Aboneliği kaydetme.](register-a-subscription.md)

Aboneliğinizi kaydettikten sonra kayıt durumunu kontrol ederek kayıt işleminin tamamlandıktan emin olun. Bunu yapmak için [bkz. Abonelik kayıt durumunu alma.](get-subscription-registration-status.md)

> [!NOTE]
> Azure Microsoft Azure müşteri için rezervasyon satın alırken önce Azure planını kaydetmeniz gerekir. Microsoft Azure (**MS-AZR-0145P**) aboneliğine benzer şekilde, Azure planı da İş Ortağı Merkezi [Aboneliği kaynağıyla temsil](subscription-resources.md) edilen bir Azure planıdır. Bu nedenle, bir Azure planını [kaydetmek için aynı Abonelik](register-a-subscription.md) kaydetme yöntemini kullanabilirsiniz.

## <a name="discovery"></a>Bulma

Abonelik Azure rezervasyonları satın almak için etkinleştirildikten sonra ürünleri ve SKI'ları seçmeye ve aşağıdaki API modellerini kullanarak bunların kullanılabilirliğini İş Ortağı Merkezi hazır olursanız:

- [Ürün](product-resources.md#product) - Satınlanabilir ürünler veya hizmetler için bir gruplama yapısı. Tek başına ürün, satın edilebilir bir öğe değildir.

- [SKU](product-resources.md#sku) - Ürün altında satınlanabilir bir SKU. Bunlar ürünün farklı şekillerini temsil ediyor.

- [Kullanılabilirlik:](product-resources.md#availability) SKU'nun satın alına hazır olduğu yapılandırma (ülke, para birimi ve sektör segmenti gibi).

Azure rezervasyonu satın almadan önce aşağıdaki adımları tamamlayın:

1. Satın almak istediğiniz Ürün ve SKU'ları belirleyin ve alın. Bunu yapmak için önce ürünleri ve SKU'ları listelenin veya Ürün ve SKU'nun kimliklerini biliyorsanız bunları seçin.

   - [Ürünlerin bir listesini alma (ülkeye göre)](get-a-list-of-products.md)
   - [Ürün kimliğini kullanarak ürün al](get-a-product-by-id.md)
   - [Bir ürüne ait SKU’ların listesini alma (ülkeye göre)](get-a-list-of-skus-for-a-product.md)
   - [SKU Kimliğini kullanarak SKU'ya sahip olmak](get-a-sku-by-id.md)

2. SKU envanterini denetleme. Bu adım yalnızca InventoryCheck önkoşulları ile etiketlenmiş **SKU'lar için** gereklidir.

   - [Envanter denetleme](check-inventory.md)

3. SKU [için](product-resources.md#availability) [kullanılabilirliği alın.](product-resources.md#sku) Siparişi sağlarken **kullanılabilirlik CatalogItemId'ye** ihtiyacınız olacak. Bu değeri almak için aşağıdaki API'lerden birini kullanın:

   - [Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma](get-a-list-of-availabilities-for-a-sku.md)
   - [Kullanılabilirlik kimliğini kullanarak kullanılabilirlik elde edin](get-an-availability-by-id.md)

> [!IMPORTANT]
> Her Microsoft Azure ürün, Microsoft Azure (**MS-AZR-0145P**) aboneliği ve Azure planı için farklı kullanılabilirliklere sahip. Ürünlerin [listesini almak (ülkeye göre)](get-a-list-of-products.md)veya Bir ürünün SKU listesini [almak (ülkeye göre)](get-a-list-of-skus-for-a-product.md)veya Yalnızca Azure planı için geçerli olan [bir SKU'nun kullanılabilirlik](get-a-list-of-availabilities-for-a-sku.md) listesini almak için "reservationScope=AzurePlan" parametresini belirtin.

## <a name="order-submission"></a>Sipariş gönderimi

Azure rezervasyon siparişinizi göndermek için aşağıdaki görevleri gerçekleştirin:

1. Satın almayı istediğiniz katalog öğelerinin koleksiyonunu tutmak için bir sepet oluşturun. Bir Sepet [oluşturma sırasında](cart-resources.md)sepet [satır öğeleri](cart-resources.md#cartlineitem) aynı Sipariş içinde birlikte satın alınarak otomatik olarak [gruplanır.](order-resources.md)

   - [Alışveriş sepeti oluşturma](create-a-cart.md)
   - [Alışveriş sepetini güncelleştirme](update-a-cart.md)

2. Sepete göz at. Sepete göz atarak Sipariş oluşturulmasına neden [olur.](order-resources.md)

   - [Sepete göz at](checkout-a-cart.md)

## <a name="get-order-details"></a>Sipariş ayrıntılarını al

Azure rezervasyon siparişinizi oluşturduktan sonra sipariş kimliğini kullanarak tek bir siparişin ayrıntılarını alabilir veya müşteri için siparişlerin listesini edinebilirsiniz. Bir siparişin gönderilme zamanı ile müşterinin sipariş listesinde görünmesi arasında 15 dakikaya kadar bir gecikme olur.

- Sipariş kimliğini kullanarak tek bir siparişin ayrıntılarını almak için. Bkz. [Kimliğine göre sipariş al.](get-an-order-by-id.md)

- Müşteri kimliğini kullanarak müşterinin sipariş listesini almak için. Bkz. [Müşterinin tüm siparişlerini alma.](get-all-of-a-customer-s-orders.md)

- Azure rezervasyon siparişlerini (tek [](product-resources.md#billingcycletype) kullanımlık ücretler) ve yıllık veya aylık faturalandırmış siparişleri ayrı olarak listeleyebilirsiniz. Bkz. [Müşteriye ve faturalama döngüsü türüne göre siparişlerin listesini alma.](get-a-list-of-orders-by-customer-and-billing-cycle-type.md)

## <a name="lifecycle-management"></a>Yaşam döngüsü yönetimi

İş Ortağı Merkezi'da Azure rezervasyonlarının yaşam döngüsünün yönetilmesi kapsamında, Azure rezervasyon yetkilendirmeleri [](entitlement-resources.md)hakkında bilgi alabilir ve rezervasyon sipariş kimliğini kullanarak rezervasyon ayrıntılarını edinebilirsiniz. Bunu yapma örnekleri için bkz. [Yetkilendirmeleri al.](get-a-collection-of-entitlements.md)   

## <a name="invoice-and-reconciliation"></a>Fatura ve mutabakat

Aşağıdaki senaryolar, müşterinizin faturalarını program aracılığıyla [](invoice-resources.md)görüntülemeyi ve Azure rezervasyonları için tek kullanımlık ücretleri içeren hesap bakiyelerinizi ve özetlerinizi nasıl alasınız?

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
