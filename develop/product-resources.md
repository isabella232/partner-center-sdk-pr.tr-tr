---
title: Ürün kaynakları
description: Satın edilebilir ürünleri veya hizmetleri temsil eden kaynaklar. Ürün türünü ve şeklini (SKU) açıklamaya ve stokta ürünün kullanılabilirliğini denetlemeye için kaynaklar içerir.
ms.date: 02/16/2016
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 20e2d7bcaf1041f186f0723d7ff453bebbe46dd2
ms.sourcegitcommit: f112efee7344d739bdbf385adba0c554ea2a63e3
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/04/2021
ms.locfileid: "129439370"
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
| productType        | [Itemtype](#itemtype)         | Bu ürünün tür kategorilerini açıklayan bir nesne.     |
| isMicrosoftProduct | bool                          | Bunun bir Microsoft ürünü olup olmadığını gösterir.                          |
| publisherName      | string                        | Varsa ürünün yayımcısı adı.                          |
| Bağlantı              | [ProductLinks](#productlinks) | Ürünün içinde yer alan kaynak bağlantıları.                         |

## <a name="itemtype"></a>ItemType

Bir ürünün türünü temsil eder.

| Özellik        | Tür                          | Description                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| kimlik              | string                        | Tür tanımlayıcısı.                                                                 |
| displayName     | string                        | Bu tür için görünen ad.                                                      |
| Alt         | [Itemtype](#itemtype)         | İsteğe bağlı. Bu öğe türü için bir alt tür kategorilerini açıklayan nesne.     |

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
| supportedBillingCycles | dize dizisi | Bu SKU için desteklenen faturalama döngülerinin listesi. Desteklenen değerler, [BillingCycleType](#billingcycletype)içinde bulunan üye adlarıdır. |
| purchasePrerequisites  | dize dizisi | Bu öğeyi satın almadan önce gerekli olan önkoşul adımlarının veya eylemlerin listesi. Desteklenen değerler:<br/>  "InventoryCheck" - Bu öğeyi satın alma girişiminde bulunmadan önce öğenin envanterini değerlendirmenin gerektiğini gösterir.<br/> "AzureSubscriptionRegistration" - Bu öğeyi satın almak için önce bir Azure aboneliği gerektiğini ve kayıtlı olması gerektiğini gösterir.  |
| inventoryVariables     | dize dizisi | Bu öğe üzerinde bir envanter denetimi yürütmek için gereken değişkenlerin listesi. Desteklenen değerler şunlardır:<br/> "CustomerID"-satınalmanın müşterinin KIMLIĞI.<br/> "Azu, Scriptionıd"-bir Azure ayırması satın alma için kullanılacak Azure aboneliğinin KIMLIĞI.</br> "ArmRegionName"-stok doğrulanacak bölge. Bu değer, SKU 'nun DynamicAttributes öğesinden "ArmRegionName" ile eşleşmelidir. |
| provisioningVariables  | dize dizisi | Bu öğe satın alınırken bir [sepet çizgisi öğesinin](cart-resources.md#cartlineitem) sağlama bağlamına sağlanması gereken değişkenlerin listesi. Desteklenen değerler şunlardır:<br/> Kapsam-bir Azure ayırması satın alma kapsamı: "tek", "paylaşılan".<br/> "SubscriptionID"-bir Azure ayırması satın alma için kullanılacak Azure aboneliğinin KIMLIĞI.<br/> "Duration"-Azure ayırma süresi: "1Year", "3Year".  |
| dynamicAttributes      | anahtar/değer çiftleri  | Bu öğe için uygulanan dinamik özelliklerin sözlüğü. Bu sözlükteki Özellikler dinamiktir ve bildirimde bulunmaksızın değiştirilebilir. Bu özelliğin değerinde mevcut olan belirli anahtarlar üzerinde güçlü bağımlılıklar oluşturmamalıdır.    |
| Köprü                  | [Resourcelmürekkepler](utility-resources.md#resourcelinks) | SKU içinde yer alan kaynak bağlantıları.                   |
| AttestationProperties                  | [AttestationProperties](#attestationproperties) | SKU için kanıtlama özellikleri.                   |
| Tüketim Mptiontype                  | string | Yalnızca SKU, *fazla kullanım* gibi tüketimi destekliyorsa kullanılabilir.               |

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
| Köprü           | [ResourceLinks](utility-resources.md#resourcelinks) | Kullanılabilirlik içinde yer alan kaynak bağlantıları. |

## <a name="renewal-instruction"></a>Yenileme yönergesi

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir
> 

Belirli bir kullanılabilirlik için yenileme yönergelerini temsil eder.

| Özellik        | Tür                        | Description                                                                         |
|-----------------|-----------------------------------------------------|-------------------------------------------------------------|
| applicableTermIds       | dize dizisi                       | Yönergelerin geçerli olduğu Terim Kimlikleri |
| RenewalOptions       | RenewalOption dizisi                     | Yenilemeleri tanımlayan seçenekler |

## <a name="renewaloption"></a>RenewalOption    

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir
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
| Yıllık             | 2            | Ortağın yıllık olarak ücretlendirileceğini gösterir.                                       |
| Hiçbiri               | 3            | Ortağın ücretlendirilmeyeceğini belirtir. Bu değer, deneme öğeleri için kullanılabilir.    |
| Kerelik            | 4            | Ortağın bir kez ücretlendirileceğini gösterir.                                       |

## <a name="attestationproperties"></a>AttestationProperties

Bir kanıtlama türünü ve satın alma için gerekiyorsa temsil eder.

| Özellik              | Tür                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | string                                      | Kanıtlama türünü gösterir. Windows 365 için değer Windows365. Windows 365 kanıtlama metni "Windows hibrit avantajı ile Windows 365 iş kullanan her kişinin, birincil iş cihazında Windows 10/11 Pro geçerli bir kopyasına sahip olması gerektiğini anladım." |
| Enforcekanıtlama           | boolean                                      | Satın alma için kanıtlama gerekip gerekmediğini gösterir.           |
