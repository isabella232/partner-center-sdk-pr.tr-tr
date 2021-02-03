---
title: Ticari market aboneliğini için otomatik yenilemeyi güncelleştirme
description: Müşteri ve abonelik KIMLIĞIYLE eşleşen bir abonelik kaynağı için autorenew özelliğini güncelleştirin.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dccec57901ea4ea429b74044e3b6c28178c43f6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769586"
---
# <a name="update-autorenew-for-a-commercial-marketplace-subscription"></a><span data-ttu-id="2946f-103">Ticari market aboneliğini için otomatik yenilemeyi güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2946f-103">Update autorenew for a commercial marketplace subscription</span></span>

<span data-ttu-id="2946f-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="2946f-104">**Applies To**</span></span>

- <span data-ttu-id="2946f-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2946f-105">Partner Center</span></span>

<span data-ttu-id="2946f-106">Müşteri ve abonelik KIMLIĞIYLE eşleşen bir ticari Market [abonelik](subscription-resources.md) kaynağı için autorenew özelliğini güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="2946f-106">Update the autorenew property for a commercial marketplace [Subscription](subscription-resources.md) resource that matches the customer and subscription ID.</span></span>

<span data-ttu-id="2946f-107">Iş Ortağı Merkezi panosunda, bu işlem ilk olarak [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilir.</span><span class="sxs-lookup"><span data-stu-id="2946f-107">In the Partner Center dashboard, this operation is performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="2946f-108">Ardından, güncelleştirmek istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="2946f-108">Then, select the subscription that you wish to update.</span></span> <span data-ttu-id="2946f-109">Son olarak, **Otomatik Yenile** seçeneğini açıp **Gönder**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2946f-109">Finally, toggle the **Auto-renew** option, then select **Submit**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2946f-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2946f-110">Prerequisites</span></span>

- <span data-ttu-id="2946f-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2946f-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2946f-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2946f-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2946f-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2946f-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2946f-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2946f-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2946f-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2946f-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2946f-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2946f-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2946f-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="2946f-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2946f-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="2946f-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2946f-119">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="2946f-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="2946f-120">C\#</span><span class="sxs-lookup"><span data-stu-id="2946f-120">C\#</span></span>

<span data-ttu-id="2946f-121">Bir müşterinin aboneliğini güncelleştirmek için önce [aboneliği alın](get-a-subscription-by-id.md), sonra aboneliğin [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) özelliğini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2946f-121">To update a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then set the subscription's [**autoRenewEnabled**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.autoRenewEnabled) property.</span></span> <span data-ttu-id="2946f-122">Değişiklik yapıldıktan sonra **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2946f-122">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="2946f-123">Ardından, ve ardından [**Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemiyle [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2946f-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="2946f-124">Ardından, **Patch ()** yöntemini çağırarak son ' u kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2946f-124">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

// turn off auto renew.
selectedSubscription.AutoRenewEnabled = false;
var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="2946f-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2946f-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2946f-126">**Proje**: Partnersdk. Featuresample **sınıfı**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="2946f-126">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2946f-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2946f-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2946f-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2946f-128">Request syntax</span></span>

| <span data-ttu-id="2946f-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2946f-129">Method</span></span>    | <span data-ttu-id="2946f-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2946f-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2946f-131">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="2946f-131">**PATCH**</span></span> | <span data-ttu-id="2946f-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2946f-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2946f-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="2946f-133">URI parameter</span></span>

<span data-ttu-id="2946f-134">Bu tabloda, aboneliği askıya almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="2946f-134">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="2946f-135">Ad</span><span class="sxs-lookup"><span data-stu-id="2946f-135">Name</span></span>                    | <span data-ttu-id="2946f-136">Tür</span><span class="sxs-lookup"><span data-stu-id="2946f-136">Type</span></span>     | <span data-ttu-id="2946f-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2946f-137">Required</span></span> | <span data-ttu-id="2946f-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2946f-138">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="2946f-139">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="2946f-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="2946f-140">**'INI**</span><span class="sxs-lookup"><span data-stu-id="2946f-140">**GUID**</span></span> | <span data-ttu-id="2946f-141">Y</span><span class="sxs-lookup"><span data-stu-id="2946f-141">Y</span></span>        | <span data-ttu-id="2946f-142">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="2946f-142">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="2946f-143">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="2946f-143">**id-for-subscription**</span></span> | <span data-ttu-id="2946f-144">**'INI**</span><span class="sxs-lookup"><span data-stu-id="2946f-144">**GUID**</span></span> | <span data-ttu-id="2946f-145">Y</span><span class="sxs-lookup"><span data-stu-id="2946f-145">Y</span></span>        | <span data-ttu-id="2946f-146">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="2946f-146">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2946f-147">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2946f-147">Request headers</span></span>

<span data-ttu-id="2946f-148">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2946f-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2946f-149">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2946f-149">Request body</span></span>

<span data-ttu-id="2946f-150">İstek gövdesinde tam bir ticari Market **abonelik** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2946f-150">A full commercial marketplace **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="2946f-151">**AutoRenewEnabled** özelliğinin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2946f-151">Ensure that the **AutoRenewEnabled** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="2946f-152">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2946f-152">Request example</span></span>

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
    "status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="2946f-153">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2946f-153">REST response</span></span>

<span data-ttu-id="2946f-154">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [abonelik](subscription-resources.md) kaynak özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="2946f-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2946f-155">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2946f-155">Response success and error codes</span></span>

<span data-ttu-id="2946f-156">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2946f-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2946f-157">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2946f-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2946f-158">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2946f-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2946f-159">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2946f-159">Response example</span></span>

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
    "status": "active",
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
