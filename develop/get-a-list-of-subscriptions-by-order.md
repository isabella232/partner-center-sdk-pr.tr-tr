---
title: Siparişe göre aboneliklerin bir listesini alma
description: Verilen siparişe karşılık gelen Abonelik kaynakları koleksiyonunu alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 011a92500d0c7ed44f86030febd1ea83be2c6474
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873978"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="e07b6-103">Siparişe göre aboneliklerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="e07b6-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="e07b6-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e07b6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e07b6-105">Verilen siparişe [karşılık gelen](subscription-resources.md) Abonelik kaynakları koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="e07b6-105">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e07b6-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e07b6-106">Prerequisites</span></span>

- <span data-ttu-id="e07b6-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e07b6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e07b6-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e07b6-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="e07b6-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="e07b6-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="e07b6-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="e07b6-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="e07b6-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="e07b6-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="e07b6-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="e07b6-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="e07b6-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="e07b6-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="e07b6-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="e07b6-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="e07b6-115">Sipariş kimliği.</span><span class="sxs-lookup"><span data-stu-id="e07b6-115">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="e07b6-116">C\#</span><span class="sxs-lookup"><span data-stu-id="e07b6-116">C\#</span></span>

<span data-ttu-id="e07b6-117">Siparişe göre aboneliklerin listesini almak için **IAggregatePartner.Customers** koleksiyonu kullanın ve **ById() yöntemini** arayın.</span><span class="sxs-lookup"><span data-stu-id="e07b6-117">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="e07b6-118">Ardından [**Subscriptions özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) ve ardından **ByOrder() yöntemini** çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e07b6-118">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="e07b6-119">Get() veya [**GetAsync() çağrısıyla bitirin.**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) [](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get)</span><span class="sxs-lookup"><span data-stu-id="e07b6-119">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="e07b6-120">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e07b6-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e07b6-121">**Project:** PartnerSDK.FeatureSample **Sınıfı:** SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="e07b6-121">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e07b6-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e07b6-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e07b6-123">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="e07b6-123">Request syntax</span></span>

| <span data-ttu-id="e07b6-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e07b6-124">Method</span></span>  | <span data-ttu-id="e07b6-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e07b6-125">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="e07b6-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="e07b6-126">**GET**</span></span> | <span data-ttu-id="e07b6-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order \_ id={id-for-order} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e07b6-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e07b6-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="e07b6-128">URI parameter</span></span>

<span data-ttu-id="e07b6-129">Bu tabloda tüm abonelikleri almak için gerekli sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="e07b6-129">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="e07b6-130">Ad</span><span class="sxs-lookup"><span data-stu-id="e07b6-130">Name</span></span>                   | <span data-ttu-id="e07b6-131">Tür</span><span class="sxs-lookup"><span data-stu-id="e07b6-131">Type</span></span>     | <span data-ttu-id="e07b6-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e07b6-132">Required</span></span> | <span data-ttu-id="e07b6-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e07b6-133">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="e07b6-134">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="e07b6-134">**customer-tenant-id**</span></span> | <span data-ttu-id="e07b6-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="e07b6-135">**guid**</span></span> | <span data-ttu-id="e07b6-136">Y</span><span class="sxs-lookup"><span data-stu-id="e07b6-136">Y</span></span>        | <span data-ttu-id="e07b6-137">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="e07b6-137">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="e07b6-138">**sipariş için id**</span><span class="sxs-lookup"><span data-stu-id="e07b6-138">**id-for-order**</span></span>       | <span data-ttu-id="e07b6-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="e07b6-139">**guid**</span></span> | <span data-ttu-id="e07b6-140">Y</span><span class="sxs-lookup"><span data-stu-id="e07b6-140">Y</span></span>        | <span data-ttu-id="e07b6-141">Siparişe karşılık gelen BIR GUID.</span><span class="sxs-lookup"><span data-stu-id="e07b6-141">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="e07b6-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e07b6-142">Request headers</span></span>

<span data-ttu-id="e07b6-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e07b6-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e07b6-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e07b6-144">Request body</span></span>

<span data-ttu-id="e07b6-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="e07b6-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="e07b6-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e07b6-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="e07b6-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e07b6-147">REST response</span></span>

<span data-ttu-id="e07b6-148">Başarılı olursa, bu yöntem yanıt [gövdesinde Abonelik](subscription-resources.md) kaynakları koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="e07b6-148">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e07b6-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e07b6-149">Response success and error codes</span></span>

<span data-ttu-id="e07b6-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="e07b6-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e07b6-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e07b6-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e07b6-152">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e07b6-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e07b6-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e07b6-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
Date: Wed, 25 Nov 2015 05:50:45 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "Myofferpurchase",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "{id-for-order}",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
