---
title: Sepet kaynakları
description: Bir müşteri, teklif listesinden bir abonelik satın almak istediğinde bir iş ortağı bir siparişi bir yere koyar.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3aea428064654077ae67974132ec05918edfee65
ms.sourcegitcommit: a8fe6268fed2162843e7c92dca41c3919b25647d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/26/2020
ms.locfileid: "97769214"
---
# <a name="cart-resources"></a>Sepet kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir iş ortağı bir müşteri bir teklif listesinden abonelik satın almak istediğinde bir sipariş koyar.

## <a name="cart"></a>Sepet

Bir sepet tanımlar.

| Özellik              | Tür             | Description                                                                                            |
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

| Özellik             | Tür                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                   | string                           | Sepet çizgisi öğesi için benzersiz bir tanımlayıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                                                                   |
| Catalogıtemıd        | string                           | Katalog öğesi tanımlayıcısı.                                                                                                                          |
| friendlyName         | string                           | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                                                                 |
| miktar             | int                              | Lisans veya örnek sayısı.                                                                                                                  |
| currencyCode         | string                           | Para birimi kodu.                                                                                                                                    |
| Bilimlingcycle         | Nesne                           | Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                                                                                 |
| termDuration         | string                           | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler P1M (1 ay), P1Y (1 yıl) ve P3Y (3 yıl).                                |
| Katılımcılar         | Nesne dizesi çiftlerinin listesi      | Satınalmada iş ortağı kimliği koleksiyonu (MPNıD).                                                                                          |
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

Bir sepet oluşturulduktan sonra oluşan bir hatayı temsil eder.

| Özellik         | Tür                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| Raporladı        | [İş Ortağı Merkezi hata kodları](error-codes.md) | Sepet hatası türü.                                                                       |
| errorDescription | string                                 | Desteklenen değerler, varsayılan değerler veya limitlere ilişkin notlar da dahil olmak üzere hata açıklaması. |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Sepet kullanıma almanın sonucunu temsil eder.

| Özellik    | Tür                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| siparişler      | [Sıra](order-resources.md#order) nesnelerinin listesi.         | Siparişlerin koleksiyonu.       |
| orderErrors | [OrderError](#ordererror) nesnelerinin listesi. | Sıra hatalarının toplanması. |

## <a name="ordererror"></a>OrderError

Bir sipariş oluşturulduğunda sepet kullanıma alma sırasında oluşan bir hatayı gösterir.

| Özellik     | Tür   | Description                                     |
|--------------|--------|-------------------------------------------------|
| Ordergroupıd | string | Hatanın sipariş Grup KIMLIĞI. |
| kod         | int    | Hata kodu.                                 |
| açıklama  | string | Hatanın açıklaması.                   |
