---
title: Fatura döngüsünü değiştirme
description: Api'leri kullanarak müşteri aboneliğini aylık veya yıllık faturalamaya İş Ortağı Merkezi öğrenin. Bunu panodan da İş Ortağı Merkezi.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 435309229e2cb038c936028943f4c2cf27b032a7
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974123"
---
# <a name="change-a-customer-subscription-billing-cycle"></a>Müşteri aboneliği faturalama döngüsünü değiştirme

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bir Siparişi [aylık](order-resources.md) faturalamadan yıllık faturalamaya veya yıllık faturalamadan aylık faturalamaya doğru güncelleştirmeler.

Bu İş Ortağı Merkezi, müşterinin abonelik ayrıntıları sayfasına giderek bu işlemi gerçekleştirebilirsiniz. Bu seçenek, abonelik için geçerli faturalama döngüsünü tanımlayarak değişiklik ve gönderme olanağına sahip olur.

**Bu makalenin** kapsamı dışında:

- Denemeler için faturalama döngüsünü değiştirme
- Azure abonelikleri için yıllık olmayan dönem tekliflerinin (aylık, altı yıllık) faturalama & değiştirme
- Etkin olmayan abonelikler için faturalama döngülerini değiştirme
- Microsoft çevrimiçi hizmetler tabanlı abonelikler için faturalama döngülerini değiştirme

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Sipariş kimliği.

## <a name="c"></a>C\#

Faturalama döngüsünün sıklığını değiştirmek için [**Order.BillingCycle özelliğini güncelleştirin.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.billingcycle#Microsoft_Store_PartnerCenter_Models_Orders_Order_BillingCycle)

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

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem    | İstek URI'si                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| **Yama** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bu tabloda aboneliğin miktarını değiştirmek için gerekli sorgu parametresi listelemektedir.

| Ad                   | Tür | Gerekli | Açıklama                                                          |
|------------------------|------|----------|----------------------------------------------------------------------|
| **customer-tenant-id** | GUID |    Y     | Müşteriyi tanımlayan **GUID biçimlendirilmiş customer-tenant-id** |
| **order-id**           | GUID |    Y     | Sipariş tanımlayıcısı                                                 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Aşağıdaki tablolar istek gövdesinin özelliklerini açıklar.

### <a name="order"></a>Sipariş

| Özellik           | Tür             | Gerekli | Açıklama                                                                |
|--------------------|------------------|----------|----------------------------------------------------------------------------|
| Id                 | string           |    N     | Siparişin başarıyla oluşturulmasının ardından sağlanan sipariş tanımlayıcısı |
|ReferenceCustomerId | string           |    Y     | Müşteri tanımlayıcısı                                                    |
| BillingCycle       | string           |    Y     | İş ortağının bu sipariş için faturalandırılama sıklığını gösterir. Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. |
| LineItems          | nesne dizisi |    Y     | [OrderLineItem kaynakları](#orderlineitem) dizisi                      |
| Creationdate       | datetime         |    N     | Siparişin tarih-saat biçiminde oluşturulma tarihi                        |
| Öznitelikler         | Nesne           |    N     | "ObjectType": "OrderLineItem" içerir                                     |

### <a name="orderlineitem"></a>OrderLineItem

| Özellik             | Tür   | Gerekli | Açıklama                                                                        |
|----------------------|--------|----------|------------------------------------------------------------------------------------|
| LineItemNumber       | sayı |    Y     | 0 ile başlayan satır öğesi numarası                                              |
| OfferId              | string |    Y     | Teklifin kimliği                                                                |
| SubscriptionId       | string |    Y     | Aboneliğin kimliği                                                         |
| Friendlyname         | string |    N     | Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı |
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