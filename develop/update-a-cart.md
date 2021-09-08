---
title: Sepeti güncelleştirme
description: Sepette müşteri için sipariş güncelleştirme.
ms.date: 09/06/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 48fec2d9fb72d1a58fe79969e48ccd39a32c5ccc
ms.sourcegitcommit: 5f27733d7c984c29f71c8b9c8ba5f89753eeabc4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/07/2021
ms.locfileid: "123557295"
---
# <a name="update-a-cart"></a>Sepeti güncelleştirme

Sepette müşteri için sipariş güncelleştirme.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Mevcut sepet için sepet kimliği.

## <a name="c"></a>C\#

Müşterinin siparişlerini güncelleştirmek **için, ById()** işlevini kullanarak müşteri ve sepet kimliklerini ileterek Get() yöntemini kullanarak **sepete** sahip olun. Sepette gerekli değişiklikleri yapın. Şimdi **ById()** yöntemini kullanarak müşteri ve sepet kimliklerini kullanarak **Put** yöntemini çağır.

Son olarak, **siparişi oluşturmak için Put()** veya **PutAsync()** yöntemini arayın.

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

Bu işlemi tamamlamak ve ek kurumsal bayileri dahil etmek için aşağıdaki örnekle birlikte bakın.

### <a name="api-sample---check-out-cart"></a>API Örneği - Sepete göz at

``` csharp
{
    "orders": [
        {
            "id": "f76c6b7f449d",
            "alternateId": "f76c6b7f449d",
            "referenceCustomerId": "f81d98dd-c2f4-499e-a194-5619e260344e",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "currencySymbol": "$",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "CFQ7TTC0LH0Z:0001:CFQ7TTC0K18P",
                    "subscriptionId": "ebc0beef-7ffb-4044-c074-16f324432139",
                    "termDuration": "P1M",
                    "transactionType": "New",
                    "friendlyName": "AI Builder Capacity add-on",
                    "quantity": 1,
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
                },
                {
                    "lineItemNumber": 1,
                    "offerId": "CFQ7TTC0LFLS:0002:CFQ7TTC0KDLJ",
                    "subscriptionId": "261bac40-7d88-4327-dfa3-dacd09222d62",
                    "termDuration": "P1Y",
                    "transactionType": "New",
                    "friendlyName": "Azure Active Directory Premium P1",
                    "quantity": 2,
                    "partnerIdOnRecord": "517285",
                    "additionalPartnerIdsOnRecord": 
                        "5357564",
                        "5357563"
                    ],
                 
   "links": {
                        "product": {
                            "uri": "/products/CFQ7TTC0LFLS?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002?country=US",
                            "method": "GET",
                            "headers": []
                        },
                        "availability": {
                            "uri": "/products/CFQ7TTC0LFLS/skus/0002/availabilities/CFQ7TTC0KDLJ?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2021-08-18T07:52:23.1921872Z",
            "status": "pending",
            "transactionType": "UserPurchase",
            "links": {
                "self": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "GET",
                    "headers": []
                },
                "provisioningStatus": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "patchOperation": {
                    "uri": "/customers/f81d98dd-c2f4-499e-a194-5619e260344e/orders/f76c6b7f449d",
                    "method": "PATCH",
                    "headers": []
                }
            },
            "client": {},
            "attributes": {
                "objectType": "Order"
            }
        }
    ],
    "attributes": {
        "objectType": "CartCheckoutResult"
    }
}

```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1              |

### <a name="uri-parameters"></a>URI parametreleri

Müşteriyi tanımlamak ve güncelleştirilacak sepeti belirtmek için aşağıdaki yol parametrelerini kullanın.

| Ad            | Tür     | Gerekli | Açıklama                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | string   | Yes      | Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id.             |
| **cart-id**     | string   | Yes      | Sepeti tanımlayan GUID biçimli sepet kimliği.                     |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek [gövdesinin](cart-resources.md) Sepet özelliklerini açıklar.

| Özellik              | Tür             | Gerekli        | Açıklama                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| kimlik                    | dize           | No              | Sepetin başarıyla oluşturulmasının ardından sağlanan bir sepet tanımlayıcısı.                                  |
| creationTimeStamp     | DateTime         | No              | Sepetin tarih-saat biçiminde oluşturulma tarihi. Sepetin başarıyla oluşturulmasının ardından uygulanır.        |
| lastModifiedTimeStamp | DateTime         | No              | Sepetin en son güncelleştirilen tarih-saat biçiminde olduğu tarih. Sepetin başarıyla oluşturulmasının ardından uygulanır.    |
| expirationTimeStamp   | DateTime         | No              | Sepet tarih-saat biçiminde sona erer.  Sepetin başarıyla oluşturulmasının ardından uygulanır.            |
| lastModifiedUser      | dize           | No              | Sepeti en son güncelleştirilen kullanıcı. Sepetin başarıyla oluşturulmasının ardından uygulanır.                             |
| lineItems             | Nesne dizisi | Yes             | [Bir CartLineItem kaynakları](cart-resources.md#cartlineitem) dizisi.                                               |

Bu tablo, istek [gövdesinin CartLineItem](cart-resources.md#cartlineitem) özelliklerini açıklar.

| Özellik             | Tür                        | Gerekli     | Açıklama                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| kimlik                   | dize                      | No           | Sepet satır öğesi için benzersiz tanımlayıcı. Sepetin başarıyla oluşturulmasının ardından uygulanır.                |
| catalogId            | string                      | Yes          | Katalog öğesi tanımlayıcısı.                                                                       |
| Friendlyname         | dize                      | No           | İsteğe bağlı. Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.              |
| miktar             | int                         | Yes          | Lisans veya örnek sayısı.     |
| currencyCode         | dize                      | No           | Para birimi kodu.                                                                                 |
| billingCycle         | Nesne                      | Yes          | Geçerli dönem için ayarlanmış faturalama dönemi türü.                                              |
| Katılımcılar         | Nesne Dizesi çiftlerinin listesi | No           | Satın alma ile ilgili katılımcılardan bir koleksiyon.                                                      |
| provisioningContext  | Sözlük<dizesi, dize>  | No           | Teklifin sağlanması için kullanılan bağlam.                                                          |
| orderGroup           | dize                      | No           | Hangi öğelerin bir araya yerleştiril olduğunu belirten bir grup.                                            |
| error                | Nesne                      | No           | Bir hata durumunda sepet oluşturulduktan sonra uygulanır.                                                 |
| AdditionalPartnerIdsOnRecord | Dize | No | Dolaylı sağlayıcı dolaylı bir kurumsal bayi adına sipariş verdiylerinde, bu alanı yalnızca Ek dolaylı kurumsal bayinin MPN kimliğiyle **(dolaylı** sağlayıcının kimliği hiçbir zaman) doldurmak. Teşvikler bu ek kurumsal bayiler için geçerli değildir. Yalnızca en fazla 5 Dolaylı Kurumsal Bayi girilebilir. Bu yalnızca AB /EFTA ülkeleri içinde işlem yapılan iş ortakları için geçerlidir.  |

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

Başarılı olursa, bu yöntem yanıt [gövdesinde](cart-resources.md) doldurulmuş Sepet kaynağını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

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
