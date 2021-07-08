---
title: Müşterilerin bir listesini alma
description: Bir iş ortağının müşterilerinin tümünü temsil eden bir kaynak koleksiyonu alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 840c9d1a61451763d37a19639f99b12f1deb7521
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874355"
---
# <a name="get-a-list-of-customers"></a>Müşterilerin bir listesini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bu makalede, bir iş ortağının müşterilerinin tümünü temsil eden bir kaynak koleksiyonunun nasıl alınacağı açıklanır.

> [!TIP]
> Bu işlemi Iş Ortağı Merkezi panosunda da gerçekleştirebilirsiniz. Ana sayfada, **müşteri yönetimi** altında, **müşterileri görüntüle**' yi seçin. Ya da kenar çubuğunda **müşteriler**' i seçin.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

Tüm müşterilerin bir listesini almak için:

1. [**Iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunu kullanarak bir **ıpartner** nesnesi oluşturun.

2. [**Sorgu ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) veya [**queryasync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) yöntemlerini kullanarak müşteri listesini alın. (Sorgu oluşturma yönergeleri için bkz. [**Queryfactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfı.)

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

Bir örnek için aşağıdakilere bakın:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Project: **partnersdk. featuresamples**
- Sınıf: **Customerpaging. cs**

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Tüm müşterilerin bir listesini almak için:

1. Müşteri işlemlerine bir başvuru almak için [**ıaggregatepartner. getCustomers**] işlevini kullanın.

2. **Sorgu ()** işlevini kullanarak müşteri listesini alın.

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Müşterilerin tam listesini almak için [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) komutunu parametresiz olarak yürütün.

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                   |
|---------|-------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers? boyut = {SIZE} http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Müşterilerin bir listesini almak için aşağıdaki sorgu parametresini kullanın.

| Ad     | Tür    | Gerekli | Açıklama                                        |
|----------|---------|----------|----------------------------------------------------|
| **boyutla** | **int** | Y        | Tek seferde görüntülenecek sonuç sayısı. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir [Müşteri](customer-resources.md#customer) kaynakları koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
