---
title: Anlaşma belgesi kaynakları
description: AgreementDocument kaynağı, önizleme ve indirme için bir Microsoft sözleşmesi belgesidir. Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenir.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 4805d25b0838bf922b81bebd998810c3f6a809c3
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770030"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenen anlaşma belgesi kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi

**AgreementDocument** kaynağı şu anda yalnızca *Microsoft genel bulutundaki* iş ortağı Merkezi tarafından desteklenmektedir. Bu kaynak için geçerli değildir:

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

**AgreementDocument** kaynağı, önizleme ve indirme için kullanılabilen bir Microsoft sözleşmesi belgesini temsil eder.

## <a name="agreementdocument"></a>AgreementDocument

Bir **AgreementDocument** kaynağı aşağıdaki özellikleri içerir:

| Özellik       | Tür   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| ülke | string | Bu belgenin geçerli olduğu ülke veya Pazar. |
| language | string | Bu belgenin yerelleştirildiği dil. |
| displayUri | string | Bir tarayıcıda anlaşma belgesini önizlemek için bir bağlantı.  |
| downloadUri |string | Sözleşme belgesini indirmek için bir bağlantı (Microsoft Word biçiminde). |
