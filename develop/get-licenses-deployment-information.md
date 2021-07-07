---
title: Lisans dağıtım bilgilerini alma
description: Office ve Dynamics lisansları için dağıtım bilgilerini alın.
ms.date: 10/25/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9eb0dc655affb2216b11635e58e00ed6464d6792
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445672"
---
# <a name="get-licenses-deployment-information"></a><span data-ttu-id="dc09f-103">Lisans dağıtım bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="dc09f-103">Get licenses deployment information</span></span>

<span data-ttu-id="dc09f-104">Office ve Dynamics lisansları için dağıtım bilgilerini alın.</span><span class="sxs-lookup"><span data-stu-id="dc09f-104">How to get deployment information for Office and Dynamics licenses.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="dc09f-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="dc09f-105">Prerequisites</span></span>

<span data-ttu-id="dc09f-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="dc09f-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="dc09f-107">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="dc09f-107">This scenario supports authentication with App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="dc09f-108">REST isteği</span><span class="sxs-lookup"><span data-stu-id="dc09f-108">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="dc09f-109">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="dc09f-109">Request syntax</span></span>

| <span data-ttu-id="dc09f-110">Yöntem</span><span class="sxs-lookup"><span data-stu-id="dc09f-110">Method</span></span>  | <span data-ttu-id="dc09f-111">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="dc09f-111">Request URI</span></span>                                                                                     |
|---------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="dc09f-112">**Al**</span><span class="sxs-lookup"><span data-stu-id="dc09f-112">**GET**</span></span> | <span data-ttu-id="dc09f-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="dc09f-113">[*{baseURL}*](partner-center-rest-urls.md)/v1/analytics/commercial/deployment/license/ HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="dc09f-114">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="dc09f-114">Request headers</span></span>

<span data-ttu-id="dc09f-115">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="dc09f-115">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="uri-parameters"></a><span data-ttu-id="dc09f-116">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="dc09f-116">URI parameters</span></span>

| <span data-ttu-id="dc09f-117">Parametre</span><span class="sxs-lookup"><span data-stu-id="dc09f-117">Parameter</span></span>         | <span data-ttu-id="dc09f-118">Tür</span><span class="sxs-lookup"><span data-stu-id="dc09f-118">Type</span></span>     | <span data-ttu-id="dc09f-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="dc09f-119">Description</span></span> | <span data-ttu-id="dc09f-120">Gerekli</span><span class="sxs-lookup"><span data-stu-id="dc09f-120">Required</span></span> |
|-------------------|----------|-------------|----------|
| <span data-ttu-id="dc09f-121">top</span><span class="sxs-lookup"><span data-stu-id="dc09f-121">top</span></span>               | <span data-ttu-id="dc09f-122">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-122">string</span></span>   | <span data-ttu-id="dc09f-123">İstekte geri dönecek veri satırlarının sayısı.</span><span class="sxs-lookup"><span data-stu-id="dc09f-123">The number of rows of data to return in the request.</span></span> <span data-ttu-id="dc09f-124">Belirtilmezse en büyük değer ve varsayılan değer 10000'tir.</span><span class="sxs-lookup"><span data-stu-id="dc09f-124">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="dc09f-125">Sorguda daha fazla satır varsa yanıt gövdesi, sonraki veri sayfasını talep etmek için kullanabileceğiniz bir sonraki bağlantı içerir.</span><span class="sxs-lookup"><span data-stu-id="dc09f-125">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> | <span data-ttu-id="dc09f-126">Hayır</span><span class="sxs-lookup"><span data-stu-id="dc09f-126">No</span></span> |
| <span data-ttu-id="dc09f-127">Atla</span><span class="sxs-lookup"><span data-stu-id="dc09f-127">skip</span></span>              | <span data-ttu-id="dc09f-128">int</span><span class="sxs-lookup"><span data-stu-id="dc09f-128">int</span></span>      | <span data-ttu-id="dc09f-129">Sorguda atlana satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="dc09f-129">The number of rows to skip in the query.</span></span> <span data-ttu-id="dc09f-130">Büyük veri kümelerini sayfalara yapmak için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="dc09f-130">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="dc09f-131">Örneğin, top=10000 ve skip=0 ilk 10000 veri satırlarını, top=10000 ve skip=10000 sonraki 10000 satırı ve bu şekilde devam ediyor.</span><span class="sxs-lookup"><span data-stu-id="dc09f-131">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data, and so on.</span></span> | <span data-ttu-id="dc09f-132">Hayır</span><span class="sxs-lookup"><span data-stu-id="dc09f-132">No</span></span> |
| <span data-ttu-id="dc09f-133">filtre</span><span class="sxs-lookup"><span data-stu-id="dc09f-133">filter</span></span>            | <span data-ttu-id="dc09f-134">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-134">string</span></span>   | <span data-ttu-id="dc09f-135">*İsteğin* filtre parametresi, yanıtta satırları filtreleen bir veya daha fazla deyim içerir.</span><span class="sxs-lookup"><span data-stu-id="dc09f-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="dc09f-136">Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir ve `eq` `ne` deyimleri veya kullanılarak bir `and` araya `or` olabilir.</span><span class="sxs-lookup"><span data-stu-id="dc09f-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="dc09f-137">Bazı örnek filtre *parametreleri şu* şekildedir:</span><span class="sxs-lookup"><span data-stu-id="dc09f-137">Here are some example *filter* parameters:</span></span><br/><br/> <span data-ttu-id="dc09f-138">*filter=serviceCode eq 'O365'*</span><span class="sxs-lookup"><span data-stu-id="dc09f-138">*filter=serviceCode eq 'O365'*</span></span><br/> <span data-ttu-id="dc09f-139">*filter=serviceCode eq 'O365'* veya (*channel eq 'Reseller'*)</span><span class="sxs-lookup"><span data-stu-id="dc09f-139">*filter=serviceCode eq 'O365'* or (*channel eq 'Reseller'*)</span></span><br/><br/> <span data-ttu-id="dc09f-140">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dc09f-140">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="dc09f-141">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="dc09f-141">**serviceCode**</span></span><br/><span data-ttu-id="dc09f-142">**Hizmetadı**</span><span class="sxs-lookup"><span data-stu-id="dc09f-142">**serviceName**</span></span><br/><span data-ttu-id="dc09f-143">**Kanal**</span><span class="sxs-lookup"><span data-stu-id="dc09f-143">**channel**</span></span><br/><span data-ttu-id="dc09f-144">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="dc09f-144">**customerTenantId**</span></span><br/><span data-ttu-id="dc09f-145">**Müşteriadı**</span><span class="sxs-lookup"><span data-stu-id="dc09f-145">**customerName**</span></span><br/><span data-ttu-id="dc09f-146">**Productıd**</span><span class="sxs-lookup"><span data-stu-id="dc09f-146">**productId**</span></span><br/><span data-ttu-id="dc09f-147">**Productname**</span><span class="sxs-lookup"><span data-stu-id="dc09f-147">**productName**</span></span>  | <span data-ttu-id="dc09f-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="dc09f-148">No</span></span> |
| <span data-ttu-id="dc09f-149">Groupby</span><span class="sxs-lookup"><span data-stu-id="dc09f-149">groupby</span></span>           | <span data-ttu-id="dc09f-150">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-150">string</span></span>   | <span data-ttu-id="dc09f-151">Yalnızca belirtilen alanlara veri toplaması uygulanan bir deyim.</span><span class="sxs-lookup"><span data-stu-id="dc09f-151">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="dc09f-152">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="dc09f-152">You can specify the following fields:</span></span><br/><br/><span data-ttu-id="dc09f-153">**serviceCode**</span><span class="sxs-lookup"><span data-stu-id="dc09f-153">**serviceCode**</span></span><br/><span data-ttu-id="dc09f-154">**Hizmetadı**</span><span class="sxs-lookup"><span data-stu-id="dc09f-154">**serviceName**</span></span><br/><span data-ttu-id="dc09f-155">**Kanal**</span><span class="sxs-lookup"><span data-stu-id="dc09f-155">**channel**</span></span><br/><span data-ttu-id="dc09f-156">**customerTenantId**</span><span class="sxs-lookup"><span data-stu-id="dc09f-156">**customerTenantId**</span></span><br/><span data-ttu-id="dc09f-157">**Müşteriadı**</span><span class="sxs-lookup"><span data-stu-id="dc09f-157">**customerName**</span></span><br/><span data-ttu-id="dc09f-158">**Productıd**</span><span class="sxs-lookup"><span data-stu-id="dc09f-158">**productId**</span></span><br/><span data-ttu-id="dc09f-159">**Productname**</span><span class="sxs-lookup"><span data-stu-id="dc09f-159">**productName**</span></span><br/><br/> <span data-ttu-id="dc09f-160">Döndürülen veri satırları *groupby* parametresinde belirtilen alanları ve şunları içerir:</span><span class="sxs-lookup"><span data-stu-id="dc09f-160">The returned data rows will contain the fields specified in the *groupby* parameter and the following:</span></span><br/><br/><span data-ttu-id="dc09f-161">**dağıtılan lisanslar**</span><span class="sxs-lookup"><span data-stu-id="dc09f-161">**licensesDeployed**</span></span><br/><span data-ttu-id="dc09f-162">**licensesSold**</span><span class="sxs-lookup"><span data-stu-id="dc09f-162">**licensesSold**</span></span>  | <span data-ttu-id="dc09f-163">Hayır</span><span class="sxs-lookup"><span data-stu-id="dc09f-163">No</span></span> |
| <span data-ttu-id="dc09f-164">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="dc09f-164">processedDateTime</span></span> | <span data-ttu-id="dc09f-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="dc09f-165">DateTime</span></span> | <span data-ttu-id="dc09f-166">Kullanım verileri işlenme tarihini belirtebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="dc09f-166">One can specify the date from which usage data was processed.</span></span> <span data-ttu-id="dc09f-167">Verilerin işlenme tarihi varsayılan olarak en son tarihtir</span><span class="sxs-lookup"><span data-stu-id="dc09f-167">Defaults to the latest date when the data was processed</span></span> | <span data-ttu-id="dc09f-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="dc09f-168">No</span></span> |

### <a name="request-example"></a><span data-ttu-id="dc09f-169">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="dc09f-169">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/commercial/deployment/license?filter=customerTenantId%20eq%20%270112A436-B14E-4888-967B-CA4BB2CF1234%27 HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: bad5f75f-fd44-43ab-9325-bbc79dcba9da
MS-CorrelationId: 9cbdf63c-2608-4ad8-b0a9-abae27d859d9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="dc09f-170">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="dc09f-170">REST response</span></span>

<span data-ttu-id="dc09f-171">Başarılı olursa, yanıt gövdesi dağıtılan lisanslar hakkında verileri içeren aşağıdaki alanları içerir.</span><span class="sxs-lookup"><span data-stu-id="dc09f-171">If successful, the response body contains the following fields containing data about the licenses deployed.</span></span>

| <span data-ttu-id="dc09f-172">Alan</span><span class="sxs-lookup"><span data-stu-id="dc09f-172">Field</span></span>             | <span data-ttu-id="dc09f-173">Tür</span><span class="sxs-lookup"><span data-stu-id="dc09f-173">Type</span></span>     | <span data-ttu-id="dc09f-174">Açıklama</span><span class="sxs-lookup"><span data-stu-id="dc09f-174">Description</span></span>                           |
|-------------------|----------|---------------------------------------|
| <span data-ttu-id="dc09f-175">serviceCode</span><span class="sxs-lookup"><span data-stu-id="dc09f-175">serviceCode</span></span>       | <span data-ttu-id="dc09f-176">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-176">string</span></span>   | <span data-ttu-id="dc09f-177">Hizmet kodu</span><span class="sxs-lookup"><span data-stu-id="dc09f-177">Service code</span></span>                          |
| <span data-ttu-id="dc09f-178">Hizmetadı</span><span class="sxs-lookup"><span data-stu-id="dc09f-178">serviceName</span></span>       | <span data-ttu-id="dc09f-179">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-179">string</span></span>   | <span data-ttu-id="dc09f-180">Hizmet adı</span><span class="sxs-lookup"><span data-stu-id="dc09f-180">Service name</span></span>                          |
| <span data-ttu-id="dc09f-181">Kanal</span><span class="sxs-lookup"><span data-stu-id="dc09f-181">channel</span></span>           | <span data-ttu-id="dc09f-182">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-182">string</span></span>   | <span data-ttu-id="dc09f-183">Kanal adı, kurumsal bayi</span><span class="sxs-lookup"><span data-stu-id="dc09f-183">Channel name, reseller</span></span>                |
| <span data-ttu-id="dc09f-184">customerTenantId</span><span class="sxs-lookup"><span data-stu-id="dc09f-184">customerTenantId</span></span>  | <span data-ttu-id="dc09f-185">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-185">string</span></span>   | <span data-ttu-id="dc09f-186">Müşterinin benzersiz tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="dc09f-186">Unique identifier for the customer</span></span>    |
| <span data-ttu-id="dc09f-187">Müşteriadı</span><span class="sxs-lookup"><span data-stu-id="dc09f-187">customerName</span></span>      | <span data-ttu-id="dc09f-188">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-188">string</span></span>   | <span data-ttu-id="dc09f-189">Müşteri adı</span><span class="sxs-lookup"><span data-stu-id="dc09f-189">Customer name</span></span>                         |
| <span data-ttu-id="dc09f-190">productId</span><span class="sxs-lookup"><span data-stu-id="dc09f-190">productId</span></span>         | <span data-ttu-id="dc09f-191">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-191">string</span></span>   | <span data-ttu-id="dc09f-192">Ürün için benzersiz tanımlayıcı</span><span class="sxs-lookup"><span data-stu-id="dc09f-192">Unique identifier for the product</span></span>     |
| <span data-ttu-id="dc09f-193">Productname</span><span class="sxs-lookup"><span data-stu-id="dc09f-193">productName</span></span>       | <span data-ttu-id="dc09f-194">string</span><span class="sxs-lookup"><span data-stu-id="dc09f-194">string</span></span>   | <span data-ttu-id="dc09f-195">Ürün adı</span><span class="sxs-lookup"><span data-stu-id="dc09f-195">Product name</span></span>                          |
| <span data-ttu-id="dc09f-196">dağıtılan lisanslar</span><span class="sxs-lookup"><span data-stu-id="dc09f-196">licensesDeployed</span></span>  | <span data-ttu-id="dc09f-197">long</span><span class="sxs-lookup"><span data-stu-id="dc09f-197">long</span></span>     | <span data-ttu-id="dc09f-198">Dağıtılan lisans sayısı</span><span class="sxs-lookup"><span data-stu-id="dc09f-198">Number of licenses deployed</span></span>           |
| <span data-ttu-id="dc09f-199">licensesSold</span><span class="sxs-lookup"><span data-stu-id="dc09f-199">licensesSold</span></span>      | <span data-ttu-id="dc09f-200">long</span><span class="sxs-lookup"><span data-stu-id="dc09f-200">long</span></span>     | <span data-ttu-id="dc09f-201">Satılan lisans sayısı</span><span class="sxs-lookup"><span data-stu-id="dc09f-201">Number of licenses sold</span></span>               |
| <span data-ttu-id="dc09f-202">processedDateTime</span><span class="sxs-lookup"><span data-stu-id="dc09f-202">processedDateTime</span></span> | <span data-ttu-id="dc09f-203">DateTime</span><span class="sxs-lookup"><span data-stu-id="dc09f-203">DateTime</span></span> | <span data-ttu-id="dc09f-204">Verilerin son işlenme tarihi</span><span class="sxs-lookup"><span data-stu-id="dc09f-204">Date when the data was last processed</span></span> |

### <a name="response-success-and-error-codes"></a><span data-ttu-id="dc09f-205">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="dc09f-205">Response success and error codes</span></span>

<span data-ttu-id="dc09f-206">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="dc09f-206">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="dc09f-207">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="dc09f-207">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="dc09f-208">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="dc09f-208">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="dc09f-209">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="dc09f-209">Response example</span></span>

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
