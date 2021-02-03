---
title: Tüm arama analizi bilgilerini alma
description: Tüm arama Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 967f8d0ed2d276e0f68a047204b64d83dc69da95
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768758"
---
# <a name="get-all-search-analytics-information"></a><span data-ttu-id="3b350-103">Tüm arama analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="3b350-103">Get all search analytics information</span></span>

<span data-ttu-id="3b350-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="3b350-104">**Applies To**</span></span>

- <span data-ttu-id="3b350-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b350-105">Partner Center</span></span>
- <span data-ttu-id="3b350-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b350-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="3b350-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b350-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="3b350-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3b350-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3b350-109">Müşterileriniz için tüm arama Analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="3b350-109">How to get all the search analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3b350-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3b350-110">Prerequisites</span></span>

- <span data-ttu-id="3b350-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3b350-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3b350-112">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3b350-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="3b350-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3b350-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3b350-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3b350-114">Request syntax</span></span>

| <span data-ttu-id="3b350-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3b350-115">Method</span></span>  | <span data-ttu-id="3b350-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3b350-116">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="3b350-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="3b350-117">**GET**</span></span> | <span data-ttu-id="3b350-118">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/Search http/1.1</span><span class="sxs-lookup"><span data-stu-id="3b350-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/search HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3b350-119">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="3b350-119">URI parameters</span></span>

|    <span data-ttu-id="3b350-120">Parametre</span><span class="sxs-lookup"><span data-stu-id="3b350-120">Parameter</span></span>     |  <span data-ttu-id="3b350-121">Tür</span><span class="sxs-lookup"><span data-stu-id="3b350-121">Type</span></span>  |                                                                                                                   <span data-ttu-id="3b350-122">Description</span><span class="sxs-lookup"><span data-stu-id="3b350-122">Description</span></span>                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      <span data-ttu-id="3b350-123">filtre</span><span class="sxs-lookup"><span data-stu-id="3b350-123">filter</span></span>      | <span data-ttu-id="3b350-124">string</span><span class="sxs-lookup"><span data-stu-id="3b350-124">string</span></span> |                                                                     <span data-ttu-id="3b350-125">Filtre koşuluyla eşleşen verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="3b350-125">Returns data matching the filter condition.</span></span> </br> <span data-ttu-id="3b350-126">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3b350-126">**Example:**</span></span></br> `.../search?filter=field eq 'value'`                                                                     |
|     <span data-ttu-id="3b350-127">ölçütü</span><span class="sxs-lookup"><span data-stu-id="3b350-127">groupby</span></span>      | <span data-ttu-id="3b350-128">string</span><span class="sxs-lookup"><span data-stu-id="3b350-128">string</span></span> |                                         <span data-ttu-id="3b350-129">Hem hüküm hem de tarihleri destekler.</span><span class="sxs-lookup"><span data-stu-id="3b350-129">Supports both terms and dates.</span></span> <span data-ttu-id="3b350-130">Demet sayısını sınırlandırmak için kısa devre mantığı.</span><span class="sxs-lookup"><span data-stu-id="3b350-130">Short circuit logic to limit the number of buckets.</span></span> </br> <span data-ttu-id="3b350-131">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3b350-131">**Example:**</span></span></br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| <span data-ttu-id="3b350-132">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="3b350-132">aggregationLevel</span></span> | <span data-ttu-id="3b350-133">string</span><span class="sxs-lookup"><span data-stu-id="3b350-133">string</span></span> | <span data-ttu-id="3b350-134">*AggregationLevel* parametresi bir *GroupBy* gerektirir.</span><span class="sxs-lookup"><span data-stu-id="3b350-134">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="3b350-135">*AggregationLevel* parametresi, *GroupBy* içinde bulunan tüm tarih alanları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="3b350-135">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span> </br> <span data-ttu-id="3b350-136">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3b350-136">**Example:**</span></span></br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       <span data-ttu-id="3b350-137">top</span><span class="sxs-lookup"><span data-stu-id="3b350-137">top</span></span>        | <span data-ttu-id="3b350-138">string</span><span class="sxs-lookup"><span data-stu-id="3b350-138">string</span></span> |                                                                     <span data-ttu-id="3b350-139">Sayfa sınırı 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="3b350-139">The page limit is 10000.</span></span> <span data-ttu-id="3b350-140">10000 'den küçük bir değer alır.</span><span class="sxs-lookup"><span data-stu-id="3b350-140">Takes any value less than 10000.</span></span>  </br> <span data-ttu-id="3b350-141">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3b350-141">**Example:**</span></span></br>  `.../search?top=100`                                                                     |
|       <span data-ttu-id="3b350-142">Atla</span><span class="sxs-lookup"><span data-stu-id="3b350-142">skip</span></span>       | <span data-ttu-id="3b350-143">string</span><span class="sxs-lookup"><span data-stu-id="3b350-143">string</span></span> |                                                                                  <span data-ttu-id="3b350-144">Atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="3b350-144">Number of rows to skip.</span></span> </br> <span data-ttu-id="3b350-145">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="3b350-145">**Example:**</span></span></br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a><span data-ttu-id="3b350-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3b350-146">Request headers</span></span>

<span data-ttu-id="3b350-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3b350-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3b350-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3b350-148">Request body</span></span>

<span data-ttu-id="3b350-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="3b350-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3b350-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3b350-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="3b350-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3b350-151">REST response</span></span>

<span data-ttu-id="3b350-152">Başarılı olursa, yanıt gövdesi bir [arama](partner-center-analytics-resources.md#search-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="3b350-152">If successful, the response body contains a collection of [Search](partner-center-analytics-resources.md#search-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3b350-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3b350-153">Response success and error codes</span></span>

<span data-ttu-id="3b350-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3b350-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3b350-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3b350-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3b350-156">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3b350-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3b350-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3b350-157">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="3b350-158">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="3b350-158">See also</span></span>

- [<span data-ttu-id="3b350-159">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="3b350-159">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
