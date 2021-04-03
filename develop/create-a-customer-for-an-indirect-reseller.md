---
title: Dolaylı satıcı için müşteri oluşturma
description: Dolaylı bir sağlayıcının dolaylı bir satıcı için müşteri oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanabileceği hakkında bilgi edinin.
ms.date: 04/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 0de40d08e9fc2b9cf87b7c3c41214fdd34ad26f3
ms.sourcegitcommit: faea78fe3264cbafc2b02c04d98d5ce30e992124
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/03/2021
ms.locfileid: "106274589"
---
# <a name="create-a-customer-for-an-indirect-reseller-using-partner-center-apis"></a><span data-ttu-id="0f158-103">Iş Ortağı Merkezi API 'Lerini kullanarak dolaylı satıcı için müşteri oluşturma</span><span class="sxs-lookup"><span data-stu-id="0f158-103">Create a customer for an indirect reseller using Partner Center APIs</span></span>

<span data-ttu-id="0f158-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="0f158-104">**Applies to:**</span></span>

- <span data-ttu-id="0f158-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0f158-105">Partner Center</span></span>

<span data-ttu-id="0f158-106">Dolaylı bir sağlayıcı, dolaylı bir satıcı için müşteri oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="0f158-106">An indirect provider can create a customer for an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f158-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0f158-107">Prerequisites</span></span>

- <span data-ttu-id="0f158-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0f158-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0f158-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="0f158-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0f158-110">Dolaylı Bayi kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="0f158-110">The tenant identifier of the indirect reseller.</span></span>

- <span data-ttu-id="0f158-111">Dolaylı satıcının dolaylı sağlayıcıyla bir ortaklığı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f158-111">The indirect reseller must have a partnership with the indirect provider.</span></span>

## <a name="c"></a><span data-ttu-id="0f158-112">C\#</span><span class="sxs-lookup"><span data-stu-id="0f158-112">C\#</span></span>

<span data-ttu-id="0f158-113">Dolaylı bir satıcı için yeni bir müşteri eklemek için:</span><span class="sxs-lookup"><span data-stu-id="0f158-113">To add a new customer for an indirect reseller:</span></span>

1. <span data-ttu-id="0f158-114">Yeni bir [**Müşteri**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) nesnesi örneği oluşturun ve ardından [**Billingprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) ve [**companyprofile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile)öğesini oluşturup doldurun.</span><span class="sxs-lookup"><span data-stu-id="0f158-114">Instantiate a new [**Customer**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer) object and then instantiate and populate the [**BillingProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customerbillingprofile) and [**CompanyProfile**](/dotnet/api/microsoft.store.partnercenter.models.customers.customercompanyprofile).</span></span> <span data-ttu-id="0f158-115">Dolaylı satıcı KIMLIĞINI [**ilişkili Iş ortağı kimliği**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) özelliğine atadığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f158-115">Be sure to assign the indirect reseller ID to the [**AssociatedPartnerID**](/dotnet/api/microsoft.store.partnercenter.models.customers.customer.associatedpartnerid) property.</span></span>

2. <span data-ttu-id="0f158-116">Müşteri koleksiyonu işlemlerine bir arabirim almak için [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f158-116">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) property to get an interface to customer collection operations.</span></span>

3. <span data-ttu-id="0f158-117">Müşteriyi oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="0f158-117">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the customer.</span></span>

### <a name="c-example"></a><span data-ttu-id="0f158-118">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="0f158-118">C\# example</span></span>

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

<span data-ttu-id="0f158-119">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0f158-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0f158-120">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: createcustomerforındirectbayi. cs</span><span class="sxs-lookup"><span data-stu-id="0f158-120">**Project**: Partner Center SDK Samples **Class**: CreateCustomerforIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0f158-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0f158-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0f158-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0f158-122">Request syntax</span></span>

| <span data-ttu-id="0f158-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0f158-123">Method</span></span>   | <span data-ttu-id="0f158-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0f158-124">Request URI</span></span>                                                       |
|----------|-------------------------------------------------------------------|
| <span data-ttu-id="0f158-125">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="0f158-125">**POST**</span></span> | <span data-ttu-id="0f158-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers http/1.1</span><span class="sxs-lookup"><span data-stu-id="0f158-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0f158-127">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0f158-127">Request headers</span></span>

<span data-ttu-id="0f158-128">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0f158-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0f158-129">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0f158-129">Request body</span></span>

<span data-ttu-id="0f158-130">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0f158-130">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="0f158-131">Ad</span><span class="sxs-lookup"><span data-stu-id="0f158-131">Name</span></span>                                          | <span data-ttu-id="0f158-132">Tür</span><span class="sxs-lookup"><span data-stu-id="0f158-132">Type</span></span>   | <span data-ttu-id="0f158-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0f158-133">Required</span></span> | <span data-ttu-id="0f158-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f158-134">Description</span></span>                                                                                                                                                                                                                                                                                                                                           |
|-----------------------------------------------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| [<span data-ttu-id="0f158-135">BillingProfile</span><span class="sxs-lookup"><span data-stu-id="0f158-135">BillingProfile</span></span>](#billing-profile)             | <span data-ttu-id="0f158-136">object</span><span class="sxs-lookup"><span data-stu-id="0f158-136">object</span></span> | <span data-ttu-id="0f158-137">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-137">Yes</span></span>      | <span data-ttu-id="0f158-138">Müşterinin Faturalandırma profili bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0f158-138">The customer's billing profile information.</span></span>                                                                                                                                                                                                                                                                                                           |
| [<span data-ttu-id="0f158-139">CompanyProfile</span><span class="sxs-lookup"><span data-stu-id="0f158-139">CompanyProfile</span></span>](#company-profile)             | <span data-ttu-id="0f158-140">object</span><span class="sxs-lookup"><span data-stu-id="0f158-140">object</span></span> | <span data-ttu-id="0f158-141">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-141">Yes</span></span>      | <span data-ttu-id="0f158-142">Müşterinin şirket profili bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0f158-142">The customer's company profile information.</span></span>                                                               
| [<span data-ttu-id="0f158-143">Ilişkili iş ortağı kimliği</span><span class="sxs-lookup"><span data-stu-id="0f158-143">AssociatedPartnerId</span></span>](customer-resources.md#customer) | <span data-ttu-id="0f158-144">string</span><span class="sxs-lookup"><span data-stu-id="0f158-144">string</span></span> | <span data-ttu-id="0f158-145">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-145">Yes</span></span>      | <span data-ttu-id="0f158-146">Dolaylı satıcı KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="0f158-146">The indirect reseller ID.</span></span> <span data-ttu-id="0f158-147">Burada sağlanan KIMLIğIN gösterdiği dolaylı satıcının dolaylı sağlayıcıyla bir ortaklığı olmalıdır veya istek başarısız olur.</span><span class="sxs-lookup"><span data-stu-id="0f158-147">The indirect reseller as indicated by the ID supplied here must have a partnership with the indirect provider or the request will fail.</span></span> <span data-ttu-id="0f158-148">Ayrıca, Ilişkili iş ortağı kimliği değeri sağlanmazsa, müşterinin dolaylı satıcı yerine dolaylı sağlayıcının doğrudan müşterisi olarak oluşturulduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="0f158-148">Also note that if the AssociatedPartnerId value isn't supplied, the customer is created as a direct customer of the indirect provider rather than the indirect reseller.</span></span> |
|<span data-ttu-id="0f158-149">Etki alanı</span><span class="sxs-lookup"><span data-stu-id="0f158-149">Domain</span></span>| <span data-ttu-id="0f158-150">Dize</span><span class="sxs-lookup"><span data-stu-id="0f158-150">String</span></span>| <span data-ttu-id="0f158-151">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-151">Yes</span></span>|<span data-ttu-id="0f158-152">Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="0f158-152">The customer's domain name, such as contoso.onmicrosoft.com.</span></span>|
|<span data-ttu-id="0f158-153">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="0f158-153">organizationRegistrationNumber</span></span>|    <span data-ttu-id="0f158-154">string</span><span class="sxs-lookup"><span data-stu-id="0f158-154">string</span></span>|<span data-ttu-id="0f158-155">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-155">Yes</span></span>|     <span data-ttu-id="0f158-156">Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır).</span><span class="sxs-lookup"><span data-stu-id="0f158-156">The customer’s organization registration number (also referred to as INN number in certain countries).</span></span> <span data-ttu-id="0f158-157">Yalnızca şu ülkelerde bulunan müşterinin şirketi/kuruluşu için gereklidir: Ermenistan (Har), Azerbaycan (AZ), Belarus (BY), Macaristan (HU), Kazakistan (KZ), Kırgızistan (KG), Moldova (MD), Rusya (RU), Tacikistan dili (TJ), Özbekistan (UZ), Ukrayna (UA), Hindistan, Brezilya, Güney Afrika, Polonya, Birleşik Arap Emirlikleri, Suudi Arabistan, Türkiye, Tayland, Vietnam, Myanmar, Irak, Güney Sudan ve Venezuela.</span><span class="sxs-lookup"><span data-stu-id="0f158-157">Only required for customer’s company/organization located in the following countries: Armenia(AM), Azerbaijan(AZ), Belarus(BY), Hungary(HU), Kazakhstan(KZ), Kyrgyzstan(KG), Moldova(MD), Russia(RU), Tajikistan(TJ), Uzbekistan(UZ), Ukraine(UA), India, Brazil, South Africa, Poland, United Arab Emirates, Saudi Arabia, Turkey, Thailand, Vietnam, Myanmar, Iraq, South Sudan and Venezuela.</span></span> <span data-ttu-id="0f158-158">Müşterinin veya diğer ülkelerde bulunan şirket/kuruluş için bu, isteğe bağlı bir alandır.</span><span class="sxs-lookup"><span data-stu-id="0f158-158">For customer’s company/organization located in other countries this is an optional field.</span></span>|



#### <a name="billing-profile"></a><span data-ttu-id="0f158-159">Faturalama profili</span><span class="sxs-lookup"><span data-stu-id="0f158-159">Billing profile</span></span>

<span data-ttu-id="0f158-160">Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customerbillingprofile](customer-resources.md#customerbillingprofile) kaynağından gereken en düşük alan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0f158-160">This table describes the minimum required fields from the [CustomerBillingProfile](customer-resources.md#customerbillingprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="0f158-161">Ad</span><span class="sxs-lookup"><span data-stu-id="0f158-161">Name</span></span>             | <span data-ttu-id="0f158-162">Tür</span><span class="sxs-lookup"><span data-stu-id="0f158-162">Type</span></span>                                     | <span data-ttu-id="0f158-163">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0f158-163">Required</span></span> | <span data-ttu-id="0f158-164">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f158-164">Description</span></span>                                                                                                                                                                                                     |
|------------------|------------------------------------------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0f158-165">e-posta</span><span class="sxs-lookup"><span data-stu-id="0f158-165">email</span></span>            | <span data-ttu-id="0f158-166">string</span><span class="sxs-lookup"><span data-stu-id="0f158-166">string</span></span>                                   | <span data-ttu-id="0f158-167">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-167">Yes</span></span>      | <span data-ttu-id="0f158-168">Müşterinin e-posta adresi.</span><span class="sxs-lookup"><span data-stu-id="0f158-168">The customer's email address.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="0f158-169">kültür</span><span class="sxs-lookup"><span data-stu-id="0f158-169">culture</span></span>          | <span data-ttu-id="0f158-170">string</span><span class="sxs-lookup"><span data-stu-id="0f158-170">string</span></span>                                   | <span data-ttu-id="0f158-171">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-171">Yes</span></span>      | <span data-ttu-id="0f158-172">İletişim ve para birimi için tercih edilen kültür, "en-US" gibi.</span><span class="sxs-lookup"><span data-stu-id="0f158-172">Their preferred culture for communication and currency, such as "en-US".</span></span> <span data-ttu-id="0f158-173">Desteklenen kültürler için [Iş Ortağı Merkezi tarafından desteklenen dillere ve yerel ayarlara](partner-center-supported-languages-and-locales.md) bakın.</span><span class="sxs-lookup"><span data-stu-id="0f158-173">See [Partner Center supported languages and locales](partner-center-supported-languages-and-locales.md) for the supported cultures.</span></span> |
| <span data-ttu-id="0f158-174">language</span><span class="sxs-lookup"><span data-stu-id="0f158-174">language</span></span>         | <span data-ttu-id="0f158-175">string</span><span class="sxs-lookup"><span data-stu-id="0f158-175">string</span></span>                                   | <span data-ttu-id="0f158-176">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-176">Yes</span></span>      | <span data-ttu-id="0f158-177">Varsayılan dil.</span><span class="sxs-lookup"><span data-stu-id="0f158-177">The default language.</span></span> <span data-ttu-id="0f158-178">İki karakter dil kodu (örneğin `en` veya `fr` ) desteklenir.</span><span class="sxs-lookup"><span data-stu-id="0f158-178">Two character language codes (for example `en` or `fr`) are supported.</span></span>                                                                                                                                |
| <span data-ttu-id="0f158-179">Şirket \_ adı</span><span class="sxs-lookup"><span data-stu-id="0f158-179">company\_name</span></span>    | <span data-ttu-id="0f158-180">string</span><span class="sxs-lookup"><span data-stu-id="0f158-180">string</span></span>                                   | <span data-ttu-id="0f158-181">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-181">Yes</span></span>      | <span data-ttu-id="0f158-182">Kayıtlı şirket/kuruluş adı.</span><span class="sxs-lookup"><span data-stu-id="0f158-182">The registered company/organization name.</span></span>                                                                                                                                                                       |
| <span data-ttu-id="0f158-183">Varsayılan \_ Adres</span><span class="sxs-lookup"><span data-stu-id="0f158-183">default\_address</span></span> | [<span data-ttu-id="0f158-184">Adres</span><span class="sxs-lookup"><span data-stu-id="0f158-184">Address</span></span>](utility-resources.md#address) | <span data-ttu-id="0f158-185">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-185">Yes</span></span>      | <span data-ttu-id="0f158-186">Müşterinin şirketinin/kuruluşunun kayıtlı adresi.</span><span class="sxs-lookup"><span data-stu-id="0f158-186">The registered address of the customer's company/organization.</span></span> <span data-ttu-id="0f158-187">Herhangi bir uzunluk sınırlaması hakkında bilgi için bkz. [Adres](utility-resources.md#address) kaynağı.</span><span class="sxs-lookup"><span data-stu-id="0f158-187">See the [Address](utility-resources.md#address) resource for information on any length limitations.</span></span>                                             |

#### <a name="company-profile"></a><span data-ttu-id="0f158-188">Şirket profili</span><span class="sxs-lookup"><span data-stu-id="0f158-188">Company profile</span></span>

<span data-ttu-id="0f158-189">Bu tabloda, yeni bir müşteri oluşturmak için gereken [Customercompanyprofile](customer-resources.md#customercompanyprofile) kaynağından gereken en düşük alan açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0f158-189">This table describes the minimum required fields from the [CustomerCompanyProfile](customer-resources.md#customercompanyprofile) resource needed to create a new customer.</span></span>

| <span data-ttu-id="0f158-190">Ad</span><span class="sxs-lookup"><span data-stu-id="0f158-190">Name</span></span>   | <span data-ttu-id="0f158-191">Tür</span><span class="sxs-lookup"><span data-stu-id="0f158-191">Type</span></span>   | <span data-ttu-id="0f158-192">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0f158-192">Required</span></span> | <span data-ttu-id="0f158-193">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f158-193">Description</span></span>                                                  |
|--------|--------|----------|--------------------------------------------------------------|
| <span data-ttu-id="0f158-194">etki alanı</span><span class="sxs-lookup"><span data-stu-id="0f158-194">domain</span></span> | <span data-ttu-id="0f158-195">string</span><span class="sxs-lookup"><span data-stu-id="0f158-195">string</span></span> | <span data-ttu-id="0f158-196">Yes</span><span class="sxs-lookup"><span data-stu-id="0f158-196">Yes</span></span>     | <span data-ttu-id="0f158-197">Müşterinin etki alanı adı, örneğin contoso.onmicrosoft.com.</span><span class="sxs-lookup"><span data-stu-id="0f158-197">The customer's domain name, such as contoso.onmicrosoft.com.</span></span> |
| <span data-ttu-id="0f158-198">organizationRegistrationNumber</span><span class="sxs-lookup"><span data-stu-id="0f158-198">organizationRegistrationNumber</span></span> | <span data-ttu-id="0f158-199">string</span><span class="sxs-lookup"><span data-stu-id="0f158-199">string</span></span> | <span data-ttu-id="0f158-200">Koşula bağlıdır</span><span class="sxs-lookup"><span data-stu-id="0f158-200">Depends on condition</span></span> | <span data-ttu-id="0f158-201">Müşterinin kuruluş kayıt numarası (bazı ülkelerde ıNN numarası olarak da adlandırılır).</span><span class="sxs-lookup"><span data-stu-id="0f158-201">The customer’s organization registration number (also referred to as the INN number in certain countries).</span></span> <br/><br/><span data-ttu-id="0f158-202">Bu alanın tamamlanması yalnızca bir müşterinin şirketi/kuruluşu aşağıdaki ülkelerde bulunuyorsa gereklidir:</span><span class="sxs-lookup"><span data-stu-id="0f158-202">Completing this field is required only if a customer’s company/organization is located in the following countries:</span></span> <br/><br/><span data-ttu-id="0f158-203">-Ermenistan (Har)</span><span class="sxs-lookup"><span data-stu-id="0f158-203">- Armenia (AM)</span></span> <br/><span data-ttu-id="0f158-204">-Azerbaycan (AZ)</span><span class="sxs-lookup"><span data-stu-id="0f158-204">- Azerbaijan (AZ)</span></span><br/><span data-ttu-id="0f158-205">-Belarus (BY)</span><span class="sxs-lookup"><span data-stu-id="0f158-205">- Belarus (BY)</span></span><br/><span data-ttu-id="0f158-206">-Macaristan (HU)</span><span class="sxs-lookup"><span data-stu-id="0f158-206">- Hungary (HU)</span></span><br/><span data-ttu-id="0f158-207">-Kazakistan (KZ)</span><span class="sxs-lookup"><span data-stu-id="0f158-207">- Kazakhstan (KZ)</span></span><br/><span data-ttu-id="0f158-208">-Kırgızistan (KG)</span><span class="sxs-lookup"><span data-stu-id="0f158-208">- Kyrgyzstan (KG)</span></span><br/><span data-ttu-id="0f158-209">-Moldova (MD)</span><span class="sxs-lookup"><span data-stu-id="0f158-209">- Moldova (MD)</span></span><br/><span data-ttu-id="0f158-210">-Rusya (RU)</span><span class="sxs-lookup"><span data-stu-id="0f158-210">- Russia (RU)</span></span><br/><span data-ttu-id="0f158-211">-Tacikistan (TJ)</span><span class="sxs-lookup"><span data-stu-id="0f158-211">- Tajikistan (TJ)</span></span><br/><span data-ttu-id="0f158-212">-Özbekistan (UZ)</span><span class="sxs-lookup"><span data-stu-id="0f158-212">- Uzbekistan (UZ)</span></span><br/><span data-ttu-id="0f158-213">-Ukrayna (UA)</span><span class="sxs-lookup"><span data-stu-id="0f158-213">- Ukraine (UA)</span></span><br/><span data-ttu-id="0f158-214">-Hindistan</span><span class="sxs-lookup"><span data-stu-id="0f158-214">- India</span></span> <br/><span data-ttu-id="0f158-215">-Brezilya</span><span class="sxs-lookup"><span data-stu-id="0f158-215">- Brazil</span></span> <br/><span data-ttu-id="0f158-216">-Güney Afrika</span><span class="sxs-lookup"><span data-stu-id="0f158-216">- South Africa</span></span> <br/><span data-ttu-id="0f158-217">-Polonya</span><span class="sxs-lookup"><span data-stu-id="0f158-217">- Poland</span></span> <br/><span data-ttu-id="0f158-218">-Birleşik Arap Emirlikleri</span><span class="sxs-lookup"><span data-stu-id="0f158-218">- United Arab Emirates</span></span> <br/><span data-ttu-id="0f158-219">-Suudi Arabistan</span><span class="sxs-lookup"><span data-stu-id="0f158-219">- Saudi Arabia</span></span> <br/><span data-ttu-id="0f158-220">-Türkiye</span><span class="sxs-lookup"><span data-stu-id="0f158-220">- Turkey</span></span> <br/><span data-ttu-id="0f158-221">-Tayland</span><span class="sxs-lookup"><span data-stu-id="0f158-221">- Thailand</span></span> <br/><span data-ttu-id="0f158-222">-Vietnam</span><span class="sxs-lookup"><span data-stu-id="0f158-222">- Vietnam</span></span> <br/><span data-ttu-id="0f158-223">-Myanmar dili</span><span class="sxs-lookup"><span data-stu-id="0f158-223">- Myanmar</span></span> <br/><span data-ttu-id="0f158-224">-Irak</span><span class="sxs-lookup"><span data-stu-id="0f158-224">- Iraq</span></span> <br/><span data-ttu-id="0f158-225">-Güney Sudan</span><span class="sxs-lookup"><span data-stu-id="0f158-225">- South Sudan</span></span> <br/><span data-ttu-id="0f158-226">-Venezuela</span><span class="sxs-lookup"><span data-stu-id="0f158-226">- Venezuela</span></span><br/> <br/><span data-ttu-id="0f158-227">Müşterinin veya diğer ülkelerde bulunan şirket/kuruluş için bu, isteğe bağlı bir alandır.</span><span class="sxs-lookup"><span data-stu-id="0f158-227">For customer’s company/organization located in other countries this is an optional field.</span></span>  |

### <a name="request-example"></a><span data-ttu-id="0f158-228">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0f158-228">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0f158-229">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0f158-229">REST response</span></span>

<span data-ttu-id="0f158-230">Başarılı olursa, yanıt yeni müşteri için bir [Müşteri](customer-resources.md#customer) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="0f158-230">If successful, the response contains a [Customer](customer-resources.md#customer) resource for the new customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0f158-231">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0f158-231">Response success and error codes</span></span>

<span data-ttu-id="0f158-232">Yanıtlar, başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="0f158-232">Responses come with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0f158-233">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f158-233">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0f158-234">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0f158-234">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0f158-235">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0f158-235">Response example</span></span>

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