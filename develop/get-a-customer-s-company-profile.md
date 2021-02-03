---
title: Müşterinin şirket profilini alma
description: Müşterinin Şirket profilini alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: c26a86ecb96e5e7942ba179f8a3cc704abab7df5
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769371"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="7168f-103">Müşterinin şirket profilini alma</span><span class="sxs-lookup"><span data-stu-id="7168f-103">Get a customer's company profile</span></span>

<span data-ttu-id="7168f-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="7168f-104">**Applies To**</span></span>

- <span data-ttu-id="7168f-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7168f-105">Partner Center</span></span>
- <span data-ttu-id="7168f-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7168f-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7168f-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7168f-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7168f-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7168f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7168f-109">Müşterinin Şirket profilini alır.</span><span class="sxs-lookup"><span data-stu-id="7168f-109">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7168f-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7168f-110">Prerequisites</span></span>

- <span data-ttu-id="7168f-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7168f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7168f-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7168f-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7168f-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7168f-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7168f-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7168f-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7168f-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7168f-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7168f-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7168f-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7168f-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="7168f-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7168f-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="7168f-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="7168f-119">C\#</span><span class="sxs-lookup"><span data-stu-id="7168f-119">C\#</span></span>

<span data-ttu-id="7168f-120">Müşterinin Şirket profilini almak için müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7168f-120">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="7168f-121">Ardından, şirket özelliğine erişebilmek için, [**profiller**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) özelliğinden müşterinin [**ıcustomerprofilecollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) arabirimini alın.</span><span class="sxs-lookup"><span data-stu-id="7168f-121">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="7168f-122">Daha sonra [**ıcustomerreadonlyprofile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) arabirimini [**ıustomerprofilecollection. Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) özelliğinden alın ve [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7168f-122">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="7168f-123">**Örnek**: [iş ortağı Merkezi SDK 'sını indirin](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span><span class="sxs-lookup"><span data-stu-id="7168f-123">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="7168f-124">**Proje**: partnersdk. Featuresamples **sınıfı**: GetCustomerCompanyProfile.cs</span><span class="sxs-lookup"><span data-stu-id="7168f-124">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="7168f-125">Java</span><span class="sxs-lookup"><span data-stu-id="7168f-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="7168f-126">Müşterinin Şirket profilini almak için, müşteriyi tanımlamak üzere **ıaggregatepartner. getCustomers (). Byıd** işlevini Müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="7168f-126">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="7168f-127">Ardından Şirket özelliğine erişmek için [**Getprofiles**] Işlevinden müşterinin **ıcustomerprofilecollection** arabirimini alın.</span><span class="sxs-lookup"><span data-stu-id="7168f-127">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="7168f-128">Ardından **ıcustomerreadonlyprofile arabirimini ıustomerprofilecollection. getCompany** işlevinden alın ve **Get** işlevini çağırın. </span><span class="sxs-lookup"><span data-stu-id="7168f-128">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="7168f-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7168f-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7168f-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7168f-130">Request syntax</span></span>

| <span data-ttu-id="7168f-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7168f-131">Method</span></span>  | <span data-ttu-id="7168f-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7168f-132">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="7168f-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="7168f-133">**GET**</span></span> | <span data-ttu-id="7168f-134">*{BaseUrl}*/v1/Customers/{Customer-Tenant-ID}/Profiles/Company http/1.1</span><span class="sxs-lookup"><span data-stu-id="7168f-134">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7168f-135">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="7168f-135">URI parameter</span></span>

<span data-ttu-id="7168f-136">Şirket profilini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7168f-136">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="7168f-137">Ad</span><span class="sxs-lookup"><span data-stu-id="7168f-137">Name</span></span>                   | <span data-ttu-id="7168f-138">Tür</span><span class="sxs-lookup"><span data-stu-id="7168f-138">Type</span></span>     | <span data-ttu-id="7168f-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7168f-139">Required</span></span> | <span data-ttu-id="7168f-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7168f-140">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7168f-141">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="7168f-141">**customer-tenant-id**</span></span> | <span data-ttu-id="7168f-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="7168f-142">**guid**</span></span> | <span data-ttu-id="7168f-143">Y</span><span class="sxs-lookup"><span data-stu-id="7168f-143">Y</span></span>        | <span data-ttu-id="7168f-144">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="7168f-144">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7168f-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7168f-145">Request headers</span></span>

<span data-ttu-id="7168f-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7168f-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7168f-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7168f-147">Request body</span></span>

<span data-ttu-id="7168f-148">Yok</span><span class="sxs-lookup"><span data-stu-id="7168f-148">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7168f-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7168f-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="7168f-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7168f-150">REST response</span></span>

<span data-ttu-id="7168f-151">Başarılı olursa, bu yöntem yanıt gövdesinde bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="7168f-151">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7168f-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7168f-152">Response success and error codes</span></span>

<span data-ttu-id="7168f-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7168f-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7168f-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7168f-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7168f-155">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7168f-155">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7168f-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7168f-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 488
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ffa9174c-dbcb-47de-b70d-10e640a7f1b4
MS-RequestId: 0b6f039c-e4b5-4b9e-bdac-b39077bb60da
MS-CV: /e74N8OrkE29ycwZ.0
MS-ServerId: 101112202
Date: Wed, 04 Jan 2017 19:48:51 GMT

{
    "tenantId": "4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04",
    "domain": "dtdemocspcustomer005.onmicrosoft.com",
    "companyName": "DT Demo CSP Customer 005",
    "address": {
        "country": "US",
        "region": "WA",
        "city": "Redmond ",
        "addressLine1": "1 Microsoft Way",
        "postalCode": "98052",
        "phoneNumber": "4155551212"
    },
    "email": "daniel@hotmail.com.tw",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/profiles/company",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerCompanyProfile"
    }
}
```
