---
title: Tüm arama analizi bilgilerini alma
description: Tüm arama Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e789a013b01fb63a38c72f4fe94864ecf21f7e4b
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760173"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="75cd4-103">Tüm arama analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="75cd4-103">Get all search analytics information</span></span>

<span data-ttu-id="75cd4-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="75cd4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="75cd4-105">Müşterileriniz için tüm arama Analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="75cd4-105">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="75cd4-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="75cd4-106">Prerequisites</span></span>

- <span data-ttu-id="75cd4-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="75cd4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="75cd4-108">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="75cd4-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="75cd4-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="75cd4-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="75cd4-110">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="75cd4-110">Request syntax</span></span>

| <span data-ttu-id="75cd4-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="75cd4-111">Method</span></span>  | <span data-ttu-id="75cd4-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="75cd4-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="75cd4-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="75cd4-113">**GET**</span></span> | <span data-ttu-id="75cd4-114">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/Search http/1.1</span><span class="sxs-lookup"><span data-stu-id="75cd4-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="75cd4-115">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="75cd4-115">URI parameters</span></span>

|    <span data-ttu-id="75cd4-116">Parametre</span><span class="sxs-lookup"><span data-stu-id="75cd4-116">Parameter</span></span>     |  <span data-ttu-id="75cd4-117">Tür</span><span class="sxs-lookup"><span data-stu-id="75cd4-117">Type</span></span>  |                                                                                                                   <span data-ttu-id="75cd4-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="75cd4-118">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="75cd4-119">filtre</span><span class="sxs-lookup"><span data-stu-id="75cd4-119">filter</span></span>      | <span data-ttu-id="75cd4-120">string</span><span class="sxs-lookup"><span data-stu-id="75cd4-120">string</span></span> |                                                                     <span data-ttu-id="75cd4-121">Filtre koşuluyla eşleşen verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="75cd4-121">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="75cd4-122">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="75cd4-122">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="75cd4-123">ölçütü</span><span class="sxs-lookup"><span data-stu-id="75cd4-123">groupby</span></span>      | <span data-ttu-id="75cd4-124">string</span><span class="sxs-lookup"><span data-stu-id="75cd4-124">string</span></span> |                                         <span data-ttu-id="75cd4-125">Hem hüküm hem de tarihleri destekler.</span><span class="sxs-lookup"><span data-stu-id="75cd4-125">Supports both terms and dates.</span></span> <span data-ttu-id="75cd4-126">Demet sayısını sınırlandırmak için kısa devre mantığı.</span><span class="sxs-lookup"><span data-stu-id="75cd4-126">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="75cd4-127">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="75cd4-127">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="75cd4-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="75cd4-128">aggregationLevel</span></span> | <span data-ttu-id="75cd4-129">string</span><span class="sxs-lookup"><span data-stu-id="75cd4-129">string</span></span> | <span data-ttu-id="75cd4-130">*AggregationLevel* parametresi bir *GroupBy* gerektirir.</span><span class="sxs-lookup"><span data-stu-id="75cd4-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="75cd4-131">*AggregationLevel* parametresi, *GroupBy* içinde bulunan tüm tarih alanları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="75cd4-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="75cd4-132">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="75cd4-132">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="75cd4-133">top</span><span class="sxs-lookup"><span data-stu-id="75cd4-133">top</span></span>        | <span data-ttu-id="75cd4-134">string</span><span class="sxs-lookup"><span data-stu-id="75cd4-134">string</span></span> |                                                                     <span data-ttu-id="75cd4-135">Sayfa sınırı 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="75cd4-135">The page limit is 10000.</span></span> <span data-ttu-id="75cd4-136">10000 'den küçük bir değer alır.</span><span class="sxs-lookup"><span data-stu-id="75cd4-136">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="75cd4-137">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="75cd4-137">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="75cd4-138">Atla</span><span class="sxs-lookup"><span data-stu-id="75cd4-138">skip</span></span>       | <span data-ttu-id="75cd4-139">string</span><span class="sxs-lookup"><span data-stu-id="75cd4-139">string</span></span> |                                                                                  <span data-ttu-id="75cd4-140">Atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="75cd4-140">Number of rows to skip.</span></span> </br> <span data-ttu-id="75cd4-141">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="75cd4-141">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="75cd4-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="75cd4-142">Request headers</span></span>

<span data-ttu-id="75cd4-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="75cd4-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="75cd4-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="75cd4-144">Request body</span></span>

<span data-ttu-id="75cd4-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="75cd4-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="75cd4-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="75cd4-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="75cd4-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="75cd4-147">REST response</span></span>

<span data-ttu-id="75cd4-148">Başarılı olursa, yanıt gövdesi bir [arama](partner-center-analytics-resources.md#search-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="75cd4-148">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="75cd4-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="75cd4-149">Response success and error codes</span></span>

<span data-ttu-id="75cd4-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="75cd4-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="75cd4-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="75cd4-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="75cd4-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="75cd4-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="75cd4-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="75cd4-153">Response example</span></span>

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a><span data-ttu-id="75cd4-154">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="75cd4-154">See also</span></span>

- [<span data-ttu-id="75cd4-155">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="75cd4-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
