---
title: Anlaşma meta veri kaynakları
description: AgreementMetadata kaynak koleksiyonu, iş ortaklarının müşteri kabulünün onayını sağlamak için kullanabileceği anlaşma türlerini açıklar.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 36ba2aa2f78552dc9a835168b5bbd5b6a3ce47f3
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768837"
---
# <a name="agreement-metadata-resources"></a>Anlaşma meta veri kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi

**AgreementMetaData** kaynağı şu anda yalnızca *Microsoft genel bulutundaki* iş ortağı Merkezi tarafından desteklenmektedir. Bu kaynak için geçerli değildir:

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

**AgreementMetaData** koleksiyonu tüm anlaşma türleri hakkında meta veriler sağlar. İş ortakları, bu koleksiyonu müşteri anlaşmalarının kabul edilmesine yönelik onay sağlamak için kullanabilir. **AgreementMetaData** Collection, her iki anlaşma türü (**Microsoft bulut sözleşmesi** ve **Microsoft Müşteri Sözleşmesi**) için meta verileri döndürür.

## <a name="agreementmetadata"></a>AgreementMetaData

Döndürülen anlaşma meta verileri aşağıdaki özellikleri içerir:

| Özellik      | Tür               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| TemplateId    | string             | Sözleşme şablonunun benzersiz tanıtıcısı.                                       |
| tür          | string             | Anlaşma türü. Şu anda, desteklenen değerler **Microsoftcloudagreement** ve **microsoftcustomeragreement** (Önizleme) içerir. |
| agreementLink | string             | Sözleşme şablonunun URL 'SI.                                                    |
