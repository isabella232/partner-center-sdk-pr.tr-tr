---
title: Müşteri kaynakları
description: Müşteri veya satıcı temsil eden müşteri kaynakları.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 78622258880ab77ca99eae98082cc66acb3b66a7
ms.sourcegitcommit: 204e518e794b6b076a17488ee9ca1aaaa4beaaec
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/01/2021
ms.locfileid: "106103972"
---
# <a name="customer-resources"></a>Müşteri kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

## <a name="customer"></a>Müşteri

**Müşteri** kaynağı bir müşteriyi veya satıcısı temsil eder. Çoğu genel olarak, müşteri kaynağı Microsoft ve Microsoft 'un satıcıları ile iş yapmak isteyen herhangi bir kişi, çalışan veya kuruluş olabilir. Müşterilerin ayrıca bir şirket profili ve bir faturalandırma profili vardır.

>[!NOTE]
>**Müşteri** kaynağında, kiracı tanımlayıcısı başına dakikada 500 istekten oluşan bir hız limiti vardır.

| Özellik              | Tür                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                    | string                                                           | Müşteri KIMLIĞI.                                                                                                                             |
| commerceId            | string                                                           | Ticaret KIMLIĞI.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Şirket veya kuruluş hakkında ek bilgiler.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Faturalandırma için kullanılan ek bilgiler.                                                                                                     |
| relationshipToPartner | string                                                           | Bu müşteri için iş ortağının kullandığı lisanslama programını tanımlar: "none", "Bayi", "danışman", "dağıtım" veya "Microsoft \_ desteği". |
| allowDelegatedAccess  | boolean                                                          | İş ortağına bu müşteri tarafından atanan yönetici ayrıcalıkları verilip verilmediğini belirtir. Bu özellik yalnızca KIMLIĞE göre değil, bir müşteri alınırken kullanılabilir.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Kullanıcı kimlik bilgileri.                                                                                                                        |
| customDomains         | dize dizisi                                                 | Müşterinin özel etki alanları listesi.                                                                                                        |
| Ilişkili iş ortağı kimliği   | string                                                           | Bu müşteri hesabıyla ilişkilendirilen dolaylı satıcı. Bu değer, yalnızca dolaylı CSP iş ortakları tarafından ayarlanabilir.                              |
| Köprü                 | [Resourcelmürekkepler](utility-resources.md#resourcelinks)             | Profil içinde bulunan kaynak bağlantıları.                                                                                             |
| öznitelikler            | [ResourceAttributes](utility-resources.md#resourceattributes)   | Profile karşılık gelen meta veri öznitelikleri.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

**Customercompanyprofile** kaynağı, şirket veya kuruluş hakkında ek bilgiler.

| Özellik    | Tür                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| Değerine    | string                                                         | Azure AD için müşterinin kiracı tanımlayıcısı. Bu, aynı zamanda Microsoftıd olarak da adlandırılır. |
| etki alanı      | string                                                         | Contoso.onmicrosoft.com gibi müşterinin adı.                             |
| Tadı | string                                                         | Şirket veya kuruluşun adı.                                          |
| Köprü       | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profil içinde bulunan kaynak bağlantıları.                                  |
| öznitelikler  | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.                             |
|organizationRegistrationNumber|Dize|Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır). Yalnızca şu ülkelerde bulunan müşterinin şirketi/kuruluşu için gereklidir: Ermenistan (Har), Azerbaycan (AZ), Belarus (BY), Macaristan (HU), Kazakistan (KZ), Kırgızistan (KG), Moldova (MD), Rusya (RU), Tacikistan dili (TJ), Özbekistan (UZ), Ukrayna (UA), Hindistan, Brezilya, Güney Afrika, Polonya, Birleşik Arap Emirlikleri, Suudi Arabistan, Türkiye, Tayland, Vietnam, Myanmar, Irak, Güney Sudan ve Venezuela. Müşterinin veya diğer ülkelerde bulunan şirket/kuruluş için bu belirtilmemelidir.|


## <a name="customerbillingprofile"></a>CustomerBillingProfile

**Customerbillingprofile** kaynağı, müşteriyi faturalamak için kullanılan ek bilgiler.

| Özellik       | Tür                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik             | string                                                         | Profil tanımlayıcısı.                                                                                                                                |
| firstName      | string                                                         | Müşterinin şirketindeki faturalandırma kişisinin ilk adı. Bu, faturaların ve diğer faturalandırma iletişiminin yönlendirileceği kişidir. |
| lastName       | string                                                         | Faturalandırma kişisinin son adı.                                                                                                                  |
| e-posta          | string                                                         | Faturalandırma kişisinin e-posta adresi                                                                                                                    |
| kültür        | string                                                         | İletişim ve para birimi için tercih edilen kültür, "en-US" gibi.                                                                               |
| language       | string                                                         | İletişim için tercih edilen dili.                                                                                                            |
| Tadı    | string                                                         | Şirket veya kuruluşun adı.                                                                                                               |
| defaultAddress | [Adres](utility-resources.md#address)                       | Kambiyo senetlerinin gönderildiği, faturalama kişisinin çalıştığı adres.                                                                                   |
| Köprü          | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profil içinde bulunan kaynak bağlantıları.                                                                                                       |
| öznitelikler     | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

**Customerrelationshiprequest** kaynağı, müşteri tarafından bir iş ortağı ile bir satıcı ilişkisi kurmak için kullanılan URL 'yi içerir.

| Özellik   | Tür                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | string                                                         | Müşteri tarafından bir iş ortağıyla ilişki kurmak için kullanılan URL. |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes) | İlişki isteğine karşılık gelen meta veri öznitelikleri.       |