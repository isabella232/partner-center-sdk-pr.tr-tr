---
title: Müşteri kaynakları
description: Bir müşteriyi veya kurumsal bayiyi temsil eden müşteri kaynakları.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 10798ae0bfae8c1a4e38777096861427992b8aee3799ee2dd9154c6f0e0c0799
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995178"
---
# <a name="customer-resources"></a>Müşteri kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

## <a name="customer"></a>Müşteri

Müşteri **kaynağı** bir müşteriyi veya kurumsal bayiyi temsil eder. Müşteri kaynakları, genel olarak Microsoft ve Microsoft'un kurumsal bayileriyle iş yapmak isteyen herhangi bir kişi, çalışan veya kuruluş olabilir. Müşterilerin bir şirket profili ve faturalama profili de vardır.

>[!NOTE]
>Müşteri **kaynağının** kiracı tanımlayıcısı başına dakikada 500 istek hız sınırı vardır.

| Özellik              | Tür                                                             | Description                                                                                                                                  |
|-----------------------|------------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                    | string                                                           | Müşteri kimliği.                                                                                                                             |
| commerceId            | string                                                           | Ticari kimlik.                                                                                                                             |
| companyProfile        | [CustomerCompanyProfile](#customercompanyprofile)                | Şirket veya kuruluş hakkında ek bilgiler.                                                                                    |
| billingProfile        | [CustomerBillingProfile](#customerbillingprofile)                | Faturalama için kullanılan ek bilgiler.                                                                                                     |
| relationshipToPartner | string                                                           | İş ortağının bu müşteri için kullandığı lisans programını tanımlar: "none", "reseller", "advisor", "syndication" veya "microsoft \_ support". |
| allowDelegatedAccess  | boolean                                                          | İş ortağına bu müşteri tarafından yönetici ayrıcalıklarının temsilci olarak verilmiş olup olmadığını gösterir. Bu özellik yalnızca, listeye göre değil, kimliğine göre müşteri almada kullanılabilir.                                                         |
| userCredentials       | [UserCredentials](user-resources.md#usercredentials) | Kullanıcı kimlik bilgileri.                                                                                                                        |
| customDomains         | dize dizisi                                                 | Müşterinin özel etki alanlarının listesi.                                                                                                        |
| associatedPartnerId   | string                                                           | Bu müşteri hesabıyla ilişkili dolaylı kurumsal bayi. Bu değer yalnızca dolaylı CSP iş ortakları tarafından ayarlandırabilirsiniz.                              |
| Bağlantı                 | [ResourceLinks](utility-resources.md#resourcelinks)             | Profil içinde yer alan kaynak bağlantıları.                                                                                             |
| öznitelikler            | [Resourceattributes](utility-resources.md#resourceattributes)   | Profile karşılık gelen meta veri öznitelikleri.                                                                                        |

## <a name="customercompanyprofile"></a>CustomerCompanyProfile

**CustomerCompanyProfile** kaynağı, şirket veya kuruluş hakkında ek bilgilerdir.

| Özellik    | Tür                                                           | Description                                                                       |
|-------------|----------------------------------------------------------------|-----------------------------------------------------------------------------------|
| tenantId    | string                                                         | Müşterinin Azure AD kiracı tanımlayıcısı. Buna MicrosoftID de denir. |
| etki alanı      | string                                                         | Müşterinin adı, örneğin contoso.onmicrosoft.com.                             |
| Şirketadı | string                                                         | Şirketin veya kuruluşun adı.                                          |
| Bağlantı       | [ResourceLinks](utility-resources.md#resourcelinks)           | Profil içinde yer alan kaynak bağlantıları.                                  |
| öznitelikler  | [Resourceattributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.                             |
|organizationRegistrationNumber|Dize|Müşterinin kuruluş kayıt numarası (belirli ülkelerde INN numarası olarak da adlandırılır). Müşterinin yalnızca şu ülkelerde bulunan şirketi/kuruluşu için gereklidir: Arjantin(AM), Arjantin(AZ), Sonra(BY), Yerşek(HU), GZ), Kyrgyzstan(KG), Arjantin(MD), Rusya(RU), Tajikistan(TJ), Özbekistan(UZ), Yer (UA), Hindistan, Brezilya, Güney Afrika, Afrika Birleşik Devletleri, Birleşik Devletler, Suudi Arabistan, Suudi Arabistan, Hindistan, Vietnam, Myanmar, Hindistan, Güney Sudan ve Brezilya. Müşterinin başka ülkelerde bulunan şirketi/kuruluşu için bu belirtilmedi.|


## <a name="customerbillingprofile"></a>CustomerBillingProfile

**CustomerBillingProfile** kaynağı, müşteriyi fatura etmek için kullanılan ek bilgilerdir.

| Özellik       | Tür                                                           | Description                                                                                                                                            |
|----------------|----------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik             | string                                                         | Profil tanımlayıcısı.                                                                                                                                |
| firstName      | string                                                         | Müşterinin şirketinde faturalama ilgili kişisi adı. Bu, faturaların ve diğer faturalama iletişimini yönlendirecek kişidir. |
| lastName       | string                                                         | Faturalama ilgili kişinin soyadı.                                                                                                                  |
| e-posta          | string                                                         | Faturalama ilgili kişinin e-posta adresi                                                                                                                    |
| kültür        | string                                                         | İletişim ve para birimi için tercih edilen kültür (örneğin, "en-us").                                                                               |
| language       | string                                                         | İletişim için tercih edilen dil.                                                                                                            |
| Şirketadı    | string                                                         | Şirketin veya kuruluşun adı.                                                                                                               |
| defaultAddress | [Adres](utility-resources.md#address)                       | Kambiyo senetlerinin gönderildiği, faturalama kişisinin çalıştığı adres.                                                                                   |
| Köprü          | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Profil içinde bulunan kaynak bağlantıları.                                                                                                       |
| öznitelikler     | [ResourceAttributes](utility-resources.md#resourceattributes) | Profile karşılık gelen meta veri öznitelikleri.                                                                                                  |

## <a name="customerrelationshiprequest"></a>CustomerRelationshipRequest

**Customerrelationshiprequest** kaynağı, müşteri tarafından bir iş ortağı ile bir satıcı ilişkisi kurmak için kullanılan URL 'yi içerir.

| Özellik   | Tür                                                           | Description                                                              |
|------------|----------------------------------------------------------------|--------------------------------------------------------------------------|
| url        | string                                                         | Müşteri tarafından bir iş ortağıyla ilişki kurmak için kullanılan URL. |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes) | İlişki isteğine karşılık gelen meta veri öznitelikleri.       |