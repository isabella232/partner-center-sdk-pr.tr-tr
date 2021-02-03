---
title: Lisans kaynakları
description: Lisanslarıyla ilgili kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 681f53ec73122a4861e6f1a2f96560336481a068
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769485"
---
# <a name="license-resources"></a>Lisans kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Lisanslarıyla ilgili kaynakları açıklar.

## <a name="license"></a>Lisans

Bir kullanıcı lisansını açıklar.

>[!NOTE]
>21Vianet tarafından çalıştırılan Iş Ortağı Merkezi 'nde desteklenmez.

| Özellik     | Tür                                                           | Description                                                    |
|--------------|----------------------------------------------------------------|----------------------------------------------------------------|
| Hizmet planları | ServicePlan kaynakları dizisi                                 | Lisansa karşılık gelen hizmet planları koleksiyonu |
| productSKU 'Su   | ProductSku 'Su                                                     | Lisansa karşılık gelen ürünün SKU 'su.        |
| öznitelikler   | [ResourceAttributes](utility-resources.md#resourceattributes) | Lisansa karşılık gelen meta veri öznitelikleri.          |

## <a name="licenseupdate"></a>LicenseUpdate

Bir kullanıcıya lisans atamak veya kaldırmak için kullanılan bilgileri sağlar.

| Özellik         | Tür                                                           | Description                                               |
|------------------|----------------------------------------------------------------|-----------------------------------------------------------|
| licensestoAssign | nesne dizisi                                               | [Licenseatama](#licenseassignment) nesnelerinin dizisi. |
| licensesToRemove | dize dizisi                                               | Kaldırılacak lisansların Ürün SKU tanımlayıcıları.    |
| Licenseuyarılar  | nesne dizisi                                               | [Licensewarning](#licensewarning) nesnelerinin dizisi.       |
| öznitelikler       | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                  |

## <a name="licenseassignment"></a>Licenseatama

Bir lisans güncelleştirme işlemi için gereken bilgileri sağlar.

| Özellik      | Tür             | Description                                                                |
|---------------|------------------|----------------------------------------------------------------------------|
| Excludedplanlar | dize dizisi | Kullanım dışında tutulacak hizmet planı tanımlayıcıları. |
| skuId         | string           | Lisansın Ürün SKU 'SU tanımlayıcısı.                                |

## <a name="licensewarning"></a>LicenseWarning

Bir lisans güncelleştirme işlemi sırasında oluşan uyarı bilgilerini içerir.

| Özellik     | Tür             | Description                                         |
|--------------|------------------|-----------------------------------------------------|
| kod         | string           | Uyarı kodu.                                   |
| message      | string           | Uyarı iletisi.                                |
| Hizmet planları | dize dizisi | Uyarıyla ilişkili hizmet planı adları. |

## <a name="productsku"></a>ProductSku 'Su

Ürün ayrıntılarını açıklar.

| Özellik       | Tür             | Description                                         |
|----------------|------------------|-----------------------------------------------------|
| kimlik             | string           | Ürün tanımlayıcısı.                             |
| name           | string           | Kullanıcı asıl tanımlayıcısı.                      |
| skuPartNumber  | string           | Ürünün SKU parça numarası adı. Örneğin, Office 365 plan E3 için bu değer `EnterprisePack` . Kimlik yoksa, bu özellik kimlik yerine kullanılabilir.                |
| Öğesi     | string           | Ürünün hedef türü. Bu özellik, ürünün bir veya için geçerli olup olmadığını belirler `User` `Tenant` .                                                                    |
| Licensegroupıd | string           | , ProductSku lisansını yöneten yetkili veya hizmetten bir grup tanımlayıcısı aracılığıyla tanımlar. Ürünler, daha iyi yönetilebilirlik için lisans grupları altına alınır.<br/><br/>                                                                                     `group1` -Lisansları Azure Active Directory (AAD) tarafından yönetilebilecek tüm ürünler.<br/><br/>                                            `group2` -Minecrat ürün lisansları.                                         |

## <a name="serviceplan"></a>ServicePlan

Bir Ürün SKU 'SU içinde dağıtılabilir bir hizmeti tanımlar. Bir üründe birçok hizmet planı olabilir.

| Özellik         | Tür   | Description                                                                                                       |
|------------------|--------|-------------------------------------------------------------------------------------------------------------------|
| kimlik               | string | Hizmet planı tanımlayıcısı.                                                                                      |
| displayName      | string | Hizmet planının yerelleştirilmiş görünen adı.                                                                  |
| HizmetAdı      | string | Hizmet adı.                                                                                                 |
| capabilityStatus | string | Hizmet planının hizmet planı durumu.                                                                      |
| Öğesi       | string | Hizmet planının hedef türü. Bu özellik, ürünün bir "Kullanıcı" veya "Kiracı" için geçerli olup olmadığını belirler. |

## <a name="subscribedsku"></a>SubscribedSku

Bir kiracının sahip olduğu abone olunan bir ürünü açıklar.

| Özellik         | Tür                                                           | Description                                                                                       |
|------------------|----------------------------------------------------------------|---------------------------------------------------------------------------------------------------|
| availableUnits   | tamsayı                                                        | Atama için kullanılabilen birim sayısı. Bu değer toplam birim tüketilen birimler olarak hesaplanır. |
| activeUnits      | tamsayı                                                        | Atama için etkin birim sayısı.                                                        |
| Tüketim birimleri    | tamsayı                                                        | Tüketilen birim sayısı.                                                                     |
| suspendedUnits   | tamsayı                                                        | Askıya alınan birim sayısı.                                                                    |
| totalUnits       | tamsayı                                                        | Toplam birim sayısı. Bu değer, etkin ve uyarı birimlerinin toplamı olarak hesaplanır.         |
| warningUnits     | tamsayı                                                        | Uyarı birimlerinin sayısı.                                                                      |
| productSku 'Su       | ProductSku 'Su                                                     | Ürün SKU 'su.                                                                                  |
| Hizmet planları     | ServicePlan kaynakları dizisi                                 | Bir ürünün hizmet planları koleksiyonu.                                                     |
| capabilityStatus | string                                                         | Ürünün SKU durumu.                                                                      |
| öznitelikler       | [ResourceAttributes](utility-resources.md#resourceattributes) | Kaynağa karşılık gelen meta veri öznitelikleri.                                            |
