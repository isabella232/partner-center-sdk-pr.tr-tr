---
title: Müşteri oluşturma
description: Bulut Çözümü Sağlayıcısı (CSP) iş ortağının yeni müşteri oluşturmak İş Ortağı Merkezi API'leri nasıl kullanabileceğini öğrenin. Makalede önkoşullar ve başka neler olduğu açıklanmıştır.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 49df47441276c7e79074e1bf7f8d50cd72054b42acd93938de088046b68b6d98
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991778"
---
# <a name="create-a-customer-using-partner-center-apis"></a>İş Ortağı Merkezi API'lerini kullanarak müşteri oluşturma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu makalede yeni müşteri oluşturma açıklanmıştır.

> [!IMPORTANT]
> Dolaylı sağlayıcıysanız ve dolaylı kurumsal bayi için müşteri oluşturmak istiyorsanız lütfen bkz. Dolaylı kurumsal [bayi için müşteri oluşturma.](create-a-customer-for-an-indirect-reseller.md)

Bulut çözümü sağlayıcısı (CSP) iş ortağı olarak, müşteri oluşturma adımlarını müşteri adına sipariş veebilirsiniz. Bir müşteri oluşturmanın yanı sıra şunları da oluşturabilirsiniz:

- Müşteri Azure Active Directory (AD) kiracı nesnesi.

- Temsilci yönetici ayrıcalıkları için kullanılan kurumsal bayi ile müşteri arasındaki ilişki.

- Müşteri için yönetici olarak oturum açmanın kullanıcı adı ve parolası.

Müşteri oluşturulduktan sonra müşteri kimliğini ve Azure AD ayrıntılarını daha sonra hesap yönetimi İş Ortağı Merkezi SDK'sı kaydetmeyi öğrenin.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

> [!IMPORTANT]
> Müşteri kiracısı oluşturmak için oluşturma işlemi sırasında geçerli bir fiziksel adres sağlayabilirsiniz. Adres doğrulama senaryosunda açıklanan adımların ardından bir adres [doğrulanabilir.](validate-an-address.md) Korumalı alan ortamında geçersiz bir adres kullanarak bir müşteri oluşturmanız, bu müşteri kiracısı silmeniz mümkün olmayacaktır.

## <a name="c"></a>C\#

Müşteri eklemek için:

1. Yeni bir Customer nesnesi [**örneği**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) oluşturma. BillingProfile ve [**CompanyProfile bilgilerini**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) [**doldurmayınız gerekir.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)

2. Create veya CreateAsync [**çağrılarını kullanarak yeni müşteriyi IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) [**koleksiyonunuza ekleyin.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) [](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create)

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

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** CreateCustomer.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Yeni müşteri oluşturmak için:

1. **CustomerBillingProfile** ve **CustomerCompanyProfile nesnelerinin yeni bir örneğini** oluşturun. Gerekli alanları doldurmak için emin olun.

2. **IAggregatePartner.getCustomers().create işlevini çağırarak müşteriyi** oluşturun.

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

Müşteri oluşturmak için [**New-PartnerCustomer komutunu yürütün.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                       |
|----------|-------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

- Bu API bir kez etkilidir (birden çok kez çağırsanız farklı bir sonuç ortayalanmaz).

- İstek kimliği ve bağıntı kimliği gereklidir.

- Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde gerekli özellikleri açıklar.

| Ad                              | Tür   | Description                                 |
|-----------------------------------|--------|---------------------------------------------|
| [BillingProfile](#billing-profile) | object | Müşterinin faturalama profili bilgileri. |
| [CompanyProfile](#company-profile) | object | Müşterinin şirket profili bilgileri. |

#### <a name="billing-profile"></a>Faturalama profili

Bu tabloda, yeni müşteri oluşturmak için gereken [CustomerBillingProfile](customer-resources.md#customerbillingprofile) kaynağından gereken en düşük alanlar açıklanır.

| Ad             | Tür                                     | Description                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| e-posta            | string                                   | Müşterinin e-posta adresi.                                                                                                                                                                                   |
| kültür          | string                                   | İletişim ve para birimi için tercih edilen kültür (örneğin, "en-US"). Desteklenen [İş Ortağı Merkezi dil ve yerel dillerle](partner-center-supported-languages-and-locales.md) ilgili daha fazla şey öğrenmek için bkz. |
| language         | string                                   | Varsayılan dil. İki karakterli dil kodu (örneğin `en` veya `fr` ) de destekler.                                                                                                                                |
| şirket \_ adı    | string                                   | Kayıtlı şirket/kuruluş adı.                                                                                                                                                                       |
| varsayılan \_ adres | [Adres](utility-resources.md#address) | Müşterinin şirketinin/kuruluşun kayıtlı adresi. Uzunluk sınırlamaları [hakkında](utility-resources.md#address) bilgi için adres kaynağına bakın.                                             |

#### <a name="company-profile"></a>Şirket profili

Bu tabloda, yeni müşteri oluşturmak için gereken [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) kaynağından gereken minimum alanlar açıklanır.

| Ad   | Tür   | Description                                                  |
|--------|--------|--------------------------------------------------------------|
| etki alanı | string | Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com. |
|organizationRegistrationNumber|Dize|Müşterinin kuruluş kayıt numarası (belirli ülkelerde INN numarası olarak da adlandırılır). Müşterinin yalnızca şu ülkelerde bulunan şirketi/kuruluşu için gereklidir: Dalı(AM), Brezilya(AZ), Zaman(BY),İşle(HU), GZ), Kyrgyzstan(KG), Arjantin(MD), Rusya(RU), Tajikistan(TJ), Özbekistan(UZ), Arjantin(UA), Brezilya(BR), Hindistan, Güney Afrika, Afrika, Birleşik Krallık, Suudi Arabistan, Suudi Arabistan, Suudi Arabistan, Vietnam, Myanmar, Hindistan, Güney Sudan ve Sudan. Müşterinin başka ülkelerde bulunan şirketi/kuruluşu için bu isteğe bağlı bir alandır.|

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

Başarılı olursa, bu API yeni [müşteri için](customer-resources.md#customer) bir Müşteri kaynağı döndürür. Müşteri kimliğini ve Azure AD ayrıntılarını daha sonra kullanmak üzere İş Ortağı Merkezi SDK'sı. Örneğin, hesap yönetimiyle kullanmak için bu hesaplara ihtiyacınız olacak.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Yanıtlar, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
