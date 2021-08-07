---
title: İş ortağı MPN kimliğine göre bir müşterinin aboneliğini alma
description: Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: ebc3dc1bf557f502468f43076663b7ca1b55e7d1d8fc9ae12a8e0b2a27a21b02
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990877"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a>İş ortağı MPN kimliğine göre bir müşterinin aboneliğini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Belirli bir müşteriye verilen bir Microsoft İş Ortağı Ağı (MPN) iş ortağı tarafından sağlanan Aboneliklerin listesini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- İş ortağı MPN tanımlayıcısı.

## <a name="c"></a>C\#

Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın. Ardından, [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğinden müşteri aboneliği koleksiyonu işlemlerine yönelik bir arabirim alın ve iş ortağını tanımlamak ve iş ortağı abonelik işlemlerine bir arabirim almak için MPN kimliğiyle [**bypartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) yöntemini çağırın. Son olarak, koleksiyonu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) yöntemini çağırın.

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getsubscriptionsbympnıd. cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE **ıaggregatepartner. getCustomers. Byıd** işlevini kullanın. Ardından, **Getabonelikler** işlevinden müşteri aboneliği koleksiyonu işlemlerine bir arabirim alın ve iş ortağını tanımlamak ve iş ortağı abonelik işlemlerine bir arabirim almak için MPN kimliğiyle **bypartner** işlevini çağırın. Son olarak, koleksiyonu almak için **Get** işlevini çağırın.

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini almak için [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) komutunu yürütün. Müşteriyi belirlemek için müşteri KIMLIĞINI belirtin ve **CustomerID** parametresini kullanarak **MPNıD** parametresini MPN kimliğiyle doldurun ve iş ortağını belirleyin.

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si |
|---------|----------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/abonelikler? MPN \_ ID = {MPN-id} http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve ortağı belirlemek için aşağıdaki yolu ve sorgu parametrelerini kullanın.

| Ad        | Tür   | Gerekli | Açıklama                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| müşteri kimliği | string | Yes      | Müşteriyi tanımlayan GUID biçimli dize.       |
| MPN kimliği      | int    | Yes      | Ortağı tanımlayan Microsoft İş Ortağı Ağı KIMLIĞI. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi [abonelik](subscription-resources.md) kaynakları koleksiyonunu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a>Ayrıca bkz.

- [İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
