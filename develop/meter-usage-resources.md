---
title: Ölçüm kullanım kaydı kaynağı
description: Geçerli fatura döngüsündeki bir aboneliğin ölçüm düzeyi kullanımının tahmini parasal maliyetini anlatmak için MeterUsageRecord kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c02c859d1d8ba3edd236d83d3056cb82533f7e8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768855"
---
# <a name="meter-usage-record-resource"></a>Ölçüm kullanım kaydı kaynağı

**Uygulama hedefi:**

- İş Ortağı Merkezi

Geçerli fatura döngüsündeki bir aboneliğin ölçüm düzeyi kullanımının tahmini parasal maliyetini anlatmak için **MeterUsageRecord** kaynağını kullanabilirsiniz.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Özellik         | Tür               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | Bir Microsoft Azure (MS-AZR-0145P) aboneliğini veya bir Azure planını temsil eden bir Iş Ortağı Merkezi [abonelik kaynağının](subscription-resources.md#subscription)tanımlayıcısına karşılık gelen bir GUID. Microsoft Azure (MS-AZR-0145P) abonelikleri için bu değer, ticaret abonelik tanımlayıcısıdır. Azure planı abonelik kaynakları için bu değer, Azure plan tanımlayıcısıdır.                  |
| MeterId  | string             | Ölçüm tanımlayıcısını alır veya ayarlar.                                                        |
| MeterName          | string             | Ölçüm adını alır veya ayarlar.                                       |
| Kategori               | string             | Azure Kaynak kategorisini alır veya ayarlar.                                                 |
| Alt Kategori             | string             |  Azure Kaynak alt kategorisini alır veya ayarlar.                                                     |
| Quantitykullanıldı        | decimal             | Kullanılan Azure kaynağının miktarını alır veya ayarlar.   |
| Birim   | string             | Azure kaynağı için ölçü birimini alır veya ayarlar. |
| Toplam maliyet   | decimal             | Tahmini toplam kullanım maliyetini alır veya ayarlar. |
| CurrencyLocale   | string             | Aboneliğin kullanıldığı yerel ayar. Bu özellik faturada kullanılan para birimini belirler. Bu özellik Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir. |
| CurrencyCode   | string             | Para birimi kodunu alır veya ayarlar. Bu özellik Azure planlarında kullanılabilir.                                         |
| USDTotalCost   | decimal             | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar. Bu özellik Azure planlarında kullanılabilir.                                         |
| LastModifiedDate olarak ayarlayın | string             | Bu kaydın son değiştirildiği gün (Tarih-saat biçiminde).                             |
| Öznitelikler       | ResourceAttributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                        |                                           |
