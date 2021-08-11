---
title: Teklif kaynakları
description: Satıcı kataloğunda listelenen, müşterilerine sunabileceği bir ürünü açıklar.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bcc5b60b7d1e3e13c38bd4014a81c2af254daa1d01ef33351b680463c3fee4a6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997915"
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
| Bağlantı                       | [OfferLinks](#offerlinks)               | Teklifin "daha fazla bilgi" bağlantısı.                                                                    |
| öznitelikler                  | [Resourceattributes](utility-resources.md#resourceattributes) | Teklife karşılık gelen meta veri öznitelikleri.                         |
| AttestationProperties       | [AttestationProperties](#attestationproperties) | SKU'nun attestation özellikleri.                   |

## <a name="offercategory"></a>OfferCategory

Teklifin kategorilere ayırmayı açıklar. Bu, teklif kategorisinin derecesini veya önceliğini, aynı ürün hattında yer alan diğer ürünlerle karşılaştırıldığında içerir.

| Özellik   | Tür                                                           | Description                                                                                                                                                                |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik         | string                                                         | Kategori tanımlayıcısı.                                                                                                                                                   |
| name       | string                                                         | Kategori adı.                                                                                                                                                         |
| derece       | int                                                            | Aynı teklifte yer alan diğer kategorilere kıyasla kategori sıralaması veya önceliği. Bu özellik yalnızca bir teklif için birden fazla teklif kategorisi varsa ayarlandır. |
| locale     | string                                                         | Teklifin geçerli olduğu yerel ayar.                                                                                                                        |
| ülke    | string                                                         | Teklifin geçerli olduğu ülke/bölge.                                                                                                                   |
| Bağlantı      | [ResourceLinks](utility-resources.md#resourcelinks)           | OfferCategory'ye karşılık gelen kaynak bağlantıları.                                                                                                                     |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes) | OfferCategory'ye karşılık gelen meta veri öznitelikleri.                                                                                                                |

## <a name="offerlinks"></a>OfferLinks

Teklif hakkında daha fazla bilgi için bağlantılar içerir.

| Özellik  | Tür | Description                 |
|-----------|------|-----------------------------|
| learnMore | Bağlantı | "Daha fazla bilgi" bağlantısı.      |
| Kendini      | Bağlantı | Kendi kendine URI                |
| ileri      | Bağlantı | Öğelerin sonraki sayfası.     |
| Önceki  | Bağlantı | Öğelerin önceki sayfası. |

## <a name="offerproduct"></a>OfferProduct

Her biri farklı özellik kümelerine sahip ve farklı müşteri ihtiyaçlarına yönelik birden fazla teklife sahip olan bir ürün veya hizmet.

| Özellik | Tür   | Description              |
|----------|--------|--------------------------|
| Id       | string | Kategori tanımlayıcısı. |
| Name     | string | Kategori adı.       |
| Birim     | string | Ürün birimi.        |

## <a name="attestationproperties"></a>AttestationProperties

Birstation türünü temsil eder ve satın alma için gerekli ise.

| Özellik              | Tür                                        | Description                                                                         |
|-----------------------|-----------------------------------------------------------------------------------|-------------------------------------------------------------------------------------|
| attestationType              | string                                      | Station türünü gösterir. 365 Windows Windows365 değeridir. Windows 365 doğrulama metninde "Windows 365 business with Windows Hybrid Benefit kullanan her bir kişinin de birincil iş cihazında geçerli Windows 10/11 Pro kopyasının yüklü olması gerektiğini anlıyoruz." |
| enforceAttestation           | boolean                                      | Satın alma için doğru olup olmadığını gösterir.           |

