---
title: Lisans kullanım bilgilerini alma
description: Office ve Dynamics için iş yükü düzeyinde lisans kullanım bilgileri alma.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a144fd078a36289e4a2c70880817b1f0ca627e8a
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769430"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="5940b-103">Lisans kullanım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="5940b-103">Get licenses usage information</span></span>

<span data-ttu-id="5940b-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="5940b-104">**Applies To**</span></span>

- <span data-ttu-id="5940b-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5940b-105">Partner Center</span></span>

<span data-ttu-id="5940b-106">Office ve Dynamics için iş yükü düzeyinde lisans kullanım bilgileri alma.</span><span class="sxs-lookup"><span data-stu-id="5940b-106">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5940b-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5940b-107">Prerequisites</span></span>

<span data-ttu-id="5940b-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5940b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5940b-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="5940b-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="5940b-110">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5940b-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5940b-111">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5940b-111">Request syntax</span></span>

| <span data-ttu-id="5940b-112">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5940b-112">Method</span></span>  | <span data-ttu-id="5940b-113">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5940b-113">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="5940b-114">**Al**</span><span class="sxs-lookup"><span data-stu-id="5940b-114">**GET**</span></span> | <span data-ttu-id="5940b-115">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Analtics/, CIAL/Usage/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="5940b-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5940b-116">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5940b-116">Request headers</span></span>

<span data-ttu-id="5940b-117">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5940b-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="5940b-118">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="5940b-118">URI parameters</span></span>

| <span data-ttu-id="5940b-119">Parametre</span><span class="sxs-lookup"><span data-stu-id="5940b-119">Parameter</span></span>         | <span data-ttu-id="5940b-120">Tür</span><span class="sxs-lookup"><span data-stu-id="5940b-120">Type</span></span>     | <span data-ttu-id="5940b-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5940b-121">Description</span></span> | <span data-ttu-id="5940b-122">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5940b-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="5940b-123">top</span><span class="sxs-lookup"><span data-stu-id="5940b-123">top</span></span>               | <span data-ttu-id="5940b-124">string</span><span class="sxs-lookup"><span data-stu-id="5940b-124">string</span></span>   | <span data-ttu-id="5940b-125">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="5940b-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="5940b-126">Belirtilen en büyük değer ve varsayılan değer 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="5940b-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="5940b-127">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="5940b-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="5940b-128">No</span><span class="sxs-lookup"><span data-stu-id="5940b-128">No</span></span> |
| <span data-ttu-id="5940b-129">Atla</span><span class="sxs-lookup"><span data-stu-id="5940b-129">skip</span></span>              | <span data-ttu-id="5940b-130">int</span><span class="sxs-lookup"><span data-stu-id="5940b-130">int</span></span>      | <span data-ttu-id="5940b-131">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="5940b-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="5940b-132">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="5940b-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="5940b-133">Örneğin, top = 10000 ve Skip = 0 verilerin ilk 10000 satırını alır, top = 10000 ve Skip = 10000 sonraki 10000 satırlık verileri alır ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="5940b-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="5940b-134">No</span><span class="sxs-lookup"><span data-stu-id="5940b-134">No</span></span> |
| <span data-ttu-id="5940b-135">filtre</span><span class="sxs-lookup"><span data-stu-id="5940b-135">filter</span></span>            | <span data-ttu-id="5940b-136">string</span><span class="sxs-lookup"><span data-stu-id="5940b-136">string</span></span>   | <span data-ttu-id="5940b-137">İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor.</span><span class="sxs-lookup"><span data-stu-id="5940b-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="5940b-138">Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir **`eq`** **`ne`** ve deyimler or kullanılarak birleştirilebilir **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="5940b-138">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="5940b-139">Aşağıda bazı örnek *filtre* parametreleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="5940b-139">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="5940b-140">*Filter = workloadCode EQ ' SFB '*</span><span class="sxs-lookup"><span data-stu-id="5940b-140">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="5940b-141">*Filter = workloadCode EQ ' SFB '* veya (*Channel EQ ' Bayi '*)</span><span class="sxs-lookup"><span data-stu-id="5940b-141">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="5940b-142">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5940b-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="5940b-143">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="5940b-143">**workloadCode**</span></span><br/><span data-ttu-id="5940b-144">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="5940b-144">**workloadName**</span></span><br/><span data-ttu-id="5940b-145">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="5940b-145">**serviceCode**</span></span><br/><span data-ttu-id="5940b-146">**HizmetAdı**</span><span class="sxs-lookup"><span data-stu-id="5940b-146">**serviceName**</span></span><br/><span data-ttu-id="5940b-147">**kanalla**</span><span class="sxs-lookup"><span data-stu-id="5940b-147">**channel**</span></span><br/><span data-ttu-id="5940b-148">**Customertenantıd**</span><span class="sxs-lookup"><span data-stu-id="5940b-148">**customerTenantId**</span></span><br/><span data-ttu-id="5940b-149">**customerName**</span><span class="sxs-lookup"><span data-stu-id="5940b-149">**customerName**</span></span><br/><span data-ttu-id="5940b-150">**ProductID**</span><span class="sxs-lookup"><span data-stu-id="5940b-150">**productId**</span></span><br/><span data-ttu-id="5940b-151">**productName**</span><span class="sxs-lookup"><span data-stu-id="5940b-151">**productName**</span></span> | <span data-ttu-id="5940b-152">No</span><span class="sxs-lookup"><span data-stu-id="5940b-152">No</span></span> |
| <span data-ttu-id="5940b-153">ölçütü</span><span class="sxs-lookup"><span data-stu-id="5940b-153">groupby</span></span>           | <span data-ttu-id="5940b-154">string</span><span class="sxs-lookup"><span data-stu-id="5940b-154">string</span></span>   | <span data-ttu-id="5940b-155">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="5940b-155">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="5940b-156">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="5940b-156">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="5940b-157">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="5940b-157">**workloadCode**</span></span><br/><span data-ttu-id="5940b-158">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="5940b-158">**workloadName**</span></span><br/><span data-ttu-id="5940b-159">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="5940b-159">**serviceCode**</span></span><br/><span data-ttu-id="5940b-160">**HizmetAdı**</span><span class="sxs-lookup"><span data-stu-id="5940b-160">**serviceName**</span></span><br/><span data-ttu-id="5940b-161">**Channelcustomertenantıd**</span><span class="sxs-lookup"><span data-stu-id="5940b-161">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="5940b-162">**customerName**</span><span class="sxs-lookup"><span data-stu-id="5940b-162">**customerName**</span></span><br/><span data-ttu-id="5940b-163">**ProductID**</span><span class="sxs-lookup"><span data-stu-id="5940b-163">**productId**</span></span><br/><span data-ttu-id="5940b-164">**productName**</span><span class="sxs-lookup"><span data-stu-id="5940b-164">**productName**</span></span><br/><br/><span data-ttu-id="5940b-165">Döndürülen veri satırları, *GroupBy* parametresinde belirtilen alanları ve aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="5940b-165">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="5940b-166">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="5940b-166">**licensesActive**</span></span><br/><span data-ttu-id="5940b-167">**Lisans nitelikli**</span><span class="sxs-lookup"><span data-stu-id="5940b-167">**licensesQualified**</span></span> | <span data-ttu-id="5940b-168">No</span><span class="sxs-lookup"><span data-stu-id="5940b-168">No</span></span> |
| <span data-ttu-id="5940b-169">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="5940b-169">processedDateTime</span></span> | <span data-ttu-id="5940b-170">DateTime</span><span class="sxs-lookup"><span data-stu-id="5940b-170">DateTime</span></span> | <span data-ttu-id="5940b-171">Bunlardan biri, kullanım verilerinin işlendiği tarihi belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="5940b-171">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="5940b-172">Verilerin işlendiği tarih varsayılan olarak en geç</span><span class="sxs-lookup"><span data-stu-id="5940b-172">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="5940b-173">No</span><span class="sxs-lookup"><span data-stu-id="5940b-173">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="5940b-174">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5940b-174">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5940b-175">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5940b-175">REST response</span></span>

<span data-ttu-id="5940b-176">Başarılı olursa, yanıt gövdesi, lisans kullanımı hakkında veri içeren aşağıdaki alanları içerir.</span><span class="sxs-lookup"><span data-stu-id="5940b-176">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="5940b-177">Alan</span><span class="sxs-lookup"><span data-stu-id="5940b-177">Field</span></span>             | <span data-ttu-id="5940b-178">Tür</span><span class="sxs-lookup"><span data-stu-id="5940b-178">Type</span></span>     | <span data-ttu-id="5940b-179">Description</span><span class="sxs-lookup"><span data-stu-id="5940b-179">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="5940b-180">workloadCode</span><span class="sxs-lookup"><span data-stu-id="5940b-180">workloadCode</span></span>      | <span data-ttu-id="5940b-181">string</span><span class="sxs-lookup"><span data-stu-id="5940b-181">string</span></span>   | <span data-ttu-id="5940b-182">İş yükü kodu</span><span class="sxs-lookup"><span data-stu-id="5940b-182">Workload code</span></span>                                 |
| <span data-ttu-id="5940b-183">workloadName</span><span class="sxs-lookup"><span data-stu-id="5940b-183">workloadName</span></span>      | <span data-ttu-id="5940b-184">string</span><span class="sxs-lookup"><span data-stu-id="5940b-184">string</span></span>   | <span data-ttu-id="5940b-185">İş yükü adı</span><span class="sxs-lookup"><span data-stu-id="5940b-185">Workload name</span></span>                                 |
| <span data-ttu-id="5940b-186">serviceCode</span><span class="sxs-lookup"><span data-stu-id="5940b-186">serviceCode</span></span>       | <span data-ttu-id="5940b-187">string</span><span class="sxs-lookup"><span data-stu-id="5940b-187">string</span></span>   | <span data-ttu-id="5940b-188">Hizmet kodu</span><span class="sxs-lookup"><span data-stu-id="5940b-188">Service code</span></span>                                  |
| <span data-ttu-id="5940b-189">HizmetAdı</span><span class="sxs-lookup"><span data-stu-id="5940b-189">serviceName</span></span>       | <span data-ttu-id="5940b-190">string</span><span class="sxs-lookup"><span data-stu-id="5940b-190">string</span></span>   | <span data-ttu-id="5940b-191">Hizmet adı</span><span class="sxs-lookup"><span data-stu-id="5940b-191">Service name</span></span>                                  |
| <span data-ttu-id="5940b-192">kanalla</span><span class="sxs-lookup"><span data-stu-id="5940b-192">channel</span></span>           | <span data-ttu-id="5940b-193">string</span><span class="sxs-lookup"><span data-stu-id="5940b-193">string</span></span>   | <span data-ttu-id="5940b-194">Kanal adı, satıcı</span><span class="sxs-lookup"><span data-stu-id="5940b-194">Channel name, reseller</span></span>                        |
| <span data-ttu-id="5940b-195">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="5940b-195">customerTenantId</span></span>  | <span data-ttu-id="5940b-196">string</span><span class="sxs-lookup"><span data-stu-id="5940b-196">string</span></span>   | <span data-ttu-id="5940b-197">Müşteri için benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="5940b-197">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="5940b-198">customerName</span><span class="sxs-lookup"><span data-stu-id="5940b-198">customerName</span></span>      | <span data-ttu-id="5940b-199">string</span><span class="sxs-lookup"><span data-stu-id="5940b-199">string</span></span>   | <span data-ttu-id="5940b-200">Müşteri adı</span><span class="sxs-lookup"><span data-stu-id="5940b-200">Customer name</span></span>                                 |
| <span data-ttu-id="5940b-201">productId</span><span class="sxs-lookup"><span data-stu-id="5940b-201">productId</span></span>         | <span data-ttu-id="5940b-202">string</span><span class="sxs-lookup"><span data-stu-id="5940b-202">string</span></span>   | <span data-ttu-id="5940b-203">Ürün için benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="5940b-203">Unique identifier for the product</span></span>             |
| <span data-ttu-id="5940b-204">productName</span><span class="sxs-lookup"><span data-stu-id="5940b-204">productName</span></span>       | <span data-ttu-id="5940b-205">string</span><span class="sxs-lookup"><span data-stu-id="5940b-205">string</span></span>   | <span data-ttu-id="5940b-206">Ürün adı</span><span class="sxs-lookup"><span data-stu-id="5940b-206">Product name</span></span>                                  |
| <span data-ttu-id="5940b-207">licensesActive</span><span class="sxs-lookup"><span data-stu-id="5940b-207">licensesActive</span></span>    | <span data-ttu-id="5940b-208">long</span><span class="sxs-lookup"><span data-stu-id="5940b-208">long</span></span>     | <span data-ttu-id="5940b-209">İş yükü başına etkin lisans sayısı</span><span class="sxs-lookup"><span data-stu-id="5940b-209">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="5940b-210">Lisans nitelikli</span><span class="sxs-lookup"><span data-stu-id="5940b-210">licensesQualified</span></span> | <span data-ttu-id="5940b-211">long</span><span class="sxs-lookup"><span data-stu-id="5940b-211">long</span></span>     | <span data-ttu-id="5940b-212">İş yükü için uygun lisans sayısı</span><span class="sxs-lookup"><span data-stu-id="5940b-212">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="5940b-213">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="5940b-213">processedDateTime</span></span> | <span data-ttu-id="5940b-214">DateTime</span><span class="sxs-lookup"><span data-stu-id="5940b-214">DateTime</span></span> | <span data-ttu-id="5940b-215">Verilerin son işlendiği tarih</span><span class="sxs-lookup"><span data-stu-id="5940b-215">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5940b-216">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5940b-216">Response success and error codes</span></span>

<span data-ttu-id="5940b-217">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5940b-217">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5940b-218">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5940b-218">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5940b-219">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5940b-219">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5940b-220">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5940b-220">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 487
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CV: f0trvmq8mEScHcFS.0
MS-ServerId: 4
Date: Wed, 24 Oct 2018 22:37:18 GMT

{
"Value": [
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "SPO",
      "workloadName": "SharePoint",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
      "productName": "OFFICE 365 ENTERPRISE E3",
      "licenseActive": 0,
      "licensesQualified": 1
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "workloadCode": "EXO",
      "workloadName": "Exchange",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "45A2423B-E884-448D-A831-D9E139C52D2F",
      "productName": "EXCHANGE ONLINE PROTECTION",
      "licenseActive": 0,
      "licensesQualified": 1
    }
}
```
