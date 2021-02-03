---
title: Pazara göre adres biçimlendirme kurallarını alma
description: Pazara yönelik ISO koduna göre beklenen adres biçimini alın.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c755a38c11ed9803edb7777a0f661c1fbc5a6107
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769005"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="4d937-103">Pazara göre adres biçimlendirme kurallarını alma</span><span class="sxs-lookup"><span data-stu-id="4d937-103">Get address formatting rules by market</span></span>

<span data-ttu-id="4d937-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="4d937-104">**Applies To**</span></span>

- <span data-ttu-id="4d937-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4d937-105">Partner Center</span></span>
- <span data-ttu-id="4d937-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4d937-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4d937-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4d937-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4d937-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4d937-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4d937-109">Pazara yönelik ISO koduna göre beklenen adres biçimini alın.</span><span class="sxs-lookup"><span data-stu-id="4d937-109">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4d937-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4d937-110">Prerequisites</span></span>

- <span data-ttu-id="4d937-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4d937-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4d937-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4d937-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="4d937-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4d937-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4d937-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4d937-114">Request syntax</span></span>

| <span data-ttu-id="4d937-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4d937-115">Method</span></span>  | <span data-ttu-id="4d937-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4d937-116">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="4d937-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="4d937-117">**GET**</span></span> | <span data-ttu-id="4d937-118">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/countryvalidationkurallarını/{ısocode-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4d937-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="4d937-119">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="4d937-119">URI parameter</span></span>

| <span data-ttu-id="4d937-120">Ad</span><span class="sxs-lookup"><span data-stu-id="4d937-120">Name</span></span>           | <span data-ttu-id="4d937-121">Tür</span><span class="sxs-lookup"><span data-stu-id="4d937-121">Type</span></span>       | <span data-ttu-id="4d937-122">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4d937-122">Required</span></span> | <span data-ttu-id="4d937-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4d937-123">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="4d937-124">**ısocode kimliği**</span><span class="sxs-lookup"><span data-stu-id="4d937-124">**isocode-id**</span></span> | <span data-ttu-id="4d937-125">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="4d937-125">**string**</span></span> | <span data-ttu-id="4d937-126">Y</span><span class="sxs-lookup"><span data-stu-id="4d937-126">Y</span></span>        | <span data-ttu-id="4d937-127">İki karakterlik ISO ülke kodu.</span><span class="sxs-lookup"><span data-stu-id="4d937-127">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4d937-128">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4d937-128">Request headers</span></span>

<span data-ttu-id="4d937-129">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4d937-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4d937-130">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4d937-130">Request body</span></span>

<span data-ttu-id="4d937-131">Yok.</span><span class="sxs-lookup"><span data-stu-id="4d937-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4d937-132">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4d937-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="4d937-133">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4d937-133">REST response</span></span>

<span data-ttu-id="4d937-134">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Countryınformation** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="4d937-134">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4d937-135">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4d937-135">Response success and error codes</span></span>

<span data-ttu-id="4d937-136">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4d937-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4d937-137">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4d937-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4d937-138">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4d937-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4d937-139">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4d937-139">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1856
Content-Type: application/json
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
Date: Wed, 25 Nov 2015 06:36:47 GMT

{
    "iso2Code": "US",
    "defaultCulture": "en-US",
    "isStateRequired": true,
    "states": {
        "value": ["AK","AL","AR", "AZ","CA","CO","CT","DC","DE","FL","GA","HI","IA","ID","IL","IN",
        "KS","KY","LA","MA","MD","ME","MI","MN","MO","MS","MT","NC","ND","NE","NH","NJ","NM","NV",
        "NY","OH","OK","OR","PA","RI","SC","SD","TN","TX","UT","VA","VT","WA","WI","WV","WY"]
    },
    "supportedLanguages": {
        "value": ["en",
        "es"]
    },
    "supportedCultures": {
        "value": ["en-US",
        "es-US"]
    },
    "isPostalCodeRequired": true,
    "postalCodeRegex": "^\\d{
        5
    }(-\\d{
        4
    })?$",
    "isCityRequired": true,
    "isVatIdSupported": false,
    "taxIdFormat": "US######",
    "taxIdSample": "US999965",
    "phoneNumberRegex": "^(1[\\-\\/\\.]?)?(\((\\d{3})\)|(\\d{3}))[\\-\\/\\.]?(\\d{3})[\\-\\/\\.]?(\\d{4})$",
    "isRegistrationNumberSupported": false,
    "isTaxIdSupported": true,
    "resellerAgreementRegion": "AOC",
    "geographicRegion": "NorthAndLatinAmerica",
    "countryCallingCodes": {
        "value": ["1"]
    },
    "attributes": {
        "objectType": "CountryInformation"
    }
}
```
