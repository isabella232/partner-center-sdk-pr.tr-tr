---
title: Askıya alınmış bir aboneliği yeniden etkinleştirme
description: Daha önce ödemesiz ödeme için askıya alınmış bir Aboneliği yeniden etkinleştirdi. Bu İş Ortağı Merkezi, önce bir müşteri seçerek gerçekleştirebilirsiniz.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c2b6e3574119f9c645cc3f730047d2a23484ad8a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547725"
---
# <a name="reactivate-a-suspended-subscription"></a><span data-ttu-id="fb5d7-104">Askıya alınmış bir aboneliği yeniden etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="fb5d7-104">Reactivate a suspended subscription</span></span>

<span data-ttu-id="fb5d7-105">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="fb5d7-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="fb5d7-106">Daha önce [ödemesiz ödeme](subscription-resources.md) için askıya alınmış bir Aboneliği yeniden etkinleştirdi.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-106">Reactivates a [Subscription](subscription-resources.md) that was previously suspended for nonpayment.</span></span>

<span data-ttu-id="fb5d7-107">Bu İş Ortağı Merkezi önce bir müşteri [seçerek gerçekleştirebilirsiniz.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="fb5d7-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="fb5d7-108">Ardından, söz konusu aboneliği yeniden adlandırmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="fb5d7-109">Son olarak Etkin düğmesini **ve** ardından Gönder'i **seçin.**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-109">To finish, choose the **Active** button, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fb5d7-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fb5d7-110">Prerequisites</span></span>

- <span data-ttu-id="fb5d7-111">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="fb5d7-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="fb5d7-112">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="fb5d7-113">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="fb5d7-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="fb5d7-114">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="fb5d7-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="fb5d7-115">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="fb5d7-116">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="fb5d7-117">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="fb5d7-118">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="fb5d7-119">Abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="fb5d7-120">C\#</span><span class="sxs-lookup"><span data-stu-id="fb5d7-120">C\#</span></span>

<span data-ttu-id="fb5d7-121">Müşterinin aboneliğini yeniden etkinleştirmek için önce [Aboneliği alın,](get-a-subscription-by-id.md)ardından aboneliğin Status özelliğini [**değiştirmeniz**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-121">To reactivate a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Status**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.status) property.</span></span> <span data-ttu-id="fb5d7-122">Durum kodları hakkında **bilgi** için [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus) makalesine bakın.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-122">For information on **Status** codes, consult [SubscriptionStatus enumeration/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionstatus).</span></span> <span data-ttu-id="fb5d7-123">Değişiklik yapıldıktan sonra [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonu kullanın ve [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) arayın.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-123">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="fb5d7-124">Ardından [**Subscriptions özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) ve ardından [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-124">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="fb5d7-125">Ardından Patch() yöntemini [**çağırarak bitirin.**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch)</span><span class="sxs-lookup"><span data-stu-id="fb5d7-125">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IPartner partnerOperations;
// var selectedCustomer as Customer;
// var selectedSubscription as Subscription;

updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(
   new Subscription()
   {
      Status = SubscriptionStatus.Active
   });

```

<span data-ttu-id="fb5d7-126">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="fb5d7-126">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="fb5d7-127">**Project:** FeatureSamplesApplication.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-127">**Project**: FeatureSamplesApplication.</span></span> <span data-ttu-id="fb5d7-128">**Sınıf:** UpdateSubscription</span><span class="sxs-lookup"><span data-stu-id="fb5d7-128">**Class**: UpdateSubscription</span></span>

## <a name="rest-request"></a><span data-ttu-id="fb5d7-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="fb5d7-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="fb5d7-130">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="fb5d7-130">Request syntax</span></span>

| <span data-ttu-id="fb5d7-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="fb5d7-131">Method</span></span>    | <span data-ttu-id="fb5d7-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="fb5d7-132">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="fb5d7-133">**Yama**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-133">**PATCH**</span></span> | <span data-ttu-id="fb5d7-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="fb5d7-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="fb5d7-135">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="fb5d7-135">URI parameter</span></span>

<span data-ttu-id="fb5d7-136">Bu tabloda aboneliği yeniden etkinleştirmek için gereken sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-136">This table lists the required query parameter to reactivate the subscription.</span></span>

| <span data-ttu-id="fb5d7-137">Ad</span><span class="sxs-lookup"><span data-stu-id="fb5d7-137">Name</span></span>                    | <span data-ttu-id="fb5d7-138">Tür</span><span class="sxs-lookup"><span data-stu-id="fb5d7-138">Type</span></span>     | <span data-ttu-id="fb5d7-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="fb5d7-139">Required</span></span> | <span data-ttu-id="fb5d7-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="fb5d7-140">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="fb5d7-141">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-141">**customer-tenant-id**</span></span>  | <span data-ttu-id="fb5d7-142">**guid**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-142">**guid**</span></span> | <span data-ttu-id="fb5d7-143">Y</span><span class="sxs-lookup"><span data-stu-id="fb5d7-143">Y</span></span>        | <span data-ttu-id="fb5d7-144">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-144">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="fb5d7-145">**abonelik için id**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-145">**id-for-subscription**</span></span> | <span data-ttu-id="fb5d7-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="fb5d7-146">**guid**</span></span> | <span data-ttu-id="fb5d7-147">Y</span><span class="sxs-lookup"><span data-stu-id="fb5d7-147">Y</span></span>        | <span data-ttu-id="fb5d7-148">Aboneliğe karşılık gelen BIR GUID.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-148">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="fb5d7-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="fb5d7-149">Request headers</span></span>

<span data-ttu-id="fb5d7-150">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="fb5d7-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="fb5d7-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="fb5d7-151">Request body</span></span>

<span data-ttu-id="fb5d7-152">İstek **gövdesinde** tam bir Abonelik kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-152">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="fb5d7-153">Status özelliğinin **güncelleştirilmiş** olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-153">Ensure that the **Status** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="fb5d7-154">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="fb5d7-154">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<id-for-subscription> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
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
    "Status": "active",
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

## <a name="rest-response"></a><span data-ttu-id="fb5d7-155">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="fb5d7-155">REST response</span></span>

<span data-ttu-id="fb5d7-156">Başarılı olursa, bu yöntem yanıt [gövdesinde](subscription-resources.md) güncelleştirilmiş Abonelik kaynağı özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-156">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="fb5d7-157">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="fb5d7-157">Response success and error codes</span></span>

<span data-ttu-id="fb5d7-158">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="fb5d7-159">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="fb5d7-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="fb5d7-160">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="fb5d7-160">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="fb5d7-161">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="fb5d7-161">Response example</span></span>

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
    "Status": "active",
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
