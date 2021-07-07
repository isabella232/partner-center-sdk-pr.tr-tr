---
title: Müşteri için silinen kullanıcıları görüntüleme
description: Müşteri kimliğine göre bir müşteri için silinen CustomerUser kaynaklarının listesini alır. İsteğe bağlı olarak bir sayfa boyutu da ayarlayabilirsiniz. Bir filtre sağlamak gerekir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f4fec958a9a6bb580d35de1cf3007e1db3b2b650
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445315"
---
# <a name="view-deleted-users-for-a-customer"></a>Müşteri için silinen kullanıcıları görüntüleme

Müşteri kimliğine göre bir müşteri için silinen CustomerUser kaynaklarının listesini alır. İsteğe bağlı olarak bir sayfa boyutu da ayarlayabilirsiniz. Bir filtre sağlamak gerekir.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="what-happens-when-you-delete-a-user-account"></a>Bir kullanıcı hesabını silebilirsiniz.

Bir kullanıcı hesabını silebilirsiniz, kullanıcı durumu "etkin değil" olarak ayarlanır. 30 gün boyunca bu şekilde kalır ve bu sürenin ardından kullanıcı hesabı ve ilişkili verileri temizlenebilir ve kurtarılamaz hale değiştirilebilir. Silinen bir kullanıcı hesabını 30 günlük süre içinde geri yüklemek için bkz. Silinen bir [kullanıcıyı müşteri için geri yükleme.](restore-a-user-for-a-customer.md) Silindikten ve "etkin değil" olarak işaretlendiktan sonra, kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak [döndürülemez](get-a-list-of-all-user-accounts-for-a-customer.md)(örneğin, Bir müşteri için tüm kullanıcı hesaplarının listesini al kullanılarak). Henüz temizlenemeyen silinmiş kullanıcıların listesini almak için etkin değil olarak ayarlanmış kullanıcı hesaplarını sorgulamanız gerekir.

## <a name="c"></a>C\#

Silinen kullanıcıların listesini almak için, durumu etkin olmayan olarak ayarlanmış müşteri kullanıcılarını filtreleten bir sorgu oluşturun. İlk olarak, aşağıdaki kod parçacığında gösterildiği gibi parametrelerle [**bir SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi örneği başlatarak filtreyi oluşturun. Ardından [**BuildIndexedQuery yöntemini kullanarak sorguyu**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) oluşturun. Sayfalı sonuçları istemiyorsanız bunun yerine [**BuildSimpleQuery yöntemini kullanabilirsiniz.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) Ardından, müşteriyi [**tanımlamak için IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanın. Son olarak, isteği göndermek için [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) yöntemini çağırabilirsiniz.

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

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı **Örnekler Sınıfı:** GetCustomerInactiveUsers.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| customer-id | guid   | Yes      | Değer, müşteriyi tanımlayan GUID biçimli bir customer-id değeridir.                                                                                                            |
| boyut        | int    | Hayır       | Aynı anda görüntülenecek sonuç sayısı. Bu parametre isteğe bağlıdır.                                                                                                     |
| filtre      | filtre | Yes      | Kullanıcı aramalarını filtreleen sorgu. Silinen kullanıcıları almak için şu dizeyi dahil etmek ve kodlamanız gerekir: {"Field":"UserState","Value":"Inactive","Operator":"equals"}. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, bu yöntem yanıt gövdesinde [CustomerUser](user-resources.md#customeruser) kaynaklarının bir koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
