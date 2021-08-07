---
title: Dolaylı satıcı için müşteri oluşturma
description: Dolaylı sağlayıcının dolaylı kurumsal bayi için İş Ortağı Merkezi api'leri nasıl kullanabileceğini öğrenin.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e54e083dda758cc712c889916676007a389ba69c8009bb3d4907df343a436004
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991744"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a>İş Ortağı Merkezi API'lerini kullanarak dolaylı kurumsal bayi için müşteri oluşturma

Dolaylı sağlayıcı, dolaylı kurumsal bayi için müşteri oluşturabilir.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Dolaylı kurumsal bayinin kiracı tanımlayıcısı.

- Dolaylı kurumsal bayinin dolaylı sağlayıcıyla bir ortaklığı olması gerekir.

## <a name="c"></a>C\#

Dolaylı kurumsal bayiye yeni müşteri eklemek için:

1. Yeni bir Customer nesnesi [**örneği**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) oluşturma ve ardından [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) ve [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)örneğini oluşturma ve doldurmak. Dolaylı kurumsal bayi kimliğini [**AssociatedPartnerID özelliğine atadığınızdan emin**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) olun.

2. Müşteri toplama [**işlemlerine arabirim almak için IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) özelliğini kullanın.

3. Müşteriyi [**oluşturmak**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) için [**Create veya CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) yöntemini çağırma.

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

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı **Örnekler Sınıfı:** CreateCustomerforIndirectReseller.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                       |
|----------|-------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde gerekli özellikleri açıklar.

| Ad                                          | Tür   | Gerekli | Açıklama                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [BillingProfile](#billing-profile)             | object | Yes      | Müşterinin faturalama profili bilgileri.                                                                                                                                                                                                                                                                                                           |
| [CompanyProfile](#company-profile)             | object | Yes      | Müşterinin şirket profili bilgileri.                                                               
| [AssociatedPartnerId](customer-resources.md#customer) | string | Yes      | Dolaylı kurumsal bayi kimliği. Burada verilen kimlikle belirtilen dolaylı kurumsal bayinin dolaylı sağlayıcıyla bir ortaklığı olması gerekir, yoksa istek başarısız olur. Ayrıca AssociatedPartnerId değeri sağlanmadıktan sonra müşterinin dolaylı kurumsal bayi yerine dolaylı sağlayıcının doğrudan müşterisi olarak oluşturulacaklarını da unutmayın. |
|Etki alanı| Dize| Yes|Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com.|
|organizationRegistrationNumber|    string|Yes|     Müşterinin kuruluş kayıt numarası (belirli ülkelerde INN numarası olarak da adlandırılır). Müşterinin yalnızca şu ülkelerde bulunan şirketi/kuruluşu için gereklidir: Arjantin(AM), Arjantin(AZ), Sonra(BY), Yerşek(HU), GZ), Kyrgyzstan(KG), Arjantin(MD), Rusya(RU), Tajikistan(TJ), Özbekistan(UZ), Yer (UA), Hindistan, Brezilya, Güney Afrika, Afrika Birleşik Devletleri, Birleşik Devletler, Suudi Arabistan, Suudi Arabistan, Hindistan, Vietnam, Myanmar, Hindistan, Güney Sudan ve Brezilya. Müşterinin başka ülkelerde bulunan şirketi/kuruluşu için bu isteğe bağlı bir alandır.|



#### <a name="billing-profile"></a>Faturalama profili

Bu tabloda, yeni müşteri oluşturmak için gereken [CustomerBillingProfile](customer-resources.md#customerbillingprofile) kaynağından gereken en düşük alanlar açıklanır.

| Ad             | Tür                                     | Gerekli | Açıklama                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-posta            | string                                   | Yes      | Müşterinin e-posta adresi.                                                                                                                                                                                   |
| kültür          | string                                   | Yes      | İletişim ve para birimi için tercih edilen kültür (örneğin, "en-US"). Desteklenen [İş Ortağı Merkezi dil ve yerel dillerle](partner-center-supported-languages-and-locales.md) ilgili daha fazla şey öğrenmek için bkz. |
| language         | string                                   | Yes      | Varsayılan dil. İki karakterli dil kodu (örneğin `en` veya `fr` ) de destekler.                                                                                                                                |
| şirket \_ adı    | string                                   | Yes      | Kayıtlı şirket/kuruluş adı.                                                                                                                                                                       |
| varsayılan \_ adres | [Adres](utility-resources.md#address) | Yes      | Müşterinin şirketinin/kuruluşun kayıtlı adresi. Uzunluk sınırlamaları [hakkında](utility-resources.md#address) bilgi için adres kaynağına bakın.                                             |

#### <a name="company-profile"></a>Şirket profili

Bu tabloda, yeni müşteri oluşturmak için gereken [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) kaynağından gereken minimum alanlar açıklanır.

| Ad   | Tür   | Gerekli | Açıklama                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| etki alanı | string | Yes     | Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com. |
| organizationRegistrationNumber | string | Koşula bağlıdır | Müşterinin kuruluş kayıt numarası (belirli ülkelerdeki INN numarası olarak da adlandırılır). <br/><br/>Bu alanın tamamlanması yalnızca müşterinin şirketi/kuruluşu aşağıdaki ülkelerde bulunuyorsa gereklidir: <br/><br/>- Arjantin (AM) <br/>- Rusya (AZ)<br/>- Tümce (BY)<br/>- Devam etti (HU)<br/>- Enstantane (KZ)<br/>- Kyrgyzstan (KG)<br/>- Zaman (MD)<br/>- Rusya (RU)<br/>- Tajikistan (TJ)<br/>- Özbekistan (UZ)<br/>- Rusya (UA)<br/>- Hindistan <br/>- Brezilya <br/>- Güney Afrika <br/>- Yer <br/>- Birleşik Arab Liği <br/>- Suudi Arabistan <br/>- Türkiye <br/>- Suudi <br/>- Vietnam <br/>- Myanmar <br/>- Devam ediyor <br/>- Güney Sudan <br/>- Rusya<br/> <br/>Müşterinin başka ülkelerde bulunan şirketi/kuruluşu için bu isteğe bağlı bir alandır.  |

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

Başarılı olursa yanıt, yeni müşteri [için](customer-resources.md#customer) bir Müşteri kaynağı içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Yanıtlar, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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