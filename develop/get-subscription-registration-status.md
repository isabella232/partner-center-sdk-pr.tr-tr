---
title: Abonelik kayıt durumunu alma
description: Azure ayrılmış VM örnekleri ile kullanılmak üzere kaydedilmiş bir aboneliğin durumunu alın.
ms.date: 03/19/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e06cf8a450d6c281f7f83a68c899d1e5b29e9855
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769850"
---
# <a name="get-subscription-registration-status"></a><span data-ttu-id="b0e38-103">Abonelik kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="b0e38-103">Get subscription registration status</span></span>

<span data-ttu-id="b0e38-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="b0e38-104">**Applies To**</span></span>

- <span data-ttu-id="b0e38-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b0e38-105">Partner Center</span></span>

<span data-ttu-id="b0e38-106">Azure ayrılmış VM örnekleri satın alma için etkinleştirilen bir müşteri aboneliğinin abonelik kayıt durumunu alma.</span><span class="sxs-lookup"><span data-stu-id="b0e38-106">How to get the subscription registration status for a customer subscription that has been enabled for purchasing Azure Reserved VM Instances.</span></span>

<span data-ttu-id="b0e38-107">Iş Ortağı Merkezi API 'sini kullanarak bir Azure ayrılmış VM örneği satın almak için, en az bir tane mevcut CSP Azure aboneliğiniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="b0e38-107">To purchase an Azure Reserved VM Instance using the Partner Center API, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="b0e38-108">[Abonelik kaydetme](register-a-subscription.md) yöntemi, mevcut CSP Azure aboneliğinizi kaydetmenizi sağlar ve bunu Azure ayrılmış VM örnekleri satın almak üzere etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="b0e38-108">The [Register a subscription](register-a-subscription.md) method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure Reserved VM Instances.</span></span> <span data-ttu-id="b0e38-109">Bu yöntem, bu kaydın durumunu almanızı sağlar.</span><span class="sxs-lookup"><span data-stu-id="b0e38-109">This method allows you to retrieve the status of that registration.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b0e38-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b0e38-110">Prerequisites</span></span>

- <span data-ttu-id="b0e38-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b0e38-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b0e38-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="b0e38-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b0e38-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="b0e38-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="b0e38-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b0e38-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="b0e38-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="b0e38-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="b0e38-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="b0e38-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="b0e38-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="b0e38-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="b0e38-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="b0e38-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="b0e38-119">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="b0e38-119">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="b0e38-120">C\#</span><span class="sxs-lookup"><span data-stu-id="b0e38-120">C\#</span></span>

<span data-ttu-id="b0e38-121">Bir aboneliğin kayıt durumunu almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="b0e38-121">To get the registration status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="b0e38-122">Ardından, aboneliği tanımlamak için abonelik KIMLIĞIYLE birlikte Subscription [**. Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemini çağırarak abonelik işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="b0e38-122">Then, get an interface to subscription operations by calling the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription.</span></span> <span data-ttu-id="b0e38-123">Ardından, geçerli aboneliğin kayıt durumu işlemlerine bir arabirim almak için RegistrationStatus özelliğini kullanın ve **Subscriptionregistrationstatus** nesnesini almak için **Get** veya **GetAsync** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="b0e38-123">Next, use the RegistrationStatus property to obtain an interface to the current subscription's registration status operations, and call the **Get** or **GetAsync** method to retrieve the **SubscriptionRegistrationStatus** object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve a subscription's registration status details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).RegistrationStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="b0e38-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="b0e38-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b0e38-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b0e38-125">Request syntax</span></span>

| <span data-ttu-id="b0e38-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="b0e38-126">Method</span></span>    | <span data-ttu-id="b0e38-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="b0e38-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b0e38-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="b0e38-128">**GET**</span></span>  | <span data-ttu-id="b0e38-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/registrationstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="b0e38-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrationstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="b0e38-130">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="b0e38-130">URI parameters</span></span>

<span data-ttu-id="b0e38-131">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0e38-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="b0e38-132">Ad</span><span class="sxs-lookup"><span data-stu-id="b0e38-132">Name</span></span>                    | <span data-ttu-id="b0e38-133">Tür</span><span class="sxs-lookup"><span data-stu-id="b0e38-133">Type</span></span>       | <span data-ttu-id="b0e38-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b0e38-134">Required</span></span> | <span data-ttu-id="b0e38-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b0e38-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="b0e38-136">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="b0e38-136">customer-id</span></span>             | <span data-ttu-id="b0e38-137">string</span><span class="sxs-lookup"><span data-stu-id="b0e38-137">string</span></span>     | <span data-ttu-id="b0e38-138">Yes</span><span class="sxs-lookup"><span data-stu-id="b0e38-138">Yes</span></span>      | <span data-ttu-id="b0e38-139">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="b0e38-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="b0e38-140">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="b0e38-140">subscription-id</span></span>         | <span data-ttu-id="b0e38-141">string</span><span class="sxs-lookup"><span data-stu-id="b0e38-141">string</span></span>     | <span data-ttu-id="b0e38-142">Yes</span><span class="sxs-lookup"><span data-stu-id="b0e38-142">Yes</span></span>      | <span data-ttu-id="b0e38-143">Aboneliği tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="b0e38-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="b0e38-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="b0e38-144">Request headers</span></span>

<span data-ttu-id="b0e38-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b0e38-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b0e38-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="b0e38-146">Request body</span></span>

<span data-ttu-id="b0e38-147">Yok.</span><span class="sxs-lookup"><span data-stu-id="b0e38-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b0e38-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="b0e38-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="b0e38-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="b0e38-149">REST response</span></span>

<span data-ttu-id="b0e38-150">Başarılı olursa, yanıt gövdesi bir [Subscriptionregistrationstatus](subscription-resources.md#subscriptionregistrationstatus) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="b0e38-150">If successful, the response body contains a [SubscriptionRegistrationStatus](subscription-resources.md#subscriptionregistrationstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b0e38-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="b0e38-151">Response success and error codes</span></span>

<span data-ttu-id="b0e38-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="b0e38-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b0e38-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b0e38-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b0e38-154">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b0e38-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b0e38-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="b0e38-155">Response example</span></span>

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
