---
title: Bir abonelik için takma ad güncelleştirme
description: Müşterinin aboneliği için kolay ad veya ad alanı güncelleştirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 57a9fec4b69d4a64128425ea58b4bb84d0d7dd54
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769646"
---
# <a name="update-the-nickname-for-a-subscription"></a><span data-ttu-id="2a55e-103">Bir abonelik için takma ad güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2a55e-103">Update the nickname for a subscription</span></span>

<span data-ttu-id="2a55e-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="2a55e-104">**Applies To**</span></span>

- <span data-ttu-id="2a55e-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2a55e-105">Partner Center</span></span>
- <span data-ttu-id="2a55e-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2a55e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2a55e-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2a55e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2a55e-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2a55e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2a55e-109">Müşterinin [aboneliği](subscription-resources.md)için kolay ad veya ad alanı güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="2a55e-109">Updates the friendly name or nickname for a customer's [Subscription](subscription-resources.md).</span></span> <span data-ttu-id="2a55e-110">Bu ad, müşteri hesabındaki aboneliklerin ayırt edilmesine yardımcı olmak için Iş Ortağı Merkezi 'nde görünür.</span><span class="sxs-lookup"><span data-stu-id="2a55e-110">This name appears in Partner Center to help differentiate the subscriptions in the customer's account.</span></span>

<span data-ttu-id="2a55e-111">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="2a55e-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="2a55e-112">Sonra, söz konusu dosyayı yeniden adlandırmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="2a55e-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="2a55e-113">Son olarak, **abonelik takma ad** alanındaki adı değiştirin ve ardından Gönder ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="2a55e-113">To finish, change the name in the **Subscription nickname** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2a55e-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2a55e-114">Prerequisites</span></span>

- <span data-ttu-id="2a55e-115">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2a55e-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2a55e-116">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2a55e-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2a55e-117">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2a55e-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2a55e-118">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a55e-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2a55e-119">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2a55e-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2a55e-120">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2a55e-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2a55e-121">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="2a55e-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2a55e-122">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="2a55e-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2a55e-123">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="2a55e-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="2a55e-124">C\#</span><span class="sxs-lookup"><span data-stu-id="2a55e-124">C\#</span></span>

<span data-ttu-id="2a55e-125">Müşterinin aboneliğinin takma adını güncelleştirmek için önce [aboneliği alın](get-a-subscription-by-id.md), sonra aboneliğin [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) özelliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="2a55e-125">To update the nickname of a customer's subscription, first [Get the subscription](get-a-subscription-by-id.md), then change the subscription's [**FriendlyName**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.friendlyname) property.</span></span> <span data-ttu-id="2a55e-126">Değişiklik yapıldıktan sonra [**ıpartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2a55e-126">Once the change is made, use your [**IPartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="2a55e-127">Ardından, ve ardından [**Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemiyle [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2a55e-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="2a55e-128">Ardından, [**Patch ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) yöntemini çağırarak son ' u kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2a55e-128">Then, finish by calling the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.patch) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var SelectedcustomerId as string;

ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

// Apply changes to subscription;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="2a55e-129">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2a55e-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2a55e-130">**Proje**: partnersdk. Featuresamples **sınıfı**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="2a55e-130">**Project**: PartnerSDK.FeatureSamples **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2a55e-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2a55e-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2a55e-132">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2a55e-132">Request syntax</span></span>

| <span data-ttu-id="2a55e-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2a55e-133">Method</span></span>    | <span data-ttu-id="2a55e-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2a55e-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2a55e-135">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="2a55e-135">**PATCH**</span></span> | <span data-ttu-id="2a55e-136">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2a55e-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="2a55e-137">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="2a55e-137">URI parameter</span></span>

<span data-ttu-id="2a55e-138">Bu tabloda, abonelik takma adı 'nı güncelleştirmek için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="2a55e-138">This table lists the required query parameter to update the subscription nickname.</span></span>

| <span data-ttu-id="2a55e-139">Ad</span><span class="sxs-lookup"><span data-stu-id="2a55e-139">Name</span></span>                    | <span data-ttu-id="2a55e-140">Tür</span><span class="sxs-lookup"><span data-stu-id="2a55e-140">Type</span></span>     | <span data-ttu-id="2a55e-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2a55e-141">Required</span></span> | <span data-ttu-id="2a55e-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2a55e-142">Description</span></span>                          |
|-------------------------|----------|----------|--------------------------------------|
| <span data-ttu-id="2a55e-143">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="2a55e-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="2a55e-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="2a55e-144">**guid**</span></span> | <span data-ttu-id="2a55e-145">Y</span><span class="sxs-lookup"><span data-stu-id="2a55e-145">Y</span></span>        | <span data-ttu-id="2a55e-146">**Müşteri-Kiracı kimliği** (GUID).</span><span class="sxs-lookup"><span data-stu-id="2a55e-146">The **customer-tenant-id** (a GUID).</span></span> |
| <span data-ttu-id="2a55e-147">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="2a55e-147">**id-for-subscription**</span></span> | <span data-ttu-id="2a55e-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="2a55e-148">**guid**</span></span> | <span data-ttu-id="2a55e-149">Y</span><span class="sxs-lookup"><span data-stu-id="2a55e-149">Y</span></span>        | <span data-ttu-id="2a55e-150">Abonelik KIMLIĞI (GUID).</span><span class="sxs-lookup"><span data-stu-id="2a55e-150">The subscription ID (a GUID).</span></span>        |

### <a name="request-headers"></a><span data-ttu-id="2a55e-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2a55e-151">Request headers</span></span>

<span data-ttu-id="2a55e-152">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2a55e-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2a55e-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2a55e-153">Request body</span></span>

<span data-ttu-id="2a55e-154">İstek gövdesinde tam bir **abonelik** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="2a55e-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="2a55e-155">**FriendlyName** özelliğinin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="2a55e-155">Ensure the **FriendlyName** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="2a55e-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2a55e-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2a55e-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2a55e-157">REST response</span></span>

<span data-ttu-id="2a55e-158">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş [abonelik](subscription-resources.md) kaynak özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="2a55e-158">If successful, this method returns updated [Subscription](subscription-resources.md) resource properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2a55e-159">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2a55e-159">Response success and error codes</span></span>

<span data-ttu-id="2a55e-160">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2a55e-160">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2a55e-161">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2a55e-161">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2a55e-162">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2a55e-162">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2a55e-163">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2a55e-163">Response example</span></span>

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
