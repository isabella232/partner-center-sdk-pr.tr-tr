---
title: Anlaşma meta veri kaynakları
description: AgreementMetadata kaynak koleksiyonu, iş ortaklarının müşteri kabulünün onayını sağlamak için kullanabileceği anlaşma türlerini açıklar.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 7c09dc2a8dd88e3d3a6a7925f6f61737cbbd410eabda6ecb4c3ead13d889de04
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991268"
---
# <a name="agreement-metadata-resources"></a>Anlaşma meta veri kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi

**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

**AgreementMetaData** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir. 

**AgreementMetaData** koleksiyonu tüm anlaşma türleri hakkında meta veriler sağlar. İş ortakları, bu koleksiyonu müşteri anlaşmalarının kabul edilmesine yönelik onay sağlamak için kullanabilir. **AgreementMetaData** Collection, her iki anlaşma türü (**Microsoft bulut sözleşmesi** ve **Microsoft Müşteri Sözleşmesi**) için meta verileri döndürür.

## <a name="agreementmetadata"></a>AgreementMetaData

Döndürülen anlaşma meta verileri aşağıdaki özellikleri içerir:

| Özellik      | Tür               | Description                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| TemplateId    | string             | Sözleşme şablonunun benzersiz tanıtıcısı.                                       |
| tür          | string             | Anlaşma türü. Şu anda, desteklenen değerler **Microsoftcloudagreement** ve **microsoftcustomeragreement** (Önizleme) içerir. |
| agreementLink | string             | Sözleşme şablonunun URL 'SI.                                                    |
