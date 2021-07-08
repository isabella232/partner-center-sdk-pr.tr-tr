---
title: Kaynakları sıralama
description: Müşteri teklif listesinden abonelik satın almak istediği zaman iş ortağı sipariş verdi.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c993317f288568dd687c3b52bf47e4520fcd18c6
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548065"
---
# <a name="order-resources"></a>Kaynakları sıralama

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Müşteri teklif listesinden abonelik satın almak istediği zaman iş ortağı sipariş verdi.

>[!NOTE]
>Sipariş kaynağının kiracı tanımlayıcısı başına dakikada 500 istek hız sınırı vardır.

## <a name="order"></a>Sipariş

Bir iş ortağının siparişlerini açıklar.

| Özellik           | Tür                                               | Açıklama                                                 |
|--------------------|----------------------------------------------------|-------------------------------------------------------------|
| kimlik                 | string                                             | Siparişin başarıyla oluşturulmasının ardından sağlanan bir sipariş tanımlayıcısı.                                   |
| alternateId        | string                                             | Sipariş için kolay tanımlayıcı.                                                                          |
|referenceCustomerId | string                                             | Müşteri tanımlayıcısı. |
| billingCycle       | string                                             | İş ortağının bu sipariş için faturalandırılama sıklığını gösterir. Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. Varsayılan değer, sipariş oluşturma sırasında "Monthly" veya "OneTime" şeklindedir. Bu alan, siparişin başarıyla oluşturulmasının ardından uygulanır. |
| Transactiontype    | string                                             | Salt okunur. Siparişin işlem türü. Desteklenen değerler 'UserPurchase', 'SystemPurchase' veya 'SystemBilling' değerleridir |
| lineItems          | [OrderLineItem kaynakları](#orderlineitem) dizisi | Miktarı da dahil olmak üzere müşterinin satın alma tekliflerinin maddeli listesi.        |
| currencyCode       | string                                             | Salt okunur. Siparişin yerleştirilmesi için kullanılan para birimi. Siparişin başarıyla oluşturulmasının ardından uygulanır.           |
| Currencysymbol     | string                                             | Salt okunur. Para birimi koduyla ilişkili para birimi simgesi. |
| Creationdate       | datetime                                           | Salt okunur. Siparişin tarih-saat biçiminde oluşturulma tarihi. Siparişin başarıyla oluşturulmasının ardından uygulanır.                                   |
| durum             | string                                             | Salt okunur. Siparişin durumu.  Desteklenen değerler OrderStatus içinde bulunan üye [**adlarıdır.**](#orderstatus)        |
| Bağlantı              | [OrderLinks](utility-resources.md#resourcelinks)           | Siparişe karşılık gelen kaynak bağlantıları.            |
| öznitelikler         | [Resourceattributes](utility-resources.md#resourceattributes) | Order'a karşılık gelen meta veri öznitelikleri.       |

## <a name="orderlineitem"></a>OrderLineItem

Sipariş, tekliflerin maddeli bir listesini içerir ve her öğe bir OrderLineItem olarak temsil edilen bir listedir.

| Özellik             | Tür                                      | Açıklama                                                                                                                                                                                                                                |
|----------------------|-------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| lineItemNumber       | int                                       | Koleksiyonda yer alan her satır öğesi benzersiz bir satır numarası alır ve 0 ile 1 arasında bir sayıya kadar sayar.                                                                                                                                                 |
| offerId              | string                                    | Teklifin kimliği.                                                                                                                                                                                                                       |
| subscriptionId       | string                                    | Aboneliğin kimliği.                                                                                                                                                                                                                |
| parentSubscriptionId | string                                    | İsteğe bağlı. Eklenti teklifinde üst aboneliğin kimliği. Yalnızca PATCH için geçerlidir.                                                                                                                                                     |
| Friendlyname         | string                                    | İsteğe bağlı. Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.                                                                                                                                              |
| miktar             | int                                       | Lisans veya örnek sayısı.                                                                                                                                                                                |
| termDuration         | string                                    | Sürenin ISO 8601 gösterimi. Desteklenen geçerli değerler **P1M (1** ay), **P1Y (1** yıl) ve **P3Y** (3 yıl) değerleridir.                               |
| Transactiontype      | string                                    | Salt okunur. Satır öğesinin işlem türü. Desteklenen Değerler:'new', 'renew', 'addQuantity', 'removeQuantity', 'cancel', 'convert' veya 'customerCredit'. |
| partnerIdOnRecord    | string                                    | Dolaylı sağlayıcı dolaylı bir kurumsal bayi adına sipariş verdiylerinde, bu alanı yalnızca dolaylı kurumsal bayinin MPN kimliğiyle **(dolaylı** sağlayıcının kimliği hiçbir zaman) doldurmak. Bu, teşvikler için doğru hesaplamayı sağlar. |
| provisioningContext  | Sözlük<dizesi, dize>            | Katalogdaki bazı öğeler için sağlama için gereken bilgiler. SKU'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.                                                                                                                                               |
| Bağlantı                | [OrderLineItemLinks](#orderlineitemlinks) | Salt okunur. Sipariş satırı öğesine karşılık gelen kaynak bağlantıları.                                                                                                                                                                                |
| renewsTo             | [RenewsTo](#renewsto)                         |Yenileme süresi süresi ayrıntıları.                                                                           |

## <a name="renewsto"></a>RenewsTo

Yenileme süresi süresi ayrıntılarını temsil eder.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | dize           | No              | Yenileme süresinin ISO 8601 gösterimi. Desteklenen geçerli değerler **P1M (1** ay) ve **P1Y (1** yıl) değerleridir. |

## <a name="orderlinks"></a>OrderLinks

Siparişe karşılık gelen kaynak bağlantılarını temsil eder.

| Özellik           | Tür                                         | Açıklama                                                                   |
|--------------------|----------------------------------------------|-------------------------------------------------------------------------------|
| provisioningStatus | [Bağlantı](utility-resources.md#link)            | Doldurulduğunda, siparişin sağlama durumunu alma bağlantısı.       |
| Kendini               | [Bağlantı](utility-resources.md#link)            | Sipariş kaynağını alma bağlantısı.                                      |

## <a name="orderlineitemlinks"></a>OrderLineItemLinks

Siparişle ilişkili tam aboneliği temsil eder.

| Özellik           | Tür                                         | Açıklama                                                                          |
|--------------------|----------------------------------------------|--------------------------------------------------------------------------------------|
| provisioningStatus | [Bağlantı](utility-resources.md#link)            | Doldurulduğunda, satır öğesinin [sağlama durumunu alma](#orderlineitemprovisioningstatus) bağlantısı.       |
| Sku                | [Bağlantı](utility-resources.md#link)            | Satın alınan katalog öğesi için SKU bilgilerini alma bağlantısı.                    |
| aboneliği       | [Bağlantı](utility-resources.md#link)            | Doldurulduğunda, tam abonelik bilgilerine bağlantı.                       |
| activationLinks    | [Bağlantı](utility-resources.md#link)            | Doldurulduğunda, aboneliği etkinleştirmek için bağlantıların GET kaynağı.             |

## <a name="orderstatus"></a>OrderStatus

Siparişin durumunu belirten değerleri olan bir [Enum/dotnet/api/system.enum).

| Değer              | Konum     | Açıklama                                     |
|--------------------|--------------|-------------------------------------------------|
| Bilinmeyen            | 0            | Enum başlatıcı.                               |
| Tamamlandı          | 1            | Siparişin tamam olduğunu gösterir.          |
| bekleniyor            | 2            | Siparişin hala beklemede olduğunu gösterir.      |
| Iptal          | 3            | Siparişin iptal edildiğini gösterir.    |

## <a name="orderlineitemprovisioningstatus"></a>OrderLineItemProvisioningStatus

[OrderLineItem'ın sağlama durumunu temsil eder.](#orderlineitem)

| Özellik                        | Tür                                | Açıklama                                                                                |
|------------------------------------|-------------------------------------|--------------------------------------------------------------------------------------------|
| lineItemNumber                  | int                                 | Sipariş satırı öğesinin benzersiz satır numarası. Değerler 0 ile sayı-1 arasında değişebilir.             |
| durum                          | string                              | Sipariş satırı öğesinin sağlama durumu. Değerlere şunlar dahildir:</br>**Tamamlandı:** Siparişin yerine getirilmesi başarıyla tamamlandı ve kullanıcı rezervasyonları kullanabilir</br>**Yerine getirilmemiş:** İptal nedeniyle karşılanmaz</br>**PrefulfillmentPending:** İsteğiniz işleme devam ediyor, gerçekleştirme henüz tamamlanmadı |
| quantityProvisioningInformation | [QuantityProvisioningStatus<listele](#quantityprovisioningstatus)> | Sipariş satırı öğesi için miktar sağlama durumu bilgileri listesi. |

## <a name="quantityprovisioningstatus"></a>QuantityProvisioningStatus

Miktara göre sağlama durumunu temsil eder.

| Özellik                           | Tür                                         | Açıklama                                          |
|------------------------------------|----------------------------------------------|------------------------------------------------------|
| miktar                           | int                                          | Öğe sayısı.                                 |
| durum                             | string                                       | Öğe sayısının durumu.                   |
