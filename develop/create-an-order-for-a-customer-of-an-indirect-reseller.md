---
title: Dolaylı satıcı için müşteri siparişi oluştur
description: Dolaylı bir satıcının müşterisi için sipariş oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makale önkoşulları, adımları ve Exmaples 'leri içerir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f72ecec8d82e6b8a1bc53c277206cafd7d8a4e03
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770154"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Dolaylı satıcı müşterisi için bir sipariş oluşturma

**Uygulama hedefi:**

- İş Ortağı Merkezi

Dolaylı bir satıcı müşterisi için sipariş oluşturma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Satın alınacak öğenin teklif tanımlayıcısı.

- Dolaylı Bayi kiracı tanımlayıcısı.

## <a name="c"></a>C\#

Dolaylı bir satıcının müşterisi için sipariş oluşturmak için:

1. Oturum açmış iş ortağıyla ilişkisi olan dolaylı satıcıların bir koleksiyonunu alın.

2. Koleksiyonda dolaylı satıcı KIMLIĞIYLE eşleşen öğeye yerel bir değişken alın. Bu adım, siparişi oluştururken satıcının [**Mpnıd**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) özelliğine erişmenize yardımcı olur.

3. Bir [**Order**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) nesnesi örneği oluşturun ve müşteriyi kaydetmek Için [**Referencecustomerıd**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) özelliğini müşteri tanımlayıcısı olarak ayarlayın.

4. [**Orderlineıtem**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) nesnelerinin bir listesini oluşturun ve listeyi Order 's [**LineItems**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) özelliğine atayın. Her sipariş satırı öğesi, bir teklifin satın alma bilgilerini içerir. Her bir satır öğesinde [**Partneridonrecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) özelliğini dolaylı satıcının MPN kimliğiyle doldurduğunuzdan emin olun. En az bir sipariş satırı öğesine sahip olmanız gerekir.

5. Müşteriyi tanımlamak için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak işlemleri sipariş etmek için bir arabirim edinin ve ardından [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğinden arabirimi alın.

6. Siparişi oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metodunu çağırın.

### <a name="c-example"></a>C \# örneği

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string offerId;
// string indirectResellerId;

// Get the indirect resellers with a relationship to the signed-in partner.
var indirectResellers = partnerOperations.Relationships.Get(PartnerRelationshipType.IsIndirectCloudSolutionProviderOf);

// Find the matching reseller in the collection.
var selectedIndirectReseller = (indirectResellers != null && indirectResellers.Items.Any()) ?
    indirectResellers.Items.FirstOrDefault(reseller => reseller.Id.Equals(indirectResellerId, StringComparison.OrdinalIgnoreCase)) :
    null;

// Prepare the order and populate the PartnerIdOnRecord with the reseller&#39;s Microsoft Partner Network Id.
var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "New offer purchase.",
            Quantity = 5,
            PartnerIdOnRecord = selectedIndirectReseller != null ? selectedIndirectReseller.MpnId : null
        }
    }
};

// Place the order.
var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Örnek**: [konsol test uygulaması](console-test-app.md)**PROJESI**: iş ortağı Merkezi SDK örnekleri **sınıfı**: PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Orders http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                           |
|-------------|--------|----------|-------------------------------------------------------|
| müşteri kimliği | string | Yes      | Müşteriyi tanımlayan GUID biçimli dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

#### <a name="order"></a>Sipariş

Bu tablo, istek gövdesindeki **sıra** özelliklerini açıklar.

| Ad | Tür | Gerekli | Açıklama |
| ---- | ---- | -------- | ----------- |
| kimlik | dize | No | Siparişin başarıyla oluşturulması sırasında sağlanan bir sipariş tanımlayıcısı. |
| Referencecustomerıd | string | Yes | Müşteri tanımlayıcısı. |
| Bilimlingcycle | dize | No | Bu sipariş için ortağın faturalandırılma sıklığı. Varsayılan değer &quot; aylık &quot; ' dır ve siparişin başarıyla oluşturulması üzerine uygulanır. Desteklenen değerler, [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)içinde bulunan üye adlarıdır. Note: yıllık faturalandırma özelliği henüz genel kullanıma sunulmamıştır. Yıllık faturalandırmaya yönelik destek yakında kullanıma sunulacak. |
| LineItems | nesne dizisi | Yes | [**Orderlineıtem**](#orderlineitem) kaynakları dizisi. |
| creationDate | dize | No | Siparişin oluşturulduğu tarih ve saat biçimi. Siparişin başarıyla oluşturulmasından sonra uygulandı. |
| öznitelikler | object | No | "ObjectType": "Order" içerir. |

#### <a name="orderlineitem"></a>Orderlineıtem

Bu tablo, istek gövdesinde **Orderlineıtem** özelliklerini açıklar.

| Ad | Tür | Gerekli | Açıklama |
| ---- | ---- | -------- | ----------- |
| Lineıtemnumber | int | Yes | Koleksiyondaki her bir satır öğesi, 0 ' dan say-1 ' e kadar sayarak benzersiz bir satır numarası alır. |
| OfferId | string | Yes | Teklif tanımlayıcısı. |
| subscriptionId | dize | No | Abonelik tanımlayıcısı. |
| Parentsubscriptionıd | dize | No | İsteğe bağlı. Bir eklenti teklifinde üst aboneliğin KIMLIĞI. Yalnızca düzeltme eki için geçerlidir. |
| friendlyName | dize | No | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı. |
| miktar | int | Yes | Lisans tabanlı abonelik için lisans sayısı. |
| partnerIdOnRecord | dize | No | Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir). Bu, teşvikleri için doğru hesaplamayı sağlar. **Satıcı MPN KIMLIĞI sağlama hatası, siparişin başarısız olmasına neden olmaz. Ancak, satıcı kaydedilmez ve bir sonuç olarak hesaplamalar satışı içermez.** |
| öznitelikler | object | No | "ObjectType": "Orderlineıtem" içerir. |

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 410
Expect: 100-continue

{
    "Id": null,
    "ReferenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "BillingCycle": "unknown",
    "LineItems": [{
            "LineItemNumber": 0,
            "OfferId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "SubscriptionId": null,
            "ParentSubscriptionId": null,
            "FriendlyName": "New offer purchase.",
            "Quantity": 5,
            "PartnerIdOnRecord": "4847383",
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

Başarılı olursa, yanıt gövdesi doldurulmuş [sipariş](order-resources.md) kaynağını içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 831
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 85195ae6-3de5-4978-abd4-7be2fbfe4c84
MS-RequestId: 02109f46-3ff2-4be4-9f37-b2eb6d58d542
MS-CV: Nd3Oum/L5EywtKQK.0
MS-ServerId: 020021921
Date: Mon, 10 Apr 2017 23:02:24 GMT

{
    "id": "3eddcac6-63b2-4c40-b0b6-f47e18301492",
    "referenceCustomerId": "c501c3c4-d776-40ef-9ecf-9cefb59442c1",
    "billingCycle": "monthly",
    "lineItems": [{
            "lineItemNumber": 0,
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "subscriptionId": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "friendlyName": "New offer purchase.",
            "quantity": 5,
            "partnerIdOnRecord": "4847383",
            "links": {
                "subscription": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2017-04-10T16:02:25.983-07:00",
    "links": {
        "self": {
            "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/orders/3eddcac6-63b2-4c40-b0b6-f47e18301492",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "eyJpZCI6IjNlZGRjYWM2LTYzYjItNGM0MC1iMGI2LWY0N2UxODMwMTQ5MiIsInZlcnNpb24iOjF9",
        "objectType": "Order"
    }
}
```
