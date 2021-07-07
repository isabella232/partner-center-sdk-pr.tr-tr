---
title: Kimliğe göre bir SKU alma
description: Belirtilen SKU kimliğini kullanarak belirtilen ürün için bir SKU alır.
ms.date: 01/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9516a87a438a0a84a6f6069c1f9b2a2e97e90fba
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873862"
---
# <a name="get-a-sku-by-id"></a><span data-ttu-id="c4975-103">Kimliğe göre bir SKU alma</span><span class="sxs-lookup"><span data-stu-id="c4975-103">Get a SKU by ID</span></span>

<span data-ttu-id="c4975-104">Belirtilen SKU kimliğini kullanarak belirtilen ürün için bir SKU alır.</span><span class="sxs-lookup"><span data-stu-id="c4975-104">Gets a SKU for the specified product using the specified SKU ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4975-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c4975-105">Prerequisites</span></span>

- <span data-ttu-id="c4975-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="c4975-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c4975-107">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="c4975-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c4975-108">Ürün kimliği.</span><span class="sxs-lookup"><span data-stu-id="c4975-108">A product ID.</span></span>

- <span data-ttu-id="c4975-109">SKU Kimliği.</span><span class="sxs-lookup"><span data-stu-id="c4975-109">A SKU ID.</span></span>

## <a name="c"></a><span data-ttu-id="c4975-110">C\#</span><span class="sxs-lookup"><span data-stu-id="c4975-110">C\#</span></span>

<span data-ttu-id="c4975-111">Belirli bir SKU'nun ayrıntılarını almak için, [](get-a-product-by-id.md) Belirli bir ürünün işlemlerinin arabirimini almak için Kimle ürün al adımlarını izleyin.</span><span class="sxs-lookup"><span data-stu-id="c4975-111">To get the details of a specific SKU, start by following the steps in [Get a product by ID](get-a-product-by-id.md) to get the interface for a specific product's operations.</span></span> <span data-ttu-id="c4975-112">Elde edilen arabirimden **SKU'lar** özelliğini seçerek SKU'lar için kullanılabilir işlemlere sahip bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="c4975-112">From the resulting interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span> <span data-ttu-id="c4975-113">SKU Kimliğini **ById()** yöntemine iletin ve SKU ayrıntılarını almak **için Get()** veya **GetAsync()** çağrısında bulundurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4975-113">Pass the SKU ID to the **ById()** method, and call **Get()** or **GetAsync()** to retrieve the SKU details.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;

// Get the SKU details.
var sku = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Get();
```

## <a name="rest-request"></a><span data-ttu-id="c4975-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c4975-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c4975-115">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="c4975-115">Request syntax</span></span>

| <span data-ttu-id="c4975-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c4975-116">Method</span></span>  | <span data-ttu-id="c4975-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c4975-117">Request URI</span></span>                                                                                                         |
|---------|---------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c4975-118">**Al**</span><span class="sxs-lookup"><span data-stu-id="c4975-118">**GET**</span></span> | <span data-ttu-id="c4975-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="c4975-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}?country={country-code} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="c4975-120">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="c4975-120">URI parameter</span></span>

<span data-ttu-id="c4975-121">Belirtilen SKU kimliğini kullanarak belirtilen ürün için bir SKU almak üzere aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4975-121">Use the following path and query parameters to get a SKU for the specified product using the specified SKU ID.</span></span>

| <span data-ttu-id="c4975-122">Ad</span><span class="sxs-lookup"><span data-stu-id="c4975-122">Name</span></span>                   | <span data-ttu-id="c4975-123">Tür</span><span class="sxs-lookup"><span data-stu-id="c4975-123">Type</span></span>     | <span data-ttu-id="c4975-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c4975-124">Required</span></span> | <span data-ttu-id="c4975-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4975-125">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="c4975-126">product-id</span><span class="sxs-lookup"><span data-stu-id="c4975-126">product-id</span></span>             | <span data-ttu-id="c4975-127">string</span><span class="sxs-lookup"><span data-stu-id="c4975-127">string</span></span>   | <span data-ttu-id="c4975-128">Yes</span><span class="sxs-lookup"><span data-stu-id="c4975-128">Yes</span></span>      | <span data-ttu-id="c4975-129">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="c4975-129">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="c4975-130">sku-id</span><span class="sxs-lookup"><span data-stu-id="c4975-130">sku-id</span></span>                 | <span data-ttu-id="c4975-131">string</span><span class="sxs-lookup"><span data-stu-id="c4975-131">string</span></span>   | <span data-ttu-id="c4975-132">Yes</span><span class="sxs-lookup"><span data-stu-id="c4975-132">Yes</span></span>      | <span data-ttu-id="c4975-133">SKU'ları tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="c4975-133">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="c4975-134">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="c4975-134">country-code</span></span>           | <span data-ttu-id="c4975-135">string</span><span class="sxs-lookup"><span data-stu-id="c4975-135">string</span></span>   | <span data-ttu-id="c4975-136">Yes</span><span class="sxs-lookup"><span data-stu-id="c4975-136">Yes</span></span>      | <span data-ttu-id="c4975-137">Ülke/bölge kimliği.</span><span class="sxs-lookup"><span data-stu-id="c4975-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="c4975-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c4975-138">Request headers</span></span>

<span data-ttu-id="c4975-139">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="c4975-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c4975-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c4975-140">Request body</span></span>

<span data-ttu-id="c4975-141">Yok.</span><span class="sxs-lookup"><span data-stu-id="c4975-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c4975-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c4975-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c4975-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c4975-143">REST response</span></span>

<span data-ttu-id="c4975-144">Başarılı olursa yanıt gövdesi bir [SKU kaynağı](product-resources.md#sku) içerir.</span><span class="sxs-lookup"><span data-stu-id="c4975-144">If successful, the response body contains a [SKU](product-resources.md#sku) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c4975-145">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c4975-145">Response success and error codes</span></span>

<span data-ttu-id="c4975-146">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="c4975-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c4975-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4975-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c4975-148">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="c4975-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="c4975-149">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="c4975-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="c4975-150">HTTP Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="c4975-150">HTTP Status Code</span></span>     | <span data-ttu-id="c4975-151">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="c4975-151">Error code</span></span>   | <span data-ttu-id="c4975-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4975-152">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c4975-153">404</span><span class="sxs-lookup"><span data-stu-id="c4975-153">404</span></span>                  | <span data-ttu-id="c4975-154">400013</span><span class="sxs-lookup"><span data-stu-id="c4975-154">400013</span></span>       | <span data-ttu-id="c4975-155">Ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="c4975-155">Product was not found.</span></span>                                                                                    |
| <span data-ttu-id="c4975-156">404</span><span class="sxs-lookup"><span data-stu-id="c4975-156">404</span></span>                  | <span data-ttu-id="c4975-157">400018</span><span class="sxs-lookup"><span data-stu-id="c4975-157">400018</span></span>       | <span data-ttu-id="c4975-158">Sku bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="c4975-158">Sku was not found.</span></span>                                                                                        |

### <a name="response-example"></a><span data-ttu-id="c4975-159">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c4975-159">Response example</span></span>

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
