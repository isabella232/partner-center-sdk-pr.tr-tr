---
title: Transferuygunluk kaynakları
description: Bir iş ortağı, bir müşteri aboneliğini başka bir ortağa aktarılacak iş ortağıyla istediğinde bir aktarım oluşturabilir.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f121d499abffb4c4dda688c2a91c25f83d2e863
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530217"
---
# <a name="transfereligibility-resources"></a>Transferuygunluk kaynakları

Bir iş ortağı, bir müşteri aboneliğini başka bir ortağa aktarılacak iş ortağıyla istediğinde bir aktarım oluşturabilir. Bir aboneliğin aktarılmasının uygun olup olmadığını denetlemek için Transferuygunluk kullanın.

## <a name="transfereligibility"></a>Transferuygunluk

Bir Transferuygunluk tanımlar.

| Özellik              | Tür             | Açıklama                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| kimlik                    | string           | Müşterinin abonelik tanımlayıcısı.                                                  |
| IBir hal            | bool             | Aboneliğin aktarım için uygun olup olmadığını gösterir.                         |
| Nedeni                | string           | Reason özelliği aboneliğin aktarım için uygun olmadığını açıklar. |