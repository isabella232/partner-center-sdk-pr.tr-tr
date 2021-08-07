---
title: Yazılım satın alımlarını iptal etme
description: Yeni API'leri kullanarak yazılım aboneliklerini ve kalıcı yazılım satın almalarını iptal İş Ortağı Merkezi seçeneği.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f7dfa5122c585a8519312e8492922f718a51972f177a12d7431015e1cdcb5d06
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992203"
---
# <a name="cancel-software-purchases"></a>Yazılım satın alımlarını iptal etme

Yazılım aboneliklerini ve kalıcı yazılım satın almalarını iptal etmek için İş Ortağı Merkezi API'lerini kullanabilirsiniz (bu satın alma işlemleri satın alma tarihine kadar iptal penceresinde yapılmış olduğu sürece). Bu tür iptaller yapmak için bir destek bileti oluşturmanıza gerek yok ve bunun yerine aşağıdaki self servis yöntemleri kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="c"></a>C\#

Bir yazılım siparişini iptal etmek için,

1. İş ortağı işlemlerini almak için bir [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) arabirimi almak için [**createPartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) yöntemine hesap kimlik bilgilerinizi girin.

2. İptal etmek [istediğiniz belirli](order-resources.md#order) bir Siparişi seçin. Müşteri [**tanımlayıcısıyla Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini, ardından sipariş **tanımlayıcısıyla Orders.ById()** yöntemini arayın.

3. Siparişi almak **için Get** **veya GetAsync** yöntemini çağırma.

4. [**Order.Status özelliğini**](order-resources.md#order) olarak `cancelled` ayarlayın.

5. (İsteğe bağlı) İptal için belirli satır öğelerini belirtmek için [**Order.LineItems'i**](order-resources.md#order) iptal etmek istediğiniz satır öğelerinin listesine ayarlayın.

6. Siparişi **güncelleştirmek için Patch()** yöntemini kullanın.

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem     | İstek URI'si                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Yama** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Bir müşteriyi silmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, kurumsal bayinin kurumsal bayiye ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı tanımlayıcısıdır. |
| **order-id** | **string** | Y        | değeri, iptal etmek istediğiniz siparişin tanımlayıcısını ifade eder. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem iptal edilen satır öğeleriyle siparişi döndürür.

Sipariş durumu, **siparişteki** tüm satır öğeleri iptal edilirse iptal edildi  olarak işaretlenir veya siparişteki tüm satır öğeleri iptal edilmezse tamamlanmış olur.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

Aşağıdaki örnek yanıtta teklif tanımlayıcısına sahip satır öğesi miktarının sıfır **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** (0) olduğunu görüyorsunuz. Bu değişiklik, iptal için işaretlenmiş satır öğesinin başarıyla iptal edildiği anlamına gelir. Örnek sipariş, iptal edile diğer satır öğelerini içerir. Başka bir ifadeyle, genel siparişin durumu tamamlandı **olarak** işaretlenir, iptal **edilmez.**

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
