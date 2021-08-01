---
title: Teklif kaynakları
description: Satıcı kataloğunda listelenen, müşterilerine sunabileceği bir ürünü açıklar.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a7a0dd2dccc59536797c3ce533d9d8829a04f96
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009231"
---
# <a name="offer-resources"></a>Teklif kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Satıcı kataloğunda listelenen, müşterilerine sunabileceği bir ürünü açıklar.

## <a name="offer"></a>Sunduğu

| Özellik                    | Tür                      | Description                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                          | string                    | Teklif tanımlayıcısı.                                                                                           |
| name                        | string                    | Teklif adı.                                                                                                 |
| açıklama                 | string                    | Teklifin açıklaması.                                                                                     |
| minimumQuantity             | int                       | Kullanılabilir minimum miktar.                                                                                 |
| maximumQuantity             | int                       | Kullanılabilir maksimum miktar.                                                                                 |
| derece                        | int                       | Aynı ürün satırındaki diğer kategorilerle karşılaştırıldığında, teklif derecesi veya önceliği. Bu özellik yalnızca belirli bir ürün satırı için birden fazla teklif varsa ayarlanmalıdır.  |
| kullanılmamışsa                         | string                    | Teklif URI 'SI.                                                                                                  |
| locale                      | string                    | Teklifin geçerli olduğu yerel ayar.                                                                          |
| ülke                     | string                    | Teklifin uygulandığı ülke/bölge.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Teklifin kategorisi.                                                                   |
| limitUnitOfMeasure          | string                    | Satın alma sınırlaması türünü gösteren bir değer. Olası değerler şunlardır:<br/> "Hiçbiri"-satın alınan teklifi temel alan abonelik sayısında kısıtlama yoktur.<br/> "Eşzamanlı"-belirli bir zamanda müşteri kiracısında mevcut olabilecek aboneliklerin sayısı, bu, etkin veya iptal edilen abonelikleri içerir. Bu değer, genellikle lisans sayımlarının 300 ' den küçük olduğu küçük iş tekliflerini uygular. Ön hazırlaştırılmış abonelikler sayılmaz.<br/> "Ömür"-müşteri kiracının kullanım ömrü boyunca var olan aboneliklerin sayısı. Bu değer en çok deneme için geçerlidir. Ön hazırlaştırılmış abonelikler sayılmaz.      |
| limit                       | int                       | LimitUnitOfMeasure temel alınarak bu teklifin satın alınabilecek aboneliklerin sayısı.                |
| ÖnkoşullarBu          | string                    | Önkoşul teklifleri.                                                                                        |
| isAddOn                     | boolean                   | Bu örneğin bir eklenti olup olmadığını gösteren bir değer.                                                           |
| hasAddOns                   | boolean                   | Bu teklifin herhangi bir addons içerip içermediğini gösteren bir değer.                                                           |
| Isavailablesatın alma      | boolean                   | Bu örneğin satın alma için kullanılabilir olup olmadığını gösteren bir değer.                                             |
| billing                     | string                    | Satır öğesi satın alma için Faturalandırma türünü belirtir: "none", "Usage" veya "License".                           |
| Supportedbillingdöngüleri      | dize dizisi          | Bu teklif için desteklenen faturalandırma döngülerini gösterir. Desteklenen değerler [BillingCycleType](product-resources.md#billingcycletype) içinde bulunan üye adlarıdır   |
| isAutoRenewable             | boolean                   | Teklifin otomatik olarak desteklenip yenilemediğini gösteren bir değer.                                                      |
| upgradeTargetOffers         | dize dizisi          | Bu teklifin yükseltibileceği tekliflerin listesi.                                                          |
| conversionTargetOffers      | dize dizisi          | Bu teklifin dönüştürülebileceği tekliflerin listesi.                                                         |
| resellet Equal      | dize dizisi          | Bir iş ortağının teklifi satın alması için müşterinin gereken nitelikleri.     |
| Resellernitelikler      | dize dizisi          | Teklifi müşteri için satın almak üzere iş ortağı için gereken nitelikler.                       |
| Salesgroupıd                | string                    | Teklifleri ayrı siparişlerde gruplamak için kullanılan bir dize.                                                             |
| Isdeneme                     | boolean                   | Bunun deneme teklifi olup olmadığını gösteren bir değer.                                                               |
| ürün                     | [OfferProduct](#offerproduct)           | Teklif ürününü alır.                                                                           |
| unitType                    | string                    | Birimin türü.                                                                                      |
| Köprü                       | [OfferLinks](#offerlinks)               | Teklifin "daha fazla bilgi" bağlantısı.                                                                    |
| öznitelikler                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Teklifine karşılık gelen meta veri öznitelikleri.                         |
| AttestationProperties       | [AttestationProperties](#attestationproperties) | SKU için kanıtlama özellikleri.                   |

## <a name="offercategory"></a>OfferCategory

Bir teklifin kategorilerini açıklar. Bu, aynı ürün satırındaki diğer kullanıcılarla karşılaştırılan bu teklif kategorisinin derecesini veya önceliğini içerir.

| Özellik   | Tür                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik         | string                                                         | Kategori tanımlayıcısı.                                                                                                                                                   |
| name       | string                                                         | Kategori adı.                                                                                                                                                         |
| derece       | int                                                            | Kategori derecesi veya önceliği, aynı teklifteki diğer kategorilerle karşılaştırılır. Bu özellik yalnızca belirli bir teklif için birden fazla teklif kategorisi varsa ayarlanmalıdır. |
| locale     | string                                                         | Teklifin geçerli olduğu yerel ayar.                                                                                                                        |
| ülke    | string                                                         | Teklifin uygulandığı ülke/bölge.                                                                                                                   |
| Köprü      | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | OfferCategory öğesine karşılık gelen kaynak bağlantıları.                                                                                                                     |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes) | OfferCategory öğesine karşılık gelen meta veri öznitelikleri.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Teklif hakkında daha fazla bilgi edinmek için bağlantılar içerir.

| Özellik  | Tür | Description                 |
|-----------|------|-----------------------------|
| Daha fazlasını öğrenin | Bağlantı | "Daha fazla bilgi" bağlantısı.      |
| Self      | Bağlantı | Kendi kendine URI                |
| ileri      | Bağlantı | Öğelerin sonraki sayfası.     |
| Öncekini  | Bağlantı | Öğelerin önceki sayfası. |

## <a name="offerproduct"></a>OfferProduct

Her biri farklı özellik kümelerine ve farklı müşteri gereksinimlerine hedeflenmiş, kendisiyle ilişkili birden fazla teklifi olabilecek bir ürün veya hizmet.

| Özellik | Tür   | Description              |
|----------|--------|--------------------------|
| Id       | string | Kategori tanımlayıcısı. |
| Name     | string | Kategori adı.       |
| Birim     | string | Ürün birimi.        |

## <a name="attestationproperties"></a>AttestationProperties

Bir kanıtlama türünü ve satın alma için gerekiyorsa temsil eder.

| Özellik              | Tür                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | string                                      | Kanıtlama türünü gösterir. Windows 365 için değer Windows365. Windows 365 kanıtlama metni "Windows hibrit avantajı ile Windows 365 iş kullanan her kişinin, birincil iş cihazında Windows 10/11 Pro geçerli bir kopyasına sahip olması gerektiğini anladım." |
| Enforcekanıtlama           | boolean                                      | Satın alma için kanıtlama gerekip gerekmediğini gösterir.           |

