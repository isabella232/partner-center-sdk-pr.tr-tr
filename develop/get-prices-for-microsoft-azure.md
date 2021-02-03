---
title: Microsoft Azure için fiyat alma
description: Azure teklifi için gerçek zamanlı fiyatlara sahip bir Azure ücret kartı alma. Azure fiyatlandırması oldukça dinamik ve sık sık değişir.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0716f0428b13604105b435a2ce8287a8b4609fea
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97770293"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="a1706-104">Microsoft Azure için fiyat alma</span><span class="sxs-lookup"><span data-stu-id="a1706-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="a1706-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="a1706-105">**Applies To**</span></span>

- <span data-ttu-id="a1706-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a1706-106">Partner Center</span></span>
- <span data-ttu-id="a1706-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a1706-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a1706-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a1706-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a1706-109">Azure teklifi için gerçek zamanlı fiyatlara sahip bir [Azure ücret kartı](azure-rate-card-resources.md) alma.</span><span class="sxs-lookup"><span data-stu-id="a1706-109">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="a1706-110">Azure fiyatlandırması oldukça dinamik ve sık sık değişir.</span><span class="sxs-lookup"><span data-stu-id="a1706-110">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="a1706-111">Kullanımı izlemek ve aylık faturanızı ve tek tek müşterilerin ücretini tahmin etmeye yardımcı olmak için, [Azure için bir müşterinin kullanım kayıtlarını almaya](get-a-customer-s-utilization-record-for-azure.md)yönelik bir istekle Microsoft Azure fiyatlarını almak üzere bu Azure fiyatı kartı sorgusunu birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1706-111">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="a1706-112">Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="a1706-112">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="a1706-113">Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="a1706-113">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="a1706-114">Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="a1706-114">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="a1706-115">Daha fazla bilgi için bkz. [URI parametreleri](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="a1706-115">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="a1706-116">C\#</span><span class="sxs-lookup"><span data-stu-id="a1706-116">C\#</span></span>

<span data-ttu-id="a1706-117">Azure fiyat kartını edinmek için, Azure fiyatlarını içeren [**Azursilinebilir tecard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) kaynağını döndürmek üzere [**ıazursilinebilir Tecard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="a1706-117">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="a1706-118">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="a1706-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="a1706-119">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetAzureRateCard.cs</span><span class="sxs-lookup"><span data-stu-id="a1706-119">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="a1706-120">Java</span><span class="sxs-lookup"><span data-stu-id="a1706-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a1706-121">Azure fiyat kartını edinmek için **ıazursilinebilir Tecard. Get** Işlevini çağırıp Azure fiyatlarını içeren ücret kartı ayrıntılarını döndürün.</span><span class="sxs-lookup"><span data-stu-id="a1706-121">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="a1706-122">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a1706-122">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a1706-123">Azure kartını almak için [**Get-Partnerazursilinebilir Tecard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) komutunu çalıştırarak Azure fiyatlarını içeren ücret kartı ayrıntılarını döndürün.</span><span class="sxs-lookup"><span data-stu-id="a1706-123">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="a1706-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a1706-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a1706-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a1706-125">Request syntax</span></span>

| <span data-ttu-id="a1706-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a1706-126">Method</span></span>  | <span data-ttu-id="a1706-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a1706-127">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="a1706-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="a1706-128">**GET**</span></span> | <span data-ttu-id="a1706-129">*{BaseUrl}*/v1/ratecards/Azure? para birimi = {currency} &bölgesi = {Region}</span><span class="sxs-lookup"><span data-stu-id="a1706-129">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="a1706-130">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a1706-130">URI parameters</span></span>

| <span data-ttu-id="a1706-131">Ad</span><span class="sxs-lookup"><span data-stu-id="a1706-131">Name</span></span>     | <span data-ttu-id="a1706-132">Tür</span><span class="sxs-lookup"><span data-stu-id="a1706-132">Type</span></span>   | <span data-ttu-id="a1706-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a1706-133">Required</span></span> | <span data-ttu-id="a1706-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a1706-134">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a1706-135">currency</span><span class="sxs-lookup"><span data-stu-id="a1706-135">currency</span></span> | <span data-ttu-id="a1706-136">dize</span><span class="sxs-lookup"><span data-stu-id="a1706-136">string</span></span> | <span data-ttu-id="a1706-137">No</span><span class="sxs-lookup"><span data-stu-id="a1706-137">No</span></span>       | <span data-ttu-id="a1706-138">Kaynak tarifelerinin sağlandığı para birimi için isteğe bağlı üç harfli ISO kodu (örneğin `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="a1706-138">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="a1706-139">Varsayılan değer: `USD`.</span><span class="sxs-lookup"><span data-stu-id="a1706-139">The default is `USD`.</span></span> |
| <span data-ttu-id="a1706-140">region</span><span class="sxs-lookup"><span data-stu-id="a1706-140">region</span></span>   | <span data-ttu-id="a1706-141">dize</span><span class="sxs-lookup"><span data-stu-id="a1706-141">string</span></span> | <span data-ttu-id="a1706-142">No</span><span class="sxs-lookup"><span data-stu-id="a1706-142">No</span></span>       | <span data-ttu-id="a1706-143">Teklifin satın alındığı pazarı belirten, isteğe bağlı iki harfli ISO ülke/bölge kodu (örneğin `FR` ).</span><span class="sxs-lookup"><span data-stu-id="a1706-143">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="a1706-144">Varsayılan değer: `US`.</span><span class="sxs-lookup"><span data-stu-id="a1706-144">The default is `US`.</span></span>        |

<span data-ttu-id="a1706-145">İsteğe bağlı X-locale [üst bilgisini](headers.md#rest-request-headers) isteğinize dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a1706-145">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="a1706-146">X-locale üst bilgisini eklemezseniz, varsayılan değer ("en-US") kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1706-146">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="a1706-147">İsteğiniz için para birimi ve bölge parametreleri sağlarsanız, yanıtın dilini belirlemekte X-locale değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1706-147">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="a1706-148">İsteğiniz içinde bölge ve para birimi parametreleri sağlamazsanız, yanıtın bölge, para birimi ve dilini belirlemekte X-locale değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="a1706-148">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="a1706-149">İstek üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="a1706-149">Request header</span></span>

<span data-ttu-id="a1706-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a1706-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a1706-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a1706-151">Request body</span></span>

<span data-ttu-id="a1706-152">Yok.</span><span class="sxs-lookup"><span data-stu-id="a1706-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a1706-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a1706-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="a1706-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a1706-154">REST response</span></span>

<span data-ttu-id="a1706-155">İstek başarılı olursa, bir [Azure ücret kartı](azure-rate-card-resources.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="a1706-155">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a1706-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a1706-156">Response success and error codes</span></span>

<span data-ttu-id="a1706-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a1706-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a1706-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a1706-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a1706-159">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a1706-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a1706-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a1706-160">Response example</span></span>

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
    "locale": "en",
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
