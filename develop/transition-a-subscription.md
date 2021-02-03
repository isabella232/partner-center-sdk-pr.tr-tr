---
title: Bir aboneliği geçirme
description: Bir müşterinin aboneliğini belirtilen bir hedef aboneliğe yükseltir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b757eee8bc65c16b5c65221a4c14b6c0fd6369e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768938"
---
# <a name="transition-a-subscription"></a><span data-ttu-id="96302-103">Bir aboneliği geçirme</span><span class="sxs-lookup"><span data-stu-id="96302-103">Transition a subscription</span></span>

<span data-ttu-id="96302-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="96302-104">**Applies To**</span></span>

- <span data-ttu-id="96302-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="96302-105">Partner Center</span></span>
- <span data-ttu-id="96302-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="96302-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="96302-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="96302-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="96302-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="96302-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="96302-109">Bir müşterinin aboneliğini belirtilen bir hedef aboneliğe yükseltir.</span><span class="sxs-lookup"><span data-stu-id="96302-109">Upgrades a customer's subscription to a specified target subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96302-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="96302-110">Prerequisites</span></span>

- <span data-ttu-id="96302-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="96302-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="96302-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="96302-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="96302-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="96302-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="96302-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96302-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="96302-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="96302-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="96302-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="96302-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="96302-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="96302-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="96302-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="96302-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="96302-119">Biri ilk abonelik diğeri de hedef abonelik için olmak üzere iki abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="96302-119">Two subscription IDs, one for the initial subscription and one for the target subscription.</span></span>

## <a name="c"></a><span data-ttu-id="96302-120">C\#</span><span class="sxs-lookup"><span data-stu-id="96302-120">C\#</span></span>

<span data-ttu-id="96302-121">Bir müşterinin aboneliğini yükseltmek için önce bu müşterinin [müşterimizin aboneliğini alın](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="96302-121">To upgrade a customer's subscription, first [get that's customer's subscription](get-a-subscription-by-id.md).</span></span> <span data-ttu-id="96302-122">Ardından, **yükseltmeler** özelliğini çağırarak **Get ()** veya **GetAsync ()** yöntemleri tarafından bu abonelik için yükseltmelerin bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="96302-122">Then, obtain a list of upgrades for that subscription by calling the **Upgrades** property followed by the **Get()** or **GetAsync()** methods.</span></span> <span data-ttu-id="96302-123">Bu yükseltmeler listesinden bir hedef yükseltme seçin ve ardından ilk aboneliğin **yükseltmeler** özelliğini çağırın ve ardından **Create ()** yöntemi gelir.</span><span class="sxs-lookup"><span data-stu-id="96302-123">Choose a target upgrade from that list of upgrades, and then call the **Upgrades** property of the initial subscription, followed by the **Create()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string subscriptionIdForUpgrade;
// Upgrade targetOffer;

UpgradeResult upgradeResult = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(subscriptionIdForUpgrade).Upgrades.Create(targetOffer);
```

<span data-ttu-id="96302-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="96302-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="96302-125">**Proje**: partnersdk. Featuresamples **sınıfı**: UpgradeSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="96302-125">**Project**: PartnerSDK.FeatureSamples **Class**: UpgradeSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="96302-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="96302-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="96302-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="96302-127">Request syntax</span></span>

| <span data-ttu-id="96302-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="96302-128">Method</span></span>   | <span data-ttu-id="96302-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="96302-129">Request URI</span></span>                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="96302-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="96302-130">**GET**</span></span>  | <span data-ttu-id="96302-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/yükseltmeler http/1.1</span><span class="sxs-lookup"><span data-stu-id="96302-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades HTTP/1.1</span></span> |
| <span data-ttu-id="96302-132">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="96302-132">**POST**</span></span> | <span data-ttu-id="96302-133">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Target}/yükseltmeler http/1.1</span><span class="sxs-lookup"><span data-stu-id="96302-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-target}/upgrades HTTP/1.1</span></span>       |

### <a name="uri-parameter"></a><span data-ttu-id="96302-134">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="96302-134">URI parameter</span></span>

<span data-ttu-id="96302-135">Aboneliği geçmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="96302-135">Use the following query parameter to transition the subscription.</span></span>

| <span data-ttu-id="96302-136">Ad</span><span class="sxs-lookup"><span data-stu-id="96302-136">Name</span></span>                    | <span data-ttu-id="96302-137">Tür</span><span class="sxs-lookup"><span data-stu-id="96302-137">Type</span></span>     | <span data-ttu-id="96302-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="96302-138">Required</span></span> | <span data-ttu-id="96302-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="96302-139">Description</span></span>                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| <span data-ttu-id="96302-140">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="96302-140">**customer-tenant-id**</span></span>  | <span data-ttu-id="96302-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="96302-141">**guid**</span></span> | <span data-ttu-id="96302-142">Y</span><span class="sxs-lookup"><span data-stu-id="96302-142">Y</span></span>        | <span data-ttu-id="96302-143">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="96302-143">A GUID corresponding to the customer.</span></span>             |
| <span data-ttu-id="96302-144">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="96302-144">**id-for-subscription**</span></span> | <span data-ttu-id="96302-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="96302-145">**guid**</span></span> | <span data-ttu-id="96302-146">Y</span><span class="sxs-lookup"><span data-stu-id="96302-146">Y</span></span>        | <span data-ttu-id="96302-147">İlk aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="96302-147">A GUID corresponding to the initial subscription.</span></span> |
| <span data-ttu-id="96302-148">**hedef için kimlik**</span><span class="sxs-lookup"><span data-stu-id="96302-148">**id-for-target**</span></span>       | <span data-ttu-id="96302-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="96302-149">**guid**</span></span> | <span data-ttu-id="96302-150">Y</span><span class="sxs-lookup"><span data-stu-id="96302-150">Y</span></span>        | <span data-ttu-id="96302-151">Hedef aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="96302-151">A GUID corresponding to the target subscription.</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="96302-152">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="96302-152">Request headers</span></span>

<span data-ttu-id="96302-153">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="96302-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="96302-154">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="96302-154">Request body</span></span>

<span data-ttu-id="96302-155">Yok</span><span class="sxs-lookup"><span data-stu-id="96302-155">None</span></span>

### <a name="request-example"></a><span data-ttu-id="96302-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="96302-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="96302-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="96302-157">REST response</span></span>

<span data-ttu-id="96302-158">Başarılı olursa, bu yöntem yanıt gövdesinde bir **yükseltme** sonucu kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="96302-158">If successful, this method returns an **Upgrade** result resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="96302-159">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="96302-159">Response success and error codes</span></span>

<span data-ttu-id="96302-160">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="96302-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="96302-161">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="96302-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="96302-162">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="96302-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="96302-163">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="96302-163">Response example</span></span>

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
