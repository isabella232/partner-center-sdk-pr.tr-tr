---
title: Ölçüm kullanım kaydı kaynağı
description: Geçerli fatura döngüsündeki bir aboneliğin ölçüm düzeyi kullanımının tahmini parasal maliyetini anlatmak için MeterUsageRecord kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbc8d1bd2cd3f9a9c1a657d88f3fe4899676e9df
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274657"
---
# <a name="meter-usage-record-resource"></a>Ölçüm kullanım kaydı kaynağı

**Uygulama hedefi:**

- İş Ortağı Merkezi

Geçerli fatura döngüsündeki bir aboneliğin ölçüm düzeyi kullanımının tahmini parasal maliyetini anlatmak için **MeterUsageRecord** kaynağını kullanabilirsiniz.

## <a name="meterusagerecord"></a>MeterUsageRecord

| Özellik         | Tür               | Description                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------|--------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId   | string             | Bir Microsoft Azure (MS-AZR-0145P) aboneliğini veya bir Azure planını temsil eden bir Iş Ortağı Merkezi [abonelik kaynağının](subscription-resources.md#subscription)tanımlayıcısına karşılık gelen bir GUID. Microsoft Azure (MS-AZR-0145P) abonelikleri için bu değer, ticaret abonelik tanımlayıcısıdır. Azure planı abonelik kaynakları için bu değer, Azure plan tanımlayıcısıdır. |
| MeterId          | string             | Ölçüm tanımlayıcısını alır veya ayarlar.                                                                                                                                                                                                                                                                                                                                                                  |
| MeterName        | string             | Ölçüm adını alır veya ayarlar.                                                                                                                                                                                                                                                                                                                                                                        |
| Kategori         | string             | Azure Kaynak kategorisini alır veya ayarlar.                                                                                                                                                                                                                                                                                                                                                           |
| Alt Kategori      | string             | Azure Kaynak alt kategorisini alır veya ayarlar.                                                                                                                                                                                                                                                                                                                                                       |
| Quantitykullanıldı     | decimal            | Kullanılan Azure kaynağının miktarını alır veya ayarlar.                                                                                                                                                                                                                                                                                                                                               |
| Birim             | string             | Azure kaynağı için ölçü birimini alır veya ayarlar.                                                                                                                                                                                                                                                                                                                                            |
| Toplam maliyet        | decimal            | Tahmini toplam kullanım maliyetini alır veya ayarlar.                                                                                                                                                                                                                                                                                                                                                     |
| CurrencyLocale   | string             | Aboneliğin kullanıldığı yerel ayar. Bu özellik faturada kullanılan para birimini belirler. Bu özellik Microsoft Azure (MS-AZR-0145P) abonelikleri için kullanılabilir.                                                                                                                                                                                                      |
| CurrencyCode     | string             | Para birimi kodunu alır veya ayarlar. Bu özellik Azure planlarında kullanılabilir.                                                                                                                                                                                                                                                                                                                         |
| USDTotalCost     | decimal            | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar. Bu özellik Azure planlarında kullanılabilir.                                                                                                                                                                                                                                                                                                           |
| LastModifiedDate olarak ayarlayın | string             | Bu kaydın son değiştirildiği gün (Tarih-saat biçiminde).                                                                                                                                                                                                                                                                                                                                   |
| Öznitelikler       | ResourceAttributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                                                                                                                                                                                                                                                                                                                              |
