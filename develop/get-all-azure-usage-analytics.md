---
title: Tüm Azure kullanım analizi bilgilerini alma
description: Tüm Azure kullanım analizi bilgilerini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 7fe987c7dc50d55b26cd72d5aead52963eb1cfbe
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760224"
---
# <a name="get-all-azure-usage-analytics-information"></a><span data-ttu-id="03894-103">Tüm Azure kullanım analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="03894-103">Get all Azure usage analytics information</span></span>

<span data-ttu-id="03894-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="03894-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="03894-105">Müşterileriniz için tüm Azure kullanım analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="03894-105">How to get all the Azure usage analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03894-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="03894-106">Prerequisites</span></span>

- <span data-ttu-id="03894-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="03894-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="03894-108">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="03894-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="03894-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="03894-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="03894-110">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="03894-110">Request syntax</span></span>

| <span data-ttu-id="03894-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="03894-111">Method</span></span>  | <span data-ttu-id="03894-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="03894-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="03894-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="03894-113">**GET**</span></span> | <span data-ttu-id="03894-114">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analysistics/Usage/Azure http/1.1</span><span class="sxs-lookup"><span data-stu-id="03894-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/usage/azure HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="03894-115">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="03894-115">URI parameters</span></span>

|<span data-ttu-id="03894-116">Parametre</span><span class="sxs-lookup"><span data-stu-id="03894-116">Parameter</span></span>        |<span data-ttu-id="03894-117">Tür</span><span class="sxs-lookup"><span data-stu-id="03894-117">Type</span></span>                        |<span data-ttu-id="03894-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="03894-118">Description</span></span>               |
|:----------------|:---------------------------|:-------------------------|
|<span data-ttu-id="03894-119">top</span><span class="sxs-lookup"><span data-stu-id="03894-119">top</span></span>              | <span data-ttu-id="03894-120">string</span><span class="sxs-lookup"><span data-stu-id="03894-120">string</span></span>                     | <span data-ttu-id="03894-121">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="03894-121">The number of rows of data to return in the request.</span></span> <span data-ttu-id="03894-122">Belirtilen en büyük değer ve varsayılan değer 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="03894-122">The maximum value and the default value if not specified is 10000.</span></span> <span data-ttu-id="03894-123">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="03894-123">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span>                        |
|<span data-ttu-id="03894-124">Atla</span><span class="sxs-lookup"><span data-stu-id="03894-124">skip</span></span>             | <span data-ttu-id="03894-125">int</span><span class="sxs-lookup"><span data-stu-id="03894-125">int</span></span>                        | <span data-ttu-id="03894-126">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="03894-126">The number of rows to skip in the query.</span></span> <span data-ttu-id="03894-127">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="03894-127">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="03894-128">Örneğin, `top=10000 and skip=0` ilk 10000 veri satırını alır, `top=10000 and skip=10000` sonraki 10000 veri satırını alır ve bu şekilde devam eder.</span><span class="sxs-lookup"><span data-stu-id="03894-128">For example, `top=10000 and skip=0` retrieves the first 10000 rows of data, `top=10000 and skip=10000` retrieves the next 10000 rows of data, and so on.</span></span>                       |
|<span data-ttu-id="03894-129">filtre</span><span class="sxs-lookup"><span data-stu-id="03894-129">filter</span></span>           | <span data-ttu-id="03894-130">string</span><span class="sxs-lookup"><span data-stu-id="03894-130">string</span></span>                     | <span data-ttu-id="03894-131">İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor.</span><span class="sxs-lookup"><span data-stu-id="03894-131">The *filter* parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="03894-132">Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir `eq` `ne` ve deyimler or kullanılarak birleştirilebilir `and` `or` .</span><span class="sxs-lookup"><span data-stu-id="03894-132">Each statement contains a field and value that are associated with the `eq` or `ne` operators, and statements can be combined using `and` or `or`.</span></span> <span data-ttu-id="03894-133">Aşağıdaki dizeleri belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="03894-133">You can specify the following strings:</span></span><br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="03894-134">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="03894-134">**Example:**</span></span><br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> <span data-ttu-id="03894-135">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="03894-135">**Example:**</span></span><br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|<span data-ttu-id="03894-136">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="03894-136">aggregationLevel</span></span> | <span data-ttu-id="03894-137">string</span><span class="sxs-lookup"><span data-stu-id="03894-137">string</span></span>                    | <span data-ttu-id="03894-138">Toplam verilerinin alınacağı zaman aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="03894-138">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="03894-139">Aşağıdaki dizelerden biri olabilir: `day` , `week` , veya `month` .</span><span class="sxs-lookup"><span data-stu-id="03894-139">Can be one of the following strings: `day`, `week`, or `month`.</span></span> <span data-ttu-id="03894-140">Belirtilmemişse, varsayılan olur `day` .</span><span class="sxs-lookup"><span data-stu-id="03894-140">If unspecified, the default is `day`.</span></span><br/><br/>                                              <span data-ttu-id="03894-141">`aggregationLevel`Parametresi, olmadan desteklenmez `groupby` .</span><span class="sxs-lookup"><span data-stu-id="03894-141">The `aggregationLevel` parameter isn't supported without a `groupby`.</span></span> <span data-ttu-id="03894-142">`aggregationLevel`Parametresi, içinde bulunan tüm tarih alanları için geçerlidir `groupby` .</span><span class="sxs-lookup"><span data-stu-id="03894-142">The `aggregationLevel` parameter applies to all date fields present in the `groupby`.</span></span>                                                      |
|<span data-ttu-id="03894-143">OrderBy</span><span class="sxs-lookup"><span data-stu-id="03894-143">orderby</span></span>          |<span data-ttu-id="03894-144">string</span><span class="sxs-lookup"><span data-stu-id="03894-144">string</span></span>                     | <span data-ttu-id="03894-145">Her bir yüklemenin sonuç verileri değerlerini sıralayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="03894-145">A statement that orders the result data values for each install.</span></span> <span data-ttu-id="03894-146">Söz dizimi `...&orderby=field [order],field [order],...` şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="03894-146">The syntax is `...&orderby=field [order],field [order],...`.</span></span> <span data-ttu-id="03894-147">`field`Parametresi aşağıdaki dizelerden biri olabilir:</span><span class="sxs-lookup"><span data-stu-id="03894-147">The `field` parameter can be one of the following strings:</span></span><br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> <span data-ttu-id="03894-148">*Order* parametresi isteğe bağlıdır ve `asc` `desc` sırasıyla her bir alan için artan veya azalan sıralama belirtmek için ya da olabilir.</span><span class="sxs-lookup"><span data-stu-id="03894-148">The *order* parameter is optional and can be `asc` or `desc` to specify ascending or descending order for each field, respectively.</span></span> <span data-ttu-id="03894-149">Varsayılan değer: `asc`.</span><span class="sxs-lookup"><span data-stu-id="03894-149">The default is `asc`.</span></span><br/><br/><span data-ttu-id="03894-150">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="03894-150">**Example:**</span></span><br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|<span data-ttu-id="03894-151">ölçütü</span><span class="sxs-lookup"><span data-stu-id="03894-151">groupby</span></span>          |<span data-ttu-id="03894-152">string</span><span class="sxs-lookup"><span data-stu-id="03894-152">string</span></span>                    | <span data-ttu-id="03894-153">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="03894-153">A statement that applies data aggregation only to the specified fields.</span></span> <span data-ttu-id="03894-154">Aşağıdaki alanları belirtebilirsiniz:</span><span class="sxs-lookup"><span data-stu-id="03894-154">You can specify the following fields:</span></span><br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/><span data-ttu-id="03894-155">Döndürülen veri satırları, parametresinde belirtilen alanları `groupby`  ve *miktarı* içerir.</span><span class="sxs-lookup"><span data-stu-id="03894-155">The returned data rows will contain the fields specified in the `groupby`  parameter and the *Quantity*.</span></span><br/><br/><span data-ttu-id="03894-156">`groupby`Parametresi parametresiyle birlikte kullanılabilir `aggregationLevel` .</span><span class="sxs-lookup"><span data-stu-id="03894-156">The `groupby` parameter can be used with the `aggregationLevel` parameter.</span></span><br/><br/><span data-ttu-id="03894-157">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="03894-157">**Example:**</span></span><br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a><span data-ttu-id="03894-158">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="03894-158">Request headers</span></span>

<span data-ttu-id="03894-159">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="03894-159">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="03894-160">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="03894-160">Request body</span></span>

<span data-ttu-id="03894-161">Yok.</span><span class="sxs-lookup"><span data-stu-id="03894-161">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="03894-162">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="03894-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="03894-163">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="03894-163">REST response</span></span>

<span data-ttu-id="03894-164">Başarılı olursa, yanıt gövdesi bir [Azure kullanım](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="03894-164">If successful, the response body contains a collection of [Azure usage](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="03894-165">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="03894-165">Response success and error codes</span></span>

<span data-ttu-id="03894-166">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="03894-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="03894-167">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="03894-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="03894-168">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="03894-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="03894-169">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="03894-169">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="03894-170">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="03894-170">See also</span></span>

- [<span data-ttu-id="03894-171">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="03894-171">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
