---
title: Kimliğe göre bir ürün alma
description: Ürün KIMLIĞI kullanarak belirtilen ürün kaynağını alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 8aca626597e9ec903ebecca7d55577ba636c518e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769034"
---
# <a name="get-a-product-by-id"></a><span data-ttu-id="c367f-103">Kimliğe göre bir ürün alma</span><span class="sxs-lookup"><span data-stu-id="c367f-103">Get a product by ID</span></span>

<span data-ttu-id="c367f-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="c367f-104">**Applies To**</span></span>

- <span data-ttu-id="c367f-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c367f-105">Partner Center</span></span>

<span data-ttu-id="c367f-106">Ürün KIMLIĞI kullanarak belirtilen ürün kaynağını alır.</span><span class="sxs-lookup"><span data-stu-id="c367f-106">Gets the specified product resource using a product ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c367f-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c367f-107">Prerequisites</span></span>

- <span data-ttu-id="c367f-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c367f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c367f-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c367f-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="c367f-110">Bir ürün KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="c367f-110">A product ID.</span></span>

## <a name="c"></a><span data-ttu-id="c367f-111">C\#</span><span class="sxs-lookup"><span data-stu-id="c367f-111">C\#</span></span>

<span data-ttu-id="c367f-112">KIMLIĞE göre belirli bir ürünü bulmak için **ıaggregatepartneri. Products** koleksiyonunuzu kullanın, **bycountry ()** yöntemini kullanarak ülkeyi seçin ve ardından **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c367f-112">To find a specific product by ID, use your **IAggregatePartner.Products** collection, select the country by using the **ByCountry()** method, then call the **ById()** method.</span></span> <span data-ttu-id="c367f-113">Son olarak, ürünü döndürmek için **Get ()** veya **GetAsync ()** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="c367f-113">Finally, call the **Get()** or **GetAsync()** method to return the product.</span></span>

```csharp
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.Products.ByCountry("US").ById("DZH318Z0BQ3Q").Get();
```

## <a name="java"></a><span data-ttu-id="c367f-114">Java</span><span class="sxs-lookup"><span data-stu-id="c367f-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="c367f-115">KIMLIĞE göre belirli bir ürünü bulmak için **ıaggregatepartner. getProducts** işlevinizi kullanın, **bycountry ()** işlevini kullanarak ülkeyi seçin ve ardından **byıd ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c367f-115">To find a specific product by ID, use your **IAggregatePartner.getProducts** function, select the country by using the **byCountry()** function, then call the **byId()** function.</span></span> <span data-ttu-id="c367f-116">Son olarak, ürünü döndürmek için **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c367f-116">Finally, call the **get()** function to return the product.</span></span>

```java
// IAggregatePartner partnerOperations;

Product productDetail = partnerOperations.getProducts().byCountry("US").byId("DZH318Z0BQ3Q").get();
```

## <a name="powershell"></a><span data-ttu-id="c367f-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c367f-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="c367f-118">KIMLIĞE göre belirli bir ürünü bulmak için [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) komutunu yürütün ve **ProductID** parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="c367f-118">To find a specific product by ID, execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command and specify the **ProductId** parameter.</span></span> <span data-ttu-id="c367f-119">**CountryCode** parametresi, belirtilmemişse, satıcı ile ilişkili ülkenin kullanılacaktır.</span><span class="sxs-lookup"><span data-stu-id="c367f-119">The **CountryCode** parameter is options, if it isn't specified then the country associated with the reseller will be used.</span></span>

```powershell
Get-PartnerProduct -ProductId 'DZH318Z0BQ3Q'
```

## <a name="rest-request"></a><span data-ttu-id="c367f-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c367f-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c367f-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c367f-121">Request syntax</span></span>

| <span data-ttu-id="c367f-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c367f-122">Method</span></span>  | <span data-ttu-id="c367f-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c367f-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="c367f-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="c367f-124">**GET**</span></span> | <span data-ttu-id="c367f-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}? ülke = {Country} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c367f-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}?country={country} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="c367f-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="c367f-126">URI parameter</span></span>

<span data-ttu-id="c367f-127">Belirtilen ürünü almak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c367f-127">Use the following path parameters to get the specified product.</span></span>

| <span data-ttu-id="c367f-128">Ad</span><span class="sxs-lookup"><span data-stu-id="c367f-128">Name</span></span>                   | <span data-ttu-id="c367f-129">Tür</span><span class="sxs-lookup"><span data-stu-id="c367f-129">Type</span></span>     | <span data-ttu-id="c367f-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c367f-130">Required</span></span> | <span data-ttu-id="c367f-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c367f-131">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="c367f-132">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="c367f-132">product-id</span></span>             | <span data-ttu-id="c367f-133">string</span><span class="sxs-lookup"><span data-stu-id="c367f-133">string</span></span>   | <span data-ttu-id="c367f-134">Yes</span><span class="sxs-lookup"><span data-stu-id="c367f-134">Yes</span></span>      | <span data-ttu-id="c367f-135">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="c367f-135">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="c367f-136">ülke</span><span class="sxs-lookup"><span data-stu-id="c367f-136">country</span></span>                | <span data-ttu-id="c367f-137">string</span><span class="sxs-lookup"><span data-stu-id="c367f-137">string</span></span>   | <span data-ttu-id="c367f-138">Yes</span><span class="sxs-lookup"><span data-stu-id="c367f-138">Yes</span></span>      | <span data-ttu-id="c367f-139">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="c367f-139">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="c367f-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c367f-140">Request headers</span></span>

<span data-ttu-id="c367f-141">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c367f-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c367f-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c367f-142">Request body</span></span>

<span data-ttu-id="c367f-143">Yok.</span><span class="sxs-lookup"><span data-stu-id="c367f-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c367f-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c367f-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/{product-id}?country=US HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="c367f-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c367f-145">REST response</span></span>

<span data-ttu-id="c367f-146">Başarılı olursa, yanıt gövdesi bir [ürün](product-resources.md#product) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="c367f-146">If successful, the response body contains a [Product](product-resources.md#product) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c367f-147">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c367f-147">Response success and error codes</span></span>

<span data-ttu-id="c367f-148">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c367f-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c367f-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c367f-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c367f-150">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c367f-150">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="c367f-151">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="c367f-151">This method returns the following error codes:</span></span>

| <span data-ttu-id="c367f-152">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="c367f-152">HTTP Status Code</span></span>     | <span data-ttu-id="c367f-153">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="c367f-153">Error code</span></span>   | <span data-ttu-id="c367f-154">Description</span><span class="sxs-lookup"><span data-stu-id="c367f-154">Description</span></span>                                                                |
|----------------------|--------------|----------------------------------------------------------------------------|
| <span data-ttu-id="c367f-155">404</span><span class="sxs-lookup"><span data-stu-id="c367f-155">404</span></span>                  | <span data-ttu-id="c367f-156">400013</span><span class="sxs-lookup"><span data-stu-id="c367f-156">400013</span></span>       | <span data-ttu-id="c367f-157">Ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="c367f-157">Product was not found.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="c367f-158">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c367f-158">Response example</span></span>

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
