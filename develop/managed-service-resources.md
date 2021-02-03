---
title: Yönetilen hizmet kaynakları
description: Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef644ac4d8ae9660cffc9558af33cc27832556c7
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768861"
---
# <a name="managed-service-resources"></a>Yönetilen hizmet kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.

## <a name="managedservice"></a>ManagedService

Yönetilen bir hizmeti açıklar.

| Özellik   | Tür                | Description                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | Yönetilen hizmet kimliği.                                  |
| Name       | string              | Yönetilen hizmetin adı.                         |
| Adýdýr  | string              | Hizmetin ait olduğu grubun adı.      |
| Bağlantılar      | Managedservicelmürekkepler | Yönetilen hizmete karşılık gelen kaynak bağlantıları. |
| Öznitelikler | ResourceAttributes  | Sözleşmeye karşılık gelen meta veri öznitelikleri.  |

## <a name="managedservicelinks"></a>Managedservicelmürekkepler

Hizmet desteği sağlamak için, yetkilendirilmiş yönetici izinlerine sahip ortağa izin veren bağlantıları içerir.

| Özellik      | Tür | Description                 |
|---------------|------|-----------------------------|
| AdminService  | Bağlantı | Yönetim hizmeti URI 'SI.      |
| ServiceHealth | Bağlantı | Hizmet durumu URI 'SI.     |
| ServiceTicket | Bağlantı | Hizmet bileti URI 'SI.     |
| Kendi          | Bağlantı | Self URI.               |
| Sonraki          | Bağlantı | Öğelerin sonraki sayfası.     |
| Önceki      | Bağlantı | Öğelerin önceki sayfası. |

