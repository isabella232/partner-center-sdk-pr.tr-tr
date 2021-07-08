---
title: Kaynak teklifi
description: Kurumsal bayi kataloğunda listelenen ve müşterilerine sunlarında buluna bir ürünü açıklar.
ms.date: 03/15/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 704e5580f2cdf84fc82b627e3b2ca165b81a3af5
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548116"
---
# <a name="offer-resources"></a>Kaynak teklifi

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Kurumsal bayi kataloğunda listelenen ve müşterilerine sunlarında buluna bir ürünü açıklar.

## <a name="offer"></a>Sunduğu

| Özellik                    | Tür                      | Açıklama                                                                                                                                                                |
|-----------------------------|---------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                          | string                    | Teklif tanımlayıcısı.                                                                                           |
| name                        | string                    | Teklif adı.                                                                                                 |
| açıklama                 | string                    | Teklifin açıklaması.                                                                                     |
| minimum Miktar             | int                       | Kullanılabilir minimum miktar.                                                                                 |
| maximumQuantity             | int                       | Kullanılabilir maksimum miktar.                                                                                 |
| derece                        | int                       | Aynı ürün hattında yer alan diğer kategorilere kıyasla teklif sıralaması veya önceliği. Bu özellik yalnızca, verilen bir ürün satırı için birden fazla teklif varsa ayarlanır.  |
| Urı                         | string                    | Teklif URI'si.                                                                                                  |
| locale                      | string                    | Teklifin geçerli olduğu yerel ayar.                                                                          |
| ülke                     | string                    | Teklifin geçerli olduğu ülke/bölge.                                                                    |
| category                    | [OfferCategory](#offercategory)           | Teklifin kategorisi.                                                                   |
| limitUnitOfMeasure          | string                    | Satın alma sınırlamasının türünü belirten bir değer. Olası değerler şunlardır:<br/> "Hiçbiri" - Satın alınan teklife bağlı olarak abonelik sayısıyla ilgili bir kısıtlama yoktur.<br/> "Eşzamanlı" - Belirli bir zamanda müşteri kiracısı üzerinde mevcut olan aboneliklerin sayısı; buna etkin veya iptal edilmiş abonelikler dahildir. Bu değer çoğunlukla lisans sayılarında 300'den az olan küçük işletme tekliflerini uygular. Sağlanan abonelikler sayılmaz.<br/> "LifeTime" - Müşteri kiracısı ömrü boyunca mevcut olan aboneliklerin sayısı. Bu değer en çok Denemeler için geçerlidir. Sağlanan abonelikler sayılmaz.      |
| limit                       | int                       | limitUnitOfMeasure temel alınarak bu teklifin satın alınabilirsiniz abonelik sayısı.                |
| prerequisiteOffers          | string                    | Önkoşul teklifleri.                                                                                        |
| isAddOn                     | boolean                   | Bu örneğin bir eklenti olup olmadığını belirten bir değer.                                                           |
| hasAddOns                   | boolean                   | Bu teklifte herhangi bir eklenti olup olmadığını belirten bir değer.                                                           |
| isAvailableForPurchase      | boolean                   | Bu örneğin satın alınabilir olup olmadığını belirten bir değer.                                             |
| billing                     | string                    | Satır öğesi satın alma için faturalama türünü belirtir: "none", "usage" veya "license".                           |
| supportedBillingCycles      | dize dizisi          | Bu teklif için desteklenen faturalama döngülerini gösterir. Desteklenen değerler [BillingCycleType](product-resources.md#billingcycletype) içinde bulunan üye adlarıdır   |
| isAutoRenewable             | boolean                   | Teklifin otomatik olarak yenilenip yenilenmey olmadığını belirten bir değer.                                                      |
| upgradeTargetOffers         | dize dizisi          | Bu teklif yükseltilebilir tekliflerin listesi.                                                          |
| conversionTargetOffers      | dize dizisi          | Bu teklifin dönüştürülmesi için tekliflerin listesi.                                                         |
| reselleeQualifications      | dize dizisi          | Bir iş ortağının bu müşteri için teklifi satın almak için müşteri tarafından gerekli olan nitelikler.     |
| resellerQualifications      | dize dizisi          | Müşteri için teklifi satın almak için iş ortağının gerekli nitelikler.                       |
| salesGroupId                | string                    | Teklifleri ayrı siparişlere ayırmak için kullanılan bir dize.                                                             |
| isTrial                     | boolean                   | Bunun bir deneme teklifi olup olmadığını belirten bir değer.                                                               |
| ürün                     | [OfferProduct](#offerproduct)           | Teklif ürününü alır.                                                                           |
| Unittype                    | string                    | Birimin türü.                                                                                      |
| Köprü                       | [OfferLinks](#offerlinks)               | Teklifin "daha fazla bilgi" bağlantısı.                                                                    |
| öznitelikler                  | [ResourceAttributes](utility-resources.md#resourceattributes) | Teklifine karşılık gelen meta veri öznitelikleri.                         |

## <a name="offercategory"></a>OfferCategory

Bir teklifin kategorilerini açıklar. Bu, aynı ürün satırındaki diğer kullanıcılarla karşılaştırılan bu teklif kategorisinin derecesini veya önceliğini içerir.

| Özellik   | Tür                                                           | Açıklama                                                                                                                                                                |
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

| Özellik  | Tür | Açıklama                 |
|-----------|------|-----------------------------|
| Daha fazlasını öğrenin | Bağlantı | "Daha fazla bilgi" bağlantısı.      |
| Self      | Bağlantı | Kendi kendine URI                |
| ileri      | Bağlantı | Öğelerin sonraki sayfası.     |
| Öncekini  | Bağlantı | Öğelerin önceki sayfası. |

## <a name="offerproduct"></a>OfferProduct

Her biri farklı özellik kümelerine ve farklı müşteri gereksinimlerine hedeflenmiş, kendisiyle ilişkili birden fazla teklifi olabilecek bir ürün veya hizmet.

| Özellik | Tür   | Açıklama              |
|----------|--------|--------------------------|
| Id       | string | Kategori tanımlayıcısı. |
| Name     | string | Kategori adı.       |
| Birim     | string | Ürün birimi.        |
