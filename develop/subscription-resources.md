---
title: Abonelik kaynakları
description: Abonelik kaynakları, destek, para iadesi, Azure yetkilendirmeleri gibi yaşam döngüsünün tamamında abonelikler hakkında daha fazla bilgi sağlayabilir.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd835e46e99b1fcb1e0b0e694ad73b1dca1240c9
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768963"
---
# <a name="subscription-resources"></a>Abonelik kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Abonelik, müşterinin belirli bir süre boyunca hizmet kullanmasına olanak sağlar. Tüm alanlar tüm abonelikler için uygulanmaz. Birçok alan yalnızca yaşam döngüsünün bir abonelik askıya alınma veya iptal edilme gibi belirli noktalarda geçerlidir.

## <a name="subscription"></a>Abonelik

>[!NOTE]
>**Abonelik** kaynağında, kiracı tanımlayıcısı başına dakikada 500 istek bir hız limiti vardır.

Abonelik **kaynağı bir** aboneliğin yaşam döngüsünü temsil eder ve abonelik yaşam döngüsü boyunca durumları tanımlayan özellikleri içerir.

| Özellik             | Tür                                                          | Description                                                                                                                                                                   |
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
| commitmentEndDate    | UTC Tarih saat biçiminde dize                                | Bu abonelik için tarih-saat biçiminde taahhüt bitiş tarihi. Otomatik olarak yenilenebilen abonelikler için bu, gelecekte bir tarihi temsil eder.       |
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
| termDuration         | string                                                        | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay), **P1Y** (1 yıl) ve **P3Y** (3 yıl).                                                        |
| öznitelikler           | [ResourceAttributes](utility-resources.md#resourceattributes) | Aboneliğe karşılık gelen meta veri öznitelikleri.                                                                                                                    |
| renewalTermDuration  | string                                                        | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl).                                                        |

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
| Self               | [Bağlantı](utility-resources.md#link) | Self URI.                         |
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

**Registersubscription** kaynağı, bir aboneliğin kayıt durumunu sorgulamak için kullanılabilecek bir bağlantı döndürür. Kayıt durumu, Azure aboneliğini kaydetmek için başarıyla kabul edilen bir isteğin yanıt gövdesinde döndürülür.

| Özellik                | Tür                               | Description                                                                           |
|-------------------------|------------------------------------|---------------------------------------------------------------------------------------|
| httpResponseMessage     | object                             | Kayıt durumunu sorgulamak için bir bağlantı içeren konum üst bilgisi olan 202 "kabul edildi" HTTP durum kodunu döndürür. Örneğin, `"/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus"` |

## <a name="refundoption"></a>Geri alınamaz

**Refundoresource** , abonelik için olası bir para iadesi seçeneğini temsil eder.

| Özellik          | Tür | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| tür | string | Para iadesi türü. Desteklenen değerler "partial" ve "Full" |
| expiresAfter      | UTC Tarih saat biçiminde dize | Bu seçenek sona erdiğinde zaman damgası. Null ise bu, süresi dolmayacağı anlamına gelir. |

## <a name="azureentitlement"></a>AzureEntitlement

**AzureEntitlement** kaynağı, abonelik için Azure yetkilendirmelerini temsil eder.

| Özellik          | Tür | Description                                                                         |
|-------------------|--------|-------------------------------------------------------------------------------------|
| kimlik | string | Yetkilendirme tanımlayıcısı |
| friendlyName      | string | Yetkilendirme kolay adı. |
| durum | string | Yetkilendirme durumu. |
| subscriptionId | string | Yetkilendirimin ait olduğu abonelik tanımlayıcısı. |
