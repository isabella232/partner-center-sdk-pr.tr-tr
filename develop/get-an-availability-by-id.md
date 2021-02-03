---
title: KIMLIĞE göre kullanılabilirliği al
description: Bir kullanılabilirlik KIMLIĞI kullanarak belirtilen ürün ve SKU için kullanılabilirliği alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768759"
---
# <a name="get-the-availability-by-id"></a>KIMLIĞE göre kullanılabilirliği al

**Uygulama hedefi**

- İş Ortağı Merkezi

Bir kullanılabilirlik KIMLIĞI kullanarak belirtilen ürün ve SKU için kullanılabilirliği alır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir ürün KIMLIĞI.

- SKU KIMLIĞI.

- Bir kullanılabilirlik KIMLIĞI.

## <a name="c"></a>C\#

Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak için, belirli bir [SKU 'nun](product-resources.md#sku) işlemlerine yönelik arabirimi almak üzere [bir SKU 'yu kimliğe göre Al](get-a-sku-by-id.md) ' daki adımları kullanarak başlayın. Sonuç arabiriminden, kullanılabilirliği için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **kullanılabilirlik** özelliğini seçin. Bundan sonra, söz konusu kullanılabilirliğe yönelik işlemleri almak için kullanılabilirlik KIMLIĞINI **Byıd ()** yöntemine geçirin ve ardından kullanılabilirlik ayrıntılarını almak için **Get ()** veya **GetAsync ()** öğesini çağırın.

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak için, belirli bir [SKU 'nun](product-resources.md#sku) işlemlerine yönelik arabirimi almak üzere [bir SKU 'yu kimliğe göre Al](get-a-sku-by-id.md) ' daki adımları kullanarak başlayın. Sonuç arabiriminden, kullanılabilirlik için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **Getavailalıklara** işlevini seçin. Bundan sonra, söz konusu kullanılabilirliğe yönelik işlemleri almak için kullanılabilirlik KIMLIĞINI **Byıd ()** işlevine geçirin ve ardından kullanılabilirlik ayrıntılarını almak için **Get ()** işlevini çağırın.

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak Için, [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) ' ı yürütün ve kullanılabilirlik ayrıntılarını almak için kullanılabilirlik **kimliği**, **CountryCode**, **ProductID** ve **skuid** parametrelerini belirtin.

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKUs/{SKU-id}/availabilities/{Availability-id}? ülke = {Country-Code} http/1.1         |

### <a name="uri-parameter"></a>URI parametresi

Bir kullanılabilirlik KIMLIĞI kullanarak belirli bir kullanılabilirliği almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ürün kimliği             | string   | Yes      | Ürünü tanımlayan GUID biçimli dize.            |
| SKU kimliği                 | string   | Yes      | SKU 'YU tanımlayan GUID biçimli dize.                |
| kullanılabilirlik kimliği        | string   | Yes      | Kullanılabilirliği tanımlayan bir GUID biçimli dize.       |
| ülke kodu           | string   | Yes      | Ülke/bölge KIMLIĞI.                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [kullanılabilirlik](product-resources.md#availability) kaynağı içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP durum kodu     | Hata kodu   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Ürün bulunamadı.                                                                                    |
| 404                  | 400018       | SKU bulunamadı.                                                                                        |
| 404                  | 400019       | Kullanılabilirlik bulunamadı.                                                                                   |

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
