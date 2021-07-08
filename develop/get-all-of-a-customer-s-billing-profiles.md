---
title: Müşterinin faturalandırma profilini alma
description: Müşterinin faturalama profilini alır. Bu İş Ortağı Merkezi, önce bir müşteri seçerek gerçekleştirebilirsiniz.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d22be53a5be4efcda76a568578468615495febb6
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760598"
---
# <a name="get-a-customers-billing-profile"></a>Müşterinin faturalandırma profilini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Müşterinin faturalama profilini alır.

Bu İş Ortağı Merkezi önce bir müşteri [seçerek gerçekleştirebilirsiniz.](get-a-customer-by-name.md) Ardından, sol kenar çubuğuna müşterinin adının altında Hesap'ı **seçin.** Faturalama profili Fatura bilgileri **başlığı altında** bulunabilir.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="c"></a>C\#

Müşterinin faturalama profilini almak için [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonu kullanın ve [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) arayın. Ardından [**Profiles özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) ve ardından [**Faturalama**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) özelliğini arayın. Son olarak [**Get() veya**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) [**GetAsync() yöntemlerini**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) arayın.

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** PartnerSDK.FeatureSamples **Sınıfı:** GetCustomerBillingProfile.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Faturalama profilini almak için aşağıdaki sorgu parametresini kullanın.

| Ad                   | Tür     | Gerekli | Açıklama                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| **customer-tenant-id** | **guid** | Y        | Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt [gövdesinde profil](profile-resources.md) kaynakları koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1206
Content-Type: application/json
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
Date: Mon, 23 Nov 2015 18:13:43 GMT

{
    "id": "<billing-profile-id>",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "CompanyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "firstName": "FirstName",
        "lastName": "LastName",
        "phoneNumber": "4255555555"
    },
    "links": {
        "self": {
            "uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "etag": "<etag>",
        "objectType": "CustomerBillingProfile"
    }
}
```
