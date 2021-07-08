---
title: Ürünlerin bir listesini alma (ülkeye göre)
description: Ürün kaynağını kullanarak müşteri ülkesine göre bir ürün koleksiyonu elde etmek için kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1258727ecbe7c5cc332624577fa8a355e28e3717
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874219"
---
# <a name="get-a-list-of-products-by-country"></a>Ürünlerin bir listesini alma (ülkeye göre)

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Belirli bir ülkede kullanılabilen ürün koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Ülke.

## <a name="c"></a>C\#

Ürünlerin listesini almak için:

1. **ByCountry()** yöntemini kullanarak ülkeyi seçmek için **IAggregatePartner.Products** koleksiyonu kullanın.

2. **ByTargetView() yöntemini kullanarak katalog görünümünü** seçin.

3. (İsteğe bağlı) **ByReservationScope() yöntemini kullanarak rezervasyon kapsamını** seçin.

4. (İsteğe bağlı) **ByTargetSegment() yöntemini kullanarak hedef segmenti** seçin.

5. Koleksiyonu geri **almak için Get()** **veya GetAsync()** yöntemini çağırma.

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

Ürünlerin listesini almak için:

1. **byCountry()** işlevini kullanarak ülkeyi seçmek için **IAggregatePartner.getProducts** işlevinizi kullanın.

2. **byTargetView() işlevini kullanarak katalog görünümünü** seçin.
3. (İsteğe bağlı) **byTargetSegment() işlevini kullanarak hedef segmenti** seçin.

4. Koleksiyonu geri **almak için get()** işlevini çağırma.

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Ürünlerin listesini almak için:

1. [**Get-PartnerProduct komutunu**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) yürütün.

2. **Katalog** parametresini belirterek kataloğu seçin.
3. (İsteğe bağlı) Segment parametresini belirterek hedef **segmenti** seçin.

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Ürünlerin listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| ülke                | string   | Yes      | Ülke/bölge kimliği.                                                  |
| targetView             | string   | Yes      | Kataloğun hedef görünümünü tanımlar. Desteklenen değerler: <br/><br/>**Tüm Azure** öğelerini içeren Azure<br/><br/>Tüm Azure rezervasyon öğelerini içeren **AzureReservations**<br/><br/>Tüm sanal makine (VM) rezervasyon öğelerini içeren **AzureReservationsVM**<br/><br/>**Tüm rezervasyon öğelerini içeren AzureReservationsSQL** SQL öğeleri<br/><br/>**Tüm veritabanı rezervasyon öğelerini içeren AzureReservationsCosmosDb** Cosmos öğeleri<br/><br/>Microsoft Azure abonelikleri (**MS-AZR-0145P**) ve Azure planları için öğeleri içeren **MicrosoftAzure**<br/><br/>Tüm çevrimiçi hizmet öğelerini (ticari market ürünleri dahil) içeren **OnlineServices**<br/><br/>**Yazılım**, tüm yazılım öğelerini içerir<br/><br/>**SoftwareSUSELinux**, tüm yazılım SUSE Linux öğelerini içerir<br/><br/>Tüm kalıcı yazılım öğelerini içeren **SoftwarePerpetual**<br/><br/>Tüm yazılım aboneliği öğelerini içeren **YazılımAubscriptions**    |
| targetSegment          | dize   | No       | Hedef segmenti tanımlar. Farklı hedef kitlelere yönelik görünüm. Desteklenen değerler: <br/><br/>**Ticari**<br/>**Eğitim**<br/>**Hükümet**<br/>**Kar amacı gütme -yen**  |
| reservationScope | dize   | No | Azure Rezervasyonları için ürünlerin listesini sorgularken, Azure planları için `reservationScope=AzurePlan` geçerli olan ürünlerin listesini almak için belirtin. Microsoft Azure (**MS-AZR-0145P**) abonelikleri için geçerli olan Azure rezervasyonlarının ürünlerinin listesini almak için bu parametreyi hariç tutabilirsiniz.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-examples"></a>İstek örnekleri

#### <a name="products-by-country"></a>Ülkeye göre ürünler

Microsoft Azure (MS-AZR-0145P) abonelikleri ve Azure planları için ülkeye göre ürünlerin listesini almak için bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a>Azure VM rezervasyonları (Azure planı)

Azure planları için geçerli olan Azure VM rezervasyonları için ülkeye göre ürünlerin listesini almak için bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a>Microsoft Azure (MS-AZR-0145P) abonelikleri için Azure VM rezervasyonları

Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan Azure VM rezervasyonları için ülkeye göre ürünlerin listesini almak için bu örneği izleyin.

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt gövdesi bir Ürün kaynakları [**koleksiyonu**](product-resources.md#product) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP Durum Kodu     | Hata kodu   | Açıklama                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| 403                  | 400030       | İstenen targetSegment'a erişime izin verilmiyor.                                                     |
| 403                  | 400036       | İstenen targetView 'a erişime izin verilmiyor.                                                        |

### <a name="response-example"></a>Yanıt örneği

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
