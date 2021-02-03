---
title: Azure kullanım kaydı kaynakları
description: Azure kullanım kaydı, bir Azure aboneliği kaynağının kullanımı hakkındaki ayrıntıları içerir.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 21d39c4497c00f5abeeeb771dfe20cd1e2b1c13a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768831"
---
# <a name="azure-utilization-record-resources"></a>Azure kullanım kaydı kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Azure kullanım kaydı, bir Azure aboneliği kaynağının kullanımı hakkındaki ayrıntıları içerir. Müşterilerinizin Azure aboneliklerine ait faturalandırma ilişkisine sahip olan bir bulut hizmeti sağlayıcısı iş ortağıysanız, her faturalandırma döngüsünün sonunda müşterilerinize fatura göndermek için aboneliklerde oluşan kullanımı izlemenin ölçeklenebilir bir yolunu sağlamak üzere bu REST API kullanabilirsiniz.

Kullanımı izlemek ve aylık faturanızı ve tek tek müşterilerin ücretini tahmin etmeye yardımcı olmak için, bir ücret kartı sorgusu birleştirerek [müşterinin Azure 'a ait kullanım kayıtlarını almaya](get-a-customer-s-utilization-record-for-azure.md)yönelik bir istekle birlikte [Microsoft Azure fiyatlar alabilirsiniz](get-prices-for-microsoft-azure.md) .

Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun. Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir. Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir.

## <a name="azureutilizationrecord"></a>AzureUtilizationRecord

Bir Azure kullanım kaydı kaynağının özelliklerini açıklar.

| Özellik       | Tür                                      | Gerekli | Açıklama                                                                                                                                                                             |
|----------------|-------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageStartTime | string                                    | Yes      | Kullanım toplama zaman aralığının başlangıcı. Yanıt, tüketim zamanına göre gruplandırılır (kaynak gerçekten kullanıldığında, faturalandırma sistemine raporlandığı zaman). |
| Usagebitişsaati   | string                                    | Yes      | Kullanım toplama zaman aralığının sonu. Yanıt, tüketim zamanına göre gruplandırılır. Diğer bir deyişle, kaynak gerçekten ne zaman ve faturalama sistemine bildirilmediği.   |
| kaynak       | object                                    | Yes      | Bir [AzureResource](#azureresource) nesnesi içerir.                                                                                                                                     |
| miktar       | sayı                                    | Yes      | AzureResource tüketilen miktar [.](#azureresource)                                                                                                                           |
| unit           | dize                                    | No       | Miktarın türü (saat, bayt vb.) Bu özellik isteğe bağlıdır                                                                                                                     |
| Çocuk bağlantıları     | object                                    | Yes      | Örnek düzeyi ayrıntılarının anahtar-değer çiftleri. Bu nesne boş olabilir.                                                                                                                    |
| InstanceData   | object                                    | No       | Örnek düzeyi ayrıntılarının anahtar-değer çiftlerini içeren bir [AzureInstanceData](#azureinstancedata) nesnesi içerir. Bu özellik isteğe bağlıdır ve dahil bulunmayabilir.                  |
| öznitelikler     | [ResourceAttributes](utility-resources.md#resourceattributes) | Yes      | Meta veri öznitelikleri. "ObjectType" içerir: "AzureUtilizationRecord"                                                                                                                |

### <a name="operations-on-the-azureutilizationrecord-resource"></a>AzureUtilizationRecord kaynaktaki işlemler

- [Müşterinin Azure kullanım kayıtlarını alma](get-a-customer-s-utilization-record-for-azure.md)

## <a name="azureresource"></a>AzureResource

Bir Azure kaynağının özelliklerini açıklar.

| Özellik    | Tür   | Gerekli | Açıklama                                                                         |
|-------------|--------|----------|-------------------------------------------------------------------------------------|
| kimlik          | string | Yes      | Azure kaynağının benzersiz tanıtıcısı. RESOURCEID veya kaynak GUID 'SI olarak da bilinir. |
| name        | dize | No       | Tüketilmekte olan kaynağın kolay adı. Bu özellik isteğe bağlıdır.            |
| category    | dize | No       | Tüketilen kaynağın kategorisi. Bu özellik isteğe bağlıdır.                   |
| alt kategori | dize | No       | Tüketilen kaynağın alt kategorisi. Bu özellik isteğe bağlıdır.               |
| region      | dize | No       | Tüketilen kaynağın bölgesi. Bu özellik isteğe bağlıdır.                     |

## <a name="azureinstancedata"></a>AzureInstanceData

Azure örnek veri kaynağının özelliklerini açıklar.

| Özellik       | Tür             | Gerekli | Açıklama                                                                                                        |
|----------------|------------------|----------|--------------------------------------------------------------------------------------------------------------------|
| resourceUri    | string           | Yes      | Kaynak grupları ve örnek adı da dahil olmak üzere tam Azure Kaynak KIMLIĞI.                   |
| location       | string           | Yes      | Hizmetin çalıştırıldığı bölge.                                                                               |
| partNumber     | object           | Yes      | Ticari Market üçüncü taraf kullanımının kaynağını tanımlamak için kullanılan benzersiz ad alanı. Bu özellik boş bir dize olabilir. |
| Sipariş numarası    | sayı           | Yes      | Ticari Market için üçüncü taraf siparişi tanımlamak üzere kullanılan benzersiz ad alanı. Bu özellik boş bir dize olabilir.          |
| tags           | dize dizisi | No       | Kullanıcı tarafından belirtilen kaynak etiketleri. Bu özellik isteğe bağlıdır ve dahil bulunmayabilir.                            |
| additionalInfo | dize dizisi | No       | Bir Azure kaynağı için ek veriler. Bu özellik isteğe bağlıdır ve dahil bulunmayabilir.                          |