---
title: Tümleştirme korumalı alanı 'ndan bir siparişi iptal etme
description: Iş Ortağı Merkezi API 'Lerini, tümleştirme korumalı alanı hesaplarından farklı türdeki abonelik siparişlerinin iptal etmek için nasıl kullanacağınızı öğrenin.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3bf862c62804a56e6f73dd3ec36d2e9eb65f997
ms.sourcegitcommit: f59a9311c8a37d45695caf74794ec1697426acc9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2021
ms.locfileid: "108210028"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a>Iş Ortağı Merkezi API 'Lerini kullanarak tümleştirme korumalı alanından bir siparişi iptal etme

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, Iş Ortağı Merkezi API 'Lerinin, tümleştirme korumalı alanı hesaplarından farklı abonelik siparişlerinin türlerini iptal etmek için nasıl kullanılacağı açıklanır. Bu şekilde, ayrılmış örnekler, yazılımlar ve hizmet olarak satılan Market (SaaS) abonelik siparişleri bulunabilir.

>[!NOTE] 
>Lütfen ayrılmış örneğin iptalinin veya ticari Market SaaS Abonelik siparişlerinin yalnızca tümleştirme korumalı alanı hesaplarından yapılacağına dikkat edin. 60 günden eski olan tüm korumalı alan siparişleri Iş Ortağı Merkezi 'nden iptal edilemez. Yardıma ihtiyacınız varsa, Iş Ortağı Merkezi desteğine ulaşın. 

API aracılığıyla yazılım üretim emirlerini iptal etmek için [iptal-yazılım-satın](cancel-software-purchases.md)alma kullanın.
Ayrıca, [satın alma işlemini iptal etmek](/partner-center/csp-software-subscriptions)için pano aracılığıyla yazılımın üretim emirlerini iptal edebilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteriyle, etkin ayrılmış örnek/yazılım/üçüncü taraf SaaS Abonelik emirlerine sahip bir tümleştirme korumalı alan iş ortağı hesabı.

## <a name="c"></a>C\#

Tümleştirme korumalı alanından bir siparişi iptal etmek için, [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) iş ortağı işlemlerini almak üzere bir arabirim almak üzere hesap kimlik bilgilerinizi metoduna geçirin.

Belirli bir [siparişi](order-resources.md#order)seçmek için müşteri tanımlayıcısı ile iş ortağı işlemlerini ve çağrı [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın, ardından siparişi **`Orders.ById()`** ve son olarak **`Get`** ya da alma yöntemini belirtmek için Order Identifier ' ı seçin **`GetAsync`** .

[**`Order.Status`**](order-resources.md#order)Özelliğini olarak ayarlayın `cancelled` ve **`Patch()`** sıralamayı güncelleştirmek için yöntemini kullanın.

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

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem     | İstek URI'si                                                                            |
|------------|----------------------------------------------------------------------------------------|
| **DÜZELTMESI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | **guid** | Y        | Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir. |
| **sıra kimliği** | **string** | Y        | Değer, iptal edilmesi gereken sıra kimliklerini belirten bir dizedir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

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

Başarılı olursa, bu yöntem iptal edildi sırasını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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
