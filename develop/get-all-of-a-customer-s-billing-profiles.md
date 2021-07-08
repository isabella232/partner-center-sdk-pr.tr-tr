---
title: Müşterinin faturalandırma profilini alma
description: Müşterinin faturalama profilini alır. Bu İş Ortağı Merkezi, önce bir müşteri seçerek gerçekleştirebilirsiniz.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d22be53a5be4efcda76a568578468615495febb6
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760598"
---
# <a name="get-a-customers-billing-profile"></a><span data-ttu-id="9c89c-104">Müşterinin faturalandırma profilini alma</span><span class="sxs-lookup"><span data-stu-id="9c89c-104">Get a customer's billing profile</span></span>

<span data-ttu-id="9c89c-105">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9c89c-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9c89c-106">Müşterinin faturalama profilini alır.</span><span class="sxs-lookup"><span data-stu-id="9c89c-106">Gets the billing profile of a customer.</span></span>

<span data-ttu-id="9c89c-107">Bu İş Ortağı Merkezi önce bir müşteri [seçerek gerçekleştirebilirsiniz.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="9c89c-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="9c89c-108">Ardından, sol kenar çubuğuna müşterinin adının altında Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="9c89c-108">Then, under the customer's name in the left sidebar, select **Account**.</span></span> <span data-ttu-id="9c89c-109">Faturalama profili Fatura bilgileri **başlığı altında** bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="9c89c-109">The billing profile can be found under the **Bill-to info** heading.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9c89c-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9c89c-110">Prerequisites</span></span>

- <span data-ttu-id="9c89c-111">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9c89c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9c89c-112">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="9c89c-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9c89c-113">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9c89c-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9c89c-114">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="9c89c-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9c89c-115">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="9c89c-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9c89c-116">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="9c89c-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9c89c-117">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="9c89c-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9c89c-118">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="9c89c-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9c89c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="9c89c-119">C\#</span></span>

<span data-ttu-id="9c89c-120">Müşterinin faturalama profilini almak için [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonu kullanın ve [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) arayın.</span><span class="sxs-lookup"><span data-stu-id="9c89c-120">To get a customer's billing profile, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="9c89c-121">Ardından [**Profiles özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) ve ardından [**Faturalama**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) özelliğini arayın.</span><span class="sxs-lookup"><span data-stu-id="9c89c-121">Then call the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, followed by the [**Billing**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.billing) property.</span></span> <span data-ttu-id="9c89c-122">Son olarak [**Get() veya**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) [**GetAsync() yöntemlerini**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) arayın.</span><span class="sxs-lookup"><span data-stu-id="9c89c-122">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;

var billingProfile = partnerOperations.Customers.ById(selectedCustomerId).Profiles.Billing.Get();
```

<span data-ttu-id="9c89c-123">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9c89c-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9c89c-124">**Project:** PartnerSDK.FeatureSamples **Sınıfı:** GetCustomerBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="9c89c-124">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9c89c-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9c89c-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9c89c-126">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="9c89c-126">Request syntax</span></span>

| <span data-ttu-id="9c89c-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9c89c-127">Method</span></span>  | <span data-ttu-id="9c89c-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9c89c-128">Request URI</span></span>                                                                                             |
|---------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9c89c-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="9c89c-129">**GET**</span></span> | <span data-ttu-id="9c89c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9c89c-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/profiles/billing HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9c89c-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="9c89c-131">URI parameter</span></span>

<span data-ttu-id="9c89c-132">Faturalama profilini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c89c-132">Use the following query parameter to get the billing profile.</span></span>

| <span data-ttu-id="9c89c-133">Ad</span><span class="sxs-lookup"><span data-stu-id="9c89c-133">Name</span></span>                   | <span data-ttu-id="9c89c-134">Tür</span><span class="sxs-lookup"><span data-stu-id="9c89c-134">Type</span></span>     | <span data-ttu-id="9c89c-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9c89c-135">Required</span></span> | <span data-ttu-id="9c89c-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9c89c-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9c89c-137">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="9c89c-137">**customer-tenant-id**</span></span> | <span data-ttu-id="9c89c-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="9c89c-138">**guid**</span></span> | <span data-ttu-id="9c89c-139">Y</span><span class="sxs-lookup"><span data-stu-id="9c89c-139">Y</span></span>        | <span data-ttu-id="9c89c-140">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="9c89c-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9c89c-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9c89c-141">Request headers</span></span>

<span data-ttu-id="9c89c-142">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9c89c-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9c89c-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9c89c-143">Request body</span></span>

<span data-ttu-id="9c89c-144">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="9c89c-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="9c89c-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9c89c-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a5581a74-2778-4e34-9172-18baa4877081
MS-CorrelationId: 51d521b3-62db-4682-b75d-fb8ab09113b2
```

## <a name="rest-response"></a><span data-ttu-id="9c89c-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9c89c-146">REST response</span></span>

<span data-ttu-id="9c89c-147">Başarılı olursa, bu yöntem yanıt [gövdesinde profil](profile-resources.md) kaynakları koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="9c89c-147">If successful, this method returns a collection of [Profile](profile-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9c89c-148">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9c89c-148">Response success and error codes</span></span>

<span data-ttu-id="9c89c-149">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="9c89c-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9c89c-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9c89c-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9c89c-151">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9c89c-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9c89c-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9c89c-152">Response example</span></span>

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
