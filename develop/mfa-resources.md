---
title: İş Ortağı Güvenlik gereksinimleri kaynakları
description: İş Ortağı Güvenlik Gereksinimlerini karşılamak için çok faktörlü kimlik doğrulaması (MFA) benimseme ayrıntılarını anlama.
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.date: 05/29/2020
ms.openlocfilehash: 6377dbde574edd1b8d8058f7b8e88ae6497d615b9237bbda91e9c4617486b569
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997898"
---
# <a name="partner-security-requirements-resources"></a>İş ortağı güvenlik gereksinimleri kaynakları

Bu makale, çok faktörlü kimlik doğrulaması (MFA) benimseme ayrıntılarını anlamanıza yardımcı olur ve bu sayede kuruluşta iş ortağı güvenlik gereksinimi durumunu karşılamaya yardımcı olur. 

## <a name="portal-request-without-mfa"></a>MFA olmadan portal isteği

MFA kimlik doğrulaması olmadan İş Ortağı Merkezi erişen bir kullanıcıya işaret edin.

| Özellik                            | Tür            | Açıklama                           |
|-------------------------------------|-----------------|---------------------------------------|
| ObjectId                            | string          | Kullanıcı Nesne Kimliği                        |
| TenantId                            | string          | CSP kiracı kimliği                         |
| Upn                                 | string          | Kullanıcı asıl adı                   |
| LastNonMfaCompliantLoginDateTime    | datetime        | MFA olmadan en son kullanıcı oturum açma zamanı |


## <a name="api-request-summarized-by-application"></a>Uygulama tarafından özetlenen API isteği

APP + Kullanıcı kimlik bilgileri tarafından yapılan API isteğinin, istek tarihine ve Uygulama Kimliğine göre toplanmış bir özeti.

| Özellik                            | Tür            | Description               |
|-------------------------------------|-----------------|---------------------------|
| LoginDate                           | datetime        | API istek tarihi          |
| MfaCompliantRequestCount            | long            | MFA ile istek sayısı    |
| TotalRequestCount                   | long            | Toplam istek sayısı       |
| ApplicationID                       | string          | Uygulama kimliği        |
| ApplicationName                     | string          | Uygulama adı      |


## <a name="api-request-details"></a>API isteği ayrıntıları

APP + Kullanıcı kimlik bilgileri tarafından yapılan API isteği. 

| Özellik                            | Tür            | Description                              |
|-------------------------------------|-----------------|------------------------------------------|
| Requestıd                           | string          | MS-RequestId                             |
| CorrelationId                       | string          | MS-CorrelationId                         |
| OperationName                       | string          | İstek yöntemiyle API yolu         |
| RequestDateTime                     | DateTime        | API istek süresi                     |
| ıpaddress                           | string          | Kaynak IP adresi                        |
| ObjectId                            | string          | Kullanıcı nesnesi kimliği                           |
| TenantId                            | string          | CSP kiracı kimliği                            |
| Upn                                 | string          | Kullanıcı asıl adı                      |
| ApplicationID                       | string          | Uygulamanız                         |
| MfaCompliant                        | bool            | İsteği MFA ile veya MFA olmadan belirt |
