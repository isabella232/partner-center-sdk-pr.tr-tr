---
title: Dönüştürme kaynakları
description: Deneme aboneliğini ücretli aboneliğe dönüştürmenize yardımcı olması için Iş Ortağı Merkezi API dönüştürme kaynaklarını kullanma hakkında bilgi edinin.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1863c365627807d8de2534a2d3116807a5de70e1
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973902"
---
# <a name="conversion-resources-to-convert-trial-subscriptions-to-paid"></a>Deneme aboneliklerini ücretli olarak dönüştürmek için dönüştürme kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Dönüştürme kaynakları, bir deneme aboneliğinin ücretli aboneliğe dönüştürülmesini destekler.

## <a name="conversion"></a>Dönüştürme

Bir deneme aboneliğini ücretli aboneliğe dönüştürmek için kullanılan bilgileri içerir.

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| OfferId | string | Orijinal, deneme teklifinin teklif tanımlayıcısı. |
| targetOfferId | string | Hedef teklif için teklif tanımlayıcısı. |
| Sipariş | string | Sıra tanımlayıcısı. |
| miktar | int | Lisans sayısı. Varsayılan değer, deneme aboneliğindeki lisansların sayısıdır. |
| Bilimlingcycle | string | İş ortağının abonelik için ne sıklıkta ücretlendirileceğini gösterir. Olası değerler: **aylık** (iş ortağı aylık olarak faturalandırılır), **yıllık** (iş ortağı yıllık olarak faturalandırılır) veya **hiçbiri** (iş ortağı faturalandırılmaz). Deneme abonelikleri için kullanılır). |

## <a name="conversionerror"></a>Dönüştürme hatası

Dönüştürme sırasında oluşan bir hatayı temsil eder.

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| kod | string | Sorunla ilişkili hata kodu. Olası değerler: **diğer** (genel hata), **Conversionsnotfound** (dönüştürmeye yönelik deneme aboneliği için herhangi bir dönüştürme bulunamıyor).
| açıklama | string | Sorunu açıklayan kolay metin. |

## <a name="conversionresult"></a>ConversionResult

Abonelik dönüştürmesi gerçekleştirme sonucunu temsil eder.

| Özellik       | Tür                                | Açıklama                                                            |
|----------------|-------------------------------------|------------------------------------------------------------------------|
| subscriptionId | string                              | Abonelik tanımlayıcısı.                                           |
| OfferId        | string                              | Özgün teklif tanımlayıcısı.                                         |
| targetOfferId  | string                              | Hedef teklif için teklif tanımlayıcısı.                             |
| error          | [Dönüştürme hatası](#conversionerror) | Varsa, dönüştürme denenirken hatayla karşılaşıldı. |