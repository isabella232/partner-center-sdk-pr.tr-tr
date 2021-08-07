---
title: Azure ücret kartı-geçerli Azure fiyatlandırması
description: Bölgenizdeki Azure teklifleri için gerçek zamanlı, güncel fiyatlar almak üzere Azure ücret kartı 'nın nasıl kullanılacağını öğrenin. Azure ücret kartına Iş Ortağı Merkezi REST API üzerinden erişilir.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 52b9a9bea59690a8185a381647498de69a1476b1a4d4e8d632c5d13382776114
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991234"
---
# <a name="azure-rate-card-resources-to-get-real-time-current-azure-prices-on-azure-offers-in-your-region"></a>Azure ücret kartı kaynakları, bölgenizdeki Azure tekliflerinizi gerçek zamanlı, güncel Azure fiyatlarına sahip olacak şekilde alabilir

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Azure ücret kartı, Azure teklifleri için gerçek zamanlı fiyatlar sağlar. Azure fiyatlandırması dinamik ve sık sık değişir. Microsoft, güncelleştirmeleri iş ortağı merkezi 'nde yayımlar, ancak REST API Bulut Çözümü Sağlayıcısı iş ortaklarının geçerli fiyatları alması için en hızlı yolu sağlar.

kullanımı izlemek ve aylık faturanızı ve tek tek müşterilerin ücretini tahmin etmeye yardımcı olmak için, bir ücret kartı sorgusu birleştirerek [müşterinin Azure 'a ait kullanım kayıtlarını almaya](get-a-customer-s-utilization-record-for-azure.md)yönelik bir istekle birlikte [Microsoft Azure fiyatlar alabilirsiniz](get-prices-for-microsoft-azure.md) .

Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun. Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir. Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir.

## <a name="azureratecard"></a>Azursilinebilir Tecard

Bir Azure ücret kartı kaynağının özelliklerini açıklar.

| Özellik      | Tür                                      | Description                                                       |
|---------------|-------------------------------------------|-------------------------------------------------------------------|
| currency      | string                                    | Oranların sağlandığı para birimi.                     |
| Istaxiçerilen | boolean                                   | Tüm ücretler ön vergi olduğundan bu özellik olarak döndürülür `false` . |
| locale        | string                                    | Kaynak bilgisinin yerelleştirildiği kültür.       |
| gösterilmiştir        | nesne dizisi                          | [AzureMeter](#azuremeter) nesnelerinin dizisi.                       |
| offerTerms    | nesne dizisi                          | [AzureOfferTerm](#azureofferterm) nesnelerinin dizisi.               |
| öznitelikler    | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri. Vardır `"objectType": "AzureRateCard"`   |

### <a name="operations-on-the-azureratecard-resource"></a>Azursilinebilir Tecard kaynağı üzerinde işlemler

- [Microsoft Azure için fiyat alma](get-prices-for-microsoft-azure.md)

## <a name="azuremeter"></a>AzureMeter

| Özellik         | Tür             | Description                                                                                   |
|------------------|------------------|-----------------------------------------------------------------------------------------------|
| kimlik               | string           | Ölçerin benzersiz tanımlayıcısı.                                                                    |
| name             | string           | Ölçerin kolay adı.                                                                   |
| hızını            | object           | Ölçüm oranları. Anahtar, ölçüm miktarı (dize) ve değer ölçüm oranıdır (sayı). |
| etiketler             | dize dizisi | İsteğe bağlı ölçüm etiketleri. Bu dizi boş olabilir.                                                 |
| category         | string           | Kaynağın kategorisi.                                                                     |
| alt kategori      | string           | Kaynağın alt kategorisi.                                                                 |
| region           | string           | KIMLIğIN bölgesi.                                                                             |
| unit             | string           | Miktarın türü (saat, bayt vb.)                                                     |
| includedQuantity | sayı           | Ölçüm miktarı, ücretsiz olarak dahil edilir.                                               |
| effectiveDate    | string           | Bu ölçerin geçerli olduğu tarih.                                                             |

## <a name="azureofferterm"></a>AzureOfferTerm

| Özellik         | Tür             | Description                             |
|------------------|------------------|-----------------------------------------|
| name             | string           | Teklif teriminin kolay adı.        |
| discount         | sayı           | Varsa, uygulanan indirim.           |
| excludedMeterIds | dize dizisi | Varsa, tekliften çıkarılan ölçümler. |
| effectiveDate    | string           | Teklifin etkin olduğu tarih.        |
