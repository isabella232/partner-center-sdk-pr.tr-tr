---
title: Microsoft Azure için fiyat alma
description: Azure teklifi için gerçek zamanlı fiyatlara sahip bir Azure ücret kartı alma. Azure fiyatlandırması oldukça dinamik ve sık sık değişir.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4f66ab19ef3723fbaa27acff941cf48683a7c25c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548796"
---
# <a name="get-prices-for-microsoft-azure"></a><span data-ttu-id="84cc3-104">Microsoft Azure için fiyat alma</span><span class="sxs-lookup"><span data-stu-id="84cc3-104">Get prices for Microsoft Azure</span></span>

<span data-ttu-id="84cc3-105">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="84cc3-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="84cc3-106">Azure teklifi için gerçek zamanlı fiyatlara sahip bir [Azure ücret kartı](azure-rate-card-resources.md) alma.</span><span class="sxs-lookup"><span data-stu-id="84cc3-106">How to get an [Azure Rate Card](azure-rate-card-resources.md) with real-time prices for an Azure offer.</span></span> <span data-ttu-id="84cc3-107">Azure fiyatlandırması oldukça dinamik ve sık sık değişir.</span><span class="sxs-lookup"><span data-stu-id="84cc3-107">Azure pricing is quite dynamic and changes frequently.</span></span>

<span data-ttu-id="84cc3-108">kullanımı izlemek ve aylık faturanızı ve tek tek müşterilerin ücretini tahmin etmeye yardımcı olmak için, [azure için bir müşterinin kullanım kayıtlarını almaya](get-a-customer-s-utilization-record-for-azure.md)yönelik bir istekle Microsoft Azure fiyatlarını almak üzere bu Azure fiyatı kartı sorgusunu birleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84cc3-108">To track usage and help predict your monthly bill and the bills for individual customers, you can combine this Azure Rate Card query to get prices for Microsoft Azure with a request to [Get a customer's utilization records for Azure](get-a-customer-s-utilization-record-for-azure.md).</span></span>

<span data-ttu-id="84cc3-109">Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="84cc3-109">Prices differ by market and currency, and this API takes location into consideration.</span></span> <span data-ttu-id="84cc3-110">Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="84cc3-110">By default, the API uses your partner profile settings in Partner Center and your browser language, and those settings are customizable.</span></span> <span data-ttu-id="84cc3-111">Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir.</span><span class="sxs-lookup"><span data-stu-id="84cc3-111">The location awareness is especially relevant if you manage sales in multiple markets from a single, centralized office.</span></span> <span data-ttu-id="84cc3-112">Daha fazla bilgi için bkz. [URI parametreleri](#uri-parameters).</span><span class="sxs-lookup"><span data-stu-id="84cc3-112">For more information, see [URI parameters](#uri-parameters).</span></span>

## <a name="c"></a><span data-ttu-id="84cc3-113">C\#</span><span class="sxs-lookup"><span data-stu-id="84cc3-113">C\#</span></span>

<span data-ttu-id="84cc3-114">Azure fiyat kartını edinmek için, Azure fiyatlarını içeren [**Azursilinebilir tecard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) kaynağını döndürmek üzere [**ıazursilinebilir Tecard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="84cc3-114">To obtain the Azure Rate Card, call the [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) method to return an [**AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) resource that contains the Azure prices.</span></span>

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

<span data-ttu-id="84cc3-115">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="84cc3-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="84cc3-116">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: GetAzureRateCard. cs</span><span class="sxs-lookup"><span data-stu-id="84cc3-116">**Project**: Partner Center SDK Samples **Class**: GetAzureRateCard.cs</span></span>

## <a name="java"></a><span data-ttu-id="84cc3-117">Java</span><span class="sxs-lookup"><span data-stu-id="84cc3-117">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="84cc3-118">Azure fiyat kartını edinmek için **ıazursilinebilir Tecard. Get** Işlevini çağırıp Azure fiyatlarını içeren ücret kartı ayrıntılarını döndürün.</span><span class="sxs-lookup"><span data-stu-id="84cc3-118">To obtain the Azure Rate Card, call the **IAzureRateCard.get** function to return rate card details that contains the Azure prices.</span></span>

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a><span data-ttu-id="84cc3-119">PowerShell</span><span class="sxs-lookup"><span data-stu-id="84cc3-119">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="84cc3-120">Azure kartını almak için [**Get-Partnerazursilinebilir Tecard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) komutunu çalıştırarak Azure fiyatlarını içeren ücret kartı ayrıntılarını döndürün.</span><span class="sxs-lookup"><span data-stu-id="84cc3-120">To obtain the Azure Card, execute the [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) command to return rate card details that contains the Azure prices.</span></span>

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a><span data-ttu-id="84cc3-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="84cc3-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="84cc3-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="84cc3-122">Request syntax</span></span>

| <span data-ttu-id="84cc3-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="84cc3-123">Method</span></span>  | <span data-ttu-id="84cc3-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="84cc3-124">Request URI</span></span>                                                        |
|---------|--------------------------------------------------------------------|
| <span data-ttu-id="84cc3-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="84cc3-125">**GET**</span></span> | <span data-ttu-id="84cc3-126">*{BaseUrl}*/v1/ratecards/Azure? para birimi = {currency} &bölgesi = {Region}</span><span class="sxs-lookup"><span data-stu-id="84cc3-126">*{baseURL}*/v1/ratecards/azure?currency={currency}&region={region}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="84cc3-127">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="84cc3-127">URI parameters</span></span>

| <span data-ttu-id="84cc3-128">Ad</span><span class="sxs-lookup"><span data-stu-id="84cc3-128">Name</span></span>     | <span data-ttu-id="84cc3-129">Tür</span><span class="sxs-lookup"><span data-stu-id="84cc3-129">Type</span></span>   | <span data-ttu-id="84cc3-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="84cc3-130">Required</span></span> | <span data-ttu-id="84cc3-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84cc3-131">Description</span></span>                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="84cc3-132">currency</span><span class="sxs-lookup"><span data-stu-id="84cc3-132">currency</span></span> | <span data-ttu-id="84cc3-133">dize</span><span class="sxs-lookup"><span data-stu-id="84cc3-133">string</span></span> | <span data-ttu-id="84cc3-134">No</span><span class="sxs-lookup"><span data-stu-id="84cc3-134">No</span></span>       | <span data-ttu-id="84cc3-135">Kaynak tarifelerinin sağlandığı para birimi için isteğe bağlı üç harfli ISO kodu (örneğin `EUR` ).</span><span class="sxs-lookup"><span data-stu-id="84cc3-135">Optional three letter ISO code for the currency in which the resource rates will be provided (for example `EUR`).</span></span> <span data-ttu-id="84cc3-136">Varsayılan değer: `USD`.</span><span class="sxs-lookup"><span data-stu-id="84cc3-136">The default is `USD`.</span></span> |
| <span data-ttu-id="84cc3-137">region</span><span class="sxs-lookup"><span data-stu-id="84cc3-137">region</span></span>   | <span data-ttu-id="84cc3-138">dize</span><span class="sxs-lookup"><span data-stu-id="84cc3-138">string</span></span> | <span data-ttu-id="84cc3-139">No</span><span class="sxs-lookup"><span data-stu-id="84cc3-139">No</span></span>       | <span data-ttu-id="84cc3-140">Teklifin satın alındığı pazarı belirten, isteğe bağlı iki harfli ISO ülke/bölge kodu (örneğin `FR` ).</span><span class="sxs-lookup"><span data-stu-id="84cc3-140">Optional two-letter ISO country/region code that indicates the market where the offer is purchased (for example `FR`).</span></span> <span data-ttu-id="84cc3-141">Varsayılan değer: `US`.</span><span class="sxs-lookup"><span data-stu-id="84cc3-141">The default is `US`.</span></span>        |

<span data-ttu-id="84cc3-142">İsteğe bağlı X-locale [üst bilgisini](headers.md#rest-request-headers) isteğinize dahil edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="84cc3-142">You can include the optional X-Locale [header](headers.md#rest-request-headers) in your request.</span></span> <span data-ttu-id="84cc3-143">X-locale üst bilgisini eklemezseniz, varsayılan değer ("en-US") kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84cc3-143">If you don't include the X-Locale header, the default value ("en-US") is used.</span></span>

- <span data-ttu-id="84cc3-144">İsteğiniz için para birimi ve bölge parametreleri sağlarsanız, yanıtın dilini belirlemekte X-locale değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84cc3-144">If you provide currency and region parameters in your request, the value of X-Locale is used to determine the response's language.</span></span>

- <span data-ttu-id="84cc3-145">İsteğiniz içinde bölge ve para birimi parametreleri sağlamazsanız, yanıtın bölge, para birimi ve dilini belirlemekte X-locale değeri kullanılır.</span><span class="sxs-lookup"><span data-stu-id="84cc3-145">If you don't provide region and currency parameters in your request, the value of X-Locale is used to determine the response's region, currency, and language.</span></span>

### <a name="request-header"></a><span data-ttu-id="84cc3-146">İstek üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="84cc3-146">Request header</span></span>

<span data-ttu-id="84cc3-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="84cc3-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="84cc3-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="84cc3-148">Request body</span></span>

<span data-ttu-id="84cc3-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="84cc3-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="84cc3-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="84cc3-150">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="84cc3-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="84cc3-151">REST response</span></span>

<span data-ttu-id="84cc3-152">İstek başarılı olursa, bir [Azure ücret kartı](azure-rate-card-resources.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="84cc3-152">If the request is successful, it returns an [Azure Rate Card](azure-rate-card-resources.md) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="84cc3-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="84cc3-153">Response success and error codes</span></span>

<span data-ttu-id="84cc3-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="84cc3-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="84cc3-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="84cc3-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="84cc3-156">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="84cc3-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="84cc3-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="84cc3-157">Response example</span></span>

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
