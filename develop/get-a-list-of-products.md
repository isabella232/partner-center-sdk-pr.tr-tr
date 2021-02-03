---
title: Ürünlerin bir listesini alma (ülkeye göre)
description: Ürün kaynağını, müşteri ülkesine göre ürünlerin koleksiyonunu almak için kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: ea239aa008a5b7c33740e9c4697c3795908415cd
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769448"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="6666a-103">Ürünlerin bir listesini alma (ülkeye göre)</span><span class="sxs-lookup"><span data-stu-id="6666a-103">Get a list of products (by country)</span></span>

<span data-ttu-id="6666a-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="6666a-104">**Applies to:**</span></span>

- <span data-ttu-id="6666a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6666a-105">Partner Center</span></span>
- <span data-ttu-id="6666a-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6666a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6666a-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6666a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="6666a-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6666a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6666a-109">Belirli bir ülkede bulunan ürünlerin bir koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6666a-109">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6666a-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6666a-110">Prerequisites</span></span>

- <span data-ttu-id="6666a-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6666a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6666a-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="6666a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6666a-113">Bir ülke.</span><span class="sxs-lookup"><span data-stu-id="6666a-113">A country.</span></span>

## <a name="c"></a><span data-ttu-id="6666a-114">C\#</span><span class="sxs-lookup"><span data-stu-id="6666a-114">C\#</span></span>

<span data-ttu-id="6666a-115">Ürünlerin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="6666a-115">To get a list of products:</span></span>

1. <span data-ttu-id="6666a-116">**Bycountry ()** yöntemini kullanarak ülkeyi seçmek Için **ıaggregatepartner. Products** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6666a-116">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="6666a-117">**Bytargetview ()** yöntemini kullanarak katalog görünümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="6666a-117">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="6666a-118">Seçim **Byrezervationscope ()** yöntemini kullanarak ayırma kapsamını seçin.</span><span class="sxs-lookup"><span data-stu-id="6666a-118">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="6666a-119">Seçim **Bytargetsegment ()** yöntemini kullanarak hedef segmenti seçin.</span><span class="sxs-lookup"><span data-stu-id="6666a-119">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="6666a-120">Koleksiyonu döndürmek için **Get ()** veya **GetAsync ()** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="6666a-120">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

```csharp
IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").Get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.Products.ByCountry("US").ByTargetView("MicrosoftAzure").ByTargetSegment("commercial").Get();

// Get the products for Azure reservations which are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").Get();

// Get the products for Azure reservations which are applicable to Azure plans only.
ResourceCollection<Product> products = partnerOperations.Products.ByCountry("US").ByTargetView("AzureReservations").ByReservationScope("AzurePlan").Get();

```

## <a name="java"></a><span data-ttu-id="6666a-121">Java</span><span class="sxs-lookup"><span data-stu-id="6666a-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="6666a-122">Ürünlerin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="6666a-122">To get a list of products:</span></span>

1. <span data-ttu-id="6666a-123">**Bycountry ()** işlevini kullanarak ülkeyi seçmek Için **ıaggregatepartner. GetProducts** işlevinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6666a-123">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="6666a-124">**Bytargetview ()** işlevini kullanarak katalog görünümünü seçin.</span><span class="sxs-lookup"><span data-stu-id="6666a-124">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="6666a-125">Seçim **Bytargetsegment ()** işlevini kullanarak hedef segmenti seçin.</span><span class="sxs-lookup"><span data-stu-id="6666a-125">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="6666a-126">Koleksiyonu döndürmek için **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="6666a-126">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="6666a-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6666a-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="6666a-128">Ürünlerin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="6666a-128">To get a list of products:</span></span>

1. <span data-ttu-id="6666a-129">[**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="6666a-129">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="6666a-130">**Katalog parametresini belirterek** kataloğu seçin.</span><span class="sxs-lookup"><span data-stu-id="6666a-130">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="6666a-131">Seçim **Segment** parametresini belirterek hedef segmenti seçin.</span><span class="sxs-lookup"><span data-stu-id="6666a-131">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="6666a-132">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6666a-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6666a-133">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6666a-133">Request syntax</span></span>

| <span data-ttu-id="6666a-134">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6666a-134">Method</span></span>  | <span data-ttu-id="6666a-135">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6666a-135">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="6666a-136">**Al**</span><span class="sxs-lookup"><span data-stu-id="6666a-136">**GET**</span></span> | <span data-ttu-id="6666a-137">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Products? ülke = {country} &targetview = {targetview} &targetsegment = {TARGETSEGMENT} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6666a-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6666a-138">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="6666a-138">URI parameters</span></span>

<span data-ttu-id="6666a-139">Ürünlerin bir listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6666a-139">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="6666a-140">Ad</span><span class="sxs-lookup"><span data-stu-id="6666a-140">Name</span></span>                   | <span data-ttu-id="6666a-141">Tür</span><span class="sxs-lookup"><span data-stu-id="6666a-141">Type</span></span>     | <span data-ttu-id="6666a-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6666a-142">Required</span></span> | <span data-ttu-id="6666a-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6666a-143">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="6666a-144">ülke</span><span class="sxs-lookup"><span data-stu-id="6666a-144">country</span></span>                | <span data-ttu-id="6666a-145">string</span><span class="sxs-lookup"><span data-stu-id="6666a-145">string</span></span>   | <span data-ttu-id="6666a-146">Yes</span><span class="sxs-lookup"><span data-stu-id="6666a-146">Yes</span></span>      | <span data-ttu-id="6666a-147">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="6666a-147">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="6666a-148">targetView</span><span class="sxs-lookup"><span data-stu-id="6666a-148">targetView</span></span>             | <span data-ttu-id="6666a-149">string</span><span class="sxs-lookup"><span data-stu-id="6666a-149">string</span></span>   | <span data-ttu-id="6666a-150">Yes</span><span class="sxs-lookup"><span data-stu-id="6666a-150">Yes</span></span>      | <span data-ttu-id="6666a-151">Kataloğun hedef görünümünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6666a-151">Identifies the target view of the catalog.</span></span> <span data-ttu-id="6666a-152">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6666a-152">The supported values are:</span></span> <br/><br/><span data-ttu-id="6666a-153">Tüm Azure öğelerini içeren **Azure**</span><span class="sxs-lookup"><span data-stu-id="6666a-153">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="6666a-154">Tüm Azure ayırma öğelerini içeren **Azurereservations**</span><span class="sxs-lookup"><span data-stu-id="6666a-154">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="6666a-155">Tüm sanal makine (VM) rezervasyon öğelerini içeren **Azurereservationsvm**</span><span class="sxs-lookup"><span data-stu-id="6666a-155">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="6666a-156">Tüm SQL rezervasyon öğelerini içeren **Azurereservationssql**</span><span class="sxs-lookup"><span data-stu-id="6666a-156">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="6666a-157">Tüm Cosmos veritabanı ayırma öğelerini içeren **Azurereservationscosmosdb**</span><span class="sxs-lookup"><span data-stu-id="6666a-157">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="6666a-158">Microsoft Azure aboneliklerine (**MS-AZR-0145P**) ve Azure planlarına yönelik öğeler içeren **MicrosoftAzure**</span><span class="sxs-lookup"><span data-stu-id="6666a-158">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="6666a-159">Tüm çevrimiçi hizmet öğelerini içeren **OnlineServices**(ticari Market ürünleri dahil)</span><span class="sxs-lookup"><span data-stu-id="6666a-159">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="6666a-160">Tüm yazılım öğelerini içeren **yazılım**</span><span class="sxs-lookup"><span data-stu-id="6666a-160">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="6666a-161">Tüm yazılım SUSE Linux öğelerini içeren **SoftwareSUSELinux**</span><span class="sxs-lookup"><span data-stu-id="6666a-161">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="6666a-162">Tüm kalıcı yazılım öğelerini içeren **Softwarekalıcı**</span><span class="sxs-lookup"><span data-stu-id="6666a-162">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="6666a-163">Tüm yazılım aboneliği öğelerini içeren **SoftwareSubscriptions**</span><span class="sxs-lookup"><span data-stu-id="6666a-163">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="6666a-164">targetSegment</span><span class="sxs-lookup"><span data-stu-id="6666a-164">targetSegment</span></span>          | <span data-ttu-id="6666a-165">dize</span><span class="sxs-lookup"><span data-stu-id="6666a-165">string</span></span>   | <span data-ttu-id="6666a-166">No</span><span class="sxs-lookup"><span data-stu-id="6666a-166">No</span></span>       | <span data-ttu-id="6666a-167">Hedef segmenti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6666a-167">Identifies the target segment.</span></span> <span data-ttu-id="6666a-168">Farklı hedef kitlelerinin görünümü.</span><span class="sxs-lookup"><span data-stu-id="6666a-168">The view for different target audiences.</span></span> <span data-ttu-id="6666a-169">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="6666a-169">The supported values are:</span></span> <br/><br/><span data-ttu-id="6666a-170">**seniz**</span><span class="sxs-lookup"><span data-stu-id="6666a-170">**commercial**</span></span><br/><span data-ttu-id="6666a-171">**öğrenim**</span><span class="sxs-lookup"><span data-stu-id="6666a-171">**education**</span></span><br/><span data-ttu-id="6666a-172">**Devlet**</span><span class="sxs-lookup"><span data-stu-id="6666a-172">**government**</span></span><br/><span data-ttu-id="6666a-173">**kar amacı gütmeyen**</span><span class="sxs-lookup"><span data-stu-id="6666a-173">**nonprofit**</span></span>  |
| <span data-ttu-id="6666a-174">Rezervationscope</span><span class="sxs-lookup"><span data-stu-id="6666a-174">reservationScope</span></span> | <span data-ttu-id="6666a-175">dize</span><span class="sxs-lookup"><span data-stu-id="6666a-175">string</span></span>   | <span data-ttu-id="6666a-176">No</span><span class="sxs-lookup"><span data-stu-id="6666a-176">No</span></span> | <span data-ttu-id="6666a-177">Azure ayırmaları için bir ürün listesi sorgulanırken, `reservationScope=AzurePlan` Azure planlarına uygun ürünlerin bir listesini almak için belirtin.</span><span class="sxs-lookup"><span data-stu-id="6666a-177">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="6666a-178">Microsoft Azure (**MS-azr-0145P**) abonelikleri için geçerli olan Azure ayırmaları ürünlerinin bir listesini almak için bu parametreyi dışlayın.</span><span class="sxs-lookup"><span data-stu-id="6666a-178">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="6666a-179">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6666a-179">Request headers</span></span>

<span data-ttu-id="6666a-180">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6666a-180">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6666a-181">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6666a-181">Request body</span></span>

<span data-ttu-id="6666a-182">Yok.</span><span class="sxs-lookup"><span data-stu-id="6666a-182">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="6666a-183">İstek örnekleri</span><span class="sxs-lookup"><span data-stu-id="6666a-183">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="6666a-184">Ülkeye göre ürünler</span><span class="sxs-lookup"><span data-stu-id="6666a-184">Products by country</span></span>

<span data-ttu-id="6666a-185">Microsoft Azure (MS-AZR-0145P) abonelikleri ve Azure planları için ülkeye göre ürünlerin bir listesini almak üzere bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="6666a-185">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="6666a-186">Azure VM ayırmaları (Azure planı)</span><span class="sxs-lookup"><span data-stu-id="6666a-186">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="6666a-187">Azure planlarına uygun Azure VM ayırmaları için ülkeye göre ürünlerin bir listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="6666a-187">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="6666a-188">Microsoft Azure için Azure VM ayırmaları (MS-AZR-0145P) abonelikleri</span><span class="sxs-lookup"><span data-stu-id="6666a-188">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="6666a-189">Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan Azure VM ayırmaları ülkeye göre ürünlerin bir listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="6666a-189">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="6666a-190">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6666a-190">REST response</span></span>

<span data-ttu-id="6666a-191">Başarılı olursa, yanıt gövdesi bir [**ürün**](product-resources.md#product) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="6666a-191">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6666a-192">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6666a-192">Response success and error codes</span></span>

<span data-ttu-id="6666a-193">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="6666a-193">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6666a-194">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6666a-194">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6666a-195">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6666a-195">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="6666a-196">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="6666a-196">This method returns the following error codes:</span></span>

| <span data-ttu-id="6666a-197">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="6666a-197">HTTP Status Code</span></span>     | <span data-ttu-id="6666a-198">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="6666a-198">Error code</span></span>   | <span data-ttu-id="6666a-199">Description</span><span class="sxs-lookup"><span data-stu-id="6666a-199">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6666a-200">403</span><span class="sxs-lookup"><span data-stu-id="6666a-200">403</span></span>                  | <span data-ttu-id="6666a-201">400030</span><span class="sxs-lookup"><span data-stu-id="6666a-201">400030</span></span>       | <span data-ttu-id="6666a-202">İstenen targetSegment erişimine izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="6666a-202">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="6666a-203">403</span><span class="sxs-lookup"><span data-stu-id="6666a-203">403</span></span>                  | <span data-ttu-id="6666a-204">400036</span><span class="sxs-lookup"><span data-stu-id="6666a-204">400036</span></span>       | <span data-ttu-id="6666a-205">İstenen targetView 'a erişime izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="6666a-205">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="6666a-206">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6666a-206">Response example</span></span>

```http
{
    "totalCount": 19,
    "items": [
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
        },
        ...
    ],
    "links": {
        "self": {
            "uri": "/products?country=US&targetView=Azure",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
