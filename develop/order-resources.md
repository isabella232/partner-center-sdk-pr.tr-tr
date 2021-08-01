---
title: Kaynakları sıralama
description: Bir iş ortağı bir müşteri bir teklif listesinden abonelik satın almak istediğinde bir sipariş koyar.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 128c9e041cacc1c15f6187c4d99690d5c5fa4183
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009180"
---
# <a name="order-resources"></a>Kaynakları sıralama

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bir iş ortağı bir müşteri bir teklif listesinden abonelik satın almak istediğinde bir sipariş koyar.

>[!NOTE]
>Sipariş kaynağı, kiracı tanımlayıcısı başına dakikada 500 istekten oluşan bir hız sınırına sahiptir.

## <a name="order"></a>Sipariş

Ortağın sırasını açıklar.

| Özellik           | Tür                                               | Description                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| kimlik                 | string                                             | Siparişin başarıyla oluşturulması sırasında sağlanan bir sipariş tanımlayıcısı.                                   |
| AlternateId        | string                                             | Sipariş için kolay bir tanımlayıcı.                                                                          |
|Referencecustomerıd | string                                             | Müşteri tanımlayıcısı. |
| Bilimlingcycle       | string                                             | Ortağın bu sipariş için faturalandırılabileceği sıklığı belirtir. Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. "Aylık" veya "OneTime" varsayılan olarak sıralı oluşturma. Bu alan, siparişin başarıyla oluşturulmasından sonra uygulanır. |
| Işlem türü    | string                                             | Salt okunur. Siparişin işlem türü. Desteklenen değerler ' UserPurchase ', ' SystemPurchase ' veya ' Systemfaturalandırma ' |
| LineItems          | [Orderlineıtem](#orderlineitem) kaynakları dizisi | Müşterinin miktarı dahil satın aldığı tekliflerinin listesi.        |
| currencyCode       | string                                             | Salt okunur. Sipariş yerleştirilirken kullanılan para birimi. Siparişin başarıyla oluşturulmasından sonra uygulandı.           |
| currencySymbol     | string                                             | Salt okunur. Para birimi koduyla ilişkili para birimi simgesi. |
| creationDate       | datetime                                           | Salt okunur. Siparişin oluşturulduğu tarih ve saat biçimi. Siparişin başarıyla oluşturulmasından sonra uygulandı.                                   |
| durum             | string                                             | Salt okunur. Siparişin durumu.  Desteklenen değerler [**Orderstatus**](#orderstatus)içinde bulunan üye adlarıdır.        |
| Köprü              | [OrderLinks](utility-resources.md#resourcelinks)           | Sıraya karşılık gelen kaynak bağlantıları.            |
| öznitelikler         | [ResourceAttributes](utility-resources.md#resourceattributes) | Sıraya karşılık gelen meta veri öznitelikleri.       |

## <a name="orderlineitem"></a>Orderlineıtem

Bir sipariş, tekliflerin bir listesini içerir ve her öğe bir Orderlineıtem olarak temsil edilir.

| Özellik             | Tür                                      | Description                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lineıtemnumber       | int                                       | Koleksiyondaki her bir satır öğesi, 0 ' dan say-1 ' e kadar sayarak benzersiz bir satır numarası alır.                                                                                                                                                 |
| OfferId              | string                                    | Teklifin KIMLIĞI.                                                                                                                                                                                                                       |
| subscriptionId       | string                                    | Aboneliğin KIMLIĞI.                                                                                                                                                                                                                |
| Parentsubscriptionıd | string                                    | İsteğe bağlı. Bir eklenti teklifinde üst aboneliğin KIMLIĞI. Yalnızca düzeltme eki için geçerlidir.                                                                                                                                                     |
| friendlyName         | string                                    | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.                                                                                                                                              |
| miktar             | int                                       | Lisans veya örnek sayısı.                                                                                                                                                                                |
| termDuration         | string                                    | Terimin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay), **P1Y** (1 yıl) ve **P3Y** (3 yıl).                               |
| Işlem türü      | string                                    | Salt okunur. Satır öğesinin işlem türü. Desteklenen değerler ' New ', ' Renew ', ' addQuantity ', ' removeQuantity ', ' Cancel ', ' Convert ' veya ' Customerkred' değerleridir. |
| partnerIdOnRecord    | string                                    | Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir). Bu, teşvikleri için doğru hesaplamayı sağlar. |
| provisioningContext  | Sözlük<dize, dize>            | Katalogdaki bazı öğelerin sağlanması için gereken bilgiler. SKU 'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.                                                                                                                                               |
| Köprü                | [Orderlineıtemlinks](#orderlineitemlinks) | Salt okunur. Sipariş satırı öğesine karşılık gelen kaynak bağlantıları.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Yenileme dönemi süresi ayrıntıları.                                                                           |
| AttestationAccepted             | bool                 | Teklif veya SKU koşullarına yönelik anlaşmayı gösterir. Yalnızca SkuAttestationProperties veya OfferAttestationProperties Enforcekanıtlama 'nin doğru olduğu teklifler veya SKU 'lar için gereklidir.                                                                            |

## <a name="renewsto"></a>RenewsTo

Yenileme dönemi süre ayrıntılarını temsil eder.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | dize           | No              | Yenileme teriminin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl). |

## <a name="orderlinks"></a>OrderLinks

Sıraya karşılık gelen kaynak bağlantılarını temsil eder.

| Özellik           | Tür                                         | Description                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Bağlantısının](utility-resources.md#link)            | Doldurulduğunda, sipariş için sağlama durumunu alma bağlantısı.       |
| Self               | [Bağlantısının](utility-resources.md#link)            | Sipariş kaynağını alma bağlantısı.                                      |

## <a name="orderlineitemlinks"></a>Orderlineıtemlinks

Siparişle ilişkili tam aboneliği temsil eder.

| Özellik           | Tür                                         | Description                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Bağlantısının](utility-resources.md#link)            | Doldurulduğunda, satır öğesinin [sağlama durumunu](#orderlineitemprovisioningstatus) alma bağlantısı.       |
| isteyin                | [Bağlantısının](utility-resources.md#link)            | Satın alınan katalog öğesi için SKU bilgilerini alma bağlantısı.                    |
| aboneliği       | [Bağlantısının](utility-resources.md#link)            | Doldurulduğunda, tam abonelik bilgilerinin bağlantısı.                       |
| activationLinks    | [Bağlantısının](utility-resources.md#link)            | Doldurulduğunda, aboneliği etkinleştirmek için bağlantılar kaynağı al.             |

## <a name="orderstatus"></a>OrderStatus

Siparişin durumunu belirten değerler içeren bir [enum/DotNet/api/System. Enum).

| Değer              | Konum     | Description                                     |
|--------------------|--------------|-------------------------------------------------|
| bilinmeyen            | 0            | Sabit Listesi başlatıcısı.                               |
| dım          | 1            | Siparişin tamamlandığını gösterir.          |
| bekleniyor            | 2            | Siparişin hala beklendiğini gösterir.      |
| yürütüldükten          | 3            | Siparişin iptal edildiğini gösterir.    |

## <a name="orderlineitemprovisioningstatus"></a>Orderlineıtemprovisioningstatus

Bir [Orderlineıtem öğesinin](#orderlineitem)sağlama durumunu temsil eder.

| Özellik                        | Tür                                | Description                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| Lineıtemnumber                  | int                                 | Sipariş satırı öğesinin benzersiz satır numarası. Değerler 0 ile Count-1 arasındadır.             |
| durum                          | string                              | Sipariş satırı öğesinin sağlama durumu. Değerlere şunlar dahildir:</br>**Yerine getirilme**: siparişin yerine getirilmesi başarıyla tamamlandı ve Kullanıcı ayırmaları kullanabiliyor</br>**Karşılanmayan**: iptal nedeniyle karşılanmadı</br>**PrefulfillmentPending**: isteğiniz hala işleniyor, tamamlama henüz tamamlanmadı |
| Quantityprovisioningınformation | Liste<[Quantityprovisioningstatus](#quantityprovisioningstatus)> | Sipariş satırı öğesi için miktar sağlama durum bilgilerinin listesi. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Kaynak sağlama durumunu miktara göre gösterir.

| Özellik                           | Tür                                         | Description                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| miktar                           | int                                          | Öğe sayısı.                                 |
| durum                             | string                                       | Öğe sayısının durumu.                   |
