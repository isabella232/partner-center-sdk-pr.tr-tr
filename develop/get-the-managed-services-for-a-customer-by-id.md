---
title: Kimliğe göre bir müşterinin yönetilen hizmetlerini alma
description: Müşteri için yönetilen hizmetleri alır. Başka bir deyişle, yönetici ayrıcalıkları için temsilci olarak seçen müşterinin tüm aboneliklerinin bağlantılarını edinin. Microsoft ile destek ve dosya hizmeti istekleri sağlamak için bu bağlantıları kullanabilirsiniz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cf7e7b62113bd96b00fdc2301e4e7ac4f5d4243
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548456"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a>Kimliğe göre bir müşterinin yönetilen hizmetlerini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Müşteri için yönetilen hizmetleri alır. Başka bir deyişle, yönetici ayrıcalıkları için temsilci olarak seçen müşterinin tüm aboneliklerinin bağlantılarını edinin. Microsoft ile destek ve dosya hizmeti istekleri sağlamak için bu bağlantıları kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="c"></a>C\#

Bir müşteri için tüm yönetilen hizmetlerin listesini görüntülemek için **IAggregatePartner.Customers** koleksiyonu kullanın ve [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) arayın. Ardından [**ManagedServices özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) ve ardından [**Get() veya**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) yöntemlerini çağırabilirsiniz.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** PartnerCenterSDK.FeaturesSamples **Sınıfı:** CustomerManagedServices.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşterinin yönetilen hizmetlerini almak için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                           |
|------------------------|----------|----------|---------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Müşteriye karşılık gelen bir GUID. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt **gövdesinde Yönetilen Hizmet** nesnelerinin bir koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
