---
title: Müşteri siparişi oluşturma
description: Müşteri için sipariş İş Ortağı Merkezi API'leri kullanmayı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3a86a99f43bdeec5e4c560ab59e1924b76c0636
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973562"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>İş Ortağı Merkezi API'lerini kullanarak müşteri İş Ortağı Merkezi oluşturma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government

Azure ayrılmış **VM örneği ürünleri için sipariş oluşturma yalnızca** *aşağıdakiler için* geçerlidir:

- İş Ortağı Merkezi

Şu anda satış için nelerin kullanılabilir olduğu hakkında daha fazla bilgi için, Bulut Çözümü Sağlayıcısı [bakın.](/partner-center/csp-offers)

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Teklif tanımlayıcısı.

## <a name="c"></a>C\#

Bir müşteriye sipariş oluşturmak için:

1. Bir Order nesnesi [**örneği**](order-resources.md) oluşturma ve müşteriyi kaydetmek **için ReferenceCustomerID** özelliğini müşteri kimliğine ayarlayın.

2. [**OrderLineItem nesnelerinin**](order-resources.md#orderlineitem) listesini oluşturun ve listeyi siparişin **LineItems özelliğine** attayabilirsiniz. Her sipariş satırı öğesi, bir teklif için satın alma bilgilerini içerir. En az bir sipariş satırı öğeniz olması gerekir.

3. İşlemleri sıralamak için bir arabirim elde edin. İlk olarak, [**müşteri kimliğini kullanarak IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak müşteriyi tanıyın. Ardından Orders özelliğinden [**arabirimini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) alın.

4. [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) veya [**CreateAsync yöntemini**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) çağırma ve [**Order nesnesine**](order-resources.md) geçme.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** CreateOrder.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                                |
|-------------|--------|----------|------------------------------------------------------------|
| customer-id | string | Yes      | Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

#### <a name="order"></a>Sipariş

Bu tablo, istek [gövdesinin](order-resources.md) Sipariş özelliklerini açıklar.

| Özellik             | Tür                        | Gerekli                        | Açıklama                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| kimlik                   | dize                      | No                              | Siparişin başarıyla oluşturulmasının ardından sağlanan bir sipariş tanımlayıcısı.   |
| referenceCustomerId  | dize                      | No                              | Müşteri tanımlayıcısı. |
| billingCycle         | dize                      | No                              | İş ortağının bu sipariş için faturalandırılama sıklığını gösterir. Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. Varsayılan değer, sipariş oluşturma sırasında "Monthly" veya "OneTime" şeklindedir. Bu alan, siparişin başarıyla oluşturulmasının ardından uygulanır. |
| lineItems            | [OrderLineItem kaynakları](order-resources.md#orderlineitem) dizisi | Yes      | Miktarı da dahil olmak üzere müşterinin satın alma tekliflerinin maddeli listesi.        |
| currencyCode         | dize                      | No                              | Salt okunur. Siparişin yerleştirilmesi için kullanılan para birimi. Siparişin başarıyla oluşturulmasının ardından uygulanır.           |
| Creationdate         | datetime                    | Hayır                              | Salt okunur. Siparişin tarih-saat biçiminde oluşturulma tarihi. Siparişin başarıyla oluşturulmasının ardından uygulanır.                                   |
| durum               | dize                      | No                              | Salt okunur. Siparişin durumu.  Desteklenen değerler OrderStatus içinde bulunan üye [adlarıdır.](order-resources.md#orderstatus)        |
| Bağlantı                | [OrderLinks](utility-resources.md#resourcelinks)              | Hayır                              | Siparişe karşılık gelen kaynak bağlantıları. |
| öznitelikler           | [Resourceattributes](utility-resources.md#resourceattributes) | Hayır                              | Order'a karşılık gelen meta veri öznitelikleri. |

#### <a name="orderlineitem"></a>Orderlineıtem

Bu tablo, istek gövdesinde [Orderlineıtem](order-resources.md#orderlineitem) özelliklerini açıklar.

>[!NOTE]
>PartnerIdOnRecord yalnızca dolaylı bir sağlayıcı dolaylı bir satıcı adına sipariş yerleştirirse sağlanmalıdır. Yalnızca dolaylı satıcının Microsoft İş Ortağı Ağı KIMLIĞINI depolamak için kullanılır (dolaylı sağlayıcının KIMLIĞI değildir).

| Ad                 | Tür   | Gerekli | Açıklama                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lineıtemnumber       | int    | Yes      | Koleksiyondaki her bir satır öğesi, 0 ' dan say-1 ' e kadar sayarak benzersiz bir satır numarası alır.                                                                                                                                                 |
| OfferId              | string | Yes      | Teklif tanımlayıcısı.                                                                                                                                                                                                                      |
| subscriptionId       | dize | No       | Abonelik tanımlayıcısı.                                                                                                                                                                                                               |
| Parentsubscriptionıd | dize | No       | İsteğe bağlı. Bir eklenti teklifinde üst aboneliğin KIMLIĞI. Yalnızca düzeltme eki için geçerlidir.                                                                                                                                                     |
| friendlyName         | dize | No       | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.                                                                                                                                              |
| miktar             | int    | Yes      | Lisans tabanlı abonelik için lisans sayısı.                                                                                                                                                                                   |
| partnerIdOnRecord    | dize | No       | Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir). Bu, teşvikleri için doğru hesaplamayı sağlar. |
| provisioningContext  | Sözlük<dize, dize>                | Hayır       |  Katalogdaki bazı öğelerin sağlanması için gereken bilgiler. SKU 'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.                  |
| Köprü                | [Orderlineıtemlinks](order-resources.md#orderlineitemlinks) | Hayır       |  Salt okunur. Sipariş satırı öğesine karşılık gelen kaynak bağlantıları.  |
| öznitelikler           | [ResourceAttributes](utility-resources.md#resourceattributes) | Hayır       | Orderlineıtem öğesine karşılık gelen meta veri öznitelikleri. |
| renewsTo             | Nesne dizisi                          | Hayır    |[RenewsTo](order-resources.md#renewsto) kaynaklarından oluşan bir dizi.                                                                            |

##### <a name="renewsto"></a>RenewsTo

Bu tablo, istek gövdesinde [RenewsTo](order-resources.md#renewsto) özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| termDuration          | dize           | No              | Yenileme teriminin süresinin ISO 8601 temsili. Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl). |

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
