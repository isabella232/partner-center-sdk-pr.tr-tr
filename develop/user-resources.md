---
title: Kullanıcı kaynakları
description: Tek bir Iş Ortağı Merkezi kullanıcıyı, kişisel ve hesap bilgilerini ve Iş Ortağı Merkezi 'nde sahip oldukları izinleri açıklar.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 26bb202db3eefd9be8fe57ed2cc4dc220c8807d4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529690"
---
# <a name="user-resources"></a>Kullanıcı kaynakları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Tek bir Iş Ortağı Merkezi kullanıcıyı, kişisel ve hesap bilgilerini ve Iş Ortağı Merkezi 'nde sahip oldukları izinleri açıklar.

## <a name="user"></a>Kullanıcı

Tek bir kullanıcıyı açıklar.

| Özellik              | Tür                                                           | Açıklama                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                    | string                                                         | Kullanıcı tanımlayıcısı.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Kullanıcı asıl tanımlayıcısı.                                                                                                                                                                                             |
| firstName             | string                                                         | Kullanıcının ilk adı.                                                                                                                                                                                                |
| lastName              | string                                                         | Kullanıcının soyadı.                                                                                                                                                                                                 |
| displayName           | string                                                         | Kullanıcının görünen adı.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Kullanıcının parola profili.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | Kullanıcının telefon numarası.                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC Tarih saat biçiminde dize                                 | Azure Active Directory ve şirket içi Active Directory arasında bu kullanıcı bilgilerinin son eşitlendiği zaman. bir tarih saat değeri yalnızca Azure AD Connect eşitleme etkinse görüntülenir. Aksi halde değer null olur. |
| userDomainType        | string                                                         | Kullanıcı etki alanı türü: "none", "Managed" veya "federe".                                                                                                                                                                   |
| state                 | string                                                         | Kullanıcının durumu: "etkin", "etkin değil" (silinen kullanıcı için).                                                                                                                                                          |
| softDeletionTime      | UTC Tarih saat biçiminde dize                                 | Silinen bir kullanıcıyla ilişkili verilerin kalıcı olarak silinmesini ve bu nedenle kurtarılamaz olduğunu 30 günlük sürenin başlangıcını temsil eder.                                                                          |
| Köprü                 | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                                                                                                                                                                        |
| öznitelikler            | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Bir müşteri kullanıcısını açıklar.

| Özellik              | Tür                                                           | Açıklama                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | string                                                         | Kullanıcının lisansı kullanmayı amaçladığı konum.                                                                                                                                                                    |
| kimlik                    | string                                                         | Kullanıcı tanımlayıcısı.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Kullanıcı asıl tanımlayıcısı.                                                                                                                                                                                             |
| firstName             | string                                                         | Kullanıcının ilk adı.                                                                                                                                                                                                |
| lastName              | string                                                         | Kullanıcının soyadı.                                                                                                                                                                                                 |
| displayName           | string                                                         | Kullanıcının görünen adı.                                                                                                                                                                                            |
| ImmutableID           | string                                                         | Kullanıcının sabit KIMLIĞI.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Kullanıcının parola profili.                                                                                                                                                                                               |
| phoneNumber           | string                                                         | Kullanıcının telefon numarası.                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC Tarih saat biçiminde dize                                 | Azure Active Directory ve şirket içi Active Directory arasında bu kullanıcı bilgilerinin son eşitlendiği zaman. bir tarih saat değeri yalnızca Azure AD Connect eşitleme etkinse görüntülenir. Aksi halde değer null olur. |
| userDomainType        | string                                                         | Kullanıcı etki alanı türü: "none", "Managed" veya "federe".                                                                                                                                                                   |
| state                 | string                                                         | Kullanıcının durumu: "etkin", "etkin değil" (silinen kullanıcı için).                                                                                                                                                          |
| softDeletionTime      | UTC Tarih saat biçiminde dize                                 | Silinen bir kullanıcıyla ilişkili verilerin kalıcı olarak silinmesini ve bu nedenle kurtarılamaz olduğunu 30 günlük sürenin başlangıcını temsil eder.                                                                          |
| Köprü                 | [Resourcelmürekkepler](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                                                                                                                                                                        |
| öznitelikler            | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                                                                                                                                                                   |

## <a name="usercredentials"></a>UserCredentials

Kullanıcının oturum açma kimlik bilgilerini açıklar.

| Özellik | Tür                                               | Açıklama                          |
|----------|----------------------------------------------------|--------------------------------------|
| userName | string                                             | Kullanıcının adı.                |
| password | [SecureString](utility-resources.md#securestring) | Kullanıcının güvenli şekilde depolanan parolası. |

## <a name="usermember"></a>UserMember

Kullanıcının üye bilgilerini açıklar.

| Özellik          | Tür                                                           | Açıklama                        |
|-------------------|----------------------------------------------------------------|------------------------------------|
| displayName       | string                                                         | Kullanıcının görünen adı.   |
| userPrincipalName | string                                                         | Kullanıcı sorumlusunun adı.    |
| RoleID            | string                                                         | Kullanıcı rolünün tanımlayıcısı. |
| kimlik                | string                                                         | Üyenin tanımlayıcısı.      |
| öznitelikler        | [ResourceAttributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.           |

