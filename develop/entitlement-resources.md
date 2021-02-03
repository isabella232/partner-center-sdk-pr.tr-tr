---
title: Yetkilendirme kaynakları
description: Yetkilendirkaynaklarla ilgili kaynakları açıklar.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 428ac6f8b4d67894092119a6246279045a04dac0
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769299"
---
# <a name="entitlement-resources"></a>Yetkilendirme kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

## <a name="entitlement"></a>Yetkilendirme

Bu kaynak, katalogdan öğeler üzerinde iş ortağı satın alma nedeniyle müşterinin kullanması gereken ürünleri temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Yetkilendirbir şekilde sonuçlanan sıra başvurusu. |
| productId | string | Ürünün kimliği. |
| skuId | string | SKU 'nun KIMLIĞI. |
| miktar | int | Yetkilendirmelerin miktarı (yerine getirilmemiş/aktarmamış yetkilendirmeler hariç). |
| quantityDetails | IEnumerable<[Quantitydetail](#quantitydetail)> | Yetkilendirme miktarı ayrıntılarının listesi (öğelerin sayısı ve her bir miktarın durumu). |
| entitlementType | string | Yetkilendirme türü. (SDK 1,8 ' deki [EntitlementType](#entitlementtype) öğesinden dizeye güncelleştirildi.) |
| entitledArtifacts | IEnumerable<[yapıtı](#artifact)> | Yetkilendirmeden ilişkili yapıtların listesi. |
| Includedentitlements | IEnumerable<[Yetkilendirme](#artifact)> | Katalogdan satın alınan ProductID/SkuId 'in bir sonucu olarak örtük olarak dahil olan yetkilendirmelerin listesi. |
| ExpiryDate | UTC Tarih-saat biçiminde dize  | Yetkilendirme bitiş tarihi (varsa). |

## <a name="referenceorder"></a>ReferenceOrder

Yetkilendirbir yetkilendirme sırası başvurusu.

| Özellik | Tür | Description |
|----------|------|-------------|
| kimlik | string | Başvurulan siparişin KIMLIĞI. |
| Lineıtemıd | string | Başvurulan sipariş satırı öğesinin KIMLIĞI. |
| AlternateId | string | Başvurulan sipariş satırı öğesinin alternatif KIMLIĞI. |

## <a name="quantitydetail"></a>QuantityDetail

Bir yetkilendirme miktarının ayrıntılarını temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| miktar | int | Öğe sayısı. |
| durum | string | Miktarın durumu. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> SDK v 1.9 'da kullanım dışı

Yetkilendirme türünü belirten değerleri içeren bir [enum](/dotnet/api/system.enum) .

| Değer | Açıklama |
|-------|-------------|
| Yazılım | Yazılımla ilgili yetkilendirme türünü gösterir. |
| Virtualmachinereservedınstance | Azure ayrılmış sanal makine örnekleriyle ilgili yetkilendirme türünü gösterir. |

## <a name="artifact"></a>Yapıt

Yetkilendirmeden ilişkili yapıt.

| Özellik | Tür | Description |
|----------|------|-------------|
| artifactType | string | Yapıt türü. (SDK V 1.8 'de [ArtifactType](#artifacttype) 'dan dizeye güncelleştirilmiş) |
| dynamicAttributes | Sözlük &lt; dizesi, nesne&gt; | ArtifactType 'a özgü değerler içeren dinamik öznitelikler. Örneğin, artifactType = "reservedınstance" olduğunda, bu özellik "Rezervationtype" = "virtualmachines" veya "Rezervationtype" = "sqldatabases" (sanal makine ayrılmış örneği veya Azure SQL ayrılmış örneği) içerir. (SDK v 1.9 'den başlayarak kullanılabilir) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> SDK v 1.9 'da kullanım dışı

Yetkilendirme yapıtı türünü belirten değerler içeren bir [enum](/dotnet/api/system.enum) .

| Değer                          | Açıklama                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| Virtualmachinereservedınstance | Yapıt 'nin Azure ayrılmış sanal makine örneklerinin alınmasına yardımcı olduğunu gösterir. |

## <a name="reservedinstanceartifact"></a>Reservedınstanceartifact

Azure ayrılmış örneği yetkilendirimiyle ilişkilendirilen yapıt. [Yapıt](#artifact) sınıfından devralır.

| Özellik   | Tür                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| bağlantı       | [Bağlantı](./utility-resources.md#link) | Tüm ilişkili yapıt ayrıntılarını almak için bağlantı.   |
| RESOURCEID | string                         | Azure rezervasyon siparişi veya kaynağının KIMLIĞI. |

## <a name="reservedinstanceartifactdetails"></a>Reservedınstanceartifactdetails

Azure ayrılmış örnek yapıt bağlantısının çağrılmasıyla döndürülen varlığı temsil eder.

|   Özellik   |           Tür           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     tür     |          string          |                     Yapıt türü.                     |
| oluşturamaz | IEnumerable<Reservation> | Azure kaynağı veya rezervasyon siparişi tanımlayıcısını gösterir. |

## <a name="reservation"></a>Ayırma

Tek bir ayırmayı temsil eder.

| Özellik          | Tür                           | Description                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | Ayırmanın KIMLIĞI.                                         |
| Ssosession         | string                         | Sanal makine rezervasyonuna ilişkin kapsam türü. |
| displayName       | string                         | Ayırmanın görünen adı.                               |
| appliedScopes     | IEnumerable                    | Ayırma ile ilişkili uygulanan kapsamların listesi. (Yalnızca scopeType paylaştırılmamış olduğunda kullanılabilir.) |
| miktar          | int                            | Ayırma içindeki sanal makine sayısı.                 |
| Expirrivdatetime    | UTC Tarih-saat biçiminde dize | Ayırmanın sona erme tarihi.                                |
| Etkilenen bir tarih saat | UTC Tarih-saat biçiminde dize | Ayırmanın geçerlilik tarihi.                             |
| provisioningState | string                         | Ayırmanın sağlama durumu.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>Virtualmachinereservedınstanceartifact

> [!IMPORTANT]
> SDK v 1.9 'da kullanım dışı

Azure ayrılmış sanal makine örneği yetkilendirimiyle ilişkili yapıt. [Yapıt](#artifact) sınıfından devralır.

| Özellik   | Tür                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| bağlantı       | [Bağlantı](utility-resources.md#link) | Tüm ilişkili yapıt ayrıntılarını almak için bağlantı.   |
| RESOURCEID | string                            | Azure rezervasyon siparişi veya kaynağının KIMLIĞI. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>Virtualmachinereservedınstanceartifactdetails

> [!IMPORTANT]
> SDK v 1.9 'da kullanım dışı

Azure ayrılmış sanal makine örneği yapıt bağlantısının çağrılmasıyla döndürülen varlığı temsil eder.

| Özellik                    | Tür                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| tür                        | [ArtifactType](#artifacttype)                                        | Yapıt türü. |
| virtualMachineReservations  | IEnumerable<[Virtualmachinereservation](#virtualmachinereservation)> | Azure kaynağı veya rezervasyon siparişi tanımlayıcısını gösterir. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> SDK v 1.9 'da kullanım dışı

Tek bir sanal makine ayırmasını temsil eder.

|     Özellik      |              Tür              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         Ayırmanın KIMLIĞI.                                         |
|     Ssosession     |             string             |                     Sanal makine rezervasyonuna ilişkin kapsam türü.                     |
|    displayName    |             string             |                                    Ayırmanın görünen adı.                                    |
|   appliedScopes   |      IEnumerable<string>       | Ayırma ile ilişkili uygulanan kapsamların listesi. (Yalnızca scopeType paylaştırılmamış olduğunda kullanılabilir.) |
|     miktar      |              int               |                             Ayırma içindeki sanal makine sayısı.                             |
|  Expirrivdatetime   | UTC Tarih-saat biçiminde dize |                                    Ayırmanın sona erme tarihi.                                     |
| Etkilenen bir tarih saat | UTC Tarih-saat biçiminde dize |                                   Ayırmanın geçerlilik tarihi.                                   |
| provisioningState |             string             |                                 Ayırmanın sağlama durumu.                                 |
