---
title: Kimliğe göre bir ürün alma
description: Ürün kimliği kullanarak belirtilen ürün kaynağını alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 769a4307dc3cebdc7ebbdcf51d9f2b67a9f4b7c2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874032"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="cb5b9-103">Kimliğe göre bir ürün alma</span><span class="sxs-lookup"><span data-stu-id="cb5b9-103">Get a product by ID</span></span>

<span data-ttu-id="cb5b9-104">Ürün kimliği kullanarak belirtilen ürün kaynağını alır.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-104">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cb5b9-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cb5b9-105">Prerequisites</span></span>

- <span data-ttu-id="cb5b9-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="cb5b9-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cb5b9-107">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cb5b9-108">Ürün kimliği.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-108">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="cb5b9-109">C\#</span><span class="sxs-lookup"><span data-stu-id="cb5b9-109">C\#</span></span>

<span data-ttu-id="cb5b9-110">Kimliğine göre belirli bir ürünü bulmak için **IAggregatePartner.Products** koleksiyonu kullanın, **ByCountry()** yöntemini kullanarak ülkeyi seçin ve **ById()** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-110">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="cb5b9-111">Son olarak, ürünü **iade etmek için Get()** veya **GetAsync()** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-111">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="cb5b9-112">Java</span><span class="sxs-lookup"><span data-stu-id="cb5b9-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="cb5b9-113">Kimliğine göre belirli bir ürünü bulmak için **IAggregatePartner.getProducts** işlevinizi kullanın, **byCountry()** işlevini kullanarak ülkeyi seçin ve **byId() işlevini** çağırın.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-113">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="cb5b9-114">Son olarak, ürünü **iade etmek için get()** işlevini arayın.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-114">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="cb5b9-115">PowerShell</span><span class="sxs-lookup"><span data-stu-id="cb5b9-115">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="cb5b9-116">Kimliğine göre belirli bir ürünü bulmak için [**Get-PartnerProduct komutunu**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) yürütün ve **ProductId parametresini** belirtin.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-116">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="cb5b9-117">**CountryCode** parametresi seçeneklerdir, belirtilmezse satıcıyla ilişkilendirilmiş ülke kullanılır.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-117">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="cb5b9-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="cb5b9-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cb5b9-119">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="cb5b9-119">Request syntax</span></span>

| <span data-ttu-id="cb5b9-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="cb5b9-120">Method</span></span>  | <span data-ttu-id="cb5b9-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="cb5b9-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="cb5b9-122">**Al**</span><span class="sxs-lookup"><span data-stu-id="cb5b9-122">**GET**</span></span> | <span data-ttu-id="cb5b9-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="cb5b9-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="cb5b9-124">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="cb5b9-124">URI parameter</span></span>

<span data-ttu-id="cb5b9-125">Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-125">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="cb5b9-126">Ad</span><span class="sxs-lookup"><span data-stu-id="cb5b9-126">Name</span></span>                   | <span data-ttu-id="cb5b9-127">Tür</span><span class="sxs-lookup"><span data-stu-id="cb5b9-127">Type</span></span>     | <span data-ttu-id="cb5b9-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cb5b9-128">Required</span></span> | <span data-ttu-id="cb5b9-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb5b9-129">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="cb5b9-130">product-id</span><span class="sxs-lookup"><span data-stu-id="cb5b9-130">product-id</span></span>             | <span data-ttu-id="cb5b9-131">string</span><span class="sxs-lookup"><span data-stu-id="cb5b9-131">string</span></span>   | <span data-ttu-id="cb5b9-132">Yes</span><span class="sxs-lookup"><span data-stu-id="cb5b9-132">Yes</span></span>      | <span data-ttu-id="cb5b9-133">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-133">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="cb5b9-134">ülke</span><span class="sxs-lookup"><span data-stu-id="cb5b9-134">country</span></span>                | <span data-ttu-id="cb5b9-135">string</span><span class="sxs-lookup"><span data-stu-id="cb5b9-135">string</span></span>   | <span data-ttu-id="cb5b9-136">Yes</span><span class="sxs-lookup"><span data-stu-id="cb5b9-136">Yes</span></span>      | <span data-ttu-id="cb5b9-137">Ülke/bölge kimliği.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-137">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="cb5b9-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="cb5b9-138">Request headers</span></span>

<span data-ttu-id="cb5b9-139">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="cb5b9-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cb5b9-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="cb5b9-140">Request body</span></span>

<span data-ttu-id="cb5b9-141">Yok.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="cb5b9-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="cb5b9-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="cb5b9-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="cb5b9-143">REST response</span></span>

<span data-ttu-id="cb5b9-144">Başarılı olursa yanıt gövdesi bir Ürün [kaynağı](product-resources.md#product) içerir.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-144">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cb5b9-145">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="cb5b9-145">Response success and error codes</span></span>

<span data-ttu-id="cb5b9-146">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cb5b9-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cb5b9-148">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="cb5b9-148">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="cb5b9-149">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="cb5b9-149">This method returns the following error codes:</span></span>

| <span data-ttu-id="cb5b9-150">HTTP Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="cb5b9-150">HTTP Status Code</span></span>     | <span data-ttu-id="cb5b9-151">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="cb5b9-151">Error code</span></span>   | <span data-ttu-id="cb5b9-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cb5b9-152">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="cb5b9-153">404</span><span class="sxs-lookup"><span data-stu-id="cb5b9-153">404</span></span>                  | <span data-ttu-id="cb5b9-154">400013</span><span class="sxs-lookup"><span data-stu-id="cb5b9-154">400013</span></span>       | <span data-ttu-id="cb5b9-155">Ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="cb5b9-155">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="cb5b9-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="cb5b9-156">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Tue, 23 Jan 2018 23:13:01 GMT

{
    "id": "DZH318Z0BQ3Q",
    "title": "Virtual Machines DSv2 Series",
    "description": "Dsv2-series instances are the latest generation of D-series instances that will carry more powerful CPUs which are on average about 35% faster than D-series instances, and carry the same memory and disk configurations as the D-series. Dsv2-series instances are based on the latest generation 2.4 GHz Intel Xeon® E5-2673 v3 (Haswell) processor, and with Intel Turbo Boost Technology 2.0 can go to 3.2 GHz.",
    "productType": {
        "id": "Azure",
        "displayName": "Azure",
        "subType": {
            "id": "VirtualMachines",
            "displayName": "VirtualMachines"
        }
    },
    "isMicrosoftProduct": true,
    "publisherName": "Microsoft",
    "links": {
        "skus": {
            "uri": "/products/DZH318Z0BQ3Q/skus?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/products/DZH318Z0BQ3Q?country=US",
            "method": "GET",
            "headers": []
        }
    }
}
```
