---
title: Envanteri denetle
description: Belirli bir katalog öğeleri kümesinin envanterini denetlemek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Bunu bir müşterinin ürünlerini veya SKU 'Larını belirlemek için yapabilirsiniz.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6921760abc0b95aff820467e84b3e8e9435731cd
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770085"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Iş Ortağı Merkezi API 'Lerini kullanarak Katalog öğelerinin envanterini denetleme

**Uygulama hedefi:**

- İş Ortağı Merkezi

Belirli bir katalog öğeleri kümesinin envanterini denetleme.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir veya daha fazla ürün kimliği. İsteğe bağlı olarak, SKU kimlikleri de belirlenebilir.

- Belirtilen Ürün/SKU KIMLIKLERI tarafından başvurulan SKU 'ları envanterin doğrulanması için gereken ek bağlam. Bu gereksinimler Ürün/SKU türüne göre farklılık gösterebilir ve [SKU](product-resources.md#sku) 'nun **ınventoryvariables** özelliğinden belirlenebilir.

## <a name="c"></a>C\#

Sayımı denetlemek için, denetlenecek her öğe için bir [ınventoryıtem](product-resources.md#inventoryitem) nesnesi kullanarak bir [ınventorycheckrequest](product-resources.md#inventorycheckrequest) nesnesi oluşturun. Ardından bir **ıaggregatepartner. Extensions** erişimcisi kullanın, bunu **ürüne** göre belirleyin ve ardından **bycountry ()** yöntemini kullanarak ülkeyi seçin. Son olarak, **ınventorycheckrequest** nesneniz Ile **checkınventory ()** yöntemini çağırın.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? ülke = {Country-Code} http/1.1                        |

### <a name="uri-parameter"></a>URI parametresi

Stoku denetlemek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ülke kodu           | string   | Yes      | Ülke/bölge KIMLIĞI.                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bir veya daha fazla [ınventoryıtem](product-resources.md#inventoryitem) kaynağı Içeren bir [ınventorycheckrequest](product-resources.md#inventorycheckrequest) kaynağı içeren envanter isteği ayrıntıları.

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi, varsa kısıtlama ayrıntıları ile doldurulmuş bir [ınventoryıtem](product-resources.md#inventoryitem) nesneleri koleksiyonu içerir.

>[!NOTE]
>Bir giriş ınventoryıtem, katalogda bulunamayan bir öğeyi temsil ediyorsa, çıkış koleksiyonuna dahil edilmez.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
