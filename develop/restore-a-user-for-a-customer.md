---
title: Silinen bir kullanıcıyı bir müşteri için geri yükleme
description: Silinen bir kullanıcıyı müşteri KIMLIĞINE ve Kullanıcı KIMLIĞINE göre geri yükleme.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769797"
---
# <a name="restore-a-deleted-user-for-a-customer"></a>Silinen bir kullanıcıyı bir müşteri için geri yükleme

**Uygulama hedefi**

- İş Ortağı Merkezi

Silinen bir **kullanıcıyı** müşteri kimliğine ve kullanıcı kimliğine göre geri yükleme.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Kullanıcı kimliği. Kullanıcı KIMLIĞINIZ yoksa, bkz. [bir müşteri için silinen kullanıcıları görüntüleme](view-a-deleted-user.md).

## <a name="when-can-you-restore-a-deleted-user-account"></a>Silinen bir kullanıcı hesabını geri yüklemek ne zaman olabilir?

Bir kullanıcı hesabını sildiğinizde Kullanıcı durumu "devre dışı" olarak ayarlanır. Bu, otuz gün boyunca, Kullanıcı hesabının ve ilişkili verilerinin temizlenme ve kurtarılamaz hale getirilme yolunda kalır. Silinen bir kullanıcı hesabını yalnızca bu otuz günlük pencere sırasında geri yükleyebilirsiniz. Silinen ve "etkin olmayan" olarak işaretlenen "etkin değil" Kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak döndürülmez (örneğin, [bir müşterinin tüm Kullanıcı hesaplarının listesini al](get-a-list-of-all-user-accounts-for-a-customer.md)' ı kullanarak).

## <a name="c"></a>C\#

Bir kullanıcıyı geri yüklemek için [**customeruser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) sınıfının yeni bir örneğini oluşturun ve [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) özelliğinin değerini [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)olarak ayarlayın.

Silinen bir kullanıcıyı, kullanıcının durumunu etkin olarak ayarlayarak geri yükleyebilirsiniz. Kullanıcı kaynağındaki kalan alanları yeniden doldurmanız gerekmez. Bu değerler, silinen, etkin olmayan kullanıcı kaynağından otomatik olarak geri yüklenir. Ardından, müşteriyi tanımlamak için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve kullanıcıyı tanımlamak için [**Users. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini kullanın.

Son olarak, [**yama**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) yöntemini çağırın ve kullanıcıyı geri yükleme isteğini göndermek Için **customeruser** örneğini geçirin.

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

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CustomerUserRestore.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem    | İstek URI'si                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| **DÜZELTMESI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşteri kimliğini ve Kullanıcı kimliğini belirtmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y        | Değer, satıcının sonuçları belirli bir müşteriye filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** olur. |
| **Kullanıcı kimliği**            | **guid** | Y        | Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.                                         |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.

| Ad       | Tür   | Gerekli | Açıklama                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| Durum      | string | Y        | Kullanıcı durumu. Silinen bir kullanıcıyı geri yüklemek için, bu dize "etkin" içermelidir. |
| Öznitelikler | object | N        | "ObjectType": "CustomerUser" içerir.                                 |

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

Başarılı olursa yanıt, yanıt gövdesinde geri yüklenen Kullanıcı bilgilerini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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
