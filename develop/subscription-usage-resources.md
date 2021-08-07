---
title: Abonelik kullanım kaynakları
description: Abonelik kullanım kaynakları, kullanım tabanlı faturalandırma ile abonelikleri anlatmaktadır. Bu aboneliklerin günlük ve aylık kullanım kayıtları, her ödeme dönemi için bir Kullanım Özeti vardır.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e8af4e9b8a4660b5bc9d287ece258dca9aa9ba7a749cfdc89e9c9b47e4af61b1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990282"
---
# <a name="subscription-usage-resources"></a>Abonelik kullanım kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Kullanım tabanlı faturalandırma ile belirli bir abonelik için kullanım bilgilerini almak üzere aşağıdaki abonelik kullanım kaynaklarını kullanabilirsiniz. Bu aboneliklerin günlük ve aylık kullanım kayıtları, her ödeme dönemi için bir Kullanım Özeti vardır.

## <a name="subscriptiondailyusagerecord"></a>SubscriptionDailyUsageRecord

***SubscriptionDailyUsageRecord** kaynağı kullanılmıyor ve hatalı sonuçlar verebilir. uygulamalarınızı [Azure için bir müşterinin kullanım kayıtlarını edinme](get-a-customer-s-utilization-record-for-azure.md) ve bunun yerine [Microsoft Azure fiyatları edinme](get-prices-for-microsoft-azure.md) konularında açıklanan apı 'leri kullanacak şekilde güncelleştirmenizi öneririz.*

**SubscriptionDailyUsageRecord** kaynağı, bir aboneliğin tek bir günde ne kadar kullanıldığını açıklar.

| Özellik         | Tür               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Tarih kullanıldı         | string             | Aboneliğin kullanıldığı tarih-saat biçiminde gün.                                 |
| ResourceId       | string             | 'İni. Kaynağın benzersiz KIMLIĞI.                                                          |
| ResourceName     | string             | Kaynağın adı.                                                                     |
| Toplam maliyet        | decimal             | Belirtilen gün içindeki abonelikteki kaynakları kullanmanın tahmini toplam maliyeti.     |
| CurrencyLocale   | string             | Aboneliğin kullanıldığı yerel ayar, faturada kullanılacak para birimini belirler. |
| LastModifiedDate olarak ayarlayın | string             | Tarih-saat biçiminde, bu kaydın son değiştirildiği gün.                             |
| Öznitelikler       | ResourceAttributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                        |

## <a name="subscriptionmonthlyusagerecord"></a>SubscriptionMonthlyUsageRecord

**SubscriptionMonthlyUsageRecord** kaynağı, bir aboneliğin tek bir ayda ne kadar kullanıldığını açıklar.

| Özellik         | Tür               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| Durum           | string             | Aboneliğin durumu: "none", "Active", "askıya alındı" veya "Deleted".                  |
| PartnerOnRecord  | string             | "Kayıt üzerinde iş ortağının MPN KIMLIĞI."                                                        |
| OfferId          | string             | 'İni. Bu abonelikle ilgili teklifin KIMLIĞI.                                       |
| Id               | string             | 'İni. Aboneliğin veya kaynağın KIMLIĞI.                                                 |
| Name             | string             | Aboneliğin veya kaynağın adı.                                                     |
| Toplam maliyet        | decimal             | Belirtilen aydaki abonelik içindeki kaynakları kullanmanın tahmini toplam maliyeti.   |
| CurrencyLocale   | string             | Aboneliğin kullanıldığı yerel ayar, faturada kullanılacak para birimini belirler. Microsoft Azure (MS-azr-0145p) abonelikleri için kullanılabilir. |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Azure plan aboneliği kaynakları için kullanılabilir.                                         |
| USDTotalCost     | decimal             | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | string             | Tarih-saat biçiminde, bu kaydın son değiştirildiği gün.                             |
| Öznitelikler       | ResourceAttributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                        |

## <a name="subscriptionusagesummary"></a>SubscriptionUsageSummary

**Subscriptionusagesummary** kaynağı, geçerli fatura döneminde belirli bir aboneliğin ne kadar kullanıldığını tanımlar.

| Özellik         | Tür               | Description                                                                                                            |
|------------------|--------------------|------------------------------------------------------------------------------------------------------------------------|
| ResourceId       | string             | 'İni. Aboneliğin veya kaynağın KIMLIĞI. CustomerMonthlyUsageRecord bağlamında bu KIMLIK müşteri KIMLIĞIDIR. |
| ResourceName     | string             | Aboneliğin veya kaynağın adı. CustomerMonthlyUsageRecord bağlamında, bu ad müşteri adıdır. |
| BillingStartDate | date               | Geçerli fatura döneminin tarih-saat biçiminde başlangıç tarihi.                                                     |
| BillingEndDate   | date               | Geçerli fatura döneminin tarih-saat biçiminde bitiş tarihi.                                                       |
| Toplam maliyet        | double             | Belirtilen faturalama dönemi boyunca abonelikte kaynakları kullanmanın tahmini toplam maliyeti.               |
| CurrencyLocale   | string             | Aboneliğin kullanılan yerel ayarı, faturada kullanılacak para birimini belirler. Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir. |
| CurrencyCode   | string             | Para birimi kodunu alır veya ayarlar. Azure planları için kullanılabilir.                                         |
| USDTotalCost   | decimal             | Tahmini toplam maliyeti ABD doları olarak alır veya ayarlar. Azure planı abonelik kaynakları için kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | string             | Bu kaydın son değiştiril olduğu tarih-saat biçimindeki gün.                                                      |
| Bağlantılar            | ResourceLinks      | SubscriptionUsageSummary'ye karşılık gelen kaynak bağlantıları.                                                      |
| Öznitelikler       | Resourceattributes | SubscriptionUsageSummary'ye karşılık gelen meta veri öznitelikleri.                                                 |
