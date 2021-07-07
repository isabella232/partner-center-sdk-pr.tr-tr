---
title: Abonelik kaynakları
description: Abonelik kaynakları, destek, para iadesi, Azure yetkilendirmeleri gibi yaşam döngüsünün tamamında abonelikler hakkında daha fazla bilgi sağlayabilir.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35d8c86ab061797109b3c152eff02f354b7ea23a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547469"
---
# <a name="subscription-resources"></a>Abonelik kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Abonelik, müşterinin belirli bir süre boyunca hizmet kullanmasına olanak sağlar. Tüm alanlar tüm abonelikler için uygulanmaz. Birçok alan yalnızca yaşam döngüsünün bir abonelik askıya alınma veya iptal edilme gibi belirli noktalarda geçerlidir.

## <a name="subscription"></a>Abonelik

>[!NOTE]
>**Abonelik** kaynağında, kiracı tanımlayıcısı başına dakikada 500 istek bir hız limiti vardır.

Abonelik **kaynağı bir** aboneliğin yaşam döngüsünü temsil eder ve abonelik yaşam döngüsü boyunca durumları tanımlayan özellikleri içerir.

| Özellik             | Tür                                                          | Açıklama                                                                                                                                                                   |
|----------------------|---------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                   | string                                                        | Abonelik tanımlayıcısı.                                                                                                                                                  |
| OfferId              | string                                                        | Teklif tanımlayıcısı.                                                                                                                                                         |
| entitlementId        | string                                                        | Yetkilendirme tanımlayıcısı (bir Azure abonelik KIMLIĞI).                                                                                                                        |
| offerName            | string                                                        | Teklif adı.                                                                                                                                                               |
| friendlyName         | string                                                        | Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.                                                                                           |
| miktar             | sayı                                                        | Miktar. Örneğin, lisans tabanlı faturalandırma durumunda bu özellik lisans sayısına ayarlanır.                                                            |
| unitType             | string                                                        | Abonelik için miktarı tanımlayan birimler.                                                                                                                             |
| Parentsubscriptionıd | string                                                        | Üst abonelik tanımlayıcısını alır veya ayarlar.                                                                                                                              |
| creationDate         | string                                                        | Oluşturulma tarihini tarih-saat biçiminde alır veya ayarlar.                                                                                                                          |
| effectiveStartDate   | UTC Tarih saat biçiminde dize                                | Bu abonelik için tarih-saat biçiminde geçerli başlangıç tarihini alır veya ayarlar. Geçirilen bir aboneliğin tarihini geri almak veya başka bir abonelik ile hizalamak için kullanılır.                |
| commitmentEndDate    | UTC Tarih saat biçiminde dize                                | Bu abonelik için tarih-saat biçiminde taahhüt bitiş tarihi. Otomatik olarak yenilenebilecek abonelikler için bu, gelecekte bir tarihi temsil eder.       |
| durum               | string                                                        | Abonelik durumu: "none", "Active", "Pending", "askıya alındı" veya "Deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer alır.                                                                                                    |
| billingType          | string                                                        | Aboneliğin nasıl faturalandırıldığını belirtir: "none", "Usage" veya "License".                                                                                                      |
| Bilimlingcycle         | string                                                        | Ortağın bu sipariş için faturalandırılabileceği sıklığı belirtir. Desteklenen değerler, [**BillingCycleType**](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. |
| hasPurchasableAddons | boolean                                                       | Aboneliğin satın alınabilir alınırken eklentilere sahip olup olmadığını gösteren bir değer alır veya ayarlar.                                                                                             |
| Isdeneme              | boolean                                                       | Bunun deneme aboneliği olup olmadığını gösteren bir değer.                                                                                                                      |
| ımicrosoftürünü   | boolean                                                       | Bunun bir Microsoft ürünü olup olmadığını gösteren bir değer.                                                                                                                       |
| publisherName        | string                                                        | Yayımcı adı.                                                                                                                                                           |
| eylem              | dize dizisi                                              | İzin verilen eylemleri alır veya ayarlar. Olası değerler: "Düzenle", "iptal"                                                                                                  |
| iş ortağı kimliği            | string                                                        | Dolaylı iş ortağı modelinde kullanılan kayıt satıcısının MPN KIMLIĞI.                                                                                                     |
| suspensionReasons    | dize dizisi                                              | Salt okunur. Abonelik askıya alınmışsa neden olduğunu gösterir.                                                                                                                  |
| contractType         | string                                                        | Salt okunur. Sözleşmenin türü: "Subscription", "productKey" veya "Mptioncode".                                                                                           |
| geri alınabilir seçenekler        | geri [alınamaz](#refundoption) Kaynak dizisi   | Salt okunurdur. Bu abonelik için kullanılabilen geri ödeme seçenekleri kümesi.                                                                                              |
| Köprü                | [SubscriptionLinks](#subscriptionlinks)                       | Abonelik bağlantılarını alır veya ayarlar.                                                                                                                                          |
| Sipariş              | string                                                        | Aboneliği başlatmak için verilen sıranın KIMLIĞI.                                                                                                                |
| termDuration         | string                                                        | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler **P1M (1** ay), **P1Y (1** yıl) ve **P3Y** (3 yıl) değerleridir.                                                        |
| öznitelikler           | [Resourceattributes](utility-resources.md#resourceattributes) | Aboneliğe karşılık gelen meta veri öznitelikleri.                                                                                                                    |
| renewalTermDuration  | string                                                        | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler **P1M (1** ay) ve **P1Y (1** yıl) değerleridir.                                                        |

## <a name="subscriptionlinks"></a>SubscriptionLinks

**SubscriptionLinks** kaynağı, bir abonelik kaynağına bağlı bağlantıların koleksiyonunu açıklar.

| Özellik           | Tür                               | Açıklama                           |
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

| Özellik   | Tür                                                           | Açıklama                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | string                                                         | Ürün SKU'su tanımlayan GUID biçimli bir dize.             |
| durum     | string                                                         | Sağlama durumunu gösterir: "success", "pending" veya "failed". |
| miktar   | sayı                                                         | Sağlama sonrasında abonelik miktarını sağlar.               |
| Bitiştarihi    | UTC tarih saat biçiminde dize                                 | Aboneliğin bitiş tarihi.                                    |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

**SubscriptionRegistrationStatus** kaynağı, bir abonelik kaynağına bağlı bağlantı koleksiyonunu açıklar.

| Özellik           | Tür                               | Açıklama                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | string                             | Abonelik tanımlayıcısı.                                                          |
| durum             | string                             | Kayıt durumunu gösterir: "registered", "registering" veya "notregistered".    |

## <a name="supportcontact"></a>SupportContact

**SupportContact kaynağı,** müşterinin aboneliği için bir destek ilgili kişisi temsil eder.

| Özellik        | Tür                                                           | Açıklama                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| supportTenantId | string                                                         | Destek ilgili kişinin kiracı tanımlayıcısını gösteren GUID biçimli bir dize. |
| supportMpnId    | string                                                         | Kişinin Microsoft İş Ortağı Ağı (MPN) tanımlayıcısı.                       |
| name            | string                                                         | Destek ilgili kişisi adı.                                                |
| Bağlantı           | [ResourceLinks](utility-resources.md#resourcelinks)            | Destek ilgili kişisi bağlantıları.                                              |
| öznitelikler      | [Resourceattributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri. "objectType": " SupportContact" ifadesini içerir.              |

## <a name="registersubscription"></a>RegisterSubscription

**RegisterSubscription** kaynağı, bir aboneliğin kayıt durumunu sorgulamak için kullanılan bir bağlantı döndürür. Kayıt durumu, Başarıyla kabul edilen bir Azure aboneliğini kaydetme isteğinin yanıt gövdesinde döndürülür.

| Özellik                | Tür                               | Açıklama                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Kayıt durumunu sorgulamak için bir bağlantı içeren konum üst bilgisi olan 202 "kabul edildi" HTTP durum kodunu döndürür. Örneğin, `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>Geri alınamaz

**Refundoresource** , abonelik için olası bir para iadesi seçeneğini temsil eder.

| Özellik          | Tür | Açıklama                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| tür | string | Para iadesi türü. Desteklenen değerler "partial" ve "Full" |
| expiresAfter      | UTC Tarih saat biçiminde dize | Bu seçenek sona erdiğinde zaman damgası. Null ise bu, süresi dolmayacağı anlamına gelir. |

## <a name="azureentitlement"></a>AzureEntitlement

**AzureEntitlement** kaynağı, abonelik için Azure yetkilendirmelerini temsil eder.

| Özellik          | Tür | Açıklama                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| kimlik | string | Yetkilendirme tanımlayıcısı |
| friendlyName      | string | Yetkilendirme kolay adı. |
| durum | string | Yetkilendirme durumu. |
| subscriptionId | string | Yetkilendirimin ait olduğu abonelik tanımlayıcısı. |
