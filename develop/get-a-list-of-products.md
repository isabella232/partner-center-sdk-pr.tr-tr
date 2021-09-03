---
title: Ürünlerin bir listesini alma (ülkeye göre)
description: Ürün kaynağını, müşteri ülkesine göre ürünlerin koleksiyonunu almak için kullanabilirsiniz.
ms.date: 02/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 601fc2c8012d92d6964f0aaa29a3a46d732df300
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123456061"
---
# <a name="get-a-list-of-products-by-country"></a>Ürünlerin bir listesini alma (ülkeye göre)

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Belirli bir ülkede bulunan ürünlerin bir koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir ülke.

## <a name="c"></a>C\#

Ürünlerin bir listesini almak için:

1. **Bycountry ()** yöntemini kullanarak ülkeyi seçmek Için **ıaggregatepartner. Products** koleksiyonunuzu kullanın.

2. **Bytargetview ()** yöntemini kullanarak katalog görünümünü seçin.

3. Seçim **Byrezervationscope ()** yöntemini kullanarak ayırma kapsamını seçin.

4. Seçim **Bytargetsegment ()** yöntemini kullanarak hedef segmenti seçin.

5. Koleksiyonu döndürmek için **Get ()** veya **GetAsync ()** metodunu çağırın.

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Ürünlerin bir listesini almak için:

1. **Bycountry ()** işlevini kullanarak ülkeyi seçmek Için **ıaggregatepartner. GetProducts** işlevinizi kullanın.

2. **Bytargetview ()** işlevini kullanarak katalog görünümünü seçin.
3. Seçim **Bytargetsegment ()** işlevini kullanarak hedef segmenti seçin.

4. Koleksiyonu döndürmek için **Get ()** işlevini çağırın.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Ürünlerin bir listesini almak için:

1. [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) komutunu yürütün.

2. **Katalog parametresini belirterek** kataloğu seçin.
3. Seçim **Segment** parametresini belirterek hedef segmenti seçin.

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **AL** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products? ülke = {country} &targetview = {targetview} &targetsegment = {TARGETSEGMENT} http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Ürünlerin bir listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| ülke                | string   | Yes      | Ülke/bölge KIMLIĞI.                                                  |
| targetView             | string   | Yes      | Kataloğun hedef görünümünü tanımlar. Desteklenen değerler şunlardır: <br/><br/>Tüm Azure öğelerini içeren **Azure**<br/><br/>Tüm Azure ayırma öğelerini içeren **Azurereservations**<br/><br/>Tüm sanal makine (VM) rezervasyon öğelerini içeren **Azurereservationsvm**<br/><br/>tüm SQL ayırma öğelerini içeren **azurereservationssql**<br/><br/>tüm Cosmos veritabanı ayırma öğelerini içeren **azurereservationscosmosdb**<br/><br/>Microsoft Azure aboneliklerine (**MS-azr-0145p**) ve Azure planlarına yönelik öğeler içeren **MicrosoftAzure**<br/><br/>Tüm çevrimiçi hizmet öğelerini içeren **OnlineServices**. Bu targetView, ticari Market, geleneksel lisans tabanlı hizmetler ve yeni ticaret lisansı tabanlı hizmetler içerir<br/><br/>Tüm yazılım öğelerini içeren **yazılım**<br/><br/>Tüm yazılım SUSE Linux öğelerini içeren **SoftwareSUSELinux**<br/><br/>Tüm kalıcı yazılım öğelerini içeren **Softwarekalıcı**<br/><br/>Tüm yazılım aboneliği öğelerini içeren **SoftwareSubscriptions**    |
| targetSegment          | dize   | No       | Hedef segmenti tanımlar. Farklı hedef kitlelerinin görünümü. Desteklenen değerler şunlardır: <br/><br/>**seniz**<br/>**öğrenim**<br/>**Devlet**<br/>**kar amacı gütmeyen**  |
| Rezervationscope | dize   | No | Azure ayırmaları için bir ürün listesi sorgulanırken, `reservationScope=AzurePlan` Azure planlarına uygun ürünlerin bir listesini almak için belirtin. Microsoft Azure (**MS-azr-0145p**) abonelikleri için geçerli olan Azure ayırmaları ürünlerinin bir listesini almak için bu parametreyi dışlayın.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-examples"></a>İstek örnekleri

#### <a name="products-by-country"></a>Ülkeye göre ürünler

Microsoft Azure (MS-azr-0145p) abonelikleri ve Azure planları için ülkeye göre ürünlerin bir listesini almak üzere bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Azure VM ayırmaları (Azure planı)

Azure planlarına uygun Azure VM ayırmaları için ülkeye göre ürünlerin bir listesini almak için bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure için Azure VM ayırmaları (MS-azr-0145p) abonelikleri

Microsoft Azure (MS-azr-0145p) abonelikleri için geçerli olan Azure VM ayırmaları ülkeye göre ürünlerin bir listesini almak için bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="new-commerce-license-based-services"></a>Yeni ticaret lisansı tabanlı hizmetler

> [!Note] 
> Yeni ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinin parçası olan iş ortakları tarafından kullanılabilir

Yeni ticaret deneyimi teknik önizlemesinin bir parçası olarak yeni ticari lisans tabanlı hizmetlere ülkeye göre ürünlerin bir listesini almak için bu örneği izleyin. Yeni ticaret lisansı tabanlı hizmetler, **Onlineservicesnce**'nin ID ve DisplayNames değerleriyle belirlenir. Aşağıdaki yanıt örneğine bakın.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=OnlineServices HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [**ürün**](product-resources.md#product) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP durum kodu     | Hata kodu   | Description                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | İstenen targetSegment erişimine izin verilmiyor.                                                     |
| 403                  | 400036       | İstenen targetView 'a erişime izin verilmiyor.                                                        |

### <a name="response-example-for-azure-vm-reservations-azure-plan"></a>Azure VM ayırmaları için yanıt örneği (Azure planı)

```http
{
    "totalCount": 19,
    "items": [
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
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="response-example-for-new-commerce-license-based-services"></a>Yeni ticaret lisansı tabanlı hizmetler için yanıt örneği

> [!Note] 
> Yeni ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinin parçası olan iş ortakları tarafından kullanılabilir

```http
{
  "totalCount": 19,
  "items": [{
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
    },
    ...
  ],
  "links": {
    "self": {
      "uri": "/products?country=US&targetView=OnlineServices",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```

