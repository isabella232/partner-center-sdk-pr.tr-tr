---
title: Fatura kaynakları
description: Iş Ortağı Merkezi API 'Leri aracılığıyla birden fazla faturaya yönelik kaynak mevcuttur. Bu kaynaklar, fatura ve satır öğesi ayrıntıları ile ilgilidir.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d2e801dc3b082411e140b88cd495807b1381ef915e8f5f06803d64ca2cca1c6b
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996555"
---
# <a name="invoice-resources"></a>Fatura kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Aşağıdaki faturaya ilişkin kaynaklar Iş Ortağı Merkezi API 'Leri aracılığıyla kullanılabilir.

## <a name="invoice"></a>Fatura

| Özellik | Tür | Description |
| -------- | ---- | ----------- |
| kimlik | string | Fatura tanımlayıcısı. |
| InvoiceDate | UTC Tarih-saat biçiminde dize | Faturanın oluşturulduğu tarih. |
| billingPeriodStartDate | UTC Tarih-saat biçiminde dize | Fatura dönemi başlangıç tarihi (UTC). |
| billingPeriodEndDate | UTC Tarih-saat biçiminde dize   | Fatura dönemi bitiş tarihi (UTC). |
| Toplam ücretler | sayı | Toplam ücretler. İşlemler ve ayarlamalar için ücretler içerir.     |
| Paidadmount | sayı  | İş ortağı tarafından ödenen miktar. Ödeme alınmışsa negatif.  |
| currencyCode | string  | Tüm fatura öğesi miktarları ve toplamları için kullanılan para birimini belirten kod. |
| currencySymbol  | string | Tüm fatura öğesi tutarları ve toplamları için kullanılan para birimi simgesi. |
| pdfDownloadLink | string  | Faturayı PDF biçiminde indirmek için bir bağlantı. Bu bağlantı, arama sonuçlarının bir parçası olarak döndürülmez ve yalnızca faturaya KIMLIĞE göre erişildiğinde doldurulur. Bu bağlantı, 30 dakika içinde otomatik olarak sona erer. |
| InvoiceDetails  | [InvoiceDetail](#invoicedetail) nesneleri dizisi  | Fatura Ayrıntıları.  |
| siparişlerinde      | [Fatura](#invoice) nesneleri dizisi   | Bu faturaya düzeltme.  |
| documentType    | string | Faturanın belge türü: "Kredi dekontu", "fatura". |
| Düzeltme        | string | Bu belgenin bir düzeltme olduğu belgenin başvuru numarası.  |
| Faturano Etype     | string  | Faturanın türü: "yinelenen", "bir \_ kez".   |
| Köprü           | [Resourcelmürekkepler](utility-resources.md#resourcelinks)  | Kaynak bağlantıları.  |
| öznitelikler      | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.  |

## <a name="invoicedetail"></a>InvoiceDetail

Fatura, faturalanan öğelerin bir koleksiyonunu içerir ve her öğe bir InvoiceDetail kaynağıyla temsil edilir.

| Özellik            | Tür                                                           | Description                                                                       |
|---------------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| Faturadan Elineıtemtype | string                                                         | Fatura ayrıntısı türü: "none", "kullanım \_ satırı \_ öğeleri", "Faturalandırma \_ satırı \_ öğeleri". |
| billingProvider     | string                                                         | Faturalandırma sağlayıcısı: "none", "Office", "Azure" veya "Azure \_ veri \_ marketi".         |
| Köprü               | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                               |
| öznitelikler          | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                          |

## <a name="invoicelineitem"></a>Faturadan, Elinei öğe

Bir faturadaki her bir ücret, bir fatura Elinei olarak temsil edilir.

| Özellik            | Tür                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Faturadan Elineıtemtype | string                                                         | Fatura satır öğesi türü: "none", "kullanım \_ satırı \_ öğeleri", "Faturalandırma \_ satırı \_ öğeleri". |
| billingProvider     | string                                                         | Faturalandırma sağlayıcısı: "none", "Office", "Azure" veya "Azure \_ veri \_ marketi".            |
| öznitelikler          | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                             |

## <a name="invoicesummary"></a>Faturalaresummary

Bir faturanın bakiye ve toplam ücretlerine ilişkin bir Özet açıklanır.

| Özellik                 | Tür                                                           | Description                                                           |
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

| Özellik            | Tür                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| Faturano Etype         | string                                                         | Faturanın türü: "yinelenen", "bir \_ kez".                                       |
| Özet             | [Faturalaresummary](#invoicesummary) nesnesi                       | Fatura türü başına Fatura Özeti.                                         |

## <a name="invoicesummaries"></a>InvoiceSummaries

Para birimi başına bir fatura türü için bireysel ayrıntıları içeren fatura [Esummary](#invoicesummary) türünde bir koleksiyonu temsil eder.

| Özellik            | Tür                                                           | Description                                                                          |
|---------------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------|
| collectionOfSummary | [faturadan Esummary](#invoicesummary) nesneleri dizisi             | Para birimi başına fatura türü başına Fatura Özeti.                            |

## <a name="licensebasedlineitem"></a>Licensebasedlineıtem

Lisanslı tabanlı abonelikler için fatura fatura satırı maddesini temsil eder.

| Özellik                 | Tür                                                           | Description                                                           |
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
| Mpnıd                    | sayı                                                         | Bu satır öğesiyle ilişkili MPN KIMLIĞINI alır veya ayarlar. Doğrudan satıcılar için bu, satıcının MPN KIMLIĞIDIR. Dolaylı satıcılar için, bu değer eklenen satıcı (VAR), MPN KIMLIĞIDIR.                                   |
| OfferId                  | string                                                         | Teklifin benzersiz tanımlayıcısını alır veya ayarlar.                             |
| offerName                | string                                                         | Teklif adını alır veya ayarlar.                                          |
| Sipariş                  | string                                                         | Sıra benzersiz tanımlayıcısını alır veya ayarlar.                             |
| iş ortağı kimliği                | string                                                         | İş ortağı Azure Active Directory kiracı KIMLIĞINI alır veya ayarlar.            |
| miktar                 | sayı                                                         | Bu satır öğesiyle ilişkili birim sayısını alır veya ayarlar.      |
| Abonelik açıklaması  | string                                                         | Abonelik açıklamasını alır veya ayarlar.                            |
| subscriptionEndDate      | UTC Tarih-saat biçiminde dize                                 | Aboneliğin süresi dolduğunda tarihi alır veya ayarlar.                      |
| subscriptionId           | string                                                         | Abonelik benzersiz tanımlayıcısını alır veya ayarlar.                      |
| subscriptionName         | string                                                         | Abonelik adını alır veya ayarlar.                                   |
| subscriptionStartDate    | UTC Tarih-saat biçiminde dize                                 | Aboneliğin başladığı tarihi alır veya ayarlar.                   |
| Dikçe                 | sayı                                                         | İndirimden sonra tutarı alır veya ayarlar.                               |
| syndicationPartnerSubscriptionNumber | string                                             | Dağıtım ortağı abonelik numarasını alır veya ayarlar.             |
| VERG                      | sayı                                                         | Ücretlendirilen vergileri alır veya ayarlar.                                       |
| tier2MpnId               | sayı                                                         | Bu satır öğesiyle ilişkili katman 2 ortağının MPN KIMLIĞINI alır veya ayarlar. |
| totalForCustomer         | sayı                                                         | İskontoların ve verginin toplam miktarını alır veya ayarlar.                 |
| totalOtherDiscount       | sayı                                                         | Bu satınalmayla ilişkili iskontoyu alır veya ayarlar.              |
| unitPrice                | sayı                                                         | Birim fiyatını alır veya ayarlar.                                          |

## <a name="usagebasedlineitem"></a>Usagebasedlineıtem

Kullanım tabanlı abonelikler için fatura faturalama satırı öğesini temsil eder.

| Özellik                 | Tür                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| öznitelikler               | string                                                         | Öznitelikleri alır.                                                  |
| billingCycleType         | string                                                         | Faturalandırma dönem türünü alır veya ayarlar.                                  |
| billingProvider          | string                                                         | Faturalandırma sağlayıcısını alır.                                            |
| chargeEndDate            | UTC Tarih-saat biçiminde dize                                 | Ücret için bitiş tarihini alır veya ayarlar.                             |
| chargeStartDate          | UTC Tarih-saat biçiminde dize                                 | Ücret için başlangıç tarihini alır veya ayarlar.                           |
| chargeType               | string                                                         | Ücret türünü alır veya ayarlar.                                      |
| consumedQuantity         | sayı                                                         | Tüketilen toplam birim sayısını alır veya ayarlar.                                |
| Sarf Mptiondiscount      | string                                                         | Tüketim indirimi alır veya ayarlar.                             |
| Tüketimptionprice         | string                                                         | Tüketilen miktarın fiyatını alır veya ayarlar.                          |
| currency                 | string                                                         | Fiyatlarla ilişkili para birimini alır veya ayarlar.                 |
| customerName             | string                                                         | Müşteri adını alır veya ayarlar.                                       |
| customerId               | string                                                         | Müşterinin benzersiz tanımlayıcısını alır veya ayarlar.                          |
| Detaillineıtemıd         | sayı                                                         | Ayrıntı satırı öğe KIMLIĞINI alır veya ayarlar. Hesaplamanın tüketilen birimlerde farklı olduğu durumlarda satır öğelerini benzersiz şekilde tanımlar. Örnek: tüketilen toplam = 1338, 1024 tek bir oran ile ücretlendirilir, 314 farklı bir oran ile ücretlendirilir.        |
| Etki               | string                                                         | Etki alanı adını alır veya ayarlar.                                             |
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

| Özellik                 | Tür                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | contentType = application/pdf ile ByteArrayContent.                  |

## <a name="onetimeinvoicelineitem"></a>OneTimeInvoiceLineItem

Lisanslı abonelikler için fatura faturalama satırı öğesini temsil eder.

| Özellik | Tür | Description |
| --- | --- | --- |
| PartnerId | string | İş ortağı kiracı kimliğini alır veya ayarlar. |
| CustomerId | string | Müşteri kiracı kimliğini alır veya ayarlar. |
| CustomerName | string | Müşteri adını alır veya ayarlar. |
| CustomerDomainName | string | Müşteri etki alanı adını alır veya ayarlar. |
| CustomerCountry | string | Müşteri ülkelerini alır veya ayarlar. |
| InvoiceNumber | string | Fatura numarasını alır veya ayarlar. |
| MpnId | string | Bu satır öğesiyle ilişkili MPN kimliğini alır veya ayarlar. |
| ResellerMpnId | int | Sipariş benzersiz tanımlayıcısını alır veya ayarlar. |
| OrderDate | DateTime | Siparişin oluşturulma tarihini alır veya ayarlar. |
| ProductId | string | Ürün benzersiz tanımlayıcısını alır veya ayarlar. |
| SkuId | string | SKU benzersiz tanımlayıcısını alır veya ayarlar. |
| AvailabilityId | string | Kullanılabilirlik benzersiz tanımlayıcısını alır veya ayarlar. |
| ProductName | string | Ürün adını alır veya ayarlar. |
| SkuName | string | SKU adını alır veya ayarlar. |
| ChargeType | string | Ücret türünü alır veya ayarlar. |
| UnitPrice | decimal | Birim fiyatı alır veya ayarlar. |
| EffectiveUnitPrice | decimal | Geçerli birim fiyatını alır veya ayarlar. |
| Unittype | string | Birim türünü alır veya ayarlar. |
| Miktar | int | Bu satır öğesiyle ilişkili birim sayısını alır veya ayarlar. |
| Ara toplam | decimal | İndirimden sonra tutarı alır veya ayarlar. |
| TaxTotal | decimal | Tahsil edilecek vergileri alır veya ayarlar. |
| TotalForCustomer | decimal | İndirim ve vergiden sonra toplam tutarı alır veya ayarlar. |
| Para Birimi | string | Bu satır öğesi için kullanılan para birimini alır veya ayarlar. |
| PublisherName | string | Bu satın alma ile ilişkili yayımcı adını alır veya ayarlar. |
| PublisherId | string | Bu satın alma ile ilişkili yayımcı kimliğini alır veya ayarlar. |
| SubscriptionDescription | string | Bu satın alma ile ilişkili abonelik açıklamasını alır veya ayarlar. |
| SubscriptionId | string | Bu satın alma ile ilişkili abonelik kimliğini alır veya ayarlar. |
| ChargeStartDate | DateTime | Bu satın alma ile ilişkili ücret başlangıç tarihini alır veya ayarlar. |
| ChargeEndDate | DateTime | Bu satın alma ile ilişkili ücret bitiş tarihini alır veya ayarlar. |
| TermAndBillingCycle | string | Bu satın alma ile ilişkili dönemi ve faturalama döngüsünü alır veya ayarlar. |
| AlternateId | string | Alternatif Kimliği (teklif kimliği) alır veya ayarlar. |
| PriceAdjustmentDescription | string | Fiyat ayarlama açıklamasını alır veya ayarlar. |
| CreditReasonCode | string | Kredi nedeni kodunu alır veya ayarlar. |
| DiscountDetails | string |  **kullanım dışı.** Bu satın alma ile ilişkili indirim ayrıntılarını alır veya ayarlar. |
| PricingCurrency | string | Fiyatlandırma para birimi kodunu alır veya ayarlar. |
| PCToBCExchangeRate | decimal | Fiyatlandırma para birimini alır veya faturalama para birimi döviz kuruna ayarlar. |
| PCToBCExchangeRateDate | DateTime | Fiyatlandırma para biriminin faturalama para birimi döviz kuru belirlendi olduğu döviz kuru tarihini alır veya ayarlar. |
| BillableQuantity | decimal | Satın alınan birimleri alır veya ayarlar. **BillableQuantity** olarak adlandırılmış her tasarım sütunu için. |
| MeterDescription | string | Tüketim satırı öğesi için ölçüm açıklamasını alır veya ayarlar. |
| ReservationOrderId | string | Azure RI Satın Alma için rezervasyon siparişi tanımlayıcısını alır veya ayarlar. |
| BillingFrequency | string | Faturalama sıklığını alır veya ayarlar. |
| InvoiceLineItemType | InvoiceLineItemType | Fatura satırı öğesinin türünü döndürür. |
| BillingProvider | BillingProvider | Faturalama sağlayıcısını döndürür. |

## <a name="dailyratedusagelineitem"></a>DailyRatedUsageLineItem

Günlük derecelendirilmiş kullanım için faturalanmamış, faturalanan mutabakat satırı öğelerini temsil eder.

| Özellik | Tür | Description |
| --- | --- | --- |
| PartnerId | string | İş ortağı kiracı kimliğini alır veya ayarlar. |
| PartnerName | string | İş ortağı adını alır veya ayarlar. |
| CustomerId | string | Kullanımın ait olduğu müşterinin kiracı kimliğini alır veya ayarlar. |
| CustomerName | string | Kullanımın ait olduğu müşteri şirketinin adını alır veya ayarlar. |
| CustomerDomainName | string | Kullanımın ait olduğu müşterinin etki alanı adını alır veya ayarlar. |
| InvoiceNumber | string | Kullanımın ait olduğu faturanın kimliğini alır veya ayarlar. |
| ProductId | string | Ürün benzersiz tanımlayıcısını alır veya ayarlar. |
| SkuId | string | SKU benzersiz tanımlayıcısını alır veya ayarlar. |
| AvailabilityId | string | Kullanılabilirlik benzersiz tanımlayıcısını alır veya ayarlar. |
| SkuName | string | Hizmetin SKU adını alır veya ayarlar. |
| ProductName | string | Ürünün adını alır veya ayarlar. |
| PublisherName | string | Yayımcının adını alır veya ayarlar. |
| PublisherId | string | Yayımcının kimliğini alır veya ayarlar. |
| SubscriptionId | string | Abonelik kimliğini alır veya ayarlar. |
| SubscriptionDescription | string | Abonelik açıklamasını alır veya ayarlar. |
| ChargeStartDate | DateTime | Ücret başlangıç tarihini alır veya ayarlar. |
| ChargeEndDate | DateTime | Ücret bitiş tarihini alır veya ayarlar. |
| UsageDate | DateTime | Kullanım tarihini alır veya ayarlar. |
| MeterType | string | Ölçüm türünü alır veya ayarlar. |
| MeterCategory | string | Ölçüm kategorisini alır veya ayarlar. |
| MeterId | string | Ölçüm kimliğini (GUID) alır veya ayarlar. |
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
