---
title: Silinen bir kullanıcıyı bir müşteri için geri yükleme
description: Silinen bir Kullanıcının müşteri kimliğine ve kullanıcı kimliğine göre geri yükleme.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445723"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Silinen bir kullanıcıyı bir müşteri için geri yükleme

Silinen bir Kullanıcının müşteri **kimliğine ve** kullanıcı kimliğine göre geri yükleme.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Kullanıcı kimliği. Kullanıcı kimliğiniz yoksa bkz. [Müşteri için silinen kullanıcıları görüntüleme.](view-a-deleted-user.md)

## <a name="when-can-you-restore-a-deleted-user-account"></a>Silinen bir kullanıcı hesabını ne zaman geri yükleyebilirsiniz?

Bir kullanıcı hesabını silebilirsiniz, kullanıcı durumu "etkin değil" olarak ayarlanır. 30 gün boyunca bu şekilde kalır ve bu sürenin ardından kullanıcı hesabı ve ilişkili verileri temizlenebilir ve kurtarılamaz hale değiştirilebilir. Silinen bir kullanıcı hesabını yalnızca bu 30 günlük süre boyunca geri yükleyebilirsiniz. Silinen ve "etkin olmayan" olarak işaretlenen kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak döndürülemez (örneğin, Bir müşteri için tüm kullanıcı hesaplarının listesini [al](get-a-list-of-all-user-accounts-for-a-customer.md)kullanılarak).

## <a name="c"></a>C\#

Bir kullanıcı geri yüklemek için [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) sınıfının yeni bir örneğini oluşturun ve User.State özelliğinin değerini [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) [**olarak ayarlayın.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)

Silinen bir kullanıcının durumunu etkin olarak ayarerek geri yükleyebilirsiniz. Kullanıcı kaynağında kalan alanları yeniden doldurmanız zorunda değildir. Bu değerler silinen, etkin olmayan kullanıcı kaynağından otomatik olarak geri yüklenir. Ardından [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanarak müşteriyi ve kullanıcıyı tanımlamak için [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini kullanın.

Son olarak [**Patch yöntemini çağırarak**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) **CustomerUser örneğini** geçarak kullanıcıya geri yükleme isteği gönderin.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** CustomerUserRestore.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem    | İstek URI'si                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **Yama** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşteri kimliğini ve kullanıcı kimliğini belirtmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, kurumsal bayinin sonuçları belirli bir müşteriye filtrelemesini sağlayan GUID biçimli bir **customer-tenant-id** değeridir. |
| **user-id**            | **guid** | Y        | Değer, tek bir kullanıcı hesabına ait OLAN GUID biçimli bir **user-id** değeridir.                                         |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde gerekli özellikleri açıklar.

| Ad       | Tür   | Gerekli | Açıklama                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Durum      | string | Y        | Kullanıcı durumu. Silinen bir kullanıcı geri yüklemek için bu dizenin "etkin" olması gerekir. |
| Öznitelikler | object | N        | "ObjectType": "CustomerUser" ifadesini içerir.                                 |

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt, yanıt gövdesinde geri yüklenen kullanıcı bilgilerini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [REST İş Ortağı Merkezi Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
