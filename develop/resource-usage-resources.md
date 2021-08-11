---
title: Kaynak kullanım kaydı kaynakları
description: Geçerli fatura döngüsündeki bir aboneliğin kaynak düzeyi kullanımının tahmini parasal maliyetini anlatmak için ResourceUsageRecord kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b330c49518bc12a63f2be731eef5c57884f5b15b706ce4007bbdf1a7bb8fab0e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996946"
---
# <a name="resource-usage-record-resources"></a>Kaynak kullanım kaydı kaynakları

Geçerli fatura döngüsündeki bir aboneliğin kaynak düzeyi kullanımının tahmini parasal maliyetini anlatmak için **ResourceUsageRecord** kaynağını kullanabilirsiniz.

## <a name="resourceusagerecord"></a>ResourceUsageRecord

| Özellik          | Tür               | Description                                                                                                                                                                                                |
|-------------------|--------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| SubscriptionId    | string             | Abonelik tanımlayıcısını alır veya ayarlar. Microsoft Azure (MS-azr-0145p) abonelikleri için bu değer, ticaret abonelik tanımlayıcısıdır. Azure planları için bu değer Azure plan tanımlayıcısıdır. |
| ResourceUri       | string             | Kaynak URI 'sini alır veya ayarlar. "                                                                                                                                                                            |
| ResourceType      | string             | Kaynak türünü alır veya ayarlar.                                                                                                                                                                            |
| EntitlementId     | string             | Yetkilendirme tanımlayıcısını (Azure abonelik tanımlayıcısı) alır veya ayarlar.                                                                                                                               |
| EntitlementName   | string             | Yetkilendirme adını alır veya ayarlar.                                                                                                                                                                         |
| ResourceGroupName | double             | Kaynak grubu adını alır veya ayarlar.                                                                                                                                                                      |
| Name              | string             | Kaynağın adı.                                                                                                                                                                                  |
| ResourceName      | string             | Kaynağın adını alır veya ayarlar.                                                                                                                                                                     |
| Toplam maliyet         | decimal            | Tahmini toplam maliyet kullanımını alır veya ayarlar.                                                                                                                                                               |
| CurrencyCode      | string             | Para birimi kodunu alır veya ayarlar.                                                                                                                                                                            |
| USDTotalCost      | decimal            | Tahmini toplam maliyeti USD cinsinden alır veya ayarlar.                                                                                                                                                              |
| LastModifiedDate olarak ayarlayın  | string             | Bu kaydın son değiştirildiği gün (Tarih-saat biçiminde).                                                                                                                                          |
| Öznitelikler        | ResourceAttributes | Kaynağa karşılık gelen meta veri öznitelikleri.                                                                                                                                                     |
