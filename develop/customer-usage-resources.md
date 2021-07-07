---
title: Müşteri kullanım kaynakları
description: Kullanım tabanlı aboneliğe sahip müşterilere yönelik kaynaklar ve aylık kullanım bütçeleri (CustomerMonthlyUsageRecord, CustomerUsageSummary, PartnerUsageSummary ve Spendingbütçesi dahil).
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eae516e2f759dfc2e8f80e946a835d70760c5c9e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973052"
---
# <a name="customer-usage-resources"></a>Müşteri kullanım kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Kullanım tabanlı aboneliğe sahip müşteriler aylık kullanım bütçesine sahip olabilir. Bu bütçe, müşterinin en yüksek kullanım kullanımı için bir sınır ayarlar ve ortağın zaman içinde kullanımını izlemesine olanak sağlar.

> [!NOTE]
> Müşteri kullanım numaraları, Faturalandırma amacıyla kullanılmamalıdır (son değerler değil) tahminlerdir.

## <a name="customermonthlyusagerecord"></a>CustomerMonthlyUsageRecord

**CustomerMonthlyUsageRecord** , geçerli aydaki bir müşterinin kullanımının tahmini parasal maliyetini temsil eder.

| Özellik         | Tür               | Açıklama                                                              |
|------------------|--------------------|--------------------------------------------------------------------------|
| Bütçe           | Spendingbütçe     | Müşteri için ayrılan harcama bütçesi.                          |
| Yüztused      | decimal             | Ayrılan bütçenin yüzdesi.                        |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı.                                   |
| ResourceName     | string             | Kaynağın adı.                                                |
| Toplam maliyet        | decimal             | Abonelikteki kaynaklar için tahmini toplam kullanım maliyeti.|
| CurrencyLocale   | string             | Müşterinin para birimi yerel ayarı. Microsoft Azure (MS-azr-0145p) abonelikleri için kullanılabilir.            |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.           |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| Iyükseltilen       | bool             | Müşterinin Azure aboneliğinin yükseltilip yükseltilmediğini gösteren bir değer alır veya ayarlar. **True** değeri, bir Azure planına sahip olan müşterileri temsil eder.                         |
| LastModifiedDate olarak ayarlayın | date               | Kullanım verilerinin son değiştirilme tarihi.                               |
| Öznitelikler       | ResourceAttributes | Kullanım kaydına karşılık gelen meta veri öznitelikleri.               |

## <a name="customerusagesummary"></a>CustomerUsageSummary

**Customerusagesummary** , bir fatura döneminin tamamına ait müşterinin kullanımının özetini temsil eder.

| Özellik         | Tür               | Açıklama                                                                                                      |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------|
| Bütçe           | Spendingbütçe     | Müşteri için ayrılan harcama bütçesi.                                                                  |
| ResourceId       | string             | Kaynağın benzersiz tanımlayıcısı. CustomerMonthlyUsageRecord bağlamında bu KIMLIK müşteri KIMLIĞIDIR. |
| ResourceName     | string             | Kaynağın adı. CustomerMonthlyUsageRecord bağlamında, bu müşteri adıdır.               |
| BillingStartDate | date               | Geçerli fatura döneminin başlangıç tarihi.                                                                    |
| BillingEndDate   | date               | Geçerli fatura döneminin bitiş tarihi.                                                                      |
| Toplam maliyet        | decimal             | Abonelikteki kaynaklar için tahmini toplam kullanım maliyeti.                                         |
| CurrencyLocale   | string             | Müşterinin para birimi yerel ayarı. Microsoft Azure (MS-azr-0145p) abonelikleri için kullanılabilir.                                         |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar. Azure plan aboneliği kaynakları için kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | date               | Kullanım verilerinin son değiştirilme tarihi.                                                                       |
| Bağlantılar            | Resourcelmürekkepler      | Kullanım özetine karşılık gelen kaynak bağlantıları.                                                           |
| Öznitelikler       | ResourceAttributes | Kullanım özetine karşılık gelen meta veri öznitelikleri.                                                      |

## <a name="partnerusagesummary"></a>PartnerUsageSummary

**Partnerusagesummary** , tüm müşteriler için kullanım bütçesinin iş ortağı düzeyinde özetini temsil eder.

| Özellik         | Tür               | Açıklama                                                                                                      |
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

| Özellik   | Tür               | Açıklama                                                                                         |
|------------|--------------------|-----------------------------------------------------------------------------------------------------|
| Miktar     | decimal             | Ayrılan bütçe. Değer null ise, bu müşteriye ayrılan harcama bütçesi yoktur. |
| Öznitelikler | ResourceAttributes | Bütçeye karşılık gelen meta veri öznitelikleri.                                                |
