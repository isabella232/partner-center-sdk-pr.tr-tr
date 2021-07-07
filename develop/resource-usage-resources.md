---
title: Kaynak kullanım kaydı kaynakları
description: Geçerli faturalama döngüsünde aboneliğin kaynak düzeyi kullanımının tahmini parasal maliyetini açıklamak için ResourceUsageRecord kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: eb626b9d4cb4c57a07f45bcf7b914f534e62ab68
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446590"
---
# <a name="resource-usage-record-resources"></a>Kaynak kullanım kaydı kaynakları

Geçerli faturalama döngüsünde aboneliğin kaynak düzeyi kullanımının tahmini parasal maliyetini açıklamak için **ResourceUsageRecord** kaynağını kullanabilirsiniz.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Özellik          | Tür               | Açıklama                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | string             | Abonelik tanımlayıcısını alır veya ayarlar. Daha Microsoft Azure (MS-AZR-0145P) abonelikleri için bu değer ticari abonelik tanımlayıcısıdır. Azure planları için bu değer Azure planı tanımlayıcısıdır). |
| ResourceUri       | string             | Kaynak URI'lerini alır veya ayarlar."                                                                                                                                                                            |
| ResourceType      | string             | Kaynak türünü alır veya ayarlar.                                                                                                                                                                            |
| EntitlementId     | string             | Yetkilendirme tanımlayıcısını (Azure abonelik tanımlayıcısı) alır veya ayarlar.                                                                                                                               |
| EntitlementName   | string             | Yetkilendirme adını alır veya ayarlar.                                                                                                                                                                         |
| ResourceGroupName | double             | Kaynak grubu adını alır veya ayarlar.                                                                                                                                                                      |
| Name              | string             | Kaynağın adı.                                                                                                                                                                                  |
| ResourceName      | string             | Kaynağın adını alır veya ayarlar.                                                                                                                                                                     |
| Toplam Toplam Toplam         | decimal            | Tahmini toplam maliyet kullanımını alır veya ayarlar.                                                                                                                                                               |
| CurrencyCode      | string             | Para birimi kodunu alır veya ayarlar.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Tahmini toplam maliyeti ABD doları olarak alır veya ayarlar.                                                                                                                                                              |
| LastModifiedDate olarak ayarlayın  | string             | Bu kaydın son değiştiril olduğu gün (tarih-saat biçiminde).                                                                                                                                          |
| Öznitelikler        | Resourceattributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                                                                                                                                     |
