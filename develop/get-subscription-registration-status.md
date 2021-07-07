---
title: Abonelik kayıt durumunu alma
description: Azure ayrılmış VM örnekleri ile kullanılmak üzere kaydedilmiş bir aboneliğin durumunu alın.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9e39f94c0eac402a0be3afde84279aa637868f96
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445961"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="252ab-103">Abonelik kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="252ab-103">Get subscription registration status</span></span>

<span data-ttu-id="252ab-104">Azure ayrılmış VM örnekleri satın alma için etkinleştirilen bir müşteri aboneliğinin abonelik kayıt durumunu alma.</span><span class="sxs-lookup"><span data-stu-id="252ab-104">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="252ab-105">Iş Ortağı Merkezi API 'sini kullanarak bir Azure ayrılmış VM örneği satın almak için, en az bir tane mevcut CSP Azure aboneliğiniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="252ab-105">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="252ab-106">[Abonelik kaydetme](register-a-subscription.md) yöntemi, mevcut CSP Azure aboneliğinizi kaydetmenizi sağlar ve bunu Azure ayrılmış VM örnekleri satın almak üzere etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="252ab-106">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="252ab-107">Bu yöntem, bu kaydın durumunu almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="252ab-107">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="252ab-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="252ab-108">Prerequisites</span></span>

- <span data-ttu-id="252ab-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="252ab-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="252ab-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="252ab-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="252ab-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="252ab-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="252ab-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="252ab-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="252ab-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="252ab-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="252ab-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="252ab-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="252ab-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="252ab-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="252ab-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="252ab-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="252ab-117">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="252ab-117">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="252ab-118">C\#</span><span class="sxs-lookup"><span data-stu-id="252ab-118">C\#</span></span>

<span data-ttu-id="252ab-119">Bir aboneliğin kayıt durumunu almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="252ab-119">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="252ab-120">Ardından, aboneliği tanımlamak için abonelik KIMLIĞIYLE birlikte Subscription [**. Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemini çağırarak abonelik işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="252ab-120">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="252ab-121">Ardından, geçerli aboneliğin kayıt durumu işlemlerine bir arabirim almak için RegistrationStatus özelliğini kullanın ve **Subscriptionregistrationstatus** nesnesini almak için **Get** veya **GetAsync** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="252ab-121">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="252ab-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="252ab-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="252ab-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="252ab-123">Request syntax</span></span>

| <span data-ttu-id="252ab-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="252ab-124">Method</span></span>    | <span data-ttu-id="252ab-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="252ab-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="252ab-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="252ab-126">**GET**</span></span>  | <span data-ttu-id="252ab-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/registrationstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="252ab-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="252ab-128">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="252ab-128">URI parameters</span></span>

<span data-ttu-id="252ab-129">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="252ab-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="252ab-130">Ad</span><span class="sxs-lookup"><span data-stu-id="252ab-130">Name</span></span>                    | <span data-ttu-id="252ab-131">Tür</span><span class="sxs-lookup"><span data-stu-id="252ab-131">Type</span></span>       | <span data-ttu-id="252ab-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="252ab-132">Required</span></span> | <span data-ttu-id="252ab-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="252ab-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="252ab-134">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="252ab-134">customer-id</span></span>             | <span data-ttu-id="252ab-135">string</span><span class="sxs-lookup"><span data-stu-id="252ab-135">string</span></span>     | <span data-ttu-id="252ab-136">Yes</span><span class="sxs-lookup"><span data-stu-id="252ab-136">Yes</span></span>      | <span data-ttu-id="252ab-137">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="252ab-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="252ab-138">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="252ab-138">subscription-id</span></span>         | <span data-ttu-id="252ab-139">string</span><span class="sxs-lookup"><span data-stu-id="252ab-139">string</span></span>     | <span data-ttu-id="252ab-140">Yes</span><span class="sxs-lookup"><span data-stu-id="252ab-140">Yes</span></span>      | <span data-ttu-id="252ab-141">Aboneliği tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="252ab-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="252ab-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="252ab-142">Request headers</span></span>

<span data-ttu-id="252ab-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="252ab-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="252ab-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="252ab-144">Request body</span></span>

<span data-ttu-id="252ab-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="252ab-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="252ab-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="252ab-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="252ab-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="252ab-147">REST response</span></span>

<span data-ttu-id="252ab-148">Başarılı olursa, yanıt gövdesi bir [Subscriptionregistrationstatus](subscription-resources.md#subscriptionregistrationstatus) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="252ab-148">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="252ab-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="252ab-149">Response success and error codes</span></span>

<span data-ttu-id="252ab-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="252ab-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="252ab-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="252ab-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="252ab-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="252ab-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="252ab-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="252ab-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344

{
    "subscriptionId":"<subscription-id>",
    "status":"NotRegistered",
    "attributes":{
        "objectType":"SubscriptionRegistrationStatus"
    }
}
```
