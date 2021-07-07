---
title: Tüm başvuru analizi bilgilerini alma
description: Tüm referans analizi bilgilerini nasıl elde edinebilirsiniz?
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 7deda4098ceb9eb4e1ee75056c53c754618bf3e2
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760615"
---
# <a name="get-all-referrals-analytics-information"></a><span data-ttu-id="f748a-103">Tüm başvuru analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="f748a-103">Get all referrals analytics information</span></span>

<span data-ttu-id="f748a-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="f748a-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f748a-105">Müşterileriniz için tüm referans analizi bilgilerini nasıl elde edersiniz?</span><span class="sxs-lookup"><span data-stu-id="f748a-105">How to get all the referrals analytics information for your customers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f748a-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f748a-106">Prerequisites</span></span>

- <span data-ttu-id="f748a-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="f748a-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f748a-108">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="f748a-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="f748a-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f748a-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f748a-110">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="f748a-110">Request syntax</span></span>

| <span data-ttu-id="f748a-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f748a-111">Method</span></span>  | <span data-ttu-id="f748a-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f748a-112">Request URI</span></span> |
|---------|-------------|
| <span data-ttu-id="f748a-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="f748a-113">**GET**</span></span> | <span data-ttu-id="f748a-114">[*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referanslar HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="f748a-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/referrals HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="f748a-115">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="f748a-115">URI parameters</span></span>

| <span data-ttu-id="f748a-116">Parametre</span><span class="sxs-lookup"><span data-stu-id="f748a-116">Parameter</span></span> | <span data-ttu-id="f748a-117">Tür</span><span class="sxs-lookup"><span data-stu-id="f748a-117">Type</span></span> | <span data-ttu-id="f748a-118">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f748a-118">Description</span></span> |
|-----------|------|-------------|
| <span data-ttu-id="f748a-119">filtre</span><span class="sxs-lookup"><span data-stu-id="f748a-119">filter</span></span> | <span data-ttu-id="f748a-120">string</span><span class="sxs-lookup"><span data-stu-id="f748a-120">string</span></span> | <span data-ttu-id="f748a-121">Filtre koşuluyla eşleşen verileri döndürür.</span><span class="sxs-lookup"><span data-stu-id="f748a-121">Returns data matching the filter condition.</span></span></br> <span data-ttu-id="f748a-122">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="f748a-122">**Example:**</span></span></br>  `.../referrals?filter=field eq 'value'` |
| <span data-ttu-id="f748a-123">Groupby</span><span class="sxs-lookup"><span data-stu-id="f748a-123">groupby</span></span> | <span data-ttu-id="f748a-124">string</span><span class="sxs-lookup"><span data-stu-id="f748a-124">string</span></span> | <span data-ttu-id="f748a-125">Hem terimleri hem de tarihleri destekler.</span><span class="sxs-lookup"><span data-stu-id="f748a-125">Supports both terms and dates.</span></span> <span data-ttu-id="f748a-126">Demet sayısını sınırlamak için kısa devre mantığı.</span><span class="sxs-lookup"><span data-stu-id="f748a-126">Short circuit logic to limit the number of buckets.</span></span></br> <span data-ttu-id="f748a-127">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="f748a-127">**Example:**</span></span></br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| <span data-ttu-id="f748a-128">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="f748a-128">aggregationLevel</span></span> | <span data-ttu-id="f748a-129">string</span><span class="sxs-lookup"><span data-stu-id="f748a-129">string</span></span> | <span data-ttu-id="f748a-130">*aggregationLevel parametresi* bir *groupby gerektirir.*</span><span class="sxs-lookup"><span data-stu-id="f748a-130">The *aggregationLevel* parameter requires a *groupby*.</span></span> <span data-ttu-id="f748a-131">*aggregationLevel* parametresi, groupby içinde mevcut olan tüm tarih *alanlarına uygulanır.*</span><span class="sxs-lookup"><span data-stu-id="f748a-131">The *aggregationLevel* parameter applies to all date fields present in the *groupby*.</span></span></br> <span data-ttu-id="f748a-132">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="f748a-132">**Example:**</span></span></br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| <span data-ttu-id="f748a-133">top</span><span class="sxs-lookup"><span data-stu-id="f748a-133">top</span></span> | <span data-ttu-id="f748a-134">string</span><span class="sxs-lookup"><span data-stu-id="f748a-134">string</span></span> | <span data-ttu-id="f748a-135">Sayfa sınırı 10000'tir.</span><span class="sxs-lookup"><span data-stu-id="f748a-135">The page limit is 10000.</span></span> <span data-ttu-id="f748a-136">10000'den küçük herhangi bir değeri alır.</span><span class="sxs-lookup"><span data-stu-id="f748a-136">Takes any value less than 10000.</span></span></br> <span data-ttu-id="f748a-137">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="f748a-137">**Example:**</span></span></br> `.../referrals?top=100`</br> |
| <span data-ttu-id="f748a-138">Atla</span><span class="sxs-lookup"><span data-stu-id="f748a-138">skip</span></span> | <span data-ttu-id="f748a-139">string</span><span class="sxs-lookup"><span data-stu-id="f748a-139">string</span></span> | <span data-ttu-id="f748a-140">Atlan satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="f748a-140">Number of rows to skip.</span></span></br> <span data-ttu-id="f748a-141">**Örnek:**</span><span class="sxs-lookup"><span data-stu-id="f748a-141">**Example:**</span></span></br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a><span data-ttu-id="f748a-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f748a-142">Request headers</span></span>

<span data-ttu-id="f748a-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="f748a-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f748a-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f748a-144">Request body</span></span>

<span data-ttu-id="f748a-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="f748a-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f748a-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f748a-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="f748a-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f748a-147">REST response</span></span>

<span data-ttu-id="f748a-148">Başarılı olursa, yanıt gövdesi Bir Referans kaynakları [koleksiyonu](partner-center-analytics-resources.md#referrals-resource) içerir.</span><span class="sxs-lookup"><span data-stu-id="f748a-148">If successful, the response body contains a collection of [Referrals](partner-center-analytics-resources.md#referrals-resource) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f748a-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f748a-149">Response success and error codes</span></span>

<span data-ttu-id="f748a-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="f748a-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f748a-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f748a-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f748a-152">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="f748a-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f748a-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f748a-153">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="f748a-154">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f748a-154">See also</span></span>

- [<span data-ttu-id="f748a-155">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f748a-155">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
