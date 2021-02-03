---
title: Sepet oluşturma
description: Iş Ortağı Merkezi API 'Lerini kullanarak bir sepette müşteri için sipariş ekleme hakkında bilgi edinin. Konu başlığı, bir sepet ve Önkoşullar oluşturma hakkında bilgiler içerir.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a1c559b415a7d42af4e904e09795f92aed7f125f
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770127"
---
# <a name="create-a-cart-with-a-customer-order"></a>Müşteri siparişi içeren bir sepet oluşturma

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir sepetteki bir müşteri için sipariş ekleyebilirsiniz. Şu anda Satım için kullanılabilir olanlar hakkında daha fazla bilgi için bkz. [Cloud Solution Provider programındaki Iş ortağı teklifleri](/partner-center/csp-offers).

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="c"></a>C\#

Bir müşteri için sipariş oluşturmak için:

1. Bir sepet nesnesi örneği oluşturun.

2. **Cartlineıtem** nesnelerinin bir listesini oluşturun ve listeyi sepetin LineItems özelliğine atayın. Her sepet çizgisi öğesi, bir ürünün satın alma bilgilerini içerir. En az bir sepet çizgisi öğesi olmalıdır.

3. Müşteriyi belirlemek için müşteri KIMLIĞI ile **ıaggregatepartner. Customers. Byıd** yöntemini çağırarak ve sonra da **sepet** özelliğinden arabirimi almak için bir arabirim elde edin.

4. Sepetini oluşturmak için **Create** veya **createasync** metodunu çağırın.

### <a name="c-example"></a>C \# örneği

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

var cart = new Cart()
{
    LineItems = new List<CartLineItem>()
    {
        new CartLineItem()
        {
      /* Microsoft Azure Subscription */
            Id = 0,
            CatalogItemId = "MS-AZR-0145P",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1Y"
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 1,
            CatalogItemId = "DZH318Z0BQ36:004G:DZH318Z08C0S",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P1Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Azure Reserved Instance */
            Id = 2,
            CatalogItemId = "DZH318Z0BQ36:004J:DZH318Z08B8X",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime,
            TermDuration = "P3Y",
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", subscriptionId },
                { "scope", "shared" }
            }
        },
        new CartLineItem()
        {
      /* Perpetual Software */
            Id = 3,
            CatalogItemId = "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
            Quantity = 1,
            BillingCycle = BillingCycleType.OneTime
        },
        new CartLineItem()
        {
      /* SaaS */
            Id = 4,
            CatalogItemId = "DZH318Z0BXWC:0002:DZH318Z0BMRV",
            Quantity = 1,
            BillingCycle = BillingCycleType.Monthly,
            TermDuration = "P1M"
        },
        new CartLineItem()
        {
      /* SaaS Free Trial */
            Id = 5,
            CatalogItemId = "DZH318Z0C0WF:0001:DZH318Z0BP69",
            Quantity = 10,
            BillingCycle = BillingCycleType.None,
            TermDuration = "P1M",
            RenewsTo = new RenewsTo
            {
                TermDuration = "P1Y"
            }
        }
    }
};

cart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Bir müşteri için sipariş oluşturmak için:

1. Bir sepet nesnesi örneği oluşturun.

2. **Cartlineıtem** nesnelerinin bir listesini oluşturun ve listeyi sepetinin çizgi öğelerine atayın. Her sepet çizgisi öğesi, bir ürünün satın alma bilgilerini içerir. En az bir sepet çizgisi öğesi olmalıdır.

3. Müşteriyi belirlemek için müşteri KIMLIĞIYLE **ıaggregatepartner. getCustomers (). Byıd** işlevini çağırarak ve sonra **getcart** işlevinden arabirimi alarak, işlem yapmak için bir arabirim elde edin.

4. Sepetini oluşturmak için **Oluştur** işlevini çağırın.

## <a name="java-example"></a>Java örneği

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String subscriptionId;
// String catalogItemId;

CartLineItem lineItem = new CartLineItem();

lineItem.setBillingCycle(BillingCycleType.OneTime);
lineItem.setCatalogItemId(catalogItemId);
lineItem.setFriendlyName("Sample RI Purchase");
lineItem.setQuantity(1);

Map<String, String> provisioningContext = new HashMap<String,String>();

provisioningContext.put("duration", "3Years");
provisioningContext.put("scope", "shared");
provisioningContext.put("subscriptionId", subscriptionId);

lineItem.setProvisioningContext(provisioningContext);

List<CartLineItem> lineItemList = new ArrayList<CartLineItem>();
lineItemList.add(lineItem);

Cart cart = new Cart();
cart.setLineItems(lineItemList);

Cart cartCreated = partnerOperations.getCustomers().byId(customerId).getCarts().create(cart);
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Bir müşteri için sipariş oluşturmak için:

1. Bir sepet nesnesi örneği oluşturun.

2. **Cartlineıtem** nesnelerinin bir listesini oluşturun ve listeyi sepetinin çizgi öğelerine atayın. Her sepet çizgisi öğesi, bir ürünün satın alma bilgilerini içerir. En az bir sepet çizgisi öğesi olmalıdır.

3. Sepetini oluşturmak için [**New-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomerCart.md) komutunu yürütün.

```powershell
# $customerId
# $subscriptionId
# $catalogItemId

$lineItem = New-Object -TypeName Microsoft.Store.PartnerCenter.PowerShell.Models.Carts.PSCartLineItem

$lineItem.BillingCycle = 'OneTime'
$lineItem.CatalogItemId = $catalogItemId
$lineItem.FriendlyName = 'Sample RI Purchase'
$lineItem.ProvisioningContext.Add('duration', '1Year')
$lineItem.ProvisioningContext.Add('scope', 'shared')
$lineItem.ProvisioningContext.Add('subscriptionId', $subsciptionId)
$lineItem.Quantity = 10

New-PartnerCustomerCart -CustomerId $customerId -LineItems $lineItem
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts http/1.1                        |

### <a name="uri-parameter"></a>URI parametresi

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad            | Tür     | Gerekli | Açıklama                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **müşteri kimliği** | string   | Yes      | Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.             |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde [sepet](cart-resources.md) özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| kimlik                    | dize           | No              | Sepet başarıyla oluşturulduktan sonra sağlanan bir sepet tanımlayıcısı.                                  |
| creationTimeStamp     | DateTime         | No              | Sepetin oluşturulduğu tarih ve saat biçimi. Sepet başarıyla oluşturulduktan sonra uygulandı.         |
| lastModifiedTimeStamp | DateTime         | No              | Sepetin son güncelleştirildiği tarih ve saat biçimi. Sepet başarıyla oluşturulduktan sonra uygulandı.    |
| expirationTimeStamp   | DateTime         | No              | Sepetin süresinin dolacağı tarih-saat biçiminde.  Sepet başarıyla oluşturulduktan sonra uygulandı.            |
| lastModifiedUser      | dize           | No              | Sepetini son güncelleştiren Kullanıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                             |
| LineItems             | Nesne dizisi | Yes             | Bir [Cartlineıtem](cart-resources.md#cartlineitem) kaynakları dizisi.                                     |

Bu tablo, istek gövdesinde [Cartlineıtem](cart-resources.md#cartlineitem) özelliklerini açıklar.

|      Özellik       |            Tür             | Gerekli |                                                                                         Açıklama                                                                                         |
|---------------------|-----------------------------|----------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|         kimlik          |           dize            |    No    |                                                     Sepet çizgisi öğesi için benzersiz bir tanımlayıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                                                     |
|      catalogId      |           string            |   Yes    |                                                                                Katalog öğesi tanımlayıcısı.                                                                                 |
|    friendlyName     |           dize            |    No    |                                                    İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                                                    |
|      miktar       |             int             |   Yes    |                                                                            Lisans veya örnek sayısı.                                                                             |
|    currencyCode     |           dize            |    No    |                                                                                     Para birimi kodu.                                                                                      |
|    Bilimlingcycle     |           Nesne            |   Yes    |                                                                    Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                                                    |
|    Katılımcılar     | Nesne dizesi çiftlerinin listesi |    No    |                                                                Satınalmada iş ortağı kimliği koleksiyonu (MPNıD).                                                                 |
| provisioningContext | Sözlük<dize, dize>  |    No    | Katalogdaki bazı öğelerin sağlanması için gereken bilgiler. SKU 'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir. |
|     orderGroup      |           dize            |    No    |                                                                   Hangi öğelerin birlikte yerleştirilebileceğini belirten bir grup.                                                                   |
|        error        |           Nesne            |    No    |                                                                     Bir hata durumunda sepet oluşturulduktan sonra uygulandı.                                                                      |
|     renewsTo        | Nesne dizisi            |    No    |                                                    [RenewsTo](cart-resources.md#renewsto) kaynaklarından oluşan bir dizi.                                                                            |

Bu tablo, istek gövdesinde [RenewsTo](cart-resources.md#renewsto) özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | dize           | No              | Yenileme teriminin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl). |

### <a name="request-example"></a>İstek örneği

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
  "lineItems": [
    {
    /* Microsoft Azure Subscription */
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1Y"
    },
    {
    /* Azure Reserved Instance */
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      }
    },
    {
    /* Azure Reserved Instance */
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "single"
      }
    },
    {
    /* Perpetual Software */
      "id": 3,
      "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSFM",
      "quantity": 1,
      "billingCycle": "one_time"
    },
    {
    /* SaaS */
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "billingCycle": "monthly",
      "termDuration": "P1M"
    },
  {
    /* SaaS Free Trial */
       "id": 5,
       "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
       "quantity": 10,
       "billingCycle": "none",
       "termDuration": "P1M",
       "renewsTo": {
         "termDuration": "P1Y"
       }
    }
  ]
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [sepet](cart-resources.md) kaynağını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
  "id": "3655b1a0-b1c9-4268-9824-577fdbc4d0be",
  "creationTimestamp": "2019-01-16T00:45:41.6062996Z",
  "lastModifiedTimestamp": "2019-01-16T00:45:41.6062996Z",
  "expirationTimestamp": "2019-01-16T01:00:54.4188497Z",
  "lastModifiedUser": "1824b7fc-2fac-4478-b177-66823c40ab75",
  "status": "Active",
  "lineItems": [
    {
      "id": 0,
      "catalogItemId": "MS-AZR-0145P",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1Y",
      "orderGroup": "OMS-0"
    },
    {
      "id": 1,
      "catalogItemId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P1Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 2,
      "catalogItemId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "termDuration": "P3Y",
      "provisioningContext": {
        "subscriptionId": "1C461A25-F729-4FA5-AADB-280947DD05E8",
        "scope": "shared"
      },
      "orderGroup": "0"
    },
    {
      "id": 3,
      "catalogItemId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "one_time",
      "orderGroup": "0"
    },
    {
      "id": 4,
      "catalogItemId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
      "quantity": 1,
      "currencyCode": "USD",
      "billingCycle": "monthly",
      "termDuration": "P1M",
      "orderGroup": "1"
    },
  {
      "id": 5,
      "catalogItemId": "DZH318Z0C0WF:0001:DZH318Z0BP69",
      "quantity": 10,
      "currencyCode": "USD",
      "billingCycle": "none",
      "termDuration": "P1M",
      "renewsTo": {
  "termDuration": "P1Y"
      },
    "orderGroup": "2"
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/28045616-f6b9-462f-9701-0d89b5e65c44/carts/3655b1a0-b1c9-4268-9824-577fdbc4d0be",
      "method": "GET",
      "headers": []
    }
  },
  "attributes": {
    "objectType": "Cart"
  }
}
```
