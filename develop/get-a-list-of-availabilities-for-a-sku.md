---
title: Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma
description: Müşteri ülkesine göre belirtilen ürün ve SKU için kullanılabilirlik koleksiyonu alma.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: b97a4ce85b5edd9de1301a577988f8c54096ebeb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769124"
---
# <a name="get-a-list-of-availabilities-for-a-sku-by-country"></a><span data-ttu-id="2ac8a-103">Bir SKU (ülkeye göre) için kullanılabilirlik listesini alma</span><span class="sxs-lookup"><span data-stu-id="2ac8a-103">Get a list of availabilities for a SKU (by country)</span></span>

<span data-ttu-id="2ac8a-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="2ac8a-104">**Applies to:**</span></span>

- <span data-ttu-id="2ac8a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2ac8a-105">Partner Center</span></span>

<span data-ttu-id="2ac8a-106">Bu makalede, belirli bir ülkede belirtilen ürün ve SKU için bir kullanılabilirlik koleksiyonunun nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-106">This article describes how to get a collection of availabilities in a particular country for a specified product and SKU.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ac8a-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2ac8a-107">Prerequisites</span></span>

- <span data-ttu-id="2ac8a-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2ac8a-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2ac8a-110">Bir ürün tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-110">A product identifier.</span></span>

- <span data-ttu-id="2ac8a-111">Bir SKU tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-111">A SKU identifier.</span></span>

- <span data-ttu-id="2ac8a-112">Bir ülke.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-112">A country.</span></span>

## <a name="c"></a><span data-ttu-id="2ac8a-113">C\#</span><span class="sxs-lookup"><span data-stu-id="2ac8a-113">C\#</span></span>

<span data-ttu-id="2ac8a-114">[SKU](product-resources.md#sku)'nun [kullanılabilirliği](product-resources.md#availability) listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="2ac8a-114">To get the list of [availabilities](product-resources.md#availability) for a [SKU](product-resources.md#sku):</span></span>

1. <span data-ttu-id="2ac8a-115">Belirli bir SKU 'nun işlemlerinin arabirimini almak için [kimliğe göre SKU 'Yu edinme](get-a-sku-by-id.md) bölümündeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-115">Follow the steps in [Get a SKU by ID](get-a-sku-by-id.md) to get the interface for a specific SKU's operations.</span></span>

2. <span data-ttu-id="2ac8a-116">SKU arabiriminden, kullanılabilirliği olan işlemleri içeren bir arabirim almak için **kullanılabilirlik** özelliğini seçin.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-116">From the SKU interface, select the **Availabilities** property to get an interface with the operations for availabilities.</span></span>

3. <span data-ttu-id="2ac8a-117">Seçim Kullanılabilirliği hedef kesime göre filtrelemek için **Bytargetsegment ()** yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-117">(Optional) Use the **ByTargetSegment()** method to filter the availabilities by target segment.</span></span>

4. <span data-ttu-id="2ac8a-118">Bu SKU 'nun kullanılabilirliği koleksiyonunu almak için **Get ()** veya **GetAsync ()** öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-118">Call **Get()** or **GetAsync()** to retrieve a collection of the availabilities for this SKU.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="2ac8a-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2ac8a-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2ac8a-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2ac8a-120">Request syntax</span></span>

| <span data-ttu-id="2ac8a-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2ac8a-121">Method</span></span>  | <span data-ttu-id="2ac8a-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2ac8a-122">Request URI</span></span>                                                                                                                              |
|---------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ac8a-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="2ac8a-123">**GET**</span></span> | <span data-ttu-id="2ac8a-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products/{product-id}/SKUs/{SKU-id}/kullanılabilirlik lıklara mi? ülke = {Country-code} &targetsegment = {Target-segment} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2ac8a-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/products/{product-id}/skus/{sku-id}/availabilities?country={country-code}&targetSegment={target-segment} HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="2ac8a-125">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="2ac8a-125">URI parameters</span></span>

<span data-ttu-id="2ac8a-126">SKU 'nun kullanılabilirliği listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-126">Use the following path and query parameters to get a list of availabilities for a SKU.</span></span>

| <span data-ttu-id="2ac8a-127">Ad</span><span class="sxs-lookup"><span data-stu-id="2ac8a-127">Name</span></span>                   | <span data-ttu-id="2ac8a-128">Tür</span><span class="sxs-lookup"><span data-stu-id="2ac8a-128">Type</span></span>     | <span data-ttu-id="2ac8a-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2ac8a-129">Required</span></span> | <span data-ttu-id="2ac8a-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2ac8a-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="2ac8a-131">ürün kimliği</span><span class="sxs-lookup"><span data-stu-id="2ac8a-131">product-id</span></span>             | <span data-ttu-id="2ac8a-132">string</span><span class="sxs-lookup"><span data-stu-id="2ac8a-132">string</span></span>   | <span data-ttu-id="2ac8a-133">Yes</span><span class="sxs-lookup"><span data-stu-id="2ac8a-133">Yes</span></span>      | <span data-ttu-id="2ac8a-134">Ürünü tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-134">A string that identifies the product.</span></span>                           |
| <span data-ttu-id="2ac8a-135">SKU kimliği</span><span class="sxs-lookup"><span data-stu-id="2ac8a-135">sku-id</span></span>                 | <span data-ttu-id="2ac8a-136">string</span><span class="sxs-lookup"><span data-stu-id="2ac8a-136">string</span></span>   | <span data-ttu-id="2ac8a-137">Yes</span><span class="sxs-lookup"><span data-stu-id="2ac8a-137">Yes</span></span>      | <span data-ttu-id="2ac8a-138">SKU 'YU tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-138">A string that identifies the SKU.</span></span>                               |
| <span data-ttu-id="2ac8a-139">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="2ac8a-139">country-code</span></span>           | <span data-ttu-id="2ac8a-140">string</span><span class="sxs-lookup"><span data-stu-id="2ac8a-140">string</span></span>   | <span data-ttu-id="2ac8a-141">Yes</span><span class="sxs-lookup"><span data-stu-id="2ac8a-141">Yes</span></span>      | <span data-ttu-id="2ac8a-142">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-142">A country/region ID.</span></span>                                            |
| <span data-ttu-id="2ac8a-143">hedef segment</span><span class="sxs-lookup"><span data-stu-id="2ac8a-143">target-segment</span></span>         | <span data-ttu-id="2ac8a-144">dize</span><span class="sxs-lookup"><span data-stu-id="2ac8a-144">string</span></span>   | <span data-ttu-id="2ac8a-145">No</span><span class="sxs-lookup"><span data-stu-id="2ac8a-145">No</span></span>       | <span data-ttu-id="2ac8a-146">Filtreleme için kullanılan hedef segmenti tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-146">A string that identifies the target segment used for filtering.</span></span> |
| <span data-ttu-id="2ac8a-147">Rezervationscope</span><span class="sxs-lookup"><span data-stu-id="2ac8a-147">reservationScope</span></span> | <span data-ttu-id="2ac8a-148">dize</span><span class="sxs-lookup"><span data-stu-id="2ac8a-148">string</span></span>   | <span data-ttu-id="2ac8a-149">No</span><span class="sxs-lookup"><span data-stu-id="2ac8a-149">No</span></span> | <span data-ttu-id="2ac8a-150">Bir Azure ayırma SKU 'SU için bir kullanılabilirlik listesi sorgulanırken, `reservationScope=AzurePlan` Azuplanlama için geçerli olan kullanılabilirlik listesini almak için belirtin.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-150">When querying for a list of availabilities for an Azure Reservation SKU, specify `reservationScope=AzurePlan` to get a list of availabilities which are applicable to AzurePlan.</span></span> <span data-ttu-id="2ac8a-151">Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan kullanılabilirliği listesini almak için bu parametreyi dışlayın.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-151">Exclude this parameter to get a list of availabilities which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="2ac8a-152">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2ac8a-152">Request headers</span></span>

<span data-ttu-id="2ac8a-153">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2ac8a-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2ac8a-154">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2ac8a-154">Request body</span></span>

<span data-ttu-id="2ac8a-155">Yok.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-155">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="2ac8a-156">İstek örnekleri</span><span class="sxs-lookup"><span data-stu-id="2ac8a-156">Request examples</span></span>

#### <a name="availabilities-for-sku-by-country"></a><span data-ttu-id="2ac8a-157">Ülkeye göre SKU için kullanılabilirlik</span><span class="sxs-lookup"><span data-stu-id="2ac8a-157">Availabilities for SKU by country</span></span>

<span data-ttu-id="2ac8a-158">Ülkeye göre belirli bir SKU 'nun kullanılabilirliği listesini almak için bu örneği izleyin:</span><span class="sxs-lookup"><span data-stu-id="2ac8a-158">Follow this example to get a list of availabilities for a given SKU by country:</span></span>

```http
GET http:// api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 70324727-62d8-4195-8f99-70ea25058d02
MS-CorrelationId: 83b644b5-e54a-4bdc-b354-f96c525b3c58
```

#### <a name="availabilities-for-vm-reservations-azure-plan"></a><span data-ttu-id="2ac8a-159">VM ayırmaları için kullanılabilirlik (Azure planı)</span><span class="sxs-lookup"><span data-stu-id="2ac8a-159">Availabilities for VM reservations (Azure plan)</span></span>

<span data-ttu-id="2ac8a-160">Azure VM ayırma SKU 'Larının ülkeye göre kullanılabilirliği listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-160">Follow this example to get a list of availabilities by country for Azure VM reservation SKUs.</span></span> <span data-ttu-id="2ac8a-161">Bu örnek, Azure planlarına uygulanan SKU 'Lara yöneliktir:</span><span class="sxs-lookup"><span data-stu-id="2ac8a-161">This example is for SKUs that apply to Azure plans:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products/DZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="availabilities-for-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="2ac8a-162">Microsoft Azure (MS-AZR-0145P) abonelikleri için VM ayırmaları kullanılabilirliği</span><span class="sxs-lookup"><span data-stu-id="2ac8a-162">Availabilities for VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="2ac8a-163">Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan Azure VM ayırmaları için ülkeye göre kullanılabilirlik listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-163">Follow this example to get a list of availabilities by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/productsDZH318Z0BQ3Q/skus/0001/availabilities?country=US&targetView=AzureAzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="2ac8a-164">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2ac8a-164">REST response</span></span>

<span data-ttu-id="2ac8a-165">Başarılı olursa, yanıt gövdesi bir [**kullanılabilirlik**](product-resources.md#availability) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-165">If successful, the response body contains a collection of [**Availability**](product-resources.md#availability) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2ac8a-166">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2ac8a-166">Response success and error codes</span></span>

<span data-ttu-id="2ac8a-167">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2ac8a-168">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2ac8a-169">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2ac8a-169">For a full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="2ac8a-170">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="2ac8a-170">This method returns the following error codes:</span></span>

| <span data-ttu-id="2ac8a-171">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="2ac8a-171">HTTP Status Code</span></span>     | <span data-ttu-id="2ac8a-172">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="2ac8a-172">Error code</span></span>   | <span data-ttu-id="2ac8a-173">Description</span><span class="sxs-lookup"><span data-stu-id="2ac8a-173">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2ac8a-174">403</span><span class="sxs-lookup"><span data-stu-id="2ac8a-174">403</span></span>                  | <span data-ttu-id="2ac8a-175">400030</span><span class="sxs-lookup"><span data-stu-id="2ac8a-175">400030</span></span>       | <span data-ttu-id="2ac8a-176">İstenen **Targetsegment** erişimine izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="2ac8a-176">Access to the requested **targetSegment** is not allowed.</span></span>                                                     |

### <a name="response-example"></a><span data-ttu-id="2ac8a-177">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2ac8a-177">Response example</span></span>

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
