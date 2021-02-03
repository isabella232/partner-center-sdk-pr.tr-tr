---
title: Envanteri denetle
description: Belirli bir katalog öğeleri kümesinin envanterini denetlemek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Bunu bir müşterinin ürünlerini veya SKU 'Larını belirlemek için yapabilirsiniz.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6921760abc0b95aff820467e84b3e8e9435731cd
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770085"
---
# <a name="check-the-inventory-of-catalog-items-using-partner-center-apis"></a><span data-ttu-id="d839c-104">Iş Ortağı Merkezi API 'Lerini kullanarak Katalog öğelerinin envanterini denetleme</span><span class="sxs-lookup"><span data-stu-id="d839c-104">Check the inventory of catalog items using Partner Center APIs</span></span>

<span data-ttu-id="d839c-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="d839c-105">**Applies to:**</span></span>

- <span data-ttu-id="d839c-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d839c-106">Partner Center</span></span>

<span data-ttu-id="d839c-107">Belirli bir katalog öğeleri kümesinin envanterini denetleme.</span><span class="sxs-lookup"><span data-stu-id="d839c-107">How to check the inventory for a specific set of catalog items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d839c-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d839c-108">Prerequisites</span></span>

- <span data-ttu-id="d839c-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d839c-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d839c-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="d839c-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d839c-111">Bir veya daha fazla ürün kimliği.</span><span class="sxs-lookup"><span data-stu-id="d839c-111">One or more product IDs.</span></span> <span data-ttu-id="d839c-112">İsteğe bağlı olarak, SKU kimlikleri de belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d839c-112">Optionally, SKU IDs can also be specified.</span></span>

- <span data-ttu-id="d839c-113">Belirtilen Ürün/SKU KIMLIKLERI tarafından başvurulan SKU 'ları envanterin doğrulanması için gereken ek bağlam.</span><span class="sxs-lookup"><span data-stu-id="d839c-113">Any additional context needed for verifying the inventory of the SKU(s) referenced by the provided product/SKU ID(s).</span></span> <span data-ttu-id="d839c-114">Bu gereksinimler Ürün/SKU türüne göre farklılık gösterebilir ve [SKU](product-resources.md#sku) 'nun **ınventoryvariables** özelliğinden belirlenebilir.</span><span class="sxs-lookup"><span data-stu-id="d839c-114">These requirements may vary by type of product/SKU and can be determined from the [SKU's](product-resources.md#sku) **InventoryVariables** property.</span></span>

## <a name="c"></a><span data-ttu-id="d839c-115">C\#</span><span class="sxs-lookup"><span data-stu-id="d839c-115">C\#</span></span>

<span data-ttu-id="d839c-116">Sayımı denetlemek için, denetlenecek her öğe için bir [ınventoryıtem](product-resources.md#inventoryitem) nesnesi kullanarak bir [ınventorycheckrequest](product-resources.md#inventorycheckrequest) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d839c-116">To check the inventory, build an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) object using an [InventoryItem](product-resources.md#inventoryitem) object for each item to be checked.</span></span> <span data-ttu-id="d839c-117">Ardından bir **ıaggregatepartner. Extensions** erişimcisi kullanın, bunu **ürüne** göre belirleyin ve ardından **bycountry ()** yöntemini kullanarak ülkeyi seçin.</span><span class="sxs-lookup"><span data-stu-id="d839c-117">Then, use an **IAggregatePartner.Extensions** accessor, scope it down to **Product** and then select the country using the **ByCountry()** method.</span></span> <span data-ttu-id="d839c-118">Son olarak, **ınventorycheckrequest** nesneniz Ile **checkınventory ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d839c-118">Finally, call the **CheckInventory()** method with your **InventoryCheckRequest** object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string subscriptionId;
string countryCode;
string productId;

// Build the inventory check request details object.
var inventoryCheckRequest = new InventoryCheckRequest()
{
    TargetItems = new InventoryItem[]{ new InventoryItem { ProductId = productId } },
    InventoryContext = new Dictionary<string, string>()
    {
      { "customerId", customerId },
      { "azureSubscriptionId", subscriptionId }
      { "armRegionName", armRegionName }
    }
};

// Get the inventory results.
var inventoryResults = partnerOperations.Extensions.Product.ByCountry(countryCode).CheckInventory(inventoryCheckRequest);
```

## <a name="rest-request"></a><span data-ttu-id="d839c-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d839c-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d839c-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d839c-120">Request syntax</span></span>

| <span data-ttu-id="d839c-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d839c-121">Method</span></span>   | <span data-ttu-id="d839c-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d839c-122">Request URI</span></span>                                                                                                                              |
|----------|------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d839c-123">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="d839c-123">**POST**</span></span> | <span data-ttu-id="d839c-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Extensions/Product/checkInventory? ülke = {Country-Code} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d839c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/extensions/product/checkInventory?country={country-code} HTTP/1.1</span></span>                        |

### <a name="uri-parameter"></a><span data-ttu-id="d839c-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d839c-125">URI parameter</span></span>

<span data-ttu-id="d839c-126">Stoku denetlemek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d839c-126">Use the following query parameter to check the inventory.</span></span>

| <span data-ttu-id="d839c-127">Ad</span><span class="sxs-lookup"><span data-stu-id="d839c-127">Name</span></span>                   | <span data-ttu-id="d839c-128">Tür</span><span class="sxs-lookup"><span data-stu-id="d839c-128">Type</span></span>     | <span data-ttu-id="d839c-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d839c-129">Required</span></span> | <span data-ttu-id="d839c-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d839c-130">Description</span></span>                                                     |
|------------------------|----------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="d839c-131">ülke kodu</span><span class="sxs-lookup"><span data-stu-id="d839c-131">country-code</span></span>           | <span data-ttu-id="d839c-132">string</span><span class="sxs-lookup"><span data-stu-id="d839c-132">string</span></span>   | <span data-ttu-id="d839c-133">Yes</span><span class="sxs-lookup"><span data-stu-id="d839c-133">Yes</span></span>      | <span data-ttu-id="d839c-134">Ülke/bölge KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d839c-134">A country/region ID.</span></span>                                            |

### <a name="request-headers"></a><span data-ttu-id="d839c-135">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d839c-135">Request headers</span></span>

<span data-ttu-id="d839c-136">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d839c-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d839c-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d839c-137">Request body</span></span>

<span data-ttu-id="d839c-138">Bir veya daha fazla [ınventoryıtem](product-resources.md#inventoryitem) kaynağı Içeren bir [ınventorycheckrequest](product-resources.md#inventorycheckrequest) kaynağı içeren envanter isteği ayrıntıları.</span><span class="sxs-lookup"><span data-stu-id="d839c-138">The inventory request details, consisting of an [InventoryCheckRequest](product-resources.md#inventorycheckrequest) resource containing one or more [InventoryItem](product-resources.md#inventoryitem) resources.</span></span>

### <a name="request-example"></a><span data-ttu-id="d839c-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d839c-139">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/extensions/product/checkinventory?country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json

{"TargetItems":[{"ProductId":"DZH318Z0BQ3P"}],"InventoryContext":{"customerId":"d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d","azureSubscriptionId":"3A231FBE-37FE-4410-93FD-730D3D5D4C75","armRegionName":"Europe"}}
```

## <a name="rest-response"></a><span data-ttu-id="d839c-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d839c-140">REST response</span></span>

<span data-ttu-id="d839c-141">Başarılı olursa, yanıt gövdesi, varsa kısıtlama ayrıntıları ile doldurulmuş bir [ınventoryıtem](product-resources.md#inventoryitem) nesneleri koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="d839c-141">If successful, the response body contains a collection of [InventoryItem](product-resources.md#inventoryitem) objects populated with the restriction details, if any apply.</span></span>

>[!NOTE]
><span data-ttu-id="d839c-142">Bir giriş ınventoryıtem, katalogda bulunamayan bir öğeyi temsil ediyorsa, çıkış koleksiyonuna dahil edilmez.</span><span class="sxs-lookup"><span data-stu-id="d839c-142">If an input InventoryItem represents an item that could not be found in the catalog, it will not be included in the output collection.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d839c-143">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d839c-143">Response success and error codes</span></span>

<span data-ttu-id="d839c-144">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="d839c-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d839c-145">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d839c-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d839c-146">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d839c-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d839c-147">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d839c-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1021
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4acb26a1-3536-4081-bc7d-092869a4961a
MS-RequestId: d1b1981a-e088-4610-870a-eebec96d6bcd
X-Locale: en-US
[
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0039",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0038",
        "isRestricted": true,
        "restrictions": [
            {
                "reasonCode": "NotAvailableForSubscription",
                "description": "Restriction identified of type 'Location' with values 'japanwest'.",
                "properties": {
                    "type": "Location",
                    "values": "japanwest"
                }
            }
        ]
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "000S",
        "isRestricted": false,
        "restrictions": []
    },
    {
        "productId": "DZH318Z0BQ3P",
        "skuId": "0011",
        "isRestricted": false,
        "restrictions": []
    }
]
```
