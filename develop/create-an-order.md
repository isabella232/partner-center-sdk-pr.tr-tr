---
title: Müşteri siparişi oluşturma
description: Müşteri için sipariş oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a2a980634e3887780c9d6dbd4fa3271956978884
ms.sourcegitcommit: 59950cf131440786779c8926be518c2dc4bc4030
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/31/2021
ms.locfileid: "115009178"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>Iş Ortağı Merkezi API 'Lerini kullanarak bir müşteri için sipariş oluşturma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

**Azure ayrılmış VM örneği ürünlerinin bir sırası** oluşturmak için *yalnızca* şu şekilde geçerlidir:

- İş Ortağı Merkezi

şu anda satım için kullanılabilir olan bilgiler hakkında bilgi için [Bulut Çözümü Sağlayıcısı programındaki iş ortağı teklifleri](/partner-center/csp-offers)konusuna bakın.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Bir teklif tanımlayıcısı.

## <a name="c"></a>C\#

Bir müşteri için sipariş oluşturmak için:

1. Bir [**Order**](order-resources.md) nesnesi örneği oluşturun ve müşteriyi kaydetmek Için **Referencecustomerıd** özelliğini müşteri kimliği olarak ayarlayın.

2. [**Orderlineıtem**](order-resources.md#orderlineitem) nesnelerinin bir listesini oluşturun ve listeyi Order 's **LineItems** özelliğine atayın. Her sipariş satırı öğesi, bir teklifin satın alma bilgilerini içerir. En az bir sipariş satırı öğesine sahip olmanız gerekir.

3. Sipariş işlemlerine yönelik bir arabirim edinin. İlk olarak, müşteriyi tanımlamak için [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) YÖNTEMINI Müşteri kimliğiyle çağırın. Sonra, [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğinden arabirimi alın.

4. [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metodunu çağırın ve [**Order**](order-resources.md) nesnesini geçirin.

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

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: createorder. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                            |
|----------|----------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Orders http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                                |
|-------------|--------|----------|------------------------------------------------------------|
| müşteri kimliği | string | Yes      | Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

#### <a name="order"></a>Sipariş

Bu tablo, istek gövdesindeki [sıra](order-resources.md) özelliklerini açıklar.

| Özellik             | Tür                        | Gerekli                        | Açıklama                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| kimlik                   | dize                      | No                              | Siparişin başarıyla oluşturulması sırasında sağlanan bir sipariş tanımlayıcısı.   |
| Referencecustomerıd  | dize                      | No                              | Müşteri tanımlayıcısı. |
| Bilimlingcycle         | dize                      | No                              | Ortağın bu sipariş için faturalandırılabileceği sıklığı belirtir. Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. "Aylık" veya "OneTime" varsayılan olarak sıralı oluşturma. Bu alan, siparişin başarıyla oluşturulmasından sonra uygulanır. |
| LineItems            | [Orderlineıtem](order-resources.md#orderlineitem) kaynakları dizisi | Yes      | Müşterinin miktarı dahil satın aldığı tekliflerinin listesi.        |
| currencyCode         | dize                      | No                              | Salt okunur. Sipariş yerleştirilirken kullanılan para birimi. Siparişin başarıyla oluşturulmasından sonra uygulandı.           |
| creationDate         | datetime                    | No                              | Salt okunur. Siparişin oluşturulduğu tarih ve saat biçimi. Siparişin başarıyla oluşturulmasından sonra uygulandı.                                   |
| durum               | dize                      | No                              | Salt okunur. Siparişin durumu.  Desteklenen değerler [Orderstatus](order-resources.md#orderstatus)içinde bulunan üye adlarıdır.        |
| Köprü                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | Sıraya karşılık gelen kaynak bağlantıları. |
| öznitelikler           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | Sıraya karşılık gelen meta veri öznitelikleri. |

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
| provisioningContext  | Sözlük<dize, dize>                | No       |  Katalogdaki bazı öğelerin sağlanması için gereken bilgiler. SKU 'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.                  |
| Köprü                | [Orderlineıtemlinks](order-resources.md#orderlineitemlinks) | No       |  Salt okunur. Sipariş satırı öğesine karşılık gelen kaynak bağlantıları.  |
| öznitelikler           | [ResourceAttributes](utility-resources.md#resourceattributes) | No       | Orderlineıtem öğesine karşılık gelen meta veri öznitelikleri. |
| renewsTo             | Nesne dizisi                          | No    |[RenewsTo](order-resources.md#renewsto) kaynaklarından oluşan bir dizi.                                                                            |
| AttestationAccepted             | bool                 | No   |  Teklif veya SKU koşullarına yönelik anlaşmayı gösterir. Yalnızca SkuAttestationProperties veya OfferAttestationProperties Enforcekanıtlama 'nin doğru olduğu teklifler veya SKU 'lar için gereklidir.          |

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
