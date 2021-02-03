---
title: Pazara göre teklif kategorilerinin bir listesini alma
description: Belirli bir ülke/bölge ve yerel ayarda yer alan tüm teklif kategorilerini içeren bir koleksiyon alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 22c46ed03a8579c53ee18c14cbca9a1e19ddb82a
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769544"
---
# <a name="get-a-list-of-offer-categories-by-market"></a><span data-ttu-id="5631d-103">Pazara göre teklif kategorilerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="5631d-103">Get a list of offer categories by market</span></span>

<span data-ttu-id="5631d-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="5631d-104">**Applies to:**</span></span>

- <span data-ttu-id="5631d-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5631d-105">Partner Center</span></span>
- <span data-ttu-id="5631d-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5631d-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5631d-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5631d-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5631d-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5631d-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5631d-109">Bu makalede, belirli bir ülke/bölge ve yerel ayarda yer alan tüm teklif kategorilerini içeren bir koleksiyonun nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="5631d-109">This article describes how to get a collection that contains all the offer categories in a given country/region and locale.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5631d-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5631d-110">Prerequisites</span></span>

- <span data-ttu-id="5631d-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5631d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5631d-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5631d-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="5631d-113">C\#</span><span class="sxs-lookup"><span data-stu-id="5631d-113">C\#</span></span>

<span data-ttu-id="5631d-114">Belirli bir ülke/bölge ve yerel ayarda teklif kategorilerinin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="5631d-114">To get a list of offer categories in a given country/region and locale:</span></span>

1. <span data-ttu-id="5631d-115">Belirtilen bağlamda [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) yöntemini çağırmak Için [**ıaggregatepartner. Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="5631d-115">Use your [**IAggregatePartner.Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) collection to call the [**With()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) method on a given context.</span></span>

2. <span data-ttu-id="5631d-116">Elde edilen nesnenin [**Offercategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) özelliğini inceleyin.</span><span class="sxs-lookup"><span data-stu-id="5631d-116">Inspect the [**OfferCategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) property of the resulting object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

<span data-ttu-id="5631d-117">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="5631d-117">For an example, see the following:</span></span>

- <span data-ttu-id="5631d-118">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5631d-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5631d-119">Proje: **Partnersdk. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="5631d-119">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="5631d-120">Sınıf: **Partnersdk. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="5631d-120">Class: **PartnerSDK.FeatureSample**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5631d-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5631d-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5631d-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5631d-122">Request syntax</span></span>

| <span data-ttu-id="5631d-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5631d-123">Method</span></span>  | <span data-ttu-id="5631d-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5631d-124">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="5631d-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="5631d-125">**GET**</span></span> | <span data-ttu-id="5631d-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/offercategories? ülke = {ülke-KIMLIĞI} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5631d-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/offercategories?country={country-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="5631d-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="5631d-127">URI parameter</span></span>

<span data-ttu-id="5631d-128">Bu tablo teklif kategorilerini almak için gerekli sorgu parametrelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="5631d-128">This table lists the required query parameters to get the offer categories.</span></span>

| <span data-ttu-id="5631d-129">Ad</span><span class="sxs-lookup"><span data-stu-id="5631d-129">Name</span></span>           | <span data-ttu-id="5631d-130">Tür</span><span class="sxs-lookup"><span data-stu-id="5631d-130">Type</span></span>       | <span data-ttu-id="5631d-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5631d-131">Required</span></span> | <span data-ttu-id="5631d-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5631d-132">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="5631d-133">**ülke kimliği**</span><span class="sxs-lookup"><span data-stu-id="5631d-133">**country-id**</span></span> | <span data-ttu-id="5631d-134">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="5631d-134">**string**</span></span> | <span data-ttu-id="5631d-135">Y</span><span class="sxs-lookup"><span data-stu-id="5631d-135">Y</span></span>        | <span data-ttu-id="5631d-136">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="5631d-136">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5631d-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5631d-137">Request headers</span></span>

<span data-ttu-id="5631d-138">Dize olarak biçimlendirilen bir **yerel ayar kimliği** gereklidir.</span><span class="sxs-lookup"><span data-stu-id="5631d-138">A **locale-id** formatted as a string is required.</span></span>

<span data-ttu-id="5631d-139">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5631d-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5631d-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5631d-140">Request body</span></span>

<span data-ttu-id="5631d-141">Yok.</span><span class="sxs-lookup"><span data-stu-id="5631d-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5631d-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5631d-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="5631d-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5631d-143">REST response</span></span>

<span data-ttu-id="5631d-144">Başarılı olursa, bu yöntem yanıt gövdesinde **Offercategory** kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="5631d-144">If successful, this method returns a collection of **OfferCategory** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5631d-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5631d-145">Response success and error codes</span></span>

<span data-ttu-id="5631d-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5631d-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5631d-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5631d-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5631d-148">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5631d-148">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5631d-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5631d-149">Response example</span></span>

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
