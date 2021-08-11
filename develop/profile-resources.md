---
title: Profil kaynakları
description: Bir Bulut Çözümü Sağlayıcısı davranışını açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d4c091e186b7a3ad13aee7202b3d992af95db8db50acd40a5ade496d7087359
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997320"
---
# <a name="profile-resources"></a>Profil kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bir Bulut Çözümü Sağlayıcısı davranışını açıklar.

## <a name="billingprofile"></a>BillingProfile

Bir iş ortağının faturalama profilini açıklar.

| Özellik            | Tür                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| Şirketadı         | string                                                         | Faturalama şirketi adı.                                   |
| adres             | [Adres](utility-resources.md#address)                       | Şirketin veya kuruluşun faturalama adresi. |
| primaryContact      | [İletişim](utility-resources.md#contact)                       | Şirket veya kuruluş için birincil kişi.        |
| purchaseOrderNumber | string                                                         | Şirketin veya kuruluşun satın alma siparişi numarası.        |
| taxId               | string                                                         | Şirketin veya kuruluşun vergi numarası.                       |
| billingCurrency     | string                                                         | Şirket veya kuruluş tarafından kullanılan para birimi.           |
| profileType         | string                                                         | İş ortağı profili türü.                                   |
| Bağlantı               | [ResourceLinks](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.            |
| öznitelikler          | [Resourceattributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Bir iş ortağının yasal iş profilini açıklar.

| Özellik               | Tür                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Şirketadı            | string                                                         | Yasal şirket adı.                                                                                                                                              |
| adres                | [Adres](utility-resources.md#address)                       | Şirketin veya kuruluşun adresi.                                                                                                                          |
| primaryContact         | [İletişim](utility-resources.md#contact)                       | Şirket veya kuruluş için birincil kişi.                                                                                                                 |
| companyApproverAddress | [Adres](utility-resources.md#address)                       | Şirket onaylayan adresi.                                                                                                                                        |
| companyApproverEmail   | string                                                         | Şirket onaylayan e-postası.                                                                                                                                          |
| vettingStatus          | string                                                         | Risk durumu. Bu değer, [**VettingStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)içinde bulunan üye adlarından birinin dize gösterimidir.           |
| vettingSubStatus       | string                                                         | Yokma alt İstatistikleri. Bu değer, [**VettingSubStatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)içinde bulunan üye adlarından birinin dize gösterimidir. |
| profileType            | string                                                         | İş ortağı profili türü.                                                                                                                                            |
| Bağlantı                  | [ResourceLinks](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.                                                                                                                     |
| öznitelikler             | [Resourceattributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Bir iş ortağının Microsoft İş Ortağı Ağı açıklar.

| Özellik    | Tür                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | Şirket veya kuruluş adı.                     |
| mpnId       | string                                                         | Microsoft İş Ortağı Ağı (MPN) kimliği.                     |
| profileType | string                                                         | İş ortağı profili türü.                             |
| Bağlantı       | [ResourceLinks](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.      |
| öznitelikler  | [Resourceattributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri. |

## <a name="organizationprofile"></a>OrganizationProfile

Bir iş ortağının kuruluş profilini açıklar.

| Özellik       | Tür                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| kimlik             | string                                                         | Kuruluşun KIMLIĞI.                                                 |
| Tadı    | string                                                         | Şirket veya kuruluşun adı.                               |
| defaultAddress | [Adres](utility-resources.md#address)                       | Şirket veya kuruluşun varsayılan adresi.                    |
| Değerine       | string                                                         | Kiracı tanımlayıcısı.                                                 |
| etki alanı         | string                                                         | Şirket veya kuruluşun etki alanı.                                  |
| e-posta          | string                                                         | Üst aboneliği alır veya ayarlar.                                  |
| language       | string                                                         | İletişim için tercih edilen dil.                              |
| kültür        | string                                                         | İletişim ve para birimi için tercih edilen kültür ("en-US" gibi). |
| profileType    | string                                                         | İş ortağı profili türü.                                              |
| Köprü          | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.                       |
| öznitelikler     | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.                  |

## <a name="supportprofile"></a>SupportProfile

Ortağın Destek profilini açıklar.

| Özellik    | Tür                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| e-posta       | string                                                         | Profille ilişkili e-posta adresi.        |
| Telefon   | string                                                         | Profille ilişkili telefon numarası.         |
| web sitesi     | string                                                         | Destek Web sitesi.                                  |
| profileType | string                                                         | İş ortağı profili türü.                             |
| Köprü       | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.      |
| öznitelikler  | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri. |

