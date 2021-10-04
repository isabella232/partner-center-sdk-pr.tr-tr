---
title: Abonelik kaynakları
description: Abonelik kaynakları, destek, para iadesi, Azure yetkilendirmeleri gibi yaşam döngüsünün tamamında abonelikler hakkında daha fazla bilgi sağlayabilir.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 461df9cdb909fc44be9069cb7eb4b41fa2a5f170
ms.sourcegitcommit: 3ee00d9fe9da6b9df0fb7027ae506e2abe722770
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/04/2021
ms.locfileid: "129417296"
---
# <a name="subscription-resources"></a>Abonelik kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

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
| durum               | string                                                        | Abonelik durumu: "none", "etkin", "bekleyen", "askıya alındı", "süre dolmuþ" veya "Deleted".                                                                                                         |
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
| ProductType  | [ItemType](product-resources.md#itemtype)                             | Salt okunur. Aboneliğin için olduğu ürün türü.     |
| Tüketim Mptiontype  | [fazla kullanım](subscription-resources.md#overage) kaynakları dizisi   | Belirli bir müşterinin fazla kullanım süresini alır veya ayarlar.     |

## <a name="subscriptionlinks"></a>SubscriptionLinks

**Subscriptionlinks** kaynağı bir abonelik kaynağına ekli bağlantıların koleksiyonunu açıklar.

| Özellik           | Tür                               | Description                           |
|--------------------|------------------------------------|---------------------------------------|
| teklif              | [Bağlantısının](utility-resources.md#link) | Teklifi alır veya ayarlar.               |
| parentSubscription | [Bağlantısının](utility-resources.md#link) | Üst aboneliği alır veya ayarlar. |
| ürün            | [Bağlantısının](utility-resources.md#link) | Abonelikle ilişkili ürünü alır. |
| isteyin                | [Bağlantısının](utility-resources.md#link) | Abonelikle ilişkili Ürün SKU 'sunu alır. |
| availability       | [Bağlantısının](utility-resources.md#link) | Abonelikle ilişkili ürün sku kullanılabilirliğini alır. |
| activationLinks    | [Bağlantısının](utility-resources.md#link) | Abonelikle ilişkili etkinleştirme bağlantılarının listesini alır. |
| Self               | [Bağlantısının](utility-resources.md#link) | Self-URI.                         |
| ileri               | [Bağlantısının](utility-resources.md#link) | Öğelerin sonraki sayfası.               |
| Öncekini           | [Bağlantısının](utility-resources.md#link) | Öğelerin önceki sayfası.           |

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

## <a name="overage"></a>Kapasite Aşımı

**Fazla kullanım** kaynağı, atanan ve satıcıya atanan tüketim aboneliğini temsil eder.

| Özellik        | Tür               | Description                                                                     |
|-----------------|--------------------|---------------------------------------------------------------------------------|
| azureEntitlementId | string       | Tüketim abonelik tanımlayıcısını gösteren GUID biçimli dize. |
| iş ortağı kimliği    | string            | Abonelikle ilişkili Bayi Microsoft İş Ortağı Ağı (MPN) tanımlayıcısı.        |
| tür    | string       | Fazla kullanım türü "PhoneServices" olabilir       |
| fazla kullanım            | boolean      | Fazla kullanım özelliğinin etkinleştirilip etkinleştirilmediğini gösteren değer.       |
| Köprü           | [Resourcelmürekkepler](utility-resources.md#resourcelinks)            | Fazla kullanım ile ilgili bağlantılar.                          |
| öznitelikler      | [ResourceAttributes](utility-resources.md#resourceattributes)  | Meta veri öznitelikleri. "ObjectType" içerir: "fazla kullanım".  |



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
