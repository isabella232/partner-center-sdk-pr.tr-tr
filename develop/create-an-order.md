---
title: Müşteri siparişi oluşturma
description: Müşteri için sipariş İş Ortağı Merkezi API'leri kullanmayı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 232888ee798b4579246bbfd787e049f9f6e2e8a3
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557261"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a>İş Ortağı Merkezi API'lerini kullanarak müşteri için sipariş oluşturma

**Için geçerlidir:** İş Ortağı Merkezi | 21Vianet İş Ortağı Merkezi tarafından çalıştırılan | İş Ortağı Merkezi için Microsoft Cloud for US Government

Azure ayrılmış **VM örneği ürünleri için sipariş oluşturma yalnızca** *aşağıdakiler için* geçerlidir:

- İş Ortağı Merkezi

Satış için şu anda nelerin kullanılabilir olduğu hakkında bilgi için [bkz. Bulut Çözümü Sağlayıcısı programda iş ortağı teklifleri.](/partner-center/csp-offers)

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

5. Doğrulandıktan sonra ek kurumsal bayileri dahil etmek için aşağıdaki örnek İstek ve Yanıt Örneklerine bakın:

### <a name="request-example"></a>İstek örneği

``` csharp
{
    "PartnerOnRecordAttestationAccepted":true, 
    "lineItems": [
        {
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "quantity": 1,
            "lineItemNumber": 0,
            "PartnerIdOnRecord": "873452",
            "AdditionalPartnerIdsOnRecord":["4847383","873452"]
        }
    ],
    "billingCycle": "monthly"
}
```

### <a name="response-example"></a>Yanıt örneği

``` csharp
{
    "id": "5cf72f146967",
    "alternateId": "5cf72f146967",
    "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
    "billingCycle": "monthly",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
            "subscriptionId": "fcddfa52-1da8-4529-d347-50ea51e1e7be",
            "termDuration": "P1M",
            "transactionType": "New",
            "friendlyName": "AI Builder Capacity add-on",
            "quantity": 1,
            "partnerIdOnRecord": "873452",
            "additionalPartnerIdsOnRecord": [
                "4847383",
                "873452"
            ],
            "links": {
                "product": {
                    "uri": "/products/CFQ7TTC0LH0Z?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/CFQ7TTC0LH0Z/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/CFQ7TTC0LH0Z/skus/0001/availabilities/CFQ7TTC0K18P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2021-08-17T18:13:11.3122226Z",
    "status": "pending",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/5cf72f146967",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {},
    "attributes": {
        "objectType": "Order"
    }
}

```

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
| **YAYINLA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                                |
|-------------|--------|----------|------------------------------------------------------------|
| customer-id | string | Yes      | Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

#### <a name="order"></a>Sipariş

Bu tabloda istek [gövdesinde Sipariş](order-resources.md) özellikleri açık edilmektedir.

| Özellik             | Tür                        | Gerekli                        | Açıklama                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| kimlik                   | dize                      | No                              | Siparişin başarıyla oluşturulmasının ardından sağlanan bir sipariş tanımlayıcısı.   |
| referenceCustomerId  | dize                      | No                              | Müşteri tanımlayıcısı. |
| billingCycle         | dize                      | No                              | İş ortağının bu sipariş için faturalandırılama sıklığını gösterir. Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır. Varsayılan değer, sipariş oluşturma sırasında "Monthly" veya "OneTime" şeklindedir. Bu alan, siparişin başarıyla oluşturulmasının ardından uygulanır. |
| lineItems            | [OrderLineItem kaynakları](order-resources.md#orderlineitem) dizisi | Yes      | Miktarı da dahil olmak üzere müşterinin satın alma tekliflerinin maddeli listesi.        |
| currencyCode         | dize                      | No                              | Salt okunur. Siparişin yerleştirilmesi için kullanılan para birimi. Siparişin başarıyla oluşturulmasının ardından uygulanır.           |
| Creationdate         | datetime                    | No                              | Salt okunur. Siparişin tarih-saat biçiminde oluşturulma tarihi. Siparişin başarıyla oluşturulmasının ardından uygulanır.                                   |
| durum               | dize                      | No                              | Salt okunur. Siparişin durumu.  Desteklenen değerler OrderStatus içinde bulunan [üye adlarıdır.](order-resources.md#orderstatus)        |
| Bağlantı                | [OrderLinks](utility-resources.md#resourcelinks)              | No                              | Siparişe karşılık gelen kaynak bağlantıları. |
| öznitelikler           | [ResourceAttributes](utility-resources.md#resourceattributes) | No                              | Sıraya karşılık gelen meta veri öznitelikleri. |
| Partneronrecordattestationkabul edildi | Boole | Yes | Kanıtlama tamamlamayı onaylar |


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
| Additionalpartnerıdsonrecord | Dize | No | Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca ek dolaylı** satıcının MPN kimliğiyle doldurun (dolaylı sağlayıcının kimliği hiçbir zaman değildir). Teşvikleri bu ek satıcılar için geçerli değildir. Yalnızca en fazla 5 dolaylı satıcıda girilebilir. Bu, AB/EFTA ülkelerinde yalnızca geçerli iş ortakları deneyimidir. |

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
