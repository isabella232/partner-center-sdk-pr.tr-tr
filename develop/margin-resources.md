---
title: Kenar boşluğu kaynakları
description: Kenar boşluklarını temsil eden kaynaklar. Kenar boşluklarını açıklayan kaynakları içerir.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 83ea2f95c72f4e5074e3396ef226462b5b007878
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646420"
---
# <a name="margin-resources"></a>Kenar boşluğu kaynakları

Kullanılabilir kenar boşluklarını temsil eden kaynaklar. Bir kenar boşluğunu açıklamak için kaynaklar içerir.  

Bağımsız yazılım satıcısı (ISV), belirli bulut çözümü sağlayıcıları (CSP 'Ler) için indirim veya kenar boşlukları oluşturabilir. Kenar boşluklarını temsil eden ve tanımlayan kaynaklar aşağıda verilmiştir.
                
## <a name="margin"></a>Marj                   
                        
Belirli bir CSP için kullanılabilir bir kenar boşluğunu temsil eder.
                
| Ad            | Tür            | Description                               |
|-----------------|-----------------|-------------------------------------------|
| kimlik              | string          | Kenar boşluğu için benzersiz tanımlayıcı.         |
| marginPercentage | sayı         | CSP perakende fiyatına uygulanan yüzde indirimi.  |
| productId       | string          | Kenar boşluğunun için kullanılabilir ürün KIMLIĞI.   |
| productTitle    | string          | Kenar boşluğu için kullanılabilen ürün başlığı. |
| productType     | string          | Kenar boşluğu için kullanılabilir ürün türü.   |
| publisherName   | string          | Kenar boşluğunu oluşturan ISV 'nin adı.  |
| skuId           | string          | Kenar boşluğunun için kullanılabilir SKU KIMLIĞI.  |
| skuTitle        | string          | Kenar boşluğunun için kullanılabilir olduğu SKU başlığı. |
| Başlangıç       | string          | Kenar boşluğunun başlangıç tarihi vardır. |
| endDate         | string          | Kenar boşluğunun bitiş tarihi kullanılabilir. |
| durum          | string          | Kenar boşluğunun kullanılabilir olup olmadığını gösteren durum. |
| statusDate      | string          | Durumun son güncelleştirildiği tarih. |

## <a name="definitions"></a>Tanımlar

Kenar boşluklarını açıklayan farklı yapıt türleri.                    

| Ad            | Açıklama          |
|-----------------|----------------------|
| Marj |  Tek bir kenar boşluğu tanımlar.  |    
| MarginSearchResponse |  Kenar boşluğu yanıt verilerini tanımlar.  |  
        
## <a name="related-documentation"></a>İlgili belgeler

- [Iş Ortağı Merkezi 'ne genel bakış](/partner-center/csp-commercial-marketplace-margins)
- [Market tekliflerini satın alma](/partner-center/csp-commercial-marketplace-purchase)
- [Market tekliflerini yönetme](/partner-center/csp-commercial-marketplace-manage)
- [Kenar boşluklarının bir listesini alın](get-margins.md)
- [Kenar boşluklarının bir listesini indirin](download-margins.md)
