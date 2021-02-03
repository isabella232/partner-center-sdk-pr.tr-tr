---
title: Bir aboneliğin destek kişisini güncelleştirme
description: Bir aboneliğin destek kişisini iş ortağının değer eklenmiş satıcılarından biriyle güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c8c6b658cfe6e14c75b0c06b177920ce3eb1b4ed
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769587"
---
# <a name="update-a-subscriptions-support-contact"></a>Bir aboneliğin destek kişisini güncelleştirme

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bir aboneliğin destek kişisini iş ortağının değer eklenmiş satıcılarından biriyle güncelleştirme.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- Abonelik tanımlayıcısı.

- Yeni destek kişisi hakkında bilgi: kiracı tanımlayıcı, Microsoft İş Ortağı Ağı tanımlayıcı ve ad. Destek kişisi, ortağın değer eklenmiş satıcılarından biri olmalıdır.

## <a name="c"></a>C\#

Bir aboneliğin destek ilgili kişisini güncelleştirmek için ilk olarak bir [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.supportcontact) nesnesi oluşturun ve yeni değerlerle doldurun. Ardından müşteriyi tanımlamak için [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) YÖNTEMINI Müşteri kimliğiyle birlikte kullanın. Ardından, abonelik KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim elde edin. Ardından, iletişim işlemlerini desteklemek için bir arabirim elde etmek üzere [**supportcontact**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.supportcontact) özelliğini kullanın. Son olarak, destek kişisini güncelleştirmek için, doldurulmuş SupportContact nesnesiyle [**Update**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.update) veya [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionsupportcontact.updateasync) yöntemini çağırın.

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Instantiate a SupportContact object and populate it with the new support contact information.
var supportContact = new SupportContact()
{
    Name = "Support contact's name",
    SupportTenantId = "Support contact's tenant ID",
    SupportMpnId = "Support contact's MPN ID"
};

// Update the support contact with a new object that has valid VAR values.
var updatedSupportContact = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).SupportContact.Update(supportContact);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdateSubscriptionSupportContact.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                                                    |
|---------|--------------------------------------------------------------------------------------------------------------------------------|
| **PUT** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/supportcontact http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.

| Ad            | Tür   | Gerekli | Açıklama                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| müşteri kimliği     | string | Yes      | Müşteriyi tanımlayan GUID biçimli dize.           |
| abonelik kimliği | string | Yes      | Deneme aboneliğini tanımlayan GUID biçimli dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

İstek gövdesine doldurulmuş bir [Supportcontact](subscription-resources.md#supportcontact) kaynağı dahil etmeniz gerekir. Destek ilgili kişisi, iş ortağıyla ilişkisi olan mevcut bir satıcı olmalıdır.

### <a name="request-example"></a>İstek örneği

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b72d732a-eed7-4a60-82d1-1b2e6cba0ed2
MS-CorrelationId: 84eff9e1-6a8c-42aa-8678-c00b0d3fb26f
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 320
Expect: 100-continue

{
    "SupportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "SupportMpnId": "4391507",
    "Name": "Trey Research",
    "Links": {
        "Self": {
            "Uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "Method": "Get",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "SupportContact"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi [Supportcontact](subscription-resources.md#supportcontact) kaynağını içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 328
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b0cd9bcc-742e-4c76-9e34-a96d3bdc7673
MS-RequestId: 7591ca22-d4e3-409d-bfa6-09806eaff4f3
MS-CV: W8Tzj6NGckKHcq+E.0
MS-ServerId: 030020344
Date: Wed, 21 Jun 2017 01:01:17 GMT

{
    "supportTenantId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "supportMpnId": "4391507",
    "name": "Trey Research",
    "links": {
        "self": {
            "uri": "/customers/0C39D6D5-C70D-4C55-BC02-F620844F3FD1/subscriptions/C8D8FBAB-6A62-44DC-BE50-B7C74E43A296/supportcontact",
            "method": "Get",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "SupportContact"
    }
}
```
