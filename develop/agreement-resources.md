---
title: Anlaşma kaynakları
description: Anlaşma kaynağı, iş ortağı tarafından sağlanan sertifikasyon ayrıntılarının yer alan bir Microsoft bulut müşteri sözleşmesini temsil eder.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: dc67d93a40cdced977412ff8151a661f6655c0fa1d079c8f1bc468f0f8b1eea2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992492"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Microsoft bulut müşteri sözleşmelerini temsil eden sözleşme kaynakları

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Sözleşme **kaynağı** şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde kullanılabilir.

Anlaşma **kaynağı** bir Microsoft bulut müşterisi anlaşmasını temsil eder.

## <a name="agreement"></a>Sözleşme

Anlaşma **kaynağı,** iş ortağı tarafından sağlanan sertifikasyon ayrıntılarını temsil eder.

| Özellik       | Tür   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         | İş ortağı kuruluş adına onay sağlayan iş ortağı kiracısında oturum açmış kullanıcının nesne tanımlayıcısı. Bir Sözleşme kaynağı oluşturmak için App+User kimlik doğrulaması kullanılırken, İş Ortağı Merkezi App+User belirteclerinden **userId** öznitelik değerini otomatik olarak türetebilirsiniz.                                                                             |
| primaryContact | [İletişim](./utility-resources.md#contact) | Sözleşmeyi kabul eden müşteri kuruluşundan kullanıcı hakkında bilgiler:  **firstName**, **lastName,** **email** ve **phoneNumber** (isteğe bağlı). |
| dateAgreed     | UTC tarih saat biçiminde dize | Müşterinin sözleşmeyi kabul etme tarihi.                                 |
| templateId     |string                          | Müşterinin kabul etmiş olduğu sözleşmenin benzersiz tanımlayıcısı. |
| tür           |string                          | Anlaşma türü. Şu anda desteklenen değerler **MicrosoftCloudAgreement ve** **MicrosoftCustomerAgreement'tir.**|
| agreementLink  | string                         | Anlaşma şablonunun URL'si.                                                    |
