---
title: Bir abonelik için eklentilerin bir listesini alma
description: Müşterinin aboneliğine eklemeyi seçtiği eklenti koleksiyonunu alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: c627f595333a295048b02ec4326dcdc279d07b51
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874644"
---
# <a name="get-a-list-of-add-ons-for-a-subscription"></a><span data-ttu-id="d3ddf-103">Bir abonelik için eklentilerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="d3ddf-103">Get a list of add-ons for a subscription</span></span>

<span data-ttu-id="d3ddf-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d3ddf-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d3ddf-105">Bu makalede, bir müşterinin Abonelik kaynağına eklemeyi seçtiği eklenti koleksiyonunun nasıl alın **[açıklanmıştır.](subscription-resources.md)**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-105">This article describes how to get a collection of add-ons that a customer has chosen to add to their **[Subscription](subscription-resources.md)** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d3ddf-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d3ddf-106">Prerequisites</span></span>

- <span data-ttu-id="d3ddf-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d3ddf-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d3ddf-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d3ddf-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d3ddf-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d3ddf-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d3ddf-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d3ddf-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d3ddf-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d3ddf-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d3ddf-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d3ddf-115">Abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-115">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="d3ddf-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d3ddf-116">C\#</span></span>

<span data-ttu-id="d3ddf-117">Müşterinin aboneliği için eklentilerin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="d3ddf-117">To get the list of add-ons for a customer's subscription:</span></span>

1. <span data-ttu-id="d3ddf-118">**ById()** **yöntemini çağırarak IAggregatePartner.Customers** koleksiyonu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-118">Use your **IAggregatePartner.Customers** collection to call the **ById()** method.</span></span>

2. <span data-ttu-id="d3ddf-119">Subscriptions [**özelliğini ve**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) ardından [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) çağırma.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-119">Call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span>

3. <span data-ttu-id="d3ddf-120">Addons [**özelliğini,**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) ardından [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) veya [**GetAsync() çağrısı.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync)</span><span class="sxs-lookup"><span data-stu-id="d3ddf-120">Call the [**Addons**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.addons) property, followed by [**Get()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionaddoncollection.getasync).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// var selectedSubscription Subscription;

var subscriptionDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).AddOns.Get();

```

<span data-ttu-id="d3ddf-121">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="d3ddf-121">For an example, see the following:</span></span>

- <span data-ttu-id="d3ddf-122">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d3ddf-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d3ddf-123">Project: **PartnerSDK.FeatureSample**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-123">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="d3ddf-124">Sınıf: **SubscriptionAddons.cs**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-124">Class: **SubscriptionAddons.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="d3ddf-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d3ddf-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d3ddf-126">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="d3ddf-126">Request syntax</span></span>

| <span data-ttu-id="d3ddf-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d3ddf-127">Method</span></span>  | <span data-ttu-id="d3ddf-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d3ddf-128">Request URI</span></span>                                                                                                                       |
|---------|-----------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d3ddf-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-129">**GET**</span></span> | <span data-ttu-id="d3ddf-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d3ddf-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/addons HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d3ddf-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d3ddf-131">URI parameter</span></span>

<span data-ttu-id="d3ddf-132">Bu tabloda abonelik için eklentilerin listesini almak için gerekli sorgu parametreleri listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-132">This table lists the required query parameters to get the list of add-ons for the subscription.</span></span>

| <span data-ttu-id="d3ddf-133">Ad</span><span class="sxs-lookup"><span data-stu-id="d3ddf-133">Name</span></span>                    | <span data-ttu-id="d3ddf-134">Tür</span><span class="sxs-lookup"><span data-stu-id="d3ddf-134">Type</span></span>     | <span data-ttu-id="d3ddf-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d3ddf-135">Required</span></span> | <span data-ttu-id="d3ddf-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d3ddf-136">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="d3ddf-137">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-137">**customer-tenant-id**</span></span>  | <span data-ttu-id="d3ddf-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-138">**guid**</span></span> | <span data-ttu-id="d3ddf-139">Y</span><span class="sxs-lookup"><span data-stu-id="d3ddf-139">Y</span></span>        | <span data-ttu-id="d3ddf-140">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-140">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="d3ddf-141">**abonelik için id**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-141">**id-for-subscription**</span></span> | <span data-ttu-id="d3ddf-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="d3ddf-142">**guid**</span></span> | <span data-ttu-id="d3ddf-143">Y</span><span class="sxs-lookup"><span data-stu-id="d3ddf-143">Y</span></span>        | <span data-ttu-id="d3ddf-144">Aboneliğe karşılık gelen BIR GUID.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-144">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d3ddf-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d3ddf-145">Request headers</span></span>

<span data-ttu-id="d3ddf-146">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d3ddf-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d3ddf-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d3ddf-147">Request body</span></span>

<span data-ttu-id="d3ddf-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d3ddf-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d3ddf-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription>/addons HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 429902e2-ea2f-4704-b8a0-27fc53c539ba
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
```

## <a name="rest-response"></a><span data-ttu-id="d3ddf-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d3ddf-150">REST response</span></span>

<span data-ttu-id="d3ddf-151">Başarılı olursa, bu yöntem yanıt gövdesinde bir kaynak koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-151">If successful, this method returns a collection of resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d3ddf-152">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d3ddf-152">Response success and error codes</span></span>

<span data-ttu-id="d3ddf-153">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d3ddf-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d3ddf-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d3ddf-155">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d3ddf-155">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d3ddf-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d3ddf-156">Response example</span></span>

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
