---
title: Bir ürüne ait SKU’ların listesini alma (ülkeye göre)
description: Iş Ortağı Merkezi API 'Lerini kullanarak bir ürün için ülkeye göre STB koleksiyonu alabilir ve filtreleyebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 9d5ec9172ed92d33e6ff291eafd523cbc13bfbbd
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769094"
---
# <a name="get-a-list-of-skus-for-a-product-by-country"></a><span data-ttu-id="a1458-103">Bir ürüne ait SKU’ların listesini alma (ülkeye göre)</span><span class="sxs-lookup"><span data-stu-id="a1458-103">Get a list of SKUs for a product (by country)</span></span>

<span data-ttu-id="a1458-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="a1458-104">**Applies to:**</span></span>

- <span data-ttu-id="a1458-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a1458-105">Partner Center</span></span>

<span data-ttu-id="a1458-106">Iş Ortağı Merkezi API 'Lerini kullanarak belirli bir ürün için bir ülkede bulunan SKU 'ların bir koleksiyonunu edinebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1458-106">You can get a collection of SKUs available in a country for a specific product using Partner Center APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a1458-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a1458-107">Prerequisites</span></span>

- <span data-ttu-id="a1458-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a1458-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a1458-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="a1458-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a1458-110">Bir ürün tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a1458-110">A product identifier.</span></span>

## <a name="c"></a><span data-ttu-id="a1458-111">C\#</span><span class="sxs-lookup"><span data-stu-id="a1458-111">C\#</span></span>

<span data-ttu-id="a1458-112">Bir ürüne ait SKU 'ların listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="a1458-112">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="a1458-113">[Kimliğe göre ürün edinme](get-a-product-by-id.md)bölümündeki adımları izleyerek belirli bir ürünün işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="a1458-113">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="a1458-114">Arabirimde, SKU 'Lar için kullanılabilir işlemleri içeren bir arabirim elde etmek üzere **SKU 'ları** özelliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="a1458-114">From the interface, select the **Skus** property to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="a1458-115">Ürün için kullanılabilir SKU 'ların bir koleksiyonunu almak için **Get ()** veya **GetAsync ()** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="a1458-115">Call the **Get()** or **GetAsync()** method to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="a1458-116">Seçim **Byrezervationscope ()** yöntemini kullanarak ayırma kapsamını seçin.</span><span class="sxs-lookup"><span data-stu-id="a1458-116">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

5. <span data-ttu-id="a1458-117">Seçim **Get ()** veya **GetAsync ()** çağrısı yapmadan önce SKU 'ları hedef kesimine göre filtrelemek için **bytargetsegment ()** yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1458-117">(Optional) Use the **ByTargetSegment()** method to filter the SKUs by target segment before calling **Get()** or **GetAsync()**.</span></span>

``` csharp
IAggregatePartner partnerOperations;

string countryCode;
string productId;
string productIdForAzureReservation;
string targetSegment;

// Get the available SKUs.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.Get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ByTargetSegment(targetSegment).Get();

// Get the skus for an Azure reservation product which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.Get();

// Get the skus for an Azure reservation product which are applicable to Azure plans only.
var skus = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="a1458-118">Java</span><span class="sxs-lookup"><span data-stu-id="a1458-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a1458-119">Bir ürüne ait SKU 'ların listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="a1458-119">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="a1458-120">[Kimliğe göre ürün edinme](get-a-product-by-id.md)bölümündeki adımları izleyerek belirli bir ürünün işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="a1458-120">Get an interface for a specific product's operations by following the steps in [Get a product by ID](get-a-product-by-id.md).</span></span>

2. <span data-ttu-id="a1458-121">Arabirimde, SKU 'Lar için kullanılabilir işlemleri içeren bir arabirim edinmek üzere **GetSku 'ları** işlevini seçin.</span><span class="sxs-lookup"><span data-stu-id="a1458-121">From the interface, select the **getSkus** function to obtain an interface with the available operations for SKUs.</span></span>

3. <span data-ttu-id="a1458-122">Ürün için kullanılabilir SKU 'ların bir koleksiyonunu almak için **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a1458-122">Call the **get()** function to retrieve a collection of the available SKUs for the product.</span></span>

4. <span data-ttu-id="a1458-123">Seçim **Get ()** işlevini çağırmadan önce STB 'leri hedef kesimine göre filtrelemek Için **bytargetsegment ()** işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1458-123">(Optional) Use the **byTargetSegment()** function to filter the SKUs by target segment before calling the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

// String countryCode;
// String productId;
// String targetSegment;

// Get the available SKUs.
ResourceCollection<Sku> skus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().get();

// Get the available SKUs, filtered by target segment.
var segmentSkus = partnerOperations.getProducts().byCountry(countryCode).byId(productId).getSkus().byTargetSegment(targetSegment).get();
```

## <a name="powershell"></a><span data-ttu-id="a1458-124">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1458-124">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a1458-125">Bir ürüne ait SKU 'ların listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="a1458-125">To get the list of SKUs for a product:</span></span>

1. <span data-ttu-id="a1458-126">[**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="a1458-126">Execute the [**Get-PartnerProductSku**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProductSku.md) command.</span></span>

2. <span data-ttu-id="a1458-127">Seçim SKU 'Ları hedef kesimine göre filtrelemek için **segment** parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1458-127">(Optional) Specify the **Segment** parameter to filter the SKUs by target segment.</span></span>

```powershell
# $productId
# $targetSegment

# Get the available SKUs.
Get-PartnerProductSku -ProductId $productId

# Get the available SKUs, filtered by target segment.
Get-PartnerProductSku -ProductId $productId -Segment $targetSegment
```

## <a name="rest-request"></a><span data-ttu-id="a1458-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a1458-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a1458-129">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a1458-129">Request syntax</span></span>

| <span data-ttu-id="a1458-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a1458-130">Method</span></span>  | <span data-ttu-id="a1458-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a1458-131">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a1458-132">**Al**</span><span class="sxs-lookup"><span data-stu-id="a1458-132">**GET**</span></span> | <span data-ttu-id="a1458-133">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKU 'ları? ülke = {Country-code} &targetsegment = {Target-segment} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a1458-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="a1458-134">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a1458-134">URI parameters</span></span>

<span data-ttu-id="a1458-135">Bir ürüne yönelik SKU 'ların listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1458-135">Use the following path and query parameters to get a list of SKUs for a product.</span></span>

| <span data-ttu-id="a1458-136">Ad</span><span class="sxs-lookup"><span data-stu-id="a1458-136">Name</span></span>                   | <span data-ttu-id="a1458-137">Tür</span><span class="sxs-lookup"><span data-stu-id="a1458-137">Type</span></span>     | <span data-ttu-id="a1458-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a1458-138">Required</span></span> | <span data-ttu-id="a1458-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a1458-139">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="a1458-140">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="a1458-140">product-id</span></span>             | <span data-ttu-id="a1458-141">string</span><span class="sxs-lookup"><span data-stu-id="a1458-141">string</span></span>   | <span data-ttu-id="a1458-142">Yes</span><span class="sxs-lookup"><span data-stu-id="a1458-142">Yes</span></span>      | <span data-ttu-id="a1458-143">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="a1458-143">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="a1458-144">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="a1458-144">country-code</span></span>           | <span data-ttu-id="a1458-145">string</span><span class="sxs-lookup"><span data-stu-id="a1458-145">string</span></span>   | <span data-ttu-id="a1458-146">Yes</span><span class="sxs-lookup"><span data-stu-id="a1458-146">Yes</span></span>      | <span data-ttu-id="a1458-147">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="a1458-147">A country/region ID.</span></span>                                            |
| <span data-ttu-id="a1458-148">hedef segment</span><span class="sxs-lookup"><span data-stu-id="a1458-148">target-segment</span></span>         | <span data-ttu-id="a1458-149">dize</span><span class="sxs-lookup"><span data-stu-id="a1458-149">string</span></span>   | <span data-ttu-id="a1458-150">No</span><span class="sxs-lookup"><span data-stu-id="a1458-150">No</span></span>       | <span data-ttu-id="a1458-151">Filtreleme için kullanılan hedef segmenti tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="a1458-151">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="a1458-152">Rezervationscope</span><span class="sxs-lookup"><span data-stu-id="a1458-152">reservationScope</span></span> | <span data-ttu-id="a1458-153">dize</span><span class="sxs-lookup"><span data-stu-id="a1458-153">string</span></span>   | <span data-ttu-id="a1458-154">No</span><span class="sxs-lookup"><span data-stu-id="a1458-154">No</span></span> | <span data-ttu-id="a1458-155">Bir Azure rezervasyon ürününe yönelik SKU 'ların listesini sorgularken, `reservationScope=AzurePlan` Azuplanlama için geçerli olan SKU 'ların listesini almak için belirtin.</span><span class="sxs-lookup"><span data-stu-id="a1458-155">When querying for a list of SKUs for an Azure Reservation product, specify `reservationScope=AzurePlan` to get a list of SKUs which are applicable to AzurePlan.</span></span> <span data-ttu-id="a1458-156">Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan bir Azure ayırma ürününe yönelik SKU 'ların listesini almak için bu parametreyi dışlayın.</span><span class="sxs-lookup"><span data-stu-id="a1458-156">Exclude this parameter to get a list of SKUs for an Azure Reservation products which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="a1458-157">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a1458-157">Request headers</span></span>

<span data-ttu-id="a1458-158">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a1458-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a1458-159">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a1458-159">Request body</span></span>

<span data-ttu-id="a1458-160">Yok.</span><span class="sxs-lookup"><span data-stu-id="a1458-160">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="a1458-161">İstek örnekleri</span><span class="sxs-lookup"><span data-stu-id="a1458-161">Request examples</span></span>

<span data-ttu-id="a1458-162">Belirli bir ürün için SKU 'ların listesini alın:</span><span class="sxs-lookup"><span data-stu-id="a1458-162">Get a list of SKUs for a given product:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BPS6/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="a1458-163">Bir Azure rezervasyon ürününe ait SKU 'ların listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a1458-163">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="a1458-164">Yalnızca Azure planlarına uygulanabilen ve Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan SKU 'Ları dahil edin:</span><span class="sxs-lookup"><span data-stu-id="a1458-164">Only include the SKUs which are applicable to Azure plans and not Microsoft Azure (MS-AZR-0145P) subscriptions:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

<span data-ttu-id="a1458-165">Bir Azure rezervasyon ürününe ait SKU 'ların listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a1458-165">Get a list of SKUs for an Azure Reservation product.</span></span> <span data-ttu-id="a1458-166">Yalnızca Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan SKU 'Ları (Azure planlarına değil) dahil edin:</span><span class="sxs-lookup"><span data-stu-id="a1458-166">Only include the SKUs which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions and not Azure plans:</span></span>

```http
GET http://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ5S/skus?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51
```

## <a name="rest-response"></a><span data-ttu-id="a1458-167">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a1458-167">REST response</span></span>

<span data-ttu-id="a1458-168">Başarılı olursa, yanıt gövdesi bir [SKU](product-resources.md#sku) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="a1458-168">If successful, the response body contains a collection of [SKU](product-resources.md#sku) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a1458-169">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a1458-169">Response success and error codes</span></span>

<span data-ttu-id="a1458-170">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a1458-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a1458-171">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1458-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a1458-172">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a1458-172">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="a1458-173">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="a1458-173">This method returns the following error codes:</span></span>

| <span data-ttu-id="a1458-174">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="a1458-174">HTTP Status Code</span></span>     | <span data-ttu-id="a1458-175">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="a1458-175">Error code</span></span>   | <span data-ttu-id="a1458-176">Description</span><span class="sxs-lookup"><span data-stu-id="a1458-176">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a1458-177">403</span><span class="sxs-lookup"><span data-stu-id="a1458-177">403</span></span>                  | <span data-ttu-id="a1458-178">400030</span><span class="sxs-lookup"><span data-stu-id="a1458-178">400030</span></span>       | <span data-ttu-id="a1458-179">İstenen targetSegment erişimine izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="a1458-179">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="a1458-180">404</span><span class="sxs-lookup"><span data-stu-id="a1458-180">404</span></span>                  | <span data-ttu-id="a1458-181">400013</span><span class="sxs-lookup"><span data-stu-id="a1458-181">400013</span></span>       | <span data-ttu-id="a1458-182">Üst ürün bulunamadı.</span><span class="sxs-lookup"><span data-stu-id="a1458-182">The parent product was not found.</span></span>                                                                         |

### <a name="response-example"></a><span data-ttu-id="a1458-183">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a1458-183">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: e75c1060-852e-4b49-92b0-cd15167a0d51,e75c1060-852e-4b49-92b0-cd15167a0d51
MS-RequestId: 18b41adf-29b5-48eb-b14f-c9683a4e5b7d,18b41adf-29b5-48eb-b14f-c9683a4e5b7d
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTVTXHNrdXM=?=
X-Powered-By: ASP.NET
Date: Thu, 15 Mar 2018 21:06:03 GMT
Content-Length: 50917

{
    "totalCount": 40,
    "items": [
        {
            "id": "0001",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND12s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND12s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND12s",
                "cores": "12",
                "ram": "224",
                "skuDisplayName": "ND12",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0002",
            "productId": "DZH318Z0BQ5S",
            "title": "Reserved VM Instance, Standard_ND6s, US West 2, 1 Year",
            "description": "Reserved Virtual Machines Instance, Standard_ND6s, US West 2, 1 Year",
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
            "provisioningVariables": [
                "Scope",
                "SubscriptionId"
            ],
            "dynamicAttributes": {
                "armSkuName": "Standard_ND6s",
                "cores": "6",
                "ram": "112",
                "skuDisplayName": "ND6",
                "category": "GPU",
                "armRegionName": "westus2",
                "duration": "1Year",
                "region": "US West 2",
                "diskType": "Hdd"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002/availabilities?country=US",
                    "method": "GET",
                    "headers": []
                },
            "self": {
                    "uri": "/products/DZH318Z0BQ5S/skus/0002?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
        [...]
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ5S/skus?country=US",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
