---
title: Müşteri oluşturma
description: Bulut Çözümü Sağlayıcısı (CSP) iş ortağının yeni müşteri oluşturmak İş Ortağı Merkezi API'leri nasıl kullanabileceğini öğrenin. Makalede önkoşullar ve başka neler olduğu açıklanmıştır.
ms.date: 03/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6232ca77d057f2f5168b73d81ec551669d540246
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973732"
---
# <a name="create-a-customer-using-partner-center-apis"></a><span data-ttu-id="6237c-104">İş Ortağı Merkezi API'lerini kullanarak müşteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="6237c-104">Create a customer using Partner Center APIs</span></span>

<span data-ttu-id="6237c-105">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6237c-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6237c-106">Bu makalede yeni müşteri oluşturma açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="6237c-106">This article explains how to create a new customer.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6237c-107">Dolaylı sağlayıcıysanız ve dolaylı kurumsal bayi için müşteri oluşturmak istiyorsanız lütfen bkz. Dolaylı kurumsal [bayi için müşteri oluşturma.](create-a-customer-for-an-indirect-reseller.md)</span><span class="sxs-lookup"><span data-stu-id="6237c-107">If you are an indirect provider and you want to create a customer for an indirect reseller, please see [Create a customer for an indirect reseller](create-a-customer-for-an-indirect-reseller.md).</span></span>

<span data-ttu-id="6237c-108">Bulut çözümü sağlayıcısı (CSP) iş ortağı olarak, müşteri oluşturma adımlarını müşteri adına sipariş veebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6237c-108">As a cloud solution provider (CSP) partner, when you create a customer you can place orders on behalf of the customer.</span></span> <span data-ttu-id="6237c-109">Bir müşteri oluşturmanın yanı sıra şunları da oluşturabilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="6237c-109">When you create a customer, you also create:</span></span>

- <span data-ttu-id="6237c-110">Müşteri Azure Active Directory (AD) kiracı nesnesi.</span><span class="sxs-lookup"><span data-stu-id="6237c-110">An Azure Active Directory (AD) tenant object for the customer.</span></span>

- <span data-ttu-id="6237c-111">Temsilci yönetici ayrıcalıkları için kullanılan kurumsal bayi ile müşteri arasındaki ilişki.</span><span class="sxs-lookup"><span data-stu-id="6237c-111">A relationship between the reseller and customer, used for delegated admin privileges.</span></span>

- <span data-ttu-id="6237c-112">Müşteri için yönetici olarak oturum açmanın kullanıcı adı ve parolası.</span><span class="sxs-lookup"><span data-stu-id="6237c-112">A user name and password to sign in as an admin for the customer.</span></span>

<span data-ttu-id="6237c-113">Müşteri oluşturulduktan sonra müşteri kimliğini ve Azure AD ayrıntılarını daha sonra hesap yönetimi İş Ortağı Merkezi SDK'sı kaydetmeyi öğrenin.</span><span class="sxs-lookup"><span data-stu-id="6237c-113">Once the customer is created, be sure to save the customer ID and Azure AD details for future use with the Partner Center SDK (for example, account management).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6237c-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6237c-114">Prerequisites</span></span>

- <span data-ttu-id="6237c-115">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6237c-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6237c-116">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="6237c-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6237c-117">Müşteri kiracısı oluşturmak için oluşturma işlemi sırasında geçerli bir fiziksel adres sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6237c-117">To create a customer tenant you must provide a valid physical address during the creation process.</span></span> <span data-ttu-id="6237c-118">Adres doğrulama senaryosunda açıklanan adımların ardından bir adres [doğrulanabilir.](validate-an-address.md)</span><span class="sxs-lookup"><span data-stu-id="6237c-118">An address can be validated by following the steps outlined in the [Validate an address](validate-an-address.md) scenario.</span></span> <span data-ttu-id="6237c-119">Korumalı alan ortamında geçersiz bir adres kullanarak bir müşteri oluşturmanız, bu müşteri kiracısı silmeniz mümkün olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="6237c-119">If you create a customer using an invalid address in the sandbox environment, you will not be able to delete that customer tenant.</span></span>

## <a name="c"></a><span data-ttu-id="6237c-120">C\#</span><span class="sxs-lookup"><span data-stu-id="6237c-120">C\#</span></span>

<span data-ttu-id="6237c-121">Müşteri eklemek için:</span><span class="sxs-lookup"><span data-stu-id="6237c-121">To add a customer:</span></span>

1. <span data-ttu-id="6237c-122">Yeni bir Customer nesnesi [**örneği**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) oluşturma.</span><span class="sxs-lookup"><span data-stu-id="6237c-122">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object.</span></span> <span data-ttu-id="6237c-123">BillingProfile ve [**CompanyProfile bilgilerini**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) [**doldurmayınız gerekir.**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)</span><span class="sxs-lookup"><span data-stu-id="6237c-123">Be sure to fill in the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span>

2. <span data-ttu-id="6237c-124">Create veya CreateAsync [**çağrılarını kullanarak yeni müşteriyi IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) [**koleksiyonunuza ekleyin.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) [](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create)</span><span class="sxs-lookup"><span data-stu-id="6237c-124">Add the new customer to your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection by calling [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync).</span></span>

### <a name="c-example"></a><span data-ttu-id="6237c-125">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="6237c-125">C\# example</span></span>

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

<span data-ttu-id="6237c-126">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6237c-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6237c-127">**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** CreateCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="6237c-127">**Project**: Partner Center SDK Samples **Class**: CreateCustomer.cs</span></span>

## <a name="java"></a><span data-ttu-id="6237c-128">Java</span><span class="sxs-lookup"><span data-stu-id="6237c-128">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="6237c-129">Yeni müşteri oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="6237c-129">To create a new customer:</span></span>

1. <span data-ttu-id="6237c-130">**CustomerBillingProfile** ve **CustomerCompanyProfile nesnelerinin yeni bir örneğini** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6237c-130">Create a new instance of the **CustomerBillingProfile** and the **CustomerCompanyProfile** objects.</span></span> <span data-ttu-id="6237c-131">Gerekli alanları doldurmak için emin olun.</span><span class="sxs-lookup"><span data-stu-id="6237c-131">Be sure to populate the required fields.</span></span>

2. <span data-ttu-id="6237c-132">**IAggregatePartner.getCustomers().create işlevini çağırarak müşteriyi** oluşturun.</span><span class="sxs-lookup"><span data-stu-id="6237c-132">Create the customer by calling the **IAggregatePartner.getCustomers().create** function.</span></span>

### <a name="java-example"></a><span data-ttu-id="6237c-133">Java örneği</span><span class="sxs-lookup"><span data-stu-id="6237c-133">Java example</span></span>

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

## <a name="powershell"></a><span data-ttu-id="6237c-134">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6237c-134">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="6237c-135">Müşteri oluşturmak için [**New-PartnerCustomer komutunu yürütün.**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md)</span><span class="sxs-lookup"><span data-stu-id="6237c-135">To create a customer, execute the [**New-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/New-PartnerCustomer.md) command.</span></span>

```powershell
New-PartnerCustomer -BillingAddressLine1 '1 Microsoft Way' -BillingAddressCity 'Redmond' -BillingAddressCountry 'US' -BillingAddressPostalCode '98052' -BillingAddressState 'WA' -ContactEmail 'jdoe@customer.com' -ContactFirstName 'Jane' -ContactLastName 'Doe' -Culture 'en-US' -Domain 'newcustomer.onmicrosoft.com' -Language 'en' -Name 'New Customer'
```

## <a name="rest-request"></a><span data-ttu-id="6237c-136">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6237c-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6237c-137">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="6237c-137">Request syntax</span></span>

| <span data-ttu-id="6237c-138">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6237c-138">Method</span></span>   | <span data-ttu-id="6237c-139">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6237c-139">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="6237c-140">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="6237c-140">**POST**</span></span> | <span data-ttu-id="6237c-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6237c-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6237c-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6237c-142">Request headers</span></span>

- <span data-ttu-id="6237c-143">Bu API bir kez etkilidir (birden çok kez çağırsanız farklı bir sonuç ortayalanmaz).</span><span class="sxs-lookup"><span data-stu-id="6237c-143">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>

- <span data-ttu-id="6237c-144">İstek kimliği ve bağıntı kimliği gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6237c-144">A request ID and correlation ID are required.</span></span>

- <span data-ttu-id="6237c-145">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6237c-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6237c-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6237c-146">Request body</span></span>

<span data-ttu-id="6237c-147">Bu tablo, istek gövdesinde gerekli özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="6237c-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="6237c-148">Ad</span><span class="sxs-lookup"><span data-stu-id="6237c-148">Name</span></span>                              | <span data-ttu-id="6237c-149">Tür</span><span class="sxs-lookup"><span data-stu-id="6237c-149">Type</span></span>   | <span data-ttu-id="6237c-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6237c-150">Description</span></span>                                 |
|-----------------------------------|--------|---------------------------------------------|
| [<span data-ttu-id="6237c-151">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="6237c-151">BillingProfile</span></span>](#billing-profile) | <span data-ttu-id="6237c-152">object</span><span class="sxs-lookup"><span data-stu-id="6237c-152">object</span></span> | <span data-ttu-id="6237c-153">Müşterinin faturalama profili bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6237c-153">The customer's billing profile information.</span></span> |
| [<span data-ttu-id="6237c-154">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="6237c-154">CompanyProfile</span></span>](#company-profile) | <span data-ttu-id="6237c-155">object</span><span class="sxs-lookup"><span data-stu-id="6237c-155">object</span></span> | <span data-ttu-id="6237c-156">Müşterinin şirket profili bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6237c-156">The customer's company profile information.</span></span> |

#### <a name="billing-profile"></a><span data-ttu-id="6237c-157">Faturalama profili</span><span class="sxs-lookup"><span data-stu-id="6237c-157">Billing profile</span></span>

<span data-ttu-id="6237c-158">Bu tabloda, yeni müşteri oluşturmak için gereken [CustomerBillingProfile](customer-resources.md#customerbillingprofile) kaynağından gereken en düşük alanlar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="6237c-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="6237c-159">Ad</span><span class="sxs-lookup"><span data-stu-id="6237c-159">Name</span></span>             | <span data-ttu-id="6237c-160">Tür</span><span class="sxs-lookup"><span data-stu-id="6237c-160">Type</span></span>                                     | <span data-ttu-id="6237c-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6237c-161">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6237c-162">e-posta</span><span class="sxs-lookup"><span data-stu-id="6237c-162">email</span></span>            | <span data-ttu-id="6237c-163">string</span><span class="sxs-lookup"><span data-stu-id="6237c-163">string</span></span>                                   | <span data-ttu-id="6237c-164">Müşterinin e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="6237c-164">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="6237c-165">kültür</span><span class="sxs-lookup"><span data-stu-id="6237c-165">culture</span></span>          | <span data-ttu-id="6237c-166">string</span><span class="sxs-lookup"><span data-stu-id="6237c-166">string</span></span>                                   | <span data-ttu-id="6237c-167">İletişim ve para birimi için tercih edilen kültür (örneğin, "en-US").</span><span class="sxs-lookup"><span data-stu-id="6237c-167">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="6237c-168">Desteklenen [İş Ortağı Merkezi dil ve yerel dillerle](partner-center-supported-languages-and-locales.md) ilgili daha fazla şey öğrenmek için bkz.</span><span class="sxs-lookup"><span data-stu-id="6237c-168">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="6237c-169">language</span><span class="sxs-lookup"><span data-stu-id="6237c-169">language</span></span>         | <span data-ttu-id="6237c-170">string</span><span class="sxs-lookup"><span data-stu-id="6237c-170">string</span></span>                                   | <span data-ttu-id="6237c-171">Varsayılan dil.</span><span class="sxs-lookup"><span data-stu-id="6237c-171">The default language.</span></span> <span data-ttu-id="6237c-172">İki karakterli dil kodu (örneğin `en` veya `fr` ) de destekler.</span><span class="sxs-lookup"><span data-stu-id="6237c-172">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="6237c-173">şirket \_ adı</span><span class="sxs-lookup"><span data-stu-id="6237c-173">company\_name</span></span>    | <span data-ttu-id="6237c-174">string</span><span class="sxs-lookup"><span data-stu-id="6237c-174">string</span></span>                                   | <span data-ttu-id="6237c-175">Kayıtlı şirket/kuruluş adı.</span><span class="sxs-lookup"><span data-stu-id="6237c-175">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="6237c-176">varsayılan \_ adres</span><span class="sxs-lookup"><span data-stu-id="6237c-176">default\_address</span></span> | [<span data-ttu-id="6237c-177">Adres</span><span class="sxs-lookup"><span data-stu-id="6237c-177">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="6237c-178">Müşterinin şirketinin/kuruluşun kayıtlı adresi.</span><span class="sxs-lookup"><span data-stu-id="6237c-178">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="6237c-179">Uzunluk sınırlamaları [hakkında](utility-resources.md#address) bilgi için adres kaynağına bakın.</span><span class="sxs-lookup"><span data-stu-id="6237c-179">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="6237c-180">Şirket profili</span><span class="sxs-lookup"><span data-stu-id="6237c-180">Company profile</span></span>

<span data-ttu-id="6237c-181">Bu tabloda, yeni müşteri oluşturmak için gereken [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) kaynağından gereken minimum alanlar açıklanır.</span><span class="sxs-lookup"><span data-stu-id="6237c-181">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="6237c-182">Ad</span><span class="sxs-lookup"><span data-stu-id="6237c-182">Name</span></span>   | <span data-ttu-id="6237c-183">Tür</span><span class="sxs-lookup"><span data-stu-id="6237c-183">Type</span></span>   | <span data-ttu-id="6237c-184">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6237c-184">Description</span></span>                                                  |
|--------|--------|--------------------------------------------------------------|
| <span data-ttu-id="6237c-185">etki alanı</span><span class="sxs-lookup"><span data-stu-id="6237c-185">domain</span></span> | <span data-ttu-id="6237c-186">string</span><span class="sxs-lookup"><span data-stu-id="6237c-186">string</span></span> | <span data-ttu-id="6237c-187">Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="6237c-187">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
|<span data-ttu-id="6237c-188">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="6237c-188">organizationRegistrationNumber</span></span>|<span data-ttu-id="6237c-189">Dize</span><span class="sxs-lookup"><span data-stu-id="6237c-189">String</span></span>|<span data-ttu-id="6237c-190">Müşterinin kuruluş kayıt numarası (belirli ülkelerde INN numarası olarak da adlandırılır).</span><span class="sxs-lookup"><span data-stu-id="6237c-190">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="6237c-191">Müşterinin yalnızca şu ülkelerde bulunan şirketi/kuruluşu için gereklidir: Dalı(AM), Brezilya(AZ), Zaman(BY),İşle(HU), GZ), Kyrgyzstan(KG), Arjantin(MD), Rusya(RU), Tajikistan(TJ), Özbekistan(UZ), Arjantin(UA), Brezilya(BR), Hindistan, Güney Afrika, Afrika, Birleşik Krallık, Suudi Arabistan, Suudi Arabistan, Suudi Arabistan, Vietnam, Myanmar, Hindistan, Güney Sudan ve Sudan.</span><span class="sxs-lookup"><span data-stu-id="6237c-191">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), Brazil(BR), India, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="6237c-192">Müşterinin başka ülkelerde bulunan şirketi/kuruluşu için bu isteğe bağlı bir alandır.</span><span class="sxs-lookup"><span data-stu-id="6237c-192">For customer’s company/organization located in other countries, this is an optional field.</span></span>|

### <a name="request-example"></a><span data-ttu-id="6237c-193">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6237c-193">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6237c-194">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6237c-194">REST response</span></span>

<span data-ttu-id="6237c-195">Başarılı olursa, bu API yeni [müşteri için](customer-resources.md#customer) bir Müşteri kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="6237c-195">If successful, this API returns a [Customer](customer-resources.md#customer) resource for the new customer.</span></span> <span data-ttu-id="6237c-196">Müşteri kimliğini ve Azure AD ayrıntılarını daha sonra kullanmak üzere İş Ortağı Merkezi SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="6237c-196">Save the customer ID and Azure AD details for future use with the Partner Center SDK.</span></span> <span data-ttu-id="6237c-197">Örneğin, hesap yönetimiyle kullanmak için bu hesaplara ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="6237c-197">You will need them for use with account management, for example.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6237c-198">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6237c-198">Response success and error codes</span></span>

<span data-ttu-id="6237c-199">Yanıtlar, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="6237c-199">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6237c-200">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6237c-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6237c-201">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6237c-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6237c-202">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6237c-202">Response example</span></span>

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
