---
title: Kimliğe göre bir SKU alma
description: Belirtilen SKU kimliğini kullanarak belirtilen ürün için bir SKU elde.
ms.date: 02/16/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: bc7036467142d666aed6e9f41b86b1c2d2f0c8ec
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456129"
---
# <a name="get-a-sku-by-id"></a>Kimliğe göre bir SKU alma

Belirtilen SKU kimliğini kullanarak belirtilen ürün için bir SKU alır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Ürün kimliği.

- SKU Kimliği.

## <a name="c"></a>C\#

Belirli bir SKU'nun ayrıntılarını almak için, [](get-a-product-by-id.md) Belirli bir ürünün işlemlerinin arabirimini almak için Kimle ürün al adımlarını izleyin. Elde edilen arabirimden **SKU'lar** özelliğini seçerek SKU'lar için kullanılabilir işlemlere sahip bir arabirim elde edin. SKU Kimliğini **ById()** yöntemine geçin ve SKU ayrıntılarını almak **için Get()** veya **GetAsync()** çağrısında bulundurabilirsiniz.

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| **AL** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1   |

### <a name="uri-parameter"></a>URI parametresi

Belirtilen SKU kimliğini kullanarak belirtilen ürün için bir SKU almak üzere aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| product-id             | string   | Yes      | Ürünü tanımlayan bir dize.                           |
| sku-id                 | string   | Yes      | SKU'ları tanımlayan bir dize.                               |
| ülke kodu           | string   | Yes      | Ülke/bölge kimliği.                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt gövdesi bir [SKU kaynağı](product-resources.md#sku) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP Durum Kodu     | Hata kodu   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 404                  | 400013       | Ürün bulunamadı.                                                                                    |
| 404                  | 400018       | Sku bulunamadı.                                                                                        |

### <a name="response-example-for-azure-vm-reservations-azure-plan"></a>Azure VM rezervasyonları için yanıt örneği (Azure planı)

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
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
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
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
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "id": "0001",
    "productId": "CFQ7TTC0LH18",
    "title": "Microsoft 365 Business Basic",
    "description": "Best for businesses that need professional email, cloud file storage, and online meetings & chat. Desktop versions of Office apps like Excel, Word, and PowerPoint not included. For businesses with up to 300 employees.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "isTrial": false,
    "supportedBillingCycles": [
        "annual",
        "monthly"
    ],
    "purchasePrerequisites": [
        "MicrosoftCloudAgreement"
    ],
    "inventoryVariables": [],
    "provisioningVariables": [],
    "actions": [
        "Refund"
    ],
    "dynamicAttributes": {
        "isMicrosoftProduct": true,
        "hasConstraints": true,
        "isAddon": false,
        "prerequisiteSkus": [],
        "isSoftwareAssuranceApplicable": false,
        "upgradeTargetOffers": [
            "CFQ7TTC0LDPB:0001",
            "CFQ7TTC0LF8Q:0001"
…
        ],
        "provisioningId": "3b555118-da6a-4418-894f-7df1e2096870",
        "internal": false
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
```
