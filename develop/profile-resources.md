---
title: Profil kaynakları
description: Bir bulut çözümü sağlayıcısının profillerinin davranışını açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e0561278995f4f9747320866b51de57efea8f712
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769664"
---
# <a name="profile-resources"></a>Profil kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir bulut çözümü sağlayıcısının profillerinin davranışını açıklar.

## <a name="billingprofile"></a>BillingProfile

Ortağın faturalandırma profilini açıklar.

| Özellik            | Tür                                                           | Description                                                 |
|---------------------|----------------------------------------------------------------|-------------------------------------------------------------|
| Tadı         | string                                                         | Faturalama şirket adı.                                   |
| adres             | [Adres](utility-resources.md#address)                       | Şirketin veya kuruluşun fatura adresi adresi. |
| primaryContact      | [İletişim](utility-resources.md#contact)                       | Şirket veya kuruluş için birincil iletişim.        |
| purchaseOrderNumber | string                                                         | Şirket veya kuruluşun satın alma siparişi numarası.        |
| TaxID               | string                                                         | Şirket veya kuruluşun vergi kimliği.                       |
| billingCurrency     | string                                                         | Şirket veya kuruluş tarafından kullanılan para birimi.           |
| profileType         | string                                                         | İş ortağı profili türü.                                   |
| Köprü               | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.            |
| öznitelikler          | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.       |

## <a name="legalbusinessprofile"></a>LegalBusinessProfile

Ortağın yasal iş profilini açıklar.

| Özellik               | Tür                                                           | Description                                                                                                                                                          |
|------------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tadı            | string                                                         | Yasal Şirket adı.                                                                                                                                              |
| adres                | [Adres](utility-resources.md#address)                       | Şirket veya kuruluşun adresi.                                                                                                                          |
| primaryContact         | [İletişim](utility-resources.md#contact)                       | Şirket veya kuruluş için birincil iletişim.                                                                                                                 |
| companyApproverAddress | [Adres](utility-resources.md#address)                       | Şirket onaylayanın adresi.                                                                                                                                        |
| companyApproverEmail   | string                                                         | Şirket onaylayan e-postası.                                                                                                                                          |
| vettingStatus          | string                                                         | Diting durumu. Bu değer, [**Vettingstatus**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingstatus)içinde bulunan üye adlarından birinin dize gösterimidir.           |
| Vettingalt durumu       | string                                                         | Diting alt durumu. Bu değer, [**Vettingalt durumu**](/dotnet/api/microsoft.store.partnercenter.models.partners.vettingsubstatus)'nda bulunan üye adlarından birinin dize gösterimidir. |
| profileType            | string                                                         | İş ortağı profili türü.                                                                                                                                            |
| Köprü                  | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.                                                                                                                     |
| öznitelikler             | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.                                                                                                                |

## <a name="mpnprofile"></a>MpnProfile

Ortağın Microsoft İş Ortağı Ağı profilini açıklar.

| Özellik    | Tür                                                           | Description                                           |
|-------------|----------------------------------------------------------------|-------------------------------------------------------|
| partnerName | string                                                         | Şirket veya kuruluş adı.                     |
| Mpnıd       | string                                                         | Microsoft İş Ortağı Ağı kimliği.                     |
| profileType | string                                                         | İş ortağı profili türü.                             |
| Köprü       | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profile karşılık gelen kaynak bağlantıları.      |
| öznitelikler  | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri. |

## <a name="organizationprofile"></a>OrganizationProfile

Ortağın kuruluş profilini açıklar.

| Özellik       | Tür                                                           | Description                                                            |
|----------------|----------------------------------------------------------------|------------------------------------------------------------------------|
| kimlik             | string                                                         | Kuruluşun kimliği.                                                 |
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

