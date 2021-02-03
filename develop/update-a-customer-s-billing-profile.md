---
title: Müşterinin faturalandırma profilini güncelleştirme
description: Bir müşterinin faturalandırma profilini, profille ilişkili adres da dahil olmak üzere güncelleştirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: adf4e3de9941fded632e0561624d91d854c5aa24
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769778"
---
# <a name="update-a-customers-billing-profile"></a><span data-ttu-id="f2621-103">Müşterinin faturalandırma profilini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="f2621-103">Update a customer's billing profile</span></span>

<span data-ttu-id="f2621-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="f2621-104">**Applies To**</span></span>

- <span data-ttu-id="f2621-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2621-105">Partner Center</span></span>
- <span data-ttu-id="f2621-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2621-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f2621-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2621-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f2621-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2621-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f2621-109">Bir müşterinin faturalandırma profilini, profille ilişkili adres da dahil olmak üzere güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="f2621-109">Updates a customer's billing profile, including the address associated with the profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f2621-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f2621-110">Prerequisites</span></span>

- <span data-ttu-id="f2621-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f2621-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f2621-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="f2621-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f2621-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f2621-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f2621-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2621-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f2621-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f2621-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f2621-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f2621-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f2621-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="f2621-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f2621-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="f2621-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f2621-119">C\#</span><span class="sxs-lookup"><span data-stu-id="f2621-119">C\#</span></span>

<span data-ttu-id="f2621-120">Müşterinin faturalandırma profilini güncelleştirmek için faturalandırma profilini alın ve özellikleri gerektiği gibi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f2621-120">To update a customer's billing profile, retrieve the billing profile and update the properties as necessary.</span></span> <span data-ttu-id="f2621-121">Ardından, [**ıpartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu alın ve ardından [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f2621-121">Then, retrieve your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection, and then call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="f2621-122">Ardından [**faturalandırma**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) özelliği tarafından izlenen [**profiller**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f2621-122">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="f2621-123">Ardından, [**Update ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) veya [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) yöntemlerini çağırarak son ' u çalıştırın.</span><span class="sxs-lookup"><span data-stu-id="f2621-123">Then, finish by calling the [**Update()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofile-1.updateasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();

// Apply changes to profile;

billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Update(billingProfile);
```

<span data-ttu-id="f2621-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f2621-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f2621-125">**Proje**: partnersdk. Featuresamples **sınıfı**: UpdateCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="f2621-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f2621-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f2621-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f2621-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f2621-127">Request syntax</span></span>

| <span data-ttu-id="f2621-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f2621-128">Method</span></span>  | <span data-ttu-id="f2621-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f2621-129">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f2621-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="f2621-130">**PUT**</span></span> | <span data-ttu-id="f2621-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Profiles/faturalandırma http/1.1</span><span class="sxs-lookup"><span data-stu-id="f2621-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f2621-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="f2621-132">URI parameter</span></span>

<span data-ttu-id="f2621-133">Faturalandırma profilini güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2621-133">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="f2621-134">Ad</span><span class="sxs-lookup"><span data-stu-id="f2621-134">Name</span></span>                   | <span data-ttu-id="f2621-135">Tür</span><span class="sxs-lookup"><span data-stu-id="f2621-135">Type</span></span>     | <span data-ttu-id="f2621-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f2621-136">Required</span></span> | <span data-ttu-id="f2621-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f2621-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f2621-138">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="f2621-138">**customer-tenant-id**</span></span> | <span data-ttu-id="f2621-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="f2621-139">**guid**</span></span> | <span data-ttu-id="f2621-140">Y</span><span class="sxs-lookup"><span data-stu-id="f2621-140">Y</span></span>        | <span data-ttu-id="f2621-141">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="f2621-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f2621-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f2621-142">Request headers</span></span>

- <span data-ttu-id="f2621-143">**IF-Match**: &lt; &gt; eşzamanlılık algılama için "ETag" gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2621-143">**If-Match**: "&lt;ETag&gt;" is required for concurrency detection.</span></span>
<span data-ttu-id="f2621-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f2621-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f2621-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f2621-145">Request body</span></span>

<span data-ttu-id="f2621-146">Tam kaynak.</span><span class="sxs-lookup"><span data-stu-id="f2621-146">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="f2621-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f2621-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="f2621-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f2621-148">REST response</span></span>

<span data-ttu-id="f2621-149">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [profil](profile-resources.md) kaynağı özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f2621-149">If successful, this method returns updated [Profile](profile-resources.md) resource properties in the response body.</span></span> <span data-ttu-id="f2621-150">Bu çağrı eşzamanlılık algılama için ETag gerektirir.</span><span class="sxs-lookup"><span data-stu-id="f2621-150">This call requires an ETag for concurrency detection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f2621-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f2621-151">Response success and error codes</span></span>

<span data-ttu-id="f2621-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="f2621-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f2621-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2621-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f2621-154">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f2621-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f2621-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f2621-155">Response example</span></span>

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
