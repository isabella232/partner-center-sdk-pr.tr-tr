---
title: Sipariş satırı öğesine göre etkinleştirme bağlantısını alma
description: Sipariş satırı öğesine göre abonelik etkinleştirme bağlantısını alır.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 61cb6659961cfeb22d3b0fe7ad5dd8533d5f72dda76fe96e64b4c64f39ece397
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994158"
---
# <a name="get-activation-link-by-order-line-item"></a>Sipariş satırı öğesine göre etkinleştirme bağlantısını alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Sipariş satırı öğe numarasına göre ticari market aboneliği etkinleştirme bağlantısını alır.

İş Ortağı Merkezi panosunda, ana sayfada Abonelik altında Belirli bir  Abonelik seçerek veya Abonelikler sayfasında etkinleştirmek için aboneliğin yanındaki **Publisher'nin sitesine** git bağlantısını seçerek bu işlemi  **yapabilirsiniz.**

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Etkinleştirmesi gereken ürünle sipariş tamamlandı.

## <a name="c"></a>C\#

Bir satır öğesinin etkinleştirme bağlantısını almak için [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonu kullanın ve seçilen müşteri kimliğiyle [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini arayın. Ardından Orders [**özelliğini ve**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) belirttiğiniz [**OrderId değeriyle çağırabilirsiniz.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id) Ardından satır öğesi numarası tanımlayıcısıyla **ById()** yöntemiyle [**LineItems'i**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) çağırabilirsiniz.  Son olarak **ActivationLinks() yöntemini** arayın.

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt [gövdesinde bir](customer-resources.md#customer) Müşteri kaynakları koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
