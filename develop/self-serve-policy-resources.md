---
title: Self Servis Ilkesi kaynakları
description: Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffca78481572e201d3ef9f488e7d594a9c1176249b4415a347b488f4b9b81c51
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996776"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy kaynağı

Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.

## <a name="selfservepolicy"></a>SelfServePolicy

Bir sepet tanımlar.

| Özellik              | Tür             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan kendi kendine bir ilke tanımlayıcısı.     |
| SelfServeEntity       | SelfServeEntity  | Erişim izni verilen self servis varlığı.                                                     |
| Verenin Grant izni               | Verenin Grant izni          | Erişim veren granör.                                                                    |
| İzinler           | Izin dizisi| [İzin](#permission) kaynakları dizisi.                                                                     |

## <a name="selfserveentity"></a>SelfServeEntity

İzin verilen varlığı temsil eder.

| Özellik             | Tür|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| SelfServeEntityType  | string                           | Erişim izni verilen varlık, kabul edilen değerler: müşteri.                                 |
| Değerine             | string                           | Erişim izni verilen varlığın kiracı tanımlayıcısı.                                   |

## <a name="grantor"></a>Verenin Grant izni

İzinleri veren granayı temsil eder.

| Özellik             | Tür|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| GrantorType          | string                           | Erişim verme, kabul edilen değerler: BillToPartner.                               |
| Değerine             | string                           | Erişim veren varlığın kiracı tanımlayıcısı.                                       |


## <a name="permission"></a>İzin

Self Servis ilkesindeki bir izni temsil eder.

| Özellik             | Tür|Description|
|----------------------|----------------------------------|--------------------------------------------------------------------------------------------|
| Kaynak             | string                           | Kaynak erişimine çok fazla: Azurereservedınstances verildi.                          |
| Eylem               | string                           | Şu için eylem erişimi verildi: satın alma                                           |
