---
title: Ürünlerin bir listesini alma (müşteriye göre)
description: Müşterinin bir ürün koleksiyonunu almak için bir müşteri tanımlayıcısı kullanabilirsiniz.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: a7cb2430aa93beb89e4d1f9b8c89a016d66624ca
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874202"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="4f7a0-103">Ürünlerin bir listesini alma (müşteriye göre)</span><span class="sxs-lookup"><span data-stu-id="4f7a0-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="4f7a0-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4f7a0-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4f7a0-105">Mevcut bir müşteriye yönelik ürünlerin bir koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-105">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4f7a0-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4f7a0-106">Prerequisites</span></span>

- <span data-ttu-id="4f7a0-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4f7a0-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4f7a0-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4f7a0-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4f7a0-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4f7a0-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4f7a0-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4f7a0-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4f7a0-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="4f7a0-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="4f7a0-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4f7a0-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4f7a0-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4f7a0-116">Request syntax</span></span>

| <span data-ttu-id="4f7a0-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4f7a0-117">Method</span></span> | <span data-ttu-id="4f7a0-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4f7a0-118">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4f7a0-119">POST</span><span class="sxs-lookup"><span data-stu-id="4f7a0-119">POST</span></span>   | <span data-ttu-id="4f7a0-120">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products? targetView = {targetview} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4f7a0-120">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="4f7a0-121">İstek URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="4f7a0-121">Request URI parameters</span></span>

| <span data-ttu-id="4f7a0-122">Ad</span><span class="sxs-lookup"><span data-stu-id="4f7a0-122">Name</span></span>               | <span data-ttu-id="4f7a0-123">Tür</span><span class="sxs-lookup"><span data-stu-id="4f7a0-123">Type</span></span> | <span data-ttu-id="4f7a0-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4f7a0-124">Required</span></span> | <span data-ttu-id="4f7a0-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4f7a0-125">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="4f7a0-126">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-126">**customer-tenant-id**</span></span> | <span data-ttu-id="4f7a0-127">GUID</span><span class="sxs-lookup"><span data-stu-id="4f7a0-127">GUID</span></span> | <span data-ttu-id="4f7a0-128">Yes</span><span class="sxs-lookup"><span data-stu-id="4f7a0-128">Yes</span></span> | <span data-ttu-id="4f7a0-129">Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-129">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="4f7a0-130">**targetView**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-130">**targetView**</span></span> | <span data-ttu-id="4f7a0-131">string</span><span class="sxs-lookup"><span data-stu-id="4f7a0-131">string</span></span> | <span data-ttu-id="4f7a0-132">Yes</span><span class="sxs-lookup"><span data-stu-id="4f7a0-132">Yes</span></span> | <span data-ttu-id="4f7a0-133">Kataloğun hedef görünümünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-133">Identifies the target view of the catalog.</span></span> <span data-ttu-id="4f7a0-134">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="4f7a0-134">The supported values are:</span></span> <br/><br/><span data-ttu-id="4f7a0-135">Tüm Azure öğelerini içeren **Azure**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-135">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="4f7a0-136">Tüm Azure ayırma öğelerini içeren **Azurereservations**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-136">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="4f7a0-137">Tüm sanal makine (VM) rezervasyon öğelerini içeren **Azurereservationsvm**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-137">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="4f7a0-138">tüm SQL ayırma öğelerini içeren **azurereservationssql**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-138">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="4f7a0-139">tüm Cosmos veritabanı ayırma öğelerini içeren **azurereservationscosmosdb**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-139">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="4f7a0-140">Microsoft Azure aboneliklerine (**MS-azr-0145p**) ve Azure planlarına yönelik öğeler içeren **MicrosoftAzure**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-140">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="4f7a0-141">Ticari Market ürünleri dahil tüm çevrimiçi hizmet öğelerini içeren **OnlineServices**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-141">**OnlineServices**, which includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="4f7a0-142">Tüm yazılım öğelerini içeren **yazılım**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-142">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="4f7a0-143">Tüm yazılım SUSE Linux öğelerini içeren **SoftwareSUSELinux**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-143">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="4f7a0-144">Tüm kalıcı yazılım öğelerini içeren **Softwarekalıcı**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-144">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="4f7a0-145">Tüm yazılım aboneliği öğelerini içeren **SoftwareSubscriptions**</span><span class="sxs-lookup"><span data-stu-id="4f7a0-145">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="4f7a0-146">İstek üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="4f7a0-146">Request header</span></span>

<span data-ttu-id="4f7a0-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4f7a0-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4f7a0-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4f7a0-148">Request body</span></span>

<span data-ttu-id="4f7a0-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4f7a0-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4f7a0-150">Request example</span></span>

<span data-ttu-id="4f7a0-151">Belirli bir müşteri tarafından kullanılabilen Azure kullanım tabanlı ürünlerin bir listesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-151">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="4f7a0-152">yalnızca Microsoft Azure (MS-azr-0145p) ve Azure planlarına yönelik ürünler, genel buluttaki müşteriler için döndürülür:</span><span class="sxs-lookup"><span data-stu-id="4f7a0-152">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="4f7a0-153">Rest yanıtı</span><span class="sxs-lookup"><span data-stu-id="4f7a0-153">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4f7a0-154">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4f7a0-154">Response success and error codes</span></span>

<span data-ttu-id="4f7a0-155">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4f7a0-156">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4f7a0-157">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4f7a0-157">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="4f7a0-158">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="4f7a0-158">This method returns the following error codes:</span></span>

| <span data-ttu-id="4f7a0-159">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="4f7a0-159">HTTP Status Code</span></span> | <span data-ttu-id="4f7a0-160">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="4f7a0-160">Error code</span></span>   | <span data-ttu-id="4f7a0-161">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4f7a0-161">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="4f7a0-162">403</span><span class="sxs-lookup"><span data-stu-id="4f7a0-162">403</span></span> | <span data-ttu-id="4f7a0-163">400036</span><span class="sxs-lookup"><span data-stu-id="4f7a0-163">400036</span></span> | <span data-ttu-id="4f7a0-164">İstenen targetView 'a erişime izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="4f7a0-164">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="4f7a0-165">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4f7a0-165">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
