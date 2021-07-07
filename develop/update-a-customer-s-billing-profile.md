---
title: Müşterinin faturalandırma profilini güncelleştirme
description: Bir müşterinin faturalandırma profilini, profille ilişkili adres da dahil olmak üzere güncelleştirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 1605c3e8cb050717209cb482d2299e2a42b9b186
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530048"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="afa3a-103">Müşterinin faturalandırma profilini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="afa3a-103">Update a customer's billing profile</span></span>

<span data-ttu-id="afa3a-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="afa3a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="afa3a-105">Bir müşterinin faturalandırma profilini, profille ilişkili adres da dahil olmak üzere güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="afa3a-105">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="afa3a-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="afa3a-106">Prerequisites</span></span>

- <span data-ttu-id="afa3a-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="afa3a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="afa3a-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="afa3a-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="afa3a-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="afa3a-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="afa3a-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="afa3a-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="afa3a-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="afa3a-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="afa3a-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="afa3a-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="afa3a-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="afa3a-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="afa3a-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="afa3a-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="afa3a-115">C\#</span><span class="sxs-lookup"><span data-stu-id="afa3a-115">C\#</span></span>

<span data-ttu-id="afa3a-116">Müşterinin faturalandırma profilini güncelleştirmek için faturalandırma profilini alın ve özellikleri gerektiği gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="afa3a-116">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="afa3a-117">Ardından, [**ıpartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu alın ve ardından [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="afa3a-117">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="afa3a-118">Ardından [**faturalandırma**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) özelliği tarafından izlenen [**profiller**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="afa3a-118">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="afa3a-119">Ardından, [**Update ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) veya [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) yöntemlerini çağırarak son ' u çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="afa3a-119">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="afa3a-120">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="afa3a-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="afa3a-121">**Project**: partnersdk. featuresamples **sınıfı**: updatecustomerbillingprofile. cs</span><span class="sxs-lookup"><span data-stu-id="afa3a-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="afa3a-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="afa3a-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="afa3a-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="afa3a-123">Request syntax</span></span>

| <span data-ttu-id="afa3a-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="afa3a-124">Method</span></span>  | <span data-ttu-id="afa3a-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="afa3a-125">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="afa3a-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="afa3a-126">**PUT**</span></span> | <span data-ttu-id="afa3a-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Profiles/faturalandırma http/1.1</span><span class="sxs-lookup"><span data-stu-id="afa3a-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="afa3a-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="afa3a-128">URI parameter</span></span>

<span data-ttu-id="afa3a-129">Faturalandırma profilini güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="afa3a-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="afa3a-130">Ad</span><span class="sxs-lookup"><span data-stu-id="afa3a-130">Name</span></span>                   | <span data-ttu-id="afa3a-131">Tür</span><span class="sxs-lookup"><span data-stu-id="afa3a-131">Type</span></span>     | <span data-ttu-id="afa3a-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="afa3a-132">Required</span></span> | <span data-ttu-id="afa3a-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="afa3a-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="afa3a-134">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="afa3a-134">**customer-tenant-id**</span></span> | <span data-ttu-id="afa3a-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="afa3a-135">**guid**</span></span> | <span data-ttu-id="afa3a-136">Y</span><span class="sxs-lookup"><span data-stu-id="afa3a-136">Y</span></span>        | <span data-ttu-id="afa3a-137">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="afa3a-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="afa3a-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="afa3a-138">Request headers</span></span>

- <span data-ttu-id="afa3a-139">**IF-Match**: &lt; &gt; eşzamanlılık algılama için "ETag" gereklidir.</span><span class="sxs-lookup"><span data-stu-id="afa3a-139">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="afa3a-140">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="afa3a-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="afa3a-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="afa3a-141">Request body</span></span>

<span data-ttu-id="afa3a-142">Tam kaynak.</span><span class="sxs-lookup"><span data-stu-id="afa3a-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="afa3a-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="afa3a-143">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
Content-Type: application/json
Content-Length: 639
Expect: 100-continue

{
    "Id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "FirstName": "FirstName",
    "LastName": "LastName",
    "Email": "email@sample.com",
    "Culture": "en-US",
    "Language": "en",
    "CompanyName": "CompanyName",
    "DefaultAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "One Microsoft Way",
        "AddressLine2": null,
        "PostalCode": "98052",
        "FirstName": "FirstName",
        "LastName": "LastName",
        "PhoneNumber": "4255555555"
    },
    "Links": {
        "Self": {
            "Uri": "/v1/customers/<customer-tenant-id>/profiles/billing",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "CustomerBillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="afa3a-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="afa3a-144">REST response</span></span>

<span data-ttu-id="afa3a-145">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [profil](profile-resources.md) kaynağı özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="afa3a-145">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="afa3a-146">Bu çağrı eşzamanlılık algılama için ETag gerektirir.</span><span class="sxs-lookup"><span data-stu-id="afa3a-146">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="afa3a-147">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="afa3a-147">Response success and error codes</span></span>

<span data-ttu-id="afa3a-148">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="afa3a-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="afa3a-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="afa3a-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="afa3a-150">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="afa3a-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="afa3a-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="afa3a-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1210
Content-Type: application/json
MS-CorrelationId: ff1b757d-cfaf-463a-b48b-0f96d05e95d7
MS-RequestId: ff85f13a-eb65-4b8e-9b67-05beb0565410
Date: Mon, 23 Nov 2015 18:20:43 GMT

{
    "id": "a58ceba5-60ac-48e4-a0bc-2a855811807a",
    "firstName": "FirstName",
    "lastName": "LastName",
    "email": "email@sample.com",
    "culture": "en-US",
    "language": "en",
    "companyName": "companyName",
    "defaultAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "One Microsoft Way",
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
