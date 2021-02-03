---
title: Kimliğe göre bir SKU alma
description: Belirtilen SKU KIMLIĞINI kullanarak belirtilen ürün için bir SKU alır.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 54ef72413d2d2b9e7154e82e4bbdd7427a79a2dd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769089"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="e4e3c-103">Kimliğe göre bir SKU alma</span><span class="sxs-lookup"><span data-stu-id="e4e3c-103">Get a SKU by ID</span></span>

<span data-ttu-id="e4e3c-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="e4e3c-104">**Applies To**</span></span>

- <span data-ttu-id="e4e3c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e4e3c-105">Partner Center</span></span>

<span data-ttu-id="e4e3c-106">Belirtilen SKU KIMLIĞINI kullanarak belirtilen ürün için bir SKU alır.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-106">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e4e3c-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e4e3c-107">Prerequisites</span></span>

- <span data-ttu-id="e4e3c-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e4e3c-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e4e3c-110">Bir ürün KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-110">A product ID.</span></span>

- <span data-ttu-id="e4e3c-111">SKU KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-111">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="e4e3c-112">C\#</span><span class="sxs-lookup"><span data-stu-id="e4e3c-112">C\#</span></span>

<span data-ttu-id="e4e3c-113">Belirli bir SKU 'nun ayrıntılarını almak için, belirli bir ürünün işlemlerine yönelik arabirimi almak amacıyla [kimliğe göre ürün edinme](get-a-product-by-id.md) bölümündeki adımları izleyerek işe başlayın.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-113">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="e4e3c-114">Sonuç arabiriminden, SKU 'Lar için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **SKU 'ları** özelliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-114">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="e4e3c-115">SKU KIMLIĞINI **byıd ()** yöntemine GEÇIRIN ve SKU ayrıntılarını almak için **Get ()** veya **GetAsync ()** çağırın.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-115">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="e4e3c-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e4e3c-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e4e3c-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e4e3c-117">Request syntax</span></span>

| <span data-ttu-id="e4e3c-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e4e3c-118">Method</span></span>  | <span data-ttu-id="e4e3c-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e4e3c-119">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4e3c-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="e4e3c-120">**GET**</span></span> | <span data-ttu-id="e4e3c-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKUs/{SKU-id}? ülke = {Country-Code} http/1.1</span><span class="sxs-lookup"><span data-stu-id="e4e3c-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="e4e3c-122">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="e4e3c-122">URI parameter</span></span>

<span data-ttu-id="e4e3c-123">Belirtilen SKU KIMLIĞINI kullanarak belirtilen ürün için bir SKU almak üzere aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-123">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="e4e3c-124">Ad</span><span class="sxs-lookup"><span data-stu-id="e4e3c-124">Name</span></span>                   | <span data-ttu-id="e4e3c-125">Tür</span><span class="sxs-lookup"><span data-stu-id="e4e3c-125">Type</span></span>     | <span data-ttu-id="e4e3c-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e4e3c-126">Required</span></span> | <span data-ttu-id="e4e3c-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e4e3c-127">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="e4e3c-128">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="e4e3c-128">product-id</span></span>             | <span data-ttu-id="e4e3c-129">string</span><span class="sxs-lookup"><span data-stu-id="e4e3c-129">string</span></span>   | <span data-ttu-id="e4e3c-130">Yes</span><span class="sxs-lookup"><span data-stu-id="e4e3c-130">Yes</span></span>      | <span data-ttu-id="e4e3c-131">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-131">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="e4e3c-132">SKU kimliği</span><span class="sxs-lookup"><span data-stu-id="e4e3c-132">sku-id</span></span>                 | <span data-ttu-id="e4e3c-133">string</span><span class="sxs-lookup"><span data-stu-id="e4e3c-133">string</span></span>   | <span data-ttu-id="e4e3c-134">Yes</span><span class="sxs-lookup"><span data-stu-id="e4e3c-134">Yes</span></span>      | <span data-ttu-id="e4e3c-135">SKU 'YU tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-135">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="e4e3c-136">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="e4e3c-136">country-code</span></span>           | <span data-ttu-id="e4e3c-137">string</span><span class="sxs-lookup"><span data-stu-id="e4e3c-137">string</span></span>   | <span data-ttu-id="e4e3c-138">Yes</span><span class="sxs-lookup"><span data-stu-id="e4e3c-138">Yes</span></span>      | <span data-ttu-id="e4e3c-139">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="e4e3c-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e4e3c-140">Request headers</span></span>

<span data-ttu-id="e4e3c-141">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e4e3c-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e4e3c-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e4e3c-142">Request body</span></span>

<span data-ttu-id="e4e3c-143">Yok.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e4e3c-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e4e3c-144">Request example</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3V/skus/00G1?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="e4e3c-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e4e3c-145">REST response</span></span>

<span data-ttu-id="e4e3c-146">Başarılı olursa, yanıt gövdesi bir [SKU](product-resources.md#sku) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-146">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e4e3c-147">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e4e3c-147">Response success and error codes</span></span>

<span data-ttu-id="e4e3c-148">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e4e3c-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e4e3c-150">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e4e3c-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="e4e3c-151">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="e4e3c-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="e4e3c-152">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="e4e3c-152">HTTP Status Code</span></span>     | <span data-ttu-id="e4e3c-153">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="e4e3c-153">Error code</span></span>   | <span data-ttu-id="e4e3c-154">Description</span><span class="sxs-lookup"><span data-stu-id="e4e3c-154">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e4e3c-155">404</span><span class="sxs-lookup"><span data-stu-id="e4e3c-155">404</span></span>                  | <span data-ttu-id="e4e3c-156">400013</span><span class="sxs-lookup"><span data-stu-id="e4e3c-156">400013</span></span>       | <span data-ttu-id="e4e3c-157">Ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-157">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="e4e3c-158">404</span><span class="sxs-lookup"><span data-stu-id="e4e3c-158">404</span></span>                  | <span data-ttu-id="e4e3c-159">400018</span><span class="sxs-lookup"><span data-stu-id="e4e3c-159">400018</span></span>       | <span data-ttu-id="e4e3c-160">SKU bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="e4e3c-160">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="e4e3c-161">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e4e3c-161">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 956eae17-7650-4470-94d2-4f61b9b02a23,956eae17-7650-4470-94d2-4f61b9b02a23
MS-RequestId: e0ae69a5-6322-4d7e-809d-59e02b51d71f,e0ae69a5-6322-4d7e-809d-59e02b51d71f
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNWXHNrdXNcMDBHMQ==?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 17:43:25 GMT
Content-Length: 1108

{
    "id": "00G1",
    "productId": "DZH318Z0BQ3V",
    "title": "Reserved VM Instance, Standard_D32s_v3, US West 2, 3 Years",
    "description": "Reserved Virtual Machines Instance, Standard_D32s_v3, US West 2, 3 Years",
    "minimumQuantity": 1,
    "maximumQuantity": 999999999,
    "isTrial": false,
    "supportedBillingCycles": [
        "one_time"
    ],
    "purchasePrerequisites": [
        "AzureSubscriptionRegistration",
        "InventoryCheck"
    ],
    "inventoryVariables": [
        "CustomerId",
        "AzureSubscriptionId"
    ],
    "provisioningVariables": [
        "Scope",
        "SubscriptionId"
    ],
    "dynamicAttributes": {
        "armSkuName": "Standard_D32s_v3",
        "cores": "32",
        "ram": "128",
        "skuDisplayName": "D32s v3",
        "category": "General purpose",
        "armRegionName": "westus2",
        "duration": "3Years",
        "region": "US West 2",
        "diskType": "Ssd"
    },
    "links": {
        "availabilities": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1/availabilities?country=us",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3V/skus/00G1?country=us",
            "method": "GET",
            "headers": []
        }
    }
}
```
