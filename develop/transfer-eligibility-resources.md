---
title: TransferEligibility kaynakları
description: Bir iş ortağı, müşteri iş ortağıyla aboneliğini başka bir iş ortağına aktarma isteğinda bulundurarak bir aktarım oluşturabilir.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ffe72aa04de17cf6e45e49e9fdbec8ba08da2deed89f5d54425a17825c91a53a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996657"
---
# <a name="transfereligibility-resources"></a>TransferEligibility kaynakları

Bir iş ortağı, müşteri iş ortağıyla aboneliğini başka bir iş ortağına aktarma isteğinda bulundurarak bir aktarım oluşturabilir. Aboneliğin aktarıla uygun olup olmadığını kontrol etmek için TransferEligibility kullanın.

## <a name="transfereligibility"></a>AktarımAtırılığı

TransferEligibility'i açıklar.

| Özellik              | Tür             | Description                                                                              |
|-----------------------|------------------|------------------------------------------------------------------------------------------|
| kimlik                    | string           | Müşterinin abonelik tanımlayıcısı.                                                  |
| isEligible            | bool             | Aboneliğin aktarım için uygun olup olmadığını gösterir.                         |
| Nedeni                | string           | neden özelliği aboneliğin aktarım için uygun olmadığını açıklar. |