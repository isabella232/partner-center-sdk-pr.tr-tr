---
title: Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma
description: Müşteri ülkesine göre belirtilen ürün ve SKU için kullanılabilirlik koleksiyonu alma.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 8e5fe9bae436d8b7f237b9039c66b369f0e32109
ms.sourcegitcommit: b0534995c36d644cc5f7bdf31b2afd5355cf7149
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/16/2021
ms.locfileid: "122208084"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma

Bu makalede, belirli bir ülkede belirtilen ürün ve SKU için bir kullanılabilirlik koleksiyonunun nasıl alınacağı açıklanır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir ürün tanımlayıcısı.

- Bir SKU tanımlayıcısı.

- Bir ülke.

## <a name="c"></a>C\#

[SKU](product-resources.md#sku)'nun [kullanılabilirliği](product-resources.md#availability) listesini almak için:

1. Belirli bir SKU 'nun işlemlerinin arabirimini almak için [kimliğe göre SKU 'Yu edinme](get-a-sku-by-id.md) bölümündeki adımları izleyin.

2. SKU arabiriminden, kullanılabilirliği olan işlemleri içeren bir arabirim almak için **kullanılabilirlik** özelliğini seçin.

3. Seçim Kullanılabilirliği hedef kesime göre filtrelemek için **Bytargetsegment ()** yöntemini kullanın.

4. Bu SKU 'nun kullanılabilirliği koleksiyonunu almak için **Get ()** veya **GetAsync ()** öğesini çağırın.

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **AL** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKUs/{SKU-id}/kullanılabilirlik lıklara mi? ülke = {Country-code} &targetsegment = {Target-segment} http/1.1     |

### <a name="uri-parameters"></a>URI parametreleri

SKU 'nun kullanılabilirliği listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ürün kimliği             | string   | Yes      | Ürünü tanımlayan bir dize.                           |
| SKU kimliği                 | string   | Yes      | SKU 'YU tanımlayan bir dize.                               |
| ülke kodu           | string   | Yes      | Ülke/bölge KIMLIĞI.                                            |
| hedef segment         | dize   | No       | Filtreleme için kullanılan hedef segmenti tanımlayan bir dize. |
| Rezervationscope | dize   | No | Bir Azure ayırma SKU 'SU için bir kullanılabilirlik listesi sorgulanırken, `reservationScope=AzurePlan` Azuplanlama için geçerli olan kullanılabilirlik listesini almak için belirtin. Microsoft Azure (MS-azr-0145p) abonelikleri için geçerli olan kullanılabilirliği listesini almak için bu parametreyi dışlayın.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-examples"></a>İstek örnekleri

#### <a name="availabilities-for-sku-by-country"></a>Ülkeye göre SKU için kullanılabilirlik

Ülkeye göre belirli bir SKU 'nun kullanılabilirliği listesini almak için bu örneği izleyin:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>VM ayırmaları için kullanılabilirlik (Azure planı)

Azure VM ayırma SKU 'Larının ülkeye göre kullanılabilirliği listesini almak için bu örneği izleyin. Bu örnek, Azure planlarına uygulanan SKU 'Lara yöneliktir:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-azr-0145p) abonelikleri için VM ayırmaları kullanılabilirliği

Microsoft Azure (MS-azr-0145p) abonelikleri için geçerli olan Azure VM ayırmaları için ülkeye göre kullanılabilirlik listesini almak için bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [**kullanılabilirlik**](product-resources.md#availability) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP durum kodu     | Hata kodu   | Açıklama                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | İstenen **Targetsegment** erişimine izin verilmiyor.                                                     |

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
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
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
