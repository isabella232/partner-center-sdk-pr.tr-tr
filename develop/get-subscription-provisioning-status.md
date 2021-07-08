---
title: Abonelik sağlama durumunu alma
description: Bir müşteri aboneliği için abonelik sağlama durumunu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8797fa494cd77f11a1179d6406ca021f0d7788c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548711"
---
# <a name="get-subscription-provisioning-status"></a>Abonelik sağlama durumunu alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bir müşteri aboneliği için abonelik sağlama durumunu alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik tanımlayıcısı.

- Bu işlemi gerçekleştirmek için abonelikte yönetici temsilcisi izinleri gereklidir.

## <a name="c"></a>C\#

Bir aboneliğin sağlama durumunu almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın. Ardından, abonelik KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim elde edin. Ardından, geçerli aboneliğin sağlama durumu işlemlerine bir arabirim almak için [**Provisioningstatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) özelliğini kullanın ve ardından [**subscriptionprovisioningstatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) nesnesini almak Için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/provisioningstatus http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad            | Tür   | Gerekli | Açıklama                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| müşteri kimliği     | string | Yes      | Müşteriyi tanımlayan GUID biçimli dize.     |
| abonelik kimliği | string | Yes      | Aboneliği tanımlayan GUID biçimli dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

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

Başarılı olursa, yanıt gövdesi bir [Subscriptionprovisioningstatus](subscription-resources.md#subscriptionprovisioningstatus) kaynağı içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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

- Lisans değişikliği ataması sırasında, [Subscriptionprovisioningstatus](subscription-resources.md#subscriptionprovisioningstatus) içindeki durum alanı "bekliyor" olarak ayarlanır.

- Durum alanı 15 dakikada bir güncelleştirilir.
