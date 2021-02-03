---
title: Hizmet maliyetleri kaynakları
description: Bir müşteri tarafından satın alınan hizmetlerle ilgili kaynakları açıklar.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c0236329d93d8ddc9019a15fb67a81a3af3e7620
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769197"
---
# <a name="service-costs-resources"></a>Hizmet maliyetleri kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi

Bir müşteri tarafından satın alınan hizmetlerle ilgili kaynakları açıklar.

## <a name="servicecostssummary"></a>ServiceCostsSummary

**Servicecostssummary** , fatura dönemi boyunca belirtilen müşteri tarafından satın alınan tüm hizmetleri toplayan bir Özet içerir.

| Özellik | Tür | Description |
| -------- | ---- | ----------- |
| bilgileri | [ServiceCostsSummaryDetail](#servicecostssummarydetail) nesneleri dizisi | Fatura tipine göre ayırt edilen hizmet maliyeti Özet ayrıntısı listesi.|
| Köprü | [Resourcelmürekkepler](utility-resources.md#resourcelinks) | Kaynak bağlantıları. |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. |

> [!IMPORTANT]
> **Aşağıdaki tabloda yer alan alanlar kullanım dışı bırakılmıştır.** Yinelenen ve tek seferlik hizmet maliyeti özetlerini almak için, bunun yerine **Ayrıntılar** alanını kullanın. **Ayrıntılar** alanı önceki tabloda açıklanmıştır. **Ayrıntılar** alanının karşılık gelen veri değerlerine bakın, ancak kök düzeyi alanları değildir.

| Özellik | Tür | Description |
| -------- | ---- | ----------- |
| billingStartDate | date | Fatura döneminin başlangıcı. |
| billingEndDate | date | Fatura döneminin sonu. |
| pretaxTotal | double | Müşterinin tüm maliyetlerinin ön vergi toplamı. |
| VERG  | double | Müşteri tarafından satın alınan tüm öğeler üzerinde tahakkuk eden toplam vergi. |
| afterTaxTotal | double | Müşteri tarafından satın alınan tüm öğelerin net toplam maliyeti. |
| currencyCode | string | Maliyetler için kullanılan para birimini temsil eder. |
| currencySymbol | string | Maliyetler için kullanılan para birimi simgesi. |
| customerId | string | Satın alma yapan müşterinin KIMLIĞI. |

## <a name="servicecostssummarydetail"></a>ServiceCostsSummaryDetail

**ServiceCostsSummaryDetail** , fatura dönemi (yinelenen veya tek seferlik faturalardan) sırasında belirtilen müşteri tarafından satın alınan tüm hizmetleri toplayan bir servis maliyeti Özeti açıklar.

| Özellik | Tür | Description |
| -------- | ---- | ----------- |
| Faturano Etype | string | Faturaya ait hizmet maliyeti Özeti oluşturulmuştur. |
| Özet | [ServiceCostsSummary](#servicecostssummary) | Bir müşteri tarafından bir fatura türü altında toplanan hizmet maliyet özeti. |

## <a name="servicecostlineitem"></a>Servicecostlineıtem

**Servicecostlineıtem** , müşteri tarafından satın alınan tek bir öğeyi açıklar.

> [!IMPORTANT]
> Aşağıdaki özellikler yalnızca ürünün *bir kerelik satın alma* işlemi olduğu servis maliyeti satırı öğeleri *için geçerlidir* : **ProductID**, **ProductName**, **skuid**, **skuname**, **kullanılabilirliği bilityıd**, **publisherID**, **PublisherName**, **terdibillingcycle**, **decountdetails**. Bu özellikler, ürünün *yinelenen satın alma* işlemi olduğu hizmet satırı öğeleri *için uygulanmaz* . Örneğin, bu özellikler abonelik tabanlı Office 365 ve Azure için *geçerlidir* .

| Özellik                 | Tür                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| Başlangıç                | UTC Tarih-saat biçiminde dize | Ücret için başlangıç tarihi.                                       |
| endDate                  | UTC Tarih-saat biçiminde dize | Ücretin bitiş tarihi.                                         |
| subscriptionFriendlyName | string                         | Aboneliğin kolay adı.                              |
| subscriptionId           | string                         | Abonelik tanımlayıcısı.                                         |
| Sipariş                  | string                         | Sıra tanımlayıcısı.                                                |
| OfferId                  | string                         | Teklif tanımlayıcısı.                                                |
| offerName                | string                         | Teklif adı.                                                      |
| Resellermpnıd            | string                         | Yalnızca 2 katmanlı iş ortağı senaryolarında kullanılır. MPN tanımlayıcısını ifade eder. |
| chargeType               | string                         | İlişkili ücret türü.                                          |
| miktar                 | sayı                         | Kullanılan veya satın alınan birim miktarı.                             |
| unitPrice                | sayı                         | Birim başına fiyat.                                                  |
| pretaxTotal              | sayı                         | Bu öğe için vergi öncesi toplam ücret.                         |
| VERG                      | sayı                         | Bu öğe için tahakkuk eden toplam vergi ücreti.                         |
| afterTaxTotal            | sayı                         | Bu öğe için net toplam maliyet.                                    |
| currencyCode             | string                         | Maliyetler için kullanılan para birimini temsil eder.                          |
| currencySymbol           | string                         | Maliyetler için kullanılan para birimi simgesi.                              |
| customerId               | string                         | Satın alma yapan müşterinin KIMLIĞI.                          |
| customerName             | string                         | Satın alma yapan müşterinin adı.                        |
| Faturanumarası            | string                         | Bu satır öğesinin ait olduğu fatura numarası.                   |
| productId                | string                         | Ürün tanımlayıcısı.                                              |
| skuId                    | string                         | SKU tanımlayıcısı.                                                  |
| Kullanılabilirlik kimliği           | string                         | Kullanılabilirlik tanımlayıcısı.                                         |
| productName              | string                         | Ürün adı.                                                    |
| skuName                  | string                         | SKU adı.                                                        |
| publisherName            | string                         | Yayımcı adı.                                                  |
| PublisherId              | string                         | Yayımcı tanımlayıcısı.                                            |
| Tertermbillingcycle      | string                         | Terim ve fatura dönemi.                                          |
| discountDetails          | string                         | İndirim ayrıntıları.                                                |

## <a name="servicecostssummarylinks"></a>ServiceCostsSummaryLinks

| Özellik             | Tür                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| Servicecostlineıtems | [Bağlantı](utility-resources.md#link) | Satır öğelerinin alınması için URI. |
| Self                 | [Bağlantı](utility-resources.md#link) | Self URI.                       |
