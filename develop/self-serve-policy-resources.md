---
title: Self Servis Ilkesi kaynakları
description: Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.
ms.date: 04/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04daf6aaeb69153c4139941188f53dbab8979969
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768951"
---
# <a name="selfservepolicy-resource"></a>SelfServePolicy kaynağı

**Uygulama hedefi:**

- İş Ortağı Merkezi

Bir iş ortağı, bir müşteri için self servis ilkelerini ayarlar.

## <a name="selfservepolicy"></a>SelfServePolicy

Bir sepet tanımlar.

| Özellik              | Tür             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | Self Servis ilkesinin başarıyla oluşturulması sırasında sağlanan self servis ilke tanımlayıcısı.     |
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
