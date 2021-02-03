---
title: Kaynak kullanım kaydı kaynakları
description: Geçerli fatura döngüsündeki bir aboneliğin kaynak düzeyi kullanımının tahmini parasal maliyetini anlatmak için ResourceUsageRecord kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6a293818cf4a6545dc705bf30fae6753f2e7eaf1
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768999"
---
# <a name="resource-usage-record-resources"></a>Kaynak kullanım kaydı kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi

Geçerli fatura döngüsündeki bir aboneliğin kaynak düzeyi kullanımının tahmini parasal maliyetini anlatmak için **ResourceUsageRecord** kaynağını kullanabilirsiniz.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Özellik         | Tür               | Description                                                                                   |
|------------------|--------------------|-----------------------------------------------------------------------------------------------|
| SubscriptionId           | string             | Abonelik tanımlayıcısını alır veya ayarlar. Microsoft Azure (MS-AZR-0145P) abonelikleri için bu değer, ticaret abonelik tanımlayıcısıdır. Azure planları için bu değer Azure plan tanımlayıcısıdır.                  |
| ResourceUri  | string             | Kaynak URI 'sini alır veya ayarlar. "                                                        |
| ResourceType          | string             | Kaynak türünü alır veya ayarlar.                                       |
| EntitlementId               | string             | Yetkilendirme tanımlayıcısını (Azure abonelik tanımlayıcısı) alır veya ayarlar.                                                 |
| EntitlementName             | string             | Yetkilendirme adını alır veya ayarlar.                                                     |
| ResourceGroupName        | double             | Kaynak grubu adını alır veya ayarlar.   |
| Name   | string             | Kaynağın adı. |
| ResourceName   | string             | Kaynağın adını alır veya ayarlar. |
| Toplam maliyet   | decimal             | Tahmini toplam maliyet kullanımını alır veya ayarlar. |
| CurrencyCode   | string             | Para birimi kodunu alır veya ayarlar.                                          |
| USDTotalCost   | decimal             | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar.                                         |
| LastModifiedDate olarak ayarlayın | string             | Bu kaydın son değiştirildiği gün (Tarih-saat biçiminde).                             |
| Öznitelikler       | ResourceAttributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                        |                                           |
