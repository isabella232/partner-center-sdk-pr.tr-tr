---
title: Lisans kullanım bilgilerini alma
description: Office dynamics için iş yükü düzeyinde lisans kullanım bilgilerini alın.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea3658089ce7eb5c1ad7cc65c3db34f9b6353cdd
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445995"
---
# <a name="get-licenses-usage-information"></a><span data-ttu-id="94f59-103">Lisans kullanım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="94f59-103">Get licenses usage information</span></span>

<span data-ttu-id="94f59-104">Office dynamics için iş yükü düzeyinde lisans kullanım bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="94f59-104">How to get licenses usage information at the workload level for Office and Dynamics.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94f59-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="94f59-105">Prerequisites</span></span>

<span data-ttu-id="94f59-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="94f59-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="94f59-107">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="94f59-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="94f59-108">REST isteği</span><span class="sxs-lookup"><span data-stu-id="94f59-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="94f59-109">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="94f59-109">Request syntax</span></span>

| <span data-ttu-id="94f59-110">Yöntem</span><span class="sxs-lookup"><span data-stu-id="94f59-110">Method</span></span>  | <span data-ttu-id="94f59-111">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="94f59-111">Request URI</span></span>                                                                                |
|---------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="94f59-112">**Al**</span><span class="sxs-lookup"><span data-stu-id="94f59-112">**GET**</span></span> | <span data-ttu-id="94f59-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="94f59-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/usage/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="94f59-114">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="94f59-114">Request headers</span></span>

<span data-ttu-id="94f59-115">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="94f59-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="94f59-116">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="94f59-116">URI parameters</span></span>

| <span data-ttu-id="94f59-117">Parametre</span><span class="sxs-lookup"><span data-stu-id="94f59-117">Parameter</span></span>         | <span data-ttu-id="94f59-118">Tür</span><span class="sxs-lookup"><span data-stu-id="94f59-118">Type</span></span>     | <span data-ttu-id="94f59-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94f59-119">Description</span></span> | <span data-ttu-id="94f59-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="94f59-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="94f59-121">top</span><span class="sxs-lookup"><span data-stu-id="94f59-121">top</span></span>               | <span data-ttu-id="94f59-122">string</span><span class="sxs-lookup"><span data-stu-id="94f59-122">string</span></span>   | <span data-ttu-id="94f59-123">İstekte geri dönecek veri satırlarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="94f59-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="94f59-124">Belirtilmezse en büyük değer ve varsayılan değer 10000'tir.</span><span class="sxs-lookup"><span data-stu-id="94f59-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="94f59-125">Sorguda daha fazla satır varsa yanıt gövdesi, sonraki veri sayfasını talep etmek için kullanabileceğiniz bir sonraki bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="94f59-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="94f59-126">Hayır</span><span class="sxs-lookup"><span data-stu-id="94f59-126">No</span></span> |
| <span data-ttu-id="94f59-127">Atla</span><span class="sxs-lookup"><span data-stu-id="94f59-127">skip</span></span>              | <span data-ttu-id="94f59-128">int</span><span class="sxs-lookup"><span data-stu-id="94f59-128">int</span></span>      | <span data-ttu-id="94f59-129">Sorguda atlana satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="94f59-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="94f59-130">Büyük veri kümelerini sayfalara yapmak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="94f59-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="94f59-131">Örneğin, top=10000 ve skip=0 ilk 10000 veri satırlarını, top=10000 ve skip=10000 sonraki 10000 satırı ve bu şekilde devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="94f59-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="94f59-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="94f59-132">No</span></span> |
| <span data-ttu-id="94f59-133">filtre</span><span class="sxs-lookup"><span data-stu-id="94f59-133">filter</span></span>            | <span data-ttu-id="94f59-134">string</span><span class="sxs-lookup"><span data-stu-id="94f59-134">string</span></span>   | <span data-ttu-id="94f59-135">*İsteğin* filtre parametresi, yanıtta satırları filtreleen bir veya daha fazla deyim içerir.</span><span class="sxs-lookup"><span data-stu-id="94f59-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="94f59-136">Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir ve **`eq`** **`ne`** deyimleri veya kullanılarak bir **`and`** araya **`or`** olabilir.</span><span class="sxs-lookup"><span data-stu-id="94f59-136">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators, and statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="94f59-137">Bazı örnek filtre *parametreleri şu* şekildedir:</span><span class="sxs-lookup"><span data-stu-id="94f59-137">Here are some example *filter* parameters:</span></span><br/><br/><span data-ttu-id="94f59-138">*filter=workloadCode eq 'SFB'*</span><span class="sxs-lookup"><span data-stu-id="94f59-138">*filter=workloadCode eq 'SFB'*</span></span><br/><br/><span data-ttu-id="94f59-139">*filter=workloadCode eq 'SFB'* veya (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="94f59-139">*filter=workloadCode eq 'SFB'* or (*channel eq 'Reseller'*)</span></span><br/><br/><span data-ttu-id="94f59-140">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="94f59-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="94f59-141">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="94f59-141">**workloadCode**</span></span><br/><span data-ttu-id="94f59-142">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="94f59-142">**workloadName**</span></span><br/><span data-ttu-id="94f59-143">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="94f59-143">**serviceCode**</span></span><br/><span data-ttu-id="94f59-144">**Hizmetadı**</span><span class="sxs-lookup"><span data-stu-id="94f59-144">**serviceName**</span></span><br/><span data-ttu-id="94f59-145">**Kanal**</span><span class="sxs-lookup"><span data-stu-id="94f59-145">**channel**</span></span><br/><span data-ttu-id="94f59-146">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="94f59-146">**customerTenantId**</span></span><br/><span data-ttu-id="94f59-147">**Müşteriadı**</span><span class="sxs-lookup"><span data-stu-id="94f59-147">**customerName**</span></span><br/><span data-ttu-id="94f59-148">**Productıd**</span><span class="sxs-lookup"><span data-stu-id="94f59-148">**productId**</span></span><br/><span data-ttu-id="94f59-149">**Productname**</span><span class="sxs-lookup"><span data-stu-id="94f59-149">**productName**</span></span> | <span data-ttu-id="94f59-150">Hayır</span><span class="sxs-lookup"><span data-stu-id="94f59-150">No</span></span> |
| <span data-ttu-id="94f59-151">Groupby</span><span class="sxs-lookup"><span data-stu-id="94f59-151">groupby</span></span>           | <span data-ttu-id="94f59-152">string</span><span class="sxs-lookup"><span data-stu-id="94f59-152">string</span></span>   | <span data-ttu-id="94f59-153">Yalnızca belirtilen alanlara veri toplaması uygulanan bir deyim.</span><span class="sxs-lookup"><span data-stu-id="94f59-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="94f59-154">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="94f59-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="94f59-155">**workloadCode**</span><span class="sxs-lookup"><span data-stu-id="94f59-155">**workloadCode**</span></span><br/><span data-ttu-id="94f59-156">**workloadName**</span><span class="sxs-lookup"><span data-stu-id="94f59-156">**workloadName**</span></span><br/><span data-ttu-id="94f59-157">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="94f59-157">**serviceCode**</span></span><br/><span data-ttu-id="94f59-158">**Hizmetadı**</span><span class="sxs-lookup"><span data-stu-id="94f59-158">**serviceName**</span></span><br/><span data-ttu-id="94f59-159">**channelcustomerTenantId**</span><span class="sxs-lookup"><span data-stu-id="94f59-159">**channelcustomerTenantId**</span></span><br/><span data-ttu-id="94f59-160">**Müşteriadı**</span><span class="sxs-lookup"><span data-stu-id="94f59-160">**customerName**</span></span><br/><span data-ttu-id="94f59-161">**Productıd**</span><span class="sxs-lookup"><span data-stu-id="94f59-161">**productId**</span></span><br/><span data-ttu-id="94f59-162">**Productname**</span><span class="sxs-lookup"><span data-stu-id="94f59-162">**productName**</span></span><br/><br/><span data-ttu-id="94f59-163">Döndürülen veri satırları *groupby* parametresinde belirtilen alanları ve şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="94f59-163">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="94f59-164">**licensesActive**</span><span class="sxs-lookup"><span data-stu-id="94f59-164">**licensesActive**</span></span><br/><span data-ttu-id="94f59-165">**licensesQualified**</span><span class="sxs-lookup"><span data-stu-id="94f59-165">**licensesQualified**</span></span> | <span data-ttu-id="94f59-166">Hayır</span><span class="sxs-lookup"><span data-stu-id="94f59-166">No</span></span> |
| <span data-ttu-id="94f59-167">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="94f59-167">processedDateTime</span></span> | <span data-ttu-id="94f59-168">DateTime</span><span class="sxs-lookup"><span data-stu-id="94f59-168">DateTime</span></span> | <span data-ttu-id="94f59-169">Kullanım verileri işlenme tarihini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94f59-169">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="94f59-170">Verilerin işlenme tarihi varsayılan olarak en son tarihtir</span><span class="sxs-lookup"><span data-stu-id="94f59-170">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="94f59-171">Hayır</span><span class="sxs-lookup"><span data-stu-id="94f59-171">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="94f59-172">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="94f59-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/usage/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="94f59-173">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="94f59-173">REST response</span></span>

<span data-ttu-id="94f59-174">Başarılı olursa, yanıt gövdesi lisans kullanımıyla ilgili verileri içeren aşağıdaki alanları içerir.</span><span class="sxs-lookup"><span data-stu-id="94f59-174">If successful, the response body contains the following fields containing data about licenses usage.</span></span>

| <span data-ttu-id="94f59-175">Alan</span><span class="sxs-lookup"><span data-stu-id="94f59-175">Field</span></span>             | <span data-ttu-id="94f59-176">Tür</span><span class="sxs-lookup"><span data-stu-id="94f59-176">Type</span></span>     | <span data-ttu-id="94f59-177">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94f59-177">Description</span></span>                                   |
|-------------------|----------|-----------------------------------------------|
| <span data-ttu-id="94f59-178">workloadCode</span><span class="sxs-lookup"><span data-stu-id="94f59-178">workloadCode</span></span>      | <span data-ttu-id="94f59-179">string</span><span class="sxs-lookup"><span data-stu-id="94f59-179">string</span></span>   | <span data-ttu-id="94f59-180">İş yükü kodu</span><span class="sxs-lookup"><span data-stu-id="94f59-180">Workload code</span></span>                                 |
| <span data-ttu-id="94f59-181">workloadName</span><span class="sxs-lookup"><span data-stu-id="94f59-181">workloadName</span></span>      | <span data-ttu-id="94f59-182">string</span><span class="sxs-lookup"><span data-stu-id="94f59-182">string</span></span>   | <span data-ttu-id="94f59-183">İş yükü adı</span><span class="sxs-lookup"><span data-stu-id="94f59-183">Workload name</span></span>                                 |
| <span data-ttu-id="94f59-184">serviceCode</span><span class="sxs-lookup"><span data-stu-id="94f59-184">serviceCode</span></span>       | <span data-ttu-id="94f59-185">string</span><span class="sxs-lookup"><span data-stu-id="94f59-185">string</span></span>   | <span data-ttu-id="94f59-186">Hizmet kodu</span><span class="sxs-lookup"><span data-stu-id="94f59-186">Service code</span></span>                                  |
| <span data-ttu-id="94f59-187">Hizmetadı</span><span class="sxs-lookup"><span data-stu-id="94f59-187">serviceName</span></span>       | <span data-ttu-id="94f59-188">string</span><span class="sxs-lookup"><span data-stu-id="94f59-188">string</span></span>   | <span data-ttu-id="94f59-189">Hizmet adı</span><span class="sxs-lookup"><span data-stu-id="94f59-189">Service name</span></span>                                  |
| <span data-ttu-id="94f59-190">Kanal</span><span class="sxs-lookup"><span data-stu-id="94f59-190">channel</span></span>           | <span data-ttu-id="94f59-191">string</span><span class="sxs-lookup"><span data-stu-id="94f59-191">string</span></span>   | <span data-ttu-id="94f59-192">Kanal adı, kurumsal bayi</span><span class="sxs-lookup"><span data-stu-id="94f59-192">Channel name, reseller</span></span>                        |
| <span data-ttu-id="94f59-193">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="94f59-193">customerTenantId</span></span>  | <span data-ttu-id="94f59-194">string</span><span class="sxs-lookup"><span data-stu-id="94f59-194">string</span></span>   | <span data-ttu-id="94f59-195">Müşterinin benzersiz tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="94f59-195">Unique identifier for the customer</span></span>            |
| <span data-ttu-id="94f59-196">Müşteriadı</span><span class="sxs-lookup"><span data-stu-id="94f59-196">customerName</span></span>      | <span data-ttu-id="94f59-197">string</span><span class="sxs-lookup"><span data-stu-id="94f59-197">string</span></span>   | <span data-ttu-id="94f59-198">Müşteri adı</span><span class="sxs-lookup"><span data-stu-id="94f59-198">Customer name</span></span>                                 |
| <span data-ttu-id="94f59-199">productId</span><span class="sxs-lookup"><span data-stu-id="94f59-199">productId</span></span>         | <span data-ttu-id="94f59-200">string</span><span class="sxs-lookup"><span data-stu-id="94f59-200">string</span></span>   | <span data-ttu-id="94f59-201">Ürün için benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="94f59-201">Unique identifier for the product</span></span>             |
| <span data-ttu-id="94f59-202">productName</span><span class="sxs-lookup"><span data-stu-id="94f59-202">productName</span></span>       | <span data-ttu-id="94f59-203">string</span><span class="sxs-lookup"><span data-stu-id="94f59-203">string</span></span>   | <span data-ttu-id="94f59-204">Ürün adı</span><span class="sxs-lookup"><span data-stu-id="94f59-204">Product name</span></span>                                  |
| <span data-ttu-id="94f59-205">licensesActive</span><span class="sxs-lookup"><span data-stu-id="94f59-205">licensesActive</span></span>    | <span data-ttu-id="94f59-206">long</span><span class="sxs-lookup"><span data-stu-id="94f59-206">long</span></span>     | <span data-ttu-id="94f59-207">İş yükü başına etkin lisans sayısı</span><span class="sxs-lookup"><span data-stu-id="94f59-207">Number of active licenses per workload</span></span>        |
| <span data-ttu-id="94f59-208">Lisans nitelikli</span><span class="sxs-lookup"><span data-stu-id="94f59-208">licensesQualified</span></span> | <span data-ttu-id="94f59-209">long</span><span class="sxs-lookup"><span data-stu-id="94f59-209">long</span></span>     | <span data-ttu-id="94f59-210">İş yükü için uygun lisans sayısı</span><span class="sxs-lookup"><span data-stu-id="94f59-210">Number of qualified licenses for the workload</span></span> |
| <span data-ttu-id="94f59-211">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="94f59-211">processedDateTime</span></span> | <span data-ttu-id="94f59-212">DateTime</span><span class="sxs-lookup"><span data-stu-id="94f59-212">DateTime</span></span> | <span data-ttu-id="94f59-213">Verilerin son işlendiği tarih</span><span class="sxs-lookup"><span data-stu-id="94f59-213">Date when the data was last processed</span></span>         |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="94f59-214">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="94f59-214">Response success and error codes</span></span>

<span data-ttu-id="94f59-215">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="94f59-215">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="94f59-216">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="94f59-216">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="94f59-217">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="94f59-217">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="94f59-218">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="94f59-218">Response example</span></span>

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
