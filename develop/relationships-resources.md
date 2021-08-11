---
title: İlişkiler kaynakları
description: İlişkilerle ilgili kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bbbc973679ae80c3ad6b9d67945c6fbcb087789484939b67f8d8a6b538ce7d37
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997099"
---
# <a name="relationships-resources"></a>İlişkiler kaynakları

İlişkilerle ilgili kaynakları açıklar.

## <a name="partnerrelationship"></a>PartnerRelationship

İki iş ortağı arasındaki ilişkiyi temsil eder.

| Özellik         | Tür                                                           | Description                                                                                                                                    |
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

| Özellik   | Tür                                                           | Description                   |
|------------|----------------------------------------------------------------|-------------------------------|
| url        | string                                                         | İlişki isteği URL 'SI. |
| öznitelikler | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.      |
