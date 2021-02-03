---
title: Bir abonelik için eklenti satın alma
description: Mevcut bir aboneliğe eklenti satın alma.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 975a2516bccdc6274bfec5d6a3286a649fc4f808
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769658"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Bir abonelik için eklenti satın alma

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Mevcut bir aboneliğe eklenti satın alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik KIMLIĞI. Bu, eklenti teklifinin satın alınacağı mevcut bir aboneliğiniz.

- Satın almaya yönelik eklenti teklifini tanımlayan bir teklif KIMLIĞI.

## <a name="purchasing-an-add-on-through-code"></a>Kod üzerinden eklenti satın alma

Bir aboneliğe eklenti satın aldığınızda, özgün abonelik sırasını eklentinin sırasıyla güncelliyor olursunuz. Aşağıda, CustomerID müşteri KIMLIĞI, SubscriptionID abonelik KIMLIĞI, Addonofferıd ise eklentinin teklif KIMLIĞIDIR.

Adımlar aşağıdaki gibidir:

1.  Abonelik işlemlerine yönelik bir arabirim alın.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Bir abonelik nesnesi oluşturmak için bu arabirimi kullanın. Bu, sipariş kimliği de dahil olmak üzere üst abonelik ayrıntılarını alır.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Yeni bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği oluşturun. Bu sipariş örneği, aboneliği satın almak için kullanılan orijinal sırayı güncelleştirmek için kullanılır. Eklentiyi temsil eden sıraya tek satırlık bir öğe ekleyin.
    ``` csharp
    var orderToUpdate = new Order()
    {
        ReferenceCustomerId = customerId,
        LineItems = new List<OrderLineItem>()
        {
            new OrderLineItem()
            {
                LineItemNumber = 0,
                OfferId = addOnOfferId,
                FriendlyName = "Some friendly name",
                Quantity = 2,
                ParentSubscriptionId = subscriptionId
            }
        }
    };
    ```

4.  Eklenti için yeni siparişle abonelik için orijinal sırayı güncelleştirin.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Bir eklenti satın almak için, müşteriyi belirlemek için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak ve eklenti teklifini içeren aboneliği belirlemek için [**abonelikler. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim edinerek başlayın. [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get)yöntemini çağırarak abonelik ayrıntılarını almak için bu [**arabirimi**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) kullanın. Abonelik ayrıntılarına neden ihtiyacınız var? Abonelik siparişinin sipariş kimliği gereklidir. Bu, eklenti ile güncelleştirilme sıraatalım.

Ardından, yeni bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği oluşturun ve aşağıdaki kod parçacığında gösterildiği gibi, eklentiyi tanımlayan bilgileri içeren tek bir [**LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) örneğiyle doldurun. Bu yeni nesneyi, eklenti ile abonelik sırasını güncelleştirmek için kullanacaksınız. Son olarak, ilk olarak, bir müşteriyi [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) ve [**Orders. byıd**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)ile sipariş olarak tanımladıktan sonra, abonelik sırasını güncelleştirmek için [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;
// string addOnOfferId;

// Get an interface to the operations for the subscription.
var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);

// Get the parent subscription details.
var parentSubscription = subscriptionOperations.Get();

// In order to buy an add-on subscription for this offer, we need to patch/update the order through which the base offer was purchased
// by creating an order object with a single line item which represents the add-on offer purchase.
var orderToUpdate = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = addOnOfferId,
            FriendlyName = "Some friendly name",
            Quantity = 2,
            ParentSubscriptionId = subscriptionId
        }
    }
};

// Update the order to apply the add on purchase.
Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: AddSubscriptionAddOn.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem    | İstek URI'si                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **DÜZELTMESI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve siparişi tanımlamak için aşağıdaki parametreleri kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y        | Değer, müşteriyi tanımlayan bir GUID biçimli **Müşteri-Kiracı kimliği** olur. |
| **sıra kimliği**           | **guid** | Y        | Sıra tanımlayıcısı.                                                              |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Aşağıdaki tablolarda, istek gövdesindeki özellikler açıklanır.

## <a name="order"></a>Sipariş

| Ad                | Tür             | Gerekli | Açıklama                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | string           | N        | Sipariş KIMLIĞI.                                        |
| Referencecustomerıd | string           | Y        | Müşteri KIMLIĞI.                                     |
| LineItems           | nesne dizisi | Y        | [Orderlineıtem](#orderlineitem) nesneleri dizisi. |
| CreationDate        | string           | N        | Siparişin oluşturulduğu tarih ve saat biçimi. |
| Öznitelikler          | object           | N        | "ObjectType": "Order" içerir.                      |

## <a name="orderlineitem"></a>Orderlineıtem

| Ad                 | Tür   | Gerekli | Açıklama                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| Lineıtemnumber       | sayı | Y        | Satır öğe numarası, 0 ile başlar.                       |
| OfferId              | string | Y        | Eklentinin teklif KIMLIĞI.                                  |
| SubscriptionId       | string | N        | Satın alınan eklenti aboneliğinin KIMLIĞI.                 |
| Parentsubscriptionıd | string | Y        | Eklenti teklifine sahip olan üst aboneliğin KIMLIĞI. |
| FriendlyName         | string | N        | Bu satır öğesi için kolay ad.                        |
| Miktar             | sayı | Y        | Lisans sayısı.                                      |
| PartnerIdOnRecord    | string | N        | Kayıt ortağının MPN KIMLIĞI.                         |
| Öznitelikler           | object | N        | "ObjectType": "Orderlineıtem" içerir.                      |

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/CF3B0E37-BE0B-4CDD-B584-D1A97D98A922 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 414
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": null,
            "ParentSubscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "FriendlyName": "Some friendly name",
            "Quantity": 2,
            "PartnerIdOnRecord": null,
            "Attributes": {
                "ObjectType": "OrderLineItem"
            }
        }
    ],
    "CreationDate": null,
    "Attributes": {
        "ObjectType": "Order"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş abonelik sırasını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1135
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 60efdd24-17ef-4080-9b02-4fc315f916ff
MS-RequestId: 17a2658e-d2cc-439b-a2f0-2aefd9344fbc
MS-CV: WtFy3zI8V0u2lnT9.0
MS-ServerId: 020021921
Date: Wed, 25 Jan 2017 23:01:08 GMT

{
    "id": "cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
    "referenceCustomerId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "billingCycle": "none",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "195416C1-3447-423A-B37B-EE59A99A19C4",
            "subscriptionId": "1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/1C2B75C1-74A5-472A-A729-7F8CEFC477F9",
                    "method": "GET",
                    "headers": []
                }
            }
        }, {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "968BA1CF-C146-4ADF-A300-308DCF718EEE",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/968BA1CF-C146-4ADF-A300-308DCF718EEE",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-01-25T14:53:12.093-08:00",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/orders/cf3b0e37-be0b-4cdd-b584-d1a97d98a922",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6ImNmM2IwZTM3LWJlMGItNGNkZC1iNTg0LWQxYTk3ZDk4YTkyMiIsInZlcnNpb24iOjJ9",
        "objectType": "Order"
    }
}
```
