---
title: Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma
description: Müşteri ülkesi tarafından belirtilen ürün ve SKU için kullanılabilirlik koleksiyonunu elde etmek.
ms.date: 02/16/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 763a116cf120aaeeea7fddc1be7b2931f4a513e6
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456010"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a>Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma

Bu makalede belirli bir ülkede belirli bir ürün ve SKU için bir kullanılabilirlik koleksiyonunun nasıl elde edildikleri açıklanmıştır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Ürün tanımlayıcısı.

- SKU tanımlayıcısı.

- Ülke.

## <a name="c"></a>C\#

[Bir SKU'nun](product-resources.md#sku) [kullanılabilirlik](product-resources.md#availability) listesini almak için:

1. Belirli bir [SKU'nun işlemlerinin arabirimini](get-a-sku-by-id.md) almak için Kimle SKU elde etme adımlarını izleyin.

2. SKU arabiriminden Kullanılabilirlik **işlemleriyle bir** arabirim elde etmek için Kullanılabilirlik özelliğini seçin.

3. (İsteğe bağlı) **Kullanılabilirlikleri hedef segmente göre filtrelemek için ByTargetSegment()** yöntemini kullanın.

4. Bu SKU'nun kullanılabilirlik koleksiyonunu almak için **Get()** veya **GetAsync()** çağrısında bulundurabilirsiniz.

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

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **AL** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1     |

### <a name="uri-parameters"></a>URI parametreleri

Bir SKU'nun kullanılabilirlik listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| product-id             | string   | Yes      | Ürünü tanımlayan bir dize.                           |
| sku-id                 | string   | Yes      | SKU'ları tanımlayan bir dize.                               |
| ülke kodu           | string   | Yes      | Ülke/bölge kimliği.                                            |
| hedef segment         | dize   | No       | Filtreleme için kullanılan hedef segmenti tanımlayan bir dize. |
| reservationScope | dize   | No | Azure Rezervasyon SKU'sunuz için kullanılabilirlik listesini sorgularken, AzurePlan için geçerli olan kullanılabilirliklerin listesini almak `reservationScope=AzurePlan` için belirtin. Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli kullanılabilirliklerin listesini almak için bu parametreyi hariç tutabilirsiniz.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-examples"></a>İstek örnekleri

#### <a name="availabilities-for-sku-by-country"></a>Ülkeye göre SKU kullanılabilirlikleri

Ülkeye göre verilen SKU'nun kullanılabilirlik listesini almak için bu örneği izleyin:

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a>VM rezervasyonları için kullanılabilirlik (Azure planı)

Azure VM rezervasyon SKUS'ları için ülkeye göre kullanılabilirlik listesini almak için bu örneği izleyin. Bu örnek, Azure planları için geçerli olan SKUS'lar için geçerlidir:

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-AZR-0145P) abonelikleri için VM rezervasyonları için kullanılabilirlik

Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan Azure VM rezervasyonları için ülkeye göre kullanılabilirlik listesini almak için bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi Kullanılabilirlik kaynaklarının bir [**koleksiyonunu**](product-resources.md#availability) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP Durum Kodu     | Hata kodu   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | İstenen **targetSegment'a erişime** izin verilmiyor.                                                     |

### <a name="response-example-for-azure-vm-reservations-azure-plan"></a>Azure VM rezervasyonları için yanıt örneği (Azure planı)

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

### <a name="response-example-for-new-commerce-license-based-services"></a>Yeni ticari lisans tabanlı hizmetler için yanıt örneği

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir

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
    "id": "CFQ7TTC0K971",
    "productId": "CFQ7TTC0LH18",
    "skuId": "0001",
    "catalogItemId": "CFQ7TTC0LH18:0001:CFQ7TTC0K971",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": true, 
    "renewalInstructions": [
        {
            "applicableTermIds": [
                "5aeco6mffyxo"
            ],
            "renewalOptions": [
                {
                    "renewToId": "CFQ7TTC0LH18:0001",
                    "isAutoRenewable": true
                }
            ]
        },
     …
    ],
    "terms": [
        {
            "id": "5aeco6mffyxo",
            "duration": "P1Y",
            "description": "One-Year commitment for monthly/yearly billing",
            "billingCycle": "Annual",
            "cancellationPolicies": [
                {
                    "refundOptions": [
                        {
                            "sequenceId": 0,
                            "type": "Full",
                            "expiresAfter": "P1D"
                        }
                    ]
                }
            ]
        },
       …
    ],
    "links": {
        "self": {
            "uri": "/products/CFQ7TTC0LH18/skus/0001/availabilities/CFQ7TTC0K971?country=US",
            "method": "GET",
            "headers": []
        }
    },
        "links": {
            "availabilities": {
                "uri": "/products/CFQ7TTC0LH18/skus/0001/availabilities?country=US",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/products/CFQ7TTC0LH18/skus/0001?country=US",
                "method": "GET",
                "headers": []
            }
        }
    }
}
```
