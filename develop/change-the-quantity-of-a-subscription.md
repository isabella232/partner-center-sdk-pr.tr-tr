---
title: Bir aboneliğin miktarını değiştirme
description: Bir müşteri aboneliği için lisans miktarını değiştirmek üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Bunu Iş Ortağı Merkezi panosunda da yapabilirsiniz.
ms.date: 06/05/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9b781c50895aa3a14819bec43fcca1e931e3b30
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770072"
---
# <a name="change-the-quantity-of-licenses-in-a-customer-subscription"></a><span data-ttu-id="cbbbb-104">Bir müşteri aboneliğinde lisans miktarını değiştirme</span><span class="sxs-lookup"><span data-stu-id="cbbbb-104">Change the quantity of licenses in a customer subscription</span></span>

<span data-ttu-id="cbbbb-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="cbbbb-105">**Applies to:**</span></span>

- <span data-ttu-id="cbbbb-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="cbbbb-106">Partner Center</span></span>
- <span data-ttu-id="cbbbb-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="cbbbb-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="cbbbb-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="cbbbb-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="cbbbb-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="cbbbb-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="cbbbb-110">Lisans miktarını artırmak veya azaltmak için bir [aboneliği](subscription-resources.md) güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-110">Updates a [subscription](subscription-resources.md) to increase or decrease the quantity of licenses.</span></span>

<span data-ttu-id="cbbbb-111">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-111">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="cbbbb-112">Sonra, söz konusu dosyayı yeniden adlandırmak istediğiniz aboneliği seçin.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-112">Then, select the subscription in question that you wish to rename.</span></span> <span data-ttu-id="cbbbb-113">Son olarak, **Miktar** alanındaki değeri değiştirin ve ardından Gönder ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="cbbbb-113">To finish, change the value in the **Quantity** field, then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cbbbb-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cbbbb-114">Prerequisites</span></span>

- <span data-ttu-id="cbbbb-115">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cbbbb-116">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cbbbb-117">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="cbbbb-117">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="cbbbb-118">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-118">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="cbbbb-119">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-119">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="cbbbb-120">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-120">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="cbbbb-121">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-121">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="cbbbb-122">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="cbbbb-122">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="cbbbb-123">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-123">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="cbbbb-124">C\#</span><span class="sxs-lookup"><span data-stu-id="cbbbb-124">C\#</span></span>

<span data-ttu-id="cbbbb-125">Bir müşterinin aboneliğine ait miktarı değiştirmek için önce [aboneliği alın](get-a-subscription-by-id.md), sonra aboneliğin [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) özelliğini değiştirin.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-125">To change the quantity of a customer's subscription, first [get the subscription](get-a-subscription-by-id.md), then change the subscription's [**Quantity**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscription.quantity) property.</span></span> <span data-ttu-id="cbbbb-126">Değişiklik yapıldıktan sonra **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-126">Once the change is made, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="cbbbb-127">Ardından, ve ardından [**Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemiyle [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-127">Then call the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, followed by the [**ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method.</span></span> <span data-ttu-id="cbbbb-128">Ardından, **Patch ()** yöntemini çağırarak son ' u kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-128">Then, finish by calling the **Patch()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var customerId;
// var subscriptionId;

//retrieving the subscription, for the purpose of the sample
ResourceCollection<Subscription> customerSubscriptions = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.Get();
Subscription selectedSubscription = customerSubscriptions.Items.FirstOrDefault(sub => sub.Status == SubscriptionStatus.Active);

//update selected subscription,
selectedSubscription.Quantity++;

var updatedSubscription = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscription.Id).Patch(selectedSubscription);
```

<span data-ttu-id="cbbbb-129">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="cbbbb-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="cbbbb-130">**Proje**: Partnersdk. Featuresample **sınıfı**: UpdateSubscription.cs</span><span class="sxs-lookup"><span data-stu-id="cbbbb-130">**Project**: PartnerSDK.FeatureSample **Class**: UpdateSubscription.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="cbbbb-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="cbbbb-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cbbbb-132">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cbbbb-132">Request syntax</span></span>

| <span data-ttu-id="cbbbb-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="cbbbb-133">Method</span></span>    | <span data-ttu-id="cbbbb-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="cbbbb-134">Request URI</span></span>                                                                                                                |
|-----------|----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cbbbb-135">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="cbbbb-135">**PATCH**</span></span> | <span data-ttu-id="cbbbb-136">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cbbbb-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="cbbbb-137">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="cbbbb-137">URI parameter</span></span>

<span data-ttu-id="cbbbb-138">Bu tabloda, abonelik miktarını değiştirmek için gerekli sorgu parametresi listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-138">This table lists the required query parameter to change the quantity of the subscription.</span></span>

| <span data-ttu-id="cbbbb-139">Ad</span><span class="sxs-lookup"><span data-stu-id="cbbbb-139">Name</span></span>                    | <span data-ttu-id="cbbbb-140">Tür</span><span class="sxs-lookup"><span data-stu-id="cbbbb-140">Type</span></span>     | <span data-ttu-id="cbbbb-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cbbbb-141">Required</span></span> | <span data-ttu-id="cbbbb-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cbbbb-142">Description</span></span>                               |
|-------------------------|----------|----------|-------------------------------------------|
| <span data-ttu-id="cbbbb-143">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="cbbbb-143">**customer-tenant-id**</span></span>  | <span data-ttu-id="cbbbb-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="cbbbb-144">**guid**</span></span> | <span data-ttu-id="cbbbb-145">Y</span><span class="sxs-lookup"><span data-stu-id="cbbbb-145">Y</span></span>        | <span data-ttu-id="cbbbb-146">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-146">A GUID corresponding to the customer.</span></span>     |
| <span data-ttu-id="cbbbb-147">**abonelik kimliği**</span><span class="sxs-lookup"><span data-stu-id="cbbbb-147">**id-for-subscription**</span></span> | <span data-ttu-id="cbbbb-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="cbbbb-148">**guid**</span></span> | <span data-ttu-id="cbbbb-149">Y</span><span class="sxs-lookup"><span data-stu-id="cbbbb-149">Y</span></span>        | <span data-ttu-id="cbbbb-150">Aboneliğe karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-150">A GUID corresponding to the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="cbbbb-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="cbbbb-151">Request headers</span></span>

<span data-ttu-id="cbbbb-152">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cbbbb-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cbbbb-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="cbbbb-153">Request body</span></span>

<span data-ttu-id="cbbbb-154">İstek gövdesinde tam bir **abonelik** kaynağı gereklidir.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-154">A full **Subscription** resource is required in the request body.</span></span> <span data-ttu-id="cbbbb-155">**Quantity** özelliğinin güncelleştirildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-155">Ensure that the **Quantity** property has been updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="cbbbb-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="cbbbb-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="cbbbb-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="cbbbb-157">REST response</span></span>

<span data-ttu-id="cbbbb-158">Başarılı olursa, bu yöntem yanıt gövdesinde bir **http durum 200** durum kodu ve güncelleştirilmiş [abonelik kaynak](subscription-resources.md)  özellikleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-158">If successful, this method returns an **HTTP status 200** status code and updated [subscription resource](subscription-resources.md)  properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cbbbb-159">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="cbbbb-159">Response success and error codes</span></span>

<span data-ttu-id="cbbbb-160">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-160">Each response returns an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cbbbb-161">Durum kodunu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-161">Use a network trace tool to read the status code, error type, and additional parameters.</span></span> <span data-ttu-id="cbbbb-162">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cbbbb-162">For the full list, see [Error Codes](error-codes.md).</span></span>

<span data-ttu-id="cbbbb-163">Düzeltme Eki işlemi beklenen süreden uzun sürerse, Iş ortağı merkezi bir **http durum 202** durum kodu ve aboneliğin nereden alındığını gösteren bir konum üst bilgisi gönderir.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-163">When the patch operation takes longer than the expected time, the Partner Center sends an **HTTP status 202** status code and a location header that points to where to retrieve the subscription.</span></span> <span data-ttu-id="cbbbb-164">Durum ve miktar değişikliklerini izlemek için aboneliği düzenli aralıklarla sorgulayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cbbbb-164">You can query the subscription periodically to monitor the status and quantity changes.</span></span>

### <a name="response-examples"></a><span data-ttu-id="cbbbb-165">Yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="cbbbb-165">Response examples</span></span>

#### <a name="response-example-1"></a><span data-ttu-id="cbbbb-166">Yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="cbbbb-166">Response example 1</span></span>

<span data-ttu-id="cbbbb-167">**Http durumu 200** olan başarılı istek durum kodu:</span><span class="sxs-lookup"><span data-stu-id="cbbbb-167">Successful request with an **HTTP status 200** status code:</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="cbbbb-168">Yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="cbbbb-168">Response example 2</span></span>

<span data-ttu-id="cbbbb-169">**Http durumu 202** olan başarılı istek durum kodu:</span><span class="sxs-lookup"><span data-stu-id="cbbbb-169">Successful request with an **HTTP status 202** status code:</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions/<subscriptionID> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 01880c1b-1966-40f0-d470-501a66d9948b
MS-CorrelationId: 2c5827c1-d5f9-4835-cc6d-f1918b782c79
Content-Type: application/json
Content-Length: 1432
Connection: Keep-Alive
Location: /customers/<customer-tenant-id>/subscriptions/<subscriptionID>
```
