---
title: Tüm başvuru analizi bilgilerini alma
description: Tüm başvuru Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769082"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="bc10d-103">Tüm başvuru analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="bc10d-103">Get all referrals analytics information</span></span>

<span data-ttu-id="bc10d-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="bc10d-104">**Applies To**</span></span>

- <span data-ttu-id="bc10d-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bc10d-105">Partner Center</span></span>
- <span data-ttu-id="bc10d-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bc10d-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="bc10d-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bc10d-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bc10d-108">Müşterileriniz için tüm başvuru Analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="bc10d-108">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc10d-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bc10d-109">Prerequisites</span></span>

- <span data-ttu-id="bc10d-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="bc10d-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bc10d-111">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="bc10d-111">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="bc10d-112">REST isteği</span><span class="sxs-lookup"><span data-stu-id="bc10d-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bc10d-113">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="bc10d-113">Request syntax</span></span>

| <span data-ttu-id="bc10d-114">Yöntem</span><span class="sxs-lookup"><span data-stu-id="bc10d-114">Method</span></span>  | <span data-ttu-id="bc10d-115">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="bc10d-115">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="bc10d-116">**Al**</span><span class="sxs-lookup"><span data-stu-id="bc10d-116">**GET**</span></span> | <span data-ttu-id="bc10d-117">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/başvuruları http/1.1</span><span class="sxs-lookup"><span data-stu-id="bc10d-117">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="bc10d-118">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="bc10d-118">URI parameters</span></span>

| <span data-ttu-id="bc10d-119">Parametre</span><span class="sxs-lookup"><span data-stu-id="bc10d-119">Parameter</span></span> | <span data-ttu-id="bc10d-120">Tür</span><span class="sxs-lookup"><span data-stu-id="bc10d-120">Type</span></span> | <span data-ttu-id="bc10d-121">Description</span><span class="sxs-lookup"><span data-stu-id="bc10d-121">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="bc10d-122">filtre</span><span class="sxs-lookup"><span data-stu-id="bc10d-122">filter</span></span> | <span data-ttu-id="bc10d-123">string</span><span class="sxs-lookup"><span data-stu-id="bc10d-123">string</span></span> | <span data-ttu-id="bc10d-124">Filtre koşuluyla eşleşen verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="bc10d-124">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="bc10d-125">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="bc10d-125">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="bc10d-126">ölçütü</span><span class="sxs-lookup"><span data-stu-id="bc10d-126">groupby</span></span> | <span data-ttu-id="bc10d-127">string</span><span class="sxs-lookup"><span data-stu-id="bc10d-127">string</span></span> | <span data-ttu-id="bc10d-128">Hem hüküm hem de tarihleri destekler.</span><span class="sxs-lookup"><span data-stu-id="bc10d-128">Supports both terms and dates.</span></span> <span data-ttu-id="bc10d-129">Demet sayısını sınırlandırmak için kısa devre mantığı.</span><span class="sxs-lookup"><span data-stu-id="bc10d-129">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="bc10d-130">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="bc10d-130">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="bc10d-131">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="bc10d-131">aggregationLevel</span></span> | <span data-ttu-id="bc10d-132">string</span><span class="sxs-lookup"><span data-stu-id="bc10d-132">string</span></span> | <span data-ttu-id="bc10d-133">*AggregationLevel* parametresi bir *GroupBy* gerektirir.</span><span class="sxs-lookup"><span data-stu-id="bc10d-133">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="bc10d-134">*AggregationLevel* parametresi, *GroupBy* içinde bulunan tüm tarih alanları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="bc10d-134">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="bc10d-135">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="bc10d-135">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="bc10d-136">top</span><span class="sxs-lookup"><span data-stu-id="bc10d-136">top</span></span> | <span data-ttu-id="bc10d-137">string</span><span class="sxs-lookup"><span data-stu-id="bc10d-137">string</span></span> | <span data-ttu-id="bc10d-138">Sayfa sınırı 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="bc10d-138">The page limit is 10000.</span></span> <span data-ttu-id="bc10d-139">10000 'den küçük bir değer alır.</span><span class="sxs-lookup"><span data-stu-id="bc10d-139">Takes any value less than 10000.</span></span></br> <span data-ttu-id="bc10d-140">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="bc10d-140">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="bc10d-141">Atla</span><span class="sxs-lookup"><span data-stu-id="bc10d-141">skip</span></span> | <span data-ttu-id="bc10d-142">string</span><span class="sxs-lookup"><span data-stu-id="bc10d-142">string</span></span> | <span data-ttu-id="bc10d-143">Atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="bc10d-143">Number of rows to skip.</span></span></br> <span data-ttu-id="bc10d-144">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="bc10d-144">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="bc10d-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="bc10d-145">Request headers</span></span>

<span data-ttu-id="bc10d-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bc10d-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bc10d-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="bc10d-147">Request body</span></span>

<span data-ttu-id="bc10d-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="bc10d-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bc10d-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="bc10d-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="bc10d-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="bc10d-150">REST response</span></span>

<span data-ttu-id="bc10d-151">Başarılı olursa, yanıt gövdesi bir [başvuru](partner-center-analytics-resources.md#referrals-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="bc10d-151">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bc10d-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="bc10d-152">Response success and error codes</span></span>

<span data-ttu-id="bc10d-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="bc10d-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bc10d-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bc10d-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bc10d-155">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bc10d-155">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bc10d-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="bc10d-156">Response example</span></span>

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a><span data-ttu-id="bc10d-157">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="bc10d-157">See also</span></span>

- [<span data-ttu-id="bc10d-158">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="bc10d-158">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
