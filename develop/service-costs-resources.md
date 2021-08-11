---
title: Hizmet maliyetleri kaynakları
description: Bir müşteri tarafından satın alınan hizmetlerle ilgili kaynakları açıklar.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c1e3a05be89eee12d708a3a37e008ec7fa42358eaec7e1f020aaa47e44b452c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996147"
---
# <a name="service-costs-resources"></a>Hizmet maliyetleri kaynakları

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
> Aşağıdaki özellikler yalnızca ürünün *bir kerelik satın alma* işlemi olduğu servis maliyeti satırı öğeleri *için geçerlidir* : **ProductID**, **ProductName**, **skuid**, **skuname**, **kullanılabilirliği bilityıd**, **publisherID**, **PublisherName**, **terdibillingcycle**, **decountdetails**. Bu özellikler, ürünün *yinelenen satın alma* işlemi olduğu hizmet satırı öğeleri *için uygulanmaz* . örneğin, bu özellikler abonelik tabanlı Office 365 ve Azure için *geçerlidir* .

| Özellik                 | Tür                           | Description                                                          |
|--------------------------|--------------------------------|----------------------------------------------------------------------|
| Başlangıç                | UTC Tarih-saat biçiminde dize | Ücret için başlangıç tarihi.                                       |
| endDate                  | UTC Tarih-saat biçiminde dize | Ücretin bitiş tarihi.                                         |
| subscriptionFriendlyName | string                         | Aboneliğin kolay adı.                              |
| subscriptionId           | string                         | Abonelik tanımlayıcısı.                                         |
| Sipariş                  | string                         | Sıra tanımlayıcısı.                                                |
| OfferId                  | string                         | Teklif tanımlayıcısı.                                                |
| offerName                | string                         | Teklif adı.                                                      |
| Resellermpnıd            | string                         | Yalnızca iki katmanlı iş ortağı senaryolarında kullanılır. MPN tanımlayıcısını ifade eder. |
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

| Özellik             | Tür                               | Description                         |
|----------------------|------------------------------------|-------------------------------------|
| serviceCostLineItems | [Bağlantı](utility-resources.md#link) | Satır öğelerini almak için URI. |
| Kendini                 | [Bağlantı](utility-resources.md#link) | Kendi kendine URI.                       |
