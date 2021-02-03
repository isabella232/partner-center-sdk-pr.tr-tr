---
title: Fatura döngüsünü değiştirme
description: Iş Ortağı Merkezi API 'Lerini kullanarak aylık veya yıllık faturalandırma için bir müşteri aboneliğini güncelleştirme hakkında bilgi edinin. Bunu Iş Ortağı Merkezi panosundan de yapabilirsiniz.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 8a2879db061ced799e29d84e71be5b1259b07689
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770090"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Müşteri aboneliği fatura döngüsünü değiştirme

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir [siparişi](order-resources.md) aylık faturalandırmaya veya yıllık faturalandırmaya aylık faturalandırma olarak güncelleştirir.

Iş Ortağı Merkezi panosunda, bu işlem bir müşterinin abonelik ayrıntıları sayfasına gidilerek gerçekleştirilebilir. Bu işlem tamamlandıktan sonra, abonelik için geçerli faturalandırma döngüsünü tanımlama ve gönderme yeteneğine sahip bir seçenek görürsünüz.

Bu makalenin **kapsam dışı** :

- Deneme için faturalandırma döngüsünü değiştirme
- Yıllık olmayan dönem teklifleri (aylık, 6 yıl) & Azure abonelikleri için fatura döngülerini değiştirme
- Etkin olmayan abonelikler için faturalandırma döngülerini değiştirme
- Microsoft çevrimiçi hizmetler lisans tabanlı abonelikler için faturalandırma döngülerini değiştirme

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Bir sipariş KIMLIĞI.

## <a name="c"></a>C\#

Faturalandırma döngüsünün sıklığını değiştirmek için [**Order. BillingCycle**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle) özelliğini güncelleştirin.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string orderId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    BillingCycle = BillingCycleType.Annual,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            LineItemNumber = 0,
            OfferId = offerId,
            SubscriptionId = "69829602-C219-40FD-A3D5-4150FCA41A19",
            Quantity = 1
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.ById(orderId).Patch(order);
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem    | İstek URI'si                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **DÜZELTMESI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bu tabloda, abonelik miktarını değiştirmek için gerekli sorgu parametresi listelenmektedir.

| Ad                   | Tür | Gerekli | Açıklama                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | GUID |    Y     | Müşteriyi tanımlayan bir GUID biçimli **Müşteri Kiracı kimliği** |
| **sıra kimliği**           | GUID |    Y     | Sıra tanımlayıcısı                                                 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Aşağıdaki tablolarda, istek gövdesindeki özellikler açıklanır.

### <a name="order"></a>Sipariş

| Özellik           | Tür             | Gerekli | Açıklama                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | string           |    N     | Sıranın başarıyla oluşturulması sırasında sağlanan bir sipariş tanımlayıcısı |
|Referencecustomerıd | string           |    Y     | Müşteri tanımlayıcısı                                                    |
| BillingCycle       | string           |    Y     | Ortağın bu sipariş için faturalandırılabileceği sıklığı belirtir. Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. |
| LineItems          | nesne dizisi |    Y     | [Orderlineıtem](#orderlineitem) kaynakları dizisi                      |
| CreationDate       | datetime         |    N     | Siparişin oluşturulduğu tarih ve tarih-saat biçiminde                        |
| Öznitelikler         | Nesne           |    N     | "ObjectType" içerir: "Orderlineıtem"                                     |

### <a name="orderlineitem"></a>Orderlineıtem

| Özellik             | Tür   | Gerekli | Açıklama                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| Lineıtemnumber       | sayı |    Y     | Satır öğe numarası, 0 ile başlar                                              |
| OfferId              | string |    Y     | Teklifin KIMLIĞI                                                                |
| SubscriptionId       | string |    Y     | Aboneliğin KIMLIĞI                                                         |
| FriendlyName         | string |    N     | Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı |
| Miktar             | sayı |    Y     | Lisans veya örnek sayısı                                                |
| PartnerIdOnRecord    | string |    N     | Kayıt ortağının MPN KIMLIĞI                                                |
| Öznitelikler           | Nesne |    N     | "ObjectType" içerir: "Orderlineıtem"                                             |

### <a name="request-example"></a>İstek örneği

Yıllık faturalandırmaya Güncelleştir

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
    "BillingCycle" : "Annual",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "SubscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
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

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

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
    "billingCycle": "Annual",
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
        },
        {
            "lineItemNumber": 1,
            "offerId": "2828BE95-46BA-4F91-B2FD-0BEF192ECF60",
            "subscriptionId": "69829602-C219-40FD-A3D5-4150FCA41A19",
            "friendlyName": "Some friendly name",
            "quantity": 2,
            "links": {
                "subscription": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/subscriptions/69829602-C219-40FD-A3D5-4150FCA41A19",
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