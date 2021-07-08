---
title: Yönetilen hizmet kaynakları
description: Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 582efe75fd18a9174dd5dc173c290bee25443ee9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548133"
---
# <a name="managed-service-resources"></a>Yönetilen hizmet kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Yönetilen hizmetler, bir ortağın yönetici ayrıcalıklarına sahip olduğu hizmetlerdir. İş ortakları, yönetilen Hizmetleri adına hizmet istekleri için destek sağlayabilir.

## <a name="managedservice"></a>ManagedService

Yönetilen bir hizmeti açıklar.

| Özellik   | Tür                | Açıklama                                              |
|------------|---------------------|----------------------------------------------------------|
| Id         | string              | Yönetilen hizmet KIMLIĞI.                                  |
| Name       | string              | Yönetilen hizmetin adı.                         |
| Adýdýr  | string              | Hizmetin ait olduğu grubun adı.      |
| Bağlantılar      | Managedservicelmürekkepler | Yönetilen hizmete karşılık gelen kaynak bağlantıları. |
| Öznitelikler | ResourceAttributes  | Sözleşmeye karşılık gelen meta veri öznitelikleri.  |

## <a name="managedservicelinks"></a>Managedservicelmürekkepler

Hizmet desteği sağlamak için, yetkilendirilmiş yönetici izinlerine sahip ortağa izin veren bağlantıları içerir.

| Özellik      | Tür | Açıklama                 |
|---------------|------|-----------------------------|
| AdminService  | Bağlantı | Yönetim hizmeti URI 'SI.      |
| ServiceHealth | Bağlantı | Hizmet durumu URI 'SI.     |
| ServiceTicket | Bağlantı | Hizmet bileti URI 'SI.     |
| Kendi          | Bağlantı | Self-URI.               |
| Sonraki          | Bağlantı | Öğelerin sonraki sayfası.     |
| Önceki      | Bağlantı | Öğelerin önceki sayfası. |

