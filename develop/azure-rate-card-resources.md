---
title: Azure fiyat kartı - geçerli Azure fiyatlandırması
description: Bölgenize uygun Azure tekliflerini gerçek zamanlı ve güncel fiyatlara almak için Azure Rate Card'ın nasıl kullanılası hakkında bilgi edinin. Azure Rate Card'a İş Ortağı Merkezi REST API.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e0b1bc9d764e2132315205653f46cef73b25e02f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974344"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Bölgenize göre Azure tekliflerini gerçek zamanlı ve geçerli Azure fiyatlarına almak için Azure fiyat kartı kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Azure Rate Card, Azure teklifleri için gerçek zamanlı fiyatlar sağlar. Azure fiyatlandırması dinamiktir ve sık sık değişir. Microsoft güncelleştirmeleri İş Ortağı Merkezi yayımlar ancak REST API iş ortaklarının geçerli fiyatları Bulut Çözümü Sağlayıcısı için en hızlı yolu sağlar.

Kullanımı izlemek ve bireysel müşterilerin aylık faturanızı ve faturalarını tahmin etmeye yardımcı olmak için, Bir Rate Card sorgusunu Azure için müşterinin kullanım kayıtlarını al isteğiyle [Microsoft Azure](get-prices-for-microsoft-azure.md) fiyatları almak için [birleştirebilirsiniz.](get-a-customer-s-utilization-record-for-azure.md)

Fiyatlar pazara ve para birimine göre farklılık gösterir ve bu API konumu dikkate alır. Varsayılan olarak API, İş Ortağı Merkezi ve tarayıcınızın dilinde iş ortağı profili ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir. Konum tanıma, özellikle de birden çok pazarda satışları tek, merkezi bir ofisten yönetirken oldukça alakalıdır.

## <a name="azureratecard"></a>AzureRateCard

Azure Rate Card kaynağının özelliklerini açıklar.

| Özellik      | Tür                                      | Açıklama                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | string                                    | Oranların sağlanmıştır para birimi.                     |
| isTaxIncluded | boolean                                   | Tüm fiyatlar vergi öncesidir, bu nedenle bu özellik olarak `false` döndürür. |
| locale        | string                                    | Kaynak bilgisinin yerelleştirilmiş olduğu kültür.       |
| Metre        | nesne dizisi                          | [AzureMeter nesneleri](#azuremeter) dizisi.                       |
| offerTerms    | nesne dizisi                          | [AzureOfferTerm nesneleri](#azureofferterm) dizisi.               |
| öznitelikler    | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. Içerir `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>AzureRateCard kaynağında işlemler

- [Microsoft Azure için fiyat alma](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Özellik         | Tür             | Açıklama                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| kimlik               | string           | Ölçümün benzersiz tanımlayıcısı.                                                                    |
| name             | string           | Ölçümün kolay adı.                                                                   |
| Oran -ları            | object           | Ölçüm oranları. Anahtar, ölçüm miktarıdır (dize) ve değer de ölçüm oranıdır (sayı). |
| etiketler             | dize dizisi | İsteğe bağlı ölçüm etiketleri. Bu dizi boş olabilir.                                                 |
| category         | string           | Kaynağın kategorisi.                                                                     |
| Alt kategori      | string           | Kaynağın alt kategorisi.                                                                 |
| region           | string           | Kimliğin bölgesi.                                                                             |
| unit             | string           | Miktar türü (saat, bayt vb.)                                                     |
| includedQuantity | sayı           | Ücretsiz olarak dahil edilen ölçüm miktarı.                                               |
| effectiveDate    | string           | Bu ölçümün etkili olduğu tarih.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Özellik         | Tür             | Açıklama                             |
|------------------|------------------|-----------------------------------------|
| name             | string           | Teklif teriminin kolay adı.        |
| discount         | sayı           | Varsa uygulanan indirim.           |
| excludedMeterIds | dize dizisi | Varsa, tekliften hariç bırakılan metreler. |
| effectiveDate    | string           | Teklifin etkili olduğu tarih.        |
