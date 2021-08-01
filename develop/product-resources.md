---
title: Ürün kaynakları
description: Satın edilebilir ürünleri veya hizmetleri temsil eden kaynaklar. Ürün türünü ve şeklini (SKU) açıklamaya ve stokta ürünün kullanılabilirliğini denetlemeye için kaynaklar içerir.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2e68df1f6955fb7feb9770377621c2d649b74e4a
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009148"
---
# <a name="products-resources"></a>Ürün kaynakları

Satın edilebilir ürünleri veya hizmetleri temsil eden kaynaklar. Ürün türünü ve şeklini (SKU) açıklamaya ve stokta ürünün kullanılabilirliğini denetlemeye için kaynaklar içerir.

## <a name="product"></a>Ürün

Satın edilebilir bir iyi veya hizmeti temsil eder. Tek başına ürün, satın edilebilir bir öğe değildir.

| Özellik           | Tür                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| kimlik                 | string                        | Bu ürünün kimliği.                                                 |
| başlık              | string                        | Ürün başlığı.                                                       |
| açıklama        | string                        | Ürün açıklaması.                                                 |
| productType        | [ıtemtype](#itemtype)         | Bu ürünün tür kategorilerini açıklayan bir nesne.     |
| isMicrosoftProduct | bool                          | Bunun bir Microsoft ürünü olup olmadığını gösterir.                          |
| publisherName      | string                        | Varsa ürünün yayımcısı adı.                          |
| Bağlantı              | [ProductLinks](#productlinks) | Ürünün içinde yer alan kaynak bağlantıları.                         |

## <a name="itemtype"></a>ItemType

Bir ürünün türünü temsil eder.

| Özellik        | Tür                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| kimlik              | string                        | Tür tanımlayıcısı.                                                                 |
| displayName     | string                        | Bu tür için görünen ad.                                                      |
| Alt         | [ıtemtype](#itemtype)         | İsteğe bağlı. Bu öğe türü için bir alt tür kategorilerini açıklayan nesne.     |

## <a name="productlinks"></a>ProductLinks

Bir Ürün için bağlantıların listesini [içerir.](#product)

| Özellik        | Tür                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Skus            | [Bağlantı](utility-resources.md#link)                             | Temel alınan SKUS'lara erişim bağlantısı.          |
| Bağlantı           | [ResourceLinks](utility-resources.md#resourcelinks)           | Bu kaynağın içinde yer alan kaynak bağlantıları.   |

## <a name="sku"></a>Sku

Ürün kapsamında satın alınabilir bir Stok Tutma Birimini (SKU) temsil eder. Bunlar ürünün farklı şekillerini temsil ediyor.

| Özellik               | Tür             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| kimlik                     | string           | Bu SKU'nun kimliği. Bu kimlik yalnızca üst ürünü bağlamında benzersizdir. |
| başlık                  | string           | SKU'nun başlığı.                                                                 |
| açıklama            | string           | SKU açıklaması.                                                           |
| productId              | string           | Bu SKU'nun [yer alan](#product) üst Ürün kimliği.                      |
| minimum Miktar        | int              | Satın alma için izin verilen minimum miktar.                                            |
| maximumQuantity        | int              | Satın alma için izin verilen maksimum miktar.                                            |
| isTrial                | bool             | Bu SKU'nun bir deneme öğesi olup olmadığını gösterir.                                           |
| supportedBillingCycles | dize dizisi | Bu SKU için desteklenen faturalama döngülerinin listesi. Desteklenen değerler [BillingCycleType](#billingcycletype)içinde bulunan üye adlarıdır. |
| purchasePrerequisites  | dize dizisi | Bu öğeyi satın almadan önce gerekli olan önkoşul adımlarının veya eylemlerin listesi. Desteklenen değerler:<br/>  "InventoryCheck" - Bu öğeyi satın alma girişiminde bulunmadan önce öğenin envanterini değerlendirmenin gerektiğini gösterir.<br/> "AzureSubscriptionRegistration" - Bu öğeyi satın almak için önce bir Azure aboneliği gerektiğini ve kayıtlı olması gerektiğini gösterir.  |
| inventoryVariables     | dize dizisi | Bu öğe üzerinde bir envanter denetimi yürütmek için gereken değişkenlerin listesi. Desteklenen değerler:<br/> "CustomerId" - Satın alma için satın alınan müşterinin kimliği.<br/> "AzureSubscriptionId" - Azure rezervasyon satın alma için kullanılacak Azure aboneliğinin kimliği.</br> "ArmRegionName" - Envanterin doğrulan yer olduğu bölge. Bu değer, SKU'nun DynamicAttributes'larından "ArmRegionName" ile eşleşmeli. |
| provisioningVariables  | dize dizisi | Bu öğeyi satın alırken bir sepet satır öğesinin sağlama bağlamında [sağlanması gereken](cart-resources.md#cartlineitem) değişkenlerin listesi. Desteklenen değerler:<br/> Kapsam - Azure rezervasyon satın alma kapsamı: "Tek", "Paylaşılan".<br/> "SubscriptionId" - Azure rezervasyon satın alma için kullanılacak Azure aboneliğinin kimliği.<br/> "Süre" - Azure rezervasyon süresi: "1Year", "3Year".  |
| dynamicAttributes      | anahtar/değer çiftleri  | Bu öğe için geçerli olan dinamik özellikler sözlüğü. Bu sözlükte özellikler dinamiktir ve bildirim olmadan değişebilir. Bu özelliğin değerinde mevcut olan belirli anahtarlara güçlü bağımlılıklar oluşturmamanız gerekir.    |
| Bağlantı                  | [ResourceLinks](utility-resources.md#resourcelinks) | SKU içinde yer alan kaynak bağlantıları.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | SKU'nun attestation özellikleri.                   |

## <a name="availability"></a>Kullanılabilirlik

SKU'nun satın alınabilir olduğu bir yapılandırmayı (ülke, para birimi ve sektör segmenti gibi) temsil eder.

| Özellik        | Tür                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| kimlik              | string                        | Bu kullanılabilirlik için kimlik. Bu kimlik yalnızca üst ürünü ve [SKU'su bağlamında](#product) [benzersizdir.](#sku) **Not** Bu kimlik zaman içinde değişebilir. Bu değeri aldıktan sonra yalnızca kısa bir süre içinde güvenin.  |
| productId       | string                        | Bu kullanılabilirliği [içeren](#product) ürünün kimliği.           |
| skuId           | string                        | Bu kullanılabilirliği [içeren SKU'nun](#sku) kimliği.                   |
| catalogItemId   | string                        | Katalogda bu öğenin benzersiz tanımlayıcısı. Bu, üst SKU satın alırken [OrderLineItem.OfferId](order-resources.md#orderlineitem) veya [CartLineItem.CatalogItemId](cart-resources.md#cartlineitem) özelliklerine doldurulması [gereken kimliktir.](#sku) **Not** Bu kimlik zaman içinde değişebilir. Bu değeri aldıktan kısa bir süre sonra güvenin. Yalnızca satın alma zamanında erişilsin ve kullanılmalıdır.  |
| defaultCurrency | string                        | Bu kullanılabilirlik için desteklenen varsayılan para birimi.                               |
| segment         | string                        | Bu kullanılabilirlik için sektör segmenti. Desteklenen değerler: Ticari, Eğitim, Kamu, Kar Amacı Gütmeyen. |
| ülke         | string                                              | Bu kullanılabilirlik durumunun geçerli olduğu ülke veya bölge (ISO ülke kodu biçiminde). |
| isPursable   | bool                                                | Bu kullanılabilirlik satın edilebilir olup olmadığını gösterir. |
| isRenewable     | bool                                                | Bu kullanılabilirlik yenilenebilir olup olmadığını gösterir. |
| ürün      | [Ürün](#product)               | Bu kullanılabilirlik ürününe karşılık gelen ürün. |
| Sku          | [Sku](#sku)            | Bu kullanılabilirlik SKU'su karşılık gelen. |
| Terim           | Terim [kaynakları](#term) dizisi  | Bu kullanılabilirlik için geçerli olan koşulların koleksiyonu. |
| Bağlantı           | [ResourceLinks](utility-resources.md#resourcelinks) | Kullanılabilirlik içinde yer alan kaynak bağlantıları. |

## <a name="term"></a>Süre

Kullanılabilirliği satın almak için bir terimi temsil eder.

| Özellik              | Tür                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| süre              | string                                      | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler P1M (1 ay), P1Y (1 yıl) ve P3Y (3 yıl) değerleridir. |
| açıklama           | string                                      | Terimin açıklaması.           |

## <a name="inventorycheckrequest"></a>InventoryCheckRequest

Belirli katalog öğelerine karşı envanteri denetleme isteğini temsil eder.

| Özellik         | Tür                                                | Description                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| targetItems      | [InventoryItem dizisi](#inventoryitem)            | Envanter denetimi tarafından değerlendirilecek katalog öğelerinin listesi.                           |
| inventoryContext | anahtar/değer çiftleri                                     | Envanter denetimlerini yapmak için gereken bağlam değerlerinin sözlüğü. Ürünlerin [her SKU'su](#sku) bu işlemi yapmak için hangi değerlerin (varsa) gerekli olduğunu tanımlar.  |
| Bağlantı            | [ResourceLinks](utility-resources.md#resourcelinks) | Envanter denetimi isteği içinde yer alan kaynak bağlantıları.                            |

## <a name="inventoryitem"></a>InventoryItem

Envanter denetimi işlemi içinde tek bir öğeyi temsil eder. Bu kaynak, bir giriş isteğinde hedef öğeleri belirtmek için kullanılır ve envanter denetimi işlemi çıktı sonuçlarını temsil etmek için de kullanılır.

| Özellik         | Tür                                                              | Description                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | string                                                            | (Gerekli) Ürünün [kimliği.](#product)                            |
| skuId            | string                                                            | [SKU'nun kimliği.](#sku) Bu kaynağı bir envanter isteğine giriş olarak kullanırken bu değer isteğe bağlıdır. Bu değer sağlanmayacaksa, ürün altındaki tüm SKU'lar envanter denetimi işlemi için hedef öğeler olarak kabul edilir.      |
| ısrestricted     | bool                                                              | Bu öğenin kısıtlı bir envantere sahip olup olmadığını gösterir.            |
| Kısıtlama -ları     | [InventoryRestriction dizisi](#inventoryrestriction)            | Bu öğe için bulunan tüm kısıtlamaların ayrıntıları. Bu özellik yalnızcaRestricted **=** "true" ise doldurulur. |

## <a name="inventoryrestriction"></a>InventoryRestriction

Envanter kısıtlaması ayrıntılarını temsil eder. Bu yalnızca stok denetimi çıkış sonuçları için geçerlidir, giriş istekleri için geçerli değildir.

| Özellik         | Tür                  | Description                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | string                | Kısıtlamanın nedenini tanımlayan kod.                                    |
| açıklama      | string                | Envanter kısıtlaması açıklaması.                                               |
| properties       | anahtar/değer çiftleri       | Kısıtlamayla ilgili daha fazla ayrıntı sağlay sözcükler sözlüğü.           |

## <a name="billingcycletype"></a>BillingCycleType

Faturalama dönemi türünü belirten değerlerin yer alan [Enum/dotnet/api/system.enum) değeri.

| Değer              | Konum     | Description                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Bilinmiyor            | 0            | Enum başlatıcı.                                                                          |
| Aylık            | 1            | İş ortağının aylık olarak ücret alın olacağını gösterir.                                        |
| Yıllık             | 2            | İş ortağının yıllık ücret alın olacağını gösterir.                                       |
| Hiçbiri               | 3            | İş ortağının ücret ödemesi olmadığını gösterir. Bu değer deneme öğeleri için kullanılabilir.    |
| OneTime            | 4            | İş ortağının bir kez ücret alın olacağını gösterir.                                       |

## <a name="attestationproperties"></a>AttestationProperties

Birstation türünü ve satın alma için gerekli ise temsil eder.

| Özellik              | Tür                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | string                                      | Station türünü gösterir. 365 Windows Windows365 değeridir. Windows 365 doğrulama metninde "Windows 365 business with Windows Hybrid Benefit kullanan her bir kişinin de birincil iş cihazında geçerli Windows 10/11 Pro kopyasının yüklü olması gerektiğini anlıyoruz." |
| enforceAttestation           | boolean                                      | Satın alma için doğru olup olmadığını gösterir.           |
