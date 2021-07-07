---
title: Sözleşme meta veri kaynakları
description: AgreementMetadata kaynak koleksiyonu, iş ortaklarının müşteri kabulünü onaylaması için kullanabileceği sözleşme türlerini açıklar.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: b930e3691b9d269ddb8d76ae18b6b26a217123c0
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025641"
---
# <a name="agreement-metadata-resources"></a>Sözleşme meta veri kaynakları

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

**AgreementMetaData** kaynağı şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde kullanılabilir. 

**AgreementMetaData koleksiyonu,** tüm anlaşma türleri hakkında meta veriler sağlar. İş ortakları bu koleksiyonu kullanarak müşterinin sözleşme kabulünü onaylar. **AgreementMetaData koleksiyonu,** hem sözleşme türleri **(** hem de Microsoft Bulut Anlaşması) için **meta Microsoft Müşteri Sözleşmesi** döndürür.

## <a name="agreementmetadata"></a>AgreementMetaData

Döndürülen sözleşme meta verileri aşağıdaki özellikleri içerir:

| Özellik      | Tür               | Açıklama                                                                       |
|---------------|--------------------|-----------------------------------------------------------------------------------|
| templateId    | string             | Anlaşma şablonunun benzersiz tanımlayıcısı.                                       |
| tür          | string             | Anlaşma türü. Şu anda desteklenen değerler **Arasında MicrosoftCloudAgreement ve** **MicrosoftCustomerAgreement** (önizleme) yer alır. |
| agreementLink | string             | Anlaşma şablonunun URL'si.                                                    |
