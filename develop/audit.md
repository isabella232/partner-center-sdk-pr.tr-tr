---
title: Iş Ortağı Merkezi etkinliğinin denetim işlemleri
description: Iş Ortağı Merkezi etkinliğinin kaydını almak için kullanabileceğiniz Iş Ortağı Merkezi API 'SI denetim işlemlerinin türü hakkında bilgi edinin.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 019bebe40c43f6ee1c2ac7da381a86ca190702d4
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97769994"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>İş Ortağı Merkezi etkinliğinin kaydını gösteren Iş Ortağı Merkezi API 'SI aracılığıyla kullanılabilir denetim işlemleri

Ortak Merkezi API 'Leri, Iş Ortağı Merkezi etkinliğinin kaydını alabilmeniz için denetim özellikleri sağlar.

Geçerli tarihten önceki 30 güne ait denetim kayıtlarını veya başlangıç tarihi ile/veya bitiş tarihi dahil ederek belirtilen bir tarih aralığını alabilirsiniz. Bununla birlikte, performans nedenleriyle etkinlik günlüğü veri kullanılabilirliğinin önceki 90 güne sınırlı olduğunu unutmayın. Geçerli tarihten önce 90 günden daha büyük bir başlangıç tarihi olan istekler, hatalı bir istek özel durumu (hata kodu: 400) ve uygun bir ileti alır.

## <a name="retrieve-audit-records"></a>Denetim kayıtlarını al

Bir iş ortağı Kullanıcı veya uygulama tarafından gerçekleştirilen işlemlerin ayrıntılı geçmiş denetim kayıtlarını alın:

- [İş Ortağı Merkezi etkinliğinin kaydını alma](get-a-record-of-partner-center-activity-by-user.md)
- [Kaynakları denetleme](auditing-resources.md)