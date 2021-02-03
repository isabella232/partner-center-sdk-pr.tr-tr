---
title: Kimliğe göre bir teklif alma
description: Teklif KIMLIĞIYLE eşleşen bir teklif kaynağı alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: brentserbus
ms.author: brserbus
ms.openlocfilehash: 9448276e817affb823eddabbcab8757c79615fbd
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769910"
---
# <a name="get-an-offer-by-id"></a><span data-ttu-id="a3147-103">Kimliğe göre bir teklif alma</span><span class="sxs-lookup"><span data-stu-id="a3147-103">Get an offer by ID</span></span>

<span data-ttu-id="a3147-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="a3147-104">**Applies To**</span></span>

- <span data-ttu-id="a3147-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a3147-105">Partner Center</span></span>
- <span data-ttu-id="a3147-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a3147-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a3147-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a3147-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a3147-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a3147-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a3147-109">Teklif KIMLIĞIYLE eşleşen bir **teklif** kaynağı alır.</span><span class="sxs-lookup"><span data-stu-id="a3147-109">Gets an **Offer** resource that matches the offer ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a3147-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a3147-110">Prerequisites</span></span>

- <span data-ttu-id="a3147-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a3147-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a3147-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="a3147-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a3147-113">Bir teklif KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="a3147-113">An offer ID.</span></span>

## <a name="c"></a><span data-ttu-id="a3147-114">C\#</span><span class="sxs-lookup"><span data-stu-id="a3147-114">C\#</span></span>

<span data-ttu-id="a3147-115">KIMLIĞE göre belirli bir teklifi bulmak için **ıaggregatepartner. tekliflerini** kullanın, bir **bycountry ()** çağrısı yaparak ülkeyi oluşturun ve ardından [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a3147-115">To find a specific offer by ID, use your **IAggregatePartner.Offers** collection, establish the country with a call to **ByCountry()**, and then call the [**ByID()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.byid) method.</span></span> <span data-ttu-id="a3147-116">Sonra [**Get ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) veya [**Get Async ()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="a3147-116">Then, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.get) or [**Get Async()**](/dotnet/api/microsoft.store.partnercenter.offers.ioffercollection.getasync) method.</span></span>

```csharp
// IAggretagePartner partnerOperations;
// string countryCode;
// string offerId;

// retrieve the offer
var offer = partnerOperations.Offers.ByCountry(countryCode).ById(offerId).Get();
```

<span data-ttu-id="a3147-117">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a3147-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a3147-118">**Proje**: Partnersdk. Featuresample **sınıfı**: GetOffer.cs</span><span class="sxs-lookup"><span data-stu-id="a3147-118">**Project**: PartnerSDK.FeatureSample **Class**: GetOffer.cs</span></span>

## <a name="java"></a><span data-ttu-id="a3147-119">Java</span><span class="sxs-lookup"><span data-stu-id="a3147-119">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a3147-120">KIMLIĞE göre belirli bir teklifi bulmak için, **ıaggregatepartner. getOffers** işlevinizi kullanın, **bycountry ()** işlevine çağrı yaparak ülkeyi oluşturun ve ardından **byıd ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a3147-120">To find a specific offer by ID, use your **IAggregatePartner.getOffers** function, establish the country with a call to the **byCountry()** function, and then call the **byID()** function.</span></span> <span data-ttu-id="a3147-121">Sonra **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a3147-121">Then call the **get()** function.</span></span>

```java
// IAggretagePartner partnerOperations;
// String countryCode;
// String offerId;

// Retrieve the offer
Offer offer = partnerOperations.getOffers().byCountry(countryCode).byId(offerId).get();
```

## <a name="powershell"></a><span data-ttu-id="a3147-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a3147-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a3147-123">KIMLIĞE göre belirli bir teklifi bulmak için [**Get-Partnerteklifinizin**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) komutunu yürütün ve **CountryCode** ve **OfferId** parametrelerini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a3147-123">To find a specific offer by ID, execute the [**Get-PartnerOffer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOffer.md) command, and specify the **CountryCode** and **OfferId** parameters.</span></span>

```powershell
# $countryCode
# $offerId

Get-PartnerOffer -Country $countryCode -OfferId $offerId
```

## <a name="rest-request"></a><span data-ttu-id="a3147-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a3147-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a3147-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a3147-125">Request syntax</span></span>

| <span data-ttu-id="a3147-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a3147-126">Method</span></span>  | <span data-ttu-id="a3147-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a3147-127">Request URI</span></span>                                                                                    |
|---------|------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a3147-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="a3147-128">**GET**</span></span> | <span data-ttu-id="a3147-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/offers/{Offer-id}? ülke = {ülke-KIMLIĞI} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a3147-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers/{offer-id}?country={country-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="a3147-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="a3147-130">URI parameter</span></span>

| <span data-ttu-id="a3147-131">Ad</span><span class="sxs-lookup"><span data-stu-id="a3147-131">Name</span></span>           | <span data-ttu-id="a3147-132">Tür</span><span class="sxs-lookup"><span data-stu-id="a3147-132">Type</span></span>       | <span data-ttu-id="a3147-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a3147-133">Required</span></span> | <span data-ttu-id="a3147-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a3147-134">Description</span></span>                           |
|----------------|------------|----------|---------------------------------------|
| <span data-ttu-id="a3147-135">**teklif kimliği**</span><span class="sxs-lookup"><span data-stu-id="a3147-135">**offer-id**</span></span>   | <span data-ttu-id="a3147-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="a3147-136">**guid**</span></span>   | <span data-ttu-id="a3147-137">Y</span><span class="sxs-lookup"><span data-stu-id="a3147-137">Y</span></span>        | <span data-ttu-id="a3147-138">Teklifine karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="a3147-138">A GUID that corresponds to the offer.</span></span> |
| <span data-ttu-id="a3147-139">**ülke kimliği**</span><span class="sxs-lookup"><span data-stu-id="a3147-139">**country-id**</span></span> | <span data-ttu-id="a3147-140">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="a3147-140">**string**</span></span> | <span data-ttu-id="a3147-141">Y</span><span class="sxs-lookup"><span data-stu-id="a3147-141">Y</span></span>        | <span data-ttu-id="a3147-142">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="a3147-142">The country/region ID.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="a3147-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a3147-143">Request headers</span></span>

- <span data-ttu-id="a3147-144">Dize olarak biçimlendirilen bir **yerel ayar kimliği** gereklidir.</span><span class="sxs-lookup"><span data-stu-id="a3147-144">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="a3147-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a3147-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a3147-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a3147-146">Request body</span></span>

<span data-ttu-id="a3147-147">Yok.</span><span class="sxs-lookup"><span data-stu-id="a3147-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a3147-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a3147-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers/<offer-id>?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ac943950-ba3d-47a0-bd2a-c5617a7fefe8
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a3147-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a3147-149">REST response</span></span>

<span data-ttu-id="a3147-150">Başarılı olursa, bu yöntem yanıt gövdesinde bir **teklif** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="a3147-150">If successful, this method returns an **Offer** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a3147-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a3147-151">Response success and error codes</span></span>

<span data-ttu-id="a3147-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a3147-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a3147-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a3147-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a3147-154">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a3147-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a3147-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a3147-155">Response example</span></span>

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
