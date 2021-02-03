---
title: Sepeti güncelleştirme
description: Bir sepetteki müşteri için bir siparişi güncelleştirme.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768939"
---
# <a name="update-a-cart"></a>Sepeti güncelleştirme

**Uygulama hedefi**

- İş Ortağı Merkezi

Bir sepetteki müşteri için bir siparişi güncelleştirme.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Mevcut bir sepet için sepet KIMLIĞI.

## <a name="c"></a>C\#

Müşterinin bir siparişini güncelleştirmek için, **Byıd ()** işlevini kullanarak müşteriyi ve sepet kimliğini geçirerek **Get ()** yöntemini kullanarak sepetini alın. Sepette gerekli değişiklikleri yapın. Şimdi, **Byıd ()** yöntemini kullanarak Customer ve sepet kimliği ' ni kullanarak **PUT** metodunu çağırın.

Son olarak, siparişi oluşturmak için **PUT ()** veya **PutAsync ()** metodunu çağırın.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts/{cart-id} http/1.1              |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi tanımlamak için aşağıdaki yol parametrelerini kullanın ve güncelleştirileceğini seçin.

| Ad            | Tür     | Gerekli | Açıklama                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **müşteri kimliği** | string   | Yes      | Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.             |
| **sepet kimliği**     | string   | Yes      | Sepeti tanımlayan bir GUID biçimli sepet kimliği.                     |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde [sepet](cart-resources.md) özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| kimlik                    | dize           | No              | Sepet başarıyla oluşturulduktan sonra sağlanan bir sepet tanımlayıcısı.                                  |
| creationTimeStamp     | DateTime         | No              | Sepetin oluşturulduğu tarih ve saat biçimi. Sepet başarıyla oluşturulduktan sonra uygulandı.        |
| lastModifiedTimeStamp | DateTime         | No              | Sepetin son güncelleştirildiği tarih ve saat biçimi. Sepet başarıyla oluşturulduktan sonra uygulandı.    |
| expirationTimeStamp   | DateTime         | No              | Sepetin süresinin dolacağı tarih-saat biçiminde.  Sepet başarıyla oluşturulduktan sonra uygulandı.            |
| lastModifiedUser      | dize           | No              | Sepetini son güncelleştiren Kullanıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                             |
| LineItems             | Nesne dizisi | Yes             | Bir [Cartlineıtem](cart-resources.md#cartlineitem) kaynakları dizisi.                                               |

Bu tablo, istek gövdesinde [Cartlineıtem](cart-resources.md#cartlineitem) özelliklerini açıklar.

| Özellik             | Tür                        | Gerekli     | Açıklama                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| kimlik                   | dize                      | No           | Sepet çizgisi öğesi için benzersiz bir tanımlayıcı. Sepet başarıyla oluşturulduktan sonra uygulandı.                |
| catalogId            | string                      | Yes          | Katalog öğesi tanımlayıcısı.                                                                       |
| friendlyName         | dize                      | No           | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.              |
| miktar             | int                         | Yes          | Lisans veya örnek sayısı.     |
| currencyCode         | dize                      | No           | Para birimi kodu.                                                                                 |
| Bilimlingcycle         | Nesne                      | Yes          | Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                              |
| Katılımcılar         | Nesne dizesi çiftlerinin listesi | No           | Satın alımdaki katılımcılar koleksiyonu.                                                      |
| provisioningContext  | Sözlük<dize, dize>  | No           | Teklifin sağlanması için kullanılan bir bağlam.                                                          |
| orderGroup           | dize                      | No           | Hangi öğelerin birlikte yerleştirilebileceğini belirten bir grup.                                            |
| error                | Nesne                      | No           | Bir hata durumunda sepet oluşturulduktan sonra uygulandı.                                                 |

### <a name="request-example"></a>İstek örneği

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [sepet](cart-resources.md) kaynağını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
