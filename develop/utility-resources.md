---
title: Yardımcı program kaynakları
description: Iş Ortağı Merkezi REST API, SDK genelinde kullanılan genel amaçlı veri modellerini açıklayan birçok kaynak içerir.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 53d39e4f76684128d48eacdce75706d853c7ce74
ms.sourcegitcommit: f5178dca1d9a51059738972810235d8858e6a67a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/18/2020
ms.locfileid: "97770060"
---
# <a name="utility-resources"></a>Yardımcı program kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Iş Ortağı Merkezi REST API, SDK genelinde kullanılan genel amaçlı veri modellerini açıklayan birçok kaynak içerir.

## <a name="address"></a>Adres

Müşteri veya iş ortağı profilleri için kullanılacak adres. Farklı ülkelerde/bölgelerde desteklenen biçimler ve özellikler hakkında daha fazla bilgi için bkz. [pazara göre adres biçimlendirme kurallarını edinme](get-market-specific-validation-data.md).

| Özellik     | Tür   | Uzunluk (en az, en fazla) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | (1, 200)          | Adresin ilk satırı.                                                                   |
| AddressLine2 | string | (0, 200)          | Adresin ikinci satırı. Bu özellik isteğe bağlıdır.                                       |
| City         | string | yok               | Şehir.                                                                                        |
| Durum        | string | (0, 2)            | Durum.                                                                                       |
| PostalCode   | string | yok               | ZIP kodu veya posta kodu.                                                                     |
| Ülke      | string | (2, 2)            | ISO ülke kodu biçimindeki ülke/bölge.                                                   |
| Bölge       | string | yok               | Bölge.                                                                                      |
| FirstName    | string | (1, 50)           | Müşterinin şirketindeki veya kuruluşunda bir kişinin adı.                              |
| MiddleName   | string | (1, 50)           | Müşterinin şirketinde/kuruluşunda bir kişinin ikinci adı. Bu özellik isteğe bağlıdır.  |
| LastName     | string | (1, 50)           | Müşterinin şirketinde/kuruluşunda bir kişinin soyadı.                               |
| PhoneNumber  | string | yok               | Müşterinin şirketindeki veya kuruluşunda bir kişinin telefon numarası. Bu özellik isteğe bağlıdır.|
|PhoneNumber|string|yok|Müşterinin şirketindeki veya kuruluşunda bir kişinin telefon numarası. Müşteri profilinde, bu özellik müşterinin Şirket/kuruluş için aşağıdaki ülkelerde yer alan zorunludur. Ermenistan (Har), Azerbaycan (AZ), Belarus (BY), Macaristan (HU), Kazakistan (KZ), Kırgızistan (KG), Moldova (MD), Rusya (RU), Tacikistan (TJ), Özbekistan (UZ), Ukrayna (UA). Aksi takdirde bu isteğe bağlıdır.|


## <a name="contact"></a>İletişim

Belirli bir kişiye ait iletişim bilgilerini açıklar.

| Özellik    | Tür   | Description                  |
|-------------|--------|------------------------------|
| FirstName   | string | Kişinin adı.    |
| LastName    | string | Kişinin soyadı.     |
| E-posta       | string | Kişinin e-posta adresi. |
| PhoneNumber | string | Kişinin telefon numarası.  |

## <a name="fieldfilter"></a>FieldFilter

Arama sonuçlarına uygulanabilen bir filtre tanımlar.

| Özellik | Tür   | Description                                                                                                                                                                                        |
|----------|--------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Operatör | string | Filtre işleci: "eşittir", "eşit değildir \_ ", "büyüktür", "büyüktür veya eşittir", " \_ \_ küçüktür", " \_ küçüktür veya eşittir", " \_ \_ \_ \_ \_ substring", "ve", "veya", "ile başlar", "ile başlar \_ \_ \_ ". |

## <a name="fileinfo"></a>Bilgis

Iş Ortağı Merkezi 'ne yüklenen bir dış dosyayı temsil eder.

| Özellik                 | Tür   | Description                                   |
|--------------------------|--------|-----------------------------------------------|
| Yorum                  | string | Karşıya dosya yükleme ile ilişkili bir açıklama.    |
| FileExtension            | string | Dosya uzantısı.                           |
| FileNameWithoutExtension | string | Dosyanın adı, uzantı dahil değildir. |
| İ                 | long   | Dosya boyutu.                         |
| Id                       | string | Karşıya dosya yükleme için benzersiz KIMLIK.            |

## <a name="link"></a>Bağlantı

Bir URI bağlantısı ve ilgili bilgileri içerir.

| Özellik | Tür                   | Description                        |
|----------|------------------------|------------------------------------|
| URI      | string                 | URI.                           |
| Yöntem   | string                 | URI tarafından temsil edilen yöntem. |
| Üst Bilgiler  | KeyValuePairs dizisi | Bağlantının üst bilgileri.          |

## <a name="passwordprofile"></a>PasswordProfile

Belirli bir parolayı ve bu parolanın değiştirilmesinin gerekip gerekmediğini açıklar.

>[!NOTE]
>21Vianet tarafından çalıştırılan Iş Ortağı Merkezi 'nde desteklenmez.

| Özellik            | Tür                          | Description                                                            |
|---------------------|-------------------------------|------------------------------------------------------------------------|
| Parola            | [SecureString](#securestring) | Parola.                                                          |
| ForceChangePassword | boolean                       | Parolanın bir sonraki oturum açmada zorla değiştirilmesi gerekip gerekmediğini belirler. |

## <a name="resourcelinks"></a>Resourcelmürekkepler

Bir kaynak için bağlantıların bir listesini içerir.

| Özellik   | Tür                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Kendi       | [Bağlantı](#link)                             | Self URI.                                      |
| Sonraki       | [Bağlantı](#link)                             | Öğelerin sonraki sayfası.                            |
| Önceki   | [Bağlantı](#link)                             | Öğelerin önceki sayfası.                        |
| Öznitelikler | [ResourceAttributes](#resourceattributes) | Kullanıcıya karşılık gelen meta veri öznitelikleri. |

## <a name="resourceattributes"></a>ResourceAttributes

Bir kaynağın öznitelik meta verilerini içerir.

| Özellik   | Tür   | Description                                 |
|------------|--------|---------------------------------------------|
| Özelliği       | string | Nesne sürümü olarak da bilinen ETag. |
| ObjectType | string | Temel kaynağın nesne türü.    |

## <a name="securestring"></a>SecureString

Parola gibi güvenli bilgileri depolar.

| Özellik | Tür | Description                       |
|----------|------|-----------------------------------|
| Uzunluk   | int  | Güvenli dizenin uzunluğu. |

## <a name="validationcode"></a>ValidationCode

Ortağın kamu Community bulut doğrulama kodunu temsil eder.

| Özellik         | Tür         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| İş ortağı kimliği        | GUID         | İş ortağı tanımlayıcısı                                                       |
| OrganizationName | string       | Doğrulama işlemi sırasında belirtilen kuruluş adı             |
| Doğrulama kimliği     | int          | Doğrulama için benzersiz bir tanımlayıcı                                       |
| Maxyaratýr       | Nullable int | Bu doğrulama koduyla oluşturulabilecek en fazla müşteri    |
| RemainingCreates | Nullable int | Kalan müşteri bu doğrulama KIMLIĞI altında oluşturulur                      |
| Özelliği             | string       | Bu kaynağın belirli sürümü. Kaynak değiştirildiğinde değişir. |
