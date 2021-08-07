---
title: Dolaylı bir satıcının müşterilerini alma
description: Dolaylı kurumsal bayi müşterilerinin listesini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e0b3a45c8cf63334ac53e673fbe88734d3692dfca00c5fe8458695cc28c34f64
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990520"
---
# <a name="get-customers-of-an-indirect-reseller"></a>Dolaylı bir satıcının müşterilerini alma

Dolaylı kurumsal bayi müşterilerinin listesini alma.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Dolaylı kurumsal bayinin kiracı tanımlayıcısı.

## <a name="c"></a>C\#

Belirtilen dolaylı kurumsal bayiyle ilişkisi olan müşterilerin koleksiyonunu almak için önce filtreyi oluşturmak üzere [**bir SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi örneği oluşturun. [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) numaralama üyesini bir dizeye dönüştürmeniz ve filtre işlemi türü olarak [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) öğesini belirtebilirsiniz. Ayrıca filtrenin geçerli olduğu dolaylı kurumsal bayinin kiracı tanımlayıcısını da sağlayabilirsiniz.

Ardından [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemini çağırarak ve filtreyi geçerek sorguya geçmek için bir [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesi örneği oluşturun. BuildSimplyQuery, [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfı tarafından desteklenen sorgu türlerinden yalnızca birdir.

Filtreyi yürütmek ve sonucu almak için ilk olarak [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) kullanarak iş ortağının müşteri işlemlerine yönelik bir arabirim elde edersiniz. Ardından Query [**veya**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) [**QueryAsync yöntemini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) çağırabilirsiniz.

Sayfalamalı sonuçlarda geçiş yapmak için bir numaralayıcı oluşturmak [**için, IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) özelliğinden müşteri koleksiyonu numaralayıcı fabrika arabirimini elde edin ve ardından aşağıdaki kodda gösterildiği gibi [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)çağrısında bulunarak müşteri koleksiyonunu tutan değişkeni geçirebilirsiniz.

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

**Örnek:** [Konsol test uygulaması](console-test-app.md)**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** GetCustomersOfIndirectReseller.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İsteği oluşturmak için aşağıdaki sorgu parametrelerini kullanın.

| Ad   | Tür   | Gerekli | Açıklama                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| boyut   | int    | No       | Aynı anda görüntülenecek sonuç sayısı. Bu parametre isteğe bağlıdır.                                                                                                                                                                                                                |
| filtre | filtre | Yes      | Arama filtrelerini alan sorgu. Belirli bir dolaylı kurumsal bayinin müşterilerini almak için dolaylı kurumsal bayi tanımlayıcısını eklemeli ve şu dizeyi eklemeli ve kodlamalı: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts \_ with"}. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example-encoded"></a>İstek örneği (kodlanmış)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a>İstek örneği (kodu çözülen)

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi kurumsal bayinin müşterileri hakkında bilgiler içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
