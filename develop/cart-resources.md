---
title: Sepet kaynakları
description: Bir müşteri, teklif listesinden bir abonelik satın almak istediğinde bir iş ortağı bir siparişi bir yere koyar.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 08085dde1b43f20b6f6bf707120dd87c48816aba
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974157"
---
# <a name="cart-resources"></a>Sepet kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bir iş ortağı bir müşteri bir teklif listesinden abonelik satın almak istediğinde bir sipariş koyar.

## <a name="cart"></a>Sepet

Bir sepet tanımlar.

| Özellik              | Tür             | Açıklama                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | Sepet başarıyla oluşturulduktan sonra sağlanan bir sepet tanımlayıcısı.                               |
| creationTimeStamp     | DateTime         | Sepetin oluşturulduğu tarih ve saat biçimi. Sepet başarıyla oluşturulduktan sonra uygulandı.      |
| lastModifiedTimeStamp | DateTime         | Sepetin son güncelleştirildiği tarih ve saat biçimi. Sepet başarıyla oluşturulduktan sonra uygulandı. |
| expirationTimeStamp   | DateTime         | Sepetin süresinin dolacağı tarih-saat biçiminde. Sepet başarıyla oluşturulduktan sonra uygulandı.          |
| lastModifiedUser      | string           | Sepetini son güncelleştiren Kullanıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                          |
| LineItems             | Nesne dizisi | Bir [Cartlineıtem](#cartlineitem) kaynakları dizisi.                                                   |
| durum                | string           | Sepetin durumu. Olası değerler şunlardır. "etkin" (güncelleştirilemeyebilir/gönderilebilir) ve "siparişli" (daha önce gönderildi). |

## <a name="cartlineitem"></a>Cartlineıtem

Sepette bulunan bir öğeyi temsil eder.

| Özellik             | Tür                             | Açıklama                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                   | string                           | Sepet çizgisi öğesi için benzersiz bir tanımlayıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                                                                   |
| Catalogıtemıd        | string                           | Katalog öğesi tanımlayıcısı.                                                                                                                          |
| friendlyName         | string                           | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                                                                 |
| miktar             | int                              | Lisans veya örnek sayısı.                                                                                                                  |
| currencyCode         | string                           | Para birimi kodu.                                                                                                                                    |
| Bilimlingcycle         | Nesne                           | Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                                                                                 |
| termDuration         | string                           | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler P1M (1 ay), P1Y (1 yıl) ve P3Y (3 yıl).                                |
| Katılımcılar         | Nesne dizesi çiftlerinin listesi      | Satın alımdaki kayıttaki iş ortağı kimliği koleksiyonu (MPN KIMLIĞI).                                                                                          |
| provisioningContext  | Sözlük<dize, dize>       | Satın alınan öğe sağlanırken kullanılan ek bağlam. Belirli bir öğe için hangi değerlerin gerekli olduğunu öğrenmek için SKU 'nun provisioningVariables özelliğine bakın. |
| orderGroup           | string                           | Aynı sırada hangi öğelerin birlikte gönderilebileceğine işaret eden bir grup.                                                                          |
| Addonıtems           | **Cartlineıtem** nesnelerinin listesi | Eklentiler için sepet çizgisi öğeleri koleksiyonu. Bu öğeler, kök sepet çizgisi öğesinin satın alma işleminden kaynaklanan temel aboneliğe göre satın alınacaktır. |
| error                | Nesne                           | Bir hata oluştuysa sepet oluşturulduktan sonra uygulanır.                                                                                                    |
| renewsTo             | Nesne dizisi                 | [RenewsTo](#renewsto) kaynaklarından oluşan bir dizi.                                                                            |

## <a name="renewsto"></a>RenewsTo

Sepet çizgisi öğesinde bulunan bir öğeyi temsil eder.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | dize           | No              | Yenileme teriminin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl). |

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

## <a name="carterror"></a>CartError

Sepet oluşturulduktan sonra oluşan bir hatayı temsil eder.

| Özellik         | Tür                                   | Açıklama                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [İş Ortağı Merkezi hata kodları](error-codes.md) | Sepet hatasının türü.                                                                       |
| Errordescription | string                                 | Desteklenen değerler, varsayılan değerler veya sınırlar hakkında notlar da dahil olmak üzere hata açıklaması. |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Sepet iadenin sonucu temsil eder.

| Özellik    | Tür                                              | Açıklama                     |
|-------------|---------------------------------------------------|---------------------------------|
| siparişler      | Order [nesnelerinin](order-resources.md#order) listesi.         | Sipariş koleksiyonu.       |
| orderErrors | [OrderError nesnelerinin](#ordererror) listesi. | Sipariş hatalarının koleksiyonu. |

## <a name="ordererror"></a>OrderError

Sipariş oluşturulduğunda sepetin iade oluşturulduğunda oluşan bir hatayı temsil eder.

| Özellik     | Tür   | Açıklama                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | string | Hatayla birlikte siparişin sipariş grubu kimliği. |
| kod         | int    | Hata kodu.                                 |
| açıklama  | string | Hatanın açıklaması.                   |
