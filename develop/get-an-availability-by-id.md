---
title: KIMLIĞE göre kullanılabilirliği al
description: Bir kullanılabilirlik KIMLIĞI kullanarak belirtilen ürün ve SKU için kullanılabilirliği alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 824303d40e1dcb0405246c8e29562c4527d147fd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768759"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="412c1-103">KIMLIĞE göre kullanılabilirliği al</span><span class="sxs-lookup"><span data-stu-id="412c1-103">Get the availability by ID</span></span>

<span data-ttu-id="412c1-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="412c1-104">**Applies To**</span></span>

- <span data-ttu-id="412c1-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="412c1-105">Partner Center</span></span>

<span data-ttu-id="412c1-106">Bir kullanılabilirlik KIMLIĞI kullanarak belirtilen ürün ve SKU için kullanılabilirliği alır.</span><span class="sxs-lookup"><span data-stu-id="412c1-106">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="412c1-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="412c1-107">Prerequisites</span></span>

- <span data-ttu-id="412c1-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="412c1-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="412c1-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="412c1-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="412c1-110">Bir ürün KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="412c1-110">A product ID.</span></span>

- <span data-ttu-id="412c1-111">SKU KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="412c1-111">A SKU ID.</span></span>

- <span data-ttu-id="412c1-112">Bir kullanılabilirlik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="412c1-112">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="412c1-113">C\#</span><span class="sxs-lookup"><span data-stu-id="412c1-113">C\#</span></span>

<span data-ttu-id="412c1-114">Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak için, belirli bir [SKU 'nun](product-resources.md#sku) işlemlerine yönelik arabirimi almak üzere [bir SKU 'yu kimliğe göre Al](get-a-sku-by-id.md) ' daki adımları kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="412c1-114">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="412c1-115">Sonuç arabiriminden, kullanılabilirliği için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **kullanılabilirlik** özelliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="412c1-115">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="412c1-116">Bundan sonra, söz konusu kullanılabilirliğe yönelik işlemleri almak için kullanılabilirlik KIMLIĞINI **Byıd ()** yöntemine geçirin ve ardından kullanılabilirlik ayrıntılarını almak için **Get ()** veya **GetAsync ()** öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="412c1-116">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="412c1-117">Java</span><span class="sxs-lookup"><span data-stu-id="412c1-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="412c1-118">Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak için, belirli bir [SKU 'nun](product-resources.md#sku) işlemlerine yönelik arabirimi almak üzere [bir SKU 'yu kimliğe göre Al](get-a-sku-by-id.md) ' daki adımları kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="412c1-118">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="412c1-119">Sonuç arabiriminden, kullanılabilirlik için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **Getavailalıklara** işlevini seçin.</span><span class="sxs-lookup"><span data-stu-id="412c1-119">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="412c1-120">Bundan sonra, söz konusu kullanılabilirliğe yönelik işlemleri almak için kullanılabilirlik KIMLIĞINI **Byıd ()** işlevine geçirin ve ardından kullanılabilirlik ayrıntılarını almak için **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="412c1-120">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="412c1-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="412c1-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="412c1-122">Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak Için, [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) ' ı yürütün ve kullanılabilirlik ayrıntılarını almak için kullanılabilirlik **kimliği**, **CountryCode**, **ProductID** ve **skuid** parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="412c1-122">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="412c1-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="412c1-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="412c1-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="412c1-124">Request syntax</span></span>

| <span data-ttu-id="412c1-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="412c1-125">Method</span></span>  | <span data-ttu-id="412c1-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="412c1-126">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="412c1-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="412c1-127">**GET**</span></span> | <span data-ttu-id="412c1-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKUs/{SKU-id}/availabilities/{Availability-id}? ülke = {Country-Code} http/1.1</span><span class="sxs-lookup"><span data-stu-id="412c1-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="412c1-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="412c1-129">URI parameter</span></span>

<span data-ttu-id="412c1-130">Bir kullanılabilirlik KIMLIĞI kullanarak belirli bir kullanılabilirliği almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="412c1-130">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="412c1-131">Ad</span><span class="sxs-lookup"><span data-stu-id="412c1-131">Name</span></span>                   | <span data-ttu-id="412c1-132">Tür</span><span class="sxs-lookup"><span data-stu-id="412c1-132">Type</span></span>     | <span data-ttu-id="412c1-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="412c1-133">Required</span></span> | <span data-ttu-id="412c1-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="412c1-134">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="412c1-135">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="412c1-135">product-id</span></span>             | <span data-ttu-id="412c1-136">string</span><span class="sxs-lookup"><span data-stu-id="412c1-136">string</span></span>   | <span data-ttu-id="412c1-137">Yes</span><span class="sxs-lookup"><span data-stu-id="412c1-137">Yes</span></span>      | <span data-ttu-id="412c1-138">Ürünü tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="412c1-138">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="412c1-139">SKU kimliği</span><span class="sxs-lookup"><span data-stu-id="412c1-139">sku-id</span></span>                 | <span data-ttu-id="412c1-140">string</span><span class="sxs-lookup"><span data-stu-id="412c1-140">string</span></span>   | <span data-ttu-id="412c1-141">Yes</span><span class="sxs-lookup"><span data-stu-id="412c1-141">Yes</span></span>      | <span data-ttu-id="412c1-142">SKU 'YU tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="412c1-142">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="412c1-143">kullanılabilirlik kimliği</span><span class="sxs-lookup"><span data-stu-id="412c1-143">availability-id</span></span>        | <span data-ttu-id="412c1-144">string</span><span class="sxs-lookup"><span data-stu-id="412c1-144">string</span></span>   | <span data-ttu-id="412c1-145">Yes</span><span class="sxs-lookup"><span data-stu-id="412c1-145">Yes</span></span>      | <span data-ttu-id="412c1-146">Kullanılabilirliği tanımlayan bir GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="412c1-146">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="412c1-147">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="412c1-147">country-code</span></span>           | <span data-ttu-id="412c1-148">string</span><span class="sxs-lookup"><span data-stu-id="412c1-148">string</span></span>   | <span data-ttu-id="412c1-149">Yes</span><span class="sxs-lookup"><span data-stu-id="412c1-149">Yes</span></span>      | <span data-ttu-id="412c1-150">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="412c1-150">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="412c1-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="412c1-151">Request headers</span></span>

<span data-ttu-id="412c1-152">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="412c1-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="412c1-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="412c1-153">Request body</span></span>

<span data-ttu-id="412c1-154">Yok.</span><span class="sxs-lookup"><span data-stu-id="412c1-154">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="412c1-155">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="412c1-155">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="412c1-156">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="412c1-156">REST response</span></span>

<span data-ttu-id="412c1-157">Başarılı olursa, yanıt gövdesi bir [kullanılabilirlik](product-resources.md#availability) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="412c1-157">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="412c1-158">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="412c1-158">Response success and error codes</span></span>

<span data-ttu-id="412c1-159">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="412c1-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="412c1-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="412c1-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="412c1-161">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="412c1-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="412c1-162">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="412c1-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="412c1-163">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="412c1-163">HTTP Status Code</span></span>     | <span data-ttu-id="412c1-164">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="412c1-164">Error code</span></span>   | <span data-ttu-id="412c1-165">Description</span><span class="sxs-lookup"><span data-stu-id="412c1-165">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="412c1-166">404</span><span class="sxs-lookup"><span data-stu-id="412c1-166">404</span></span>                  | <span data-ttu-id="412c1-167">400013</span><span class="sxs-lookup"><span data-stu-id="412c1-167">400013</span></span>       | <span data-ttu-id="412c1-168">Ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="412c1-168">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="412c1-169">404</span><span class="sxs-lookup"><span data-stu-id="412c1-169">404</span></span>                  | <span data-ttu-id="412c1-170">400018</span><span class="sxs-lookup"><span data-stu-id="412c1-170">400018</span></span>       | <span data-ttu-id="412c1-171">SKU bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="412c1-171">Sku was not found.</span></span>                                                                                        |
| <span data-ttu-id="412c1-172">404</span><span class="sxs-lookup"><span data-stu-id="412c1-172">404</span></span>                  | <span data-ttu-id="412c1-173">400019</span><span class="sxs-lookup"><span data-stu-id="412c1-173">400019</span></span>       | <span data-ttu-id="412c1-174">Kullanılabilirlik bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="412c1-174">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="412c1-175">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="412c1-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 2e12a576-ded5-437e-a5ec-dbfbcbd1624c,2e12a576-ded5-437e-a5ec-dbfbcbd1624c
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllc1xEWkgzMThaMEhNS1E=?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:43 GMT
Content-Length: 440

{
    "id": "DZH318XZXPHL",
    "productId": "DZH318Z0BQ3Q",
    "skuId": "0001",
    "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXPHL",
    "defaultCurrency": {
        "code": "USD",
        "symbol": "$"
    },
    "segment": "commercial",
    "country": "US",
    "isPurchasable": true,
    "isRenewable": false,
    "terms": [{
        "duration": "P1Y",
        "description": "1 Year Prepaid"
    }],
    "product": { ... },
    "sku": { ... },
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318XZXPHL?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
