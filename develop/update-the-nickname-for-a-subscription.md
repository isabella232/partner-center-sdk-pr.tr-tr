---
title: Bir abonelik için takma ad güncelleştirme
description: Müşterinin aboneliği için kolay ad veya ad alanı güncelleştirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 195a85fcf29b3e4c9fe0e578d4d8cb80ca068c40
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530013"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="9743a-103">Bir abonelik için takma ad güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9743a-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="9743a-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9743a-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9743a-105">Müşterinin [aboneliği](subscription-resources.md)için kolay ad veya ad alanı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="9743a-105">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="9743a-106">Bu ad, müşteri hesabındaki aboneliklerin ayırt edilmesine yardımcı olmak için Iş Ortağı Merkezi 'nde görünür.</span><span class="sxs-lookup"><span data-stu-id="9743a-106">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="9743a-107">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="9743a-107">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="9743a-108">Sonra, söz konusu dosyayı yeniden adlandırmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="9743a-108">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="9743a-109">Son olarak, **abonelik takma ad** alanındaki adı değiştirin ve ardından Gönder ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="9743a-109">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9743a-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9743a-110">Prerequisites</span></span>

- <span data-ttu-id="9743a-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9743a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9743a-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9743a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9743a-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9743a-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9743a-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9743a-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9743a-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9743a-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9743a-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9743a-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9743a-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="9743a-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9743a-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="9743a-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9743a-119">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="9743a-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="9743a-120">C\#</span><span class="sxs-lookup"><span data-stu-id="9743a-120">C\#</span></span>

<span data-ttu-id="9743a-121">Müşterinin aboneliğinin takma adını güncelleştirmek için önce [aboneliği alın](get-a-subscription-by-id.md), sonra aboneliğin [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) özelliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="9743a-121">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="9743a-122">Değişiklik yapıldıktan sonra [**ıpartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9743a-122">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="9743a-123">Ardından, ve ardından [**Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemiyle [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9743a-123">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="9743a-124">Ardından, [**Patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) yöntemini çağırarak son ' u kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9743a-124">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="9743a-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9743a-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9743a-126">**Project**: partnersdk. featuresamples **sınıfı**: updatesubscription. cs</span><span class="sxs-lookup"><span data-stu-id="9743a-126">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9743a-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9743a-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9743a-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9743a-128">Request syntax</span></span>

| <span data-ttu-id="9743a-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9743a-129">Method</span></span>    | <span data-ttu-id="9743a-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9743a-130">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9743a-131">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="9743a-131">**PATCH**</span></span> | <span data-ttu-id="9743a-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="9743a-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="9743a-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="9743a-133">URI parameter</span></span>

<span data-ttu-id="9743a-134">Bu tabloda, abonelik takma adı 'nı güncelleştirmek için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="9743a-134">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="9743a-135">Ad</span><span class="sxs-lookup"><span data-stu-id="9743a-135">Name</span></span>                    | <span data-ttu-id="9743a-136">Tür</span><span class="sxs-lookup"><span data-stu-id="9743a-136">Type</span></span>     | <span data-ttu-id="9743a-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9743a-137">Required</span></span> | <span data-ttu-id="9743a-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9743a-138">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="9743a-139">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="9743a-139">**customer-tenant-id**</span></span>  | <span data-ttu-id="9743a-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="9743a-140">**guid**</span></span> | <span data-ttu-id="9743a-141">Y</span><span class="sxs-lookup"><span data-stu-id="9743a-141">Y</span></span>        | <span data-ttu-id="9743a-142">**Müşteri-Kiracı kimliği** (GUID).</span><span class="sxs-lookup"><span data-stu-id="9743a-142">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="9743a-143">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="9743a-143">**id-for-subscription**</span></span> | <span data-ttu-id="9743a-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="9743a-144">**guid**</span></span> | <span data-ttu-id="9743a-145">Y</span><span class="sxs-lookup"><span data-stu-id="9743a-145">Y</span></span>        | <span data-ttu-id="9743a-146">Abonelik KIMLIĞI (GUID).</span><span class="sxs-lookup"><span data-stu-id="9743a-146">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="9743a-147">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9743a-147">Request headers</span></span>

<span data-ttu-id="9743a-148">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9743a-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9743a-149">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9743a-149">Request body</span></span>

<span data-ttu-id="9743a-150">İstek gövdesinde tam bir **abonelik** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="9743a-150">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="9743a-151">**FriendlyName** özelliğinin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="9743a-151">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="9743a-152">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9743a-152">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3831
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105f2c
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive

{
    "Id": "<subscriptionID>",
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
    OrderId": "6183db3d-6318-4e52-877e-25806e4971be",
    "Attributes": {
        "Etag": "<etag>",
        "ObjectType": "Subscription"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="9743a-153">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9743a-153">REST response</span></span>

<span data-ttu-id="9743a-154">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [abonelik](subscription-resources.md) kaynak özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="9743a-154">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9743a-155">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9743a-155">Response success and error codes</span></span>

<span data-ttu-id="9743a-156">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9743a-156">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9743a-157">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9743a-157">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9743a-158">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9743a-158">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9743a-159">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9743a-159">Response example</span></span>

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
    "Id": "<subscriptionID>",
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
