---
title: Anlaşma kaynakları
description: Sözleşme kaynağı, iş ortağı tarafından sunulan sertifika ayrıntıları ile bir Microsoft bulut müşteri anlaşmasını temsil eder.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 5fa196e711d9ff899b61ba20e75edd92749165e5
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025640"
---
# <a name="agreement-resources-representing-a-microsoft-cloud-customer-agreement"></a>Microsoft bulut müşteri anlaşmasını temsil eden sözleşme kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi

**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

**Sözleşme** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.

**Sözleşme** kaynağı bir Microsoft bulut müşteri anlaşmasını temsil eder.

## <a name="agreement"></a>Sözleşme

**Anlaşma** kaynağı, iş ortağı tarafından belirtilen sertifikanın ayrıntılarını temsil eder.

| Özellik       | Tür   | Açıklama                                                                                               |
|----------------|--------|-----------------------------------------------------------------------------------------------------------|
| userId         | string                         | İş ortağı kiracısında iş ortağı kuruluşu adına onay sağlayan, oturum açmış kullanıcının nesne tanıtıcısı. Iş Ortağı Merkezi, bir anlaşma kaynağı oluşturmak için uygulama + kullanıcı kimlik doğrulaması kullanırken, uygulama + Kullanıcı belirtecinden **UserID** özniteliği değerini otomatik olarak türetir.                                                                             |
| primaryContact | [İletişim](./utility-resources.md#contact) | Müşteri kuruluşundan, sözleşmeyi kabul  **eden,** **Soyadı**, **e-posta** ve **PhoneNumber** (isteğe bağlı) dahil olmak üzere Kullanıcı hakkında bilgiler. |
| Kabul edilen tarih     | UTC Tarih saat biçiminde dize | Müşterinin sözleşmeyi kabul ettiği tarih.                                 |
| TemplateId     |string                          | Müşterinin kabul ettiği sözleşmenin benzersiz tanıtıcısı. |
| tür           |string                          | Anlaşma türü. Şu anda, desteklenen değerler **Microsoftcloudagreement** ve **microsoftcustomeragreement**' i içerir.|
| agreementLink  | string                         | Sözleşme şablonunun URL 'SI.                                                    |
