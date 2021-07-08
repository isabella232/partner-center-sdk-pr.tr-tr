---
title: Lisans kaynakları
description: Lisanslarıyla ilgili kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 27d44f89ac89f365e77e073c425ca45ab3638c68
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548405"
---
# <a name="license-resources"></a>Lisans kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Lisanslarıyla ilgili kaynakları açıklar.

## <a name="license"></a>Lisans

Bir kullanıcı lisansını açıklar.

>[!NOTE]
>21Vianet tarafından çalıştırılan Iş Ortağı Merkezi 'nde desteklenmez.

| Özellik     | Tür                                                           | Açıklama                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| Hizmet planları | ServicePlan kaynakları dizisi                                 | Lisansa karşılık gelen hizmet planları koleksiyonu |
| productSKU 'Su   | ProductSku 'Su                                                     | Lisansa karşılık gelen ürünün SKU 'su.        |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes) | Lisansa karşılık gelen meta veri öznitelikleri.          |

## <a name="licenseupdate"></a>LicenseUpdate

Bir kullanıcıya lisans atamak veya kaldırmak için kullanılan bilgileri sağlar.

| Özellik         | Tür                                                           | Açıklama                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | nesne dizisi                                               | [Licenseatama](#licenseassignment) nesnelerinin dizisi. |
| licensesToRemove | dize dizisi                                               | Kaldırılacak lisansların Ürün SKU tanımlayıcıları.    |
| Licenseuyarılar  | nesne dizisi                                               | [Licensewarning](#licensewarning) nesnelerinin dizisi.       |
| öznitelikler       | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                  |

## <a name="licenseassignment"></a>Licenseatama

Bir lisans güncelleştirme işlemi için gereken bilgileri sağlar.

| Özellik      | Tür             | Açıklama                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| Excludedplanlar | dize dizisi | Kullanım dışında tutulacak hizmet planı tanımlayıcıları. |
| skuId         | string           | Lisansın Ürün SKU 'SU tanımlayıcısı.                                |

## <a name="licensewarning"></a>LicenseWarning

Bir lisans güncelleştirme işlemi sırasında oluşan uyarı bilgilerini içerir.

| Özellik     | Tür             | Açıklama                                         |
|--------------|------------------|-----------------------------------------------------|
| kod         | string           | Uyarı kodu.                                   |
| message      | string           | Uyarı iletisi.                                |
| Hizmet planları | dize dizisi | Uyarıyla ilişkili hizmet planı adları. |

## <a name="productsku"></a>ProductSku 'Su

Ürün ayrıntılarını açıklar.

| Özellik       | Tür             | Açıklama                                         |
|----------------|------------------|-----------------------------------------------------|
| kimlik             | string           | Ürün tanımlayıcısı.                             |
| name           | string           | Kullanıcı asıl tanımlayıcısı.                      |
| skuPartNumber  | string           | Ürünün SKU parça numarası adı. örneğin, Office 365 Plan E3 için bu değer `EnterprisePack` . KIMLIK yoksa, bu özellik KIMLIK yerine kullanılabilir.                |
| Öğesi     | string           | Ürünün hedef türü. Bu özellik, ürünün bir veya için geçerli olup olmadığını belirler `User` `Tenant` .                                                                    |
| Licensegroupıd | string           | , ProductSku lisansını yöneten yetkili veya hizmetten bir grup tanımlayıcısı aracılığıyla tanımlar. Ürünler, daha iyi yönetilebilirlik için lisans grupları altına alınır.<br/><br/>                                                                                     `group1`-Lisansları Azure Active Directory (AAD) tarafından yönetilebilecek tüm ürünler.<br/><br/>                                            `group2`-Minecraft ürün lisansları.                                         |

## <a name="serviceplan"></a>ServicePlan

Bir Ürün SKU 'SU içinde dağıtılabilir bir hizmeti tanımlar. Bir üründe birçok hizmet planı olabilir.

| Özellik         | Tür   | Açıklama                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| kimlik               | string | Hizmet planı tanımlayıcısı.                                                                                      |
| displayName      | string | Hizmet planının yerelleştirilmiş görünen adı.                                                                  |
| Hizmetadı      | string | Hizmet adı.                                                                                                 |
| capabilityStatus | string | Hizmet planının hizmet planı durumu.                                                                      |
| Targettype       | string | Hizmet planının hedef türü. Bu özellik, ürünün "Kullanıcı" veya "Kiracı" için geçerli olup olmadığını tanımlar. |

## <a name="subscribedsku"></a>SubscribedSku

Kiracıya ait abone olunan bir ürünü açıklar.

| Özellik         | Tür                                                           | Açıklama                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | tamsayı                                                        | Atama için kullanılabilen birim sayısı. Bu değer, toplam birim ( tüketilen birimler) olarak hesaplanır. |
| activeUnits      | tamsayı                                                        | Atama için etkin birim sayısı.                                                        |
| consumedUnits    | tamsayı                                                        | Tüketilen birim sayısı.                                                                     |
| suspendedUnits   | tamsayı                                                        | Askıya alınan birim sayısı.                                                                    |
| totalUnits       | tamsayı                                                        | Toplam birim sayısı. Bu değer, etkin ve uyarı birimlerinin toplamı olarak hesaplanır.         |
| warningUnits     | tamsayı                                                        | Uyarı birimlerinin sayısı.                                                                      |
| productSku       | ProductSku                                                     | Ürün sku'su.                                                                                  |
| servicePlans     | ServicePlan kaynakları dizisi                                 | Bir ürünün hizmet planları koleksiyonu.                                                     |
| capabilityStatus | string                                                         | Bir ürünün sku durumu.                                                                      |
| öznitelikler       | [Resourceattributes](utility-resources.md#resourceattributes) | Kaynağa karşılık gelen meta veri öznitelikleri.                                            |
