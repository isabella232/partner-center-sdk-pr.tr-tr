---
title: Siparişe göre aboneliklerin bir listesini alma
description: Belirli bir sıraya karşılık gelen bir abonelik kaynakları koleksiyonunu alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 56b9c80021cace03976d410b2a6cd4c0eee18398
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769551"
---
# <a name="get-a-list-of-subscriptions-by-order"></a><span data-ttu-id="06a06-103">Siparişe göre aboneliklerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="06a06-103">Get a list of subscriptions by order</span></span>

<span data-ttu-id="06a06-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="06a06-104">**Applies To**</span></span>

- <span data-ttu-id="06a06-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="06a06-105">Partner Center</span></span>
- <span data-ttu-id="06a06-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="06a06-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="06a06-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="06a06-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="06a06-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="06a06-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="06a06-109">Belirli bir sıraya karşılık gelen bir [abonelik](subscription-resources.md) kaynakları koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="06a06-109">Gets a collection of [Subscription](subscription-resources.md) resources that correspond to a given order.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="06a06-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="06a06-110">Prerequisites</span></span>

- <span data-ttu-id="06a06-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="06a06-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="06a06-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="06a06-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="06a06-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="06a06-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="06a06-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06a06-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="06a06-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="06a06-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="06a06-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="06a06-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="06a06-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="06a06-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="06a06-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="06a06-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="06a06-119">Bir sipariş KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="06a06-119">An order ID.</span></span>

## <a name="c"></a><span data-ttu-id="06a06-120">C\#</span><span class="sxs-lookup"><span data-stu-id="06a06-120">C\#</span></span>

<span data-ttu-id="06a06-121">Aboneliklerin bir listesini sıraya göre almak için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="06a06-121">To get a list of subscriptions by order, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="06a06-122">Ardından **BYORDER ()** yöntemi tarafından izlenen [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="06a06-122">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the **ByOrder()** method.</span></span> <span data-ttu-id="06a06-123">[**Get ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync)çağırarak son.</span><span class="sxs-lookup"><span data-stu-id="06a06-123">Finish by calling [**Get()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// string orderID;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ByOrder(orderID).Get();
```

<span data-ttu-id="06a06-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="06a06-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="06a06-125">**Proje**: Partnersdk. Featuresample **sınıfı**: SubscriptionsByOrder.cs</span><span class="sxs-lookup"><span data-stu-id="06a06-125">**Project**: PartnerSDK.FeatureSample **Class**: SubscriptionsByOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="06a06-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="06a06-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="06a06-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="06a06-127">Request syntax</span></span>

| <span data-ttu-id="06a06-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="06a06-128">Method</span></span>  | <span data-ttu-id="06a06-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="06a06-129">Request URI</span></span>                                                                                                                   |
|---------|-------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="06a06-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="06a06-130">**GET**</span></span> | <span data-ttu-id="06a06-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/abonelikler? order \_ ID = {-for-Order} http/1.1</span><span class="sxs-lookup"><span data-stu-id="06a06-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions?order\_id={id-for-order} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="06a06-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="06a06-132">URI parameter</span></span>

<span data-ttu-id="06a06-133">Bu tablo, tüm abonelikleri almak için gerekli sorgu parametresini listeler.</span><span class="sxs-lookup"><span data-stu-id="06a06-133">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="06a06-134">Ad</span><span class="sxs-lookup"><span data-stu-id="06a06-134">Name</span></span>                   | <span data-ttu-id="06a06-135">Tür</span><span class="sxs-lookup"><span data-stu-id="06a06-135">Type</span></span>     | <span data-ttu-id="06a06-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="06a06-136">Required</span></span> | <span data-ttu-id="06a06-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="06a06-137">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="06a06-138">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="06a06-138">**customer-tenant-id**</span></span> | <span data-ttu-id="06a06-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="06a06-139">**guid**</span></span> | <span data-ttu-id="06a06-140">Y</span><span class="sxs-lookup"><span data-stu-id="06a06-140">Y</span></span>        | <span data-ttu-id="06a06-141">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="06a06-141">A GUID corresponding to the customer.</span></span> |
| <span data-ttu-id="06a06-142">**sıra kimliği**</span><span class="sxs-lookup"><span data-stu-id="06a06-142">**id-for-order**</span></span>       | <span data-ttu-id="06a06-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="06a06-143">**guid**</span></span> | <span data-ttu-id="06a06-144">Y</span><span class="sxs-lookup"><span data-stu-id="06a06-144">Y</span></span>        | <span data-ttu-id="06a06-145">Sıraya karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="06a06-145">A GUID corresponding to the order.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="06a06-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="06a06-146">Request headers</span></span>

<span data-ttu-id="06a06-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="06a06-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="06a06-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="06a06-148">Request body</span></span>

<span data-ttu-id="06a06-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="06a06-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="06a06-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="06a06-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions?order_id={id-for-order} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 16fee928-dc2c-412f-adbb-871f68babf16
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="06a06-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="06a06-151">REST response</span></span>

<span data-ttu-id="06a06-152">Başarılı olursa, bu yöntem yanıt gövdesinde bir [abonelik](subscription-resources.md) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="06a06-152">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="06a06-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="06a06-153">Response success and error codes</span></span>

<span data-ttu-id="06a06-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="06a06-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="06a06-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="06a06-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="06a06-156">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="06a06-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="06a06-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="06a06-157">Response example</span></span>

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
