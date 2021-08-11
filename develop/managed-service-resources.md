---
title: Yönetilen hizmet kaynakları
description: Yönetilen hizmetler, iş ortağının yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen hizmetleri adına ve dosya hizmeti istekleri için destek sağlar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 066c9f2a0d5ca8d03553508c2b471ca49735406a5a0566bf48b0773385c129f7
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994396"
---
# <a name="managed-service-resources"></a>Yönetilen hizmet kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Yönetilen hizmetler, iş ortağının yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen hizmetleri adına ve dosya hizmeti istekleri için destek sağlar.

## <a name="managedservice"></a>ManagedService

Yönetilen bir hizmeti açıklar.

| Özellik   | Tür                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | Yönetilen hizmet kimliği.                                  |
| Name       | string              | Yönetilen hizmetin adı.                         |
| GroupName  | string              | Hizmetin ait olduğu grubun adı.      |
| Bağlantılar      | ManagedServiceLinks | Yönetilen hizmete karşılık gelen kaynak bağlantıları. |
| Öznitelikler | Resourceattributes  | Sözleşmeye karşılık gelen meta veri öznitelikleri.  |

## <a name="managedservicelinks"></a>ManagedServiceLinks

Yönetici temsilcisi izinlerine sahip iş ortağının hizmet için destek sağlamasını sağlayan bağlantıları içerir.

| Özellik      | Tür | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Bağlantı | Yönetici hizmeti URI'si.      |
| ServiceHealth | Bağlantı | Hizmet durumu URI'si.     |
| ServiceTicket | Bağlantı | Hizmet bileti URI'sı.     |
| Kendi          | Bağlantı | Kendi kendine URI.               |
| Sonraki          | Bağlantı | Öğelerin sonraki sayfası.     |
| Önceki      | Bağlantı | Öğelerin önceki sayfası. |

