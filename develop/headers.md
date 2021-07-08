---
title: İş Ortağı Merkezi REST üstbilgileri
description: Iş Ortağı Merkezi REST API tarafından desteklenen HTTP REST istek üstbilgileri ve REST yanıt üst bilgileri hakkında bilgi edinin.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3f09ab5808a9751f02e451da2027f6b35877390b
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548473"
---
# <a name="partner-center-rest-and-response-headers-supported-by-the-partner-center-rest-api"></a>İş Ortağı Merkezi tarafından desteklenen iş ortağı merkezi REST ve yanıt başlıkları REST API 

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Aşağıdaki HTTP isteği ve yanıt üst bilgileri, Iş Ortağı Merkezi REST API tarafından desteklenir. Tüm API çağrıları tüm üst bilgileri kabul etmez.

## <a name="rest-request-headers"></a>REST istek üstbilgileri

Aşağıdaki HTTP istek üstbilgileri, Iş Ortağı Merkezi REST API tarafından desteklenir.

| Üst bilgi                       | Açıklama                                                                                                                                                                                                                                                                            | Değer Türü |
|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Yetkilendirme:               | Gereklidir. Taşıyıcı belirtecindeki yetkilendirme belirteci &lt; &gt; .                                                                                                                                                                                                                    | string     |
| Ettiğinizde                      | "Application/JSON" istek ve yanıt türünü belirtir.                                                                                                                                                                                                                           | string     |
| MS-RequestId:                | Kimlik-kuvvet sağlamak için kullanılan, çağrı için benzersiz bir tanımlayıcı. Bir zaman aşımı varsa, yeniden deneme çağrısı aynı değeri içermelidir. Yanıt aldıktan sonra (başarı veya iş hatası), sonraki çağrının değeri sıfırlanmalıdır.                                            | GUID       |
| MS-Bağıntıkimliği:            | Arama için benzersiz bir tanımlayıcı, günlüklerde ve ağ izlemelerinde yararlı olarak sorun giderme hataları. Değer her çağrı için sıfırlanmalıdır. Tüm işlemler bu üstbilgiyi içermelidir. Daha fazla bilgi için [test ve hata ayıklama](test-and-debug.md)IÇINDEKI bağıntı kimliği bilgilerine bakın. | GUID       |
| MS-Contract-Version:         | Gereklidir. İstenen API sürümünü belirtir; genellikle [senaryolar](scenarios.md) bölümünde belirtilmediği takdirde API-sürümü: v1.                                                                                                                                  | string     |
| IF-Match:                    | Eşzamanlılık denetimi için kullanılır. Bazı API çağrıları, If-Match üst bilgisi aracılığıyla ETag 'in geçirilmesini gerektirir. ETag genellikle kaynak üzerinde bulunur ve bu nedenle, en son için almayı gerektirir. Daha fazla bilgi için [test ve hata ayıklama](test-and-debug.md)içindeki ETag bilgilerine bakın.                | string     |
| MS-PartnerCenter-uygulama | İsteğe bağlı. Iş Ortağı Merkezi REST API kullanan uygulamanın adını belirtir.                                                                                                                                                                                             | string     |
| X-yerel ayar:                    | İsteğe bağlı. Hızların döndürüleceği dili belirtir. Varsayılan değer "en-US" dir. Desteklenen değerlerin listesi için bkz. [Partner Center tarafından desteklenen diller ve yerel ayarlar](partner-center-supported-languages-and-locales.md).                                                                                                                                                                                                  | string     |

## <a name="rest-response-headers"></a>REST yanıt üst bilgileri

Aşağıdaki HTTP yanıt üst bilgileri, Iş Ortağı Merkezi REST API döndürebilir.

| Üst bilgi            | Açıklama                                                                                                                                                                                                                                 | Değer Türü |
|-------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------|
| Ettiğinizde           | "Application/JSON" istek ve yanıt türünü belirtir.                                                                                                                                                                                | string     |
| MS-RequestId:     | Kimlik-kuvvet sağlamak için kullanılan, çağrı için benzersiz bir tanımlayıcı. Bir zaman aşımı varsa, yeniden deneme çağrısı aynı değeri içermelidir. Yanıt aldıktan sonra (başarı veya iş hatası), sonraki çağrının değeri sıfırlanmalıdır. | GUID       |
| MS-Bağıntıkimliği: | Çağrı için benzersiz bir tanımlayıcı. Bu değer, hatayı bulmak için günlükleri ve ağ izlemelerinin sorunlarını gidermeye yarar. Değer her çağrı için sıfırlanmalıdır. Tüm işlemler bu üstbilgiyi içermelidir.                                                       | GUID       |
