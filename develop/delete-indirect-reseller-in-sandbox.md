---
title: Korumalı Alanda Dolaylı Kurumsal Bayiyi Silme
description: Korumalı Alan Dolaylı Kurumsal Bayilerini silme ve API'leri kullanarak 2.00.000 testi etkinleştirme hakkında bilgi sağlar.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba1fd002ac62aba4e414d263b33ecc8153054602
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973018"
---
# <a name="delete-indirect-reseller-in-sandbox"></a><span data-ttu-id="695f4-103">Korumalı Alanda Dolaylı Kurumsal Bayiyi Silme</span><span class="sxs-lookup"><span data-stu-id="695f4-103">Delete Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="695f4-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için destek</span><span class="sxs-lookup"><span data-stu-id="695f4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="695f4-105">Bu belgede, Korumalı Alan Dolaylı Sağlayıcılarının nasıl silinecek ve API'ler kullanılarak esn nasıl testlerin etkinleştirildi?</span><span class="sxs-lookup"><span data-stu-id="695f4-105">This document shows how to delete Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

> [!Important]
> <span data-ttu-id="695f4-106">Bu belgede, Dolaylı Model deneyimleri için yalnızca Korumalı Alan ortamında izin verilen özellikler açıkmaktadır.</span><span class="sxs-lookup"><span data-stu-id="695f4-106">This document describes features that are only allowed in the Sandbox environment for Indirect Model experiences.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="695f4-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="695f4-107">Prerequisites</span></span>

- <span data-ttu-id="695f4-108">Kimlik Doğrulaması altında açıklandığı [gibi İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="695f4-108">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="695f4-109">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="695f4-109">This scenario supports authentication with App+User credentials.</span></span>

## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller"></a><span data-ttu-id="695f4-110">Korumalı Alan Dolaylı Sağlayıcısı – Korumalı Alan Dolaylı Kurumsal Bayiyi Silme</span><span class="sxs-lookup"><span data-stu-id="695f4-110">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller</span></span> 

<span data-ttu-id="695f4-111">Bu özellik yalnızca Korumalı Alanda kullanılabilir ve Korumalı Alan Dolaylı Sağlayıcılarına Korumalı Alan Dolaylı Kurumsal Bayileri oluşturma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="695f4-111">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="695f4-112">Korumalı Alan Dolaylı Kurumsal Bayiyi Silme Önkoşulları</span><span class="sxs-lookup"><span data-stu-id="695f4-112">Prerequisites for Deleting a Sandbox Indirect Reseller</span></span>
    1. <span data-ttu-id="695f4-113">Korumalı Alan Dolaylı Kurumsal Bayinin her müşterisi için abonelikleri askıya alma</span><span class="sxs-lookup"><span data-stu-id="695f4-113">Suspend the subscriptions for each customer of Sandbox Indirect Reseller</span></span>
    2. <span data-ttu-id="695f4-114">Dolaylı Kurumsal Bayinin tüm müşterilerini silme</span><span class="sxs-lookup"><span data-stu-id="695f4-114">Delete all customers of Indirect Reseller</span></span>
2. <span data-ttu-id="695f4-115">Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen beş Korumalı Alan Dolaylı Kurumsal Bayi sınırı.</span><span class="sxs-lookup"><span data-stu-id="695f4-115">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="695f4-116">Korumalı Alan Dolaylı kurumsal bayisi silindikten sonra kota sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="695f4-116">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

## <a name="delete-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="695f4-117">API aracılığıyla Korumalı Alan Dolaylı Kurumsal Bayisini silme</span><span class="sxs-lookup"><span data-stu-id="695f4-117">Delete Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="695f4-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="695f4-118">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="695f4-119">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="695f4-119">Request syntax</span></span>

| <span data-ttu-id="695f4-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="695f4-120">Method</span></span> | <span data-ttu-id="695f4-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="695f4-121">Request URI</span></span>                                                                             |
|------------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="695f4-122">**Silmek**</span><span class="sxs-lookup"><span data-stu-id="695f4-122">**DELETE**</span></span> | <span data-ttu-id="695f4-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span><span class="sxs-lookup"><span data-stu-id="695f4-123">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller/{resellerId}</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="695f4-124">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="695f4-124">Request headers</span></span>

- <span data-ttu-id="695f4-125">Bu API bir kez etkilidir (birden çok kez çağırsanız farklı bir sonuç ortayalanmaz)</span><span class="sxs-lookup"><span data-stu-id="695f4-125">This API is idempotent (it will not yield a different result if you call it multiple times)</span></span>
- <span data-ttu-id="695f4-126">İstek kimliği ve bağıntı kimliği gereklidir</span><span class="sxs-lookup"><span data-stu-id="695f4-126">A request ID and correlation ID are required</span></span>
- <span data-ttu-id="695f4-127">Daha fazla bilgi için [bkz. İŞ ORTAĞı MERKEZI REST üst bilgileri](headers.md)</span><span class="sxs-lookup"><span data-stu-id="695f4-127">For more information, see [Partner Center REST headers](headers.md)</span></span>

### <a name="request-example"></a><span data-ttu-id="695f4-128">İstek Örneği</span><span class="sxs-lookup"><span data-stu-id="695f4-128">Request Example</span></span>

<span data-ttu-id="695f4-129">Silmek https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span><span class="sxs-lookup"><span data-stu-id="695f4-129">DELETE https://api.partnercenter.microsoft.com/v1/sandboxIndirectReseller/{resellerID}</span></span>

```http
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
```

####  <a name="response-example"></a><span data-ttu-id="695f4-130">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="695f4-130">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Feb 2021 00:43:02 GMT
```

#### <a name="response-success-and-error-codes"></a><span data-ttu-id="695f4-131">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="695f4-131">Response success and error codes</span></span>

<span data-ttu-id="695f4-132">Her yanıt, başarılı veya başarısız olduğunu ve diğer hata ayıklama bilgilerini gösteren bir HTTP durum koduyla birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="695f4-132">Each response comes with an HTTP status code that indicates success or failure and other debugging information.</span></span> <span data-ttu-id="695f4-133">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="695f4-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="695f4-134">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="695f4-134">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="695f4-135">Bu yöntem aşağıdaki durum başarısını ve hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="695f4-135">This method returns the following status success and error codes:</span></span>

| <span data-ttu-id="695f4-136">HTTP Durum Kodu</span><span class="sxs-lookup"><span data-stu-id="695f4-136">HTTP Status Code</span></span>                     | <span data-ttu-id="695f4-137">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="695f4-137">Error code</span></span>     | <span data-ttu-id="695f4-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="695f4-138">Description</span></span>                                      |
|--------------------------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="695f4-139">401</span><span class="sxs-lookup"><span data-stu-id="695f4-139">401</span></span>                                  | <span data-ttu-id="695f4-140">6002</span><span class="sxs-lookup"><span data-stu-id="695f4-140">6002</span></span>           | <span data-ttu-id="695f4-141">Yetkisiz belirteç veya İpucu Sağlayıcısı Hesabı Değil</span><span class="sxs-lookup"><span data-stu-id="695f4-141">Unauthorized token or Not a Tip Provider Account</span></span> |
| <span data-ttu-id="695f4-142">403</span><span class="sxs-lookup"><span data-stu-id="695f4-142">403</span></span>                                  | <span data-ttu-id="695f4-143">6003</span><span class="sxs-lookup"><span data-stu-id="695f4-143">6003</span></span>           | <span data-ttu-id="695f4-144">Korumalı Alanı Silme IR'ye izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="695f4-144">Delete Sandbox IR is not allowed</span></span>                 |
| <span data-ttu-id="695f4-145">403</span><span class="sxs-lookup"><span data-stu-id="695f4-145">403</span></span>                                  | <span data-ttu-id="695f4-146">6004</span><span class="sxs-lookup"><span data-stu-id="695f4-146">6004</span></span>           | <span data-ttu-id="695f4-147">Korumalı Alan IR oluşturma işlemi izin verilmiyor</span><span class="sxs-lookup"><span data-stu-id="695f4-147">Create Sandbox IR operation not allowed</span></span>          |
| <span data-ttu-id="695f4-148">409</span><span class="sxs-lookup"><span data-stu-id="695f4-148">409</span></span>                                  | <span data-ttu-id="695f4-149">1003</span><span class="sxs-lookup"><span data-stu-id="695f4-149">1003</span></span>           | <span data-ttu-id="695f4-150">Kiracı oluşturulurken çakışma</span><span class="sxs-lookup"><span data-stu-id="695f4-150">Conflict while creating tenant</span></span>                   |
