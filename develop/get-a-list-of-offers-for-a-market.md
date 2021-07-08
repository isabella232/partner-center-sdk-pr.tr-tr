---
title: Pazara yönelik tekliflerin bir listesini alma
description: Belirli bir pazar için tüm teklifleri içeren bir koleksiyon alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 6f4fd821879545db4e781fe3202c8ee11f167615
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874253"
---
# <a name="get-a-list-of-offers-for-a-market"></a><span data-ttu-id="942ba-103">Pazara yönelik tekliflerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="942ba-103">Get a list of offers for a market</span></span>

<span data-ttu-id="942ba-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="942ba-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="942ba-105">Belirli bir pazar için tüm teklifleri içeren bir koleksiyon alır.</span><span class="sxs-lookup"><span data-stu-id="942ba-105">Gets a collection that contains all the offers for a specific market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="942ba-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="942ba-106">Prerequisites</span></span>

- <span data-ttu-id="942ba-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="942ba-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="942ba-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="942ba-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="942ba-109">C\#</span><span class="sxs-lookup"><span data-stu-id="942ba-109">C\#</span></span>

<span data-ttu-id="942ba-110">Belirli bir pazardaki tekliflerin listesini almak için **ıaggregatepartner. tekliflerini** kullanın, ülkeye göre pazara seçin ve **Get ()** veya **Get Async ()** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="942ba-110">To get a list of offers in a given market, use your **IAggregatePartner.Offers** collection, select the market by country, and call the **Get()** or **Get Async()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<Offer> offers = partnerOperations.Offers.ByCountry("US").Get();
```

<span data-ttu-id="942ba-111">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="942ba-111">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="942ba-112">**Project**: partnersdk. featuresample **sınıfı**: teklifler. cs</span><span class="sxs-lookup"><span data-stu-id="942ba-112">**Project**: PartnerSDK.FeatureSample **Class**: Offers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="942ba-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="942ba-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="942ba-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="942ba-114">Request syntax</span></span>

| <span data-ttu-id="942ba-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="942ba-115">Method</span></span>  | <span data-ttu-id="942ba-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="942ba-116">Request URI</span></span>                                                                          |
|---------|--------------------------------------------------------------------------------------|
| <span data-ttu-id="942ba-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="942ba-117">**GET**</span></span> | <span data-ttu-id="942ba-118">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/tekliflere? ülke = {ülke-KIMLIĞI} http/1.1</span><span class="sxs-lookup"><span data-stu-id="942ba-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/offers?country={country-id} HTTP/1.1</span></span>   |

### <a name="uri-parameter"></a><span data-ttu-id="942ba-119">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="942ba-119">URI parameter</span></span>

<span data-ttu-id="942ba-120">Bu tablo, teklifleri almak için gerekli sorgu parametrelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="942ba-120">This table lists the required query parameters to get the offers.</span></span>

| <span data-ttu-id="942ba-121">Ad</span><span class="sxs-lookup"><span data-stu-id="942ba-121">Name</span></span>           | <span data-ttu-id="942ba-122">Tür</span><span class="sxs-lookup"><span data-stu-id="942ba-122">Type</span></span>       | <span data-ttu-id="942ba-123">Gerekli</span><span class="sxs-lookup"><span data-stu-id="942ba-123">Required</span></span> | <span data-ttu-id="942ba-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="942ba-124">Description</span></span>            |
|----------------|------------|----------|------------------------|
| <span data-ttu-id="942ba-125">**ülke kimliği**</span><span class="sxs-lookup"><span data-stu-id="942ba-125">**country-id**</span></span> | <span data-ttu-id="942ba-126">**string**</span><span class="sxs-lookup"><span data-stu-id="942ba-126">**string**</span></span> | <span data-ttu-id="942ba-127">Y</span><span class="sxs-lookup"><span data-stu-id="942ba-127">Y</span></span>        | <span data-ttu-id="942ba-128">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="942ba-128">The country/region ID.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="942ba-129">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="942ba-129">Request headers</span></span>

- <span data-ttu-id="942ba-130">Dize olarak biçimlendirilen bir **yerel ayar kimliği** gereklidir.</span><span class="sxs-lookup"><span data-stu-id="942ba-130">A **locale-id** formatted as a string is required.</span></span>
<span data-ttu-id="942ba-131">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="942ba-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="942ba-132">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="942ba-132">Request body</span></span>

<span data-ttu-id="942ba-133">Yok.</span><span class="sxs-lookup"><span data-stu-id="942ba-133">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="942ba-134">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="942ba-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/offers?country=<country-id> HTTP/1.1
Authorization: Bearer
Accept: application/json
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
X-Locale: <locale-id>
```

## <a name="rest-response"></a><span data-ttu-id="942ba-135">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="942ba-135">REST response</span></span>

<span data-ttu-id="942ba-136">Başarılı olursa, bu yöntem yanıt gövdesinde bir **teklif** kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="942ba-136">If successful, this method returns a collection of **Offer** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="942ba-137">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="942ba-137">Response success and error codes</span></span>

<span data-ttu-id="942ba-138">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="942ba-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="942ba-139">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="942ba-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="942ba-140">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="942ba-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="942ba-141">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="942ba-141">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 26584
Content-Type: application/json
MS-CorrelationId: 7c1f6619-c176-4040-a88f-2c71f3ba4533
MS-RequestId: 031160b2-b0b0-4d40-b2b1-aaa9bb84211d
Date: Mon, 23 Nov 2015 23:20:44 GMT

{
    "totalCount":12,"items":[{
        "id":"E60E0348-1710-484B-992A-32B294D4CDE1",
        "name":"Azure Rights Management Premium (Government Pricing)",
        "description":"Microsoft Azure Rights Management Premium helps you protect confidential documents and email with strong encryption.
                       Control the use of your information by specifying who can view, edit, print, save and share your data.
                       Simple to use and integrated with Microsoft Office, SharePoint and Exchange.",
        "minimumQuantity":1,
        "maximumQuantity":10000000,
        "rank":5,
        "uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/E60E0348-1710-484B-992A-32B294D4CDE1",
        "locale":"EN-US",
        "country":"US",
        "category":{
            "id":"Government_Key",
            "name":"Government",
            "rank":40,
            "locale":"en-us",
            "country":"US",
            "attributes":{
                "objectType":"OfferCategory"
            }
        },
        "prerequisiteOffers":[],
        "isAddOn":false,
        "isAvailableForPurchase":true,
        "billing":"license",
        "isAutoRenewable":true,
        "product":{
            "id":"c52ea49f-fe5d-4e95-93ba-1de91d380f89",
            "name":"Azure Rights Management Premium",
            "unit":"Licenses"
        },
        "unitType":"Licenses",
        "links":{
            "learnMore":{
                "uri":"http://g.microsoftonline.com/0BXPS00en/0000",
                "method":"GET",
                "headers":[]
            },
            "self":{
                "uri":"/offers/E60E0348-1710-484B-992A-32B294D4CDE1",
                "method":"GET",
                "headers":[]
            }
        },
        "attributes":{
            "objectType":"Offer"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        },
        "previous":{
            "uri":"/v1/offers?country={country-id}",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"Collection"
    }
}
```
