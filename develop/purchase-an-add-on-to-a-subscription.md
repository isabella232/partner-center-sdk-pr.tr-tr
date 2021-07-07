---
title: Bir abonelik için eklenti satın alma
description: Mevcut bir aboneliğe eklenti satın alma.
ms.date: 11/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d8b700a2ad41a37ca0ad745f3e7767449974b18a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547691"
---
# <a name="purchase-an-add-on-to-a-subscription"></a>Bir abonelik için eklenti satın alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government

Mevcut bir aboneliğe eklenti satın alma.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Abonelik kimliği. Bu, eklenti teklifi satın alınarak satın alınan mevcut aboneliktir.

- Satın alınan eklenti teklifini tanımlayan teklif kimliği.

## <a name="purchasing-an-add-on-through-code"></a>Kod aracılığıyla eklenti satın alma

Bir abonelik için eklenti satın aldığınız zaman, özgün abonelik siparişlerini eklentinin siparişiyle güncelleştirebilirsiniz. Aşağıda customerId müşteri kimliği, subscriptionId abonelik kimliği, addOnOfferId ise eklentinin teklif kimliğidir.

Adımlar aşağıdaki gibidir:

1.  Aboneliğin işlemleri için bir arabirim alın.

    ``` csharp
    var subscriptionOperations = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId);
    ```

2.  Bir abonelik nesnesi örneği için bu arabirimi kullanın. Bu, sipariş kimliği de dahil olmak üzere üst abonelik ayrıntılarını size alır.

    ``` csharp
    var parentSubscription = subscriptionOperations.Get();
    ```

3.  Yeni bir Order nesnesi [**örneği**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) oluşturma. Bu sipariş örneği, aboneliği satın almak için kullanılan özgün siparişi güncelleştirmek için kullanılır. Eklentiyi temsil eden sıraya tek satırlı bir öğe ekleyin.
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

4.  Aboneliğin özgün siparişlerini eklentinin yeni siparişiyle güncelleştirin.
    ``` csharp
    Order updatedOrder = partnerOperations.Customers.ById(customerId).Orders.ById(parentSubscription.OrderId).Patch(orderToUpdate);
    ```

## <a name="c"></a>C\#

Bir eklenti satın almak için, müşteriyi tanımlamak üzere müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim elde edin ve [**subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemi ile eklenti teklifinin yer alan aboneliğini tanıyın. [**Al'ı**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription) çağırarak abonelik ayrıntılarını almak için bu arabirimi [**kullanın.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.get) Abonelik ayrıntıları, abonelik siparişinin sipariş kimliğini içerir ve bu, eklentiyle güncelleştirilen sipariştir.

Ardından yeni bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği ekleyin ve aşağıdaki kod parçacığında gösterildiği gibi eklentiyi tanımlamak için gereken bilgileri içeren tek [**bir LineItem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) örneğiyle doldurmak. Bu yeni nesneyi kullanarak abonelik siparişlerini eklentiyle güncelleştirebilirsiniz. Son olarak, önce [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) ile müşteriyi ve [**Orders.ById**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid)ile siparişi tanımdikten sonra abonelik siparişini güncelleştirmek için [**Patch**](/dotnet/api/microsoft.store.partnercenter.orders.iorder.patch) yöntemini arayın.

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

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı **Samples Sınıfı:** AddSubscriptionAddOn.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem    | İstek URI'si                                                                                              |
|-----------|----------------------------------------------------------------------------------------------------------|
| **Yama** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve siparişi belirlemek için aşağıdaki parametreleri kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, müşteriyi tanımlayan GUID **biçimli bir customer-tenant-id** değeridir. |
| **order-id**           | **guid** | Y        | Sipariş tanımlayıcısı.                                                              |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Aşağıdaki tablolar istek gövdesinin özelliklerini açıklar.

## <a name="order"></a>Sipariş

| Ad                | Tür             | Gerekli | Açıklama                                          |
|---------------------|------------------|----------|------------------------------------------------------|
| Id                  | string           | N        | Sipariş kimliği.                                        |
| ReferenceCustomerId | string           | Y        | Müşteri kimliği.                                     |
| LineItems           | nesne dizisi | Y        | [OrderLineItem nesneleri dizisi.](#orderlineitem) |
| Creationdate        | string           | N        | Siparişin tarih-saat biçiminde oluşturulma tarihi. |
| Öznitelikler          | object           | N        | "ObjectType": "Order" ifadesini içerir.                      |

## <a name="orderlineitem"></a>OrderLineItem

| Ad                 | Tür   | Gerekli | Açıklama                                                  |
|----------------------|--------|----------|--------------------------------------------------------------|
| LineItemNumber       | sayı | Y        | 0 ile başlayan satır öğesi numarası.                       |
| OfferId              | string | Y        | Eklentinin teklif kimliği.                                  |
| SubscriptionId       | string | N        | Satın alınan eklenti aboneliğinin kimliği.                 |
| ParentSubscriptionId | string | Y        | Eklenti teklifine sahip üst aboneliğin kimliği. |
| Friendlyname         | string | N        | Bu satır öğesinin kolay adı.                        |
| Miktar             | sayı | Y        | Lisans sayısı.                                      |
| PartnerIdOnRecord    | string | N        | Kayıt ortağının MPN kimliği.                         |
| Öznitelikler           | object | N        | "ObjectType": "OrderLineItem" ifadesini içerir.                      |

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

Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş abonelik siparişlerini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İş Ortağı Merkezi Kodları.](error-codes.md)

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
