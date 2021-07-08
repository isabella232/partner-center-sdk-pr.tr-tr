---
title: Müşterinin tüm kullanıcı hesaplarının listesini alma
description: Müşterilerinizden birinin ait olduğu tüm kullanıcı hesaplarının listesini nasıl elde edersiniz?
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f3d5fcc610eae8c1bff056c1e4a9e7a74093c87d
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874576"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a>Müşterinin tüm kullanıcı hesaplarının listesini alma

Bu makalede, müşterilerinizden birinin ait olduğu tüm kullanıcı hesaplarının listesini nasıl alasınız?

Kimlikle tek bir kullanıcı hesabı aray için [bkz. Kimliğine göre bir kullanıcı hesabı al.](get-a-user-account-by-id.md)

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="c"></a>C\#

Belirtilen bir müşteri için tüm kullanıcı hesaplarının koleksiyonunu almak için:

1. Müşteriyi [**tanımlamak için belirtilen müşteri kimliğiyle IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırma.

2. Koleksiyonu almak [**için Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) [**veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) yöntemini çağırma.

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

Bir örnek için aşağıdakilere bakın:

- Örnek: [Konsol test uygulaması](console-test-app.md)
- Project: **İş Ortağı Merkezi SDK'sı Örnekleri**
- Sınıf: **GetCustomerUserCollection.cs**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Doğru müşteriyi belirlemek için aşağıdaki URI parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem müşteri için bir kullanıcı hesabı koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1030
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CV: 6zmKqrSFB0+t7m3y.0
MS-ServerId: 101112616
Date: Wed, 21 Dec 2016 21:13:24 GMT

 {
    "totalCount": 2,
    "items": [{
            "usageLocation": "US",
            "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
            "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "Daniel Tsai",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }, {
            "id": "6e668259-1f09-479d-bcb8-d9b03e826b8d",
            "userPrincipalName": "admin@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "DT Demo CSP Customer 005",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/6e668259-1f09-479d-bcb8-d9b03e826b8d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
