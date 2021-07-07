---
title: Ürün kaynakları
description: Satın edilebilir ürünleri veya hizmetleri temsil eden kaynaklar. Ürün türünü ve şeklini (SKU) açıklamaya ve stokta ürünün kullanılabilirliğini denetlemeye için kaynaklar içerir.
ms.date: 04/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1d536cb78c070bd06f4ab9434e066e51fb4c008c
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445893"
---
# <a name="products-resources"></a>Ürün kaynakları

Satın edilebilir ürünleri veya hizmetleri temsil eden kaynaklar. Ürün türünü ve şeklini (SKU) açıklamaya ve stokta ürünün kullanılabilirliğini denetlemeye için kaynaklar içerir.

## <a name="product"></a>Ürün

Satın edilebilir bir iyi veya hizmeti temsil eder. Tek başına ürün, satın edilebilir bir öğe değildir.

| Özellik           | Tür                          | Açıklama                                                              |
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

| Özellik        | Tür                          | Açıklama                                                                          |
|-----------------|-------------------------------|--------------------------------------------------------------------------------------|
| kimlik              | string                        | Tür tanımlayıcısı.                                                                 |
| displayName     | string                        | Bu tür için görünen ad.                                                      |
| Alt         | [ıtemtype](#itemtype)         | İsteğe bağlı. Bu öğe türü için bir alt tür kategorilerini açıklayan nesne.     |

## <a name="productlinks"></a>ProductLinks

Bir Ürün için bağlantıların listesini [içerir.](#product)

| Özellik        | Tür                                                          | Açıklama                                          |
|-----------------|---------------------------------------------------------------|------------------------------------------------------|
| Skus            | [Bağlantı](utility-resources.md#link)                             | Temel alınan SKUS'lara erişim bağlantısı.          |
| Bağlantı           | [ResourceLinks](utility-resources.md#resourcelinks)           | Bu kaynağın içinde yer alan kaynak bağlantıları.   |

## <a name="sku"></a>Sku

Ürün kapsamında satın alınabilir bir Stok Tutma Birimini (SKU) temsil eder. Bunlar ürünün farklı şekillerini temsil ediyor.

| Özellik               | Tür             | Açıklama                                                                           |
|------------------------|------------------|---------------------------------------------------------------------------------------|
| kimlik                     | string           | Bu SKU'nun kimliği. Bu kimlik yalnızca üst ürünü bağlamında benzersizdir. |
| başlık                  | string           | SKU'nun başlığı.                                                                 |
| açıklama            | string           | SKU açıklaması.                                                           |
| productId              | string           | Bu SKU'nun [yer alan](#product) üst Ürün kimliği.                      |
| minimum Miktar        | int              | Satın alma için izin verilen minimum miktar.                                            |
| maximumQuantity        | int              | Satın alma için izin verilen maksimum miktar.                                            |
| isTrial                | bool             | Bu SKU'nun bir deneme öğesi olup olmadığını gösterir.                                           |
| supportedBillingCycles | dize dizisi | Bu SKU için desteklenen faturalama döngülerinin listesi. Desteklenen değerler, [BillingCycleType](#billingcycletype)içinde bulunan üye adlarıdır. |
| purchasePrerequisites  | dize dizisi | Bu öğeyi satın almadan önce gerekli olan önkoşul adımlarının veya eylemlerin listesi. Desteklenen değerler:<br/>  "InventoryCheck" - Bu öğeyi satın alma girişiminde bulunmadan önce öğenin envanterini değerlendirmenin gerektiğini gösterir.<br/> "AzureSubscriptionRegistration" - Bir Azure aboneliği gerektiğini ve bu öğeyi satın alma girişiminden önce kayıtlı olması gerektiğini gösterir.  |
| inventoryVariables     | dize dizisi | Bu öğe üzerinde bir envanter denetimi yürütmek için gereken değişkenlerin listesi. Desteklenen değerler şunlardır:<br/> "CustomerID"-satınalmanın müşterinin KIMLIĞI.<br/> "Azu, Scriptionıd"-bir Azure ayırması satın alma için kullanılacak Azure aboneliğinin KIMLIĞI.</br> "ArmRegionName"-stok doğrulanacak bölge. Bu değer, SKU 'nun DynamicAttributes öğesinden "ArmRegionName" ile eşleşmelidir. |
| provisioningVariables  | dize dizisi | Bu öğe satın alınırken bir [sepet çizgisi öğesinin](cart-resources.md#cartlineitem) sağlama bağlamına sağlanması gereken değişkenlerin listesi. Desteklenen değerler şunlardır:<br/> Kapsam-bir Azure ayırması satın alma kapsamı: "tek", "paylaşılan".<br/> "SubscriptionID"-bir Azure ayırması satın alma için kullanılacak Azure aboneliğinin KIMLIĞI.<br/> "Duration"-Azure ayırma süresi: "1Year", "3Year".  |
| dynamicAttributes      | anahtar/değer çiftleri  | Bu öğe için uygulanan dinamik özelliklerin sözlüğü. Bu sözlükteki Özellikler dinamiktir ve bildirimde bulunmaksızın değiştirilebilir. Bu özelliğin değerinde mevcut olan belirli anahtarlar üzerinde güçlü bağımlılıklar oluşturmamalıdır.    |
| Köprü                  | [Resourcelmürekkepler](utility-resources.md#resourcelinks) | SKU içinde yer alan kaynak bağlantıları.                   |

## <a name="availability"></a>Kullanılabilirlik

Bir SKU 'nun satın alma için kullanılabildiği bir yapılandırmayı (ülke, para birimi ve sektör segmenti gibi) temsil eder.

| Özellik        | Tür                        | Açıklama                                                                         |
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
| ürün      | [Ürün](#product)               | Bu kullanılabilirliğinin karşılık geldiği ürün. |
| isteyin          | [İsteyin](#sku)            | Bu kullanılabilirliğinin karşılık geldiği SKU. |
| larındaki           | [terim](#term) dizisi kaynakları  | Bu kullanılabilirlik için geçerli olan koşulların toplanması. |
| Köprü           | [Resourcelmürekkepler](utility-resources.md#resourcelinks) | Kullanılabilirlik içinde yer alan kaynak bağlantıları. |

## <a name="term"></a>Süre

Kullanılabilirliğinin satın alınabilecek bir terimi temsil eder.

| Özellik              | Tür                                        | Açıklama                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| süre              | string                                      | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler P1M (1 ay), P1Y (1 yıl) ve P3Y (3 yıl). |
| açıklama           | string                                      | Terimin açıklaması.           |

## <a name="inventorycheckrequest"></a>Inventorycheckrequest

Belirli Katalog öğelerinin envanterini denetlemek için bir isteği temsil eder.

| Özellik         | Tür                                                | Açıklama                                                                                 |
|------------------|-----------------------------------------------------|---------------------------------------------------------------------------------------------|
| Targetıtems      | [ınventoryıtem](#inventoryitem) dizisi            | Envanter denetimi tarafından değerlendirilecek Katalog öğelerinin listesi.                           |
| ınventorycontext | anahtar/değer çiftleri                                     | Envanter denetimini yürütmek için gereken bağlam değerlerinin sözlüğü. Ürünlerin her [SKU 'su](#sku) , bu işlemi gerçekleştirmek için hangi değerlerin (varsa) gerekli olacağını tanımlar.  |
| Köprü            | [Resourcelmürekkepler](utility-resources.md#resourcelinks) | Envanter denetimi isteği içindeki kaynak bağlantıları.                            |

## <a name="inventoryitem"></a>Inventoryıtem

Bir envanter denetimi işleminde tek bir öğeyi temsil eder. Bu kaynak, bir giriş isteğindeki hedef öğeleri belirtmek için kullanılır ve ayrıca envanter denetimi işleminin çıkış sonuçlarını göstermek için kullanılır.

| Özellik         | Tür                                                              | Açıklama                                                                      |
|------------------|-------------------------------------------------------------------|----------------------------------------------------------------------------------|
| productId        | string                                                            | Istenir [Ürünün](#product)kimliği.                            |
| skuId            | string                                                            | [SKU](#sku)'nun kimliği. Bu kaynağı bir envanter isteğine giriş olarak kullanırken, bu değer isteğe bağlıdır. Bu değer sağlanmazsa, ürün altındaki tüm SKU 'Lar, envanter denetimi işleminin hedef öğeleri olarak kabul edilir.      |
| IsRestricted     | bool                                                              | Bu öğenin kısıtlı envanterle bulunup bulunmadığını gösterir.            |
| larından     | [ınventoryrestriction](#inventoryrestriction) dizisi            | Bu öğe için bulunan kısıtlamaların ayrıntıları. Bu özellik yalnızca **IsRestricted** = "true" ise doldurulur. |

## <a name="inventoryrestriction"></a>Inventoryrestriction

Bir stok kısıtlamasının ayrıntılarını temsil eder. Bu yalnızca envanter denetimi çıkış sonuçları için geçerlidir, giriş istekleri için geçerli değildir.

| Özellik         | Tür                  | Açıklama                                                                                 |
|------------------|-----------------------|---------------------------------------------------------------------------------------------|
| reasonCode       | string                | Kısıtlamanın nedenini tanımlayan kod.                                    |
| açıklama      | string                | Envanter kısıtlamasının açıklaması.                                               |
| properties       | anahtar/değer çiftleri       | Kısıtlama hakkında daha fazla ayrıntı sağlayabilen özelliklerin sözlüğü.           |

## <a name="billingcycletype"></a>BillingCycleType

Bir fatura döngüsünün türünü belirten değerler içeren bir [enum/DotNet/api/System. Enum).

| Değer              | Konum     | Açıklama                                                                                |
|--------------------|--------------|--------------------------------------------------------------------------------------------|
| Bilinmiyor            | 0            | Sabit Listesi başlatıcısı.                                                                          |
| Aylık            | 1            | Ortağın aylık olarak ücretlendirileceğini gösterir.                                        |
| Yıllık             | 2            | Ortağın yıllık olarak ücretlendirileceğini gösterir.                                       |
| Hiçbiri               | 3            | Ortağın ücretlendirilmeyeceğini belirtir. Bu değer, deneme öğeleri için kullanılabilir.    |
| Kerelik            | 4            | Ortağın bir kez ücretlendirileceğini gösterir.                                       |
