---
title: Kimliğe göre bir ürün alma
description: Ürün kimliği kullanarak belirtilen ürün kaynağını alır.
ms.date: 02/16/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 95821b0f3678d38c75e2f684f7ad629b82f9b43b
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456112"
---
# <a name="get-a-product-by-id"></a>Kimliğe göre bir ürün alma

Ürün kimliği kullanarak belirtilen ürün kaynağını alır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Ürün kimliği.

## <a name="c"></a>C\#

Kimliğine göre belirli bir ürünü bulmak için **IAggregatePartner.Products** koleksiyonu kullanın, **ByCountry()** yöntemini kullanarak ülkeyi seçin ve **ById()** yöntemini arayın. Son olarak, ürünü **iade etmek için Get()** veya **GetAsync()** yöntemini arayın.

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

Kimliğine göre belirli bir ürünü bulmak için **IAggregatePartner.getProducts** işlevinizi kullanın, **byCountry()** işlevini kullanarak ülkeyi seçin ve **byId() işlevini** çağırın. Son olarak, ürünü iade etmek için **get()** işlevini arayın.

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

Kimliğine göre belirli bir ürünü bulmak için [**Get-PartnerProduct komutunu**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) yürütün ve **ProductId parametresini** belirtin. **CountryCode** parametresi seçeneklerdir, belirtilmezse satıcıyla ilişkilendirilmiş ülke kullanılır.

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| **AL** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1  |

### <a name="uri-parameter"></a>URI parametresi

Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| product-id             | string   | Yes      | Ürünü tanımlayan bir dize.                           |
| ülke                | string   | Yes      | Ülke/bölge kimliği.                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt gövdesi bir Ürün [kaynağı](product-resources.md#product) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP Durum Kodu     | Hata kodu   | Description                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| 404                  | 400013       | Ürün bulunamadı.                                                     |

### <a name="response-example-for-azure-vm-reservation-azure-plan"></a>Azure VM rezervasyonu (Azure planı) için yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
### <a name="response-example-for-new-commerce-license-based-product"></a>Yeni ticari lisans tabanlı ürün için yanıt örneği

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticari deneyim teknik önizlemesi kapsamında olan iş ortakları tarafından kullanılabilir

```http
{
    "id": "CFQ7TTC0LH18",
    "title": "Microsoft 365 Business Basic",
    "description": "Best for businesses that need professional email, cloud file storage, and online meetings & chat. Desktop versions of Office apps like Excel, Word, and PowerPoint not included. For businesses with up to 300 employees.",
    "productType": {
        "id": "OnlineServicesNCE",
        "displayName": "OnlineServicesNCE"
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft Corporation",
    "links": {
        "skus": {
            "uri": "/products/CFQ7TTC0LH18/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
        "uri": "/products/CFQ7TTC0LH18?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
