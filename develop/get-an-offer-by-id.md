---
title: Kimliğe göre bir teklif alma
description: Teklif kimliğiyle eşleşen bir Teklif kaynağı alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: f759cbdeefb4f550c41b41de40e9979e72e4ddeb
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760649"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="245f9-103">Kimliğe göre bir teklif alma</span><span class="sxs-lookup"><span data-stu-id="245f9-103">Get an offer by ID</span></span>

<span data-ttu-id="245f9-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="245f9-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="245f9-105">Teklif **kimliğiyle** eşleşen bir Teklif kaynağı alır.</span><span class="sxs-lookup"><span data-stu-id="245f9-105">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="245f9-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="245f9-106">Prerequisites</span></span>

- <span data-ttu-id="245f9-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="245f9-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="245f9-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="245f9-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="245f9-109">Teklif kimliği.</span><span class="sxs-lookup"><span data-stu-id="245f9-109">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="245f9-110">C\#</span><span class="sxs-lookup"><span data-stu-id="245f9-110">C\#</span></span>

<span data-ttu-id="245f9-111">Kimliğine göre belirli bir teklifi bulmak için **IAggregatePartner.Offers** koleksiyonu kullanın, **ByCountry()** çağrısıyla ülkeyi bulun ve [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="245f9-111">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="245f9-112">Ardından [**Get() veya**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) [**Get Async() yöntemini**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) çağırarak.</span><span class="sxs-lookup"><span data-stu-id="245f9-112">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="245f9-113">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="245f9-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="245f9-114">**Project:** PartnerSDK.FeatureSample **Sınıfı**: GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="245f9-114">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="245f9-115">Java</span><span class="sxs-lookup"><span data-stu-id="245f9-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="245f9-116">Kimliğine göre belirli bir teklifi bulmak için **IAggregatePartner.getOffers** işlevinizi kullanın, **byCountry()** işlevine bir çağrı ile ülkeyi bulun ve **byID()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="245f9-116">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="245f9-117">Ardından **get() işlevini** çağırarak.</span><span class="sxs-lookup"><span data-stu-id="245f9-117">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="245f9-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="245f9-118">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="245f9-119">Kimliğine göre belirli bir teklifi bulmak için [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) komutunu yürütün ve **CountryCode** ve **OfferId** parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="245f9-119">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="245f9-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="245f9-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="245f9-121">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="245f9-121">Request syntax</span></span>

| <span data-ttu-id="245f9-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="245f9-122">Method</span></span>  | <span data-ttu-id="245f9-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="245f9-123">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="245f9-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="245f9-124">**GET**</span></span> | <span data-ttu-id="245f9-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="245f9-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="245f9-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="245f9-126">URI parameter</span></span>

| <span data-ttu-id="245f9-127">Ad</span><span class="sxs-lookup"><span data-stu-id="245f9-127">Name</span></span>           | <span data-ttu-id="245f9-128">Tür</span><span class="sxs-lookup"><span data-stu-id="245f9-128">Type</span></span>       | <span data-ttu-id="245f9-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="245f9-129">Required</span></span> | <span data-ttu-id="245f9-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="245f9-130">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="245f9-131">**offer-id**</span><span class="sxs-lookup"><span data-stu-id="245f9-131">**offer-id**</span></span>   | <span data-ttu-id="245f9-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="245f9-132">**guid**</span></span>   | <span data-ttu-id="245f9-133">Y</span><span class="sxs-lookup"><span data-stu-id="245f9-133">Y</span></span>        | <span data-ttu-id="245f9-134">Teklife karşılık gelen GUID.</span><span class="sxs-lookup"><span data-stu-id="245f9-134">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="245f9-135">**country-id**</span><span class="sxs-lookup"><span data-stu-id="245f9-135">**country-id**</span></span> | <span data-ttu-id="245f9-136">**string**</span><span class="sxs-lookup"><span data-stu-id="245f9-136">**string**</span></span> | <span data-ttu-id="245f9-137">Y</span><span class="sxs-lookup"><span data-stu-id="245f9-137">Y</span></span>        | <span data-ttu-id="245f9-138">Ülke/bölge kimliği.</span><span class="sxs-lookup"><span data-stu-id="245f9-138">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="245f9-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="245f9-139">Request headers</span></span>

- <span data-ttu-id="245f9-140">Dize **olarak biçimlendirilmiş bir locale-id** gereklidir.</span><span class="sxs-lookup"><span data-stu-id="245f9-140">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="245f9-141">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="245f9-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="245f9-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="245f9-142">Request body</span></span>

<span data-ttu-id="245f9-143">Yok.</span><span class="sxs-lookup"><span data-stu-id="245f9-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="245f9-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="245f9-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="245f9-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="245f9-145">REST response</span></span>

<span data-ttu-id="245f9-146">Başarılı olursa, bu yöntem yanıt **gövdesinde** bir Teklif kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="245f9-146">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="245f9-147">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="245f9-147">Response success and error codes</span></span>

<span data-ttu-id="245f9-148">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="245f9-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="245f9-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="245f9-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="245f9-150">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="245f9-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="245f9-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="245f9-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1918
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
Date: Mon, 23 Nov 2015 23:13:01 GMT

{
    "id": "031C9E47-4802-4248-838E-778FB1D2CC05",
    "name": "Office 365 Business Premium",
    "description": "For businesses with 1 to 300 users that need the latest desktop version of Office,
                    plus anywhere access to email, filesharing, and online conferencing.",
    "minimumQuantity": 1,
    "maximumQuantity": 300,
    "rank": 56,
    "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/031C9E47-4802-4248-838E-778FB1D2CC05",
    "locale": "en-us",
    "country": "US",
    "category": {
        "id": "SmallBusiness_Key",
        "name": "Small Business",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    "prerequisiteOffers": [],
    "isAddOn": false,
    "isAvailableForPurchase": true,
    "billing": "license",
    "isAutoRenewable": true,
    "product": {
        "id": "f245ecc8-75af-4f8e-b61f-27d8114de5f3",
        "name": "Office 365 Business Premium",
        "unit": "Licenses"
    },
    "unitType": "Licenses",
    "links": {
        "learnMore": {
            "uri": "http: //g.microsoftonline.com/0BXPS00en/909",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Offer"
    }
}
```
