---
title: Tüm abonelik analizi bilgilerini alma
description: Tüm abonelik Analizi bilgilerini alma.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760258"
---
# <a name="get-all-subscription-analytics-information"></a><span data-ttu-id="e60e4-103">Tüm abonelik analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="e60e4-103">Get all subscription analytics information</span></span>

<span data-ttu-id="e60e4-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="e60e4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e60e4-105">Bu makalede, müşterileriniz için tüm abonelik Analizi bilgilerinin nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="e60e4-105">This article describes how to get all the subscription analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e60e4-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e60e4-106">Prerequisites</span></span>

- <span data-ttu-id="e60e4-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="e60e4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e60e4-108">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e60e4-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="e60e4-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e60e4-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e60e4-110">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="e60e4-110">Request syntax</span></span>

| <span data-ttu-id="e60e4-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e60e4-111">Method</span></span> | <span data-ttu-id="e60e4-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e60e4-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="e60e4-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="e60e4-113">**GET**</span></span> | <span data-ttu-id="e60e4-114">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri http/1.1</span><span class="sxs-lookup"><span data-stu-id="e60e4-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="e60e4-115">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="e60e4-115">URI parameters</span></span>

<span data-ttu-id="e60e4-116">Aşağıdaki tabloda isteğe bağlı parametreler ve açıklamaları listelenmektedir:</span><span class="sxs-lookup"><span data-stu-id="e60e4-116">The following table lists optional parameters and their descriptions:</span></span>

| <span data-ttu-id="e60e4-117">Parametre</span><span class="sxs-lookup"><span data-stu-id="e60e4-117">Parameter</span></span> | <span data-ttu-id="e60e4-118">Tür</span><span class="sxs-lookup"><span data-stu-id="e60e4-118">Type</span></span> |  <span data-ttu-id="e60e4-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e60e4-119">Description</span></span> |
|-----------|------|--------------|
| <span data-ttu-id="e60e4-120">top</span><span class="sxs-lookup"><span data-stu-id="e60e4-120">top</span></span> | <span data-ttu-id="e60e4-121">int</span><span class="sxs-lookup"><span data-stu-id="e60e4-121">int</span></span> | <span data-ttu-id="e60e4-122">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="e60e4-122">The number of rows of data to return in the request.</span></span> <span data-ttu-id="e60e4-123">Değer belirtilmezse, en büyük değer ve varsayılan değer `10000` .</span><span class="sxs-lookup"><span data-stu-id="e60e4-123">If the value isn't specified, the maximum value and the default value are `10000`.</span></span> <span data-ttu-id="e60e4-124">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="e60e4-124">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="e60e4-125">Atla</span><span class="sxs-lookup"><span data-stu-id="e60e4-125">skip</span></span> | <span data-ttu-id="e60e4-126">int</span><span class="sxs-lookup"><span data-stu-id="e60e4-126">int</span></span> | <span data-ttu-id="e60e4-127">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="e60e4-127">The number of rows to skip in the query.</span></span> <span data-ttu-id="e60e4-128">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="e60e4-128">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="e60e4-129">Örneğin, `top=10000` ve `skip=0` ilk 10000 veri satırını alır `top=10000` ve `skip=10000` sonraki 10000 veri satırını alır.</span><span class="sxs-lookup"><span data-stu-id="e60e4-129">For example, `top=10000` and `skip=0` retrieves the first 10000 rows of data, `top=10000` and `skip=10000` retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="e60e4-130">filtre</span><span class="sxs-lookup"><span data-stu-id="e60e4-130">filter</span></span> | <span data-ttu-id="e60e4-131">string</span><span class="sxs-lookup"><span data-stu-id="e60e4-131">string</span></span> | <span data-ttu-id="e60e4-132">Yanıttaki satırları filtreleyen bir veya daha fazla deyim.</span><span class="sxs-lookup"><span data-stu-id="e60e4-132">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="e60e4-133">Her filtre ekstresi, yanıt gövdesinden bir alan adı ve **`eq`** , **`ne`** veya belirli alanlar için, işleci ile ilişkili bir değer içerir **`contains`** .</span><span class="sxs-lookup"><span data-stu-id="e60e4-133">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="e60e4-134">Deyimler, veya kullanılarak birleştirilebilir **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="e60e4-134">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="e60e4-135">Dize değerleri, **filtre** parametresindeki tek tırnak işaretleriyle çevrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="e60e4-135">String values must be surrounded by single quotes in the **filter** parameter.</span></span> <span data-ttu-id="e60e4-136">Filtrelenebilir alanların listesi ve bu alanlarla Desteklenen işleçler için aşağıdaki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="e60e4-136">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="e60e4-137">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="e60e4-137">aggregationLevel</span></span> | <span data-ttu-id="e60e4-138">string</span><span class="sxs-lookup"><span data-stu-id="e60e4-138">string</span></span> | <span data-ttu-id="e60e4-139">Toplam verilerinin alınacağı zaman aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="e60e4-139">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="e60e4-140">Şu dizelerden biri olabilir: **gün**, **hafta** veya **ay**.</span><span class="sxs-lookup"><span data-stu-id="e60e4-140">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="e60e4-141">Değer belirtilmezse, varsayılan olarak **Dadterange** olur.</span><span class="sxs-lookup"><span data-stu-id="e60e4-141">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="e60e4-142">Bu parametre yalnızca, **GroupBy** parametresinin bir parçası olarak bir tarih alanı geçirildiğinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="e60e4-142">This parameter applies only when a date field is passed as part of the **groupBy** parameter.</span></span> |
| <span data-ttu-id="e60e4-143">Ölçütü</span><span class="sxs-lookup"><span data-stu-id="e60e4-143">groupBy</span></span> | <span data-ttu-id="e60e4-144">string</span><span class="sxs-lookup"><span data-stu-id="e60e4-144">string</span></span> | <span data-ttu-id="e60e4-145">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="e60e4-145">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e60e4-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e60e4-146">Request headers</span></span>

<span data-ttu-id="e60e4-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="e60e4-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e60e4-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e60e4-148">Request body</span></span>

<span data-ttu-id="e60e4-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="e60e4-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e60e4-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e60e4-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="e60e4-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e60e4-151">REST response</span></span>

<span data-ttu-id="e60e4-152">Başarılı olursa, yanıt gövdesi bir [**abonelik**](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="e60e4-152">If successful, the response body contains a collection of [**Subscription**](partner-center-analytics-resources.md#subscription-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e60e4-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e60e4-153">Response success and error codes</span></span>

<span data-ttu-id="e60e4-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="e60e4-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e60e4-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e60e4-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e60e4-156">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="e60e4-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e60e4-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e60e4-157">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="e60e4-158">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="e60e4-158">See also</span></span>

- [<span data-ttu-id="e60e4-159">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="e60e4-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
