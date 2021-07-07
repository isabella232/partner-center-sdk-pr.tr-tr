---
title: Dolaylı kurumsal bayi için müşteri siparişi oluşturma
description: Dolaylı kurumsal bayi İş Ortağı Merkezi sipariş oluşturmak için api'leri kullanmayı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6253ba2289ea1f58e7d8eaa960d7d0daaa887f0d
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973561"
---
# <a name="create-an-order-for-a-customer-of-an-indirect-reseller"></a>Dolaylı satıcı müşterisi için bir sipariş oluşturma

Dolaylı kurumsal bayi müşterisi için sipariş oluşturma.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Satın alınan öğenin teklif tanımlayıcısı.

- Dolaylı kurumsal bayinin kiracı tanımlayıcısı.

## <a name="c"></a>C\#

Dolaylı kurumsal bayinin müşterisi için sipariş oluşturmak için:

1. Oturum açmış iş ortağıyla ilişkisi olan dolaylı kurumsal bayilerin koleksiyonunu alın.

2. Koleksiyonda dolaylı kurumsal bayi kimliğiyle eşleşen öğeye bir yerel değişken alın. Bu adım, siparişi 7/2012'ye kadar olan tüm bayilerin [**MpnId**](/dotnet/api/microsoft.store.partnercenter.models.relationships.partnerrelationship.mpnid) özelliğine erişmeye yardımcı olur.

3. Bir Order [**nesnesinin**](/dotnet/api/microsoft.store.partnercenter.models.orders.order) örneğini oluşturma ve müşteriyi kaydetmek için [**ReferenceCustomerID**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.referencecustomerid) özelliğini müşteri tanımlayıcısı olarak ayarlayın.

4. [**OrderLineItem nesnelerinin**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem) listesini oluşturun ve listeyi siparişin [**LineItems özelliğine**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.lineitems) attayabilirsiniz. Her sipariş satırı öğesi, bir teklif için satın alma bilgilerini içerir. Her satır öğesinde [**PartnerIdOnRecord**](/dotnet/api/microsoft.store.partnercenter.models.orders.orderlineitem.partneridonrecord) özelliğini dolaylı kurumsal bayinin MPN kimliğiyle doldurmak için emin olun. En az bir sipariş satırı öğeniz olması gerekir.

5. Müşteriyi tanımlamak için müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak işlemleri sıralamak için bir arabirim alın ve [**ardından Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğinden arabirimi alın.

6. Siparişi oluşturmak [**için Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) [**veya CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) yöntemini çağırma.

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

**Örnek:** [Konsol test uygulaması](console-test-app.md)**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** PlaceOrderForCustomer.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                           |
|-------------|--------|----------|-------------------------------------------------------|
| customer-id | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

#### <a name="order"></a>Sipariş

Bu tablo, istek **gövdesinin** Sipariş özelliklerini açıklar.

| Ad | Tür | Gerekli | Açıklama |
| ---- | ---- | -------- | ----------- |
| kimlik | dize | No | Siparişin başarıyla oluşturulmasının ardından sağlanan bir sipariş tanımlayıcısı. |
| referenceCustomerId | string | Yes | Müşteri tanımlayıcısı. |
| billingCycle | dize | No | İş ortağının bu sipariş için faturalandırılama sıklığı. Varsayılan değer &quot; Aylık'tır &quot; ve siparişin başarıyla oluşturulmasının ardından uygulanır. Desteklenen değerler, [**BillingCycleType**](/dotnet/api/microsoft.store.partnercenter.models.offers.billingcycletype)içinde bulunan üye adlarıdır. Not: Yıllık faturalama özelliği henüz genel kullanıma açık değildir. Yıllık faturalama desteği yakında gelecektir. |
| lineItems | nesne dizisi | Yes | [**OrderLineItem kaynaklarının dizisi.**](#orderlineitem) |
| Creationdate | dize | No | Siparişin tarih-saat biçiminde oluşturulma tarihi. Siparişin başarıyla oluşturulmasının ardından uygulanır. |
| öznitelikler | object | Hayır | "ObjectType": "Order" ifadesini içerir. |

#### <a name="orderlineitem"></a>OrderLineItem

Bu tablo, istek **gövdesinin OrderLineItem** özelliklerini açıklar.

| Ad | Tür | Gerekli | Açıklama |
| ---- | ---- | -------- | ----------- |
| lineItemNumber | int | Yes | Koleksiyonda yer alan her satır öğesi benzersiz bir satır numarası alır ve 0 ile 1 arasında bir sayıya kadar sayar. |
| offerId | string | Yes | Teklif tanımlayıcısı. |
| subscriptionId | dize | No | Abonelik tanımlayıcısı. |
| Parentsubscriptionıd | dize | No | İsteğe bağlı. Bir eklenti teklifinde üst aboneliğin KIMLIĞI. Yalnızca düzeltme eki için geçerlidir. |
| friendlyName | dize | No | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı. |
| miktar | int | Yes | Lisans tabanlı abonelik için lisans sayısı. |
| partnerIdOnRecord | dize | No | Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir). Bu, teşvikleri için doğru hesaplamayı sağlar. **Satıcı MPN KIMLIĞI sağlama hatası, siparişin başarısız olmasına neden olmaz. Ancak, satıcı kaydedilmez ve bir sonuç olarak hesaplamalar satışı içermez.** |
| öznitelikler | object | Hayır | "ObjectType": "Orderlineıtem" içerir. |

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
