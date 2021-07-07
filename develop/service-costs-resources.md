---
title: Hizmet maliyetleri kaynakları
description: Müşteri tarafından satın alınan hizmetlerle ilgili kaynakları açıklar.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dbddc1973dd9a904cedd549c1772cd4c74c69a60
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547419"
---
# <a name="service-costs-resources"></a>Hizmet maliyetleri kaynakları

Müşteri tarafından satın alınan hizmetlerle ilgili kaynakları açıklar.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**ServiceCostsSummary,** faturalama döneminde belirtilen müşteri tarafından satın alınan tüm hizmetleri toplanmış bir özet içerir.

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| Şey | [ServiceCostsSummaryDetail nesneleri](#servicecostssummarydetail) dizisi | Fatura türüne göre ayırt edilen hizmet maliyeti özeti ayrıntı listesi.|
| Bağlantı | [ResourceLinks](utility-resources.md#resourcelinks) | Kaynak bağlantıları. |
| öznitelikler | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. |

> [!IMPORTANT]
> **Aşağıdaki tablodaki alanlar kullanım dışıdır.** Yinelenen ve tek kullanımlık hizmet maliyeti özetlerini almak için ayrıntılar **alanını** kullanın. Ayrıntılar  alanı önceki tabloda açıklanmıştır. Ayrıntılar alanına **karşılık** gelen veri değerlerine bakın, ancak kök düzeyindeki alanlara bakın.

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| billingStartDate | date | Faturalama döneminin başlangıcı. |
| billingEndDate | date | Faturalama döneminin sonu. |
| pretaxTotal | double | Müşterinin tüm maliyetlerinin vergi öncesi toplamı. |
| Vergi  | double | Müşteri tarafından satın alınan tüm öğeler için tahakkuk eden toplam vergi. |
| afterTaxTotal | double | Müşteri tarafından satın alınan tüm öğelerin net toplam maliyeti. |
| currencyCode | string | Maliyetler için kullanılan para birimini temsil eder. |
| Currencysymbol | string | Maliyetler için kullanılan para birimi simgesi. |
| customerId | string | Satın alma yapan müşterinin kimliği. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail,** faturalama döneminde (yinelenen veya bir defalık faturalardan) belirtilen müşteri tarafından satın alınan tüm hizmetleri toplayan bir hizmet maliyeti özetini açıklar.

| Özellik | Tür | Açıklama |
| -------- | ---- | ----------- |
| invoiceType | string | Hizmet maliyeti özetini oluşturan invoiceType. |
| Özet | [ServiceCostsSummary](#servicecostssummary) | Müşteri tarafından tek bir fatura türü altında toplanan hizmet maliyeti özeti. |

## <a name="servicecostlineitem"></a>ServiceCostLineItem

**ServiceCostLineItem,** müşteri tarafından satın alınan tek bir öğeyi açıklar.

> [!IMPORTANT]
> Aşağıdaki özellikler *yalnızca ürünün* tek kullanımlık satın alma olduğu hizmet maliyeti satır öğeleri için geçerlidir: **productId**, **productName**, **skuId , skuName**, **availabilityId**, **publisherId**, **publisherName**, **termAndBillingCycle**, **discountDetails**.   Bu *özellikler, ürünün yinelenen bir* satın alma olduğu hizmet satırı öğeleri *için geçerli değildir.* Örneğin, bu özellikler *abonelik tabanlı abonelikler* ve Azure Office 365 geçerli değildir.

| Özellik                 | Tür                           | Açıklama                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| Startdate                | UTC tarih-saat biçiminde dize | Ücretin başlangıç tarihi.                                       |
| Bitiştarihi                  | UTC tarih-saat biçiminde dize | Ücretin bitiş tarihi.                                         |
| subscriptionFriendlyName | string                         | Aboneliğin kolay adı.                              |
| subscriptionId           | string                         | Abonelik tanımlayıcısı.                                         |
| Siparişno                  | string                         | Sipariş tanımlayıcısı.                                                |
| offerId                  | string                         | Teklif tanımlayıcısı.                                                |
| offerName                | string                         | Teklif adı.                                                      |
| resellerMPNId            | string                         | Yalnızca iki katmanlı iş ortağı senaryolarında kullanılır. MPN tanımlayıcısına başvurur. |
| chargeType               | string                         | İlişkili ücret türü.                                          |
| miktar                 | sayı                         | Kullanılan veya satın alınan birim miktarı.                             |
| unitPrice                | sayı                         | Birim başına fiyat.                                                  |
| pretaxTotal              | sayı                         | Vergilerden önce bu öğenin toplam ücreti.                         |
| Vergi                      | sayı                         | Bu öğe için tahakkuk eden toplam vergi ücreti.                         |
| afterTaxTotal            | sayı                         | Bu öğenin net toplam maliyeti.                                    |
| currencyCode             | string                         | Maliyetler için kullanılan para birimini temsil eder.                          |
| Currencysymbol           | string                         | Maliyetler için kullanılan para birimi simgesi.                              |
| customerId               | string                         | Satın alma yapan müşterinin kimliği.                          |
| Müşteriadı             | string                         | Satın alma yapan müşterinin adı.                        |
| invoiceNumber            | string                         | Bu satır öğesinin ait olduğu fatura numarası.                   |
| productId                | string                         | Ürün tanımlayıcısı.                                              |
| skuId                    | string                         | Sku tanımlayıcısı.                                                  |
| availabilityId           | string                         | Kullanılabilirlik tanımlayıcısı.                                         |
| Productname              | string                         | Ürün adı.                                                    |
| skuName                  | string                         | SKU adı.                                                        |
| publisherName            | string                         | Yayımcı adı.                                                  |
| publisherId              | string                         | Yayımcı tanımlayıcısı.                                            |
| termAndBillingCycle      | string                         | Terim ve faturalama döngüsü.                                          |
| discountDetails          | string                         | İndirim ayrıntıları.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Özellik             | Tür                               | Açıklama                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Bağlantı](utility-resources.md#link) | Satır öğelerini almak için URI. |
| Kendini                 | [Bağlantı](utility-resources.md#link) | Kendi kendine URI.                       |
