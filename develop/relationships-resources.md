---
title: İlişkiler kaynakları
description: İlişkilerle ilgili kaynakları açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c5701414bd704b375dc23859b920609d5a975d9f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768878"
---
# <a name="relationships-resources"></a>İlişkiler kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi

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
