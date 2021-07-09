---
title: Yetkilendirme kaynakları
description: Yetkilendirmeyle ilgili kaynakları açıklar.
ms.date: 01/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 929004fff804675218e267bb928b432f7b1209bf
ms.sourcegitcommit: 84a6f701190f46d2adcf6edcaeaafa32d58fbaba
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2021
ms.locfileid: "113510117"
---
# <a name="entitlement-resources"></a>Yetkilendirme kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

## <a name="entitlement"></a>Yetkilendirme

Bu kaynak, katalogdaki öğelerde iş ortağı satın alma nedeniyle müşterinin kullanma hakkı olan ürünleri temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| referenceOrder | [ReferenceOrder](#referenceorder) | Yetkilendirmeyle sonuçlandıran sipariş başvurusu. |
| productId | string | Ürünün kimliği. |
| skuID | string | SKU'nun kimliği. |
| miktar | int | Yetkilendirme miktarı (Yerine getirilmemiş/Aktarıldı yetkilendirmeleri hariç). |
| quantityDetails | IEnumerable<[QuantityDetail](#quantitydetail)> | Yetkilendirme miktarı ayrıntıları listesi (öğe sayısı ve her bir miktarın durumu). |
| entitlementType | string | Yetkilendirme türü. (SDK 1.8'de [EntitlementType'tan](#entitlementtype) dizeye güncelleştirildi.) |
| entitledArtifacts | IEnumerable<[Yapıt](#artifact)> | Yetkilendirmeyle ilişkili yapıtların listesi. |
| IncludedEntitlements | IEnumerable<[Yetkilendirmesi](#artifact)> | Katalogdan ProductId / SkuId satın alma sonucunda örtülü olarak dahil edilen yetkilendirmelerin listesi. |
| ExpiryDate | UTC tarih-saat biçiminde dize  | Yetkilendirme sona erme tarihi (varsa). |

## <a name="referenceorder"></a>ReferenceOrder

Yetkilendirmenin sipariş başvurusu.

| Özellik | Tür | Description |
|----------|------|-------------|
| kimlik | string | Başvurulan siparişin kimliği. |
| lineItemId | string | Başvurulan sipariş satırı öğesinin kimliği. |
| alternateId | string | Başvurulan sipariş satırı öğesinin alternatif kimliği. |

## <a name="quantitydetail"></a>QuantityDetail

Yetkilendirme miktarının ayrıntılarını temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| miktar | int | Öğe sayısı. |
| durum | string | Miktarın durumu. |

## <a name="entitlementtype"></a>EntitlementType

> [!IMPORTANT]
> SDK v1.9'da kullanım dışı

[Yetkilendirme türünü](/dotnet/api/system.enum) belirten değerlere sahip bir Enum.

| Değer | Açıklama |
|-------|-------------|
| Yazılım | Yazılımla ilgili yetkilendirme türünü gösterir. |
| VirtualMachineReservedInstance | Kaynaklarla ilgili yetkilendirme türünü Azure Ayrılmış Sanal Makine Örnekleri. |

## <a name="artifact"></a>Yapıt

Yetkilendirmeyle ilişkili yapıt.

| Özellik | Tür | Description |
|----------|------|-------------|
| Artifacttype | string | Yapıt türü. (SDK V1.8'de [ArtifactType'tan](#artifacttype) dizeye güncelleştirildi) |
| dynamicAttributes | Sözlük &lt; dizesi, nesne&gt; | Yapıt türüne özgü değerler içeren dinamik öznitelikler. Örneğin artifactType = "reservedinstance" olduğunda, bu özellik sanal makine ayrılmış örneğine veya Azure SQL ayrılmış örneğine açıklama ek olarak "reservationType" = "virtualmachines" veya "reservationType" = "sqldatabases" ifadesini içerir. (SDK v1.9'dan başlayarak kullanılabilir) |

## <a name="artifacttype"></a>Artifacttype

> [!IMPORTANT]
> SDK v1.9'da kullanım dışı

Yetkilendirme [yapıt](/dotnet/api/system.enum) türünü belirten değerlere sahip bir Enum.

| Değer                          | Açıklama                                                                             |
|--------------------------------| ----------------------------------------------------------------------------------------|
| VirtualMachineReservedInstance | Uygulamanın alınmasıyla birlikte yapıt yardımcılarını Azure Ayrılmış Sanal Makine Örnekleri. |

## <a name="reservedinstanceartifact"></a>ReservedInstanceArtifact

Azure Ayrılmış Örneği yetkilendirmesi ile ilişkili yapıt. [Yapıt](#artifact) sınıfından devralınır.

| Özellik   | Tür                           | Description                                        |
|------------|--------------------------------|----------------------------------------------------|
| bağlantı       | [Bağlantı](./utility-resources.md#link) | İlişkili tüm yapıt ayrıntılarını almak için bağlantı.   |
| Resourceıd | string                         | Azure rezervasyon siparişinin veya kaynağının kimliği. |

## <a name="reservedinstanceartifactdetails"></a>ReservedInstanceArtifactDetails

Azure Ayrılmış Örneği yapıtı bağlantısının çağrılsı üzerine döndürülen varlığı temsil eder.

|   Özellik   |           Tür           |                          Description                          |
|--------------|--------------------------|---------------------------------------------------------------|
|     tür     |          string          |                     Yapıt türü.                     |
| Rezervasyonlar | `IEnumerable<Reservation>` | Azure kaynağını veya rezervasyon siparişi tanımlayıcısını gösterir. |

## <a name="reservation"></a>Ayırma

Tek bir rezervasyonu temsil eder.

| Özellik          | Tür                           | Description                                                        |
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

| Özellik   | Tür                              | Description                                        |
|------------|-----------------------------------|----------------------------------------------------|
| bağlantı       | [Bağlantı](utility-resources.md#link) | İlişkili tüm yapıt ayrıntılarını almak için bağlantı.   |
| Resourceıd | string                            | Azure rezervasyon siparişinin veya kaynağının kimliği. |

## <a name="virtualmachinereservedinstanceartifactdetails"></a>VirtualMachineReservedInstanceArtifactDetails

> [!IMPORTANT]
> SDK v1.9'da kullanım dışı

Azure Ayrılmış Sanal Makine Örneği yapıtı bağlantısının çağrılsı üzerine döndürülen varlığı temsil eder.

| Özellik                    | Tür                                                                 | Description           |
|-----------------------------|----------------------------------------------------------------------|-----------------------|
| tür                        | [Artifacttype](#artifacttype)                                        | Yapıt türü. |
| virtualMachineReservations  | [VirtualMachineReservation](#virtualmachinereservation)<IEnumerable> | Azure kaynağını veya rezervasyon siparişi tanımlayıcısını gösterir. |

## <a name="virtualmachinereservation"></a>VirtualMachineReservation

> [!IMPORTANT]
> SDK v1.9'da kullanım dışı

Tek bir sanal makine ayırmayı temsil eder.

|     Özellik      |              Tür              |                                                Description                                                 |
|-------------------|--------------------------------|------------------------------------------------------------------------------------------------------------|
|   reservationId   |             string             |                                         Rezervasyonun kimliği.                                         |
|     scopeType     |             string             |                     Sanal makine rezervasyonuyla ilişkili kapsam türü.                     |
|    displayName    |             string             |                                    Rezervasyonun görünen adı.                                    |
|   appliedScopes   |      `IEnumerable<string>`       | Rezervasyonla ilişkili uygulanan kapsamların listesi. (Yalnızca scopeType paylaşılmazken kullanılabilir.) |
|     miktar      |              int               |                             Rezervasyonda sanal makine sayısı.                             |
|  expiryDateTime   | UTC tarih-saat biçiminde dize |                                    Rezervasyonun sona erme tarihi.                                     |
| effectiveDateTime | UTC tarih-saat biçiminde dize |                                   Rezervasyonun geçerli olduğu tarih.                                   |
| provisioningState |             string             |                                 Rezervasyonun sağlama durumu.                                 |
