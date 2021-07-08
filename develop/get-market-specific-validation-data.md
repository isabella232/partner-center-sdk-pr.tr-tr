---
title: Pazara göre adres biçimlendirme kurallarını alma
description: Pazarın iso koduna göre beklenen adres biçimini elde edin.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5233d059ea6e71c28df36b2242659c28c5dd857
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549051"
---
# <a name="get-address-formatting-rules-by-market"></a><span data-ttu-id="86584-103">Pazara göre adres biçimlendirme kurallarını alma</span><span class="sxs-lookup"><span data-stu-id="86584-103">Get address formatting rules by market</span></span>

<span data-ttu-id="86584-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="86584-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>


<span data-ttu-id="86584-105">Pazarın iso koduna göre beklenen adres biçimini elde edin.</span><span class="sxs-lookup"><span data-stu-id="86584-105">Get the expected address format based on the iso code for the market.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="86584-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="86584-106">Prerequisites</span></span>

- <span data-ttu-id="86584-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="86584-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="86584-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="86584-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="rest-request"></a><span data-ttu-id="86584-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="86584-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="86584-110">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="86584-110">Request syntax</span></span>

| <span data-ttu-id="86584-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="86584-111">Method</span></span>  | <span data-ttu-id="86584-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="86584-112">Request URI</span></span>                                                                                 |
|---------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="86584-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="86584-113">**GET**</span></span> | <span data-ttu-id="86584-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="86584-114">[*{baseURL}*](partner-center-rest-urls.md)/v1/countryvalidationrules/{isocode-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="86584-115">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="86584-115">URI parameter</span></span>

| <span data-ttu-id="86584-116">Ad</span><span class="sxs-lookup"><span data-stu-id="86584-116">Name</span></span>           | <span data-ttu-id="86584-117">Tür</span><span class="sxs-lookup"><span data-stu-id="86584-117">Type</span></span>       | <span data-ttu-id="86584-118">Gerekli</span><span class="sxs-lookup"><span data-stu-id="86584-118">Required</span></span> | <span data-ttu-id="86584-119">Açıklama</span><span class="sxs-lookup"><span data-stu-id="86584-119">Description</span></span>                         |
|----------------|------------|----------|-------------------------------------|
| <span data-ttu-id="86584-120">**isocode-id**</span><span class="sxs-lookup"><span data-stu-id="86584-120">**isocode-id**</span></span> | <span data-ttu-id="86584-121">**string**</span><span class="sxs-lookup"><span data-stu-id="86584-121">**string**</span></span> | <span data-ttu-id="86584-122">Y</span><span class="sxs-lookup"><span data-stu-id="86584-122">Y</span></span>        | <span data-ttu-id="86584-123">İki karakterli ISO ülke kodu.</span><span class="sxs-lookup"><span data-stu-id="86584-123">The two-character ISO country code.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="86584-124">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="86584-124">Request headers</span></span>

<span data-ttu-id="86584-125">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="86584-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="86584-126">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="86584-126">Request body</span></span>

<span data-ttu-id="86584-127">Yok.</span><span class="sxs-lookup"><span data-stu-id="86584-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="86584-128">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="86584-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/countryvalidationrules/{isocode-id} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 124b0e41-a093-4fec-b871-3eeb45fd734b
MS-CorrelationId: 5cfd634d-b936-47af-87f0-0f0217425dcc
```

## <a name="rest-response"></a><span data-ttu-id="86584-129">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="86584-129">REST response</span></span>

<span data-ttu-id="86584-130">Başarılı olursa, bu yöntem yanıt **gövdesinde bir CountryInformation** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="86584-130">If successful, this method returns a **CountryInformation** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="86584-131">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="86584-131">Response success and error codes</span></span>

<span data-ttu-id="86584-132">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="86584-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="86584-133">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="86584-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="86584-134">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="86584-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="86584-135">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="86584-135">Response example</span></span>

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
