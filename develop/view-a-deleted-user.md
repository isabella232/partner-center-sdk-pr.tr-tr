---
title: Müşteri için silinen kullanıcıları görüntüleme
description: Müşteri KIMLIĞINE göre bir müşterinin silinen CustomerUser kaynaklarının bir listesini alır. İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz. Bir filtre sağlamanız gerekir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769533"
---
# <a name="view-deleted-users-for-a-customer"></a>Müşteri için silinen kullanıcıları görüntüleme

**Uygulama hedefi**

- İş Ortağı Merkezi

Müşteri KIMLIĞINE göre bir müşterinin silinen CustomerUser kaynaklarının bir listesini alır. İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz. Bir filtre sağlamanız gerekir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="what-happens-when-you-delete-a-user-account"></a>Bir kullanıcı hesabını sildiğinizde ne olur?

Bir kullanıcı hesabını sildiğinizde Kullanıcı durumu "devre dışı" olarak ayarlanır. Bu, otuz gün boyunca, Kullanıcı hesabının ve ilişkili verilerinin temizlenme ve kurtarılamaz hale getirilme yolunda kalır. Bir silinen kullanıcı hesabını otuz gün penceresinde geri yüklemek isterseniz, bkz. bir [müşteri için silinen bir kullanıcıyı geri yükleme](restore-a-user-for-a-customer.md). Silinen ve "etkin olmayan" olarak işaretlenen Kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak döndürülmez (örneğin, [bir müşterinin tüm Kullanıcı hesaplarının listesini al](get-a-list-of-all-user-accounts-for-a-customer.md)' ı kullanarak). Henüz temizlenmemiş silinen kullanıcıların bir listesini almak için, etkin olmayan olarak ayarlanmış kullanıcı hesaplarını sorgumalısınız.

## <a name="c"></a>C\#

Silinen kullanıcıların bir listesini almak için, durumu devre dışı olarak ayarlanan müşteri kullanıcıları için filtre uygulayan bir sorgu oluşturun. İlk olarak, aşağıdaki kod parçacığında gösterildiği gibi parametreleriyle bir [**Simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesini örnekleyerek filtre oluşturun. Sonra [**Buildındexedquery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) yöntemini kullanarak sorguyu oluşturun. Disk belleğine alınmış sonuçları istemiyorsanız, bunun yerine [**Buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemini kullanabilirsiniz. Ardından, müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın. Son olarak, isteği göndermek için [**sorgu**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? size = {size} &filtre = {FILTER} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| müşteri kimliği | guid   | Yes      | Değer, müşteriyi tanımlayan bir GUID biçimli müşteri kimliği olur.                                                                                                            |
| boyut        | int    | No       | Tek seferde görüntülenecek sonuç sayısı. Bu parametre isteğe bağlıdır.                                                                                                     |
| filtre      | filtre | Yes      | Kullanıcı aramasına filtre uygulayan sorgu. Silinen kullanıcıları almak için şu dizeyi dahil etmeniz ve kodlamanız gerekir: {"alan": "UserState", "Value": "etkin olmayan", "Işleç": "Equals"}. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir [Customeruser](user-resources.md#customeruser) kaynakları koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
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
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
