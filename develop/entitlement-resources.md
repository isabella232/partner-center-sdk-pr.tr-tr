---
title: Yetkilendirme kaynakları
description: Yetkilendirkaynaklarla ilgili kaynakları açıklar.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a5ddf5dcd1189f686c5d41c05d7c66abc46605cc
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906363"
---
# <a name="entitlement-resources"></a>Yetkilendirme kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

## <a name="entitlement"></a>Yetkilendirme

Bu kaynak, katalogdan öğeler üzerinde iş ortağı satın alma nedeniyle müşterinin kullanması gereken ürünleri temsil eder.

| Özellik | Tür | Açıklama |
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

| Özellik | Tür | Açıklama |
|----------|------|-------------|
| kimlik | string | Başvurulan siparişin KIMLIĞI. |
| Lineıtemıd | string | Başvurulan sipariş satırı öğesinin KIMLIĞI. |
| AlternateId | string | Başvurulan sipariş satırı öğesinin alternatif KIMLIĞI. |

## <a name="quantitydetail"></a>QuantityDetail

Bir yetkilendirme miktarının ayrıntılarını temsil eder.

| Özellik | Tür | Açıklama |
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

| Özellik | Tür | Açıklama |
|----------|------|-------------|
| artifactType | string | Yapıt türü. (SDK V 1.8 'de [ArtifactType](#artifacttype) 'dan dizeye güncelleştirilmiş) |
| dynamicAttributes | Sözlük &lt; dizesi, nesne&gt; | ArtifactType 'a özgü değerler içeren dinamik öznitelikler. örneğin, artifacttype = "reservedınstance" olduğunda, bu özellik "rezervationtype" = "virtualmachines" veya "rezervationtype" = "sqldatabases" ile sanal makine ayrılmış örneği veya Azure SQL ayrılmış örneği içerir. (SDK v 1.9 'den başlayarak kullanılabilir) |

## <a name="artifacttype"></a>ArtifactType

> [!IMPORTANT]
> SDK v 1.9 'da kullanım dışı

Yetkilendirme yapıtı türünü belirten değerler içeren bir [enum](/dotnet/api/system.enum) .

| Değer                          | Açıklama                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| Virtualmachinereservedınstance | Yapıt 'nin Azure ayrılmış sanal makine örneklerinin alınmasına yardımcı olduğunu gösterir. |

## <a name="reservedinstanceartifact"></a>Reservedınstanceartifact

Azure ayrılmış örneği yetkilendirimiyle ilişkilendirilen yapıt. [Yapıt](#artifact) sınıfından devralır.

| Özellik   | Tür                           | Açıklama                                        |
|------------|--------------------------------|----------------------------------------------------|
| bağlantı       | [Bağlantısının](./utility-resources.md#link) | İlişkili tüm yapıt ayrıntılarını almak için bağlantı.   |
| Resourceıd | string                         | Azure rezervasyon siparişinin veya kaynağının kimliği. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Azure Ayrılmış Örneği yapıtı bağlantısının çağrılsı üzerine döndürülen varlığı temsil eder.

|   Özellik   |           Tür           |                          Açıklama                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     tür     |          string          |                     Yapıt türü.                     |
| Rezervasyonlar | ıenumerable<Reservation> | Azure kaynağını veya rezervasyon siparişi tanımlayıcısını gösterir. |

## <a name="reservation"></a>Ayırma

Tek bir rezervasyonu temsil eder.

| Özellik          | Tür                           | Açıklama                                                        |
|-------------------|--------------------------------|--------------------------------------------------------------------|
| reservationId     | string                         | Rezervasyonun kimliği.                                         |
| scopeType         | string                         | Sanal makine rezervasyonuyla ilişkili kapsam türü. |
| displayName       | string                         | Rezervasyonun görünen adı.                               |
| appliedScopes     | ıenumerable                    | Rezervasyonla ilişkili uygulanan kapsamların listesi. (Yalnızca scopeType paylaşılmazken kullanılabilir.) |
| miktar          | int                            | Rezervasyonda sanal makine sayısı.                 |
| expiryDateTime    | UTC tarih-saat biçiminde dize | Rezervasyonun sona erme tarihi.                                |
| effectiveDateTime | UTC tarih-saat biçiminde dize | Rezervasyonun geçerli olduğu tarih.                             |
| provisioningState | string                         | Rezervasyonun sağlama durumu.                         |

## <a name="virtualmachinereservedinstanceartifact"></a>VirtualMachineReservedInstanceArtifact

> [!IMPORTANT]
> SDK v1.9'da kullanım dışı

Azure Ayrılmış Sanal Makine Örneği yetkilendirmesi ile ilişkili yapıt. [Yapıt](#artifact) sınıfından devralınır.

| Özellik   | Tür                              | Açıklama                                        |
|------------|-----------------------------------|----------------------------------------------------|
| bağlantı       | [Bağlantı](utility-resources.md#link) | İlişkili tüm yapıt ayrıntılarını almak için bağlantı.   |
| Resourceıd | string                            | Azure rezervasyon siparişinin veya kaynağının kimliği. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> SDK v1.9'da kullanım dışı

Azure Ayrılmış Sanal Makine Örneği yapıtı bağlantısının çağrılsı üzerine döndürülen varlığı temsil eder.

| Özellik                    | Tür                                                                 | Açıklama           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| tür                        | [Artifacttype](#artifacttype)                                        | Yapıt türü. |
| virtualMachineReservations  | [VirtualMachineReservation](#virtualmachinereservation)<IEnumerable> | Azure kaynağını veya rezervasyon siparişi tanımlayıcısını gösterir. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> SDK v1.9'da kullanım dışı

Tek bir sanal makine ayırmayı temsil eder.

|     Özellik      |              Tür              |                                                Açıklama                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         Rezervasyonun kimliği.                                         |
|     scopeType     |             string             |                     Sanal makine rezervasyonuyla ilişkili kapsam türü.                     |
|    displayName    |             string             |                                    Rezervasyonun görünen adı.                                    |
|   appliedScopes   |      ıenumerable<string>       | Rezervasyonla ilişkili uygulanan kapsamların listesi. (Yalnızca scopeType paylaşılmazken kullanılabilir.) |
|     miktar      |              int               |                             Rezervasyonda sanal makine sayısı.                             |
|  expiryDateTime   | UTC tarih-saat biçiminde dize |                                    Rezervasyonun sona erme tarihi.                                     |
| effectiveDateTime | UTC tarih-saat biçiminde dize |                                   Rezervasyonun geçerli olduğu tarih.                                   |
| provisioningState |             string             |                                 Ayırmanın sağlama durumu.                                 |
