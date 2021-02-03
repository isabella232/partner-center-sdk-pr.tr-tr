---
title: Ülke bilgileri kaynakları
description: Ülke bilgi kaynaklarıyla Iş Ortağı Merkezi API 'Lerini ve belirli bir ülke veya bölgeyle ilgili açıklayıcı meta verileri kullanma hakkında bilgi edinin.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0974cf736ff86038f8abf9c77d6a648984d1df
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770141"
---
# <a name="country-information-resources-available-from-partner-center-apis"></a>Iş Ortağı Merkezi API 'Lerinde ülke bilgisi kaynakları mevcuttur

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Aşağıdaki kaynaklar bir ülke/bölge için açıklayıcı meta verileridir.

## <a name="countryinformation"></a>Countryınformation

| Özellik                      | Tür               | Description                                                                                        |
|-------------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| ExtensionData                 | string             | Uzantı verileri.                                                                                |
| Iso2Code                      | string             | ISO-2 kodu.                                                                                     |
| Iso3Code                      | string             | ISO-3 kodu.                                                                                     |
| DefaultCulture                | string             | Varsayılan kültür.                                                                               |
| IsStateRequired               | boolean            | Bir eyalet/eyalet gerekip gerekmediğini belirtir.                                             |
| SupportedStatesList           | dize dizisi   | Bir eyalet/bölge gerekliyse, bu ülkenin/bölgenin tam listesini döndürür.                    |
| SupportedLanguagesList        | dize dizisi   | Desteklenen dillerin listesi.                                                                     |
| Supportedkültureslist         | dize dizisi   | Desteklenen kültürlerin listesi.                                                                      |
| IsPostalCodeRequired          | boolean            | Bir posta kodu veya posta kodunun gerekli olup olmadığını belirtir.                                    |
| PostalCodeRegex               | string             | ZIP/posta kodunu tanımlayan normal ifade.                                          |
| SCC gerekli                | boolean            | Bir şehrin gerekli olup olmadığını belirtir.                                                       |
| IsVatIdSupported              | boolean            | KDV KIMLIĞININ gerekli olup olmadığını belirtir.                                                     |
| Taxıdformat                   | string             | Vergi KIMLIĞI biçimi.                                                                                 |
| Taxıdsample                   | string             | Vergi KIMLIĞI örneği.                                                                                 |
| VatIdRegex                    | string             | Vergi KIMLIĞI normal ifadesi.                                                                     |
| PhoneNumberRegex              | string             | Telefon numarası normal ifadesi.                                                               |
| Isregistrationnumberdestekleniyor | boolean            | Bir kayıt numarasının desteklenip desteklenmediğini belirtir.                                       |
| Istaxıdsupported              | boolean            | Vergi KIMLIĞININ desteklenip desteklenmediğini belirtir. Bu, IsVatIdSupported 'den farklıdır. |
| ResellerAgreementRegion       | string             | Satıcı sözleşmesi bölgesi.                                                                     |
| GeographicRegion              | string             | Coğrafi bölge.                                                                             |
| CountryCallingCodesList       | dize dizisi   | Ülkede/bölgede desteklenen çağırma kodları.                                                 |
| Öznitelikler                    | ResourceAttributes | Countryınformation kaynağına karşılık gelen meta veri öznitelikleri.                          |

## <a name="countryvalidationrules"></a>CountryValidationRules

Ülke/bölge için adres biçimlendirme kurallarını açıklar.

| Özellik                | Tür               | Description                                                                                        |
|-------------------------|--------------------|----------------------------------------------------------------------------------------------------|
| Iso2Code                | string             | ISO-2 kodu.                                                                                     |
| DefaultCulture          | string             | Varsayılan kültür.                                                                               |
| IsStateRequired         | boolean            | Bir eyalet/eyalet gerekip gerekmediğini belirtir.                                             |
| SupportedStatesList     | dize dizisi   | Bir eyalet/bölge gerekliyse, bu ülkenin/bölgenin tam listesini döndürür.                    |
| SupportedLanguagesList  | dize dizisi   | Desteklenen dillerin listesi.                                                                     |
| Supportedkültureslist   | dize dizisi   | Desteklenen kültürlerin listesi.                                                                      |
| IsPostalCodeRequired    | boolean            | Bir posta kodu veya posta kodunun gerekli olup olmadığını belirtir.                                    |
| PostalCodeRegex         | string             | ZIP/posta kodunu tanımlayan normal ifade.                                          |
| SCC gerekli          | boolean            | Bir şehrin gerekli olup olmadığını belirtir.                                                       |
| IsVatIdSupported        | boolean            | KDV KIMLIĞININ gerekli olup olmadığını belirtir.                                                     |
| Taxıdformat             | string             | Vergi KIMLIĞI biçimi.                                                                                 |
| Taxıdsample             | string             | Vergi KIMLIĞI örneği.                                                                                 |
| VatIdRegex              | string             | Vergi KIMLIĞI normal ifadesi.                                                                     |
| PhoneNumberRegex        | string             | Telefon numarası normal ifadesi.                                                               |
| Istaxıdsupported        | boolean            | Vergi KIMLIĞININ desteklenip desteklenmediğini belirtir. Bu özellik IsVatIdSupported 'den farklıdır. |
| IsTaxIdOptional         | boolean            | Vergi KIMLIĞININ isteğe bağlı olup olmadığını gösterir.                                                     |
| CountryCallingCodesList | dize dizisi   | Ülkede/bölgede desteklenen çağırma kodları.                                                 |
| Öznitelikler              | ResourceAttributes | Countryınformation kaynağına karşılık gelen meta veri öznitelikleri.                          |
