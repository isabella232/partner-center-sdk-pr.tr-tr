---
title: Kullanıcı kaynakları
description: Bir kullanıcıya İş Ortağı Merkezi, kişisel ve hesap bilgilerine ve kullanıcıya sahip olduğu izinlere İş Ortağı Merkezi.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8c91e3509d86c8817da30c8ad0d96a2b1b6eec7697e43b47d3dfb96055cac632
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989228"
---
# <a name="user-resources"></a>Kullanıcı kaynakları

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bir kullanıcıya İş Ortağı Merkezi, kişisel ve hesap bilgilerine ve kullanıcıya sahip olduğu izinlere İş Ortağı Merkezi.

## <a name="user"></a>Kullanıcı

Tek bir kullanıcıyı açıklar.

| Özellik              | Tür                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                    | string                                                         | Kullanıcı tanımlayıcısı.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Kullanıcı asıl tanımlayıcısı.                                                                                                                                                                                             |
| firstName             | string                                                         | Kullanıcının adı.                                                                                                                                                                                                |
| lastName              | string                                                         | Kullanıcının soyadı.                                                                                                                                                                                                 |
| displayName           | string                                                         | Kullanıcının görüntülenen adı.                                                                                                                                                                                            |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Kullanıcının parola profili.                                                                                                                                                                                               |
| Phonenumber           | string                                                         | Kullanıcının telefon numarası.                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC tarih saat biçiminde dize                                 | Bu kullanıcıya ilişkin bilgilerin Azure Active Directory ile şirket içi Active Directory. Tarih saat değeri yalnızca Azure AD eşitleme Bağlan etkinse görüntülenir. Aksi takdirde değer null olur. |
| userDomainType        | string                                                         | Kullanıcı etki alanı türü: "none", "managed" veya "federated".                                                                                                                                                                   |
| state                 | string                                                         | Kullanıcının durumu: "etkin", "etkin değil" (silinen bir kullanıcı için).                                                                                                                                                          |
| softDeletionTime      | UTC tarih saat biçiminde dize                                 | Silinen bir kullanıcıyla ilişkili verilerin kalıcı olarak silindikten ve dolayısıyla kurtarılamaz hale gelen 30 günlük sürenin başlangıcını temsil eder.                                                                          |
| Bağlantı                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                                                                                                                                                                        |
| öznitelikler            | [Resourceattributes](utility-resources.md#resourceattributes) | Meta veri öznitelikleri.                                                                                                                                                                                                   |

## <a name="customeruser"></a>CustomerUser

Müşteri kullanıcılarını açıklar.

| Özellik              | Tür                                                           | Description                                                                                                                                                                                                                |
|-----------------------|----------------------------------------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| usageLocation         | string                                                         | Kullanıcının lisansı kullanmayı amacının bulunduğu konum.                                                                                                                                                                    |
| kimlik                    | string                                                         | Kullanıcı tanımlayıcısı.                                                                                                                                                                                                       |
| userPrincipalName     | string                                                         | Kullanıcı asıl tanımlayıcısı.                                                                                                                                                                                             |
| firstName             | string                                                         | Kullanıcının adı.                                                                                                                                                                                                |
| lastName              | string                                                         | Kullanıcının soyadı.                                                                                                                                                                                                 |
| displayName           | string                                                         | Kullanıcının görüntülenen adı.                                                                                                                                                                                            |
| immutableId           | string                                                         | Kullanıcının sabit kimliği.                                                                                                                                                                                              |
| passwordProfile       | [PasswordProfile](utility-resources.md#passwordprofile)       | Kullanıcının parola profili.                                                                                                                                                                                               |
| Phonenumber           | string                                                         | Kullanıcının telefon numarası.                                                                                                                                                                                                   |
| lastDirectorySyncTime | UTC tarih saat biçiminde dize                                 | Bu kullanıcıya ilişkin bilgilerin Azure Active Directory ile şirket içi Active Directory. Tarih saat değeri yalnızca Azure AD eşitleme Bağlan etkinse görüntülenir. Aksi takdirde değer null olur. |
| userDomainType        | string                                                         | Kullanıcı etki alanı türü: "none", "managed" veya "federated".                                                                                                                                                                   |
| state                 | string                                                         | Kullanıcının durumu: "etkin", "etkin değil" (silinen bir kullanıcı için).                                                                                                                                                          |
| softDeletionTime      | UTC tarih saat biçiminde dize                                 | Silinen bir kullanıcıyla ilişkili verilerin kalıcı olarak silindikten ve dolayısıyla kurtarılamaz hale gelen 30 günlük sürenin başlangıcını temsil eder.                                                                          |
| Bağlantı                 | [ResourceLinks](utility-resources.md#resourcelinks)           | Kaynak bağlantıları.                                                                                                                                                                                                        |
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

