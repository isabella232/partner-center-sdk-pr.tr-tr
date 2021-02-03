---
title: Fatura kaynakları
description: Iş Ortağı Merkezi API 'Leri aracılığıyla birden fazla faturaya yönelik kaynak mevcuttur. Bu kaynaklar, fatura ve satır öğesi ayrıntıları ile ilgilidir.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd2caefe4ae18c81a31083d084f1e87da1288dd9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768903"
---
# <a name="invoice-resources"></a>Fatura kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

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
| Mpnıd                    | sayı                                                         | Bu satır öğesiyle ilişkili MPN KIMLIĞINI alır veya ayarlar. Doğrudan satıcılar için bu, satıcının MPN kimliğidir. Dolaylı satıcılar için, bu değer eklenen satıcı (VAR), MPN KIMLIĞIDIR.                                   |
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

Kullanım tabanlı abonelikler için bir fatura faturalama satırı öğesini temsil eder.

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
| includedQuantity         | sayı                                                         | Sırada bulunan birimleri alır veya ayarlar.                         |
| Faturadan Elineıtemtype      | string                                                         | Fatura satırı öğesinin türünü alır.                                   |
| Faturanumarası            | string                                                         | Fatura numarasını alır veya ayarlar.                                      |
| listPrice                | sayı                                                         | Her bir birimin fiyatını alır veya ayarlar.                                  |
| Mpnıd                    | sayı                                                         | Bu satır öğesiyle ilişkili MPN KIMLIĞINI alır veya ayarlar. Doğrudan satıcılar için bu, satıcının MPN KIMLIĞIDIR. Dolaylı satıcılar için, bu değer eklenen satıcı (VAR), MPN KIMLIĞIDIR.                                   |
| Sipariş                  | string                                                         | Sıra benzersiz tanımlayıcısını alır veya ayarlar.                             |
| Fazla Agemiktarı          | sayı                                                         | İzin verilen kullanım üzerinde tüketilen miktarı alır veya ayarlar.               |
| Partnerbillableaccountıd | string                                                         | İş ortağı faturalandırılabilir hesap KIMLIĞINI alır veya ayarlar.                         |
| iş ortağı kimliği                | string                                                         | İş ortağı Azure Active Directory kiracı KIMLIĞINI alır veya ayarlar.            |
| partnerName              | string                                                         | Ortağın adını alır veya ayarlar.                                      |
| postTaxEffectiveRate     | sayı                                                         | Vergiler sonrasında geçerli fiyatı alır veya ayarlar.                         |
| postTaxTotal             | sayı                                                         | Vergi sonrası toplam ücretleri alır veya ayarlar. Ön vergi ücretleri + vergi tutarı |
| preTaxCharges            | sayı                                                         | Vergiler üzerinden ücretlendirildiğiniz fiyatı alır veya ayarlar.                          |
| preTaxEffectiveRate      | sayı                                                         | Vergi öncesi geçerlilik fiyatını alır veya ayarlar.                        |
| region                   | string                                                         | Kaynak örneğiyle ilişkili bölgeyi alır veya ayarlar.        |
| resourceGuid             | string                                                         | Kaynak tanımlayıcısını alır veya ayarlar.                                 |
| resourceName             | string                                                         | Kaynak adını alır veya ayarlar. Örnek: veritabanı (GB/ay).         |
| HizmetAdı              | string                                                         | Hizmet adını alır veya ayarlar. Örnek: Azure Data Service.           |
| Türü              | string                                                         | Hizmet türünü alır veya ayarlar. Örnek: Azure SQL Azure DB.           |
| isteyin                      | string                                                         | Hizmet SKU 'sunu alır veya ayarlar.                                         |
| Abonelik açıklaması  | string                                                         | Abonelik açıklamasını alır veya ayarlar.                            |
| subscriptionId           | string                                                         | Abonelik benzersiz tanımlayıcısını alır veya ayarlar.                      |
| subscriptionName         | string                                                         | Abonelik adını alır veya ayarlar.                                   |
| taxAmount                | sayı                                                         | Ücretlendirilen vergi miktarını alır veya ayarlar.                               |
| tier2MpnId               | sayı                                                         | Bu satır öğesiyle ilişkili katman 2 ortağının MPN KIMLIĞINI alır veya ayarlar. |
| unit                     | string                                                         | Azure kullanımı için ölçü birimini alır veya ayarlar.                     |

## <a name="invoicestatement"></a>Faturalarestatement

Application/PDF içindeki bir fatura bildiriminde kullanılabilir olan işlemleri temsil eder.

| Özellik                 | Tür                                                           | Description                                                           |
|--------------------------|----------------------------------------------------------------|-----------------------------------------------------------------------|
| httpResponseMessage      | object                                                         | ContentType = Application/PDF ile ByteArrayContent.                  |

## <a name="onetimeinvoicelineitem"></a>Onetimeınvotınon öğesi

Lisanslı abonelikler için fatura fatura satırı öğesini temsil eder.

| Özellik | Tür | Description |
| --- | --- | --- |
| İş ortağı kimliği | string | İş ortağı kiracı KIMLIĞINI alır veya ayarlar. |
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

| Özellik | Tür | Description |
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
| MeterRegion | string | Ölçüm bölgesini alır veya ayarlar. |
| UnitOfMeasure | string | Ölçü birimini alır veya ayarlar. |
| ResourceLocation | string | Kaynağın konumunu alır veya ayarlar. |
| ConsumedService | string | Tüketilen hizmet adını alır veya ayarlar. |
| adlı yönetilen örnek, | string | Kaynak grubunun adını alır veya ayarlar. |
| ResourceUri | string | Kullanımın ilgili olduğu kaynak örneğinin URI 'sini alır veya ayarlar. |
| Etiketler | string | Müşterinin eklediği etiketleri alır veya ayarlar. |
| AdditionalInfo | string | Hizmete özgü meta verileri alır veya ayarlar. Örneğin, sanal makinenin görüntü türü. |
| ServiceInfo1 | string | İç Azure hizmeti meta verilerini alır veya ayarlar. |
| ServiceInfo2 | string | ExpressRoute için bir sanal makine ve ISS adı için görüntü türü gibi hizmet bilgilerini alır veya ayarlar. |
| CustomerCountry | string | Müşterinin ülkesini alır veya ayarlar. |
| Mpnıd | string | Bu satır öğesiyle ilişkili MPN KIMLIĞINI alır veya ayarlar. |
| Resellermpnıd | string | Bu satır öğesiyle ilişkili katman 2 ortağının satıcı MPN KIMLIĞINI alır veya ayarlar. |
| ChargeType | string | Ücret türünü alır veya ayarlar. |
| UnitPrice | decimal | Birim fiyatını alır veya ayarlar. |
| Miktar | decimal | Kullanım miktarını alır veya ayarlar. |
| UnitType | string | Birim türünü alır veya ayarlar (örneğin, 1 saat). |
| BillingPreTaxTotal | decimal | Müşterinin veya faturalandırma para biriminin yerel para birimindeki vergi öncesine ait genişletilmiş maliyeti veya toplam maliyeti alır veya ayarlar. |
| BillingCurrency | string | Ölçerin, müşterinin veya faturalandırma para biriminin yerel para birimiyle ücretlendirilildiği ISO para birimini alır veya ayarlar. |
| PricingPreTaxTotal | decimal | KDV veya değerlendirme için kullanılan Katalog para birimi cinsinden vergi öncesi genişletilmiş maliyeti veya toplam maliyeti alır veya ayarlar. |
| PricingCurrency | string | Ölçümün, derecelendirme için kullanılan ABD Doları veya katalog para birimi cinsinden ücretlendirilildiği ISO para birimini alır veya ayarlar. |
| EntitlementId | string | Yetkilendirme (Azure aboneliği) KIMLIĞINI alır veya ayarlar. |
| EntitlementDescription | string | Yetkilendirme (Azure aboneliği) açıklamasını alır veya ayarlar. |
| PCToBCExchangeRate | string | Ödeme para birimi döviz kurundaki fiyatlandırma para birimini alır veya ayarlar. |
| PCToBCExchangeRateDate | DateTime | Ödeme para birimi döviz kuru tarihine yönelik fiyatlandırma para birimini alır veya ayarlar. |
| Efekt, BirimFiyat | decimal | Geçerli birim fiyatını alır veya ayarlar. |
| Rateofpartnerearnedkrediyi | decimal | İş ortağı kazanılmış kredisi oranını alır veya ayarlar. |
| Haspartnerearnedkrediyi | bool | İş ortağı kazanılmış krediyi alır veya ayarlar. |
| Faturadan Elineıtemtype | Faturadan Elineıtemtype | Fatura çizgisi öğesinin türünü döndürür. |
| BillingProvider | BillingProvider | Faturalandırma sağlayıcısını döndürür. |
