---
title: Ürünlerin bir listesini alma (müşteriye göre)
description: Müşterinin bir ürün koleksiyonunu almak için bir müşteri tanımlayıcısı kullanabilirsiniz.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 98a099c458535123f675c6452db950b087b9f387
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769449"
---
# <a name="get-a-list-of-products-by-customer"></a><span data-ttu-id="22bdc-103">Ürünlerin bir listesini alma (müşteriye göre)</span><span class="sxs-lookup"><span data-stu-id="22bdc-103">Get a list of products (by customer)</span></span>

<span data-ttu-id="22bdc-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="22bdc-104">**Applies to:**</span></span>

- <span data-ttu-id="22bdc-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="22bdc-105">Partner Center</span></span>
- <span data-ttu-id="22bdc-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="22bdc-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="22bdc-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="22bdc-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="22bdc-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="22bdc-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="22bdc-109">Mevcut bir müşteriye yönelik ürünlerin bir koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22bdc-109">You can use the following methods to get a collection of products for an existing customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22bdc-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="22bdc-110">Prerequisites</span></span>

- <span data-ttu-id="22bdc-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="22bdc-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="22bdc-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="22bdc-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="22bdc-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="22bdc-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="22bdc-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="22bdc-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="22bdc-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="22bdc-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="22bdc-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="22bdc-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="22bdc-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="22bdc-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="22bdc-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="22bdc-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="22bdc-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="22bdc-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="22bdc-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="22bdc-120">Request syntax</span></span>

| <span data-ttu-id="22bdc-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="22bdc-121">Method</span></span> | <span data-ttu-id="22bdc-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="22bdc-122">Request URI</span></span>                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="22bdc-123">POST</span><span class="sxs-lookup"><span data-stu-id="22bdc-123">POST</span></span>   | <span data-ttu-id="22bdc-124">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products? targetView = {targetview} http/1.1</span><span class="sxs-lookup"><span data-stu-id="22bdc-124">[*\{baseURL\}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/products?targetView={targetView} HTTP/1.1</span></span> |

#### <a name="request-uri-parameters"></a><span data-ttu-id="22bdc-125">İstek URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="22bdc-125">Request URI parameters</span></span>

| <span data-ttu-id="22bdc-126">Ad</span><span class="sxs-lookup"><span data-stu-id="22bdc-126">Name</span></span>               | <span data-ttu-id="22bdc-127">Tür</span><span class="sxs-lookup"><span data-stu-id="22bdc-127">Type</span></span> | <span data-ttu-id="22bdc-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="22bdc-128">Required</span></span> | <span data-ttu-id="22bdc-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="22bdc-129">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="22bdc-130">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="22bdc-130">**customer-tenant-id**</span></span> | <span data-ttu-id="22bdc-131">GUID</span><span class="sxs-lookup"><span data-stu-id="22bdc-131">GUID</span></span> | <span data-ttu-id="22bdc-132">Yes</span><span class="sxs-lookup"><span data-stu-id="22bdc-132">Yes</span></span> | <span data-ttu-id="22bdc-133">Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**.</span><span class="sxs-lookup"><span data-stu-id="22bdc-133">The value is a GUID-formatted **customer-tenant-id**, which is an identifier that allows you to specify a customer.</span></span> |
| <span data-ttu-id="22bdc-134">**targetView**</span><span class="sxs-lookup"><span data-stu-id="22bdc-134">**targetView**</span></span> | <span data-ttu-id="22bdc-135">string</span><span class="sxs-lookup"><span data-stu-id="22bdc-135">string</span></span> | <span data-ttu-id="22bdc-136">Yes</span><span class="sxs-lookup"><span data-stu-id="22bdc-136">Yes</span></span> | <span data-ttu-id="22bdc-137">Kataloğun hedef görünümünü tanımlar.</span><span class="sxs-lookup"><span data-stu-id="22bdc-137">Identifies the target view of the catalog.</span></span> <span data-ttu-id="22bdc-138">Desteklenen değerler şunlardır:</span><span class="sxs-lookup"><span data-stu-id="22bdc-138">The supported values are:</span></span> <br/><br/><span data-ttu-id="22bdc-139">Tüm Azure öğelerini içeren **Azure**</span><span class="sxs-lookup"><span data-stu-id="22bdc-139">**Azure**, which includes all Azure items</span></span><br/><br/><span data-ttu-id="22bdc-140">Tüm Azure ayırma öğelerini içeren **Azurereservations**</span><span class="sxs-lookup"><span data-stu-id="22bdc-140">**AzureReservations**, which includes all Azure reservation items</span></span><br/><br/><span data-ttu-id="22bdc-141">Tüm sanal makine (VM) rezervasyon öğelerini içeren **Azurereservationsvm**</span><span class="sxs-lookup"><span data-stu-id="22bdc-141">**AzureReservationsVM**, which includes all virtual machine (VM) reservation items</span></span><br/><br/><span data-ttu-id="22bdc-142">Tüm SQL rezervasyon öğelerini içeren **Azurereservationssql**</span><span class="sxs-lookup"><span data-stu-id="22bdc-142">**AzureReservationsSQL**, which includes all SQL reservation items</span></span><br/><br/><span data-ttu-id="22bdc-143">Tüm Cosmos veritabanı ayırma öğelerini içeren **Azurereservationscosmosdb**</span><span class="sxs-lookup"><span data-stu-id="22bdc-143">**AzureReservationsCosmosDb**, which includes all Cosmos database reservation items</span></span><br/><br/><span data-ttu-id="22bdc-144">Microsoft Azure aboneliklerine (**MS-AZR-0145P**) ve Azure planlarına yönelik öğeler içeren **MicrosoftAzure**</span><span class="sxs-lookup"><span data-stu-id="22bdc-144">**MicrosoftAzure**, which includes items for Microsoft Azure subscriptions (**MS-AZR-0145P**) and Azure plans</span></span><br/><br/><span data-ttu-id="22bdc-145">Ticari Market ürünleri dahil tüm çevrimiçi hizmet öğelerini içeren **OnlineServices**</span><span class="sxs-lookup"><span data-stu-id="22bdc-145">**OnlineServices**, which  includes all online service items, including commercial marketplace products</span></span><br/><br/><span data-ttu-id="22bdc-146">Tüm yazılım öğelerini içeren **yazılım**</span><span class="sxs-lookup"><span data-stu-id="22bdc-146">**Software**, which  includes all software items</span></span><br/><br/><span data-ttu-id="22bdc-147">Tüm yazılım SUSE Linux öğelerini içeren **SoftwareSUSELinux**</span><span class="sxs-lookup"><span data-stu-id="22bdc-147">**SoftwareSUSELinux**, which includes all software SUSE Linux items</span></span><br/><br/><span data-ttu-id="22bdc-148">Tüm kalıcı yazılım öğelerini içeren **Softwarekalıcı**</span><span class="sxs-lookup"><span data-stu-id="22bdc-148">**SoftwarePerpetual**, which includes all perpetual software items</span></span><br/><br/><span data-ttu-id="22bdc-149">Tüm yazılım aboneliği öğelerini içeren **SoftwareSubscriptions**</span><span class="sxs-lookup"><span data-stu-id="22bdc-149">**SoftwareSubscriptions**, which includes all software subscription items</span></span>  |

### <a name="request-header"></a><span data-ttu-id="22bdc-150">İstek üst bilgisi</span><span class="sxs-lookup"><span data-stu-id="22bdc-150">Request header</span></span>

<span data-ttu-id="22bdc-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="22bdc-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="22bdc-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="22bdc-152">Request body</span></span>

<span data-ttu-id="22bdc-153">Yok.</span><span class="sxs-lookup"><span data-stu-id="22bdc-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="22bdc-154">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="22bdc-154">Request example</span></span>

<span data-ttu-id="22bdc-155">Belirli bir müşteri tarafından kullanılabilen Azure kullanım tabanlı ürünlerin bir listesini isteyin.</span><span class="sxs-lookup"><span data-stu-id="22bdc-155">Request for a list of Azure usage-based products available to a given customer.</span></span> <span data-ttu-id="22bdc-156">Yalnızca Microsoft Azure (MS-AZR-0145P) ve Azure planlarına yönelik ürünler, genel buluttaki müşteriler için döndürülür:</span><span class="sxs-lookup"><span data-stu-id="22bdc-156">Products for both Microsoft Azure (MS-AZR-0145P) and Azure plans will be returned for customers in public cloud:</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a><span data-ttu-id="22bdc-157">Rest yanıtı</span><span class="sxs-lookup"><span data-stu-id="22bdc-157">Rest response</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="22bdc-158">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="22bdc-158">Response success and error codes</span></span>

<span data-ttu-id="22bdc-159">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="22bdc-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="22bdc-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="22bdc-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="22bdc-161">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="22bdc-161">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

<span data-ttu-id="22bdc-162">Bu yöntem aşağıdaki hata kodlarını döndürür:</span><span class="sxs-lookup"><span data-stu-id="22bdc-162">This method returns the following error codes:</span></span>

| <span data-ttu-id="22bdc-163">HTTP durum kodu</span><span class="sxs-lookup"><span data-stu-id="22bdc-163">HTTP Status Code</span></span> | <span data-ttu-id="22bdc-164">Hata kodu</span><span class="sxs-lookup"><span data-stu-id="22bdc-164">Error code</span></span>   | <span data-ttu-id="22bdc-165">Description</span><span class="sxs-lookup"><span data-stu-id="22bdc-165">Description</span></span>                     |
|------------------|--------------|---------------------------------|
| <span data-ttu-id="22bdc-166">403</span><span class="sxs-lookup"><span data-stu-id="22bdc-166">403</span></span> | <span data-ttu-id="22bdc-167">400036</span><span class="sxs-lookup"><span data-stu-id="22bdc-167">400036</span></span> | <span data-ttu-id="22bdc-168">İstenen targetView 'a erişime izin verilmiyor.</span><span class="sxs-lookup"><span data-stu-id="22bdc-168">Access to the requested targetView is not allowed.</span></span> |

### <a name="response-example"></a><span data-ttu-id="22bdc-169">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="22bdc-169">Response example</span></span>

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
