---
title: Eklentilerle bir sepet oluşturma
description: Sepet üzerinden eklentilerle İş Ortağı Merkezi sipariş eklemek için api'leri kullanmayı öğrenin. Makale, eklentilerle sepet oluşturmanın önkoşullarını ve adımlarını paylaşıyor.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: ed4b8be5171493f83aefef08253c748a7bfd90dc5f2b1e325e5ceba78e36bdc2
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991812"
---
# <a name="create-a-cart-with-add-ons-to-a-customer-order"></a>Müşteri siparişine eklentilerle sepet oluşturma

Sepet üzerinden eklentiler satın alın. Şu anda satış için kullanılabilenler hakkında daha fazla bilgi için bkz. [Bulut Çözümü Sağlayıcısı programda iş ortağı teklifleri.](/partner-center/csp-offers)

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="c"></a>C\#

Sepet, temel teklifin ve ilgili eklentilerin satın alımını sağlar. Sepet oluşturmak için şu adımları izleyin:

1. Bir Sepet nesnesi [**örneği**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart) oluşturma.

2. Temel tekliflerini [**temsil eden CartLineItem**](/dotnet/api/microsoft.store.partnercenter.models.carts.cartlineitem) nesnelerinin listesini oluşturun ve listeyi sepetin [**LineItems özelliğine**](/dotnet/api/microsoft.store.partnercenter.models.carts.cart.lineitems) attayabilirsiniz.

3. Her temel teklifin sepet satır öğesi altında, **AddOnItems** listesini her biri bu temel teklife göre satın alınacak bir eklentiyi temsil eden diğer **CartLineItem** nesneleriyle doldurmak.

4. Müşteriyi tanımlamak için müşteri kimliğiyle [**ICustomerCollection.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak ve **ardından Cart** özelliğinden arabirimi alarak [**IAggregatePartner**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) kullanarak sepet işlemleri için bir arabirim elde edin.

5. Son olarak, sepeti [**oluşturmak**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.create) için [**Create veya CreateAsync**](/dotnet/api/microsoft.store.partnercenter.carts.icartcollection.createasync) yöntemini çağırarak.

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

Mevcut temel aboneliklere göre eklentilerin satın alımını etkinleştirecek bir sepet oluşturmak için şu adımları izleyin:

1. **ProvisioningContext** özelliğinde "ParentSubscriptionId" anahtarıyla abonelik kimliğini içeren yeni bir **CartLineItem** ile bir Sepet oluşturun. 

2. **Create** veya **CreateAsync yöntemini** çağırma.

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

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts HTTP/1.1                        |

#### <a name="uri-parameter"></a>URI parametresi

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad            | Tür     | Gerekli | Açıklama                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | string   | Yes      | Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id.             |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek [gövdesinin](cart-resources.md) Sepet özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| kimlik                    | dize           | No              | Sepetin başarıyla oluşturulmasının ardından sağlanan bir sepet tanımlayıcısı.                                  |
| creationTimeStamp     | DateTime         | No              | Sepetin tarih-saat biçiminde oluşturulma tarihi. Sepetin başarıyla oluşturulmasının ardından uygulanır.         |
| lastModifiedTimeStamp | DateTime         | No              | Sepetin en son güncelleştirilen tarih-saat biçiminde olduğu tarih. Sepetin başarıyla oluşturulmasının ardından uygulanır.    |
| expirationTimeStamp   | DateTime         | No              | Sepet tarih-saat biçiminde sona erer.  Sepetin başarıyla oluşturulmasının ardından uygulanır.            |
| lastModifiedUser      | dize           | No              | Sepeti en son güncelleştirilen kullanıcı. Sepetin başarıyla oluşturulmasının ardından uygulanır.                             |
| lineItems             | Nesne dizisi | Yes             | [Bir CartLineItem kaynakları](cart-resources.md#cartlineitem) dizisi.                                             |

Bu tablo, istek [gövdesinin CartLineItem](cart-resources.md#cartlineitem) özelliklerini açıklar.

| Özellik             | Tür                             | Description                                                                                                                                           |
|----------------------|----------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------|
| kimlik                   | string                           | Sepet satır öğesi için benzersiz tanımlayıcı. Sepetin başarıyla oluşturulmasının ardından uygulanır.                                                                   |
| catalogId            | string                           | Katalog öğesi tanımlayıcısı.                                                                                                                          |
| Friendlyname         | string                           | İsteğe bağlı. Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                                                                 |
| miktar             | int                              | Lisans veya örnek sayısı.                                                                                                                  |
| currencyCode         | string                           | Para birimi kodu.                                                                                                                                    |
| Bilimlingcycle         | Nesne                           | Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                                                                                 |
| Katılımcılar         | Nesne dizesi çiftlerinin listesi      | Satın alımdaki kayıttaki iş ortağı kimliği koleksiyonu (MPN KIMLIĞI).                                                                                          |
| provisioningContext  | Sözlük<dize, dize>       | Teklifin sağlanması için kullanılan bir bağlam.                                                                                                             |
| orderGroup           | string                           | Hangi öğelerin birlikte yerleştirilebileceğini belirten bir grup.                                                                                               |
| Addonıtems           | **Cartlineıtem** nesnelerinin listesi | Ana sepet çizgisi öğesinin satın alma işleminden kaynaklanan temel aboneliğe yönelik olarak satın alınacak eklentiler için sepet çizgisi öğeleri koleksiyonu. |
| error                | Nesne                           | Bir hata varsa sepet oluşturulduktan sonra uygulanır.                                                                                                    |

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

Aşağıdaki REST örneği, mevcut bir temel aboneliğe eklentilerin nasıl ekleneceğini gösterir.

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
