---
title: Azure kullanım kaydı kaynakları
description: Azure kullanım kaydı, Bir Azure abonelik kaynağının kullanımıyla ilgili ayrıntıları içerir.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: eb905dd41d5ab177a29bc1bd949c5eb865e4614e204250709d91f1a31304b267
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992288"
---
# <a name="azure-utilization-record-resources"></a>Azure kullanım kaydı kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Azure kullanım kaydı, Bir Azure abonelik kaynağının kullanımıyla ilgili ayrıntıları içerir. Müşterinizin Azure abonelikleri için faturalama ilişkisine sahip olan bir bulut hizmeti sağlayıcısı iş ortağınız varsa, her faturalama döngüsünün sonunda müşterilerinize fatura göndermek için aboneliklerde tahakkuk eden kullanımı izlemek için ölçeklenebilir bir yol sağlamak üzere bu REST API'i kullanabilirsiniz.

Kullanımı izlemek ve bireysel müşterilerin aylık faturanızı ve faturalarını tahmin etmeye yardımcı olmak için, Bir Rate Card sorgusunu Azure için müşterinin kullanım kayıtlarını al isteğiyle [Microsoft Azure](get-prices-for-microsoft-azure.md) fiyatları almak için [birleştirebilirsiniz.](get-a-customer-s-utilization-record-for-azure.md)

Fiyatlar pazara ve para birimine göre farklılık gösterir ve bu API konumu dikkate alır. Varsayılan olarak API, İş Ortağı Merkezi ve tarayıcınızın dilinde iş ortağı profili ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir. Konum tanıma, özellikle de birden çok pazarda satışları tek, merkezi bir ofisten yönetirken oldukça alakalıdır.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Azure kullanım kaydı kaynağının özelliklerini açıklar.

| Özellik       | Tür                                      | Gerekli | Açıklama                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | string                                    | Yes      | Kullanım toplama zaman aralığının başlangıcı. Yanıt, tüketim zamanlarına göre gruplandı (kaynağın ne zaman kullanıldı ve fatura sistemine ne zaman raporlandığı). |
| usageEndTime   | string                                    | Yes      | Kullanım toplama zaman aralığının sonu. Yanıt, tüketim zamanlarına göre gruplandı. Başka bir ifadeyle kaynağın ne zaman kullanılmaya devam ettiği ve fatura sistemine ne zaman raporlandığı.   |
| kaynak       | object                                    | Yes      | Bir [AzureResource nesnesi](#azureresource) içerir.                                                                                                                                     |
| miktar       | sayı                                    | Yes      | [AzureResource'ta tüketilen miktar.](#azureresource)                                                                                                                           |
| unit           | dize                                    | No       | Miktar türü (saat, bayt vb.) Bu özellik isteğe bağlıdır                                                                                                                     |
| infoFields     | object                                    | Yes      | Örnek düzeyi ayrıntılarının anahtar-değer çiftleri. Bu nesne boş olabilir.                                                                                                                    |
| ınstancedata   | object                                    | No       | Örnek düzeyi ayrıntılarının anahtar-değer çiftlerini içeren [bir AzureInstanceData](#azureinstancedata) nesnesi içerir. Bu özellik isteğe bağlıdır ve dahil değildir.                  |
| öznitelikler     | [Resourceattributes](utility-resources.md#resourceattributes) | Yes      | Meta veri öznitelikleri. "objectType": "AzureUtilizationRecord" ifadesini içerir                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>AzureUtilizationRecord kaynağı üzerinde işlemler

- [Müşterinin Azure kullanım kayıtlarını alma](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Azure Kaynağının özelliklerini açıklar.

| Özellik    | Tür   | Gerekli | Açıklama                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| kimlik          | string | Yes      | Azure kaynağının benzersiz tanımlayıcısı. ResourceID veya kaynak GUID'si olarak da bilinir. |
| name        | dize | No       | Tüketilen kaynağın kolay adı. Bu özellik isteğe bağlıdır.            |
| category    | dize | No       | Tüketilen kaynağın kategorisi. Bu özellik isteğe bağlıdır.                   |
| Alt kategori | dize | No       | Tüketilen kaynağın alt kategorisi. Bu özellik isteğe bağlıdır.               |
| region      | dize | No       | Tüketilen kaynağın bölgesi. Bu özellik isteğe bağlıdır.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Azure Örnek Veri kaynağının özelliklerini açıklar.

| Özellik       | Tür             | Gerekli | Açıklama                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | string           | Yes      | Kaynak gruplarını ve örnek adını içeren tam Azure kaynak kimliği.                   |
| location       | string           | Yes      | Hizmetin çalıştırıldığı bölge.                                                                               |
| partNumber     | object           | Yes      | Ticari Market üçüncü taraf kullanımının kaynağını tanımlamak için kullanılan benzersiz ad alanı. Bu özellik boş bir dize olabilir. |
| Sipariş numarası    | sayı           | Yes      | Ticari Market için üçüncü taraf siparişi tanımlamak üzere kullanılan benzersiz ad alanı. Bu özellik boş bir dize olabilir.          |
| etiketler           | dize dizisi | No       | Kullanıcı tarafından belirtilen kaynak etiketleri. Bu özellik isteğe bağlıdır ve dahil bulunmayabilir.                            |
| additionalInfo | dize dizisi | No       | Bir Azure kaynağı için ek veriler. Bu özellik isteğe bağlıdır ve dahil bulunmayabilir.                          |