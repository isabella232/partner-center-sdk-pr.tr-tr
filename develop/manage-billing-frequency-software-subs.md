---
title: Yazılım abonelikleri için faturalama sıklığını yönetme
description: Müşteri ve abonelik kimliğiyle eşleşen bir Abonelik kaynağı için faturalama sıklığını güncelleştirin.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3cacfe94868afb0b4c1c93842b187d653dffe64f
ms.sourcegitcommit: 36e88224d0957b7ea6298789c75cdd18fc0f3685
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2021
ms.locfileid: "129664943"
---
# <a name="update-billing-frequency-for-software-subscriptions"></a>Yazılım abonelikleri için faturalama sıklığını güncelleştirme

**Uygulama:** İş Ortağı Merkezi

Müşteri ve abonelik kimliğiyle [eşleşen](subscription-resources.md) bir yazılım Aboneliği kaynağının faturalama sıklığını güncelleştirin.

Bu İş Ortağı Merkezi, önce bir müşteri [seçerek gerçekleştirilir.](get-a-customer-by-name.md) Ardından güncelleştirmek istediğiniz aboneliği seçin. Son olarak, seçeneği seçmek için Zamanlanmış değişiklikleri yönet'e tıklayın ve **kaydet'i seçin.**

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi'den **CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Abonelik kimliği.

## <a name="c"></a>C\#

Müşterinin yazılım aboneliğini güncelleştirmek için önce [Aboneliği alın,](get-a-subscription-by-id.md)ardından aboneliğin [**billingCycle özelliğini**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.billingCycle) ayarlayın. Değişiklik yapıldıktan sonra **IAggregatePartner.Customers** koleksiyonu kullanın ve **ById() yöntemini** arayın. Ardından [**Subscriptions özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) ve ardından [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) çağırabilirsiniz. Ardından Patch() yöntemini **çağırarak bitirin.**

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

this.Context.ConsoleHelper.StartProgress("Updating subscription scheduled change");
selectedSubscription.ScheduledNextTermInstructions = new ScheduledNextTermInstructions
{
    Product = new ProductTerm
    {
        ProductId = changeToProductId,
        SkuId = changeToSkuId,
        AvailabilityId = changeToAvailabilityId,
        BillingCycle = changeToBillingCycle,
        TermDuration = changeToTermDuration,
    },
    Quantity = changeToQuantity,
};

var updatedSubscription = subscriptionOperations.Patch(selectedSubscription);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** PartnerSDK.FeatureSample **Sınıfı:** UpdateSubscription.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem    | İstek URI'si                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| **YAMA** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Bu tabloda aboneliği askıya almak için gereken sorgu parametresi listelemektedir.

| Ad                    | Tür     | Gerekli | Açıklama                               |
|-------------------------|----------|----------|-------------------------------------------|
| **customer-tenant-id**  | **GUID** | Y        | Müşteriye karşılık gelen bir GUID.     |
| **abonelik için id** | **GUID** | Y        | Aboneliğe karşılık gelen BIR GUID. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

İstek gövdesinde **tam** bir ticari market Abonelik kaynağı gereklidir. **AutoRenewEnabled özelliğinin** güncelleştirilmiş olduğundan emin olun.

### <a name="request-example-for-a-software-subscription"></a>Yazılım aboneliği için istek örneği

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 
    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt [gövdesinde](subscription-resources.md) güncelleştirilmiş Abonelik kaynağı özelliklerini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
{ 
    "id": "d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
    "offerId": "DG7GMGF0DVSV:000P:DG7GMGF0F3Q9", 
    "offerName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "friendlyName": "Windows Server Remote Desktop Services CAL - 1 User CAL – 3 year", 
    "productType": { 
        "id": "Software", 
        "displayName": "Software" 
    }, 
    "quantity": 1, 
    "unitType": "Licenses", 
    "hasPurchasableAddons": false, 
    "creationDate": "2021-09-14T16:44:14.1210743Z", 
    "effectiveStartDate": "2021-09-14T16:44:03.4609789Z", 
    "commitmentEndDate": "2024-09-13T00:00:00Z", 
    "cancellationAllowedUntilDate": "2021-10-14T23:59:00Z", 
    "status": "active", 
    "autoRenewEnabled": true, 
    "scheduledNextTermInstructions": { 
      "product": { 
         "productId":  "DG7GMGF0DVSV", 
         "skuId":  "000P", 
         "availabilityId":  "DG7GMGF0F3Q9", 
         "billingCycle":  "Annual", 
         "termDuration":  "P3Y" 
        }, 
      "quantity":  1 
     },  // original value = null 

    "isTrial": false, 
    "billingType": "license", 
    "billingCycle": "triennial", 
    "termDuration": "P3Y", 
    "renewalTermDuration": "", 
    "isMicrosoftProduct": true, 
    "partnerId": "", 
    "attentionNeeded": false, 
    "actionTaken": false, 
    "contractType": "subscription", 
    "links": { 
        "product": { 
            "uri": "/products/DG7GMGF0DVSV?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "sku": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "availability": { 
            "uri": "/products/DG7GMGF0DVSV/skus/000P/availabilities/DG7GMGF0F3Q9?country=US", 
            "method": "GET", 
            "headers": [] 
        }, 
        "self": { 
            "uri": "/customers/1f53d7b3-cd04-43a3-a09f-e52f3eb3c205/subscriptions/d3b7c9a2-9a4b-40b2-b075-6e442909e3e7", 
            "method": "GET", 
            "headers": [] 
        } 
    }, 
    "publisherName": "Microsoft", 
    "orderId": "123456789101", 
    "attributes": { 
        "objectType": "Subscription" 
    } 
} 
```
