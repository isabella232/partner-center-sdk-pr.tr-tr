---
title: Abonelik kaynakları
description: Abonelik kaynakları, destek, para iadeleri, Azure yetkilendirmeleri gibi yaşam döngüsü boyunca abonelikler hakkında daha fazla bilgi sağlar.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c898f9673525cf0ba32619b7c7b16f91311a81c7
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456817"
---
# <a name="subscription-resources"></a>Abonelik kaynakları

**Uygulama:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet tarafından | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

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
| durum               | string                                                        | Abonelik durumu: "none", "active", "pending", "suspended", "expired" veya "deleted".                                                                                                         |
| autoRenewEnabled     | boolean                                                       | Aboneliğin otomatik olarak yenilenmeyi belirten bir değer alır.                                                                                                    |
| billingType          | string                                                        | Aboneliğin nasıl faturalandır olduğunu belirtir: "none", "usage" veya "license".                                                                                                      |
| billingCycle         | string                                                        | İş ortağının bu sipariş için faturalandırılama sıklığını gösterir. Desteklenen değerler [**BillingCycleType**](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. |
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
| termDuration         | string                                                        | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay), **P1Y** (1 yıl) ve **P3Y** (3 yıl).                                                        |
| öznitelikler           | [ResourceAttributes](utility-resources.md#resourceattributes) | Aboneliğe karşılık gelen meta veri öznitelikleri.                                                                                                                    |
| renewalTermDuration  | string                                                        | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl).                                                        |
| ProductType  | [ItemType](product-resources.md#itemtype)                             | Salt okunur. Aboneliğin için olduğu ürün türü.     |

## <a name="subscriptionlinks"></a>SubscriptionLinks

**Subscriptionlinks** kaynağı bir abonelik kaynağına ekli bağlantıların koleksiyonunu açıklar.

| Özellik           | Tür                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| teklif              | [Bağlantı](utility-resources.md#link) | Teklifi alır veya ayarlar.               |
| parentSubscription | [Bağlantı](utility-resources.md#link) | Üst aboneliği alır veya ayarlar. |
| ürün            | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili ürünü alır. |
| isteyin                | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili Ürün SKU 'sunu alır. |
| availability       | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili ürün sku kullanılabilirliğini alır. |
| activationLinks    | [Bağlantı](utility-resources.md#link) | Abonelikle ilişkili etkinleştirme bağlantılarının listesini alır. |
| Self               | [Bağlantı](utility-resources.md#link) | Self-URI.                         |
| ileri               | [Bağlantı](utility-resources.md#link) | Öğelerin sonraki sayfası.               |
| Öncekini           | [Bağlantı](utility-resources.md#link) | Öğelerin önceki sayfası.           |

## <a name="subscriptionprovisioningstatus"></a>SubscriptionProvisioningStatus

**Subscriptionprovisioningstatus** kaynağı bir aboneliğin sağlama durumu hakkında bilgi sağlar.

| Özellik   | Tür                                                           | Description                                                          |
|------------|----------------------------------------------------------------|----------------------------------------------------------------------|
| skuId      | string                                                         | Ürün SKU 'sunu tanımlayan GUID biçimli dize.             |
| durum     | string                                                         | Sağlama durumunu belirtir: "başarılı", "bekliyor" veya "başarısız". |
| miktar   | sayı                                                         | , Sağlama sonrasında abonelik miktarını sağlar.               |
| endDate    | UTC Tarih saat biçiminde dize                                 | Aboneliğin bitiş tarihi.                                    |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri.                                             |

## <a name="subscriptionregistrationstatus"></a>SubscriptionRegistrationStatus

**Subscriptionregistrationstatus** kaynağı bir abonelik kaynağına ekli bağlantıların koleksiyonunu açıklar.

| Özellik           | Tür                               | Description                                                                           |
|--------------------|------------------------------------|---------------------------------------------------------------------------------------|
| subscriptionId     | string                             | Abonelik tanımlayıcısı.                                                          |
| durum             | string                             | Kayıt durumunu belirtir: "kayıtlı", "kayıt" veya "notregistered".    |

## <a name="supportcontact"></a>SupportContact

**Supportcontact** kaynağı bir müşterinin aboneliğine yönelik bir destek kişisi temsil eder.

| Özellik        | Tür                                                           | Description                                                                     |
|-----------------|----------------------------------------------------------------|---------------------------------------------------------------------------------|
| Supporttenantıd | string                                                         | Destek kişisinin kiracı tanımlayıcısını gösteren bir GUID biçimli dize. |
| Supportmpnıd    | string                                                         | Kişinin Microsoft İş Ortağı Ağı (MPN) tanımlayıcısı.                       |
| name            | string                                                         | Destek kişisinin adı.                                                |
| Köprü           | [Resourcelmürekkepler](utility-resources.md#resourcelinks)            | Destek ile ilgili bağlantılar iletişim kurun.                                              |
| öznitelikler      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri. "ObjectType": "SupportContact" içerir.              |

## <a name="registersubscription"></a>RegisterSubscription

**Registersubscription** kaynağı, bir aboneliğin kayıt durumunu sorgulamak için kullanılabilecek bir bağlantı döndürür. Kayıt durumu, Başarıyla kabul edilen bir Azure aboneliğini kaydetme isteğinin yanıt gövdesinde döndürülür.

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
