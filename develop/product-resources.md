---
title: Ürün kaynakları
description: Satın alınabilir alınırken mal veya hizmetleri temsil eden kaynaklar. Ürün türünü ve şeklini (SKU) açıklayan kaynakları ve bir envanterde ürünün kullanılabilirliğini denetlemek için kaynaklar içerir.
ms.date: 02/16/2016
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3790d8f5ef154c637dfd3f3d014322d314757f26
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456078"
---
# <a name="products-resources"></a>Ürün kaynakları

Satın alınabilir alınırken mal veya hizmetleri temsil eden kaynaklar. Ürün türünü ve şeklini (SKU) açıklayan kaynakları ve bir envanterde ürünün kullanılabilirliğini denetlemek için kaynaklar içerir.

## <a name="product"></a>Ürün

Satın alınabilir alınırken iyi veya hizmeti temsil eder. Bir ürünün kendisi bir satın alınabilir alınırken öğesi değil.

| Özellik           | Tür                          | Description                                                              |
|--------------------|-------------------------------|--------------------------------------------------------------------------|
| kimlik                 | string                        | Bu ürünün KIMLIĞI.                                                 |
| başlık              | string                        | Ürün başlığı.                                                       |
| açıklama        | string                        | Ürün açıklaması.                                                 |
| productType        | [ItemType](#itemtype)         | Bu ürünün tür kategorilerini tanımlayan bir nesne.     |
| ımicrosoftürünü | bool                          | Bunun bir Microsoft ürünü olup olmadığını gösterir.                          |
| publisherName      | string                        | Varsa ürünün yayımcısının adı.                          |
| Köprü              | [ProductLinks](#productlinks) | Ürünün içinde yer alan kaynak bağlantıları.                         |

## <a name="itemtype"></a>ItemType

Ürünün türünü temsil eder.

| Özellik        | Tür                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| kimlik              | string                        | Tür tanımlayıcısı.                                                                 |
| displayName     | string                        | Bu tür için görünen ad.                                                      |
| subType         | [ItemType](#itemtype)         | İsteğe bağlı. Bu öğe türü için bir alt tür kategorisi tanımlayan nesne.     |

## <a name="productlinks"></a>ProductLinks

[Ürün](#product)için bağlantıların bir listesini içerir.

| Özellik        | Tür                                                          | Description                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| SKU            | [Bağlantı](utility-resources.md#link)                             | Temel SKU 'Lara erişme bağlantısı.          |
| Köprü           | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Bu kaynak içindeki kaynak bağlantıları.   |

## <a name="sku"></a>Sku

Bir ürün altındaki satın alınabilir alınırken stok tutma birimini (SKU) temsil eder. Bunlar, ürünün farklı şekillerini temsil eder.

| Özellik               | Tür             | Description                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| kimlik                     | string           | Bu SKU 'nun KIMLIĞI. Bu KIMLIK yalnızca üst ürününün bağlamı içinde benzersizdir. |
| başlık                  | string           | SKU 'nun başlığı.                                                                 |
| açıklama            | string           | SKU 'nun açıklaması.                                                           |
| productId              | string           | Bu SKU 'YU içeren üst [ürünün](#product) kimliği.                      |
| minimumQuantity        | int              | Satın alma için izin verilen minimum miktar.                                            |
| maximumQuantity        | int              | Satın alma için izin verilen maksimum miktar.                                            |
| Isdeneme                | bool             | Bu SKU 'nun bir deneme öğesi olup olmadığını gösterir.                                           |
| Supportedbillingdöngüleri | dize dizisi | Bu SKU için desteklenen faturalandırma döngülerinin listesi. Desteklenen değerler, [BillingCycleType](#billingcycletype)içinde bulunan üye adlarıdır. |
| purchasePrerequisites  | dize dizisi | Bu öğe satın almadan önce gerekli olan önkoşul adımlarının veya eylemlerinin listesi. Desteklenen değerler şunlardır:<br/>  "Inventorycheck"-Bu öğe satın alınmadan önce öğenin envanterinin değerlendirilmesi gerektiğini gösterir.<br/> "Azu, Scriptionregistration"-Bu öğeyi satın almaya çalışmadan önce bir Azure aboneliğinin gerekli olduğunu ve kaydedilmesi gerektiğini belirtir.  |
| ınventoryvariables     | dize dizisi | Bu öğe üzerinde bir envanter denetimi yürütmek için gereken değişkenlerin listesi. Desteklenen değerler şunlardır:<br/> "CustomerID"-satınalmanın müşterinin KIMLIĞI.<br/> "Azu, Scriptionıd"-bir Azure ayırması satın alma için kullanılacak Azure aboneliğinin KIMLIĞI.</br> "ArmRegionName"-stok doğrulanacak bölge. Bu değer, SKU 'nun DynamicAttributes öğesinden "ArmRegionName" ile eşleşmelidir. |
| provisioningVariables  | dize dizisi | Bu öğe satın alınırken bir [sepet çizgisi öğesinin](cart-resources.md#cartlineitem) sağlama bağlamına sağlanması gereken değişkenlerin listesi. Desteklenen değerler şunlardır:<br/> Kapsam-bir Azure ayırması satın alma kapsamı: "tek", "paylaşılan".<br/> "SubscriptionID"-bir Azure ayırması satın alma için kullanılacak Azure aboneliğinin KIMLIĞI.<br/> "Duration"-Azure ayırma süresi: "1Year", "3Year".  |
| dynamicAttributes      | anahtar/değer çiftleri  | Bu öğe için uygulanan dinamik özelliklerin sözlüğü. Bu sözlükteki Özellikler dinamiktir ve bildirimde bulunmaksızın değiştirilebilir. Bu özelliğin değerinde mevcut olan belirli anahtarlar üzerinde güçlü bağımlılıklar oluşturmamalıdır.    |
| Köprü                  | [Resourcelmürekkepler](utility-resources.md#resourcelinks) | SKU içinde yer alan kaynak bağlantıları.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | SKU için kanıtlama özellikleri.                   |

## <a name="dynamic-sku-attributes"></a>Dinamik SKU öznitelikleri

Yeni ticaret lisansı tabanlı ürünler ve hizmetlerle ilgili önemli özellikler.

> [!Note] 
> Yeni ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinin parçası olan iş ortakları tarafından kullanılabilir

| Özellik        | Tür                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
|Haskýsýtlamalarý|boolean|SKU 'nun Assetlitre içerip içerne olduğunu açıklar|
|isAddon|boolean|SKU 'nun bir ekleme olup olmadığını açıklar|
|ÖnkoşullarBu|dize dizisi|Eklentinin üzerinde çalıştığı ürünleri ve SKU 'ları açıklar|
|upgradeTargetOffers|dize dizisi|Öğenin yükseltilebilecek ürünlerin ve SKU 'ların listesi|
|Converstionyönergelerinin|Converstionyönergelerinin listesi|Conversat işlemlerine uygulanabilecek yönergelerin listesi|

## <a name="availability"></a>Kullanılabilirlik

Bir SKU 'nun satın alma için kullanılabildiği bir yapılandırmayı (ülke, para birimi ve sektör segmenti gibi) temsil eder.

| Özellik        | Tür                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------------------------------|
| kimlik              | string                        | Bu kullanılabilirliğinin KIMLIĞI. Bu KIMLIK yalnızca üst [ürün](#product) ve [SKU](#sku)'sunun bağlamı içinde benzersizdir. **Göz önünde** Bu KIMLIK, zaman içinde değişebilir. Bu değeri yalnızca kısa bir süre içinde aldıktan sonra almalısınız.  |
| productId       | string                        | Bu kullanılabilirliği içeren [ürünün](#product) kimliği.           |
| skuId           | string                        | Bu kullanılabilirliği içeren [SKU](#sku) 'nun kimliği.                   |
| Catalogıtemıd   | string                        | Katalogdaki bu öğe için benzersiz tanımlayıcı. Bu, üst [SKU](#sku)satın alınırken [Orderlineıtem. OfferId](order-resources.md#orderlineitem) veya [Cartlineıtem. CATALOGıTEMıD](cart-resources.md#cartlineitem) özelliklerine doldurulması gereken kimliğidir. **Göz önünde** Bu KIMLIK, zaman içinde değişebilir. Bu değere yalnızca kısa bir süre içinde güvenmelisiniz. Yalnızca, satın alma sırasında erişilmesi ve kullanılması gerekir.  |
| defaultCurrency | string                        | Bu kullanılabilirlik için desteklenen varsayılan para birimi.                               |
| segment         | string                        | Bu kullanılabilirlik için sektör segmenti. Desteklenen değerler şunlardır: ticari, eğitim, Kamu, kar amacı. |
| ülke         | string                                              | Bu kullanılabilirliğinin uygulandığı ülke veya bölge (ISO ülke kodu biçiminde). |
| isPurchasable   | bool                                                | Bu kullanılabilirliğinin satın alınabilir alınırken olup olmadığını gösterir. |
| ıyenilenebiliyor     | bool                                                | Bu kullanılabilirliğinin yenilenebilir olup olmadığını gösterir. |
| RenewalInstructions     | RenewalInstruction                                              | Belirli bir kullanılabilirlik için yenileme yönergelerini temsil eder. |
| ürün      | [Ürün](#product)               | Bu kullanılabilirliğinin karşılık geldiği ürün. |
| isteyin          | [İsteyin](#sku)            | Bu kullanılabilirliğinin karşılık geldiği SKU. |
| larındaki           | [terim](#term) dizisi kaynakları  | Bu kullanılabilirlik için geçerli olan koşulların toplanması. |
| Köprü           | [Resourcelmürekkepler](utility-resources.md#resourcelinks) | Kullanılabilirlik içinde yer alan kaynak bağlantıları. |

## <a name="renewal-instruction"></a>Yenileme yönergesi

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir
> 

Belirli bir kullanılabilirlik için yenileme yönergelerini temsil eder.

| Özellik        | Tür                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| applicableTermIds       | dize dizisi                       | Yönergelerin geçerli olduğu Terim Kimlikleri |
| RenewalOptions       | RenewalOption dizisi                     | Yenilemeleri tanımlayan seçenekler |

## <a name="renewaloption"></a>RenewalOption    

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir
> 

Belirli bir kullanılabilirlik için yenileme yönergelerini temsil eder.

| Özellik        | Tür                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| renewToId       | Dize       | Yenilenecek ürünü ve sku'ları temsil eder |
| isAutoRenewable       | Bool       | Kullanılabilirlik otomatik olarak yenilenip yenilene |

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

Faturalama dönemi türünü belirten değerlere sahip [Enum/dotnet/api/system.enum).

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
| attestationType              | string                                      | Station türünü gösterir. 365 Windows Windows365 değeridir. Windows 365 doğrulama metninde "Windows 365 business with Windows Hybrid Benefit kullanan her bir kişinin birincil iş cihazında geçerli Windows 10/11 Pro kopyasının da yüklü olması gerektiğini anlıyoruz." |
| enforceAttestation           | boolean                                      | Satın alma için doğru olup olmadığını gösterir.           |
