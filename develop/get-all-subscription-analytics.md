---
title: Tüm abonelik analizi bilgilerini alma
description: Tüm abonelik Analizi bilgilerini alma.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: f32fb99ad52939ae8e9de26276588d3022f18fbc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768753"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="392df-103">Tüm abonelik analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="392df-103">Get all subscription analytics information</span></span>

<span data-ttu-id="392df-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="392df-104">**Applies to:**</span></span>

- <span data-ttu-id="392df-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="392df-105">Partner Center</span></span>
- <span data-ttu-id="392df-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="392df-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="392df-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="392df-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="392df-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="392df-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="392df-109">Bu makalede, müşterileriniz için tüm abonelik Analizi bilgilerinin nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="392df-109">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="392df-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="392df-110">Prerequisites</span></span>

- <span data-ttu-id="392df-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="392df-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="392df-112">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="392df-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="392df-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="392df-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="392df-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="392df-114">Request syntax</span></span>

| <span data-ttu-id="392df-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="392df-115">Method</span></span> | <span data-ttu-id="392df-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="392df-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="392df-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="392df-117">**GET**</span></span> | <span data-ttu-id="392df-118">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri http/1.1</span><span class="sxs-lookup"><span data-stu-id="392df-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="392df-119">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="392df-119">URI parameters</span></span>

<span data-ttu-id="392df-120">Aşağıdaki tabloda isteğe bağlı parametreler ve açıklamaları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="392df-120">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="392df-121">Parametre</span><span class="sxs-lookup"><span data-stu-id="392df-121">Parameter</span></span> | <span data-ttu-id="392df-122">Tür</span><span class="sxs-lookup"><span data-stu-id="392df-122">Type</span></span> |  <span data-ttu-id="392df-123">Description</span><span class="sxs-lookup"><span data-stu-id="392df-123">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="392df-124">top</span><span class="sxs-lookup"><span data-stu-id="392df-124">top</span></span> | <span data-ttu-id="392df-125">int</span><span class="sxs-lookup"><span data-stu-id="392df-125">int</span></span> | <span data-ttu-id="392df-126">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="392df-126">The number of rows of data to return in the request.</span></span> <span data-ttu-id="392df-127">Değer belirtilmezse, en büyük değer ve varsayılan değer `10000` .</span><span class="sxs-lookup"><span data-stu-id="392df-127">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="392df-128">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="392df-128">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="392df-129">Atla</span><span class="sxs-lookup"><span data-stu-id="392df-129">skip</span></span> | <span data-ttu-id="392df-130">int</span><span class="sxs-lookup"><span data-stu-id="392df-130">int</span></span> | <span data-ttu-id="392df-131">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="392df-131">The number of rows to skip in the query.</span></span> <span data-ttu-id="392df-132">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="392df-132">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="392df-133">Örneğin, `top=10000` ve `skip=0` ilk 10000 veri satırını alır `top=10000` ve `skip=10000` sonraki 10000 veri satırını alır.</span><span class="sxs-lookup"><span data-stu-id="392df-133">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="392df-134">filtre</span><span class="sxs-lookup"><span data-stu-id="392df-134">filter</span></span> | <span data-ttu-id="392df-135">string</span><span class="sxs-lookup"><span data-stu-id="392df-135">string</span></span> | <span data-ttu-id="392df-136">Yanıttaki satırları filtreleyen bir veya daha fazla deyim.</span><span class="sxs-lookup"><span data-stu-id="392df-136">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="392df-137">Her filtre ekstresi, yanıt gövdesinden bir alan adı ve **`eq`** , **`ne`** veya belirli alanlar için, işleci ile ilişkili bir değer içerir **`contains`** .</span><span class="sxs-lookup"><span data-stu-id="392df-137">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="392df-138">Deyimler, veya kullanılarak birleştirilebilir **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="392df-138">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="392df-139">Dize değerleri, **filtre** parametresindeki tek tırnak işaretleriyle çevrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="392df-139">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="392df-140">Filtrelenebilir alanların listesi ve bu alanlarla Desteklenen işleçler için aşağıdaki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="392df-140">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="392df-141">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="392df-141">aggregationLevel</span></span> | <span data-ttu-id="392df-142">string</span><span class="sxs-lookup"><span data-stu-id="392df-142">string</span></span> | <span data-ttu-id="392df-143">Toplam verilerinin alınacağı zaman aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="392df-143">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="392df-144">Şu dizelerden biri olabilir: **gün**, **hafta** veya **ay**.</span><span class="sxs-lookup"><span data-stu-id="392df-144">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="392df-145">Değer belirtilmezse, varsayılan olarak **Dadterange** olur.</span><span class="sxs-lookup"><span data-stu-id="392df-145">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="392df-146">Bu parametre yalnızca, **GroupBy** parametresinin bir parçası olarak bir tarih alanı geçirildiğinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="392df-146">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="392df-147">Ölçütü</span><span class="sxs-lookup"><span data-stu-id="392df-147">groupBy</span></span> | <span data-ttu-id="392df-148">string</span><span class="sxs-lookup"><span data-stu-id="392df-148">string</span></span> | <span data-ttu-id="392df-149">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="392df-149">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="392df-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="392df-150">Request headers</span></span>

<span data-ttu-id="392df-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="392df-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="392df-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="392df-152">Request body</span></span>

<span data-ttu-id="392df-153">Yok.</span><span class="sxs-lookup"><span data-stu-id="392df-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="392df-154">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="392df-154">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="392df-155">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="392df-155">REST response</span></span>

<span data-ttu-id="392df-156">Başarılı olursa, yanıt gövdesi bir [**abonelik**](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="392df-156">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="392df-157">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="392df-157">Response success and error codes</span></span>

<span data-ttu-id="392df-158">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="392df-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="392df-159">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="392df-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="392df-160">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="392df-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="392df-161">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="392df-161">Response example</span></span>

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a><span data-ttu-id="392df-162">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="392df-162">See also</span></span>

- [<span data-ttu-id="392df-163">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="392df-163">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
