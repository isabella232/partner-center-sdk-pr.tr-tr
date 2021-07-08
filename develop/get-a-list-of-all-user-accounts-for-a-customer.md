---
title: Müşterinin tüm kullanıcı hesaplarının listesini alma
description: Müşterilerinizden birinin ait olduğu tüm kullanıcı hesaplarının listesini nasıl elde edersiniz?
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f3d5fcc610eae8c1bff056c1e4a9e7a74093c87d
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874576"
---
# <a name="get-a-list-of-all-user-accounts-for-a-customer"></a><span data-ttu-id="f9df3-103">Müşterinin tüm kullanıcı hesaplarının listesini alma</span><span class="sxs-lookup"><span data-stu-id="f9df3-103">Get a list of all user accounts for a customer</span></span>

<span data-ttu-id="f9df3-104">Bu makalede, müşterilerinizden birinin ait olduğu tüm kullanıcı hesaplarının listesini nasıl alasınız?</span><span class="sxs-lookup"><span data-stu-id="f9df3-104">This article describes how to get a list of all user accounts that belong to one of your customers.</span></span>

<span data-ttu-id="f9df3-105">Kimlikle tek bir kullanıcı hesabı aray için [bkz. Kimliğine göre bir kullanıcı hesabı al.](get-a-user-account-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="f9df3-105">To look up a single user account by ID, see [Get a user account by ID](get-a-user-account-by-id.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9df3-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f9df3-106">Prerequisites</span></span>

- <span data-ttu-id="f9df3-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f9df3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f9df3-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="f9df3-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f9df3-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9df3-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f9df3-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="f9df3-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f9df3-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="f9df3-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f9df3-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="f9df3-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f9df3-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="f9df3-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f9df3-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="f9df3-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f9df3-115">C\#</span><span class="sxs-lookup"><span data-stu-id="f9df3-115">C\#</span></span>

<span data-ttu-id="f9df3-116">Belirtilen bir müşteri için tüm kullanıcı hesaplarının koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="f9df3-116">To retrieve the collection of all user accounts for a specified customer:</span></span>

1. <span data-ttu-id="f9df3-117">Müşteriyi [**tanımlamak için belirtilen müşteri kimliğiyle IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="f9df3-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span>

2. <span data-ttu-id="f9df3-118">Koleksiyonu almak [**için Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) [**veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="f9df3-118">Call the [**Users.Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Get customer users collection.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Get();
```

<span data-ttu-id="f9df3-119">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="f9df3-119">For an example, see the following:</span></span>

- <span data-ttu-id="f9df3-120">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="f9df3-120">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="f9df3-121">Project: **İş Ortağı Merkezi SDK'sı Örnekleri**</span><span class="sxs-lookup"><span data-stu-id="f9df3-121">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="f9df3-122">Sınıf: **GetCustomerUserCollection.cs**</span><span class="sxs-lookup"><span data-stu-id="f9df3-122">Class: **GetCustomerUserCollection.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="f9df3-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f9df3-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f9df3-124">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="f9df3-124">Request syntax</span></span>

| <span data-ttu-id="f9df3-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f9df3-125">Method</span></span>  | <span data-ttu-id="f9df3-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f9df3-126">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f9df3-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="f9df3-127">**GET**</span></span> | <span data-ttu-id="f9df3-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f9df3-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="f9df3-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="f9df3-129">URI parameter</span></span>

<span data-ttu-id="f9df3-130">Doğru müşteriyi belirlemek için aşağıdaki URI parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9df3-130">Use the following URI parameter to identify the correct customer.</span></span>

| <span data-ttu-id="f9df3-131">Ad</span><span class="sxs-lookup"><span data-stu-id="f9df3-131">Name</span></span>                   | <span data-ttu-id="f9df3-132">Tür</span><span class="sxs-lookup"><span data-stu-id="f9df3-132">Type</span></span>     | <span data-ttu-id="f9df3-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f9df3-133">Required</span></span> | <span data-ttu-id="f9df3-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f9df3-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f9df3-135">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="f9df3-135">**customer-tenant-id**</span></span> | <span data-ttu-id="f9df3-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="f9df3-136">**guid**</span></span> | <span data-ttu-id="f9df3-137">Y</span><span class="sxs-lookup"><span data-stu-id="f9df3-137">Y</span></span>        | <span data-ttu-id="f9df3-138">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="f9df3-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f9df3-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f9df3-139">Request headers</span></span>

<span data-ttu-id="f9df3-140">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f9df3-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f9df3-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f9df3-141">Request body</span></span>

<span data-ttu-id="f9df3-142">Yok.</span><span class="sxs-lookup"><span data-stu-id="f9df3-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f9df3-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f9df3-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5d845377-5b7d-4cd4-98f6-19e5ae3faa81
MS-CorrelationId: 5a3d64d4-4490-4932-bf5e-0dc9a58f27ca
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f9df3-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f9df3-144">REST response</span></span>

<span data-ttu-id="f9df3-145">Başarılı olursa, bu yöntem müşteri için bir kullanıcı hesabı koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="f9df3-145">If successful, this method returns a collection of user accounts for a customer.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f9df3-146">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f9df3-146">Response success and error codes</span></span>

<span data-ttu-id="f9df3-147">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="f9df3-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f9df3-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9df3-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f9df3-149">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f9df3-149">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f9df3-150">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f9df3-150">Response example</span></span>

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
