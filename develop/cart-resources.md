---
title: Sepet kaynakları
description: Müşteri teklif listesinden abonelik satın almak istediği zaman iş ortağı sepete sipariş verdi.
ms.date: 08/26/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c9372bb982528127f8870094e26465d004b1f05c75140f0ac729375f5d5f3302
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992186"
---
# <a name="cart-resources"></a>Sepet kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Müşteri teklif listesinden abonelik satın almak istediği zaman iş ortağı sipariş verdi.

## <a name="cart"></a>Sepet

Bir sepeti açıklar.

| Özellik              | Tür             | Description                                                                                            |
|-----------------------|------------------|--------------------------------------------------------------------------------------------------------|
| kimlik                    | string           | Sepetin başarıyla oluşturulmasının ardından sağlanan bir sepet tanımlayıcısı.                               |
| creationTimeStamp     | DateTime         | Sepetin tarih-saat biçiminde oluşturulma tarihi. Sepetin başarıyla oluşturulmasının ardından uygulanır.      |
| lastModifiedTimeStamp | DateTime         | Sepetin en son güncelleştirilen tarih-saat biçiminde olduğu tarih. Sepetin başarıyla oluşturulmasının ardından uygulanır. |
| expirationTimeStamp   | DateTime         | Sepet tarih-saat biçiminde sona erer. Sepetin başarıyla oluşturulmasının ardından uygulanır.          |
| lastModifiedUser      | string           | Sepeti en son güncelleştirilen kullanıcı. Sepetin başarıyla oluşturulmasının ardından uygulanır.                          |
| lineItems             | Nesne dizisi | [Bir CartLineItem kaynakları](#cartlineitem) dizisi.                                                   |
| durum                | string           | Sepetin durumu. Olası değerler "Etkin" (güncelleştirilebilir/gönderebilirsiniz) ve "Sıralandı" (zaten gönderildi) değerleridir. |

## <a name="cartlineitem"></a>CartLineItem

Sepette yer alan bir öğeyi temsil eder.

| Özellik             | Tür                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                   | string                           | Sepet satır öğesi için benzersiz tanımlayıcı. Sepetin başarıyla oluşturulmasının ardından uygulanır.                                                                   |
| catalogItemId        | string                           | Katalog öğesi tanımlayıcısı.                                                                                                                          |
| Friendlyname         | string                           | İsteğe bağlı. Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                                                                 |
| miktar             | int                              | Lisans veya örnek sayısı.                                                                                                                  |
| currencyCode         | string                           | Para birimi kodu.                                                                                                                                    |
| billingCycle         | Nesne                           | Geçerli dönem için ayarlanmış faturalama dönemi türü.                                                                                                 |
| termDuration         | string                           | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler P1M (1 ay), P1Y (1 yıl) ve P3Y (3 yıl) değerleridir.                                |
| Katılımcılar         | Nesne Dizesi çiftlerinin listesi      | Satın almada Kayıtta PartnerId (MPN KIMLIĞI) koleksiyonu.                                                                                          |
| provisioningContext  | Sözlük<dizesi, dize>       | Satın alınan öğeyi sağlarken kullanılan ek bağlam. Belirli bir öğe için hangi değerlerin gerektiğini belirlemek için SKU'nun provisioningVariables özelliğine bakın. |
| orderGroup           | string                           | Hangi öğelerin birlikte aynı sırayla gönderil olduğunu belirten bir grup.                                                                          |
| addonItems           | **CartLineItem nesnelerinin** listesi | Eklentiler için sepet satır öğeleri koleksiyonu. Bu öğeler, kök sepet satır öğesinin satın alımından elde edildiklerinden temel aboneliğe doğru satın alınacak. |
| error                | Nesne                           | Bir hata oluştuktan sonra sepet oluşturulduktan sonra uygulanır.                                                                                                    |
| renewsTo             | Nesne dizisi                 | [RenewsTo kaynakları dizisi.](#renewsto)                                                                            |
| AttestationAccepted             | bool                 | Teklif veya sku koşullarının sözleşmeyi gösterir. Yalnızca SkuAttestationProperties veya OfferAttestationProperties enforceAttestation true olan teklifler veya sku'lar için gereklidir.                                                                            |

## <a name="renewsto"></a>RenewsTo

Bir sepet satır öğesinde yer alan bir öğeyi temsil eder.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | dize           | No              | Yenileme süresinin ISO 8601 gösterimi. Desteklenen geçerli değerler **P1M (1** ay) ve **P1Y (1** yıl) değerleridir. |

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

## <a name="carterror"></a>CartError

Sepet oluşturulduktan sonra oluşan bir hatayı temsil eder.

| Özellik         | Tür                                   | Description                                                                                   |
|------------------|----------------------------------------|-----------------------------------------------------------------------------------------------|
| errorCode        | [CareErrorCode](#carterrorcode) | Sepet hatasının türü.                                                                       |
| Errordescription | string                                 | Desteklenen değerler, varsayılan değerler veya sınırlar hakkında notlar da dahil olmak üzere hata açıklaması. |


## <a name="carterrorcode"></a>CartErrorCode

Sepet hatası türleri.

| Name                             | ErrorCode   | Description
|----------------------------------|-------------|-----------------------------------------------------------------------------------------------|
| CurrencyIsNotSupported           | 10000   | Para birimi, verilen pazar için desteklenmiyor  |
| CatalogItemIdIsNotValid          | 10001   | Katalog öğesi kimliği geçerli değil  |
| QuotaNotAvailable                | 10002   | Yeterli kota yok  |
| InventoryNotAvailable            | 10003   | Seçili teklif için envanter kullanılamıyor  |
| ParticipantsIsNotSupportedForPartner  | 10004   | İş Ortağı için katılımcıları ayarlama desteklenmiyor  |
| UnableToProcessCartLineItem      | 10006   | Sepet satır öğesi işemiyor.  |
| SubscriptionIsNotValid           | 10007   | Abonelik geçerli değil.  |
| SubscriptionIsNotEnabledForRI    | 10008   | RI satın alma için abonelik etkinleştirilmedi.  |
| SandboxLimitExceeded             | 10009   | Korumalı alan sınırı aşıldı.  |
| InvalidInput                     | 10010   | Genel giriş geçerli değil.  |
| SubscriptionNotRegistered        | 10011   | Abonelik geçerli değil.  |
| AttestationNotAccepted           | 10012   | Onay kabul edilmedi.  |
| Bilinmiyor                          | 0   | Varsayılan değer   |

## <a name="cartcheckoutresult"></a>CartCheckoutResult

Sepet iadenin sonucu temsil eder.

| Özellik    | Tür                                              | Description                     |
|-------------|---------------------------------------------------|---------------------------------|
| siparişler      | Order [nesnelerinin](order-resources.md#order) listesi.         | Sipariş koleksiyonu.       |
| orderErrors | [OrderError nesnelerinin](#ordererror) listesi. | Sipariş hatalarının koleksiyonu. |

## <a name="ordererror"></a>OrderError

Sipariş oluşturulduğunda sepetin iade oluşturulduğunda oluşan bir hatayı temsil eder.

| Özellik     | Tür   | Description                                     |
|--------------|--------|-------------------------------------------------|
| orderGroupId | string | Hatayla birlikte siparişin sipariş grubu kimliği. |
| kod         | int    | Hata kodu.                                 |
| açıklama  | string | Hatanın açıklaması.                   |
