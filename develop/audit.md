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
# <a name="audit-operations-available-via-partner-center-api-that-show-a-record-of-partner-center-activity"></a><span data-ttu-id="c3109-103">İş Ortağı Merkezi etkinliğinin kaydını gösteren Iş Ortağı Merkezi API 'SI aracılığıyla kullanılabilir denetim işlemleri</span><span class="sxs-lookup"><span data-stu-id="c3109-103">Audit operations available via Partner Center API that show a record of Partner Center activity</span></span>

<span data-ttu-id="c3109-104">Ortak Merkezi API 'Leri, Iş Ortağı Merkezi etkinliğinin kaydını alabilmeniz için denetim özellikleri sağlar.</span><span class="sxs-lookup"><span data-stu-id="c3109-104">The Partner Center APIs provide auditing features so you can get a record of Partner Center activity.</span></span>

<span data-ttu-id="c3109-105">Geçerli tarihten önceki 30 güne ait denetim kayıtlarını veya başlangıç tarihi ile/veya bitiş tarihi dahil ederek belirtilen bir tarih aralığını alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c3109-105">You can retrieve audit records for the previous 30 days from the current date, or for a date range specified by including the start date and/or the end date.</span></span> <span data-ttu-id="c3109-106">Bununla birlikte, performans nedenleriyle etkinlik günlüğü veri kullanılabilirliğinin önceki 90 güne sınırlı olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="c3109-106">Note, however, that for performance reasons activity log data availability is limited to the previous 90 days.</span></span> <span data-ttu-id="c3109-107">Geçerli tarihten önce 90 günden daha büyük bir başlangıç tarihi olan istekler, hatalı bir istek özel durumu (hata kodu: 400) ve uygun bir ileti alır.</span><span class="sxs-lookup"><span data-stu-id="c3109-107">Requests with a start date greater than 90 days prior to the current date will receive a bad request exception (error code: 400) and an appropriate message.</span></span>

## <a name="retrieve-audit-records"></a><span data-ttu-id="c3109-108">Denetim kayıtlarını al</span><span class="sxs-lookup"><span data-stu-id="c3109-108">Retrieve audit records</span></span>

<span data-ttu-id="c3109-109">Bir iş ortağı Kullanıcı veya uygulama tarafından gerçekleştirilen işlemlerin ayrıntılı geçmiş denetim kayıtlarını alın:</span><span class="sxs-lookup"><span data-stu-id="c3109-109">Get detailed historical audit records of operations performed by a partner user or application:</span></span>

- [<span data-ttu-id="c3109-110">İş Ortağı Merkezi etkinliğinin kaydını alma</span><span class="sxs-lookup"><span data-stu-id="c3109-110">Get a record of Partner Center activity</span></span>](get-a-record-of-partner-center-activity-by-user.md)
- [<span data-ttu-id="c3109-111">Kaynakları denetleme</span><span class="sxs-lookup"><span data-stu-id="c3109-111">Auditing resources</span></span>](auditing-resources.md)