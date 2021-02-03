---
title: Müşteri kullanım kaynakları
description: Kullanım tabanlı aboneliğe sahip müşterilere yönelik kaynaklar ve aylık kullanım bütçeleri (CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary ve Spendingbütçesi dahil).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ec82fcfe6c08a8ad55dd1fb48984859b954dd3c8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768794"
---
# <a name="customer-usage-resources"></a>Müşteri kullanım kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Kullanım tabanlı aboneliğe sahip müşteriler aylık kullanım bütçesine sahip olabilir. Bu bütçe, müşterinin en yüksek kullanım kullanımı için bir sınır ayarlar ve ortağın zaman içinde kullanımını izlemesine olanak sağlar.

> [!NOTE]
> Müşteri kullanım numaraları, Faturalandırma amacıyla kullanılmamalıdır (son değerler değil) tahminlerdir.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** , geçerli aydaki bir müşterinin kullanımının tahmini parasal maliyetini temsil eder.

| Özellik         | Tür               | Description                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Bütçe           | Spendingbütçe     | Müşteri için ayrılan harcama bütçesi.                          |
| Yüztused      | decimal             | Ayrılan bütçenin yüzdesi.                        |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı.                                   |
| ResourceName     | string             | Kaynağın adı.                                                |
| Toplam maliyet        | decimal             | Abonelikteki kaynaklar için tahmini toplam kullanım maliyeti.|
| CurrencyLocale   | string             | Müşterinin para birimi yerel ayarı. Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir.            |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.           |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| Iyükseltilen       | bool             | Müşterinin Azure aboneliğinin yükseltilip yükseltilmediğini gösteren bir değer alır veya ayarlar. **True** değeri, bir Azure planına sahip olan müşterileri temsil eder.                         |
| LastModifiedDate olarak ayarlayın | date               | Kullanım verilerinin son değiştirilme tarihi.                               |
| Öznitelikler       | ResourceAttributes | Kullanım kaydına karşılık gelen meta veri öznitelikleri.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**Customerusagesummary** , bir fatura döneminin tamamına ait müşterinin kullanımının özetini temsil eder.

| Özellik         | Tür               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Bütçe           | Spendingbütçe     | Müşteri için ayrılan harcama bütçesi.                                                                  |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı. CustomerMonthlyUsageRecord bağlamında bu kimlik müşteri kimliğidir. |
| ResourceName     | string             | Kaynağın adı. CustomerMonthlyUsageRecord bağlamında, bu müşteri adıdır.               |
| BillingStartDate | date               | Geçerli fatura döneminin başlangıç tarihi.                                                                    |
| BillingEndDate   | date               | Geçerli fatura döneminin bitiş tarihi.                                                                      |
| Toplam maliyet        | decimal             | Abonelikteki kaynaklar için tahmini toplam kullanım maliyeti.                                         |
| CurrencyLocale   | string             | Müşterinin para birimi yerel ayarı. Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir.                                         |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar. Azure plan aboneliği kaynakları için kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | date               | Kullanım verilerinin son değiştirilme tarihi.                                                                       |
| Bağlantılar            | Resourcelmürekkepler      | Kullanım özetine karşılık gelen kaynak bağlantıları.                                                           |
| Öznitelikler       | ResourceAttributes | Kullanım özetine karşılık gelen meta veri öznitelikleri.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**Partnerusagesummary** , tüm müşteriler için kullanım bütçesinin iş ortağı düzeyinde özetini temsil eder.

| Özellik         | Tür               | Description                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| EmailsToNotify   | dize dizisi   | Bildirimler için e-posta adresleri listesi.                                                                   |
| Müşter, bütçeyi aşan | tamsayı          | Bütçeyi alan müşterilerin sayısı.                                                                    |
| CustomersTrendingOver | tamsayı       | Bütçeyi üzerinden geçmek için yakın olan müşterilerin sayısı.                                                     |
| Customerswithusagebasedabonelikleri  | tamsayı | Kullanım tabanlı aboneliğe sahip müşterilerin sayısı.                                               |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı. CustomerMonthlyUsageRecord bağlamında bu kimlik müşteri kimliğidir. |
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
