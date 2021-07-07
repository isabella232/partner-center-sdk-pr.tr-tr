---
title: Abonelik kullanım kaynakları
description: Abonelik kullanım kaynakları, kullanım tabanlı faturalamaya sahip abonelikleri açıklar. Bu aboneliklerin günlük ve aylık kullanım kayıtlarına ek olarak her ödeme dönemi için kullanım özeti vardır.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcb24dcf5ca8165ec23c4b187def38d05772e1de
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547385"
---
# <a name="subscription-usage-resources"></a>Abonelik kullanım kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Kullanım tabanlı faturalama ile belirli bir aboneliğe ilişkin kullanım bilgilerini almak için aşağıdaki abonelik kullanım kaynaklarını kullanabilirsiniz. Bu aboneliklerin günlük ve aylık kullanım kayıtlarına ek olarak her ödeme dönemi için kullanım özeti vardır.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

***SubscriptionDailyUsageRecord** kaynağı eskidir ve yanlış sonuçlar üretebilir. Uygulamalarınızı Azure için müşterinin kullanım kayıtlarını al ve Bunun yerine Azure için fiyatları al konusunda açıklanan [API'leri](get-a-customer-s-utilization-record-for-azure.md) [Microsoft Azure](get-prices-for-microsoft-azure.md) öneririz.*

**SubscriptionDailyUsageRecord** kaynağı, bir aboneliğin tek bir gün içinde ne kadar kullanı olduğunu açıklar.

| Özellik         | Tür               | Açıklama                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| DateUsed         | string             | Aboneliğin kullandığı tarih-saat biçimindeki gün.                                 |
| ResourceId       | string             | Guıd. Kaynağın benzersiz kimliği.                                                          |
| ResourceName     | string             | Kaynağın adı.                                                                     |
| Toplam Toplam Toplam        | decimal             | Belirtilen günde abonelikte kaynakları kullanmanın tahmini toplam maliyeti.     |
| CurrencyLocale   | string             | Aboneliğin kullanılan yerel ayarı, faturada kullanılacak para birimini belirler. |
| LastModifiedDate olarak ayarlayın | string             | Bu kaydın son değiştiril olduğu tarih-saat biçimindeki gün.                             |
| Öznitelikler       | Resourceattributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

**SubscriptionMonthlyUsageRecord** kaynağı, bir aboneliğin tek bir ay içinde ne kadar süreyle kullan olduğunu açıklar.

| Özellik         | Tür               | Açıklama                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Durum           | string             | Aboneliğin durumu: "hiçbiri", "etkin", "askıya alındı" veya "silindi".                  |
| PartnerOnRecord  | string             | "Kayıtta iş ortağının MPN kimliği."                                                        |
| OfferId          | string             | Guıd. Bu abonelikle ilgili teklifin kimliği.                                       |
| Id               | string             | Guıd. Aboneliğin veya kaynağın kimliği.                                                 |
| Name             | string             | Aboneliğin veya kaynağın adı.                                                     |
| Toplam Toplam Toplam        | decimal             | Belirtilen ay içinde abonelikte kaynakları kullanmanın tahmini toplam maliyeti.   |
| CurrencyLocale   | string             | Aboneliğin kullanılan yerel ayarı, faturada kullanılacak para birimini belirler. Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir. |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure planı abonelik kaynakları için kullanılabilir.                                         |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti ABD doları olarak alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | string             | Bu kaydın son değiştiril olduğu tarih-saat biçimindeki gün.                             |
| Öznitelikler       | Resourceattributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

**SubscriptionUsageSummary** kaynağı, geçerli faturalama döneminde belirli bir aboneliğin ne kadarı olduğunu açıklar.

| Özellik         | Tür               | Açıklama                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | string             | Guıd. Aboneliğin veya kaynağın kimliği. CustomerMonthlyUsageRecord bağlamında bu kimlik, müşteri kimliğidir. |
| ResourceName     | string             | Aboneliğin veya kaynağın adı. CustomerMonthlyUsageRecord bağlamında bu ad müşteri adıdır. |
| BillingStartDate | date               | Geçerli faturalama döneminin tarih-saat biçimindeki başlangıç tarihi.                                                     |
| BillingEndDate   | date               | Geçerli faturalama döneminin tarih-saat biçiminde bitiş tarihi.                                                       |
| Toplam Toplam Toplam        | double             | Belirtilen faturalama dönemi boyunca abonelikte kaynakları kullanmanın tahmini toplam maliyeti.               |
| CurrencyLocale   | string             | Aboneliğin kullanılan yerel ayarı, faturada kullanılacak para birimini belirler. Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir. |
| CurrencyCode   | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| USDTotalCost   | decimal             | Tahmini toplam maliyeti ABD doları olarak alır veya ayarlar. Azure planı abonelik kaynakları için kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | string             | Bu kaydın son değiştiril olduğu tarih-saat biçimindeki gün.                                                      |
| Bağlantılar            | ResourceLinks      | SubscriptionUsageSummary'ye karşılık gelen kaynak bağlantıları.                                                      |
| Öznitelikler       | Resourceattributes | SubscriptionUsageSummary'ye karşılık gelen meta veri öznitelikleri.                                                 |
