---
title: Müşterinin faturalandırma profilini alma
description: Müşterinin faturalandırma profilini alır. Iş Ortağı Merkezi panosunda, bu işlem önce bir müşteri seçilerek gerçekleştirilebilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 6c837c1c220e334df82e75eb680b6012862c9686
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769731"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="89a09-103">Müşterinin faturalandırma profilini alma</span><span class="sxs-lookup"><span data-stu-id="89a09-103">Get a customer's billing profile</span></span>

<span data-ttu-id="89a09-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="89a09-104">**Applies To**</span></span>

- <span data-ttu-id="89a09-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="89a09-105">Partner Center</span></span>
- <span data-ttu-id="89a09-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="89a09-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="89a09-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="89a09-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="89a09-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="89a09-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="89a09-109">Müşterinin faturalandırma profilini alır.</span><span class="sxs-lookup"><span data-stu-id="89a09-109">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="89a09-110">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="89a09-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="89a09-111">Ardından, sol kenar çubuğundaki müşterinin adı altında **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="89a09-111">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="89a09-112">Fatura profili, **Fatura bilgileri** başlığı altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="89a09-112">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89a09-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="89a09-113">Prerequisites</span></span>

- <span data-ttu-id="89a09-114">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="89a09-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="89a09-115">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="89a09-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="89a09-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="89a09-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="89a09-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="89a09-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="89a09-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="89a09-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="89a09-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="89a09-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="89a09-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="89a09-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="89a09-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="89a09-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="89a09-122">C\#</span><span class="sxs-lookup"><span data-stu-id="89a09-122">C\#</span></span>

<span data-ttu-id="89a09-123">Müşterinin faturalandırma profilini almak için [**ıpartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="89a09-123">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="89a09-124">Ardından [**faturalandırma**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) özelliği tarafından izlenen [**profiller**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="89a09-124">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="89a09-125">Son olarak [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="89a09-125">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="89a09-126">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="89a09-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="89a09-127">**Proje**: partnersdk. Featuresamples **sınıfı**: GetCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="89a09-127">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="89a09-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="89a09-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="89a09-129">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="89a09-129">Request syntax</span></span>

| <span data-ttu-id="89a09-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="89a09-130">Method</span></span>  | <span data-ttu-id="89a09-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="89a09-131">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89a09-132">**Al**</span><span class="sxs-lookup"><span data-stu-id="89a09-132">**GET**</span></span> | <span data-ttu-id="89a09-133">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Profiles/faturalandırma http/1.1</span><span class="sxs-lookup"><span data-stu-id="89a09-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="89a09-134">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="89a09-134">URI parameter</span></span>

<span data-ttu-id="89a09-135">Faturalandırma profilini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="89a09-135">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="89a09-136">Ad</span><span class="sxs-lookup"><span data-stu-id="89a09-136">Name</span></span>                   | <span data-ttu-id="89a09-137">Tür</span><span class="sxs-lookup"><span data-stu-id="89a09-137">Type</span></span>     | <span data-ttu-id="89a09-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="89a09-138">Required</span></span> | <span data-ttu-id="89a09-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89a09-139">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89a09-140">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="89a09-140">**customer-tenant-id**</span></span> | <span data-ttu-id="89a09-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="89a09-141">**guid**</span></span> | <span data-ttu-id="89a09-142">Y</span><span class="sxs-lookup"><span data-stu-id="89a09-142">Y</span></span>        | <span data-ttu-id="89a09-143">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="89a09-143">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="89a09-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="89a09-144">Request headers</span></span>

<span data-ttu-id="89a09-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="89a09-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="89a09-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="89a09-146">Request body</span></span>

<span data-ttu-id="89a09-147">Yok</span><span class="sxs-lookup"><span data-stu-id="89a09-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="89a09-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="89a09-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="89a09-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="89a09-149">REST response</span></span>

<span data-ttu-id="89a09-150">Başarılı olursa, bu yöntem yanıt gövdesinde [profil](profile-resources.md) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="89a09-150">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="89a09-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="89a09-151">Response success and error codes</span></span>

<span data-ttu-id="89a09-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="89a09-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89a09-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="89a09-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89a09-154">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="89a09-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="89a09-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="89a09-155">Response example</span></span>

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
