---
title: Ticari market aboneliğini iptal etme
description: Müşteri ve abonelik kimliğiyle İş Ortağı Merkezi ticari market Abonelik kaynağını iptal etmek için api'leri kullanmayı öğrenin.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 95fa265a3c103d1ec55066f12a3ede7fdb2d0170
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974293"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="aa8e9-103">İş Ortağı Merkezi API'lerini kullanarak ticari market aboneliğini iptal etme</span><span class="sxs-lookup"><span data-stu-id="aa8e9-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="aa8e9-104">Bu makalede, müşteri ve abonelik kimliğiyle İş Ortağı Merkezi ticari [](subscription-resources.md) market abonelik kaynağını iptal etmek için api'sini nasıl kullanabileceğiniz açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-104">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa8e9-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="aa8e9-105">Prerequisites</span></span>

- <span data-ttu-id="aa8e9-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="aa8e9-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="aa8e9-107">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="aa8e9-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="aa8e9-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="aa8e9-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="aa8e9-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="aa8e9-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="aa8e9-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="aa8e9-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="aa8e9-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="aa8e9-114">Abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-114">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="aa8e9-115">İş Ortağı Merkezi panosu yöntemi</span><span class="sxs-lookup"><span data-stu-id="aa8e9-115">Partner Center dashboard method</span></span>

<span data-ttu-id="aa8e9-116">İş Ortağı Merkezi panosunda ticari market aboneliğini iptal etmek için:</span><span class="sxs-lookup"><span data-stu-id="aa8e9-116">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="aa8e9-117">[Bir müşteri seçin.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="aa8e9-117">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="aa8e9-118">İptal etmek istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-118">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="aa8e9-119">Aboneliği iptal **et seçeneğini ve** ardından Gönder'i **seçin.**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-119">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="aa8e9-120">C\#</span><span class="sxs-lookup"><span data-stu-id="aa8e9-120">C\#</span></span>

<span data-ttu-id="aa8e9-121">Müşterinin aboneliğini iptal etmek için:</span><span class="sxs-lookup"><span data-stu-id="aa8e9-121">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="aa8e9-122">[Kimliğine göre aboneliği alın.](get-a-subscription-by-id.md)</span><span class="sxs-lookup"><span data-stu-id="aa8e9-122">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="aa8e9-123">Aboneliğin Status [**özelliğini**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) değiştirme.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-123">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="aa8e9-124">Durum kodları hakkında **bilgi** için [bkz. SubscriptionStatus numaralama.](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus)</span><span class="sxs-lookup"><span data-stu-id="aa8e9-124">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="aa8e9-125">Değişiklik yapıldıktan sonra, koleksiyonu kullanın **`IAggregatePartner.Customers`** ve **ById() yöntemini** arayın.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-125">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="aa8e9-126">Subscriptions [**özelliğini ve**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) ardından [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) çağırma.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-126">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="aa8e9-127">**Patch() yöntemini** çağırma.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-127">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="aa8e9-128">Örnek konsol test uygulaması</span><span class="sxs-lookup"><span data-stu-id="aa8e9-128">Sample console test app</span></span>

<span data-ttu-id="aa8e9-129">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="aa8e9-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="aa8e9-130">**Project:** PartnerSDK.FeatureSample **Sınıfı:** UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="aa8e9-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="aa8e9-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="aa8e9-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="aa8e9-132">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="aa8e9-132">Request syntax</span></span>

| <span data-ttu-id="aa8e9-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="aa8e9-133">Method</span></span>    | <span data-ttu-id="aa8e9-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="aa8e9-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="aa8e9-135">**Yama**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-135">**PATCH**</span></span> | <span data-ttu-id="aa8e9-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="aa8e9-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="aa8e9-137">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="aa8e9-137">URI parameter</span></span>

<span data-ttu-id="aa8e9-138">Bu tabloda aboneliği askıya almak için gereken sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="aa8e9-139">Ad</span><span class="sxs-lookup"><span data-stu-id="aa8e9-139">Name</span></span>                    | <span data-ttu-id="aa8e9-140">Tür</span><span class="sxs-lookup"><span data-stu-id="aa8e9-140">Type</span></span>     | <span data-ttu-id="aa8e9-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="aa8e9-141">Required</span></span> | <span data-ttu-id="aa8e9-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aa8e9-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="aa8e9-143">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="aa8e9-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-144">**guid**</span></span> | <span data-ttu-id="aa8e9-145">Y</span><span class="sxs-lookup"><span data-stu-id="aa8e9-145">Y</span></span>        | <span data-ttu-id="aa8e9-146">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="aa8e9-147">**abonelik için id**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-147">**id-for-subscription**</span></span> | <span data-ttu-id="aa8e9-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="aa8e9-148">**guid**</span></span> | <span data-ttu-id="aa8e9-149">Y</span><span class="sxs-lookup"><span data-stu-id="aa8e9-149">Y</span></span>        | <span data-ttu-id="aa8e9-150">Aboneliğe karşılık gelen BIR GUID.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="aa8e9-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="aa8e9-151">Request headers</span></span>

<span data-ttu-id="aa8e9-152">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="aa8e9-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="aa8e9-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="aa8e9-153">Request body</span></span>

<span data-ttu-id="aa8e9-154">İstek **gövdesinde** tam bir Abonelik kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="aa8e9-155">Status özelliğinin **güncelleştirilmiş** olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="aa8e9-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="aa8e9-156">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
If-Match: <etag>
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [{
        "type": "Full",
        "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
    }],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "publisherName": "publisher Name",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {"objectType": "Subscription"},
}
```

## <a name="rest-response"></a><span data-ttu-id="aa8e9-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="aa8e9-157">REST response</span></span>

<span data-ttu-id="aa8e9-158">Başarılı olursa, bu yöntem yanıt [gövdesinde](subscription-resources.md) silinen Abonelik kaynağı özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-158">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="aa8e9-159">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="aa8e9-159">Response success and error codes</span></span>

<span data-ttu-id="aa8e9-160">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="aa8e9-161">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="aa8e9-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="aa8e9-162">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="aa8e9-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="aa8e9-163">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="aa8e9-163">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1322
Content-Type: application/json; charset=utf-8
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
X-Locale: en-US

{
    "id": "6e7aa601-629e-461b-8933-0898c3cc3c7c",
    "offerId": "DZH318Z0BXWC:0001:DZH318Z0BMJX",
    "offerName": "offer Name",
    "friendlyName": "friendly Name",
    "quantity": 1,
    "unitType": "License(s)",
    "hasPurchasableAddons": false,
    "creationDate": "2019-01-04T01:00:12.6647304Z",
    "effectiveStartDate": "2019-01-09T00:21:45.9263727+00:00",
    "commitmentEndDate": "2019-02-08T00:21:45.9263727+00:00",
    "status": "deleted",
    "autoRenewEnabled": false,
    "isTrial": false,
    "billingType": "license",
    "billingCycle": "monthly",
    "termDuration": "P1M",
    "refundOptions": [
        {
            "type": "Full",
            "expiresAt": "2019-01-10T00:21:45.9263727+00:00"
        }
    ],
    "isMicrosoftProduct": false,
    "partnerId": "",
    "contractType": "subscription",
    "links": {
        "product": {
            "uri": "/products/DZH318Z0BXWC?country=US",
            "method": "GET",
            "headers": []
        },
        "sku": {
            "uri": "/products/DZH318Z0BXWC/skus/0001?country=US",
            "method": "GET",
            "headers": []
        },
        "availability": {
            "uri": "/products/DZH318Z0BXWC/skus/0001/availabilities/DZH318Z0BMJX?country=US",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/5921f00a-32c0-4457-aaa1-e8018c650895/subscriptions/6e7aa601-629e-461b-8933-0898c3cc3c7c",
            "method": "GET",
            "headers": []
        }
    },
    "publisherName": "publishe rName",
    "orderId": "ImxjLNL4_fOc-2KoyOxGTZcrlIquzls11",
    "attributes": {
        "etag": "",
        "objectType": "Subscription"
    }
}
```
