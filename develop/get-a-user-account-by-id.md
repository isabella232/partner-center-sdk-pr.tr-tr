---
title: Kimliğe göre bir kullanıcı hesabı alma
description: Müşteri için belirli bir kullanıcı hesabı alın.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: a2f42001365324a65376318cb1f2d57dc123df0c
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769269"
---
# <a name="get-a-user-account-by-id"></a><span data-ttu-id="07154-103">Kimliğe göre bir kullanıcı hesabı alma</span><span class="sxs-lookup"><span data-stu-id="07154-103">Get a user account by ID</span></span>

<span data-ttu-id="07154-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="07154-104">**Applies To**</span></span>

- <span data-ttu-id="07154-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="07154-105">Partner Center</span></span>

<span data-ttu-id="07154-106">Müşteri için belirli bir kullanıcı hesabı alın.</span><span class="sxs-lookup"><span data-stu-id="07154-106">Get a specific user account for a customer.</span></span>

- <span data-ttu-id="07154-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="07154-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="07154-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="07154-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="07154-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="07154-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="07154-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="07154-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="07154-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="07154-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="07154-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="07154-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="07154-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="07154-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="07154-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="07154-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="07154-115">C\#</span><span class="sxs-lookup"><span data-stu-id="07154-115">C\#</span></span>

<span data-ttu-id="07154-116">Müşterinin Kullanıcı hesabını almak için müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="07154-116">To retrieve a user account for a customer, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="07154-117">Ardından, belirli kullanıcıyı almak için [**Users. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="07154-117">Next, call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to retrieve the specific user.</span></span> <span data-ttu-id="07154-118">Son olarak, Kullanıcı hesabını almak için [**Users. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="07154-118">Finally, call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the user account.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

// Get customer user detail.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Get();
```

<span data-ttu-id="07154-119">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="07154-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="07154-120">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetCustomerUserDetails.cs</span><span class="sxs-lookup"><span data-stu-id="07154-120">**Project**: Partner Center SDK Samples **Class**: GetCustomerUserDetails.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="07154-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="07154-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="07154-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="07154-122">Request syntax</span></span>

| <span data-ttu-id="07154-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="07154-123">Method</span></span>  | <span data-ttu-id="07154-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="07154-124">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="07154-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="07154-125">**GET**</span></span> | <span data-ttu-id="07154-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="07154-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="07154-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="07154-127">URI parameter</span></span>

<span data-ttu-id="07154-128">Doğru müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki URI parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="07154-128">Use the following URI parameters to identify the correct customer and user.</span></span>

| <span data-ttu-id="07154-129">Ad</span><span class="sxs-lookup"><span data-stu-id="07154-129">Name</span></span>                   | <span data-ttu-id="07154-130">Tür</span><span class="sxs-lookup"><span data-stu-id="07154-130">Type</span></span>     | <span data-ttu-id="07154-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="07154-131">Required</span></span> | <span data-ttu-id="07154-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="07154-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="07154-133">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="07154-133">**customer-tenant-id**</span></span> | <span data-ttu-id="07154-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="07154-134">**guid**</span></span> | <span data-ttu-id="07154-135">Y</span><span class="sxs-lookup"><span data-stu-id="07154-135">Y</span></span>        | <span data-ttu-id="07154-136">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="07154-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="07154-137">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="07154-137">**user-id**</span></span>            | <span data-ttu-id="07154-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="07154-138">**guid**</span></span> | <span data-ttu-id="07154-139">Y</span><span class="sxs-lookup"><span data-stu-id="07154-139">Y</span></span>        | <span data-ttu-id="07154-140">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="07154-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="07154-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="07154-141">Request headers</span></span>

<span data-ttu-id="07154-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="07154-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="07154-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="07154-143">Request body</span></span>

<span data-ttu-id="07154-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="07154-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="07154-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="07154-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="07154-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="07154-146">REST response</span></span>

<span data-ttu-id="07154-147">Başarılı olursa, bu yöntem müşterinin Kullanıcı hesabını döndürür.</span><span class="sxs-lookup"><span data-stu-id="07154-147">If successful, this method returns the user account for the customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="07154-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="07154-148">Response success and error codes</span></span>

<span data-ttu-id="07154-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="07154-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="07154-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="07154-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="07154-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="07154-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="07154-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="07154-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 432
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 24a631eb-a110-49dc-8325-99d4b196774c
MS-RequestId: c1f673cb-655c-45a7-8a6b-257a0a006f4b
MS-CV: uWM1EGU7+0aI2MvV.0
MS-ServerId: 020021921
Date: Wed, 21 Dec 2016 22:59:10 GMT

{
    "usageLocation": "US",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Daniel",
    "lastName": "Tsai",
    "displayName": "Daniel Tsai",
    "userDomainType": "none",
    "state": "active",
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a9ef48bb-8758-4590-a312-d4a47bfaded4",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "CustomerUser"
    }
}
```
