---
title: Anlaşma kaynakları
description: Sözleşme kaynağı, iş ortağı tarafından sunulan sertifika ayrıntıları ile bir Microsoft bulut müşteri anlaşmasını temsil eder.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: d964b1c7c6d70814ef68e48f05611ecbb113c8fe
ms.sourcegitcommit: d1104d5c27f8fb3908a87532f80c432f0147ef5d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/13/2020
ms.locfileid: "97770019"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Microsoft bulut müşteri anlaşmasını temsil eden sözleşme kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi

**Sözleşme** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir. Şunları yapmak için geçerli değildir:

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

**Sözleşme** kaynağı bir Microsoft bulut müşteri anlaşmasını temsil eder.

## <a name="agreement"></a>Sözleşme

**Anlaşma** kaynağı, iş ortağı tarafından belirtilen sertifikanın ayrıntılarını temsil eder.

| Özellik       | Tür   | Description                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         | İş ortağı kiracısında iş ortağı kuruluşu adına onay sağlayan, oturum açmış kullanıcının nesne tanıtıcısı. Iş Ortağı Merkezi, bir anlaşma kaynağı oluşturmak için uygulama + kullanıcı kimlik doğrulaması kullanırken, uygulama + Kullanıcı belirtecinden **UserID** özniteliği değerini otomatik olarak türetir.                                                                             |
| primaryContact | [İletişim](./utility-resources.md#contact) | Müşteri kuruluşundan, sözleşmeyi kabul  **eden,** **Soyadı**, **e-posta** ve **PhoneNumber** (isteğe bağlı) dahil olmak üzere Kullanıcı hakkında bilgiler. |
| Kabul edilen tarih     | UTC Tarih saat biçiminde dize | Müşterinin sözleşmeyi kabul ettiği tarih.                                 |
| TemplateId     |string                          | Müşterinin kabul ettiği sözleşmenin benzersiz tanıtıcısı. |
| tür           |string                          | Anlaşma türü. Şu anda, desteklenen değerler **Microsoftcloudagreement** ve **microsoftcustomeragreement**' i içerir.|
| agreementLink  | string                         | Sözleşme şablonunun URL 'SI.                                                    |
