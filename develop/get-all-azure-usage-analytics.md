---
title: Tüm Azure kullanım analizi bilgilerini alma
description: Tüm Azure kullanım analizi bilgilerini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769442"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="3fd81-103">Tüm Azure kullanım analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="3fd81-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="3fd81-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="3fd81-104">**Applies To**</span></span>

- <span data-ttu-id="3fd81-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3fd81-105">Partner Center</span></span>
- <span data-ttu-id="3fd81-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3fd81-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3fd81-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3fd81-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3fd81-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3fd81-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3fd81-109">Müşterileriniz için tüm Azure kullanım analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="3fd81-109">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3fd81-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3fd81-110">Prerequisites</span></span>

- <span data-ttu-id="3fd81-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3fd81-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3fd81-112">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3fd81-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3fd81-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3fd81-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3fd81-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3fd81-114">Request syntax</span></span>

| <span data-ttu-id="3fd81-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3fd81-115">Method</span></span>  | <span data-ttu-id="3fd81-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3fd81-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="3fd81-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="3fd81-117">**GET**</span></span> | <span data-ttu-id="3fd81-118">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analysistics/Usage/Azure http/1.1</span><span class="sxs-lookup"><span data-stu-id="3fd81-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3fd81-119">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="3fd81-119">URI parameters</span></span>

|<span data-ttu-id="3fd81-120">Parametre</span><span class="sxs-lookup"><span data-stu-id="3fd81-120">Parameter</span></span>        |<span data-ttu-id="3fd81-121">Tür</span><span class="sxs-lookup"><span data-stu-id="3fd81-121">Type</span></span>                        |<span data-ttu-id="3fd81-122">Description</span><span class="sxs-lookup"><span data-stu-id="3fd81-122">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="3fd81-123">top</span><span class="sxs-lookup"><span data-stu-id="3fd81-123">top</span></span>              | <span data-ttu-id="3fd81-124">string</span><span class="sxs-lookup"><span data-stu-id="3fd81-124">string</span></span>                     | <span data-ttu-id="3fd81-125">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="3fd81-125">The number of rows of data to return in the request.</span></span> <span data-ttu-id="3fd81-126">Belirtilen en büyük değer ve varsayılan değer 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-126">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="3fd81-127">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-127">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="3fd81-128">Atla</span><span class="sxs-lookup"><span data-stu-id="3fd81-128">skip</span></span>             | <span data-ttu-id="3fd81-129">int</span><span class="sxs-lookup"><span data-stu-id="3fd81-129">int</span></span>                        | <span data-ttu-id="3fd81-130">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="3fd81-130">The number of rows to skip in the query.</span></span> <span data-ttu-id="3fd81-131">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fd81-131">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="3fd81-132">Örneğin, `top=10000 and skip=0` ilk 10000 veri satırını alır, `top=10000 and skip=10000` sonraki 10000 veri satırını alır ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="3fd81-132">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="3fd81-133">filtre</span><span class="sxs-lookup"><span data-stu-id="3fd81-133">filter</span></span>           | <span data-ttu-id="3fd81-134">string</span><span class="sxs-lookup"><span data-stu-id="3fd81-134">string</span></span>                     | <span data-ttu-id="3fd81-135">İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor.</span><span class="sxs-lookup"><span data-stu-id="3fd81-135">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="3fd81-136">Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir `eq` `ne` ve deyimler or kullanılarak birleştirilebilir `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="3fd81-136">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="3fd81-137">Aşağıdaki dizeleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3fd81-137">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="3fd81-138">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3fd81-138">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="3fd81-139">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3fd81-139">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="3fd81-140">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="3fd81-140">aggregationLevel</span></span> | <span data-ttu-id="3fd81-141">string</span><span class="sxs-lookup"><span data-stu-id="3fd81-141">string</span></span>                    | <span data-ttu-id="3fd81-142">Toplam verilerinin alınacağı zaman aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-142">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="3fd81-143">Aşağıdaki dizelerden biri olabilir: `day` , `week` , veya `month` .</span><span class="sxs-lookup"><span data-stu-id="3fd81-143">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="3fd81-144">Belirtilmemişse, varsayılan olur `day` .</span><span class="sxs-lookup"><span data-stu-id="3fd81-144">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="3fd81-145">`aggregationLevel`Parametresi, olmadan desteklenmez `groupby` .</span><span class="sxs-lookup"><span data-stu-id="3fd81-145">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="3fd81-146">`aggregationLevel`Parametresi, içinde bulunan tüm tarih alanları için geçerlidir `groupby` .</span><span class="sxs-lookup"><span data-stu-id="3fd81-146">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="3fd81-147">OrderBy</span><span class="sxs-lookup"><span data-stu-id="3fd81-147">orderby</span></span>          |<span data-ttu-id="3fd81-148">string</span><span class="sxs-lookup"><span data-stu-id="3fd81-148">string</span></span>                     | <span data-ttu-id="3fd81-149">Her bir yüklemenin sonuç verileri değerlerini sıralayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="3fd81-149">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="3fd81-150">Söz dizimi `...&orderby=field [order],field [order],...` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-150">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="3fd81-151">`field`Parametresi aşağıdaki dizelerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="3fd81-151">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="3fd81-152">*Order* parametresi isteğe bağlıdır ve `asc` `desc` sırasıyla her bir alan için artan veya azalan sıralama belirtmek için ya da olabilir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-152">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="3fd81-153">Varsayılan değer: `asc`.</span><span class="sxs-lookup"><span data-stu-id="3fd81-153">The default is `asc`.</span></span><br/><br/><span data-ttu-id="3fd81-154">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3fd81-154">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="3fd81-155">ölçütü</span><span class="sxs-lookup"><span data-stu-id="3fd81-155">groupby</span></span>          |<span data-ttu-id="3fd81-156">string</span><span class="sxs-lookup"><span data-stu-id="3fd81-156">string</span></span>                    | <span data-ttu-id="3fd81-157">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="3fd81-157">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="3fd81-158">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="3fd81-158">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="3fd81-159">Döndürülen veri satırları, parametresinde belirtilen alanları ve `groupby` *miktarı* içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-159">The returned data rows will contain the fields specified in the `groupby`  parameter as well as the *Quantity*.</span></span><br/><br/><span data-ttu-id="3fd81-160">`groupby`Parametresi parametresiyle birlikte kullanılabilir `aggregationLevel` .</span><span class="sxs-lookup"><span data-stu-id="3fd81-160">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="3fd81-161">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3fd81-161">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="3fd81-162">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3fd81-162">Request headers</span></span>

<span data-ttu-id="3fd81-163">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3fd81-163">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3fd81-164">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3fd81-164">Request body</span></span>

<span data-ttu-id="3fd81-165">Yok.</span><span class="sxs-lookup"><span data-stu-id="3fd81-165">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3fd81-166">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3fd81-166">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="3fd81-167">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3fd81-167">REST response</span></span>

<span data-ttu-id="3fd81-168">Başarılı olursa, yanıt gövdesi bir [Azure kullanım](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-168">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3fd81-169">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3fd81-169">Response success and error codes</span></span>

<span data-ttu-id="3fd81-170">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3fd81-170">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3fd81-171">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fd81-171">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3fd81-172">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3fd81-172">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3fd81-173">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3fd81-173">Response example</span></span>

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a><span data-ttu-id="3fd81-174">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3fd81-174">See also</span></span>

- [<span data-ttu-id="3fd81-175">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3fd81-175">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
