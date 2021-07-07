---
title: Ülke bilgi kaynakları
description: Ülke bilgi kaynaklarıyla İş Ortağı Merkezi ve belirli bir ülke veya bölgeyle ilgili açıklayıcı meta verilerle api'leri kullanma hakkında bilgi edinebilirsiniz.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: caf56282d21df35ae9e179a98a37317f864117a3
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973834"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>İş Ortağı Merkezi API'İş Ortağı Merkezi kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Aşağıdaki kaynaklar bir ülke/bölge için açıklayıcı meta verilerdir.

## <a name="countryinformation"></a>CountryInformation

| Özellik                      | Tür               | Açıklama                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | string             | Uzantı verileri.                                                                                |
| Iso2Code                      | string             | ISO-2 kodu.                                                                                     |
| Iso3Code                      | string             | ISO-3 kodu.                                                                                     |
| DefaultCulture                | string             | Varsayılan kültür.                                                                               |
| IsStateRequired               | boolean            | Bir eyaletin/ilin gerekli olup olmadığını gösterir.                                             |
| SupportedStatesList           | dize dizisi   | Bir eyalet/il gerekli ise, bu ülke/bölge için tam listeyi döndürür.                    |
| SupportedLanguagesList        | dize dizisi   | Desteklenen dillerin listesi.                                                                     |
| SupportedCulturesList         | dize dizisi   | Desteklenen kültürlerin listesi.                                                                      |
| IsPostalCodeRequired          | boolean            | Posta kodunun gerekli olup olmadığını gösterir.                                    |
| PostalCodeRegex               | string             | Posta kodunu tanımlayan normal ifade.                                          |
| IsCityRequired                | boolean            | Bir şehrin gerekli olup olmadığını gösterir.                                                       |
| IsVatIdSupported              | boolean            | KDV No'ların gerekli olup olmadığını gösterir.                                                     |
| TaxIdFormat                   | string             | Vergi numarası biçimi.                                                                                 |
| TaxIdSample                   | string             | Vergi numarası örneği.                                                                                 |
| KdvIdRegex                    | string             | Vergi numarası normal ifadesi.                                                                     |
| PhoneNumberRegex              | string             | Telefon numarası normal ifadesi.                                                               |
| IsRegistrationNumberSupported | boolean            | Bir kayıt numarasının destek alınıp alın olmadığını gösterir.                                       |
| IsTaxIdSupported              | boolean            | Bir vergi kimliğinin destek isteyip olmadığını gösterir. Bu IsVatIdSupported'den farklıdır. |
| ResellerAgreementRegion       | string             | Kurumsal bayi sözleşmesi bölgesi.                                                                     |
| GeographicRegion              | string             | Coğrafi bölge.                                                                             |
| CountryCallingCodesList       | dize dizisi   | Ülke/bölgede desteklenen arama kodları.                                                 |
| Öznitelikler                    | Resourceattributes | CountryInformation kaynağına karşılık gelen meta veri öznitelikleri.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Bir ülke/bölge için adres biçimlendirme kurallarını açıklar.

| Özellik                | Tür               | Açıklama                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | string             | ISO-2 kodu.                                                                                     |
| DefaultCulture          | string             | Varsayılan kültür.                                                                               |
| IsStateRequired         | boolean            | Bir eyaletin/ilin gerekli olup olmadığını gösterir.                                             |
| SupportedStatesList     | dize dizisi   | Bir eyalet/il gerekli ise, bu ülke/bölge için tam listeyi döndürür.                    |
| SupportedLanguagesList  | dize dizisi   | Desteklenen dillerin listesi.                                                                     |
| SupportedCulturesList   | dize dizisi   | Desteklenen kültürlerin listesi.                                                                      |
| IsPostalCodeRequired    | boolean            | Posta kodunun gerekli olup olmadığını gösterir.                                    |
| PostalCodeRegex         | string             | Posta kodunu tanımlayan normal ifade.                                          |
| IsCityRequired          | boolean            | Bir şehrin gerekli olup olmadığını gösterir.                                                       |
| IsVatIdSupported        | boolean            | KDV No'ların gerekli olup olmadığını gösterir.                                                     |
| TaxIdFormat             | string             | Vergi numarası biçimi.                                                                                 |
| TaxIdSample             | string             | Vergi numarası örneği.                                                                                 |
| KdvIdRegex              | string             | Vergi numarası normal ifadesi.                                                                     |
| PhoneNumberRegex        | string             | Telefon numarası normal ifadesi.                                                               |
| IsTaxIdSupported        | boolean            | Bir vergi kimliğinin destek isteyip olmadığını gösterir. Bu özellik IsVatIdSupported özelliğinden farklıdır. |
| IsTaxIdOptional         | boolean            | Vergi kimliğinin isteğe bağlı olup olmadığını gösterir.                                                     |
| CountryCallingCodesList | dize dizisi   | Ülke/bölgede desteklenen arama kodları.                                                 |
| Öznitelikler              | Resourceattributes | CountryInformation kaynağına karşılık gelen meta veri öznitelikleri.                          |
