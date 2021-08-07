---
title: Dönüştürme kaynakları
description: Deneme aboneliğini ücretli aboneliğe dönüştürmenize yardımcı olması için Iş Ortağı Merkezi API dönüştürme kaynaklarını kullanma hakkında bilgi edinin.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e7f8985fa15f4959f3cb5a729e492bbb9f3f624a5812f5b87fc119f841dc87e
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991880"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Deneme aboneliklerini ücretli olarak dönüştürmek için dönüştürme kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Dönüştürme kaynakları, bir deneme aboneliğinin ücretli aboneliğe dönüştürülmesini destekler.

## <a name="conversion"></a>Dönüştürme

Bir deneme aboneliğini ücretli aboneliğe dönüştürmek için kullanılan bilgileri içerir.

| Özellik | Tür | Description |
| -------- | ---- | ----------- |
| OfferId | string | Orijinal, deneme teklifinin teklif tanımlayıcısı. |
| targetOfferId | string | Hedef teklif için teklif tanımlayıcısı. |
| Sipariş | string | Sıra tanımlayıcısı. |
| miktar | int | Lisans sayısı. Varsayılan değer, deneme aboneliğindeki lisansların sayısıdır. |
| Bilimlingcycle | string | İş ortağının abonelik için ne sıklıkta ücretlendirileceğini gösterir. Olası değerler: **aylık** (iş ortağı aylık olarak faturalandırılır), **yıllık** (iş ortağı yıllık olarak faturalandırılır) veya **hiçbiri** (iş ortağı faturalandırılmaz). Deneme abonelikleri için kullanılır). |

## <a name="conversionerror"></a>Dönüştürme hatası

Dönüştürme sırasında oluşan bir hatayı temsil eder.

| Özellik | Tür | Description |
| -------- | ---- | ----------- |
| kod | string | Sorunla ilişkili hata kodu. Olası değerler: **diğer** (genel hata), **Conversionsnotfound** (dönüştürmeye yönelik deneme aboneliği için herhangi bir dönüştürme bulunamıyor).
| açıklama | string | Sorunu açıklayan kolay metin. |

## <a name="conversionresult"></a>ConversionResult

Abonelik dönüştürmesi gerçekleştirme sonucunu temsil eder.

| Özellik       | Tür                                | Description                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | Abonelik tanımlayıcısı.                                           |
| OfferId        | string                              | Özgün teklif tanımlayıcısı.                                         |
| targetOfferId  | string                              | Hedef teklif için teklif tanımlayıcısı.                             |
| error          | [Dönüştürme hatası](#conversionerror) | Varsa, dönüştürme denenirken hatayla karşılaşıldı. |