---
title: Müşteri oluşturma
description: Bir bulut çözümü sağlayıcısı (CSP) ortağının yeni bir müşteri oluşturmak için Iş Ortağı Merkezi API 'Lerini nasıl kullanabileceği hakkında bilgi edinin. Makalede önkoşulları ve başka neler olduğu açıklanmaktadır.
ms.date: 11/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 3bc8081c682bdf522bcb0ca218f16cafab7b3a99
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770229"
---
# <a name="create-a-customer-using-partner-center-apis"></a>Iş Ortağı Merkezi API 'Leri kullanarak bir müşteri oluşturma

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, yeni bir müşterinin nasıl oluşturulacağı açıklanmaktadır.

> [!IMPORTANT]
> Dolaylı bir Sağlayıcıysanız ve dolaylı bir satıcı için bir müşteri oluşturmak istiyorsanız, lütfen [dolaylı bir satıcı için müşteri oluşturma](create-a-customer-for-an-indirect-reseller.md)konusuna bakın.

Bir bulut çözümü sağlayıcısı (CSP) iş ortağı olarak, bir müşteri oluşturduğunuzda müşteri adına sipariş yerleştirebilirsiniz. Bir müşteri oluşturduğunuzda şunları da oluşturursunuz:

- Müşteri için bir Azure Active Directory (AD) kiracı nesnesi.

- Temsil edilen yönetici ayrıcalıkları için kullanılan satıcı ve müşteri arasındaki ilişki.

- Müşteri için yönetici olarak oturum açmak için Kullanıcı adı ve parola.

Müşteri oluşturulduktan sonra, Iş Ortağı Merkezi SDK ile daha sonra kullanılmak üzere müşteri KIMLIĞI ve Azure AD ayrıntılarını kaydettiğinizden emin olun (örneğin, hesap yönetimi).

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

> [!IMPORTANT]
> Bir müşteri kiracısı oluşturmak için oluşturma işlemi sırasında geçerli bir fiziksel adres sağlamanız gerekir. Adres [doğrulama](validate-an-address.md) senaryosunda özetlenen adımları izleyerek bir adres doğrulanabilir. Korumalı alan ortamında geçersiz bir adres kullanarak bir müşteri oluşturursanız, bu müşteri kiracısını silemezsiniz.

## <a name="c"></a>C\#

Müşteri eklemek için:

1. Yeni bir [**Müşteri**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) nesnesi örneği oluşturun. [**Billingprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) ve [**companyprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)' i doldurduğunuzdan emin olun.

2. [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync)çağırarak, yeni müşteriyi [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonuna ekleyin.

### <a name="c-example"></a>C \# örneği

```csharp
// IAggregatePartner partnerOperations;

var partnerOperations = this.Context.UserPartnerOperations;

var customerToCreate = new Customer()
{
    CompanyProfile = new CustomerCompanyProfile()
    {
        Domain = string.Format(CultureInfo.InvariantCulture,
            "SampleApplication{0}.{1}",
            new Random().Next(),
            this.Context.Configuration.Scenario.CustomerDomainSuffix),
        //// OrganizationRegistrationNumber = "123456" // Please add if in specific country that requires
    },
    BillingProfile = new CustomerBillingProfile()
    {
        Culture = "EN-US",
        Email = "someone@example.com",
        Language = "En",
        CompanyName = "Some Company" + new Random().Next(),
        DefaultAddress = new Address()
        {
            FirstName = "Tania",
            MiddleName = "MiddleName",
            LastName = "Carr",
            AddressLine1 = "One Microsoft Way",
            City = "Redmond",
            State = "WA",
            Country = "US",
            PostalCode = "98052",
            PhoneNumber = ""
        }
    }
};

var newCustomer = partnerOperations.Customers.Create(customerToCreate);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Yeni bir müşteri oluşturmak için:

1. **Customerbillingprofile** ve **customercompanyprofile** nesnelerinin yeni bir örneğini oluşturun. Gerekli alanları doldurduğunuzdan emin olun.

2. **Iaggregatepartner. getCustomers (). Create** işlevini çağırarak müşteriyi oluşturun.

### <a name="java-example"></a>Java örneği

```java
// IAggregatePartner partnerOperations;

Address address = new Address();

address.setFirstName( "Gena" );
address.setLastName( "Soto" );
address.setAddressLine1( "One Microsoft Way" );
address.setCity( "Redmond" );
address.setState( "WA" );
address.setCountry( "US" );
address.setPostalCode( "98052" );
address.setPhoneNumber( "4255550101" );

CustomerBillingProfile billingProfile = new CustomerBillingProfile();

billingProfile.setCulture( "en-US" );
billingProfile.setEmail( "gena@wingtiptoys.com" );
billingProfile.setLanguage( "en" );
billingProfile.setCompanyName( "Wingtip Toys" + new Random().nextInt() );
billingProfile.setDefaultAddress( address );

CustomerCompanyProfile companyProfile = new CustomerCompanyProfile();

companyProfile.setDomain( "WingtipToys" + Math.abs( new Random().nextInt() ) + ".onmicrosoft.com" );

Customer customerToCreate = new Customer();

customerToCreate.setBillingProfile( billingProfile );
customerToCreate.setCompanyProfile( companyProfile );

Customer newCustomer = partnerOperations.getCustomers().create( customerToCreate );
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Bir müşteri oluşturmak için [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) komutunu yürütün.

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                       |
|----------|-------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

- Bu API, ıdempotent (birden çok kez çağırırsanız farklı bir sonuç vermez).

- İstek KIMLIĞI ve bağıntı KIMLIĞI gereklidir.

- Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.

| Ad                              | Tür   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | Müşterinin Faturalandırma profili bilgileri. |
| [CompanyProfile](#company-profile) | object | Müşterinin şirket profili bilgileri. |

#### <a name="billing-profile"></a>Faturalama profili

Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customerbillingprofile](customer-resources.md#customerbillingprofile) kaynağından gereken en düşük alan açıklanmaktadır.

| Ad             | Tür                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-posta            | string                                   | Müşterinin e-posta adresi.                                                                                                                                                                                   |
| kültür          | string                                   | İletişim ve para birimi için tercih edilen kültür, "en-US" gibi. Desteklenen kültürler için [Iş Ortağı Merkezi tarafından desteklenen dillere ve yerel ayarlara](partner-center-supported-languages-and-locales.md) bakın. |
| language         | string                                   | Varsayılan dil. İki karakter dil kodu (örneğin `en` veya `fr` ) desteklenir.                                                                                                                                |
| Şirket \_ adı    | string                                   | Kayıtlı şirket/kuruluş adı.                                                                                                                                                                       |
| Varsayılan \_ Adres | [Adres](utility-resources.md#address) | Müşterinin şirketinin/kuruluşunun kayıtlı adresi. Herhangi bir uzunluk sınırlaması hakkında bilgi için bkz. [Adres](utility-resources.md#address) kaynağı.                                             |

#### <a name="company-profile"></a>Şirket profili

Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customercompanyprofile](customer-resources.md#customercompanyprofile) kaynağından gereken en düşük alan açıklanmaktadır.

| Ad   | Tür   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| etki alanı | string | Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Dize|Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır). Yalnızca aşağıdaki ülkelerde bulunan müşterinin şirketi/kuruluşu için gereklidir. Ermenistan (Har), Azerbaycan (AZ), Belarus (BY), Macaristan (HU), Kazakistan (KZ), Kırgızistan (KG), Moldova (MD), Rusya (RU), Tacikistan (TJ), Özbekistan (UZ), Ukrayna (UA). Müşterinin veya diğer ülkelerde bulunan şirket/kuruluş için bu belirtilmemelidir.|


### <a name="request-example"></a>İstek örneği

```http
POST https://api.partnercenter.microsoft.com/v1/customers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 789
Expect: 100-continue
Connection: Keep-Alive

{
    "CompanyProfile": {
        "Domain": "xyz.ccsctp.net",
    },
    "BillingProfile": {
        "Culture": "EN-US",
        "Email": "test@outlook.com",
        "Language": "en",
        "CompanyName": "test company",
        "DefaultAddress": {
            "FirstName": "Test",
            "LastName": "Test",
            "AddressLine1": "One Microsoft Way",
            "City": "Redmond",
            "State": "WA",
            "PostalCode": "98052",
            "Country": "US",
        }
    }
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu API yeni müşteri için bir [Müşteri](customer-resources.md#customer) kaynağı döndürür. Müşteri KIMLIĞI ve Azure AD ayrıntılarını Iş Ortağı Merkezi SDK ile ileride kullanılmak üzere kaydedin. Örneğin, hesap yönetimiyle kullanım için bu kişilere ihtiyaç duyarsınız.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Yanıtlar, başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 834
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CV: ObwhuhD2tUKJoM+Z.0
MS-ServerId: 202010223
Date: Tue, 14 Feb 2017 20:06:02 GMT

{
    "id": "dfd8cc0a-c592-468c-8461-869a38d24738",
    "commerceId": "0a4ce58a-6f96-4273-8035-d9c7d31b9ba4",
    "companyProfile": {
        "tenantId": "dfd8cc0a-c592-468c-8461-869a38d24738",
        "domain": "xyz.ccsctp.net",
        "attributes": {
            "objectType": "CustomerCompanyProfile"
        }
    },
    "billingProfile": {
        "id": "d17c0275-da92-5c33-9032-782ef1d0b69b",
        "email": "test@outlook.com",
        "culture": "en-US",
        "language": "en",
        "companyName": "test company",
        "defaultAddress": {
            "country": "US",
            "city": "Redmond",
            "state": "WA",
            "addressLine1": "One Microsoft Way",
            "postalCode": "98052",
            "firstName": "Test",
            "lastName": "Test",
            "phoneNumber": ""
        },
        "attributes": {
            "etag": "5920358838484612121",
            "objectType": "CustomerBillingProfile"
        }
    },
    "relationshipToPartner": "none",
    "userCredentials": {
        "userName": "admin",
        "password": "=;;n.=s9Z"
    },
    "attributes": {
        "objectType": "Customer"
    }
}
```
