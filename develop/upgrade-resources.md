---
title: Kaynakları yükseltme
description: Bir kullanıcıyı kaynak abonelikten hedef aboneliğe yükseltmek için kullanılan kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c57994d1b1e7659df5e6448578422f6d9c21fee
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529826"
---
# <a name="upgrade-resources"></a>Kaynakları yükseltme

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bir kullanıcıyı kaynak abonelikten hedef aboneliğe yükseltmek için kullanılan kaynakları açıklar.

## <a name="upgrade"></a>Yükseltme

Tek bir yükseltme kaynağının davranışını açıklar.

| Özellik      | Tür                   | Açıklama                                                                                  |
|---------------|------------------------|----------------------------------------------------------------------------------------------|
| TargetOffer   | Sunduğu                  | Hedef aboneliğin teklifi.                                                        |
| UpgradeType   | string                 | Yükseltme türü: "none", \_ "only upgrade" veya "upgrade \_ with license \_ \_ transfer".         |
| Önemsiz    | boolean                | Yükseltmenin gerçekleştirilenin olup ola olduğunu tanımlar.                                                  |
| Miktar      | tamsayı                | Satın alınacak yeni teklifin miktarı. Varsayılan olarak kaynak abonelik miktarı kullanılır. |
| UpgradeErrors | UpgradeErrors dizisi | Uygunsa, yükseltmenin gerçekleştirilemama nedenleri.                                      |
| Öznitelikler    | Resourceattributes     | Yükseltmeye karşılık gelen meta veri öznitelikleri.                                        |

## <a name="upgradeerror"></a>UpgradeError

Yükseltmenin gerçekleştirilema nedenini açıklar.

| Özellik          | Tür               | Açıklama                                                                                                                                                                                                                                                                                                                                                                                     |
|-------------------|--------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Kod              | string             | Sorunla ilişkili hata kodu: "other", "delegated \_ admin \_ permissions \_ disabled", "subscription status not \_ \_ \_ active", "conflicting service \_ \_ types", "concurrency \_ conflicts", "user \_ context required", "subscription add ons present", "subscription does not any upgrade \_ \_ \_ \_ \_ \_ \_ \_ \_ \_ paths", "subscription \_ target offer not \_ \_ found" veya "subscription not \_ \_ \_ provisioned". |
| Description       | dize             | Hatayı açıklayan kolay metin.                                                                                                                                                                                                                                                                                                                                                             |
| AdditionalDetails | string             | Hatayla ilgili ek ayrıntılar.                                                                                                                                                                                                                                                                                                                                                         |
| Öznitelikler        | Resourceattributes | Hataya karşılık gelen meta veri öznitelikleri.                                                                                                                                                                                                                                                                                                                                             |

## <a name="upgraderesult"></a>Upgraderesult

Abonelik yükseltme işleminin sonucu açıkmektedir.

| Özellik             | Tür                        | Açıklama                                                                          |
|----------------------|-----------------------------|--------------------------------------------------------------------------------------|
| SourceSubscriptionId | string                      | Kaynak aboneliğin tanımlayıcısı.                                           |
| TargetSubscriptionID | string                      | Hedef aboneliğin tanımlayıcısı.                                           |
| UpgradeType          | string                      | Yükseltme türü: "none", \_ "only upgrade" veya "upgrade \_ with license \_ \_ transfer". |
| UpgradeErrors        | UpgradeErrors dizisi      | Varsa, yükseltme gerçekleştirmeye çalışırken karşılaşılan hatalar.           |
| LicenseErrors        | UserLicenseErrrors dizisi | Varsa, kullanıcı lisanslarını geçirme girişiminde karşılaşılan hatalar.          |
| Öznitelikler           | Resourceattributes          | Lisansa karşılık gelen meta veri öznitelikleri.                                |

## <a name="userlicenseerror"></a>UserLicenseError

Başarısız kullanıcı lisans aktarımından kaynaklanan hataları açıklar.

| Özellik     | Tür                   | Açıklama                                                               |
|--------------|------------------------|---------------------------------------------------------------------------|
| UserObjectId | string                 | Kullanıcı nesnesinin tanımlanan benzersizi.                                 |
| Name         | string                 | Kullanıcının adı.                                                     |
| E-posta        | string                 | Kullanıcının e-postası.                                                    |
| Hatalar       | ServiceFaults dizisi | Kullanıcı lisans aktarımı gerçekleştirmeye çalışılan özel durumların listesi. |
| Öznitelikler   | Resourceattributes     | Lisansa karşılık gelen meta veri öznitelikleri.                     |

