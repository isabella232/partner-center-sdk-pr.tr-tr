---
title: Anlaşma belgesi kaynakları
description: AgreementDocument kaynağı, önizleme ve indirme için bir Microsoft sözleşmesi belgesidir. Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenir.
ms.date: 08/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: eddde1e8072c6aeeee814b52f46c7648d870b6ba63c09b20e4270b17f8386383
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991115"
---
# <a name="agreement-document-resources-supported-by-partner-center-in-the-microsoft-public-cloud"></a>Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenen anlaşma belgesi kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi

**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

**AgreementDocument** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.

**AgreementDocument** kaynağı, önizleme ve indirme için kullanılabilen bir Microsoft sözleşmesi belgesini temsil eder.

## <a name="agreementdocument"></a>AgreementDocument

Bir **AgreementDocument** kaynağı aşağıdaki özellikleri içerir:

| Özellik       | Tür   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| ülke | string | Bu belgenin geçerli olduğu ülke veya Pazar. |
| language | string | Bu belgenin yerelleştirildiği dil. |
| displayUri | string | Bir tarayıcıda anlaşma belgesini önizlemek için bir bağlantı.  |
| downloadUri |string | anlaşma belgesini indirmek için bir bağlantı (Microsoft Word biçimde). |
