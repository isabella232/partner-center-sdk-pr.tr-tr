---
title: Müşteri için kullanıcı rolleri ayarlama
description: Bir müşteri hesabı içinde bir dizi dizin rolü vardır. Bu rollere kullanıcı hesapları atabilirsiniz.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 945b5180ce2fe9067a940942a6e3c61dc243978fcb9d02eb218dce69ec487402
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989041"
---
# <a name="set-user-roles-for-a-customer"></a>Müşteri için kullanıcı rolleri ayarlama

Bir müşteri hesabı içinde bir dizi dizin rolü vardır. Bu rollere kullanıcı hesapları atabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="c"></a>C\#

Bir müşteri kullanıcıya dizin rolü atamak için, ilgili kullanıcı ayrıntılarıyla [**yeni bir UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) oluşturun. Ardından, müşteriyi [**tanımlamak için belirtilen müşteri kimliğiyle IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Burada, rolü belirtmek için [**dizin rolü kimliğiyle DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) yöntemini kullanın. Ardından **UserMembers koleksiyonuna** erişin ve [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) yöntemini kullanarak yeni kullanıcı üyesini bu role atanan kullanıcı üyeleri koleksiyonuna ekleyin.

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** AddUserMemberToDirectoryRole.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Doğru müşteriyi ve rolü belirlemek için aşağıdaki URI parametrelerini kullanın. Rolün atanacak kullanıcıyı belirlemek için, istek gövdesinde tanımlayıcı bilgileri sağlar.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir. |
| **role-id**            | **guid** | Y        | Değer, kullanıcıya atanma **rolünü tanımlayan GUID** biçimli bir rol kimliğidir.                                                              |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde gerekli özellikleri açıklar.

| Ad                  | Tür       | Gerekli | Açıklama                            |
|-----------------------|------------|----------|----------------------------------------|
| **Kimliği**                | **string** | Y        | Role eklemek istediğiniz kullanıcının kimliği. |
| **DisplayName**       | **string** | Y        | Kullanıcının kolay görünen adı. |
| **Userprincipalname** | **string** | Y        | Kullanıcı sorumlusu adı.        |
| **Öznitelikler**        | **Nesne** | Y        | "ObjectType":"UserMember" içerir     |

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Bu yöntem, kullanıcıya başarıyla rol atandığı zaman rol kimliği eklenmiş kullanıcı hesabını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
