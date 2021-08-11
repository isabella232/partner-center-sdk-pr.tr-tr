---
title: Abonelik kaynakları
description: Abonelik kaynakları, destek, para iadeleri, Azure yetkilendirmeleri gibi yaşam döngüsü boyunca abonelikler hakkında daha fazla bilgi sağlar.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e48927b9d8606f8d78ed8e4b5eb12da61f7a7d27f16316bca124f896a24a6638
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997983"
---
# <a name="subscription-resources"></a>Abonelik kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Abonelik, müşterinin belirli bir süre boyunca hizmet kullanmalarını sağlar. Tüm alanlar tüm abonelikler için geçerli olmaz. Çoğu alan yalnızca yaşam döngüsünün belirli noktalarında (örneğin, bir aboneliğin askıya alınmış veya iptal edilmiş olduğu) geçerlidir.

## <a name="subscription"></a>Abonelik

>[!NOTE]
>Abonelik **kaynağının** kiracı tanımlayıcısı başına dakikada 500 istek hız sınırı vardır.

Abonelik **kaynağı,** aboneliğin yaşam döngüsünü temsil eder ve abonelik yaşam döngüsü boyunca durumları tanımlayan özellikleri içerir.

| Özellik             | Tür                                                          | Description                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                   | string                                                        | Abonelik tanımlayıcısı.                                                                                                                                                  |
| offerId              | string                                                        | Teklif tanımlayıcısı.                                                                                                                                                         |
| entitlementId        | string                                                        | Yetkilendirme tanımlayıcısı (Azure abonelik kimliği).                                                                                                                        |
| offerName            | string                                                        | Teklif adı.                                                                                                                                                               |
| Friendlyname         | string                                                        | Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.                                                                                           |
| miktar             | sayı                                                        | Miktar. Örneğin, lisans tabanlı faturalama durumunda bu özellik lisans sayısına ayarlanır.                                                            |
| Unittype             | string                                                        | Abonelik için miktarı tanımlayan birimler.                                                                                                                             |
| parentSubscriptionId | string                                                        | Üst abonelik tanımlayıcısını alır veya ayarlar.                                                                                                                              |
| Creationdate         | string                                                        | Oluşturma tarihini tarih-saat biçiminde alır veya ayarlar.                                                                                                                          |
| effectiveStartDate   | UTC tarih saat biçiminde dize                                | Bu abonelik için geçerli başlangıç tarihini tarih-saat biçiminde alır veya ayarlar. Geçirilen bir aboneliğin tarihini geri alma veya başka bir abonelikle hizalamak için kullanılır.                |
| commitmentEndDate    | UTC tarih saat biçiminde dize                                | Bu aboneliğin tarih-saat biçiminde taahhüt bitiş tarihi. Otomatik olarak yenilenebilir olmayan abonelikler için bu, gelecekte çok uzak bir tarihi temsil eder.       |
| durum               | string                                                        | Abonelik durumu: "none", "active", "pending", "suspended" veya "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Aboneliğin otomatik olarak yenilenmeyi belirten bir değer alır.                                                                                                    |
| billingType          | string                                                        | Aboneliğin nasıl faturalandır olduğunu belirtir: "none", "usage" veya "license".                                                                                                      |
| billingCycle         | string                                                        | İş ortağının bu sipariş için faturalandırılama sıklığını gösterir. Desteklenen değerler, [**BillingCycleType**](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. |
| hasPurchasableAddons | boolean                                                       | Aboneliğin satın alınabilir eklentilere sahip olup olmadığını belirten bir değer alır veya ayarlar.                                                                                             |
| isTrial              | boolean                                                       | Bunun bir deneme aboneliği olup olmadığını belirten bir değer.                                                                                                                      |
| isMicrosoftProduct   | boolean                                                       | Bunun bir Microsoft ürünü olup olmadığını belirten bir değer.                                                                                                                       |
| publisherName        | string                                                        | Yayımcı adı.                                                                                                                                                           |
| eylem              | dize dizisi                                              | İzin verilen eylemleri alır veya ayarlar. Olası değerler: "edit", "cancel"                                                                                                  |
| partnerId            | string                                                        | Dolaylı iş ortağı modelinde kullanılan kaydın kurumsal bayisi MPN kimliği.                                                                                                     |
| suspensionReasons    | dize dizisi                                              | Salt okunur. Abonelik askıya alındı ise, bunun nedeni gösterir.                                                                                                                  |
| contractType         | string                                                        | Salt okunur. Sözleşme türü: "subscription", "productKey" veya "redemptionCode".                                                                                           |
| refundOptions        | [RefundOption kaynakları](#refundoption) dizisi   | Salt Okunur. Bu abonelik için kullanılabilen para iadesi seçenekleri kümesi.                                                                                              |
| Bağlantı                | [SubscriptionLinks](#subscriptionlinks)                       | Abonelik bağlantılarını alır veya ayarlar.                                                                                                                                          |
| Siparişno              | string                                                        | Aboneliğin başlaması için yerleştirilen siparişin kimliği.                                                                                                                |
| termDuration         | string                                                        | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler **P1M (1** ay), **P1Y (1** yıl) ve **P3Y** (3 yıl) değerleridir.                                                        |
| öznitelikler           | [Resourceattributes](utility-resources.md#resourceattributes) | Aboneliğe karşılık gelen meta veri öznitelikleri.                                                                                                                    |
| renewalTermDuration  | string                                                        | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler **P1M (1** ay) ve **P1Y (1** yıl) değerleridir.                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

**SubscriptionLinks** kaynağı, bir abonelik kaynağına bağlı bağlantıların koleksiyonunu açıklar.

| Özellik           | Tür                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| teklif              | [Bağlantı](utility-resources.md#link) | Teklifi alır veya ayarlar.               |
| parentSubscription | [Bağlantı](utility-resources.md#link) | Üst aboneliği alır veya ayarlar. |
| ürün            | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili ürünü alır. |
| Sku                | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili ürün sku'larını alır. |
| availability       | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili ürün sku kullanılabilirliğini alır. |
| activationLinks    | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili etkinleştirme bağlantılarının listesini alır. |
| Kendini               | [Bağlantı](utility-resources.md#link) | Kendi kendine URI.                         |
| ileri               | [Bağlantı](utility-resources.md#link) | Öğelerin sonraki sayfası.               |
| Önceki           | [Bağlantı](utility-resources.md#link) | Öğelerin önceki sayfası.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

**SubscriptionProvisioningStatus** kaynağı, bir aboneliğin sağlama durumu hakkında bilgi sağlar.

| Özellik   | Tür                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | string                                                         | Ürün SKU'su tanımlayan GUID biçimli bir dize.             |
| durum     | string                                                         | Sağlama durumunu gösterir: "success", "pending" veya "failed". |
| miktar   | sayı                                                         | Sağlama sonrasında abonelik miktarını sağlar.               |
| Bitiştarihi    | UTC tarih saat biçiminde dize                                 | Aboneliğin bitiş tarihi.                                    |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

**SubscriptionRegistrationStatus** kaynağı, bir abonelik kaynağına bağlı bağlantı koleksiyonunu açıklar.

| Özellik           | Tür                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | string                             | Abonelik tanımlayıcısı.                                                          |
| durum             | string                             | Kayıt durumunu gösterir: "registered", "registering" veya "notregistered".    |

## <a name="supportcontact"></a>SupportContact

**SupportContact kaynağı,** müşterinin aboneliği için bir destek ilgili kişisi temsil eder.

| Özellik        | Tür                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | string                                                         | Destek ilgili kişinin kiracı tanımlayıcısını gösteren GUID biçimli bir dize. |
| supportMpnId    | string                                                         | Kişinin Microsoft İş Ortağı Ağı (MPN) tanımlayıcısı.                       |
| name            | string                                                         | Destek ilgili kişisi adı.                                                |
| Bağlantı           | [ResourceLinks](utility-resources.md#resourcelinks)            | Destek ilgili kişisi bağlantıları.                                              |
| öznitelikler      | [Resourceattributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri. "objectType": " SupportContact" ifadesini içerir.              |

## <a name="registersubscription"></a>RegisterSubscription

**RegisterSubscription** kaynağı, bir aboneliğin kayıt durumunu sorgulamak için kullanılan bir bağlantı döndürür. Kayıt durumu, Başarıyla kabul edilen bir Azure aboneliğini kaydetme isteğinin yanıt gövdesinde döndürülür.

| Özellik                | Tür                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Kayıt durumunu sorgulama bağlantısını içeren bir Konum üst bilgisi ile birlikte HTTP Durum Kodu 202 "Kabul Edildi" döndürür. Örneğin, `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>RefundOption

**RefundOption kaynağı,** abonelik için olası bir para iadesi seçeneğini temsil eder.

| Özellik          | Tür | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| tür | string | Para iadesi türü. Desteklenen değerler "Partial" ve "Full" değerleridir |
| expiresAfter      | UTC tarih saat biçiminde dize | Bu seçeneğin süresi dolduğunda zaman damgası. Null ise, bu süre sonu olmadığını gösterir. |

## <a name="azureentitlement"></a>AzureEntitlement

**AzureEntitlement kaynağı,** aboneliğin Azure yetkilendirmelerini temsil eder.

| Özellik          | Tür | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| kimlik | string | Yetkilendirme tanımlayıcısı |
| Friendlyname      | string | Yetkilendirmenin kolay adı. |
| durum | string | Yetkilendirmenin durumu. |
| subscriptionId | string | Yetkilendirmenin ait olduğu abonelik tanımlayıcısı. |
