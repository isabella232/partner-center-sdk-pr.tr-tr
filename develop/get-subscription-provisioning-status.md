---
title: Abonelik sağlama durumunu alma
description: Müşteri aboneliği için abonelik sağlama durumunu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b36776279171186da7d81f9c1ff3d0828206fc2749ab8108f882ad7460575d60
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995569"
---
# <a name="get-subscription-provisioning-status"></a>Abonelik sağlama durumunu alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Müşteri aboneliği için abonelik sağlama durumunu alma.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Abonelik tanımlayıcısı.

- Bu işlemi gerçekleştirmek için abonelikte yönetici temsilcisi izinleri gereklidir.

## <a name="c"></a>C\#

Bir aboneliğin sağlama durumunu almak için müşteri kimliğini kullanarak [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak müşteriyi tanıyın. Ardından abonelik kimliğiyle [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim alın. Ardından [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) özelliğini kullanarak geçerli aboneliğin sağlama durumu işlemlerine bir arabirim alın ve [**Ardından SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) nesnesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) yöntemini çağırabilirsiniz.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad            | Tür   | Gerekli | Açıklama                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| customer-id     | string | Yes      | Müşteriyi tanımlayan GUID biçimli bir dize.     |
| subscription-id | string | Yes      | Aboneliği tanımlayan GUID biçimli bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt gövdesi bir [SubscriptionProvisioningStatus kaynağı](subscription-resources.md#subscriptionprovisioningstatus) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a>Açıklamalar

- Lisans değişikliği ataması sırasında [SubscriptionProvisioningStatus'daki](subscription-resources.md#subscriptionprovisioningstatus) durum alanı "beklemede" olarak ayarlanır.

- Durum alanı her 15 dakikada bir güncelleştirilir.
