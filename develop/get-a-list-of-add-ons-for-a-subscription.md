---
title: Bir abonelik için eklentilerin bir listesini alma
description: Bir müşterinin aboneliğine eklemek üzere seçtiği eklentilerin koleksiyonunu alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4e62ad22cf30c34dedfeb628003c695e33b78758
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769335"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="ed07c-103">Bir abonelik için eklentilerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="ed07c-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="ed07c-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="ed07c-104">**Applies to:**</span></span>

- <span data-ttu-id="ed07c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ed07c-105">Partner Center</span></span>
- <span data-ttu-id="ed07c-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ed07c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="ed07c-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ed07c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="ed07c-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ed07c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ed07c-109">Bu makalede, bir müşterinin **[abonelik](subscription-resources.md)** kaynağına eklemeyi seçtiği eklentilerin nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="ed07c-109">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ed07c-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ed07c-110">Prerequisites</span></span>

- <span data-ttu-id="ed07c-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ed07c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ed07c-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="ed07c-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ed07c-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ed07c-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ed07c-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ed07c-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ed07c-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="ed07c-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ed07c-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ed07c-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ed07c-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="ed07c-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ed07c-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="ed07c-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ed07c-119">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="ed07c-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="ed07c-120">C\#</span><span class="sxs-lookup"><span data-stu-id="ed07c-120">C\#</span></span>

<span data-ttu-id="ed07c-121">Bir müşterinin aboneliğine ait eklentilerin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="ed07c-121">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="ed07c-122">**Byıd ()** yöntemini çağırmak Için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed07c-122">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="ed07c-123">[**Abonelik**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın, ardından [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="ed07c-123">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="ed07c-124">[**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) özelliğini çağırın, bunu [**Get ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync)ile yapın.</span><span class="sxs-lookup"><span data-stu-id="ed07c-124">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="ed07c-125">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="ed07c-125">For an example, see the following:</span></span>

- <span data-ttu-id="ed07c-126">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="ed07c-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="ed07c-127">Proje: **Partnersdk. FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="ed07c-127">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="ed07c-128">Sınıf: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="ed07c-128">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="ed07c-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="ed07c-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ed07c-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="ed07c-130">Request syntax</span></span>

| <span data-ttu-id="ed07c-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="ed07c-131">Method</span></span>  | <span data-ttu-id="ed07c-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="ed07c-132">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ed07c-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="ed07c-133">**GET**</span></span> | <span data-ttu-id="ed07c-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/addons http/1.1</span><span class="sxs-lookup"><span data-stu-id="ed07c-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="ed07c-135">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="ed07c-135">URI parameter</span></span>

<span data-ttu-id="ed07c-136">Bu tablo, abonelik için eklentilerin listesini almak üzere gerekli sorgu parametrelerini listeler.</span><span class="sxs-lookup"><span data-stu-id="ed07c-136">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="ed07c-137">Ad</span><span class="sxs-lookup"><span data-stu-id="ed07c-137">Name</span></span>                    | <span data-ttu-id="ed07c-138">Tür</span><span class="sxs-lookup"><span data-stu-id="ed07c-138">Type</span></span>     | <span data-ttu-id="ed07c-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ed07c-139">Required</span></span> | <span data-ttu-id="ed07c-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ed07c-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="ed07c-141">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="ed07c-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="ed07c-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="ed07c-142">**guid**</span></span> | <span data-ttu-id="ed07c-143">Y</span><span class="sxs-lookup"><span data-stu-id="ed07c-143">Y</span></span>        | <span data-ttu-id="ed07c-144">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="ed07c-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="ed07c-145">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="ed07c-145">**id-for-subscription**</span></span> | <span data-ttu-id="ed07c-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="ed07c-146">**guid**</span></span> | <span data-ttu-id="ed07c-147">Y</span><span class="sxs-lookup"><span data-stu-id="ed07c-147">Y</span></span>        | <span data-ttu-id="ed07c-148">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="ed07c-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ed07c-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="ed07c-149">Request headers</span></span>

<span data-ttu-id="ed07c-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ed07c-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ed07c-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="ed07c-151">Request body</span></span>

<span data-ttu-id="ed07c-152">Yok.</span><span class="sxs-lookup"><span data-stu-id="ed07c-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="ed07c-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="ed07c-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="ed07c-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="ed07c-154">REST response</span></span>

<span data-ttu-id="ed07c-155">Başarılı olursa, bu yöntem yanıt gövdesinde bir kaynak koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="ed07c-155">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ed07c-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ed07c-156">Response success and error codes</span></span>

<span data-ttu-id="ed07c-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="ed07c-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ed07c-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ed07c-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ed07c-159">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ed07c-159">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ed07c-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="ed07c-160">Response example</span></span>

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
        "entitlementId": "42226ed6-070a-4e0f-b80c-4cdfB3e97aa7",
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
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
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
