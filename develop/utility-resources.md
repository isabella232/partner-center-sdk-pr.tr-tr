---
title: Yardımcı program kaynakları
description: Iş Ortağı Merkezi REST API, SDK genelinde kullanılan genel amaçlı veri modellerini tanımlayan çok sayıda kaynak içerir.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: de97feed13a4d0bae9743939a03f8cb8470f5f960bec0507cd9c5adfad287120
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115998051"
---
# <a name="utility-resources"></a>Yardımcı program kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Iş Ortağı Merkezi REST API, SDK genelinde kullanılan genel amaçlı veri modellerini tanımlayan çok sayıda kaynak içerir.

## <a name="address"></a>Adres

Müşteri veya iş ortağı profilleri için kullanılacak adres. Farklı ülkelerde/bölgelerde desteklenen biçimler ve özellikler hakkında daha fazla bilgi için bkz. [pazara göre adres biçimlendirme kurallarını edinme](get-market-specific-validation-data.md).

| Özellik     | Tür   | Uzunluk (en az, en fazla) | Description                                                                                      |
|--------------|--------|-------------------|--------------------------------------------------------------------------------------------------|
| AddressLine1 | string | (1, 200)          | Adresin ilk satırı.                                                                   |
| AddressLine2 | string | (0, 200)          | Adresin ikinci satırı. Bu özellik isteğe bağlıdır.                                       |
| Şehir         | string | yok               | Şehir.                                                                                        |
| Durum        | string | (0, 2)            | Durum.                                                                                       |
| PostalCode   | string | yok               | ZIP kodu veya posta kodu.                                                                     |
| Ülke      | string | (2, 2)            | ISO ülke kodu biçimindeki ülke/bölge.                                                   |
| Region       | string | yok               | Bölge.                                                                                      |
| FirstName    | string | (1, 50)           | Müşterinin şirketindeki veya kuruluşunda bir kişinin adı.                              |
| MiddleName   | string | (1, 50)           | Müşterinin şirketinde/kuruluşunda bir kişinin ikinci adı. Bu özellik isteğe bağlıdır.  |
| LastName     | string | (1, 50)           | Müşterinin şirketinde/kuruluşunda bir kişinin soyadı.                               |
| PhoneNumber  | string | yok               | Müşterinin şirketindeki veya kuruluşunda bir kişinin telefon numarası. Bu özellik isteğe bağlıdır.|
|PhoneNumber|string|yok|Müşterinin şirketindeki veya kuruluşunda bir kişinin telefon numarası. Müşteri profilinde, bu özellik müşterinin Şirket/kuruluş için şu ülkelerde yer alan zorunludur: Ermenistan (Har), Azerbaycan (AZ), Belarus (BY), Macaristan (HU), Kazakistan (KZ), Kırgızistan (KG), Moldova (MD), Rusya (RU), Tacikistan dili (TJ), Özbekistan (UZ), Ukrayna (UA)), Hindistan, Brezilya, Güney Afrika, Polonya, Birleşik Arap Emirlikleri, Suudi Arabistan, Türkiye, Tayland, Vietnam, Myanmar, Irak, Güney Sudan ve Venezuela. Aksi takdirde bu isteğe bağlıdır.|


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
| ForceChangePassword | boolean                       | Bir sonraki oturum açma sırasında parolanın zorla değiştirilmesi gerekip gerekmediğini belirler. |

## <a name="resourcelinks"></a>Resourcelmürekkepler

Bir kaynak için bağlantıların bir listesini içerir.

| Özellik   | Tür                                      | Description                                        |
|------------|-------------------------------------------|----------------------------------------------------|
| Kendi       | [Bağlantısının](#link)                             | Self URI.                                      |
| Sonraki       | [Bağlantısının](#link)                             | Öğelerin sonraki sayfası.                            |
| Önceki   | [Bağlantısının](#link)                             | Öğelerin önceki sayfası.                        |
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

ortağın Government Community Cloud doğrulama kodunu temsil eder.

| Özellik         | Tür         | Description                                                              |
|------------------|--------------|--------------------------------------------------------------------------|
| İş ortağı kimliği        | GUID         | İş ortağı tanımlayıcısı                                                       |
| OrganizationName | string       | Doğrulama işlemi sırasında belirtilen kuruluş adı             |
| Doğrulama kimliği     | int          | Doğrulama için benzersiz bir tanımlayıcı                                       |
| Maxyaratýr       | Nullable int | Bu doğrulama koduyla oluşturulabilecek en fazla müşteri    |
| RemainingCreates | Nullable int | Kalan müşteri bu doğrulama KIMLIĞI altında oluşturulur                      |
| Özelliği             | string       | Bu kaynağın belirli sürümü. Kaynak değiştirildiğinde değişir. |
