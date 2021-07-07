---
title: Bir aboneliği askıya alma
description: Sahtekarlık veya ödeme dışı nedenlerle müşteri ve abonelik KIMLIĞIYLE eşleşen bir abonelik kaynağını askıya alır. Iş Ortağı Merkezi panosunda, bu işlem önce bir müşteri seçilerek gerçekleştirilebilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7dae7c3422a403c48a2b10424c4ae5dbdbc498ea
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547351"
---
# <a name="suspend-a-subscription"></a><span data-ttu-id="30210-104">Bir aboneliği askıya alma</span><span class="sxs-lookup"><span data-stu-id="30210-104">Suspend a subscription</span></span>

<span data-ttu-id="30210-105">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="30210-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="30210-106">Sahtekarlık veya ödeme dışı nedenlerle müşteri ve abonelik KIMLIĞIYLE eşleşen bir [abonelik](subscription-resources.md) kaynağını askıya alır.</span><span class="sxs-lookup"><span data-stu-id="30210-106">Suspends a [Subscription](subscription-resources.md) resource that matches the customer and subscription ID due to fraud or non-payment.</span></span>

<span data-ttu-id="30210-107">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="30210-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="30210-108">Sonra, söz konusu dosyayı yeniden adlandırmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="30210-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="30210-109">Son olarak, **askıya alındı** düğmesini seçin ve ardından Gönder ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="30210-109">To finish, choose the **Suspended** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="30210-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="30210-110">Prerequisites</span></span>

- <span data-ttu-id="30210-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="30210-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="30210-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="30210-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="30210-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="30210-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="30210-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30210-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="30210-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="30210-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="30210-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="30210-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="30210-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="30210-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="30210-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="30210-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="30210-119">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="30210-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="30210-120">C\#</span><span class="sxs-lookup"><span data-stu-id="30210-120">C\#</span></span>

<span data-ttu-id="30210-121">Bir müşterinin aboneliğini askıya almak için önce [aboneliği alın](get-a-subscription-by-id.md), sonra aboneliğin [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) özelliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="30210-121">To suspend a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="30210-122">**Durum** kodları hakkında bilgi için bkz. [subscriptionstatus Enumeration/DotNet/api/Microsoft. Store. partnercenter. modeller. abonelikler. subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="30210-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="30210-123">Değişiklik yapıldıktan sonra **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="30210-123">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="30210-124">Ardından, ve ardından [**Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemiyle [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="30210-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="30210-125">Ardından, **Patch ()** yöntemini çağırarak son ' u kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="30210-125">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId as string;
// Subscription selectedSubscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Suspended
   });
```

<span data-ttu-id="30210-126">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="30210-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="30210-127">**Project**: partnersdk. featuresample **sınıfı**: updatesubscription. cs</span><span class="sxs-lookup"><span data-stu-id="30210-127">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="30210-128">REST isteği</span><span class="sxs-lookup"><span data-stu-id="30210-128">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="30210-129">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="30210-129">Request syntax</span></span>

| <span data-ttu-id="30210-130">Yöntem</span><span class="sxs-lookup"><span data-stu-id="30210-130">Method</span></span>    | <span data-ttu-id="30210-131">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="30210-131">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="30210-132">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="30210-132">**PATCH**</span></span> | <span data-ttu-id="30210-133">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="30210-133">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="30210-134">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="30210-134">URI parameter</span></span>

<span data-ttu-id="30210-135">Bu tabloda, aboneliği askıya almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="30210-135">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="30210-136">Ad</span><span class="sxs-lookup"><span data-stu-id="30210-136">Name</span></span>                    | <span data-ttu-id="30210-137">Tür</span><span class="sxs-lookup"><span data-stu-id="30210-137">Type</span></span>     | <span data-ttu-id="30210-138">Gerekli</span><span class="sxs-lookup"><span data-stu-id="30210-138">Required</span></span> | <span data-ttu-id="30210-139">Açıklama</span><span class="sxs-lookup"><span data-stu-id="30210-139">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="30210-140">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="30210-140">**customer-tenant-id**</span></span>  | <span data-ttu-id="30210-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="30210-141">**guid**</span></span> | <span data-ttu-id="30210-142">Y</span><span class="sxs-lookup"><span data-stu-id="30210-142">Y</span></span>        | <span data-ttu-id="30210-143">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="30210-143">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="30210-144">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="30210-144">**id-for-subscription**</span></span> | <span data-ttu-id="30210-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="30210-145">**guid**</span></span> | <span data-ttu-id="30210-146">Y</span><span class="sxs-lookup"><span data-stu-id="30210-146">Y</span></span>        | <span data-ttu-id="30210-147">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="30210-147">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="30210-148">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="30210-148">Request headers</span></span>

<span data-ttu-id="30210-149">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="30210-149">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="30210-150">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="30210-150">Request body</span></span>

<span data-ttu-id="30210-151">İstek gövdesinde tam bir **abonelik** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="30210-151">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="30210-152">**Status** özelliğinin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="30210-152">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="30210-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="30210-153">Request example</span></span>

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
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="30210-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="30210-154">REST response</span></span>

<span data-ttu-id="30210-155">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [abonelik](subscription-resources.md) kaynak özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="30210-155">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="30210-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="30210-156">Response success and error codes</span></span>

<span data-ttu-id="30210-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="30210-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="30210-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="30210-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="30210-159">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="30210-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="30210-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="30210-160">Response example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-Contract-Version: v1
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
    "FriendlyName": "nickname",
    "Quantity": 2,
    "UnitType": "none",
    "ParentSubscriptionId": null,
    "CreationDate": "2015-11-25T06:41:12Z",
    "EffectiveStartDate": "2015-11-24T08:00:00Z",
    "CommitmentEndDate": "2016-12-12T08:00:00Z",
    "Status": "suspended",
    "AutoRenewEnabled": false,
    "BillingType": "none",
    "PartnerId": null,
    "ContractType": "subscription",
    "Links": {
        "Offer": {
            "Uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
            "Method": "GET",
            "Headers": []
        },
        "Entitlement": {
            "Uri": "/entitlements?key=<key>",
            "Method": "GET",
            "Headers": []
        },
        "Self": {
            "Uri": "/subscriptions?key=<key>",
            "Method": "GET",
            "Headers": []
        }
    },
    "OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```
