---
title: Tümleştirme korumalı alandan siparişi iptal etme
description: Tümleştirme korumalı alan hesaplarından İş Ortağı Merkezi abonelik siparişlerini iptal etmek için api'leri kullanmayı öğrenin.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c4b658f406e420d8d3cd425688364fe3d440d3d
ms.sourcegitcommit: a3a78ec0f5078645b5a4f3b534165eef30f2c822
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/30/2021
ms.locfileid: "113104980"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Api'leri kullanarak tümleştirme korumalı alandan İş Ortağı Merkezi iptal etme

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu makalede tümleştirme korumalı alan hesaplarından farklı İş Ortağı Merkezi sipariş türlerini iptal etmek için api'leri kullanma işlemi açıklanmıştır. Bu tür siparişler ayrılmış örnekler, yazılımlar ve ticari market Hizmet Olarak Yazılım (SaaS) abonelik siparişlerini içerebilir.

> [!NOTE] 
> Ayrılmış örnek veya ticari market SaaS abonelik siparişlerinin iptallerinin yalnızca tümleştirme korumalı alan hesaplarından mümkün olduğunu unutmayın. 60 günden eski olan tüm korumalı alan siparişleri, İş Ortağı Merkezi.

API aracılığıyla yazılım üretim siparişlerini iptal etmek için [cancel-software-purchases kullanın.](cancel-software-purchases.md)
Ayrıca, satın alma işlemini iptal etmek için pano aracılığıyla yazılım üretim [siparişlerini iptal edebilirsiniz.](/partner-center/csp-software-subscriptions)

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Etkin ayrılmış örnek / yazılım / üçüncü taraf SaaS abonelik siparişleri olan bir müşteriyle tümleştirme korumalı alan iş ortağı hesabı.

## <a name="c"></a>C\#

Tümleştirme korumalı alandan bir siparişi iptal etmek için hesap kimlik bilgilerinizi yöntemine iletir ve iş ortağı [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) işlemlerini almak için bir arabirim elde [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) edin.

Belirli bir [Sipariş seçmek için](order-resources.md#order)iş ortağı işlemlerini kullanın ve müşteri tanımlayıcısını müşteri tanımlayıcısıyla birlikte çağırma yöntemini, ardından sipariş tanımlayıcısını kullanarak siparişi ve son olarak da alma [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini **`Orders.ById()`** **`Get`** **`GetAsync`** belirtin.

özelliğini [**`Order.Status`**](order-resources.md#order) olarak ayarlayın `cancelled` ve yöntemini kullanarak **`Patch()`** siparişi güncelleştirin.

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem     | İstek URI'si                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **Yama** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir. |
| **order-id** | **string** | Y        | değeri, iptal edilmesi gereken sipariş kimliklerini not alan bir dizedir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem iptal edilen siparişi döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
