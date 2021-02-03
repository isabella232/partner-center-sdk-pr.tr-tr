---
title: Müşterinin tüm kullanıcı hesaplarının listesini alma
description: Müşterilerinizin birine ait olan tüm Kullanıcı hesaplarının listesini alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f2b1bcf9926e02232b6e2cc68b71e992b015324
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769334"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="c2af0-103">Müşterinin tüm kullanıcı hesaplarının listesini alma</span><span class="sxs-lookup"><span data-stu-id="c2af0-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="c2af0-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="c2af0-104">**Applies to:**</span></span>

- <span data-ttu-id="c2af0-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c2af0-105">Partner Center</span></span>

<span data-ttu-id="c2af0-106">Bu makalede, müşterilerinizden birine ait olan tüm Kullanıcı hesaplarının bir listesini alma açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="c2af0-106">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="c2af0-107">KIMLIĞE göre tek bir kullanıcı hesabı aramak için bkz. [kimliğe göre Kullanıcı hesabı edinme](get-a-user-account-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="c2af0-107">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2af0-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c2af0-108">Prerequisites</span></span>

- <span data-ttu-id="c2af0-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c2af0-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c2af0-110">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c2af0-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c2af0-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c2af0-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c2af0-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c2af0-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c2af0-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c2af0-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c2af0-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c2af0-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c2af0-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="c2af0-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c2af0-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="c2af0-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="c2af0-117">C\#</span><span class="sxs-lookup"><span data-stu-id="c2af0-117">C\#</span></span>

<span data-ttu-id="c2af0-118">Belirli bir müşteriye ait tüm Kullanıcı hesaplarının koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="c2af0-118">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="c2af0-119">Müşteriyi tanımlamak için belirtilen müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c2af0-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="c2af0-120">Koleksiyonu almak için [**Users. Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="c2af0-120">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="c2af0-121">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="c2af0-121">For an example, see the following:</span></span>

- <span data-ttu-id="c2af0-122">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="c2af0-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="c2af0-123">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="c2af0-123">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="c2af0-124">Sınıf: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="c2af0-124">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="c2af0-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c2af0-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c2af0-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c2af0-126">Request syntax</span></span>

| <span data-ttu-id="c2af0-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c2af0-127">Method</span></span>  | <span data-ttu-id="c2af0-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c2af0-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="c2af0-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="c2af0-129">**GET**</span></span> | <span data-ttu-id="c2af0-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="c2af0-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="c2af0-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="c2af0-131">URI parameter</span></span>

<span data-ttu-id="c2af0-132">Doğru müşteriyi tanımlamak için aşağıdaki URI parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2af0-132">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="c2af0-133">Ad</span><span class="sxs-lookup"><span data-stu-id="c2af0-133">Name</span></span>                   | <span data-ttu-id="c2af0-134">Tür</span><span class="sxs-lookup"><span data-stu-id="c2af0-134">Type</span></span>     | <span data-ttu-id="c2af0-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c2af0-135">Required</span></span> | <span data-ttu-id="c2af0-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c2af0-136">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c2af0-137">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="c2af0-137">**customer-tenant-id**</span></span> | <span data-ttu-id="c2af0-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="c2af0-138">**guid**</span></span> | <span data-ttu-id="c2af0-139">Y</span><span class="sxs-lookup"><span data-stu-id="c2af0-139">Y</span></span>        | <span data-ttu-id="c2af0-140">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="c2af0-140">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c2af0-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c2af0-141">Request headers</span></span>

<span data-ttu-id="c2af0-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c2af0-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c2af0-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c2af0-143">Request body</span></span>

<span data-ttu-id="c2af0-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="c2af0-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c2af0-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c2af0-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="c2af0-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c2af0-146">REST response</span></span>

<span data-ttu-id="c2af0-147">Başarılı olursa, bu yöntem bir müşteri için Kullanıcı hesapları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="c2af0-147">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c2af0-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c2af0-148">Response success and error codes</span></span>

<span data-ttu-id="c2af0-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c2af0-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c2af0-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2af0-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c2af0-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c2af0-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c2af0-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c2af0-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1030
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CV: 6zmKqrSFB0+t7m3y.0
MS-ServerId: 101112616
Date: Wed, 21 Dec 2016 21:13:24 GMT

 {
    "totalCount": 2,
    "items": [{
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
        }, {
            "id": "6e668259-1f09-479d-bcb8-d9b03e826b8d",
            "userPrincipalName": "admin@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Daniel",
            "lastName": "Tsai",
            "displayName": "DT Demo CSP Customer 005",
            "userDomainType": "none",
            "state": "active",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/6e668259-1f09-479d-bcb8-d9b03e826b8d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
