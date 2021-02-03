---
title: Microsoft Azure İş Ortağı Paylaşılan Hizmetleri için fiyat alma
description: Microsoft Azure Iş ortağı paylaşılan hizmetleri fiyatlarına sahip bir Azure ücret kartı alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cd396c35b6b89de4d0f092ba4da738a2ed0ac633
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769905"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a><span data-ttu-id="a5d55-103">Microsoft Azure İş Ortağı Paylaşılan Hizmetleri için fiyat alma</span><span class="sxs-lookup"><span data-stu-id="a5d55-103">Get prices for Microsoft Azure Partner Shared Services</span></span>

<span data-ttu-id="a5d55-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="a5d55-104">**Applies To**</span></span>

- <span data-ttu-id="a5d55-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a5d55-105">Partner Center</span></span>
- <span data-ttu-id="a5d55-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a5d55-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a5d55-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a5d55-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a5d55-108">Microsoft Azure Iş ortağı paylaşılan hizmetleri fiyatlarına sahip bir [Azure ücret kartı](azure-rate-card-resources.md) alma.</span><span class="sxs-lookup"><span data-stu-id="a5d55-108">How to get an [Azure Rate Card](azure-rate-card-resources.md) with prices for Microsoft Azure Partner Shared Services.</span></span>

<span data-ttu-id="a5d55-109">Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="a5d55-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="a5d55-110">Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a5d55-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="a5d55-111">Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="a5d55-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span>

## <a name="example-code"></a><span data-ttu-id="a5d55-112">Örnek kod</span><span class="sxs-lookup"><span data-stu-id="a5d55-112">Example Code</span></span>

## <a name="c"></a><span data-ttu-id="a5d55-113">C\#</span><span class="sxs-lookup"><span data-stu-id="a5d55-113">C\#</span></span>

<span data-ttu-id="a5d55-114">Azure fiyat kartını edinmek için, Azure fiyatlarını içeren bir [**Azursilinebilir tecard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) kaynağı döndürmek üzere [**ıazursilinebilir Tecard. getshared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="a5d55-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.GetShared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a><span data-ttu-id="a5d55-115">Java</span><span class="sxs-lookup"><span data-stu-id="a5d55-115">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a5d55-116">Azure fiyat kartını edinmek için, Azure fiyatlarını içeren hız kartı ayrıntılarını döndürmek üzere **ıazursilinebilir Tecard. getShared** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a5d55-116">To obtain the Azure Rate Card, call the **IAzureRateCard.getShared** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a><span data-ttu-id="a5d55-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a5d55-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a5d55-118">Azure kartını almak için [**Get-Partnerazursilinebilir Tecard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) komutunu yürütün ve Azure fiyatlarını içeren hız kartı ayrıntılarını döndürmek Için **SharedServices** parametresini belirtin.</span><span class="sxs-lookup"><span data-stu-id="a5d55-118">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command and specify the **SharedServices** parameter to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a><span data-ttu-id="a5d55-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a5d55-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a5d55-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a5d55-120">Request syntax</span></span>

| <span data-ttu-id="a5d55-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a5d55-121">Method</span></span>  | <span data-ttu-id="a5d55-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a5d55-122">Request URI</span></span>                                                               |
|---------|---------------------------------------------------------------------------|
| <span data-ttu-id="a5d55-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="a5d55-123">**GET**</span></span> | <span data-ttu-id="a5d55-124">*{BaseUrl}*/v1/ratecards/Azure-Shared? para birimi = {currency} &bölgesi = {Region}</span><span class="sxs-lookup"><span data-stu-id="a5d55-124">*{baseURL}*/v1/ratecards/azure-shared?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="a5d55-125">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a5d55-125">URI parameters</span></span>

| <span data-ttu-id="a5d55-126">Ad</span><span class="sxs-lookup"><span data-stu-id="a5d55-126">Name</span></span>     | <span data-ttu-id="a5d55-127">Tür</span><span class="sxs-lookup"><span data-stu-id="a5d55-127">Type</span></span>   | <span data-ttu-id="a5d55-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a5d55-128">Required</span></span> | <span data-ttu-id="a5d55-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a5d55-129">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a5d55-130">currency</span><span class="sxs-lookup"><span data-stu-id="a5d55-130">currency</span></span> | <span data-ttu-id="a5d55-131">dize</span><span class="sxs-lookup"><span data-stu-id="a5d55-131">string</span></span> | <span data-ttu-id="a5d55-132">No</span><span class="sxs-lookup"><span data-stu-id="a5d55-132">No</span></span>       | <span data-ttu-id="a5d55-133">Kaynak tarifelerinin sağlandığı para birimi için isteğe bağlı üç harfli ISO kodu (örneğin `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="a5d55-133">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="a5d55-134">Varsayılan değer, iş ortağı profilindeki Pazar ile ilişkili para birimidir.</span><span class="sxs-lookup"><span data-stu-id="a5d55-134">The default is the currency associated with the market in the partner profile.</span></span> |
| <span data-ttu-id="a5d55-135">region</span><span class="sxs-lookup"><span data-stu-id="a5d55-135">region</span></span>   | <span data-ttu-id="a5d55-136">dize</span><span class="sxs-lookup"><span data-stu-id="a5d55-136">string</span></span> | <span data-ttu-id="a5d55-137">No</span><span class="sxs-lookup"><span data-stu-id="a5d55-137">No</span></span>       | <span data-ttu-id="a5d55-138">Teklifin satın alındığı pazarı belirten, isteğe bağlı iki harfli ISO ülke/bölge kodu (örneğin `FR` ).</span><span class="sxs-lookup"><span data-stu-id="a5d55-138">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="a5d55-139">Varsayılan değer, iş ortağı profilinde ayarlanan ülke/bölge kodudur.</span><span class="sxs-lookup"><span data-stu-id="a5d55-139">The default is the country/region code set in the partner profile.</span></span>        |

<span data-ttu-id="a5d55-140">İsteğe bağlı X-locale üstbilgisi isteğe dahil ise, bu değer yanıttaki Ayrıntılar için kullanılan dili belirler.</span><span class="sxs-lookup"><span data-stu-id="a5d55-140">If the optional X-Locale header is included in the request, its value determines the language used for the details in the response.</span></span>

### <a name="request-headers"></a><span data-ttu-id="a5d55-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a5d55-141">Request headers</span></span>

<span data-ttu-id="a5d55-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a5d55-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a5d55-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a5d55-143">Request body</span></span>

<span data-ttu-id="a5d55-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="a5d55-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a5d55-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a5d55-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="a5d55-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a5d55-146">REST response</span></span>

<span data-ttu-id="a5d55-147">İstek başarılı olursa, bir [Azure ücret kartı](azure-rate-card-resources.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="a5d55-147">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a5d55-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a5d55-148">Response success and error codes</span></span>

<span data-ttu-id="a5d55-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a5d55-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a5d55-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a5d55-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a5d55-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a5d55-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a5d55-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a5d55-152">Response example</span></span>

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
