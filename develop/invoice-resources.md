---
title: Fatura kaynakları
description: Faturayla ilgili birden çok kaynak, İş Ortağı Merkezi kullanılabilir. Bu kaynaklar fatura ve satır öğesi ayrıntılarıyla ilgilidir.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b07b7ad14c136eac988eeb12391c24a6cf996b39
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548439"
---
# <a name="invoice-resources"></a>Fatura kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Faturayla ilgili aşağıdaki kaynaklar, fatura API'leri İş Ortağı Merkezi kullanılabilir.

## <a name="invoice"></a>Fatura

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| kimlik | string | Fatura tanımlayıcısı. |
| invoiceDate | UTC tarih-saat biçiminde dize | Faturanın oluşturulma tarihi. |
| billingPeriodStartDate | UTC tarih-saat biçiminde dize | UTC olarak faturalama dönemi başlangıç tarihi. |
| billingPeriodEndDate | UTC tarih-saat biçiminde dize   | UTC olarak faturalama dönemi bitiş tarihi. |
| totalCharges | sayı | Toplam ücretler. İşlemler ve tüm ayarlamalar için ücretleri içerir.     |
| paidAmount | sayı  | İş ortağı tarafından ödenen tutar. Ödeme alındı ise negatif.  |
| currencyCode | string  | Tüm fatura öğesi tutarları ve toplamları için kullanılan para birimini gösteren bir kod. |
| Currencysymbol  | string | Tüm fatura öğesi tutarları ve toplamları için kullanılan para birimi simgesi. |
| pdfDownloadLink | string  | Faturayı PDF biçiminde indirme bağlantısı. Bu bağlantı arama sonuçlarının bir parçası olarak döndürülz ve yalnızca faturaya kimlikle erişilirse doldurulur. Bu bağlantının süresi 30 dakika içinde otomatik olarak dolar. |
| invoiceDetails  | [InvoiceDetail nesneleri](#invoicedetail) dizisi  | Fatura ayrıntıları.  |
| Değişiklik      | Invoice [nesneleri](#invoice) dizisi   | Bu faturada yapılan değişiklikler.  |
| Documenttype    | string | Faturanın belge türü: "Kredi Notu", "Fatura". |
| amendsOf        | string | Bu belgenin bir değişiklik olduğu belgenin başvuru numarası.  |
| invoiceType     | string  | Fatura türü: "yinelenen", "bir \_ kez".   |
| Bağlantı           | [ResourceLinks](utility-resources.md#resourcelinks)  | Kaynak bağlantıları.  |
| öznitelikler      | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.  |

## <a name="invoicedetail"></a>InvoiceDetail

Fatura, faturalanmış öğelerden bir koleksiyon içerir ve her öğe bir InvoiceDetail kaynağıyla temsil edilen bir koleksiyondur.

| Özellik            | Tür                                                           | Açıklama                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | Fatura ayrıntısı türü: "none", "usage \_ line \_ items", "billing \_ line \_ items". |
| billingProvider     | string                                                         | Faturalama sağlayıcısı: "none", "office", "azure" veya "azure \_ \_ data market".         |
| Bağlantı               | [ResourceLinks](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                               |
| öznitelikler          | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                          |

## <a name="invoicelineitem"></a>InvoiceLineItem

Bir fatura içindeki her bireysel ücret InvoiceLineItem olarak temsil edilecektir.

| Özellik            | Tür                                                           | Açıklama                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| invoiceLineItemType | string                                                         | Fatura satırı öğesinin türü: "none", "usage \_ line \_ items", "billing \_ line \_ items". |
| billingProvider     | string                                                         | Faturalama sağlayıcısı: "none", "office", "azure" veya "azure \_ \_ data market".            |
| öznitelikler          | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                             |

## <a name="invoicesummary"></a>InvoiceSummary

Bakiyenin özetini ve bir faturanın toplam ücretlerini açıklar.

| Özellik                 | Tür                                                           | Açıklama                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| balanceAmount            | sayı                                                         | Faturanın bakiyesi. Bu, ödenmemiş kambiyo senetlerinin toplam miktarıdır. |
| currencyCode             | string                                                         | Bakiye miktarı için kullanılan para birimini belirten kod.       |
| currencySymbol           | string                                                         | Kullanılan para birimi simgesi.                                             |
| accountingDate           | UTC Tarih-saat biçiminde dize                                 | Bakiye tutarının son güncelleştirilme tarihi.                         |
| Firstınvoizereationdate | UTC Tarih-saat biçiminde dize                                 | Müşterinin ilk faturasının oluşturulduğu tarih.              |
| lastPaymentDate          | UTC Tarih-saat biçiminde dize                                 | Son ödemenin tarihi.                                         |
| lastPaymentAmount        | sayı                                                         | Son ödemenin miktarı.                                       |
| Latestınvoicedate        | UTC Tarih-saat biçiminde dize                                 | Müşterinin son faturasının oluşturulduğu tarih.               |
| bilgileri                  | [InvoiceSummaryDetail](#invoicesummarydetail) nesneleri dizisi | Fatura Özet ayrıntısı.                                           |
| Köprü                    | [Resourcelmürekkepler](utility-resources.md#resourcelinks)            | Kaynak bağlantıları.                                                   |
| öznitelikler               | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                              |

## <a name="invoicesummarydetail"></a>InvoiceSummaryDetail

Bir fatura türü için bireysel ayrıntıların özetini temsil eder (örneğin, yinelenen, bir \_ zaman).

| Özellik            | Tür                                                           | Açıklama                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Faturano Etype         | string                                                         | Faturanın türü: "yinelenen", "bir \_ kez".                                       |
| Özet             | [Faturalaresummary](#invoicesummary) nesnesi                       | Fatura türü başına Fatura Özeti.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Para birimi başına bir fatura türü için bireysel ayrıntıları içeren fatura [Esummary](#invoicesummary) türünde bir koleksiyonu temsil eder.

| Özellik            | Tür                                                           | Açıklama                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | [faturadan Esummary](#invoicesummary) nesneleri dizisi             | Para birimi başına fatura türü başına Fatura Özeti.                            |

## <a name="licensebasedlineitem"></a>Licensebasedlineıtem

Lisanslı tabanlı abonelikler için fatura fatura satırı maddesini temsil eder.

| Özellik                 | Tür                                                           | Açıklama                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| tutara                   | string                                                         | Toplam miktarı alır veya ayarlar. Toplam tutar = birim fiyatı * miktar.  |
| öznitelikler               | string                                                         | Öznitelikleri alır.                                                  |
| billingCycleType         | string                                                         | Faturalandırma dönem türünü alır veya ayarlar.                                  |
| billingProvider          | string                                                         | Faturalandırma sağlayıcısını alır.                                            |
| chargeEndDate            | UTC Tarih-saat biçiminde dize                                 | Ücret için bitiş tarihini alır veya ayarlar.                             |
| chargeStartDate          | UTC Tarih-saat biçiminde dize                                 | Ücret için başlangıç tarihini alır veya ayarlar.                           |
| chargeType               | string                                                         | Ücret türünü alır veya ayarlar.                                      |
| currency                 | string                                                         | Bu satır öğesi için kullanılan para birimini alır veya ayarlar.                    |
| customerId               | string                                                         | Microsoft faturalandırma platformunda müşterinin benzersiz tanımlayıcısını alır veya ayarlar.  |
| customerName             | UTC Tarih-saat biçiminde dize                                 | Müşteri adını alır veya ayarlar.                                       |
| Etki               | string                                                         | Etki alanı adını alır veya ayarlar.                                             |
| Durableofferıd           | string                                                         | Dayanıklı teklif benzersiz tanımlayıcısını alır veya ayarlar.                     |
| Faturadan Elineıtemtype      | string                                                         | Fatura satırı öğesinin türünü alır.                                   |
| Mpnıd                    | sayı                                                         | Bu satır öğesiyle ilişkili MPN KIMLIĞINI alır veya ayarlar. Doğrudan satıcılar için bu, satıcının MPN KIMLIĞIDIR. Dolaylı kurumsal bayiler için bu Değer Eklenmiş Kurumsal Bayinin (VAR) MPN Kimliğidir.                                   |
| offerId                  | string                                                         | Teklif benzersiz tanımlayıcısını alır veya ayarlar.                             |
| offerName                | string                                                         | Teklif adını alır veya ayarlar.                                          |
| Siparişno                  | string                                                         | Sipariş benzersiz tanımlayıcısını alır veya ayarlar.                             |
| partnerId                | string                                                         | İş ortağı Azure Active Directory kiracı kimliğini alır veya ayarlar.            |
| miktar                 | sayı                                                         | Bu satır öğesiyle ilişkili birim sayısını alır veya ayarlar.      |
| subscriptionDescription  | string                                                         | Abonelik açıklamasını alır veya ayarlar.                            |
| subscriptionEndDate      | UTC tarih-saat biçiminde dize                                 | Aboneliğin süresinin dolma tarihini alır veya ayarlar.                      |
| subscriptionId           | string                                                         | Abonelik benzersiz tanımlayıcısını alır veya ayarlar.                      |
| subscriptionName         | string                                                         | Abonelik adını alır veya ayarlar.                                   |
| subscriptionStartDate    | UTC tarih-saat biçiminde dize                                 | Aboneliğin başladığı tarihi alır veya ayarlar.                   |
| Alt toplam                 | sayı                                                         | İndirimden sonra tutarı alır veya ayarlar.                               |
| syndicationPartnerSubscriptionNumber | string                                             | Dağıtım iş ortağı abonelik numarasını alır veya ayarlar.             |
| Vergi                      | sayı                                                         | Tahsil edilecek vergileri alır veya ayarlar.                                       |
| tier2MpnId               | sayı                                                         | Bu satır öğesiyle ilişkili Katman 2 iş ortağının MPN kimliğini alır veya ayarlar. |
| totalForCustomer         | sayı                                                         | İndirim ve vergiden sonra toplam tutarı alır veya ayarlar.                 |
| totalOtherDiscount       | sayı                                                         | Bu satın alma ile ilişkili indirimi alır veya ayarlar.              |
| unitPrice                | sayı                                                         | Birim fiyatı alır veya ayarlar.                                          |

## <a name="usagebasedlineitem"></a>UsageBasedLineItem

Kullanım tabanlı abonelikler için fatura faturalama satırı öğesini temsil eder.

| Özellik                 | Tür                                                           | Açıklama                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| öznitelikler               | string                                                         | Öznitelikleri alır.                                                  |
| billingCycleType         | string                                                         | Faturalama döngüsü türünü alır veya ayarlar.                                  |
| billingProvider          | string                                                         | Faturalama sağlayıcısını alır.                                            |
| chargeEndDate            | UTC tarih-saat biçiminde dize                                 | Ücretin bitiş tarihini alır veya ayarlar.                             |
| chargeStartDate          | UTC tarih-saat biçiminde dize                                 | Ücretin başlangıç tarihini alır veya ayarlar.                           |
| chargeType               | string                                                         | Ücret türünü alır veya ayarlar.                                      |
| consumedQuantity         | sayı                                                         | Tüketilen toplam birimleri alır veya ayarlar.                                |
| consumptionDiscount      | string                                                         | Tüketimde indirimi alır veya ayarlar.                             |
| consumptionPrice         | string                                                         | Tüketilen miktarın fiyatını alır veya ayarlar.                          |
| currency                 | string                                                         | Fiyatlarla ilişkili para birimini alır veya ayarlar.                 |
| Müşteriadı             | string                                                         | Müşteri adını alır veya ayarlar.                                       |
| customerId               | string                                                         | Müşteri benzersiz tanımlayıcısını alır veya ayarlar.                          |
| detailLineItemId         | sayı                                                         | Ayrıntı satırı öğesi kimliğini alır veya ayarlar. Hesaplamanın tüketilen birimler için farklı olduğu durumlar için satır öğelerini benzersiz olarak tanımlar. Örnek: Tüketilen toplam = 1338, 1024 tek bir ücretle ücret, 314 ise farklı bir ücretle ücrete tabidir.        |
| Etkialanıadı               | string                                                         | Etki alanı adını alır veya ayarlar.                                             |
| includedQuantity         | sayı                                                         | Siparişe dahil edilen birimleri alır veya ayarlar.                         |
| invoiceLineItemType      | string                                                         | Fatura satırı öğesinin türünü alır.                                   |
| invoiceNumber            | string                                                         | Fatura numarasını alır veya ayarlar.                                      |
| Listprice                | sayı                                                         | Her birimin fiyatını alır veya ayarlar.                                  |
| mpnId                    | sayı                                                         | Bu satır öğesiyle ilişkili MPN kimliğini alır veya ayarlar. Doğrudan kurumsal bayiler için bu, kurumsal bayinin MPN kimliğidir. Dolaylı kurumsal bayiler için bu Değer Eklenmiş Kurumsal Bayinin (VAR) MPN Kimliğidir.                                   |
| Siparişno                  | string                                                         | Sipariş benzersiz tanımlayıcısını alır veya ayarlar.                             |
| overageQuantity          | sayı                                                         | İzin verilen kullanımın üzerinde tüketilen miktarı alır veya ayarlar.               |
| partnerBillableAccountId | string                                                         | İş ortağı faturalanabilir hesap kimliğini alır veya ayarlar.                         |
| partnerId                | string                                                         | İş ortağı Azure Active Directory kiracı kimliğini alır veya ayarlar.            |
| partnerName              | string                                                         | İş ortağının adını alır veya ayarlar.                                      |
| postTaxEffectiveRate     | sayı                                                         | Vergilerden sonra geçerli fiyatı alır veya ayarlar.                         |
| postTaxTotal             | sayı                                                         | Vergi sonrasındaki toplam ücretleri alır veya ayarlar. Vergi Öncesi Ücretler + Vergi Tutarı |
| preTaxCharges            | sayı                                                         | Vergilerden önce ücret tahsil edilecek fiyatı alır veya ayarlar.                          |
| preTaxEffectiveRate      | sayı                                                         | Vergilerden önce geçerli fiyatı alır veya ayarlar.                        |
| region                   | string                                                         | Kaynak örneğiyle ilişkili bölgeyi alır veya ayarlar.        |
| resourceGuid             | string                                                         | Kaynak tanımlayıcısını alır veya ayarlar.                                 |
| resourceName             | string                                                         | Kaynak adını alır veya ayarlar. Örnek: Veritabanı (GB/ay).         |
| Hizmetadı              | string                                                         | Hizmet adını alır veya ayarlar. Örnek: Azure Veri Hizmeti.           |
| Servicetype              | string                                                         | Hizmet türünü alır veya ayarlar. Örnek: Azure SQL Azure DB.           |
| Sku                      | string                                                         | Hizmet SKU'larını alır veya ayarlar.                                         |
| subscriptionDescription  | string                                                         | Abonelik açıklamasını alır veya ayarlar.                            |
| subscriptionId           | string                                                         | Abonelik benzersiz tanımlayıcısını alır veya ayarlar.                      |
| subscriptionName         | string                                                         | Abonelik adını alır veya ayarlar.                                   |
| taxAmount                | sayı                                                         | Ücret tahsil edilecek vergi miktarını alır veya ayarlar.                               |
| tier2MpnId               | sayı                                                         | Bu satır öğesiyle ilişkili Katman 2 iş ortağının MPN kimliğini alır veya ayarlar. |
| unit                     | string                                                         | Azure kullanımı için ölçü birimini alır veya ayarlar.                     |

## <a name="invoicestatement"></a>InvoiceStatement

Application/pdf'de bir fatura deyiminde kullanılabilen işlemleri temsil eder.

| Özellik                 | Tür                                                           | Açıklama                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | contentType = application/pdf ile ByteArrayContent.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Lisanslı abonelikler için fatura faturalama satırı öğesini temsil eder.

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| PartnerId | string | İş ortağı kiracı KIMLIĞINI alır veya ayarlar. |
| CustomerId | string | Müşteri kiracı KIMLIĞINI alır veya ayarlar. |
| CustomerName | string | Müşteri adını alır veya ayarlar. |
| CustomerDomainName | string | Müşteri etki alanı adını alır veya ayarlar. |
| CustomerCountry | string | Müşteri ülkesini alır veya ayarlar. |
| Faturanumarası | string | Fatura numarasını alır veya ayarlar. |
| Mpnıd | string | Bu satır öğesiyle ilişkili MPN KIMLIĞINI alır veya ayarlar. |
| Resellermpnıd | int | Sıra benzersiz tanımlayıcısını alır veya ayarlar. |
| OrderDate | DateTime | Siparişin oluşturulduğu tarihi alır veya ayarlar. |
| ProductId | string | Ürünün benzersiz tanımlayıcısını alır veya ayarlar. |
| SkuId | string | SKU benzersiz tanımlayıcısını alır veya ayarlar. |
| Kullanılabilirlik kimliği | string | Kullanılabilirlik benzersiz tanımlayıcısını alır veya ayarlar. |
| ProductName | string | Ürün adını alır veya ayarlar. |
| SkuName | string | SKU adını alır veya ayarlar. |
| ChargeType | string | Ücret türünü alır veya ayarlar. |
| UnitPrice | decimal | Birim fiyatını alır veya ayarlar. |
| Efekt, BirimFiyat | decimal | Geçerli birim fiyatını alır veya ayarlar. |
| UnitType | string | Birim türünü alır veya ayarlar. |
| Miktar | int | Bu satır öğesiyle ilişkili birim sayısını alır veya ayarlar. |
| Ara toplam | decimal | İndirimden sonra tutarı alır veya ayarlar. |
| Toplam vergi | decimal | Ücretlendirilen vergileri alır veya ayarlar. |
| TotalForCustomer | decimal | İskontoların ve verginin toplam miktarını alır veya ayarlar. |
| Para Birimi | string | Bu satır öğesi için kullanılan para birimini alır veya ayarlar. |
| PublisherName | string | Bu satınalmayla ilişkili yayımcı adını alır veya ayarlar. |
| PublisherId | string | Bu satınalmayla ilişkili yayımcı KIMLIĞINI alır veya ayarlar. |
| Abonelik açıklaması | string | Bu satınalmayla ilişkili abonelik açıklamasını alır veya ayarlar. |
| SubscriptionId | string | Bu satınalmayla ilişkili abonelik KIMLIĞINI alır veya ayarlar. |
| ChargeStartDate | DateTime | Bu satınalmayla ilişkili ücretlendirme başlangıç tarihini alır veya ayarlar. |
| ChargeEndDate | DateTime | Bu satınalmayla ilişkili ücretlendirme bitiş tarihini alır veya ayarlar. |
| Tertermbillingcycle | string | Bu satınalmayla ilişkili terim ve fatura döngüsünü alır veya ayarlar. |
| AlternateId | string | Alternatif KIMLIĞI (quote ID) alır veya ayarlar. |
| PriceAdjustmentDescription | string | Fiyat ayarlama açıklamasını alır veya ayarlar. |
| CreditReasonCode | string | Kredi nedeni kodunu alır veya ayarlar. |
| DiscountDetails | string |  **Kullanım dışı**. Bu satınalmayla ilişkili indirim ayrıntılarını alır veya ayarlar. |
| PricingCurrency | string | Fiyatlandırma para birimi kodunu alır veya ayarlar. |
| PCToBCExchangeRate | decimal | Ödeme para birimi döviz kurundaki fiyatlandırma para birimini alır veya ayarlar. |
| PCToBCExchangeRateDate | DateTime | Ödeme para birimi döviz kurundaki fiyatlandırma para biriminin belirlendiği Döviz Kuru tarihini alır veya ayarlar. |
| BillableQuantity | decimal | Satın alınan birimleri alır veya ayarlar. **Billablequantity** olarak adlandırılan her tasarım sütunu için. |
| MeterDescription | string | Tüketim çizgisi öğesi için ölçüm açıklamasını alır veya ayarlar. |
| ReservationOrderId | string | Bir Azure RI satın alma için rezervasyon siparişi tanımlayıcısını alır veya ayarlar. |
| BillingFrequency | string | Faturalandırma sıklığını alır veya ayarlar. |
| Faturadan Elineıtemtype | Faturadan Elineıtemtype | Fatura çizgisi öğesinin türünü döndürür. |
| BillingProvider | BillingProvider | Faturalandırma sağlayıcısını döndürür. |

## <a name="dailyratedusagelineitem"></a>Dailylartedusagelineitem

Günlük olarak derecelendirilen kullanım için faturalandırılmamış, faturalanmış mutabakat satır öğelerini temsil eder.

| Özellik | Tür | Açıklama |
| --- | --- | --- |
| İş ortağı kimliği | string | İş ortağı kiracı KIMLIĞINI alır veya ayarlar. |
| PartnerName | string | İş ortağı adını alır veya ayarlar. |
| CustomerId | string | Kullanımın ait olduğu müşterinin kiracı KIMLIĞINI alır veya ayarlar. |
| CustomerName | string | Kullanımın ait olduğu müşteri şirketinin adını alır veya ayarlar. |
| CustomerDomainName | string | Kullanımın ait olduğu müşterinin etki alanı adını alır veya ayarlar. |
| Faturanumarası | string | Kullanımın ait olduğu faturanın KIMLIĞINI alır veya ayarlar. |
| ProductId | string | Ürünün benzersiz tanımlayıcısını alır veya ayarlar. |
| SkuId | string | SKU benzersiz tanımlayıcısını alır veya ayarlar. |
| Kullanılabilirlik kimliği | string | Kullanılabilirlik benzersiz tanımlayıcısını alır veya ayarlar. |
| SkuName | string | Hizmetin SKU adını alır veya ayarlar. |
| ProductName | string | Ürünün adını alır veya ayarlar. |
| PublisherName | string | Yayımcının adını alır veya ayarlar. |
| PublisherId | string | Yayımcının KIMLIĞINI alır veya ayarlar. |
| SubscriptionId | string | Abonelik KIMLIĞINI alır veya ayarlar. |
| Abonelik açıklaması | string | Abonelik açıklamasını alır veya ayarlar. |
| ChargeStartDate | DateTime | Ücret başlangıç tarihini alır veya ayarlar. |
| ChargeEndDate | DateTime | Ücretlendirme bitiş tarihini alır veya ayarlar. |
| UsageDate | DateTime | Kullanım tarihini alır veya ayarlar. |
| MeterType | string | Ölçüm türünü alır veya ayarlar. |
| MeterCategory | string | Ölçüm kategorisini alır veya ayarlar. |
| MeterId | string | Ölçüm KIMLIĞINI (GUID) alır veya ayarlar. |
| MeterSubCategory | string | Ölçüm alt kategorisini alır veya ayarlar. |
| MeterName | string | Ölçüm adını alır veya ayarlar. |
| MeterRegion | string | Ölçüm bölgelerini alır veya ayarlar. |
| UnitOfMeasure | string | Ölçü birimini alır veya ayarlar. |
| ResourceLocation | string | Kaynağın konumunu alır veya ayarlar. |
| ConsumedService | string | Tüketilen hizmet adını alır veya ayarlar. |
| adlı yönetilen örnek, | string | Kaynak grubunun adını alır veya ayarlar. |
| ResourceUri | string | Kullanımın ilgili olduğu kaynak örneğinin uri'lerini alır veya ayarlar. |
| Etiketler | string | Müşterinin ekli etiketlerini alır veya ayarlar. |
| AdditionalInfo | string | Hizmete özgü meta verileri alır veya ayarlar. Örneğin, sanal makinenin görüntü türü. |
| ServiceInfo1 | string | İç Azure Hizmeti Meta Verilerini alır veya ayarlar. |
| ServiceInfo2 | string | Sanal makine için bir görüntü türü ve ExpressRoute için ISS adı gibi hizmet bilgilerini alır veya ayarlar. |
| CustomerCountry | string | Müşterinin ülkelerini alır veya ayarlar. |
| MpnId | string | Bu satır öğesiyle ilişkili MPN kimliğini alır veya ayarlar. |
| ResellerMpnId | string | Bu satır öğesiyle ilişkili Katman 2 iş ortağının Kurumsal Bayi MPN Kimliğini alır veya ayarlar. |
| ChargeType | string | Ücret türünü alır veya ayarlar. |
| UnitPrice | decimal | Birim fiyatını alır veya ayarlar. |
| Miktar | decimal | Kullanım miktarını alır veya ayarlar. |
| Unittype | string | Birim türünü alır veya ayarlar (örneğin 1 saat). |
| BillingPreTaxTotal | decimal | Müşterinin veya faturalama para biriminin yerel para birimiyle vergiden önce genişletilmiş maliyeti veya toplam maliyeti alır veya ayarlar. |
| BillingCurrency | string | Ölçümün müşterinin veya faturalama para biriminin yerel para birimiyle ücret ödemesi yapılan ISO para birimini alır veya ayarlar. |
| PricingPreTaxTotal | decimal | Abd doları cinsinden veya derecelendirme için kullanılan katalog para birimi cinsinden vergiden önce genişletilmiş maliyeti veya toplam maliyeti alır veya ayarlar. |
| PricingCurrency | string | Ölçümün ABD doları cinsinden veya derecelendirme için kullanılan katalog para birimi cinsinden ücret ödemesi yapılan ISO para birimini alır veya ayarlar. |
| EntitlementId | string | Yetkilendirme (Azure aboneliği) kimliğini alır veya ayarlar. |
| EntitlementDescription | string | Yetkilendirme (Azure aboneliği) açıklamasını alır veya ayarlar. |
| PCToBCExchangeRate | string | Fiyatlandırma para birimini alır veya faturalama para birimi döviz kuruna ayarlar. |
| PCToBCExchangeRateDate | DateTime | Fiyatlandırma para birimini faturalama para birimi döviz kuru tarihine alır veya ayarlar. |
| EffectiveUnitPrice | decimal | Geçerli birim fiyatını alır veya ayarlar. |
| RateOfPartnerEarnedCredit | decimal | İş ortağı tarafından kazanılan kredi oranını alır veya ayarlar. |
| HasPartnerEarnedCredit | bool | Alır veya kümeler iş ortağı tarafından kazanılan kredi uygulanır. |
| RateOfCredit | decimal | Verilen kredi türü için kredi oranını alır veya ayarlar. |
| CreditType | string | Kredi türünü alır veya ayarlar. |
| InvoiceLineItemType | InvoiceLineItemType | Fatura satırı öğesinin türünü döndürür. |
| BillingProvider | BillingProvider | Faturalama sağlayıcısını döndürür. |
