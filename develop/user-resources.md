---
title: Kullanıcı kaynakları
description: Tek bir Iş Ortağı Merkezi kullanıcıyı, kişisel ve hesap bilgilerini ve Iş Ortağı Merkezi 'nde sahip oldukları izinleri açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0c88b9b65dfb925712ff85fb42d34251cca6e0b5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768710"
---
# <a name="user-resources"></a>Kullanıcı kaynakları

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Tek bir Iş Ortağı Merkezi kullanıcıyı, kişisel ve hesap bilgilerini ve Iş Ortağı Merkezi 'nde sahip oldukları izinleri açıklar.

## <a name="user"></a>Kullanıcı

Tek bir kullanıcıyı açıklar.

| Özellik              | Tür                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                    | string                                                         | Kullanıcı tanımlayıcısı.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Kullanıcı asıl tanımlayıcısı.                                                                                                                                                                                             |
| firstName             | string                                                         | Kullanıcının ilk adı.                                                                                                                                                                                                |
| lastName              | string                                                         | Kullanıcının soyadı.                                                                                                                                                                                                 |
| displayName           | string                                                         | Kullanıcının görünen adı.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Kullanıcının parola profili.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | Kullanıcının telefon numarası.                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC Tarih saat biçiminde dize                                 | Azure Active Directory ve şirket içi Active Directory arasında bu kullanıcı bilgilerinin son eşitlendiği zaman. Bir tarih saat değeri yalnızca Azure AD Connect eşitleme etkinse görüntülenir. Aksi halde değer null olur. |
| userDomainType        | string                                                         | Kullanıcı etki alanı türü: "none", "Managed" veya "federe".                                                                                                                                                                   |
| state                 | string                                                         | Kullanıcının durumu: "etkin", "etkin değil" (silinen kullanıcı için).                                                                                                                                                          |
| softDeletionTime      | UTC Tarih saat biçiminde dize                                 | Silinen bir kullanıcıyla ilişkili verilerin kalıcı olarak silinmesini ve bu nedenle kurtarılamaz olduğunu gösteren otuz günlük dönemin başlangıcını temsil eder.                                                                          |
| Köprü                 | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                                                                                                                                                                        |
| öznitelikler            | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Bir müşteri kullanıcısını açıklar.

| Özellik              | Tür                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | string                                                         | Kullanıcının lisansı kullanmayı amaçladığı konum.                                                                                                                                                                    |
| kimlik                    | string                                                         | Kullanıcı tanımlayıcısı.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Kullanıcı asıl tanımlayıcısı.                                                                                                                                                                                             |
| firstName             | string                                                         | Kullanıcının ilk adı.                                                                                                                                                                                                |
| lastName              | string                                                         | Kullanıcının soyadı.                                                                                                                                                                                                 |
| displayName           | string                                                         | Kullanıcının görünen adı.                                                                                                                                                                                            |
| ImmutableID           | string                                                         | Kullanıcının sabit kimliği.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Kullanıcının parola profili.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | Kullanıcının telefon numarası.                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC Tarih saat biçiminde dize                                 | Azure Active Directory ve şirket içi Active Directory arasında bu kullanıcı bilgilerinin son eşitlendiği zaman. Bir tarih saat değeri yalnızca Azure AD Connect eşitleme etkinse görüntülenir. Aksi halde değer null olur. |
| userDomainType        | string                                                         | Kullanıcı etki alanı türü: "none", "Managed" veya "federe".                                                                                                                                                                   |
| state                 | string                                                         | Kullanıcının durumu: "etkin", "etkin değil" (silinen kullanıcı için).                                                                                                                                                          |
| softDeletionTime      | UTC Tarih saat biçiminde dize                                 | Silinen bir kullanıcıyla ilişkili verilerin kalıcı olarak silinmesini ve bu nedenle kurtarılamaz olduğunu gösteren otuz günlük dönemin başlangıcını temsil eder.                                                                          |
| Köprü                 | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                                                                                                                                                                        |
| öznitelikler            | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Kullanıcının oturum açma kimlik bilgilerini açıklar.

| Özellik | Tür                                               | Description                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | string                                             | Kullanıcının adı.                |
| password | [SecureString](utility-resources.md#securestring) | Kullanıcının güvenli şekilde depolanan parolası. |

## <a name="usermember"></a>UserMember

Kullanıcının üye bilgilerini açıklar.

| Özellik          | Tür                                                           | Description                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | string                                                         | Kullanıcının görünen adı.   |
| userPrincipalName | string                                                         | Kullanıcı sorumlusunun adı.    |
| RoleID            | string                                                         | Kullanıcı rolünün tanımlayıcısı. |
| kimlik                | string                                                         | Üyenin tanımlayıcısı.      |
| öznitelikler        | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.           |

