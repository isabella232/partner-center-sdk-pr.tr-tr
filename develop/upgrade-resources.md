---
title: Kaynakları yükselt
description: Bir kullanıcıyı kaynak aboneliğinden hedef aboneliğe yükseltmek için kullanılan kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bdbef383370761a01eb462f90284ad826a38ddaa
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768992"
---
# <a name="upgrade-resources"></a>Kaynakları yükselt

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir kullanıcıyı kaynak aboneliğinden hedef aboneliğe yükseltmek için kullanılan kaynakları açıklar.

## <a name="upgrade"></a>Yükseltme

Tek bir yükseltme kaynağının davranışını açıklar.

| Özellik      | Tür                   | Description                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Sunduğu                  | Hedef aboneliğin teklifi.                                                        |
| UpgradeType   | string                 | Yükseltme türü: "none", " \_ yalnızca Upgrade" veya " \_ \_ Lisans \_ aktarımıyla yükselt".         |
| IBir hal    | boolean                | Yükseltmenin gerçekleştirilip gerçekleştirilmeyeceğini belirler.                                                  |
| Miktar      | tamsayı                | Satın alınması için yeni teklifin miktarı. Varsayılan kaynak abonelik miktarı olur. |
| Yükseltme hataları | UpgradeErrors dizisi | Varsa yükseltmenin gerçekleştirilemediği nedenler.                                      |
| Öznitelikler    | ResourceAttributes     | Yükseltmeye karşılık gelen meta veri öznitelikleri.                                        |

## <a name="upgradeerror"></a>Yükseltme hatası

Yükseltmenin neden gerçekleştirilmediğini açıklar.

| Özellik          | Tür               | Description                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | string             | Sorunla ilişkili hata kodu: "diğer", " \_ yönetici \_ izinleri \_ devre dışı bırakıldı", "abonelik \_ durumu \_ etkin değil", " \_ Çakışan hizmet türleri", " \_ \_ eş zamanlı \_ Çakışmalar", "Kullanıcı \_ bağlamı gereklidir", "abonelik \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ hedef \_ teklifi bulunamadı" \_ \_ veya "abonelik \_ \_ sağlanmadı". |
| Description       | dize             | Hatayı açıklayan kolay metin.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | Hatayla ilgili ek ayrıntılar.                                                                                                                                                                                                                                                                                                                                                         |
| Öznitelikler        | ResourceAttributes | Hataya karşılık gelen meta veri öznitelikleri.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>Yükseltme Deresult

Abonelik yükseltme işleminin sonucunu açıklar.

| Özellik             | Tür                        | Description                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| Sourcesubscriptionıd | string                      | Kaynak aboneliğin tanımlayıcısı.                                           |
| Targetsubscriptionıd | string                      | Hedef aboneliğin tanımlayıcısı.                                           |
| UpgradeType          | string                      | Yükseltme türü: "none", " \_ yalnızca Upgrade" veya " \_ \_ Lisans \_ aktarımıyla yükselt". |
| Yükseltme hataları        | UpgradeErrors dizisi      | Attemption, varsa yükseltme işlemini gerçekleştirmeye çalışırken hatalarla karşılaşıldı.           |
| LicenseErrors        | UserLicenseErrrors dizisi | Varsa, kullanıcı lisanslarını geçirmeye çalışırken hatalarla karşılaşıldı.          |
| Öznitelikler           | ResourceAttributes          | Lisansa karşılık gelen meta veri öznitelikleri.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Başarısız Kullanıcı Lisans aktarımından kaynaklanan hataları açıklar.

| Özellik     | Tür                   | Description                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| Userobjectıd | string                 | Kullanıcı nesnesinin benzersiz tanımlanması.                                 |
| Name         | string                 | Kullanıcının adı.                                                     |
| E-posta        | string                 | Kullanıcının e-postası.                                                    |
| Hatalar       | ServiceFaults dizisi | Kullanıcı Lisans aktarımı gerçekleştirmeye çalışırken oluşturulan özel durumların listesi. |
| Öznitelikler   | ResourceAttributes     | Lisansa karşılık gelen meta veri öznitelikleri.                     |

