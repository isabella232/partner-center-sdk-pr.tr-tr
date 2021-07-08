---
title: Pazara göre teklif kategorilerinin bir listesini alma
description: Tüm Microsoft Bulutları için verilen bir ülkede/bölgede ve yerelde tüm teklif kategorilerini içeren bir koleksiyon elde etmeyi öğrenin.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e699355f07dda3941eafed32f5f635d94000abd1
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874287"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="9aa9d-103">Pazara göre teklif kategorilerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="9aa9d-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="9aa9d-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="9aa9d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9aa9d-105">Bu makalede, belirli bir ülkede/bölgede ve yerel bölgede tüm teklif kategorilerini içeren bir koleksiyonun nasıl elde edildiklerine yer verilmiştir.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-105">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9aa9d-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9aa9d-106">Prerequisites</span></span>

- <span data-ttu-id="9aa9d-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="9aa9d-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9aa9d-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="9aa9d-109">C\#</span><span class="sxs-lookup"><span data-stu-id="9aa9d-109">C\#</span></span>

<span data-ttu-id="9aa9d-110">Verilen bir ülkede/bölgede ve yerelde teklif kategorilerinin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="9aa9d-110">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="9aa9d-111">[**IAggregatePartner.Operations koleksiyonu kullanarak**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) verilen bağlamda [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-111">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="9aa9d-112">Sonuçta elde [**edilen nesnenin OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) özelliğini inceler.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-112">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="9aa9d-113">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="9aa9d-113">For an example, see the following:</span></span>

- <span data-ttu-id="9aa9d-114">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="9aa9d-114">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="9aa9d-115">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="9aa9d-115">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="9aa9d-116">Sınıf: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="9aa9d-116">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="9aa9d-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9aa9d-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9aa9d-118">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="9aa9d-118">Request syntax</span></span>

| <span data-ttu-id="9aa9d-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9aa9d-119">Method</span></span>  | <span data-ttu-id="9aa9d-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9aa9d-120">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="9aa9d-121">**Al**</span><span class="sxs-lookup"><span data-stu-id="9aa9d-121">**GET**</span></span> | <span data-ttu-id="9aa9d-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="9aa9d-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="9aa9d-123">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="9aa9d-123">URI parameter</span></span>

<span data-ttu-id="9aa9d-124">Bu tabloda teklif kategorilerini almak için gerekli sorgu parametreleri listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-124">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="9aa9d-125">Ad</span><span class="sxs-lookup"><span data-stu-id="9aa9d-125">Name</span></span>           | <span data-ttu-id="9aa9d-126">Tür</span><span class="sxs-lookup"><span data-stu-id="9aa9d-126">Type</span></span>       | <span data-ttu-id="9aa9d-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9aa9d-127">Required</span></span> | <span data-ttu-id="9aa9d-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9aa9d-128">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="9aa9d-129">**country-id**</span><span class="sxs-lookup"><span data-stu-id="9aa9d-129">**country-id**</span></span> | <span data-ttu-id="9aa9d-130">**string**</span><span class="sxs-lookup"><span data-stu-id="9aa9d-130">**string**</span></span> | <span data-ttu-id="9aa9d-131">Y</span><span class="sxs-lookup"><span data-stu-id="9aa9d-131">Y</span></span>        | <span data-ttu-id="9aa9d-132">Ülke/bölge kimliği.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-132">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9aa9d-133">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9aa9d-133">Request headers</span></span>

<span data-ttu-id="9aa9d-134">Dize **olarak biçimlendirilmiş bir locale-id** gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-134">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="9aa9d-135">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="9aa9d-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9aa9d-136">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9aa9d-136">Request body</span></span>

<span data-ttu-id="9aa9d-137">Yok.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9aa9d-138">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9aa9d-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9aa9d-139">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9aa9d-139">REST response</span></span>

<span data-ttu-id="9aa9d-140">Başarılı olursa, bu yöntem yanıt gövdesinde **OfferCategory** kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-140">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9aa9d-141">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9aa9d-141">Response success and error codes</span></span>

<span data-ttu-id="9aa9d-142">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9aa9d-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9aa9d-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9aa9d-144">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="9aa9d-144">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9aa9d-145">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9aa9d-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
