---
title: Bir aboneliğin miktarını değiştirme
description: Bir müşteri aboneliği için lisans miktarını değiştirmek üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Bunu Iş Ortağı Merkezi panosunda da yapabilirsiniz.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770072"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a>Bir müşteri aboneliğinde lisans miktarını değiştirme

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Lisans miktarını artırmak veya azaltmak için bir [aboneliği](subscription-resources.md) güncelleştirir.

Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir. Sonra, söz konusu dosyayı yeniden adlandırmak istediğiniz aboneliği seçin. Son olarak, **Miktar** alanındaki değeri değiştirin ve ardından Gönder ' i seçin **.**

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik KIMLIĞI.

## <a name="c"></a>C\#

Bir müşterinin aboneliğine ait miktarı değiştirmek için önce [aboneliği alın](get-a-subscription-by-id.md), sonra aboneliğin [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) özelliğini değiştirin. Değişiklik yapıldıktan sonra **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın. Ardından, ve ardından [**Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemiyle [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın. Ardından, **Patch ()** yöntemini çağırarak son ' u kullanabilirsiniz.

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Partnersdk. Featuresample **sınıfı**: UpdateSubscription.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem    | İstek URI'si                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **DÜZELTMESI** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bu tabloda, abonelik miktarını değiştirmek için gerekli sorgu parametresi listelenmektedir.

| Ad                    | Tür     | Gerekli | Açıklama                               |
|-------------------------|----------|----------|-------------------------------------------|
| **Müşteri-Kiracı kimliği**  | **guid** | Y        | Müşteriye karşılık gelen bir GUID.     |
| **abonelik kimliği** | **guid** | Y        | Aboneliğe karşılık gelen bir GUID. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesinde tam bir **abonelik** kaynağı gereklidir. **Quantity** özelliğinin güncelleştirildiğinden emin olun.

### <a name="request-example"></a>İstek örneği

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir **http durum 200** durum kodu ve güncelleştirilmiş [abonelik kaynak](subscription-resources.md)  özellikleri döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu döndürür. Durum kodunu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

Düzeltme Eki işlemi beklenen süreden uzun sürerse, Iş ortağı merkezi bir **http durum 202** durum kodu ve aboneliğin nereden alındığını gösteren bir konum üst bilgisi gönderir. Durum ve miktar değişikliklerini izlemek için aboneliği düzenli aralıklarla sorgulayabilirsiniz.

### <a name="response-examples"></a>Yanıt örnekleri

#### <a name="response-example-1"></a>Yanıt örneği 1

**Http durumu 200** olan başarılı istek durum kodu:

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "active",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

#### <a name="response-example-2"></a>Yanıt örneği 2

**Http durumu 202** olan başarılı istek durum kodu:

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
