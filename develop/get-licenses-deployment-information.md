---
title: Lisans dağıtım bilgilerini alma
description: Office ve Dynamics lisanslarıyla ilgili dağıtım bilgilerini alma.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ef0e5d73d34bc51e4cc58143db6c9fc49cb58fcb
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769436"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="8f2cd-103">Lisans dağıtım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="8f2cd-103">Get licenses deployment information</span></span>

<span data-ttu-id="8f2cd-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-104">**Applies To**</span></span>

- <span data-ttu-id="8f2cd-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8f2cd-105">Partner Center</span></span>

<span data-ttu-id="8f2cd-106">Office ve Dynamics lisanslarıyla ilgili dağıtım bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-106">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f2cd-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8f2cd-107">Prerequisites</span></span>

<span data-ttu-id="8f2cd-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8f2cd-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="8f2cd-110">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8f2cd-110">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8f2cd-111">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8f2cd-111">Request syntax</span></span>

| <span data-ttu-id="8f2cd-112">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8f2cd-112">Method</span></span>  | <span data-ttu-id="8f2cd-113">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8f2cd-113">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8f2cd-114">**Al**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-114">**GET**</span></span> | <span data-ttu-id="8f2cd-115">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Analtics/, CIAL/Deployment/License/http/1.1</span><span class="sxs-lookup"><span data-stu-id="8f2cd-115">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8f2cd-116">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8f2cd-116">Request headers</span></span>

<span data-ttu-id="8f2cd-117">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8f2cd-117">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="8f2cd-118">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="8f2cd-118">URI parameters</span></span>

| <span data-ttu-id="8f2cd-119">Parametre</span><span class="sxs-lookup"><span data-stu-id="8f2cd-119">Parameter</span></span>         | <span data-ttu-id="8f2cd-120">Tür</span><span class="sxs-lookup"><span data-stu-id="8f2cd-120">Type</span></span>     | <span data-ttu-id="8f2cd-121">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8f2cd-121">Description</span></span> | <span data-ttu-id="8f2cd-122">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8f2cd-122">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="8f2cd-123">top</span><span class="sxs-lookup"><span data-stu-id="8f2cd-123">top</span></span>               | <span data-ttu-id="8f2cd-124">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-124">string</span></span>   | <span data-ttu-id="8f2cd-125">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="8f2cd-126">Belirtilen en büyük değer ve varsayılan değer 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="8f2cd-127">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="8f2cd-128">No</span><span class="sxs-lookup"><span data-stu-id="8f2cd-128">No</span></span> |
| <span data-ttu-id="8f2cd-129">Atla</span><span class="sxs-lookup"><span data-stu-id="8f2cd-129">skip</span></span>              | <span data-ttu-id="8f2cd-130">int</span><span class="sxs-lookup"><span data-stu-id="8f2cd-130">int</span></span>      | <span data-ttu-id="8f2cd-131">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="8f2cd-132">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="8f2cd-133">Örneğin, top = 10000 ve Skip = 0 verilerin ilk 10000 satırını alır, top = 10000 ve Skip = 10000 sonraki 10000 satırlık verileri alır ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-133">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="8f2cd-134">No</span><span class="sxs-lookup"><span data-stu-id="8f2cd-134">No</span></span> |
| <span data-ttu-id="8f2cd-135">filtre</span><span class="sxs-lookup"><span data-stu-id="8f2cd-135">filter</span></span>            | <span data-ttu-id="8f2cd-136">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-136">string</span></span>   | <span data-ttu-id="8f2cd-137">İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-137">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="8f2cd-138">Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir `eq` `ne` ve deyimler or kullanılarak birleştirilebilir `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="8f2cd-138">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="8f2cd-139">Aşağıda bazı örnek *filtre* parametreleri verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="8f2cd-139">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="8f2cd-140">*Filter = serviceCode EQ ' O365 '*</span><span class="sxs-lookup"><span data-stu-id="8f2cd-140">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="8f2cd-141">*Filter = serviceCode EQ ' O365 '* veya (*Channel EQ ' Bayi '*)</span><span class="sxs-lookup"><span data-stu-id="8f2cd-141">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="8f2cd-142">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8f2cd-142">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="8f2cd-143">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-143">**serviceCode**</span></span><br/><span data-ttu-id="8f2cd-144">**HizmetAdı**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-144">**serviceName**</span></span><br/><span data-ttu-id="8f2cd-145">**kanalla**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-145">**channel**</span></span><br/><span data-ttu-id="8f2cd-146">**Customertenantıd**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-146">**customerTenantId**</span></span><br/><span data-ttu-id="8f2cd-147">**customerName**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-147">**customerName**</span></span><br/><span data-ttu-id="8f2cd-148">**ProductID**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-148">**productId**</span></span><br/><span data-ttu-id="8f2cd-149">**productName**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-149">**productName**</span></span>  | <span data-ttu-id="8f2cd-150">No</span><span class="sxs-lookup"><span data-stu-id="8f2cd-150">No</span></span> |
| <span data-ttu-id="8f2cd-151">ölçütü</span><span class="sxs-lookup"><span data-stu-id="8f2cd-151">groupby</span></span>           | <span data-ttu-id="8f2cd-152">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-152">string</span></span>   | <span data-ttu-id="8f2cd-153">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="8f2cd-154">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="8f2cd-154">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="8f2cd-155">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-155">**serviceCode**</span></span><br/><span data-ttu-id="8f2cd-156">**HizmetAdı**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-156">**serviceName**</span></span><br/><span data-ttu-id="8f2cd-157">**kanalla**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-157">**channel**</span></span><br/><span data-ttu-id="8f2cd-158">**Customertenantıd**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-158">**customerTenantId**</span></span><br/><span data-ttu-id="8f2cd-159">**customerName**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-159">**customerName**</span></span><br/><span data-ttu-id="8f2cd-160">**ProductID**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-160">**productId**</span></span><br/><span data-ttu-id="8f2cd-161">**productName**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-161">**productName**</span></span><br/><br/> <span data-ttu-id="8f2cd-162">Döndürülen veri satırları, *GroupBy* parametresinde belirtilen alanları ve aşağıdakileri içerir:</span><span class="sxs-lookup"><span data-stu-id="8f2cd-162">The returned data rows will contain the fields specified in the *groupby* parameter as well as the following:</span></span><br/><br/><span data-ttu-id="8f2cd-163">**Licensesdağıtıldı**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-163">**licensesDeployed**</span></span><br/><span data-ttu-id="8f2cd-164">**Lisanssesseski**</span><span class="sxs-lookup"><span data-stu-id="8f2cd-164">**licensesSold**</span></span>  | <span data-ttu-id="8f2cd-165">No</span><span class="sxs-lookup"><span data-stu-id="8f2cd-165">No</span></span> |
| <span data-ttu-id="8f2cd-166">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="8f2cd-166">processedDateTime</span></span> | <span data-ttu-id="8f2cd-167">DateTime</span><span class="sxs-lookup"><span data-stu-id="8f2cd-167">DateTime</span></span> | <span data-ttu-id="8f2cd-168">Bunlardan biri, kullanım verilerinin işlendiği tarihi belirtebilir.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-168">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="8f2cd-169">Verilerin işlendiği tarih varsayılan olarak en geç</span><span class="sxs-lookup"><span data-stu-id="8f2cd-169">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="8f2cd-170">No</span><span class="sxs-lookup"><span data-stu-id="8f2cd-170">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="8f2cd-171">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8f2cd-171">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8f2cd-172">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-172">REST response</span></span>

<span data-ttu-id="8f2cd-173">Başarılı olursa, yanıt gövdesi dağıtılan lisanslar hakkında veri içeren aşağıdaki alanları içerir.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-173">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="8f2cd-174">Alan</span><span class="sxs-lookup"><span data-stu-id="8f2cd-174">Field</span></span>             | <span data-ttu-id="8f2cd-175">Tür</span><span class="sxs-lookup"><span data-stu-id="8f2cd-175">Type</span></span>     | <span data-ttu-id="8f2cd-176">Description</span><span class="sxs-lookup"><span data-stu-id="8f2cd-176">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="8f2cd-177">serviceCode</span><span class="sxs-lookup"><span data-stu-id="8f2cd-177">serviceCode</span></span>       | <span data-ttu-id="8f2cd-178">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-178">string</span></span>   | <span data-ttu-id="8f2cd-179">Hizmet kodu</span><span class="sxs-lookup"><span data-stu-id="8f2cd-179">Service code</span></span>                          |
| <span data-ttu-id="8f2cd-180">HizmetAdı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-180">serviceName</span></span>       | <span data-ttu-id="8f2cd-181">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-181">string</span></span>   | <span data-ttu-id="8f2cd-182">Hizmet adı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-182">Service name</span></span>                          |
| <span data-ttu-id="8f2cd-183">kanalla</span><span class="sxs-lookup"><span data-stu-id="8f2cd-183">channel</span></span>           | <span data-ttu-id="8f2cd-184">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-184">string</span></span>   | <span data-ttu-id="8f2cd-185">Kanal adı, satıcı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-185">Channel name, reseller</span></span>                |
| <span data-ttu-id="8f2cd-186">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="8f2cd-186">customerTenantId</span></span>  | <span data-ttu-id="8f2cd-187">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-187">string</span></span>   | <span data-ttu-id="8f2cd-188">Müşteri için benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-188">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="8f2cd-189">customerName</span><span class="sxs-lookup"><span data-stu-id="8f2cd-189">customerName</span></span>      | <span data-ttu-id="8f2cd-190">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-190">string</span></span>   | <span data-ttu-id="8f2cd-191">Müşteri adı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-191">Customer name</span></span>                         |
| <span data-ttu-id="8f2cd-192">productId</span><span class="sxs-lookup"><span data-stu-id="8f2cd-192">productId</span></span>         | <span data-ttu-id="8f2cd-193">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-193">string</span></span>   | <span data-ttu-id="8f2cd-194">Ürün için benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-194">Unique identifier for the product</span></span>     |
| <span data-ttu-id="8f2cd-195">productName</span><span class="sxs-lookup"><span data-stu-id="8f2cd-195">productName</span></span>       | <span data-ttu-id="8f2cd-196">string</span><span class="sxs-lookup"><span data-stu-id="8f2cd-196">string</span></span>   | <span data-ttu-id="8f2cd-197">Ürün adı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-197">Product name</span></span>                          |
| <span data-ttu-id="8f2cd-198">Licensesdağıtıldı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-198">licensesDeployed</span></span>  | <span data-ttu-id="8f2cd-199">long</span><span class="sxs-lookup"><span data-stu-id="8f2cd-199">long</span></span>     | <span data-ttu-id="8f2cd-200">Dağıtılan lisansların sayısı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-200">Number of licenses deployed</span></span>           |
| <span data-ttu-id="8f2cd-201">Lisanssesseski</span><span class="sxs-lookup"><span data-stu-id="8f2cd-201">licensesSold</span></span>      | <span data-ttu-id="8f2cd-202">long</span><span class="sxs-lookup"><span data-stu-id="8f2cd-202">long</span></span>     | <span data-ttu-id="8f2cd-203">Satılan lisansların sayısı</span><span class="sxs-lookup"><span data-stu-id="8f2cd-203">Number of licenses sold</span></span>               |
| <span data-ttu-id="8f2cd-204">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="8f2cd-204">processedDateTime</span></span> | <span data-ttu-id="8f2cd-205">DateTime</span><span class="sxs-lookup"><span data-stu-id="8f2cd-205">DateTime</span></span> | <span data-ttu-id="8f2cd-206">Verilerin son işlendiği tarih</span><span class="sxs-lookup"><span data-stu-id="8f2cd-206">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8f2cd-207">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8f2cd-207">Response success and error codes</span></span>

<span data-ttu-id="8f2cd-208">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-208">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8f2cd-209">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8f2cd-209">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8f2cd-210">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8f2cd-210">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8f2cd-211">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="8f2cd-211">Response example</span></span>

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
      "serviceCode": "crm",
      "serviceName": "Microsoft Dynamics",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "54B84594-9C77-4499-8D65-5E0D5F410E78",
      "productName": "DYNAMICS AX TASK",
      "licensesDeployed": 0,
      "licensesSold": 9
    },
    {
      "processedDateTime": "2018-10-14T00:00:00",
      "serviceCode": "o365",
      "serviceName": "Microsoft Office 365",
      "channel": "reseller",
      "customerTenantId": "0112A436-B14E-4888-967B-CA4BB2CF1234",
      "customerName": "TEST COMPANY",
      "productId": "D3B4FE1F-9992-4930-8ACB-CA6EC609365E",
      "productName": "DOMESTIC AND INTERNATIONAL CALLING PLAN",
      "licensesDeployed": 0,
      "licensesSold": 5
    }
],
  "@nextLink": null,
  "TotalCount": 2
}
```
