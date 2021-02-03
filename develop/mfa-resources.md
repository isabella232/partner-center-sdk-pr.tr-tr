---
title: İş ortağı güvenlik gereksinimleri kaynakları
description: Iş ortağı güvenlik gereksinimlerini karşılamak için Multi-Factor Authentication (MFA) benimseme ayrıntılarını anlayın.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 5eb77c3c10e95c9dc835cfe05e014b9256531b51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768854"
---
# <a name="partner-security-requirements-resources"></a>İş ortağı güvenlik gereksinimleri kaynakları

**Uygulama hedefi:**

- İş Ortağı Merkezi

Bu makale, kuruluşunuzun iş ortağı güvenlik gereksinimi durumunu karşılamasına yardımcı olmak için Multi-Factor Authentication (MFA) benimseme ayrıntılarını anlamanıza yardımcı olur. 

## <a name="portal-request-without-mfa"></a>MFA olmadan Portal isteği

MFA kimlik doğrulaması olmadan Iş Ortağı Merkezi portalına erişen bir kullanıcı belirtin.

| Özellik                            | Tür            | Açıklama                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | string          | Kullanıcı nesnesi KIMLIĞI                        |
| TenantId                            | string          | CSP kiracı KIMLIĞI                         |
| 'Le                                 | string          | Kullanıcı asıl adı                   |
| Lastnonmfakarmaşıantlogindatetime    | datetime        | MFA olmadan en son zaman Kullanıcı oturumu açma |


## <a name="api-request-summarized-by-application"></a>Uygulamaya göre özetlenen API isteği

UYGULAMA + kullanıcı kimlik bilgileri tarafından yapılan, istek tarihine ve uygulama kimliğine göre toplanmış API isteğinin Özeti.

| Özellik                            | Tür            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | API istek tarihi          |
| Mfakarmaşıkantrequestcount            | long            | MFA ile istek sayısı    |
| TotalRequestCount                   | long            | Toplam istek sayısı       |
| ApplicationID                       | string          | Uygulama KIMLIĞI        |
| ApplicationName                     | string          | Uygulama adı      |


## <a name="api-request-details"></a>API isteği ayrıntıları

UYGULAMA + kullanıcı kimlik bilgileri tarafından gerçekleştirilen API isteği. 

| Özellik                            | Tür            | Description                              |
|-------------------------------------|-----------------|------------------------------------------|
| No                           | string          | MS-RequestId                             |
| CorrelationId                       | string          | MS-CorrelationId                         |
| OperationName                       | string          | İstek yöntemi ile API yolu         |
| RequestDateTime                     | DateTime        | API istek süresi                     |
| Belirlenemiyor                           | string          | Kaynak IP adresi                        |
| ObjectId                            | string          | Kullanıcı nesnesi KIMLIĞI                           |
| TenantId                            | string          | CSP kiracı KIMLIĞI                            |
| 'Le                                 | string          | Kullanıcı asıl adı                      |
| ApplicationID                       | string          | Uygulamanız                         |
| Mfauyumlu                        | bool            | MFA ile veya olmadan isteği belirtin |
