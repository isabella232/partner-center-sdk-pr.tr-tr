---
title: Bir ürüne ait SKU’ların listesini alma (ülkeye göre)
description: Iş Ortağı Merkezi API 'Lerini kullanarak bir ürün için ülkeye göre STB koleksiyonu alabilir ve filtreleyebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 27a2391a22a9439461fb53764b87c1cafa68b875
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873896"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a>Bir ürüne ait SKU’ların listesini alma (ülkeye göre)

Iş Ortağı Merkezi API 'Lerini kullanarak belirli bir ürün için bir ülkede bulunan SKU 'ların bir koleksiyonunu edinebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir ürün tanımlayıcısı.

## <a name="c"></a>C\#

Bir ürüne ait SKU 'ların listesini almak için:

1. [Kimliğe göre ürün edinme](get-a-product-by-id.md)bölümündeki adımları izleyerek belirli bir ürünün işlemlerine yönelik bir arabirim alın.

2. Arabirimde, SKU 'Lar için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **SKU 'ları** özelliğini seçin.

3. Ürün için kullanılabilir SKU 'ların bir koleksiyonunu almak için **Get ()** veya **GetAsync ()** metodunu çağırın.

4. Seçim **Byrezervationscope ()** yöntemini kullanarak ayırma kapsamını seçin.

5. Seçim **Get ()** veya **GetAsync ()** çağrısı yapmadan önce SKU 'ları hedef kesimine göre filtrelemek için **bytargetsegment ()** yöntemini kullanın.

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Bir ürüne ait SKU 'ların listesini almak için:

1. [Kimliğe göre ürün edinme](get-a-product-by-id.md)bölümündeki adımları izleyerek belirli bir ürünün işlemlerine yönelik bir arabirim alın.

2. Arabirimde, SKU 'Lar için kullanılabilir işlemleri içeren bir arabirim edinmek üzere **GetSku 'ları** işlevini seçin.

3. Ürün için kullanılabilir SKU 'ların bir koleksiyonunu almak için **Get ()** işlevini çağırın.

4. Seçim **Get ()** işlevini çağırmadan önce STB 'leri hedef kesimine göre filtrelemek Için **bytargetsegment ()** işlevini kullanın.

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Bir ürüne ait SKU 'ların listesini almak için:

1. [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) komutunu yürütün.

2. Seçim SKU 'Ları hedef kesimine göre filtrelemek için **segment** parametresini belirtin.

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKU 'ları? ülke = {Country-code} &targetsegment = {Target-segment} http/1.1  |

#### <a name="uri-parameters"></a>URI parametreleri

Bir ürüne yönelik SKU 'ların listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ürün kimliği             | string   | Yes      | Ürünü tanımlayan bir dize.                           |
| ülke kodu           | string   | Yes      | Ülke/bölge KIMLIĞI.                                            |
| hedef segment         | dize   | No       | Filtreleme için kullanılan hedef segmenti tanımlayan bir dize. |
| Rezervationscope | dize   | No | Bir Azure rezervasyon ürününe yönelik SKU 'ların listesini sorgularken, `reservationScope=AzurePlan` Azuplanlamada geçerli olan SKU 'ların listesini almak için belirtin. Microsoft Azure (MS-azr-0145p) abonelikleri için geçerli olan Azure rezervasyon ürünleri sku 'larının listesini almak için bu parametreyi dışlayın.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-examples"></a>İstek örnekleri

Belirli bir ürün için SKU 'ların listesini alın:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Bir Azure rezervasyon ürününe ait SKU 'ların listesini alın. yalnızca Azure planlarına uygulanabilen ve Microsoft Azure (MS-azr-0145p) abonelikleri için geçerli olan sku 'ları dahil et:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

Bir Azure rezervasyon ürününe ait SKU 'ların listesini alın. yalnızca Microsoft Azure (MS-azr-0145p) abonelikleri için geçerli olan sku 'ları (Azure planlarına değil) dahil edin:

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [SKU](product-resources.md#sku) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP durum kodu     | Hata kodu   | Açıklama                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | İstenen targetSegment erişimine izin verilmiyor.                                                     |
| 404                  | 400013       | Üst ürün bulunamadı.                                                                         |

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
            "minimumQuantity": 1,
            "maximumQuantity": 999999999,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "AzureSubscriptionRegistration",
                "InventoryCheck"
            ],
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
