---
title: İlişkiler kaynakları
description: İlişkilerle ilgili kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dba1e99a6c97c759e3c61cde1e7565faa2ef4d1
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445740"
---
# <a name="relationships-resources"></a>İlişkiler kaynakları

İlişkilerle ilgili kaynakları açıklar.

## <a name="partnerrelationship"></a>PartnerRelationship

İki iş ortağı arasındaki ilişkiyi temsil eder.

| Özellik         | Tür                                                           | Açıklama                                                                                                                                    |
|------------------|----------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik               | string                                                         | İş ortağı tanımlayıcısı. İş ortağı tanımlayıcısı, ilişkinin alıcı (Kimden) tarafında olan iş ortağının Kiracı kimliğini belirtir. |
| location         | string                                                         | İş ortağının konumu.                                                                                                                   |
| Mpnıd            | string                                                         | Ortağın Microsoft İş Ortağı Ağı (MPN) tanımlayıcısı.                                                                                 |
| name             | string                                                         | Ortağın adı.                                                                                                                       |
| relationshipType | string                                                         | İlişki türü.                                                                                                                      |
| state            | string                                                         | İlişkinin durumu (örneğin `active` ).                                                                                                 |
| öznitelikler       | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                                                                                       |

## <a name="relationshiprequest"></a>RelationshipRequest

Müşterinin bir iş ortağıyla ilişki kurabilbileceği URL 'YI sağlar.

| Özellik   | Tür                                                           | Açıklama                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | İlişki isteği URL 'SI. |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.      |
