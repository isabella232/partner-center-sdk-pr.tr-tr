---
title: Ticari market aboneliğini iptal etme
description: Müşteri ve abonelik KIMLIĞIYLE eşleşen bir ticari Market abonelik kaynağını iptal etmek için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38708c17b31e39a5e7c436e0d76b4ebabbc3a801
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770078"
---
# <a name="cancel-a-commercial-marketplace-subscription-using-partner-center-apis"></a><span data-ttu-id="6ff57-103">Iş Ortağı Merkezi API 'Lerini kullanarak ticari Market aboneliğini iptal etme</span><span class="sxs-lookup"><span data-stu-id="6ff57-103">Cancel a commercial marketplace subscription using Partner Center APIs</span></span>

<span data-ttu-id="6ff57-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="6ff57-104">**Applies to:**</span></span>

- <span data-ttu-id="6ff57-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6ff57-105">Partner Center</span></span>

<span data-ttu-id="6ff57-106">Bu makalede, Iş Ortağı Merkezi API 'sini müşteri ve abonelik KIMLIĞIYLE eşleşen bir ticari Market [abonelik](subscription-resources.md) kaynağını iptal etmek için nasıl kullanabileceğiniz açıklanır.</span><span class="sxs-lookup"><span data-stu-id="6ff57-106">This article describes how you can use Partner Center API to cancel a commercial marketplace [subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ff57-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6ff57-107">Prerequisites</span></span>

- <span data-ttu-id="6ff57-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6ff57-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6ff57-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="6ff57-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="6ff57-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6ff57-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6ff57-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6ff57-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6ff57-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="6ff57-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6ff57-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6ff57-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6ff57-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="6ff57-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6ff57-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="6ff57-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6ff57-116">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="6ff57-116">A subscription ID.</span></span>

## <a name="partner-center-dashboard-method"></a><span data-ttu-id="6ff57-117">İş Ortağı Merkezi Pano yöntemi</span><span class="sxs-lookup"><span data-stu-id="6ff57-117">Partner Center dashboard method</span></span>

<span data-ttu-id="6ff57-118">Iş Ortağı Merkezi panosunda bir ticari Market aboneliğini iptal etmek için:</span><span class="sxs-lookup"><span data-stu-id="6ff57-118">To cancel a commercial marketplace subscription in the Partner Center dashboard:</span></span>

1. <span data-ttu-id="6ff57-119">[Bir müşteri seçin](get-a-customer-by-name.md).</span><span class="sxs-lookup"><span data-stu-id="6ff57-119">[Select a customer](get-a-customer-by-name.md).</span></span>

2. <span data-ttu-id="6ff57-120">İptal etmek istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="6ff57-120">Select the subscription that you wish to cancel.</span></span>

3. <span data-ttu-id="6ff57-121">**Aboneliği Iptal et** seçeneğini belirleyip **Gönder**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="6ff57-121">Choose the **Cancel subscription** option, then select **Submit**.</span></span>

## <a name="c"></a><span data-ttu-id="6ff57-122">C\#</span><span class="sxs-lookup"><span data-stu-id="6ff57-122">C\#</span></span>

<span data-ttu-id="6ff57-123">Bir müşterinin aboneliğini iptal etmek için:</span><span class="sxs-lookup"><span data-stu-id="6ff57-123">To cancel a customer's subscription:</span></span>

1. <span data-ttu-id="6ff57-124">[ABONELIĞI kimliğe göre alın](get-a-subscription-by-id.md).</span><span class="sxs-lookup"><span data-stu-id="6ff57-124">[Get the subscription by ID](get-a-subscription-by-id.md).</span></span>

2. <span data-ttu-id="6ff57-125">Aboneliğin [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) özelliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="6ff57-125">Change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="6ff57-126">**Durum** kodları hakkında bilgi için bkz. [subscriptionstatus numaralandırması](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="6ff57-126">For information on **Status** codes, see [SubscriptionStatus enumeration](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span>

3. <span data-ttu-id="6ff57-127">Değişiklik yapıldıktan sonra, **`IAggregatePartner.Customers`** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="6ff57-127">After the change is made, use your **`IAggregatePartner.Customers`** collection and call the **ById()** method.</span></span>

4. <span data-ttu-id="6ff57-128">[**Abonelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın, ardından [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="6ff57-128">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

5. <span data-ttu-id="6ff57-129">**Patch ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="6ff57-129">Call the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

selectedSubscription.Status = SubscriptionStatus.Deleted;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

### <a name="sample-console-test-app"></a><span data-ttu-id="6ff57-130">Örnek konsol test uygulaması</span><span class="sxs-lookup"><span data-stu-id="6ff57-130">Sample console test app</span></span>

<span data-ttu-id="6ff57-131">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6ff57-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6ff57-132">**Proje**: Partnersdk. Featuresample **sınıfı**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="6ff57-132">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6ff57-133">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6ff57-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6ff57-134">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6ff57-134">Request syntax</span></span>

| <span data-ttu-id="6ff57-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6ff57-135">Method</span></span>    | <span data-ttu-id="6ff57-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6ff57-136">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="6ff57-137">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="6ff57-137">**PATCH**</span></span> | <span data-ttu-id="6ff57-138">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="6ff57-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6ff57-139">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="6ff57-139">URI parameter</span></span>

<span data-ttu-id="6ff57-140">Bu tabloda, aboneliği askıya almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-140">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="6ff57-141">Ad</span><span class="sxs-lookup"><span data-stu-id="6ff57-141">Name</span></span>                    | <span data-ttu-id="6ff57-142">Tür</span><span class="sxs-lookup"><span data-stu-id="6ff57-142">Type</span></span>     | <span data-ttu-id="6ff57-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6ff57-143">Required</span></span> | <span data-ttu-id="6ff57-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6ff57-144">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="6ff57-145">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="6ff57-145">**customer-tenant-id**</span></span>  | <span data-ttu-id="6ff57-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="6ff57-146">**guid**</span></span> | <span data-ttu-id="6ff57-147">Y</span><span class="sxs-lookup"><span data-stu-id="6ff57-147">Y</span></span>        | <span data-ttu-id="6ff57-148">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="6ff57-148">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="6ff57-149">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="6ff57-149">**id-for-subscription**</span></span> | <span data-ttu-id="6ff57-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="6ff57-150">**guid**</span></span> | <span data-ttu-id="6ff57-151">Y</span><span class="sxs-lookup"><span data-stu-id="6ff57-151">Y</span></span>        | <span data-ttu-id="6ff57-152">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="6ff57-152">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6ff57-153">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6ff57-153">Request headers</span></span>

<span data-ttu-id="6ff57-154">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6ff57-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6ff57-155">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6ff57-155">Request body</span></span>

<span data-ttu-id="6ff57-156">İstek gövdesinde tam bir **abonelik** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-156">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="6ff57-157">**Status** özelliğinin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="6ff57-157">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="6ff57-158">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6ff57-158">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6ff57-159">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6ff57-159">REST response</span></span>

<span data-ttu-id="6ff57-160">Başarılı olursa, bu yöntem yanıt gövdesinde silinen [abonelik](subscription-resources.md) kaynak özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="6ff57-160">If successful, this method returns deleted [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6ff57-161">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6ff57-161">Response success and error codes</span></span>

<span data-ttu-id="6ff57-162">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="6ff57-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6ff57-163">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6ff57-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6ff57-164">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6ff57-164">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6ff57-165">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6ff57-165">Response example</span></span>

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
