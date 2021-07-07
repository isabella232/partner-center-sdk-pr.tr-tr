---
title: Bir aboneliği geçirme
description: Müşterinin aboneliğini belirtilen hedef aboneliğe yükselter.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01455315825cad026830268b6bbd55509e964bb5
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530251"
---
# <a name="transition-a-subscription"></a><span data-ttu-id="fcc10-103">Bir aboneliği geçirme</span><span class="sxs-lookup"><span data-stu-id="fcc10-103">Transition a subscription</span></span>

<span data-ttu-id="fcc10-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fcc10-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fcc10-105">Müşterinin aboneliğini belirtilen hedef aboneliğe yükselter.</span><span class="sxs-lookup"><span data-stu-id="fcc10-105">Upgrades a customer's subscription to a specified target subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fcc10-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fcc10-106">Prerequisites</span></span>

- <span data-ttu-id="fcc10-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fcc10-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fcc10-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="fcc10-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fcc10-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fcc10-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fcc10-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fcc10-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fcc10-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="fcc10-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fcc10-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="fcc10-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fcc10-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="fcc10-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fcc10-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fcc10-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fcc10-115">Biri ilk abonelik için, biri de hedef abonelik için olmak için iki abonelik kimlikleri.</span><span class="sxs-lookup"><span data-stu-id="fcc10-115">Two subscription IDs, one for the initial subscription and one for the target subscription.</span></span>

## <a name="c"></a><span data-ttu-id="fcc10-116">C\#</span><span class="sxs-lookup"><span data-stu-id="fcc10-116">C\#</span></span>

<span data-ttu-id="fcc10-117">Müşterinin aboneliğini yükseltmek için önce [bu müşterinin aboneliğini alın.](get-a-subscription-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="fcc10-117">To upgrade a customer's subscription, first [get that's customer's subscription](get-a-subscription-by-id.md).</span></span> <span data-ttu-id="fcc10-118">Ardından, Upgrades özelliğini ve ardından **Get()** veya **GetAsync()** yöntemlerini çağırarak bu abonelik için yükseltmelerin bir listesini alın. </span><span class="sxs-lookup"><span data-stu-id="fcc10-118">Then, obtain a list of upgrades for that subscription by calling the **Upgrades** property followed by the **Get()** or **GetAsync()** methods.</span></span> <span data-ttu-id="fcc10-119">Bu yükseltme listesinden bir hedef yükseltme seçin ve ardından ilk aboneliğin **Upgrades** özelliğini ve ardından **Create() yöntemini** çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fcc10-119">Choose a target upgrade from that list of upgrades, and then call the **Upgrades** property of the initial subscription, followed by the **Create()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

<span data-ttu-id="fcc10-120">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fcc10-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fcc10-121">**Project:** PartnerSDK.FeatureSamples **Sınıfı:** UpgradeSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="fcc10-121">**Project**: PartnerSDK.FeatureSamples **Class**: UpgradeSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="fcc10-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="fcc10-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fcc10-123">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="fcc10-123">Request syntax</span></span>

| <span data-ttu-id="fcc10-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="fcc10-124">Method</span></span>   | <span data-ttu-id="fcc10-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="fcc10-125">Request URI</span></span>                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fcc10-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="fcc10-126">**GET**</span></span>  | <span data-ttu-id="fcc10-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fcc10-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span></span> |
| <span data-ttu-id="fcc10-128">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="fcc10-128">**POST**</span></span> | <span data-ttu-id="fcc10-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fcc10-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span></span>       |

### <a name="uri-parameter"></a><span data-ttu-id="fcc10-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="fcc10-130">URI parameter</span></span>

<span data-ttu-id="fcc10-131">Aboneliği geçiş yapmak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="fcc10-131">Use the following query parameter to transition the subscription.</span></span>

| <span data-ttu-id="fcc10-132">Ad</span><span class="sxs-lookup"><span data-stu-id="fcc10-132">Name</span></span>                    | <span data-ttu-id="fcc10-133">Tür</span><span class="sxs-lookup"><span data-stu-id="fcc10-133">Type</span></span>     | <span data-ttu-id="fcc10-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fcc10-134">Required</span></span> | <span data-ttu-id="fcc10-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fcc10-135">Description</span></span>                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| <span data-ttu-id="fcc10-136">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="fcc10-136">**customer-tenant-id**</span></span>  | <span data-ttu-id="fcc10-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="fcc10-137">**guid**</span></span> | <span data-ttu-id="fcc10-138">Y</span><span class="sxs-lookup"><span data-stu-id="fcc10-138">Y</span></span>        | <span data-ttu-id="fcc10-139">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="fcc10-139">A GUID corresponding to the customer.</span></span>             |
| <span data-ttu-id="fcc10-140">**abonelik için id**</span><span class="sxs-lookup"><span data-stu-id="fcc10-140">**id-for-subscription**</span></span> | <span data-ttu-id="fcc10-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="fcc10-141">**guid**</span></span> | <span data-ttu-id="fcc10-142">Y</span><span class="sxs-lookup"><span data-stu-id="fcc10-142">Y</span></span>        | <span data-ttu-id="fcc10-143">İlk aboneliğe karşılık gelen GUID.</span><span class="sxs-lookup"><span data-stu-id="fcc10-143">A GUID corresponding to the initial subscription.</span></span> |
| <span data-ttu-id="fcc10-144">**id-for-target**</span><span class="sxs-lookup"><span data-stu-id="fcc10-144">**id-for-target**</span></span>       | <span data-ttu-id="fcc10-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="fcc10-145">**guid**</span></span> | <span data-ttu-id="fcc10-146">Y</span><span class="sxs-lookup"><span data-stu-id="fcc10-146">Y</span></span>        | <span data-ttu-id="fcc10-147">Hedef aboneliğe karşılık gelen GUID.</span><span class="sxs-lookup"><span data-stu-id="fcc10-147">A GUID corresponding to the target subscription.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="fcc10-148">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="fcc10-148">Request headers</span></span>

<span data-ttu-id="fcc10-149">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fcc10-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fcc10-150">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="fcc10-150">Request body</span></span>

<span data-ttu-id="fcc10-151">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="fcc10-151">None</span></span>

### <a name="request-example"></a><span data-ttu-id="fcc10-152">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="fcc10-152">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

POST https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
Content-Type: application/json
Content-Length: 1098
Expect: 100-continue

{
    "TargetOffer":{
        "Id":"796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Name":"Office 365 Enterprise E3",
        "Description":"The best plan for businesses that need full productivity, communication and collaboration tools with the familiar Office suite, including Office Online.",
        "MinimumQuantity":1,
        "MaximumQuantity":10000000,
        "Rank":61,
        "Uri":"/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/796B6B5F-613C-4E24-A17C-EBA730D49C02",
        "Locale":"en-us",
        "Country":"US",
        "Category":{
            "Id":"Enterprise_Key",
            "Name":"Enterprise",
            "Rank":20,
            "Locale":"en-us",
            "Country":"US",
            "Attributes":{
                "ObjectType":"OfferCategory"
            }
        },
        "PrerequisiteOffers":[],
        "IsAddOn":false,
        "IsAvailableForPurchase":true,
        "Billing":"license",
        "IsAutoRenewable":true,
        "Product":{
            "Id":"6fd2c87f-b296-42f0-b197-1e91e994b900",
            "Name":"Office 365 Enterprise E3",
            "Unit":"Licenses"
        },
        "UnitType":"Licenses",
        "Links":{
            "LearnMore":{
                "Uri":"http://g.microsoftonline.com/0BXPS00en/1015",
                "Method":"GET",
                "Headers":[]
            }
        }
        "Attributes":{
            "ObjectType":"Offer"
        }
    },
    "UpgradeType":1,
    "IsEligible":true,
    "Quantity":1,
    "UpgradeErrors":[],
    "Attributes":{
        "ObjectType":"Upgrade"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="fcc10-153">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="fcc10-153">REST response</span></span>

<span data-ttu-id="fcc10-154">Başarılı olursa, bu yöntem yanıt **gövdesinde** bir Yükseltme sonucu kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="fcc10-154">If successful, this method returns an **Upgrade** result resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fcc10-155">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="fcc10-155">Response success and error codes</span></span>

<span data-ttu-id="fcc10-156">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="fcc10-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fcc10-157">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fcc10-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fcc10-158">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fcc10-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fcc10-159">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="fcc10-159">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 29 Jan 2016 20:42:26 GMT

{
    "totalCount": 1,
    "items": [{
        "targetOffer": {
            "id": "91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "name": "Office 365 Enterprise E1",
            "description": "For businesses that need communication and collaboration tools and the ability to read and do lightweight editing of documents with Office Online.",
            "minimumQuantity": 1,
            "maximumQuantity": 10000000,
            "rank": 48,
            "uri": "/3c95518e-8c37-41e3-9627-0ca339200f53/Offers/91FD106F-4B2C-4938-95AC-F54F74E9A239",
            "locale": "en-us",
            "country": "US",
            "category": {
                "id": "Enterprise_Key",
                "name": "Enterprise",
                "rank": 20,
                "locale": "en-us",
                "country": "US",
                "attributes": {
                    "objectType": "OfferCategory"
                }
            },
            "prerequisiteOffers": [],
            "isAddOn": false,
            "isAvailableForPurchase": true,
            "billing": "license",
            "isAutoRenewable": true,
            "isInternal": false,
            "conversionTargetOffers": [],
            "partnerQualifications": ["none"],
            "product": {
                "id": "18181a46-0d4e-45cd-891e-60aabd171b4e",
                "name": "Office 365 Enterprise E1",
                "unit": "Licenses"
            },
            "unitType": "Licenses",
            "links": {
                "learnMore": {
                    "uri": "http://g.microsoftonline.com/0BXPS00en/1013",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/offers/91FD106F-4B2C-4938-95AC-F54F74E9A239?country=US",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Offer"
            }
        },
        "upgradeType": "upgrade_only",
        "isEligible": false,
        "quantity": 1,
        "upgradeErrors": [{
            "code": 2,
            "description": "Subscription cannot be upgraded because the source subscription state is not active.  Additional Details contains the current source subscription state.",
            "attributes": {
                "objectType": "UpgradeError"
            }
        }],
        "attributes": {
            "objectType": "Upgrade"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}

HTTP/1.1 200 OK
Content-Length: 448
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 750fd5ea-904b-4c3e-b476-60d0feacab0d
MS-CV: RnK86LBbDkWP/w2R.0
MS-ServerId: 102031201
Date: Fri, 29 Jan 2016 20:44:21 GMT

{
    "sourceSubscriptionId":"896a2862-67e2-4f3d-bb3f-c50c42b5fad8",
    "targetSubscriptionId":"2add8a55-454a-4ae5-a4c9-5107dc6e9768",
    "upgradeType":1,
    "upgradeErrors":[],
    "licenseErrors":[],
    "attributes":{
        "objectType":"UpgradeResult"
    }
}
```
