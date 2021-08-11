---
title: Müşteri kullanım kaynakları
description: Kullanım tabanlı abonelikler ve aylık kullanım bütçeleri (CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary ve SpendingBudget dahil) olan müşteriler için kaynaklar.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066fd84f872365b419796f00125c097c685f4579731aaacd67e826bf671bd789
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995161"
---
# <a name="customer-usage-resources"></a>Müşteri kullanım kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Kullanım tabanlı abonelikleri olan müşteriler aylık kullanım bütçesine sahip olabilir. Bu bütçe, müşterinin maksimum kullanımına bir sınır ayarlar ve iş ortağının zaman içinde kullanımını izlemesine olanak sağlar.

> [!NOTE]
> Müşteri kullanım numaraları, faturalama amacıyla kullanılmayacak tahminlerdir (son değerler değildir).

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord,** geçerli ay içinde bir müşterinin kullanımının tahmini parasal maliyetini temsil eder.

| Özellik         | Tür               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Bütçe           | SpendingBudget     | Müşteri için ayrılan harcama bütçesi.                          |
| PercentUsed      | decimal             | Ayrılan bütçeden kullanılan yüzde.                        |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı.                                   |
| ResourceName     | string             | Kaynağın adı.                                                |
| Toplam Toplam Toplam        | decimal             | Abonelikte kaynaklar için tahmini toplam kullanım maliyeti.|
| CurrencyLocale   | string             | Müşterinin para birimi yerel değeri. Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir.            |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.           |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti ABD doları olarak alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| IsUpgraded       | bool             | Müşterinin Azure aboneliğinin yükseltilip yükseltil olmadığını belirten bir değer alır veya ayarlar. **true** değeri, Azure planına sahip olan müşterileri temsil eder.                         |
| LastModifiedDate olarak ayarlayın | date               | Kullanım verilerini son değiştirme tarihi.                               |
| Öznitelikler       | Resourceattributes | Kullanım kaydına karşılık gelen meta veri öznitelikleri.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**CustomerUsageSummary,** faturalama döneminin tamamı için müşterinin kullanımının özetini temsil eder.

| Özellik         | Tür               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Bütçe           | SpendingBudget     | Müşteri için ayrılan harcama bütçesi.                                                                  |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı. CustomerMonthlyUsageRecord bağlamında bu kimlik, müşteri kimliğidir. |
| ResourceName     | string             | Kaynağın adı. CustomerMonthlyUsageRecord bağlamında bu müşteri adıdır.               |
| BillingStartDate | date               | Geçerli faturalama döneminin başlangıç tarihi.                                                                    |
| BillingEndDate   | date               | Geçerli faturalama döneminin bitiş tarihi.                                                                      |
| Toplam Toplam Toplam        | decimal             | Abonelikte kaynaklar için tahmini toplam kullanım maliyeti.                                         |
| CurrencyLocale   | string             | Müşterinin para birimi yerel değeri. Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir.                                         |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti ABD doları olarak alır veya ayarlar. Azure planı abonelik kaynakları için kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | date               | Kullanım verilerini son değiştirme tarihi.                                                                       |
| Bağlantılar            | ResourceLinks      | Kullanım özetine karşılık gelen kaynak bağlantıları.                                                           |
| Öznitelikler       | Resourceattributes | Kullanım özetine karşılık gelen meta veri öznitelikleri.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**PartnerUsageSummary,** tüm müşteriler için kullanım bütçesinin iş ortağı düzeyindeki bir özetini temsil eder.

| Özellik         | Tür               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | dize dizisi   | Bildirimler için e-posta adresleri listesi.                                                                   |
| Müşter, bütçeyi aşan | tamsayı          | Bütçeyi alan müşterilerin sayısı.                                                                    |
| CustomersTrendingOver | tamsayı       | Bütçeyi üzerinden geçmek için yakın olan müşterilerin sayısı.                                                     |
| Customerswithusagebasedabonelikleri  | tamsayı | Kullanım tabanlı aboneliğe sahip müşterilerin sayısı.                                               |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı. CustomerMonthlyUsageRecord bağlamında bu KIMLIK müşteri KIMLIĞIDIR. |
| ResourceName     | string             | Kaynağın adı. CustomerMonthlyUsageRecord bağlamında, bu müşteri adıdır.               |
| BillingStartDate | date               | Geçerli fatura döneminin başlangıç tarihi.                                                                    |
| BillingEndDate   | date               | Geçerli fatura döneminin bitiş tarihi.                                                                      |
| Toplam maliyet        | decimal             | Fatura döneminin başından itibaren geçerli kullanıma bağlı olarak tüm müşteri kullanımının tahmini toplam maliyeti.      |
| CurrencyLocale   | string             | Para birimi yerel ayarı.                                                                                             |
| LastModifiedDate olarak ayarlayın | date               | Kullanım verilerinin son değiştirilme tarihi.                                                                       |
| Bağlantılar            | Resourcelmürekkepler      | Kullanım özetine karşılık gelen kaynak bağlantıları.                                                           |
| Öznitelikler       | ResourceAttributes | Kullanım özetine karşılık gelen meta veri öznitelikleri.                                                      |

## <a name="spendingbudget"></a>Spendingbütçe

**Spendingbütçe** , bu müşteriye kullanım tabanlı abonelikler için ayrılan bütçeyi temsil eder.

| Özellik   | Tür               | Description                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Miktar     | decimal             | Ayrılan bütçe. Değer null ise, bu müşteriye ayrılan harcama bütçesi yoktur. |
| Öznitelikler | ResourceAttributes | Bütçeye karşılık gelen meta veri öznitelikleri.                                                |
