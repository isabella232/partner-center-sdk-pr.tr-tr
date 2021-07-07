---
title: Dolaylı satıcı için müşteri oluşturma
description: Dolaylı bir sağlayıcının dolaylı bir satıcı için müşteri oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanabileceği hakkında bilgi edinin.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9a6218aeb61f3775c89d34b4d57a17741e3a1e93
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973749"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="f0e8b-103">Iş Ortağı Merkezi API 'Lerini kullanarak dolaylı satıcı için müşteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="f0e8b-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="f0e8b-104">Dolaylı bir sağlayıcı, dolaylı bir satıcı için müşteri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-104">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f0e8b-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f0e8b-105">Prerequisites</span></span>

- <span data-ttu-id="f0e8b-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f0e8b-107">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f0e8b-108">Dolaylı Bayi kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-108">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="f0e8b-109">Dolaylı satıcının dolaylı sağlayıcıyla bir ortaklığı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-109">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="f0e8b-110">C\#</span><span class="sxs-lookup"><span data-stu-id="f0e8b-110">C\#</span></span>

<span data-ttu-id="f0e8b-111">Dolaylı bir satıcı için yeni bir müşteri eklemek için:</span><span class="sxs-lookup"><span data-stu-id="f0e8b-111">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="f0e8b-112">Yeni bir [**Müşteri**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) nesnesi örneği oluşturun ve ardından [**Billingprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) ve [**companyprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)öğesini oluşturup doldurun.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-112">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="f0e8b-113">Dolaylı satıcı KIMLIĞINI [**ilişkili Iş ortağı kimliği**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) özelliğine atadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-113">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="f0e8b-114">Müşteri koleksiyonu işlemlerine bir arabirim almak için [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="f0e8b-115">Müşteriyi oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-115">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="f0e8b-116">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="f0e8b-116">C\# example</span></span>

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

<span data-ttu-id="f0e8b-117">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f0e8b-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f0e8b-118">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: createcustomerforindirectbayi. cs</span><span class="sxs-lookup"><span data-stu-id="f0e8b-118">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f0e8b-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f0e8b-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f0e8b-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f0e8b-120">Request syntax</span></span>

| <span data-ttu-id="f0e8b-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f0e8b-121">Method</span></span>   | <span data-ttu-id="f0e8b-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f0e8b-122">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="f0e8b-123">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="f0e8b-123">**POST**</span></span> | <span data-ttu-id="f0e8b-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="f0e8b-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f0e8b-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f0e8b-125">Request headers</span></span>

<span data-ttu-id="f0e8b-126">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f0e8b-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f0e8b-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f0e8b-127">Request body</span></span>

<span data-ttu-id="f0e8b-128">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-128">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="f0e8b-129">Ad</span><span class="sxs-lookup"><span data-stu-id="f0e8b-129">Name</span></span>                                          | <span data-ttu-id="f0e8b-130">Tür</span><span class="sxs-lookup"><span data-stu-id="f0e8b-130">Type</span></span>   | <span data-ttu-id="f0e8b-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0e8b-131">Required</span></span> | <span data-ttu-id="f0e8b-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0e8b-132">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="f0e8b-133">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="f0e8b-133">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="f0e8b-134">object</span><span class="sxs-lookup"><span data-stu-id="f0e8b-134">object</span></span> | <span data-ttu-id="f0e8b-135">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-135">Yes</span></span>      | <span data-ttu-id="f0e8b-136">Müşterinin Faturalandırma profili bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-136">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="f0e8b-137">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="f0e8b-137">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="f0e8b-138">object</span><span class="sxs-lookup"><span data-stu-id="f0e8b-138">object</span></span> | <span data-ttu-id="f0e8b-139">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-139">Yes</span></span>      | <span data-ttu-id="f0e8b-140">Müşterinin şirket profili bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-140">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="f0e8b-141">Ilişkili iş ortağı kimliği</span><span class="sxs-lookup"><span data-stu-id="f0e8b-141">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="f0e8b-142">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-142">string</span></span> | <span data-ttu-id="f0e8b-143">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-143">Yes</span></span>      | <span data-ttu-id="f0e8b-144">Dolaylı satıcı KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-144">The indirect reseller ID.</span></span> <span data-ttu-id="f0e8b-145">Burada sağlanan KIMLIğIN gösterdiği dolaylı satıcının dolaylı sağlayıcıyla bir ortaklığı olmalıdır veya istek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-145">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="f0e8b-146">Ayrıca, Ilişkili iş ortağı kimliği değeri sağlanmazsa, müşterinin dolaylı satıcı yerine dolaylı sağlayıcının doğrudan müşterisi olarak oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-146">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="f0e8b-147">Etki alanı</span><span class="sxs-lookup"><span data-stu-id="f0e8b-147">Domain</span></span>| <span data-ttu-id="f0e8b-148">Dize</span><span class="sxs-lookup"><span data-stu-id="f0e8b-148">String</span></span>| <span data-ttu-id="f0e8b-149">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-149">Yes</span></span>|<span data-ttu-id="f0e8b-150">Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-150">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="f0e8b-151">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="f0e8b-151">organizationRegistrationNumber</span></span>|    <span data-ttu-id="f0e8b-152">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-152">string</span></span>|<span data-ttu-id="f0e8b-153">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-153">Yes</span></span>|     <span data-ttu-id="f0e8b-154">Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır).</span><span class="sxs-lookup"><span data-stu-id="f0e8b-154">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="f0e8b-155">Yalnızca şu ülkelerde bulunan müşterinin şirketi/kuruluşu için gereklidir: Ermenistan (Har), Azerbaycan (AZ), Belarus (BY), Macaristan (HU), Kazakistan (KZ), Kırgızistan (KG), Moldova (MD), Rusya (RU), Tacikistan dili (TJ), Özbekistan (UZ), Ukrayna (UA), Hindistan, Brezilya, Güney Afrika, Polonya, Birleşik Arap Emirlikleri, Suudi Arabistan, Türkiye, Tayland, Vietnam, Myanmar, Irak, Güney Sudan ve Venezuela.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-155">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan, and Venezuela.</span></span> <span data-ttu-id="f0e8b-156">Müşterinin veya diğer ülkelerde bulunan şirket/kuruluş için bu, isteğe bağlı bir alandır.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-156">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="f0e8b-157">Faturalama profili</span><span class="sxs-lookup"><span data-stu-id="f0e8b-157">Billing profile</span></span>

<span data-ttu-id="f0e8b-158">Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customerbillingprofile](customer-resources.md#customerbillingprofile) kaynağından gereken en düşük alan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-158">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="f0e8b-159">Ad</span><span class="sxs-lookup"><span data-stu-id="f0e8b-159">Name</span></span>             | <span data-ttu-id="f0e8b-160">Tür</span><span class="sxs-lookup"><span data-stu-id="f0e8b-160">Type</span></span>                                     | <span data-ttu-id="f0e8b-161">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0e8b-161">Required</span></span> | <span data-ttu-id="f0e8b-162">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0e8b-162">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f0e8b-163">e-posta</span><span class="sxs-lookup"><span data-stu-id="f0e8b-163">email</span></span>            | <span data-ttu-id="f0e8b-164">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-164">string</span></span>                                   | <span data-ttu-id="f0e8b-165">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-165">Yes</span></span>      | <span data-ttu-id="f0e8b-166">Müşterinin e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-166">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="f0e8b-167">kültür</span><span class="sxs-lookup"><span data-stu-id="f0e8b-167">culture</span></span>          | <span data-ttu-id="f0e8b-168">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-168">string</span></span>                                   | <span data-ttu-id="f0e8b-169">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-169">Yes</span></span>      | <span data-ttu-id="f0e8b-170">İletişim ve para birimi için tercih edilen kültür, "en-US" gibi.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-170">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="f0e8b-171">Desteklenen kültürler için [Iş Ortağı Merkezi tarafından desteklenen dillere ve yerel ayarlara](partner-center-supported-languages-and-locales.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-171">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="f0e8b-172">language</span><span class="sxs-lookup"><span data-stu-id="f0e8b-172">language</span></span>         | <span data-ttu-id="f0e8b-173">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-173">string</span></span>                                   | <span data-ttu-id="f0e8b-174">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-174">Yes</span></span>      | <span data-ttu-id="f0e8b-175">Varsayılan dil.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-175">The default language.</span></span> <span data-ttu-id="f0e8b-176">İki karakter dil kodu (örneğin `en` veya `fr` ) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-176">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="f0e8b-177">Şirket \_ adı</span><span class="sxs-lookup"><span data-stu-id="f0e8b-177">company\_name</span></span>    | <span data-ttu-id="f0e8b-178">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-178">string</span></span>                                   | <span data-ttu-id="f0e8b-179">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-179">Yes</span></span>      | <span data-ttu-id="f0e8b-180">Kayıtlı şirket/kuruluş adı.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-180">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="f0e8b-181">Varsayılan \_ Adres</span><span class="sxs-lookup"><span data-stu-id="f0e8b-181">default\_address</span></span> | [<span data-ttu-id="f0e8b-182">Adres</span><span class="sxs-lookup"><span data-stu-id="f0e8b-182">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="f0e8b-183">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-183">Yes</span></span>      | <span data-ttu-id="f0e8b-184">Müşterinin şirketinin/kuruluşunun kayıtlı adresi.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-184">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="f0e8b-185">Herhangi bir uzunluk sınırlaması hakkında bilgi için bkz. [Adres](utility-resources.md#address) kaynağı.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-185">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="f0e8b-186">Şirket profili</span><span class="sxs-lookup"><span data-stu-id="f0e8b-186">Company profile</span></span>

<span data-ttu-id="f0e8b-187">Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customercompanyprofile](customer-resources.md#customercompanyprofile) kaynağından gereken en düşük alan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-187">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="f0e8b-188">Ad</span><span class="sxs-lookup"><span data-stu-id="f0e8b-188">Name</span></span>   | <span data-ttu-id="f0e8b-189">Tür</span><span class="sxs-lookup"><span data-stu-id="f0e8b-189">Type</span></span>   | <span data-ttu-id="f0e8b-190">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f0e8b-190">Required</span></span> | <span data-ttu-id="f0e8b-191">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f0e8b-191">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="f0e8b-192">etki alanı</span><span class="sxs-lookup"><span data-stu-id="f0e8b-192">domain</span></span> | <span data-ttu-id="f0e8b-193">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-193">string</span></span> | <span data-ttu-id="f0e8b-194">Yes</span><span class="sxs-lookup"><span data-stu-id="f0e8b-194">Yes</span></span>     | <span data-ttu-id="f0e8b-195">Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-195">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="f0e8b-196">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="f0e8b-196">organizationRegistrationNumber</span></span> | <span data-ttu-id="f0e8b-197">string</span><span class="sxs-lookup"><span data-stu-id="f0e8b-197">string</span></span> | <span data-ttu-id="f0e8b-198">Koşula bağlıdır</span><span class="sxs-lookup"><span data-stu-id="f0e8b-198">Depends on condition</span></span> | <span data-ttu-id="f0e8b-199">Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır).</span><span class="sxs-lookup"><span data-stu-id="f0e8b-199">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="f0e8b-200">Bu alanın tamamlanması yalnızca bir müşterinin şirketi/kuruluşu aşağıdaki ülkelerde bulunuyorsa gereklidir:</span><span class="sxs-lookup"><span data-stu-id="f0e8b-200">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="f0e8b-201">-Ermenistan (Har)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-201">- Armenia (AM)</span></span> <br/><span data-ttu-id="f0e8b-202">-Azerbaycan (AZ)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-202">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="f0e8b-203">-Belarus (BY)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-203">- Belarus (BY)</span></span><br/><span data-ttu-id="f0e8b-204">-Macaristan (HU)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-204">- Hungary (HU)</span></span><br/><span data-ttu-id="f0e8b-205">-Kazakistan (KZ)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-205">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="f0e8b-206">-Kırgızistan (KG)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-206">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="f0e8b-207">-Moldova (MD)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-207">- Moldova (MD)</span></span><br/><span data-ttu-id="f0e8b-208">-Rusya (RU)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-208">- Russia (RU)</span></span><br/><span data-ttu-id="f0e8b-209">-Tacikistan (TJ)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-209">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="f0e8b-210">-Özbekistan (UZ)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-210">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="f0e8b-211">-Ukrayna (UA)</span><span class="sxs-lookup"><span data-stu-id="f0e8b-211">- Ukraine (UA)</span></span><br/><span data-ttu-id="f0e8b-212">-Hindistan</span><span class="sxs-lookup"><span data-stu-id="f0e8b-212">- India</span></span> <br/><span data-ttu-id="f0e8b-213">-Brezilya</span><span class="sxs-lookup"><span data-stu-id="f0e8b-213">- Brazil</span></span> <br/><span data-ttu-id="f0e8b-214">-Güney Afrika</span><span class="sxs-lookup"><span data-stu-id="f0e8b-214">- South Africa</span></span> <br/><span data-ttu-id="f0e8b-215">-Polonya</span><span class="sxs-lookup"><span data-stu-id="f0e8b-215">- Poland</span></span> <br/><span data-ttu-id="f0e8b-216">-Birleşik Arap Emirlikleri</span><span class="sxs-lookup"><span data-stu-id="f0e8b-216">- United Arab Emirates</span></span> <br/><span data-ttu-id="f0e8b-217">-Suudi Arabistan</span><span class="sxs-lookup"><span data-stu-id="f0e8b-217">- Saudi Arabia</span></span> <br/><span data-ttu-id="f0e8b-218">-Türkiye</span><span class="sxs-lookup"><span data-stu-id="f0e8b-218">- Turkey</span></span> <br/><span data-ttu-id="f0e8b-219">-Tayland</span><span class="sxs-lookup"><span data-stu-id="f0e8b-219">- Thailand</span></span> <br/><span data-ttu-id="f0e8b-220">-Vietnam</span><span class="sxs-lookup"><span data-stu-id="f0e8b-220">- Vietnam</span></span> <br/><span data-ttu-id="f0e8b-221">-Myanmar dili</span><span class="sxs-lookup"><span data-stu-id="f0e8b-221">- Myanmar</span></span> <br/><span data-ttu-id="f0e8b-222">-Irak</span><span class="sxs-lookup"><span data-stu-id="f0e8b-222">- Iraq</span></span> <br/><span data-ttu-id="f0e8b-223">-Güney Sudan</span><span class="sxs-lookup"><span data-stu-id="f0e8b-223">- South Sudan</span></span> <br/><span data-ttu-id="f0e8b-224">-Venezuela</span><span class="sxs-lookup"><span data-stu-id="f0e8b-224">- Venezuela</span></span><br/> <br/><span data-ttu-id="f0e8b-225">Müşterinin veya diğer ülkelerde bulunan şirket/kuruluş için, bu isteğe bağlı bir alandır.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-225">For customer’s company/organization located in other countries, this is an optional field.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="f0e8b-226">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f0e8b-226">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f0e8b-227">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f0e8b-227">REST response</span></span>

<span data-ttu-id="f0e8b-228">Başarılı olursa, yanıt yeni müşteri için bir [Müşteri](customer-resources.md#customer) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-228">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f0e8b-229">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f0e8b-229">Response success and error codes</span></span>

<span data-ttu-id="f0e8b-230">Yanıtlar, başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-230">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f0e8b-231">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f0e8b-231">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f0e8b-232">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f0e8b-232">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f0e8b-233">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f0e8b-233">Response example</span></span>

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