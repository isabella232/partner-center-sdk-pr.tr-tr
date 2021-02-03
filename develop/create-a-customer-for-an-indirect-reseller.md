---
title: Dolaylı satıcı için müşteri oluşturma
description: Dolaylı bir sağlayıcının dolaylı bir satıcı için müşteri oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanabileceği hakkında bilgi edinin.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e2386f1963a5bb3ea4269bcbf4327c75987f3b91
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770178"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>Iş Ortağı Merkezi API 'Lerini kullanarak dolaylı satıcı için müşteri oluşturma

**Uygulama hedefi:**

- İş Ortağı Merkezi

Dolaylı bir sağlayıcı, dolaylı bir satıcı için müşteri oluşturabilir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Dolaylı Bayi kiracı tanımlayıcısı.

- Dolaylı satıcının dolaylı sağlayıcıyla bir ortaklığı olması gerekir.

## <a name="c"></a>C\#

Dolaylı bir satıcı için yeni bir müşteri eklemek için:

1. Yeni bir [**Müşteri**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) nesnesi örneği oluşturun ve ardından [**Billingprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) ve [**companyprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)öğesini oluşturup doldurun. Dolaylı satıcı KIMLIĞINI [**ilişkili Iş ortağı kimliği**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) özelliğine atadığınızdan emin olun.

2. Müşteri koleksiyonu işlemlerine bir arabirim almak için [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) özelliğini kullanın.

3. Müşteriyi oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metodunu çağırın.

### <a name="c-example"></a>C \# örneği

``` csharp
// IAggregatePartner partnerOperations;
// var indirectResellerId;
var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "WingtipToys{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix)
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "Gena@wingtiptoys.com",
        Language = "En",
        CompanyName = "Wingtip Toys" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Gena",
            LastName = "Soto",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = "4255550101"
        }
    },
    AssociatedPartnerId = indirectResellerId
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                       |
|----------|-------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.

| Ad                                          | Tür   | Gerekli | Açıklama                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | object | Yes      | Müşterinin Faturalandırma profili bilgileri.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | object | Yes      | Müşterinin şirket profili bilgileri.                                                               
| [Ilişkili iş ortağı kimliği](customer-resources.md#customer) | string | Yes      | Dolaylı satıcı KIMLIĞI. Burada sağlanan KIMLIğIN gösterdiği dolaylı satıcının dolaylı sağlayıcıyla bir ortaklığı olmalıdır veya istek başarısız olur. Ayrıca, Ilişkili iş ortağı kimliği değeri sağlanmazsa, müşterinin dolaylı satıcı yerine dolaylı sağlayıcının doğrudan müşterisi olarak oluşturulduğunu unutmayın. |
|Etki alanı| Dize| Yes|Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    string|Yes|     Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır). Yalnızca aşağıdaki ülkelerde bulunan müşterinin şirketi/kuruluşu için gereklidir. Ermenistan (Har), Azerbaycan (AZ), Belarus (BY), Macaristan (HU), Kazakistan (KZ), Kırgızistan (KG), Moldova (MD), Rusya (RU), Tacikistan (TJ), Özbekistan (UZ), Ukrayna (UA). Müşterinin veya diğer ülkelerde bulunan şirket/kuruluş için bu belirtilmemelidir.|



#### <a name="billing-profile"></a>Faturalama profili

Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customerbillingprofile](customer-resources.md#customerbillingprofile) kaynağından gereken en düşük alan açıklanmaktadır.

| Ad             | Tür                                     | Gerekli | Açıklama                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-posta            | string                                   | Yes      | Müşterinin e-posta adresi.                                                                                                                                                                                   |
| kültür          | string                                   | Yes      | İletişim ve para birimi için tercih edilen kültür, "en-US" gibi. Desteklenen kültürler için [Iş Ortağı Merkezi tarafından desteklenen dillere ve yerel ayarlara](partner-center-supported-languages-and-locales.md) bakın. |
| language         | string                                   | Yes      | Varsayılan dil. İki karakter dil kodu (örneğin `en` veya `fr` ) desteklenir.                                                                                                                                |
| Şirket \_ adı    | string                                   | Yes      | Kayıtlı şirket/kuruluş adı.                                                                                                                                                                       |
| Varsayılan \_ Adres | [Adres](utility-resources.md#address) | Yes      | Müşterinin şirketinin/kuruluşunun kayıtlı adresi. Herhangi bir uzunluk sınırlaması hakkında bilgi için bkz. [Adres](utility-resources.md#address) kaynağı.                                             |

#### <a name="company-profile"></a>Şirket profili

Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customercompanyprofile](customer-resources.md#customercompanyprofile) kaynağından gereken en düşük alan açıklanmaktadır.

| Ad   | Tür   | Gerekli | Açıklama                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| etki alanı | string | Yes     | Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com. |
| organizationRegistrationNumber | string | Koşula bağlıdır | Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır). <br/><br/>Bu alanın tamamlanması yalnızca bir müşterinin şirketi/kuruluşu aşağıdaki ülkelerde bulunuyorsa gereklidir: <br/><br/>-Ermenistan (Har) <br/>-Azerbaycan (AZ)<br/>-Belarus (BY)<br/>-Macaristan (HU)<br/>-Kazakistan (KZ)<br/>-Kırgızistan (KG)<br/>-Moldova (MD)<br/>-Rusya (RU)<br/>-Tacikistan (TJ)<br/>-Özbekistan (UZ)<br/>-Ukrayna (UA)<br/><br/>Müşterinin şirketi/kuruluşu burada gösterilenlerin ötesinde diğer ülkelerde bulunuyorsa bu alan gerekli değildir.  |

### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 823
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": null,
    "CommerceId": null,
    "CompanyProfile": {
        "TenantId": null,
        "Domain": "WingtipToys678152504.onmicrosoft.com",
        "CompanyName": null,
        "Attributes": {
            "ObjectType": "CustomerCompanyProfile"
        }
    },
    "BillingProfile": {
        "Id": null,
        "FirstName": null,
        "LastName": null,
        "Email": "Gena@wingtiptoys.com",
        "Culture": "EN-US",
        "Language": "En",
        "CompanyName": "Wingtip Toys678152504",
        "DefaultAddress": {
            "Country": "US",
            "Region": null,
            "City": "Redmond",
            "State": "WA",
            "AddressLine1": "One Microsoft Way",
            "AddressLine2": null,
            "PostalCode": "98052",
            "FirstName": "Gena",
            "LastName": "Soto",
            "PhoneNumber": "4255550101"
        },
        "Attributes": {
            "ObjectType": "CustomerBillingProfile"
        }
    },
    "RelationshipToPartner": "none",
    "AllowDelegatedAccess": null,
    "UserCredentials": null,
    "CustomDomains": null,
    "AssociatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "Attributes": {
        "ObjectType": "Customer"
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt yeni müşteri için bir [Müşteri](customer-resources.md#customer) kaynağı içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Yanıtlar, başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 1085
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0dd197a8-992c-44ca-aeae-21cd83494dce
MS-RequestId: d628adbe-b7ee-412e-ac55-58f22b4ba2f4
MS-CV: Yy/YaA0gYEmfQyR/.0
MS-ServerId: 030020525
Date: Tue, 06 Jun 2017 23:11:40 GMT

{
    "id": "626099fe-17af-4756-9fd0-6a73b7127859",
    "commerceId": "626099fe-17af-4756-9fd0-6a73b7127859",
    "companyProfile": {
        "tenantId": "626099fe-17af-4756-9fd0-6a73b7127859",
        "domain": "WingtipToys678152504.onmicrosoft.com",
        "companyName": "Wingtip Toys678152504",
        "links": {
            "self": {
                "uri": "/customers/626099fe-17af-4756-9fd0-6a73b7127859/profiles/company",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "7079246e-7b62-56ef-7cbd-a819514b54b5",
        "email": "Gena@wingtiptoys.com",
        "culture": "en-US",
        "language": "En",
        "companyName": "Wingtip Toys678152504",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Gena",
            "lastName": "Soto",
            "phoneNumber": "4255550101"
        },
        "attributes": {
            "etag": "-8799889149591823008",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "reseller",
    "allowDelegatedAccess": true,
    "userCredentials": {
        "userName": "admin",
        "password": "0Krha*Io"
    },
    "associatedPartnerId": "484e548c-f5f3-4528-93a9-c16c6373cb59",
    "attributes": {
        "objectType": "Customer"
    }
}
```