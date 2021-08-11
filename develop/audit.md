---
title: Iş Ortağı Merkezi etkinliğinin denetim işlemleri
description: Iş Ortağı Merkezi etkinliğinin kaydını almak için kullanabileceğiniz Iş Ortağı Merkezi API 'SI denetim işlemlerinin türü hakkında bilgi edinin.
ms.date: 05/21/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0e8010bde75bee4c4954034d8f61f19b076d96349e4a05807e272ca88efbc2fa
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994277"
---
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a>İş Ortağı Merkezi etkinliğinin kaydını gösteren Iş Ortağı Merkezi API 'SI aracılığıyla kullanılabilir denetim işlemleri

Ortak Merkezi API 'Leri, Iş Ortağı Merkezi etkinliğinin kaydını alabilmeniz için denetim özellikleri sağlar.

Geçerli tarihten önceki 30 güne ait denetim kayıtlarını veya başlangıç tarihi ile/veya bitiş tarihi dahil ederek belirtilen bir tarih aralığını alabilirsiniz. Bununla birlikte, performans nedenleriyle etkinlik günlüğü veri kullanılabilirliğinin önceki 90 güne sınırlı olduğunu unutmayın. Geçerli tarihten önce 90 günden daha büyük bir başlangıç tarihi olan istekler, hatalı bir istek özel durumu (hata kodu: 400) ve uygun bir ileti alır.

## <a name="retrieve-audit-records"></a>Denetim kayıtlarını al

Bir iş ortağı Kullanıcı veya uygulama tarafından gerçekleştirilen işlemlerin ayrıntılı geçmiş denetim kayıtlarını alın:

- [İş Ortağı Merkezi etkinliğinin kaydını alma](get-a-record-of-partner-center-activity-by-user.md)
- [Kaynakları denetleme](auditing-resources.md)