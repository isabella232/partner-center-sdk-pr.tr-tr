---
title: Bir aboneliği askıya alma
description: Sahtekarlık veya ödeme dışı nedenlerle müşteri ve abonelik KIMLIĞIYLE eşleşen bir abonelik kaynağını askıya alır. Iş Ortağı Merkezi panosunda, bu işlem önce bir müşteri seçilerek gerçekleştirilebilir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f351c87efe2bdc810a66c64a9d01b7d376f8a6e3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769598"
---
# <a name="suspend-a-subscription"></a><span data-ttu-id="d500d-103">Bir aboneliği askıya alma</span><span class="sxs-lookup"><span data-stu-id="d500d-103">Suspend a subscription</span></span>

<span data-ttu-id="d500d-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="d500d-104">**Applies To**</span></span>

- <span data-ttu-id="d500d-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d500d-105">Partner Center</span></span>
- <span data-ttu-id="d500d-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d500d-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="d500d-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d500d-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="d500d-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d500d-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d500d-109">Sahtekarlık veya ödeme dışı nedenlerle müşteri ve abonelik KIMLIĞIYLE eşleşen bir [abonelik](subscription-resources.md) kaynağını askıya alır.</span><span class="sxs-lookup"><span data-stu-id="d500d-109">Suspends a [Subscription](subscription-resources.md) resource that matches the customer and subscription ID due to fraud or non-payment.</span></span>

<span data-ttu-id="d500d-110">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d500d-110">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="d500d-111">Sonra, söz konusu dosyayı yeniden adlandırmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="d500d-111">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="d500d-112">Son olarak, **askıya alındı** düğmesini seçin ve ardından Gönder ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="d500d-112">To finish, choose the **Suspended** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d500d-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d500d-113">Prerequisites</span></span>

- <span data-ttu-id="d500d-114">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d500d-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d500d-115">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="d500d-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d500d-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d500d-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d500d-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d500d-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d500d-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="d500d-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d500d-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d500d-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d500d-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="d500d-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d500d-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="d500d-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d500d-122">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="d500d-122">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="d500d-123">C\#</span><span class="sxs-lookup"><span data-stu-id="d500d-123">C\#</span></span>

<span data-ttu-id="d500d-124">Bir müşterinin aboneliğini askıya almak için önce [aboneliği alın](get-a-subscription-by-id.md), sonra aboneliğin [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) özelliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="d500d-124">To suspend a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="d500d-125">**Durum** kodları hakkında bilgi için bkz. [subscriptionstatus Enumeration/DotNet/api/Microsoft. Store. partnercenter. modeller. abonelikler. subscriptionstatus).</span><span class="sxs-lookup"><span data-stu-id="d500d-125">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="d500d-126">Değişiklik yapıldıktan sonra **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d500d-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="d500d-127">Ardından, ve ardından [**Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemiyle [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d500d-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="d500d-128">Ardından, **Patch ()** yöntemini çağırarak son ' u kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d500d-128">Then, finish by calling the **Patch()** method.</span></span>

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

<span data-ttu-id="d500d-129">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d500d-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d500d-130">**Proje**: Partnersdk. Featuresample **sınıfı**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="d500d-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d500d-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d500d-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d500d-132">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d500d-132">Request syntax</span></span>

| <span data-ttu-id="d500d-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d500d-133">Method</span></span>    | <span data-ttu-id="d500d-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d500d-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d500d-135">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="d500d-135">**PATCH**</span></span> | <span data-ttu-id="d500d-136">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d500d-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d500d-137">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d500d-137">URI parameter</span></span>

<span data-ttu-id="d500d-138">Bu tabloda, aboneliği askıya almak için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="d500d-138">This table lists the required query parameter to suspend the subscription.</span></span>

| <span data-ttu-id="d500d-139">Ad</span><span class="sxs-lookup"><span data-stu-id="d500d-139">Name</span></span>                    | <span data-ttu-id="d500d-140">Tür</span><span class="sxs-lookup"><span data-stu-id="d500d-140">Type</span></span>     | <span data-ttu-id="d500d-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d500d-141">Required</span></span> | <span data-ttu-id="d500d-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d500d-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="d500d-143">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="d500d-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="d500d-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="d500d-144">**guid**</span></span> | <span data-ttu-id="d500d-145">Y</span><span class="sxs-lookup"><span data-stu-id="d500d-145">Y</span></span>        | <span data-ttu-id="d500d-146">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="d500d-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="d500d-147">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="d500d-147">**id-for-subscription**</span></span> | <span data-ttu-id="d500d-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="d500d-148">**guid**</span></span> | <span data-ttu-id="d500d-149">Y</span><span class="sxs-lookup"><span data-stu-id="d500d-149">Y</span></span>        | <span data-ttu-id="d500d-150">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="d500d-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d500d-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d500d-151">Request headers</span></span>

<span data-ttu-id="d500d-152">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d500d-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d500d-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d500d-153">Request body</span></span>

<span data-ttu-id="d500d-154">İstek gövdesinde tam bir **abonelik** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="d500d-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="d500d-155">**Status** özelliğinin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="d500d-155">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="d500d-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d500d-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d500d-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d500d-157">REST response</span></span>

<span data-ttu-id="d500d-158">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [abonelik](subscription-resources.md) kaynak özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="d500d-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d500d-159">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d500d-159">Response success and error codes</span></span>

<span data-ttu-id="d500d-160">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="d500d-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d500d-161">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d500d-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d500d-162">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d500d-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d500d-163">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d500d-163">Response example</span></span>

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
