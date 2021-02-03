---
title: Eklentilerle bir sepet oluşturma
description: Bir sepet aracılığıyla eklentilere bir müşteri siparişi eklemek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makalesinde, eklentilerle bir sepet oluşturmak için önkoşulları ve adımları paylaşır.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 81c41405a2f56eb4d1d3447d14b93e05d550cc70
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770132"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Eklentiler ile müşteri siparişi arasında bir sepet oluşturma

**Uygulama hedefi:**

- İş Ortağı Merkezi

Eklentileri bir sepet aracılığıyla satın alabilirsiniz. Şu anda Satım için kullanılabilir olanlar hakkında daha fazla bilgi için bkz. [Cloud Solution Provider programındaki Iş ortağı teklifleri](/partner-center/csp-offers).

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="c"></a>C\#

Bir sepet, temel teklifin ve bunlara karşılık gelen eklentilerin satın alınmasını sağlar. Bir sepet oluşturmak için aşağıdaki adımları izleyin:

1. Bir [**sepet**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) nesnesi örneği oluşturun.

2. Taban teklifleri temsil eden [**Cartlineıtem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) nesnelerinin bir listesini oluşturun ve listeyi sepetinin [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) özelliğine atayın.

3. Her temel teklifin sepet çizgisi öğesi altında, **Addonıtems** listesini her biri temel teklifte satın alınacak eklentiyi temsil eden diğer **Cartlineıtem** nesneleriyle doldurun.

4. [**Iaggregatepartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) kullanarak, müşteriyi tanımlamak üzere [**ıustomercollection. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırmak ve sonra da bu arabirimi **sepet** özelliğinden almak için bir arabirim elde edin.

5. Son olarak, sepet oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) metodunu çağırın.

### <a name="c-example"></a>C \# örneği

```csharp
// IAggregatePartner partnerOperations;
// string customerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "A_base_offer_ID",
                FriendlyName = "Myofferpurchase",
                Quantity = 3,
                BillingCycle = BillingCycleType.Monthly,
                AddonItems = new List<CartLineItem>
                {
                    new CartLineItem
                    {
                        Id = 1,
                        CatalogItemId = "An_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 2,
                    },
                    new CartLineItem
                    {
                        Id = 2,
                        CatalogItemId = "Another_addon_item_ID",
                        BillingCycle = BillingCycleType.Monthly,
                        Quantity = 3
                    }
                }
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(customerId).Carts.Create(cart);
```

Eklentilerin mevcut temel abonelikler için satın alınmasını sağlayacak bir sepet oluşturmak için bu adımları izleyin:

1. "Parentsubscriptionıd" anahtarıyla **Provisioningcontext** ÖZELLIĞINDEKI abonelik kimliğini içeren yeni bir **Cartlineıtem** içeren bir **sepet** oluşturun.

2. **Create** veya **createasync** metodunu çağırın.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var cart = new Cart()
    {
        LineItems = new List<CartLineItem>()
        {
            new CartLineItem()
            {
                Id = 0,
                CatalogItemId = "An_addon_item_ID",
                ProvisioningContext = new Dictionary<string, string>
                {
                    {
                        "ParentSubscriptionId", "An_existing_subscription_Id"
                    }
                },
                Quantity = 1,
                BillingCycle = BillingCycleType.Annual,
            }
        }
    };

var createdCart = partnerOperations.Customers.ById(selectedCustomerId).Carts.Create(cart);
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts http/1.1                        |

#### <a name="uri-parameter"></a>URI parametresi

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
| LineItems             | Nesne dizisi | Yes             | Bir [Cartlineıtem](cart-resources.md#cartlineitem) kaynakları dizisi.                                             |

Bu tablo, istek gövdesinde [Cartlineıtem](cart-resources.md#cartlineitem) özelliklerini açıklar.

| Özellik             | Tür                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                   | string                           | Sepet çizgisi öğesi için benzersiz bir tanımlayıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                                                                   |
| catalogId            | string                           | Katalog öğesi tanımlayıcısı.                                                                                                                          |
| friendlyName         | string                           | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                                                                 |
| miktar             | int                              | Lisans veya örnek sayısı.                                                                                                                  |
| currencyCode         | string                           | Para birimi kodu.                                                                                                                                    |
| Bilimlingcycle         | Nesne                           | Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                                                                                 |
| Katılımcılar         | Nesne dizesi çiftlerinin listesi      | Satınalmada iş ortağı kimliği koleksiyonu (MPNıD).                                                                                          |
| provisioningContext  | Sözlük<dize, dize>       | Teklifin sağlanması için kullanılan bir bağlam.                                                                                                             |
| orderGroup           | string                           | Hangi öğelerin birlikte yerleştirilebileceğini belirten bir grup.                                                                                               |
| Addonıtems           | **Cartlineıtem** nesnelerinin listesi | Ana sepet çizgisi öğesinin satın alma işleminden kaynaklanan temel aboneliğe yönelik olarak satın alınacak eklentiler için sepet çizgisi öğeleri koleksiyonu. |
| error                | Nesne                           | Bir hata durumunda sepet oluşturulduktan sonra uygulandı.                                                                                                    |

### <a name="request-example-new-base-subscription"></a>İstek örneği (yeni temel abonelik)

Aşağıdaki REST örneği, yeni bir temel abonelik için eklenti öğelerine sahip bir sepet oluşturmayı gösterir.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "FriendlyName":"Myofferpurchase",
            "Quantity":3,
            "BillingCycle":"monthly",
            "AddonItems": [
                {
                    "Id":1,
                    "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "Quantity":2,
                    "BillingCycle":"monthly"
                },
                {
                    "Id":2,
                    "CatalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "Quantity":3,
                    "BillingCycle":"monthly"
                }
            ]
        }
    ]
}
```

#### <a name="request-example-existing-base-subscription"></a>İstek örneği (varolan temel abonelik)

Aşağıdaki REST örneği, mevcut bir temel aboneliğe eklentilerin nasıl ekleneceğini göstermektedir.

```http
POST https://api.partnercenter.microsoft.com/v1/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b

{
    "LineItems": [
        {
            "Id":0,
            "CatalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "Quantity":1,
            "BillingCycle":"annual",
            "ProvisioningContext":{"ParentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"}
        }
    ]
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [sepet](cart-resources.md) kaynağını döndürür.

#### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

#### <a name="response-example-new-base-subscription"></a>Yanıt örneği (yeni temel abonelik)

```http
HTTP/1.1 201 Created
Content-Length: 958
Content-Type: application/json
MS-CorrelationId: f73baf70-bbc3-43d0-8b29-dffa08ff9511
MS-RequestId: f931348a-6312-47d0-a8dd-31a386dedb8f
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:29:05 GMT

{
    "id":"dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
    "creationTimestamp":"2018-11-01T22:29:03.6900182Z",
    "lastModifiedTimestamp":"2018-11-01T22:29:03.6900182Z",
    "expirationTimestamp":"2018-11-01T22:44:05.0025799Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "friendlyName":"Myofferpurchase",
            "quantity":3,
            "currencyCode":"USD",
            "billingCycle":"monthly",
            "orderGroup":"OMS-0",
            "addonItems": [
                {
                    "id":1,
                    "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
                    "quantity":2,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                },
                {
                    "id":2,
                    "catalogItemId":"43FCE491-76D1-4BCC-B709-8A288786DBAE",
                    "quantity":3,
                    "currencyCode":"USD",
                    "billingCycle":"monthly",
                    "orderGroup":"OMS-0"
                }
            ]
        }
],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/dbe2f8d4-f21d-43e2-9356-cff6387c4ba1",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```

#### <a name="response-example-existing-base-subscription"></a>Yanıt örneği (varolan temel abonelik)

```http
HTTP/1.1 201 Created
Content-Length: 707
Content-Type: application/json
MS-CorrelationId: 182474ba-7303-4d0f-870a-8c7fba5ccc4b
MS-RequestId: 512a777a-5427-452d-9637-18421387e435
X-Locale: en-US,en-US
Date: Thu, 01 Nov 2018 22:46:18 GMT

{
    "id":"4d927e27-93d1-448b-abe5-819b66ecca22",
    "creationTimestamp":"2018-11-01T22:46:16.2996364Z",
    "lastModifiedTimestamp":"2018-11-01T22:46:16.2996364Z",
    "expirationTimestamp":"2018-11-01T23:01:18.7543264Z",
    "lastModifiedUser":"1824b7fc-2fac-4478-b177-66823c40ab75",
    "status":"Active",
    "lineItems": [
        {
            "id":0,
            "catalogItemId":"C94271D8-B431-4A25-A3C5-A57737A1C909",
            "quantity":1,
            "currencyCode":"USD",
            "billingCycle":"annual",
            "provisioningContext": {
                "parentSubscriptionId":"97555B61-7461-477A-A98C-9C76148783E4"
            },
            "orderGroup":"OMS-0"
        }
    ],
    "links": {
        "self": {
            "uri":"/customers/18ac2950-8ea9-4dfc-92a4-ff4d4cd57796/carts/4d927e27-93d1-448b-abe5-819b66ecca22",
            "method":"GET",
            "headers":[
            ]
        }
    },
    "attributes": {
        "objectType":"Cart"
    }
}
```
