---
title: KIMLIĞE göre kullanılabilirliği al
description: Bir kullanılabilirlik KIMLIĞI kullanarak belirtilen ürün ve SKU için kullanılabilirliği alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c31bc12d8d484cc8042f36aa865145600d9e6738
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760207"
---
# <a name="get-the-availability-by-id"></a><span data-ttu-id="99642-103">KIMLIĞE göre kullanılabilirliği al</span><span class="sxs-lookup"><span data-stu-id="99642-103">Get the availability by ID</span></span>

<span data-ttu-id="99642-104">Bir kullanılabilirlik KIMLIĞI kullanarak belirtilen ürün ve SKU için kullanılabilirliği alır.</span><span class="sxs-lookup"><span data-stu-id="99642-104">Gets the availability for the specified product and SKU using an availability ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99642-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="99642-105">Prerequisites</span></span>

- <span data-ttu-id="99642-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="99642-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="99642-107">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="99642-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="99642-108">Bir ürün KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="99642-108">A product ID.</span></span>

- <span data-ttu-id="99642-109">SKU KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="99642-109">A SKU ID.</span></span>

- <span data-ttu-id="99642-110">Bir kullanılabilirlik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="99642-110">An availability ID.</span></span>

## <a name="c"></a><span data-ttu-id="99642-111">C\#</span><span class="sxs-lookup"><span data-stu-id="99642-111">C\#</span></span>

<span data-ttu-id="99642-112">Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak için, belirli bir [SKU 'nun](product-resources.md#sku) işlemlerine yönelik arabirimi almak üzere [bir SKU 'yu kimliğe göre Al](get-a-sku-by-id.md) ' daki adımları kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="99642-112">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="99642-113">Sonuç arabiriminden, kullanılabilirliği için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **kullanılabilirlik** özelliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="99642-113">From the resulting interface, select the **Availabilities** property to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="99642-114">Bundan sonra, söz konusu kullanılabilirliğe yönelik işlemleri almak için kullanılabilirlik KIMLIĞINI **Byıd ()** yöntemine geçirin ve ardından kullanılabilirlik ayrıntılarını almak için **Get ()** veya **GetAsync ()** öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="99642-114">After that, pass the availability ID to the **ById()** method to get the operations for that specific availability and then call **Get()** or **GetAsync()** to retrieve the availability details.</span></span>

```csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string availabilityId;

// Get the availability details.
var availability = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.ById(availabilityId).Get();
```

## <a name="java"></a><span data-ttu-id="99642-115">Java</span><span class="sxs-lookup"><span data-stu-id="99642-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="99642-116">Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak için, belirli bir [SKU 'nun](product-resources.md#sku) işlemlerine yönelik arabirimi almak üzere [bir SKU 'yu kimliğe göre Al](get-a-sku-by-id.md) ' daki adımları kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="99642-116">To get details of a specific [availability](product-resources.md#availability), start by using the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific [SKU's](product-resources.md#sku) operations.</span></span> <span data-ttu-id="99642-117">Sonuç arabiriminden, kullanılabilirlik için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **Getavailalıklara** işlevini seçin.</span><span class="sxs-lookup"><span data-stu-id="99642-117">From the resulting interface, select the **getAvailabilities** function to obtain an interface with the available operations for Availabilities.</span></span> <span data-ttu-id="99642-118">Bundan sonra, söz konusu kullanılabilirliğe yönelik işlemleri almak için kullanılabilirlik KIMLIĞINI **Byıd ()** işlevine geçirin ve ardından kullanılabilirlik ayrıntılarını almak için **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="99642-118">After that, pass the availability ID to the **byId()** function to get the operations for that specific availability and then call the **get()** function to retrieve the availability details.</span></span>

```java
IAggregatePartner partnerOperations;
String countryCode;
String productId;
String skuId;
String availabilityId;

// Get the availability details.
Availability availability = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byId(skuId).getAvailabilities().byId(availabilityId).get();
```

## <a name="powershell"></a><span data-ttu-id="99642-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="99642-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="99642-120">Belirli bir [kullanılabilirliğinin](product-resources.md#availability)ayrıntılarını almak Için, [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) ' ı yürütün ve kullanılabilirlik ayrıntılarını almak için kullanılabilirlik **kimliği**, **CountryCode**, **ProductID** ve **skuid** parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="99642-120">To get details of a specific [availability](product-resources.md#availability), execute the [**Get-PartnerProductAvailability**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductAvailability.md) and specify the **AvailabilityId**, **CountryCode**, **ProductId**, and **SkuId** parameters to retrieve the availability details.</span></span>

```powershell
Get-PartnerProductAvailability -Product $productId -SkuId $skuId -AvailabilityId $availabilityId
```

## <a name="rest-request"></a><span data-ttu-id="99642-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="99642-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="99642-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="99642-122">Request syntax</span></span>

| <span data-ttu-id="99642-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="99642-123">Method</span></span>  | <span data-ttu-id="99642-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="99642-124">Request URI</span></span> |
|---------|------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="99642-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="99642-125">**GET**</span></span> | <span data-ttu-id="99642-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKUs/{SKU-id}/availabilities/{Availability-id}? ülke = {Country-Code} http/1.1</span><span class="sxs-lookup"><span data-stu-id="99642-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities/{availability-id}?country={country-code} HTTP/1.1</span></span>         |

### <a name="uri-parameter"></a><span data-ttu-id="99642-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="99642-127">URI parameter</span></span>

<span data-ttu-id="99642-128">Bir kullanılabilirlik KIMLIĞI kullanarak belirli bir kullanılabilirliği almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="99642-128">Use the following path and query parameters to get a specific availability using an availability ID.</span></span>

| <span data-ttu-id="99642-129">Ad</span><span class="sxs-lookup"><span data-stu-id="99642-129">Name</span></span>                   | <span data-ttu-id="99642-130">Tür</span><span class="sxs-lookup"><span data-stu-id="99642-130">Type</span></span>     | <span data-ttu-id="99642-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="99642-131">Required</span></span> | <span data-ttu-id="99642-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="99642-132">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="99642-133">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="99642-133">product-id</span></span>             | <span data-ttu-id="99642-134">string</span><span class="sxs-lookup"><span data-stu-id="99642-134">string</span></span>   | <span data-ttu-id="99642-135">Yes</span><span class="sxs-lookup"><span data-stu-id="99642-135">Yes</span></span>      | <span data-ttu-id="99642-136">Ürünü tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="99642-136">A GUID formatted string that identifies the product.</span></span>            |
| <span data-ttu-id="99642-137">SKU kimliği</span><span class="sxs-lookup"><span data-stu-id="99642-137">sku-id</span></span>                 | <span data-ttu-id="99642-138">string</span><span class="sxs-lookup"><span data-stu-id="99642-138">string</span></span>   | <span data-ttu-id="99642-139">Yes</span><span class="sxs-lookup"><span data-stu-id="99642-139">Yes</span></span>      | <span data-ttu-id="99642-140">SKU 'YU tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="99642-140">A GUID formatted string that identifies the SKU.</span></span>                |
| <span data-ttu-id="99642-141">kullanılabilirlik kimliği</span><span class="sxs-lookup"><span data-stu-id="99642-141">availability-id</span></span>        | <span data-ttu-id="99642-142">string</span><span class="sxs-lookup"><span data-stu-id="99642-142">string</span></span>   | <span data-ttu-id="99642-143">Yes</span><span class="sxs-lookup"><span data-stu-id="99642-143">Yes</span></span>      | <span data-ttu-id="99642-144">Kullanılabilirliği tanımlayan bir GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="99642-144">A GUID formatted string that identifies the availability.</span></span>       |
| <span data-ttu-id="99642-145">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="99642-145">country-code</span></span>           | <span data-ttu-id="99642-146">string</span><span class="sxs-lookup"><span data-stu-id="99642-146">string</span></span>   | <span data-ttu-id="99642-147">Yes</span><span class="sxs-lookup"><span data-stu-id="99642-147">Yes</span></span>      | <span data-ttu-id="99642-148">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="99642-148">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="99642-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="99642-149">Request headers</span></span>

<span data-ttu-id="99642-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="99642-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="99642-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="99642-151">Request body</span></span>

<span data-ttu-id="99642-152">Yok.</span><span class="sxs-lookup"><span data-stu-id="99642-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="99642-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="99642-153">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="99642-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="99642-154">REST response</span></span>

<span data-ttu-id="99642-155">Başarılı olursa, yanıt gövdesi bir [kullanılabilirlik](product-resources.md#availability) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="99642-155">If successful, the response body contains an [Availability](product-resources.md#availability) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="99642-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="99642-156">Response success and error codes</span></span>

<span data-ttu-id="99642-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="99642-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="99642-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="99642-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="99642-159">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="99642-159">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="99642-160">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="99642-160">This method returns the following error codes:</span></span>

| <span data-ttu-id="99642-161">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="99642-161">HTTP Status Code</span></span>     | <span data-ttu-id="99642-162">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="99642-162">Error code</span></span>   | <span data-ttu-id="99642-163">Açıklama</span><span class="sxs-lookup"><span data-stu-id="99642-163">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="99642-164">404</span><span class="sxs-lookup"><span data-stu-id="99642-164">404</span></span>                  | <span data-ttu-id="99642-165">400013</span><span class="sxs-lookup"><span data-stu-id="99642-165">400013</span></span>       | <span data-ttu-id="99642-166">Ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="99642-166">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="99642-167">404</span><span class="sxs-lookup"><span data-stu-id="99642-167">404</span></span>                  | <span data-ttu-id="99642-168">400018</span><span class="sxs-lookup"><span data-stu-id="99642-168">400018</span></span>       | <span data-ttu-id="99642-169">SKU bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="99642-169">SKU was not found.</span></span>                                                                                        |
| <span data-ttu-id="99642-170">404</span><span class="sxs-lookup"><span data-stu-id="99642-170">404</span></span>                  | <span data-ttu-id="99642-171">400019</span><span class="sxs-lookup"><span data-stu-id="99642-171">400019</span></span>       | <span data-ttu-id="99642-172">Kullanılabilirlik bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="99642-172">Availability not found.</span></span>                                                                                   |

### <a name="response-example"></a><span data-ttu-id="99642-173">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="99642-173">Response example</span></span>

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
