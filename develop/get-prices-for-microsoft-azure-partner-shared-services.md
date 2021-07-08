---
title: Microsoft Azure İş Ortağı Paylaşılan Hizmetleri için fiyat alma
description: Microsoft Azure iş ortağı paylaşılan hizmetleri fiyatlarına sahip bir Azure ücret kartı alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0008d7474f7e57bbbd765afdf2487ee279848ac3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548813"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="3fa8c-103">Microsoft Azure İş Ortağı Paylaşılan Hizmetleri için fiyat alma</span><span class="sxs-lookup"><span data-stu-id="3fa8c-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="3fa8c-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3fa8c-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="3fa8c-105">Microsoft Azure iş ortağı paylaşılan hizmetleri fiyatlarına sahip bir [Azure ücret kartı](azure-rate-card-resources.md) alma.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-105">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="3fa8c-106">Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-106">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="3fa8c-107">Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-107">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="3fa8c-108">Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-108">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="3fa8c-109">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="3fa8c-109">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="3fa8c-110">C\#</span><span class="sxs-lookup"><span data-stu-id="3fa8c-110">C\#</span></span>

<span data-ttu-id="3fa8c-111">Azure fiyat kartını edinmek için, Azure fiyatlarını içeren bir [**Azursilinebilir tecard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) kaynağı döndürmek üzere [**ıazursilinebilir Tecard. getshared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-111">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="3fa8c-112">Java</span><span class="sxs-lookup"><span data-stu-id="3fa8c-112">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="3fa8c-113">Azure fiyat kartını edinmek için, Azure fiyatlarını içeren hız kartı ayrıntılarını döndürmek üzere **ıazursilinebilir Tecard. getShared** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-113">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="3fa8c-114">PowerShell</span><span class="sxs-lookup"><span data-stu-id="3fa8c-114">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="3fa8c-115">Azure kartını almak için [**Get-Partnerazursilinebilir Tecard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) komutunu yürütün ve Azure fiyatlarını içeren hız kartı ayrıntılarını döndürmek Için **SharedServices** parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-115">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="3fa8c-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3fa8c-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3fa8c-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3fa8c-117">Request syntax</span></span>

| <span data-ttu-id="3fa8c-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3fa8c-118">Method</span></span>  | <span data-ttu-id="3fa8c-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3fa8c-119">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="3fa8c-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="3fa8c-120">**GET**</span></span> | <span data-ttu-id="3fa8c-121">*{BaseUrl}*/v1/ratecards/Azure-Shared? para birimi = {currency} &bölgesi = {Region}</span><span class="sxs-lookup"><span data-stu-id="3fa8c-121">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="3fa8c-122">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="3fa8c-122">URI parameters</span></span>

| <span data-ttu-id="3fa8c-123">Ad</span><span class="sxs-lookup"><span data-stu-id="3fa8c-123">Name</span></span>     | <span data-ttu-id="3fa8c-124">Tür</span><span class="sxs-lookup"><span data-stu-id="3fa8c-124">Type</span></span>   | <span data-ttu-id="3fa8c-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3fa8c-125">Required</span></span> | <span data-ttu-id="3fa8c-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3fa8c-126">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3fa8c-127">currency</span><span class="sxs-lookup"><span data-stu-id="3fa8c-127">currency</span></span> | <span data-ttu-id="3fa8c-128">dize</span><span class="sxs-lookup"><span data-stu-id="3fa8c-128">string</span></span> | <span data-ttu-id="3fa8c-129">No</span><span class="sxs-lookup"><span data-stu-id="3fa8c-129">No</span></span>       | <span data-ttu-id="3fa8c-130">Kaynak tarifelerinin sağlandığı para birimi için isteğe bağlı üç harfli ISO kodu (örneğin `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="3fa8c-130">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="3fa8c-131">Varsayılan değer, iş ortağı profilindeki Pazar ile ilişkili para birimidir.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-131">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="3fa8c-132">region</span><span class="sxs-lookup"><span data-stu-id="3fa8c-132">region</span></span>   | <span data-ttu-id="3fa8c-133">dize</span><span class="sxs-lookup"><span data-stu-id="3fa8c-133">string</span></span> | <span data-ttu-id="3fa8c-134">No</span><span class="sxs-lookup"><span data-stu-id="3fa8c-134">No</span></span>       | <span data-ttu-id="3fa8c-135">Teklifin satın alındığı pazarı belirten, isteğe bağlı iki harfli ISO ülke/bölge kodu (örneğin `FR` ).</span><span class="sxs-lookup"><span data-stu-id="3fa8c-135">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="3fa8c-136">Varsayılan değer, iş ortağı profilinde ayarlanan ülke/bölge kodudur.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-136">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="3fa8c-137">İsteğe bağlı X-locale üstbilgisi isteğe dahil ise, bu değer yanıttaki Ayrıntılar için kullanılan dili belirler.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-137">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="3fa8c-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3fa8c-138">Request headers</span></span>

<span data-ttu-id="3fa8c-139">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3fa8c-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3fa8c-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3fa8c-140">Request body</span></span>

<span data-ttu-id="3fa8c-141">Yok.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="3fa8c-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3fa8c-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="3fa8c-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3fa8c-143">REST response</span></span>

<span data-ttu-id="3fa8c-144">İstek başarılı olursa, bir [Azure ücret kartı](azure-rate-card-resources.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-144">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3fa8c-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3fa8c-145">Response success and error codes</span></span>

<span data-ttu-id="3fa8c-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3fa8c-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3fa8c-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3fa8c-148">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3fa8c-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3fa8c-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3fa8c-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
