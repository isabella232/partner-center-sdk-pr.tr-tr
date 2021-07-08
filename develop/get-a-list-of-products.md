---
title: Ürünlerin bir listesini alma (ülkeye göre)
description: Ürün kaynağını kullanarak müşteri ülkesine göre bir ürün koleksiyonu elde etmek için kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 1258727ecbe7c5cc332624577fa8a355e28e3717
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874219"
---
# <a name="get-a-list-of-products-by-country"></a><span data-ttu-id="6d50d-103">Ürünlerin bir listesini alma (ülkeye göre)</span><span class="sxs-lookup"><span data-stu-id="6d50d-103">Get a list of products (by country)</span></span>

<span data-ttu-id="6d50d-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6d50d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6d50d-105">Belirli bir ülkede kullanılabilen ürün koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d50d-105">You can use the following methods to get a collection of products available in a particular country.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6d50d-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6d50d-106">Prerequisites</span></span>

- <span data-ttu-id="6d50d-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6d50d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6d50d-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="6d50d-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6d50d-109">Ülke.</span><span class="sxs-lookup"><span data-stu-id="6d50d-109">A country.</span></span>

## <a name="c"></a><span data-ttu-id="6d50d-110">C\#</span><span class="sxs-lookup"><span data-stu-id="6d50d-110">C\#</span></span>

<span data-ttu-id="6d50d-111">Ürünlerin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="6d50d-111">To get a list of products:</span></span>

1. <span data-ttu-id="6d50d-112">**ByCountry()** yöntemini kullanarak ülkeyi seçmek için **IAggregatePartner.Products** koleksiyonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d50d-112">Use your **IAggregatePartner.Products** collection to select the country by using the **ByCountry()** method.</span></span>

2. <span data-ttu-id="6d50d-113">**ByTargetView() yöntemini kullanarak katalog görünümünü** seçin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-113">Select the catalog view using the **ByTargetView()** method.</span></span>

3. <span data-ttu-id="6d50d-114">(İsteğe bağlı) **ByReservationScope() yöntemini kullanarak rezervasyon kapsamını** seçin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-114">(Optional) Select the reservation scope using the **ByReservationScope()** method.</span></span>

4. <span data-ttu-id="6d50d-115">(İsteğe bağlı) **ByTargetSegment() yöntemini kullanarak hedef segmenti** seçin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-115">(Optional) Select the target segment using the **ByTargetSegment()** method.</span></span>

5. <span data-ttu-id="6d50d-116">Koleksiyonu geri **almak için Get()** **veya GetAsync()** yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="6d50d-116">Call the **Get()** or **GetAsync()** method to return the collection.</span></span>

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

## <a name="java"></a><span data-ttu-id="6d50d-117">Java</span><span class="sxs-lookup"><span data-stu-id="6d50d-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="6d50d-118">Ürünlerin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="6d50d-118">To get a list of products:</span></span>

1. <span data-ttu-id="6d50d-119">**byCountry()** işlevini kullanarak ülkeyi seçmek için **IAggregatePartner.getProducts** işlevinizi kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d50d-119">Use your **IAggregatePartner.getProducts** function to select the country by using the **byCountry()** function.</span></span>

2. <span data-ttu-id="6d50d-120">**byTargetView() işlevini kullanarak katalog görünümünü** seçin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-120">Select the catalog view using the **byTargetView()** function.</span></span>
3. <span data-ttu-id="6d50d-121">(İsteğe bağlı) **byTargetSegment() işlevini kullanarak hedef segmenti** seçin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-121">(Optional) Select the target segment using the **byTargetSegment()** function.</span></span>

4. <span data-ttu-id="6d50d-122">Koleksiyonu geri **almak için get()** işlevini çağırma.</span><span class="sxs-lookup"><span data-stu-id="6d50d-122">Call the **get()** function to return the collection.</span></span>

```java
// IAggregatePartner partnerOperations;

// Get the products for the specified catalog view.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").get();

// Get the products filtered by target view and target segment.
ResourceCollection<Products> products = partnerOperations.getProducts().byCountry("US").byTargetView("Azure").byTargetSegment("commercial").get();
```

## <a name="powershell"></a><span data-ttu-id="6d50d-123">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6d50d-123">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="6d50d-124">Ürünlerin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="6d50d-124">To get a list of products:</span></span>

1. <span data-ttu-id="6d50d-125">[**Get-PartnerProduct komutunu**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) yürütün.</span><span class="sxs-lookup"><span data-stu-id="6d50d-125">Execute the [**Get-PartnerProduct**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerProduct.md) command.</span></span>

2. <span data-ttu-id="6d50d-126">**Katalog** parametresini belirterek kataloğu seçin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-126">Select the catalog by specifying the **Catalog** parameter.</span></span>
3. <span data-ttu-id="6d50d-127">(İsteğe bağlı) Segment parametresini belirterek hedef **segmenti** seçin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-127">(Optional) Select the target segment by specifying the **Segment** parameter.</span></span>

```powershell
Get-PartnerProduct -Catalog 'Azure' -Segment 'commercial'
```

## <a name="rest-request"></a><span data-ttu-id="6d50d-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6d50d-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6d50d-129">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="6d50d-129">Request syntax</span></span>

| <span data-ttu-id="6d50d-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6d50d-130">Method</span></span>  | <span data-ttu-id="6d50d-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6d50d-131">Request URI</span></span>                                                                                                                                    |
|---------|----------------------------------------------------------------------------------------------------------------------------------------------- |
| <span data-ttu-id="6d50d-132">**Al**</span><span class="sxs-lookup"><span data-stu-id="6d50d-132">**GET**</span></span> | <span data-ttu-id="6d50d-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6d50d-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/products?country={country}&targetView={targetView}&targetSegment={targetSegment} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="6d50d-134">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="6d50d-134">URI parameters</span></span>

<span data-ttu-id="6d50d-135">Ürünlerin listesini almak için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d50d-135">Use the following path and query parameters to get a list of products.</span></span>

| <span data-ttu-id="6d50d-136">Ad</span><span class="sxs-lookup"><span data-stu-id="6d50d-136">Name</span></span>                   | <span data-ttu-id="6d50d-137">Tür</span><span class="sxs-lookup"><span data-stu-id="6d50d-137">Type</span></span>     | <span data-ttu-id="6d50d-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6d50d-138">Required</span></span> | <span data-ttu-id="6d50d-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6d50d-139">Description</span></span>                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| <span data-ttu-id="6d50d-140">ülke</span><span class="sxs-lookup"><span data-stu-id="6d50d-140">country</span></span>                | <span data-ttu-id="6d50d-141">string</span><span class="sxs-lookup"><span data-stu-id="6d50d-141">string</span></span>   | <span data-ttu-id="6d50d-142">Yes</span><span class="sxs-lookup"><span data-stu-id="6d50d-142">Yes</span></span>      | <span data-ttu-id="6d50d-143">Ülke/bölge kimliği.</span><span class="sxs-lookup"><span data-stu-id="6d50d-143">The country/region ID.</span></span>                                                  |
| <span data-ttu-id="6d50d-144">targetView</span><span class="sxs-lookup"><span data-stu-id="6d50d-144">targetView</span></span>             | <span data-ttu-id="6d50d-145">string</span><span class="sxs-lookup"><span data-stu-id="6d50d-145">string</span></span>   | <span data-ttu-id="6d50d-146">Yes</span><span class="sxs-lookup"><span data-stu-id="6d50d-146">Yes</span></span>      | <span data-ttu-id="6d50d-147">Kataloğun hedef görünümünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6d50d-147">Identifies the target view of the catalog.</span></span> <span data-ttu-id="6d50d-148">Desteklenen değerler:</span><span class="sxs-lookup"><span data-stu-id="6d50d-148">The supported values are:</span></span> <br/><br/><span data-ttu-id="6d50d-149">**Tüm Azure** öğelerini içeren Azure</span><span class="sxs-lookup"><span data-stu-id="6d50d-149">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="6d50d-150">Tüm Azure rezervasyon öğelerini içeren **AzureReservations**</span><span class="sxs-lookup"><span data-stu-id="6d50d-150">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="6d50d-151">Tüm sanal makine (VM) rezervasyon öğelerini içeren **AzureReservationsVM**</span><span class="sxs-lookup"><span data-stu-id="6d50d-151">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="6d50d-152">**Tüm rezervasyon öğelerini içeren AzureReservationsSQL** SQL öğeleri</span><span class="sxs-lookup"><span data-stu-id="6d50d-152">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="6d50d-153">**Tüm veritabanı rezervasyon öğelerini içeren AzureReservationsCosmosDb** Cosmos öğeleri</span><span class="sxs-lookup"><span data-stu-id="6d50d-153">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="6d50d-154">Microsoft Azure abonelikleri (**MS-AZR-0145P**) ve Azure planları için öğeleri içeren **MicrosoftAzure**</span><span class="sxs-lookup"><span data-stu-id="6d50d-154">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="6d50d-155">Tüm çevrimiçi hizmet öğelerini (ticari market ürünleri dahil) içeren **OnlineServices**</span><span class="sxs-lookup"><span data-stu-id="6d50d-155">**OnlineServices**, which includes all online service items (including commercial marketplace products)</span></span><br/><br/><span data-ttu-id="6d50d-156">**Yazılım**, tüm yazılım öğelerini içerir</span><span class="sxs-lookup"><span data-stu-id="6d50d-156">**Software**, which includes all software items</span></span><br/><br/><span data-ttu-id="6d50d-157">**SoftwareSUSELinux**, tüm yazılım SUSE Linux öğelerini içerir</span><span class="sxs-lookup"><span data-stu-id="6d50d-157">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="6d50d-158">Tüm kalıcı yazılım öğelerini içeren **SoftwarePerpetual**</span><span class="sxs-lookup"><span data-stu-id="6d50d-158">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="6d50d-159">Tüm yazılım aboneliği öğelerini içeren **YazılımAubscriptions**</span><span class="sxs-lookup"><span data-stu-id="6d50d-159">**SoftwareSubscriptions**, which includes all software subscription items</span></span>    |
| <span data-ttu-id="6d50d-160">targetSegment</span><span class="sxs-lookup"><span data-stu-id="6d50d-160">targetSegment</span></span>          | <span data-ttu-id="6d50d-161">dize</span><span class="sxs-lookup"><span data-stu-id="6d50d-161">string</span></span>   | <span data-ttu-id="6d50d-162">No</span><span class="sxs-lookup"><span data-stu-id="6d50d-162">No</span></span>       | <span data-ttu-id="6d50d-163">Hedef segmenti tanımlar.</span><span class="sxs-lookup"><span data-stu-id="6d50d-163">Identifies the target segment.</span></span> <span data-ttu-id="6d50d-164">Farklı hedef kitlelere yönelik görünüm.</span><span class="sxs-lookup"><span data-stu-id="6d50d-164">The view for different target audiences.</span></span> <span data-ttu-id="6d50d-165">Desteklenen değerler:</span><span class="sxs-lookup"><span data-stu-id="6d50d-165">The supported values are:</span></span> <br/><br/><span data-ttu-id="6d50d-166">**Ticari**</span><span class="sxs-lookup"><span data-stu-id="6d50d-166">**commercial**</span></span><br/><span data-ttu-id="6d50d-167">**Eğitim**</span><span class="sxs-lookup"><span data-stu-id="6d50d-167">**education**</span></span><br/><span data-ttu-id="6d50d-168">**Hükümet**</span><span class="sxs-lookup"><span data-stu-id="6d50d-168">**government**</span></span><br/><span data-ttu-id="6d50d-169">**Kar amacı gütme -yen**</span><span class="sxs-lookup"><span data-stu-id="6d50d-169">**nonprofit**</span></span>  |
| <span data-ttu-id="6d50d-170">reservationScope</span><span class="sxs-lookup"><span data-stu-id="6d50d-170">reservationScope</span></span> | <span data-ttu-id="6d50d-171">dize</span><span class="sxs-lookup"><span data-stu-id="6d50d-171">string</span></span>   | <span data-ttu-id="6d50d-172">No</span><span class="sxs-lookup"><span data-stu-id="6d50d-172">No</span></span> | <span data-ttu-id="6d50d-173">Azure Rezervasyonları için ürünlerin listesini sorgularken, Azure planları için `reservationScope=AzurePlan` geçerli olan ürünlerin listesini almak için belirtin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-173">When querying for a list of products for Azure Reservations, specify `reservationScope=AzurePlan` to get a list of products that are applicable to Azure plans.</span></span> <span data-ttu-id="6d50d-174">Microsoft Azure (**MS-AZR-0145P**) abonelikleri için geçerli olan Azure rezervasyonlarının ürünlerinin listesini almak için bu parametreyi hariç tutabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6d50d-174">Exclude this parameter to get a list of products for Azure reservations, which are applicable to Microsoft Azure (**MS-AZR-0145P**) subscriptions.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="6d50d-175">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6d50d-175">Request headers</span></span>

<span data-ttu-id="6d50d-176">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6d50d-176">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6d50d-177">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6d50d-177">Request body</span></span>

<span data-ttu-id="6d50d-178">Yok.</span><span class="sxs-lookup"><span data-stu-id="6d50d-178">None.</span></span>

### <a name="request-examples"></a><span data-ttu-id="6d50d-179">İstek örnekleri</span><span class="sxs-lookup"><span data-stu-id="6d50d-179">Request examples</span></span>

#### <a name="products-by-country"></a><span data-ttu-id="6d50d-180">Ülkeye göre ürünler</span><span class="sxs-lookup"><span data-stu-id="6d50d-180">Products by country</span></span>

<span data-ttu-id="6d50d-181">Microsoft Azure (MS-AZR-0145P) abonelikleri ve Azure planları için ülkeye göre ürünlerin listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-181">Follow this example to get a list of products by country for Microsoft Azure (MS-AZR-0145P) subscriptions and Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-azure-plan"></a><span data-ttu-id="6d50d-182">Azure VM rezervasyonları (Azure planı)</span><span class="sxs-lookup"><span data-stu-id="6d50d-182">Azure VM reservations (Azure plan)</span></span>

<span data-ttu-id="6d50d-183">Azure planları için geçerli olan Azure VM rezervasyonları için ülkeye göre ürünlerin listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-183">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Azure plans.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureAzureReservationsVM&reservationScope=AzurePlan HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

#### <a name="azure-vm-reservations-for-microsoft-azure-ms-azr-0145p-subscriptions"></a><span data-ttu-id="6d50d-184">Microsoft Azure (MS-AZR-0145P) abonelikleri için Azure VM rezervasyonları</span><span class="sxs-lookup"><span data-stu-id="6d50d-184">Azure VM reservations for Microsoft Azure (MS-AZR-0145P) subscriptions</span></span>

<span data-ttu-id="6d50d-185">Microsoft Azure (MS-AZR-0145P) abonelikleri için geçerli olan Azure VM rezervasyonları için ülkeye göre ürünlerin listesini almak için bu örneği izleyin.</span><span class="sxs-lookup"><span data-stu-id="6d50d-185">Follow this example to get a list of products by country for Azure VM reservations that are applicable to Microsoft Azure (MS-AZR-0145P) subscriptions.</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/products?country=US&targetView=AzureReservationsVM HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

## <a name="rest-response"></a><span data-ttu-id="6d50d-186">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6d50d-186">REST response</span></span>

<span data-ttu-id="6d50d-187">Başarılı olursa yanıt gövdesi bir Ürün kaynakları [**koleksiyonu**](product-resources.md#product) içerir.</span><span class="sxs-lookup"><span data-stu-id="6d50d-187">If successful, the response body contains a collection of [**Product**](product-resources.md#product) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6d50d-188">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6d50d-188">Response success and error codes</span></span>

<span data-ttu-id="6d50d-189">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="6d50d-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6d50d-190">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6d50d-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6d50d-191">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6d50d-191">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="6d50d-192">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="6d50d-192">This method returns the following error codes:</span></span>

| <span data-ttu-id="6d50d-193">HTTP Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="6d50d-193">HTTP Status Code</span></span>     | <span data-ttu-id="6d50d-194">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="6d50d-194">Error code</span></span>   | <span data-ttu-id="6d50d-195">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6d50d-195">Description</span></span>                                                                                               |
|----------------------|--------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6d50d-196">403</span><span class="sxs-lookup"><span data-stu-id="6d50d-196">403</span></span>                  | <span data-ttu-id="6d50d-197">400030</span><span class="sxs-lookup"><span data-stu-id="6d50d-197">400030</span></span>       | <span data-ttu-id="6d50d-198">İstenen targetSegment'a erişime izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="6d50d-198">Access to the requested targetSegment is not allowed.</span></span>                                                     |
| <span data-ttu-id="6d50d-199">403</span><span class="sxs-lookup"><span data-stu-id="6d50d-199">403</span></span>                  | <span data-ttu-id="6d50d-200">400036</span><span class="sxs-lookup"><span data-stu-id="6d50d-200">400036</span></span>       | <span data-ttu-id="6d50d-201">İstenen targetView 'a erişime izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="6d50d-201">Access to the requested targetView is not allowed.</span></span>                                                        |

### <a name="response-example"></a><span data-ttu-id="6d50d-202">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6d50d-202">Response example</span></span>

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
