---
title: Envanteri denetleme
description: Belirli bir katalog İş Ortağı Merkezi envanterini kontrol etmek için api'leri kullanmayı öğrenin. Bir müşterinin ürünlerini veya SKUS'larını belirlemek için bunu yapabiliriz.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: de931c7dd89f94b6be8fdaf0ad79c8faee268267c35a2c0f8e38d36b97842f3f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992118"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a>Api'leri kullanarak katalog öğelerinin İş Ortağı Merkezi denetleme

Belirli bir katalog öğeleri kümesi için envanteri denetleme.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Bir veya daha fazla ürün kimlikleri. İsteğe bağlı olarak, SKU kimlikleri de belirtilebilir.

- Sağlanan ürün/SKU kimlikleri tarafından başvurulan SKU'ların envanterini doğrulamak için gereken ek bağlam. Bu gereksinimler ürün/SKU türüne göre değişiklik gösterebilir ve [SKU'nun](product-resources.md#sku) **InventoryVariables özelliğinden belirlenebilir.**

## <a name="c"></a>C\#

Envanteri kontrol etmek için, denetlenen her öğe için [bir InventoryItem](product-resources.md#inventoryitem) nesnesi kullanarak bir [InventoryCheckRequest](product-resources.md#inventorycheckrequest) nesnesi derleme. Ardından bir **IAggregatePartner.Extensions** erişimcisi kullanın, **kapsamı Product** olarak sildiniz ve **ByCountry()** yöntemini kullanarak ülkeyi seçin. Son olarak **InventoryCheckRequest** nesneniz ile **CheckInventory()** yöntemini çağırabilirsiniz.

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

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1                        |

### <a name="uri-parameter"></a>URI parametresi

Envanteri kontrol etmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| ülke kodu           | string   | Yes      | Ülke/bölge kimliği.                                            |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bir veya daha fazla [InventoryItem](product-resources.md#inventoryitem) kaynağı içeren [inventoryCheckRequest](product-resources.md#inventorycheckrequest) kaynağından oluşan envanter isteği ayrıntıları.

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

Başarılı olursa yanıt gövdesi, varsa kısıtlama ayrıntılarıyla doldurulmuş [bir InventoryItem](product-resources.md#inventoryitem) nesneleri koleksiyonu içerir.

>[!NOTE]
>InventoryItem girişi katalogda buluna bir öğeyi temsil ediyorsa, çıkış koleksiyonuna dahil olmaz.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)

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
