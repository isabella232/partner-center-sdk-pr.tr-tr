---
title: Self Servis Ilkesi kaynakları
description: Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e44581b805e076132984b67280699314e274ca94
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446726"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy kaynağı

Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.

## <a name="selfservepolicy"></a>SelfServePolicy

Bir sepet tanımlar.

| Özellik              | Tür             | Açıklama                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan kendi kendine bir ilke tanımlayıcısı.     |
| SelfServeEntity       | SelfServeEntity  | Erişim izni verilen self servis varlığı.                                                     |
| Verenin Grant izni               | Verenin Grant izni          | Erişim veren granör.                                                                    |
| İzinler           | Izin dizisi| [İzin](#permission) kaynakları dizisi.                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

İzin verilen varlığı temsil eder.

| Özellik             | Tür|Açıklama|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | string                           | Erişim izni verilen varlık, kabul edilen değerler: müşteri.                                 |
| Değerine             | string                           | Erişim izni verilen varlığın kiracı tanımlayıcısı.                                   |

## <a name="grantor"></a>Verenin Grant izni

İzinleri veren granayı temsil eder.

| Özellik             | Tür|Açıklama|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | string                           | Erişim verme, kabul edilen değerler: BillToPartner.                               |
| Değerine             | string                           | Erişim veren varlığın kiracı tanımlayıcısı.                                       |


## <a name="permission"></a>İzin

Self Servis ilkesindeki bir izni temsil eder.

| Özellik             | Tür|Açıklama|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Kaynak             | string                           | Kaynak erişimine çok fazla: Azurereservedınstances verildi.                          |
| Eylem               | string                           | Şu için eylem erişimi verildi: satın alma                                           |
