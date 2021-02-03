---
title: Müşteri sözleşmesinin doğrudan imzalama (doğrudan kabul) durumu.
description: DirectSignedCustomerAgreementStatus kaynağı, müşteri anlaşmasının doğrudan imzalanmasının (doğrudan kabul) durumunu temsil eder.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9c4fd12ac3319057f3c4034aa0c8d93dcda726c6
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768795"
---
# <a name="direct-signing-direct-acceptance-status-of-a-customer-agreement"></a>Müşteri sözleşmesinin doğrudan imzası (doğrudan kabul) durumu

**Uygulama hedefi:**

- İş Ortağı Merkezi

**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.

Bu kaynak için *geçerli değildir* :

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

**DirectSignedCustomerAgreementStatus** kaynağı, müşteri sözleşmesinin doğrudan kabulünün durumunu temsil eder.

## <a name="directsignedcustomeragreementstatus"></a>DirectSignedCustomerAgreementStatus

Bir **DirectSignedCustomerAgreementStatus** kaynağı aşağıdaki özellikleri içerir:

| Özellik       | Tür   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| isSigned | boolean | Müşteri sözleşmesinin müşteri tarafından doğrudan imzalanıp imzalanmadığını (kabul edildi) gösterir. |
