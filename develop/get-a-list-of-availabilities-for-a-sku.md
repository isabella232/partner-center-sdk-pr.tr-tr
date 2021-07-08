---
title: Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma
description: Müşteri ülkesi tarafından belirtilen ürün ve SKU için kullanılabilirlik koleksiyonunu elde etmek.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b29c005e74ad8a4da547a888b78e4599e74ebd02
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874542"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="96e64-103">Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma</span><span class="sxs-lookup"><span data-stu-id="96e64-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="96e64-104">Bu makalede belirli bir ülkede belirli bir ürün ve SKU için bir kullanılabilirlik koleksiyonunun nasıl elde edildikleri açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="96e64-104">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96e64-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="96e64-105">Prerequisites</span></span>

- <span data-ttu-id="96e64-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="96e64-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="96e64-107">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="96e64-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="96e64-108">Ürün tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="96e64-108">A product identifier.</span></span>

- <span data-ttu-id="96e64-109">SKU tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="96e64-109">A SKU identifier.</span></span>

- <span data-ttu-id="96e64-110">Ülke.</span><span class="sxs-lookup"><span data-stu-id="96e64-110">A country.</span></span>

## <a name="c"></a><span data-ttu-id="96e64-111">C\#</span><span class="sxs-lookup"><span data-stu-id="96e64-111">C\#</span></span>

<span data-ttu-id="96e64-112">[Bir SKU'nun](product-resources.md#sku) [kullanılabilirlik](product-resources.md#availability) listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="96e64-112">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="96e64-113">Belirli bir [SKU'nun işlemlerinin arabirimini](get-a-sku-by-id.md) almak için Kimle SKU al'daki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e64-113">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="96e64-114">SKU arabiriminden Kullanılabilirlik **işlemleriyle bir** arabirim elde etmek için Kullanılabilirlik özelliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="96e64-114">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="96e64-115">(İsteğe bağlı) **Kullanılabilirlikleri hedef segmente göre filtrelemek için ByTargetSegment()** yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e64-115">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="96e64-116">Bu SKU'nun kullanılabilirlik koleksiyonunu almak için **Get()** veya **GetAsync()** çağrısında bulundurabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e64-116">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string countryCode;
string productId;
string skuId;
string targetSegment;
string productIdForAzureReservation;
string skuIdForAzureReservation;

// Get the availabilities.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.Get();

// Get the availabilities, filtered by target segment.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productId).Skus.ById(skuId).Availabilities.BySegment(targetSegment).Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.ByReservationScope("AzurePlan").Get();

// Get the availabilities for an Azure reservation product and sku which are applicable to Azure plans only.
var availabilities = partnerOperations.Products.ByCountry(countryCode).ById(productIdForAzureReservation).Skus.ById(skuIdForAzureReservation).Availabilities.Get();

```

## <a name="rest-request"></a><span data-ttu-id="96e64-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="96e64-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="96e64-118">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="96e64-118">Request syntax</span></span>

| <span data-ttu-id="96e64-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="96e64-119">Method</span></span>  | <span data-ttu-id="96e64-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="96e64-120">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="96e64-121">**Al**</span><span class="sxs-lookup"><span data-stu-id="96e64-121">**GET**</span></span> | <span data-ttu-id="96e64-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="96e64-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="96e64-123">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="96e64-123">URI parameters</span></span>

<span data-ttu-id="96e64-124">Bir SKU'nun kullanılabilirlik listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e64-124">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="96e64-125">Ad</span><span class="sxs-lookup"><span data-stu-id="96e64-125">Name</span></span>                   | <span data-ttu-id="96e64-126">Tür</span><span class="sxs-lookup"><span data-stu-id="96e64-126">Type</span></span>     | <span data-ttu-id="96e64-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96e64-127">Required</span></span> | <span data-ttu-id="96e64-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96e64-128">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="96e64-129">product-id</span><span class="sxs-lookup"><span data-stu-id="96e64-129">product-id</span></span>             | <span data-ttu-id="96e64-130">string</span><span class="sxs-lookup"><span data-stu-id="96e64-130">string</span></span>   | <span data-ttu-id="96e64-131">Yes</span><span class="sxs-lookup"><span data-stu-id="96e64-131">Yes</span></span>      | <span data-ttu-id="96e64-132">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="96e64-132">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="96e64-133">sku-id</span><span class="sxs-lookup"><span data-stu-id="96e64-133">sku-id</span></span>                 | <span data-ttu-id="96e64-134">string</span><span class="sxs-lookup"><span data-stu-id="96e64-134">string</span></span>   | <span data-ttu-id="96e64-135">Yes</span><span class="sxs-lookup"><span data-stu-id="96e64-135">Yes</span></span>      | <span data-ttu-id="96e64-136">SKU'ları tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="96e64-136">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="96e64-137">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="96e64-137">country-code</span></span>           | <span data-ttu-id="96e64-138">string</span><span class="sxs-lookup"><span data-stu-id="96e64-138">string</span></span>   | <span data-ttu-id="96e64-139">Yes</span><span class="sxs-lookup"><span data-stu-id="96e64-139">Yes</span></span>      | <span data-ttu-id="96e64-140">Ülke/bölge kimliği.</span><span class="sxs-lookup"><span data-stu-id="96e64-140">A country/region ID.</span></span>                                            |
| <span data-ttu-id="96e64-141">hedef segment</span><span class="sxs-lookup"><span data-stu-id="96e64-141">target-segment</span></span>         | <span data-ttu-id="96e64-142">dize</span><span class="sxs-lookup"><span data-stu-id="96e64-142">string</span></span>   | <span data-ttu-id="96e64-143">No</span><span class="sxs-lookup"><span data-stu-id="96e64-143">No</span></span>       | <span data-ttu-id="96e64-144">Filtreleme için kullanılan hedef segmenti tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="96e64-144">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="96e64-145">reservationScope</span><span class="sxs-lookup"><span data-stu-id="96e64-145">reservationScope</span></span> | <span data-ttu-id="96e64-146">dize</span><span class="sxs-lookup"><span data-stu-id="96e64-146">string</span></span>   | <span data-ttu-id="96e64-147">No</span><span class="sxs-lookup"><span data-stu-id="96e64-147">No</span></span> | <span data-ttu-id="96e64-148">Azure Rezervasyon SKU'sunuz için kullanılabilirlik listesini sorgularken, AzurePlan için geçerli olan kullanılabilirliklerin listesini `reservationScope=AzurePlan` almak için belirtin.</span><span class="sxs-lookup"><span data-stu-id="96e64-148">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities that are applicable to AzurePlan.</span></span> <span data-ttu-id="96e64-149">Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli kullanılabilirliklerin listesini almak için bu parametreyi hariç tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96e64-149">Exclude this parameter to get a list of availabilities that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="96e64-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="96e64-150">Request headers</span></span>

<span data-ttu-id="96e64-151">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="96e64-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="96e64-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="96e64-152">Request body</span></span>

<span data-ttu-id="96e64-153">Yok.</span><span class="sxs-lookup"><span data-stu-id="96e64-153">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="96e64-154">İstek örnekleri</span><span class="sxs-lookup"><span data-stu-id="96e64-154">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="96e64-155">Ülkeye göre SKU kullanılabilirlikleri</span><span class="sxs-lookup"><span data-stu-id="96e64-155">Availabilities for SKU by country</span></span>

<span data-ttu-id="96e64-156">Ülkeye göre verilen SKU'nun kullanılabilirlik listesini almak için bu örneği izleyin:</span><span class="sxs-lookup"><span data-stu-id="96e64-156">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="96e64-157">VM rezervasyonları için kullanılabilirlik (Azure planı)</span><span class="sxs-lookup"><span data-stu-id="96e64-157">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="96e64-158">Azure VM rezervasyon SKUS'ları için ülkeye göre kullanılabilirlik listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e64-158">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="96e64-159">Bu örnek, Azure planları için geçerli olan SKUS'lar için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="96e64-159">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="96e64-160">Microsoft Azure (MS-AZR-0145P) abonelikleri için VM rezervasyonları için kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="96e64-160">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="96e64-161">Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan Azure VM rezervasyonları için ülkeye göre kullanılabilirlik listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="96e64-161">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="96e64-162">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="96e64-162">REST response</span></span>

<span data-ttu-id="96e64-163">Başarılı olursa, yanıt gövdesi Kullanılabilirlik kaynaklarının bir [**koleksiyonunu**](product-resources.md#availability) içerir.</span><span class="sxs-lookup"><span data-stu-id="96e64-163">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="96e64-164">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="96e64-164">Response success and error codes</span></span>

<span data-ttu-id="96e64-165">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="96e64-165">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="96e64-166">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="96e64-166">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="96e64-167">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="96e64-167">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="96e64-168">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="96e64-168">This method returns the following error codes:</span></span>

| <span data-ttu-id="96e64-169">HTTP Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="96e64-169">HTTP Status Code</span></span>     | <span data-ttu-id="96e64-170">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="96e64-170">Error code</span></span>   | <span data-ttu-id="96e64-171">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96e64-171">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="96e64-172">403</span><span class="sxs-lookup"><span data-stu-id="96e64-172">403</span></span>                  | <span data-ttu-id="96e64-173">400030</span><span class="sxs-lookup"><span data-stu-id="96e64-173">400030</span></span>       | <span data-ttu-id="96e64-174">İstenen **targetSegment'a erişime** izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="96e64-174">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="96e64-175">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="96e64-175">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58,83b644b5-e54a-4bdc-b354-f96c525b3c58
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02,70324727-62d8-4195-8f99-70ea25058d02
X-Locale: en-US,en-US
X-SourceFiles: =?UTF-8?B?QzpcVXNlcnNcbWFtZW5kZVxkZXZcZHBzLXJwZVxSUEUuUGFydG5lci5TZXJ2aWNlLkNhdGFsb2dcV2ViQXBpc1xDYXRhbG9nU2VydmljZS5WMi5XZWJcdjFccHJvZHVjdHNcRFpIMzE4WjBCUTNRXHNrdXNcMDAwMVxhdmFpbGFiaWxpdGllcw==?=
X-Powered-By: ASP.NET
Date: Wed, 14 Mar 2018 22:19:37 GMT
Content-Length: 808

{
    "totalCount": 1,
    "items": [
        {
            "id": "DZH318XZXVNF",
            "productId": "DZH318Z0BQ3Q",
            "skuId": "0001",
            "catalogItemId": "DZH318Z0BQ3Q:0001:DZH318XZXVNF",
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
                    "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities/DZH318Z0HMKQ?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetSegment=commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
