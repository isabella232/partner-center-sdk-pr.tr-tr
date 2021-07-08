---
title: Müşterinin şirket profilini alma
description: Müşterinin Şirket profilini alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: a1c0c8401207f4b0bb33755a8eabc66de0ad9ff9
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874984"
---
# <a name="get-a-customers-company-profile"></a><span data-ttu-id="24027-103">Müşterinin şirket profilini alma</span><span class="sxs-lookup"><span data-stu-id="24027-103">Get a customer's company profile</span></span>

<span data-ttu-id="24027-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="24027-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="24027-105">Müşterinin Şirket profilini alır.</span><span class="sxs-lookup"><span data-stu-id="24027-105">Gets the company profile of a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="24027-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="24027-106">Prerequisites</span></span>

- <span data-ttu-id="24027-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="24027-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="24027-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="24027-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="24027-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="24027-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="24027-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="24027-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="24027-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="24027-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="24027-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="24027-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="24027-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="24027-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="24027-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="24027-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="24027-115">C\#</span><span class="sxs-lookup"><span data-stu-id="24027-115">C\#</span></span>

<span data-ttu-id="24027-116">Müşterinin Şirket profilini almak için müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="24027-116">To get the company profile for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="24027-117">Ardından, şirket özelliğine erişebilmek için, [**profiller**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) özelliğinden müşterinin [**ıcustomerprofilecollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) arabirimini alın.</span><span class="sxs-lookup"><span data-stu-id="24027-117">Then get the customer's [**ICustomerProfileCollection**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection) interface from the [**Profiles**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.profiles) property, in order to access its Company property.</span></span> <span data-ttu-id="24027-118">Daha sonra [**ıcustomerreadonlyprofile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) arabirimini [**ıustomerprofilecollection. Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) özelliğinden alın ve [**Get ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="24027-118">Next, get the [**ICustomerReadonlyProfile**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1) interface from the [**ICustomerProfileCollection.Company**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerprofilecollection.company) property, and call its [**Get()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.profiles.icustomerreadonlyprofile-1.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var companyProfile = partnerOperations.Customers.ById(customerId).Profiles.Company.Get();
```

<span data-ttu-id="24027-119">**Örnek**: [iş ortağı Merkezi SDK 'sını indirin](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span><span class="sxs-lookup"><span data-stu-id="24027-119">**Sample**: [Download the Partner Center SDK](https://go.microsoft.com/fwlink/p/?LinkId=746681).</span></span> <span data-ttu-id="24027-120">**Project**: partnersdk. featuresamples **sınıfı**: getcustomercompanyprofile. cs</span><span class="sxs-lookup"><span data-stu-id="24027-120">**Project**: PartnerSdk.FeatureSamples **Class**: GetCustomerCompanyProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="24027-121">Java</span><span class="sxs-lookup"><span data-stu-id="24027-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="24027-122">Müşterinin Şirket profilini almak için, müşteriyi tanımlamak üzere **ıaggregatepartner. getCustomers (). Byıd** işlevini Müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="24027-122">To get the company profile for a customer, call the **IAggregatePartner.getCustomers().byId** function with the customer identifier to identify the customer.</span></span> <span data-ttu-id="24027-123">Ardından Şirket özelliğine erişmek için [**Getprofiles**] Işlevinden müşterinin **ıcustomerprofilecollection** arabirimini alın.</span><span class="sxs-lookup"><span data-stu-id="24027-123">Then get the customer's **ICustomerProfileCollection** interface from the [**getProfiles**] function, in order to access its Company property.</span></span> <span data-ttu-id="24027-124">Ardından **ıcustomerreadonlyprofile arabirimini ıustomerprofilecollection. getCompany** işlevinden alın ve **Get** işlevini çağırın. </span><span class="sxs-lookup"><span data-stu-id="24027-124">Next, get the **ICustomerReadonlyProfile** interface from the **ICustomerProfileCollection.getCompany** function, and call the **get** function.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;

CustomerCompanyProfile companyProfile = partnerOperations.getCustomers().byId(customerId).getProfiles().getCompany().get();
```

## <a name="rest-request"></a><span data-ttu-id="24027-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="24027-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="24027-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="24027-126">Request syntax</span></span>

| <span data-ttu-id="24027-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="24027-127">Method</span></span>  | <span data-ttu-id="24027-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="24027-128">Request URI</span></span>                                                             |
|---------|-------------------------------------------------------------------------|
| <span data-ttu-id="24027-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="24027-129">**GET**</span></span> | <span data-ttu-id="24027-130">*{BaseUrl}*/v1/Customers/{Customer-Tenant-ID}/Profiles/Company http/1.1</span><span class="sxs-lookup"><span data-stu-id="24027-130">*{baseURL}*/v1/customers/{customer-tenant-id}/profiles/company HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="24027-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="24027-131">URI parameter</span></span>

<span data-ttu-id="24027-132">Şirket profilini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="24027-132">Use the following query parameter to get the company profile.</span></span>

| <span data-ttu-id="24027-133">Ad</span><span class="sxs-lookup"><span data-stu-id="24027-133">Name</span></span>                   | <span data-ttu-id="24027-134">Tür</span><span class="sxs-lookup"><span data-stu-id="24027-134">Type</span></span>     | <span data-ttu-id="24027-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="24027-135">Required</span></span> | <span data-ttu-id="24027-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="24027-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="24027-137">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="24027-137">**customer-tenant-id**</span></span> | <span data-ttu-id="24027-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="24027-138">**guid**</span></span> | <span data-ttu-id="24027-139">Y</span><span class="sxs-lookup"><span data-stu-id="24027-139">Y</span></span>        | <span data-ttu-id="24027-140">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="24027-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="24027-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="24027-141">Request headers</span></span>

<span data-ttu-id="24027-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="24027-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="24027-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="24027-143">Request body</span></span>

<span data-ttu-id="24027-144">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="24027-144">None</span></span>

### <a name="request-example"></a><span data-ttu-id="24027-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="24027-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="24027-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="24027-146">REST response</span></span>

<span data-ttu-id="24027-147">Başarılı olursa, bu yöntem yanıt gövdesinde bilgi döndürür.</span><span class="sxs-lookup"><span data-stu-id="24027-147">If successful, this method returns information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="24027-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="24027-148">Response success and error codes</span></span>

<span data-ttu-id="24027-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="24027-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="24027-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="24027-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="24027-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="24027-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="24027-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="24027-152">Response example</span></span>

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
