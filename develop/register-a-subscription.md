---
title: Bir aboneliğe kaydolma
description: Mevcut bir aboneliği Azure ayırmalarını sıralamak için etkin olacak şekilde kaydettirin.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9a96bb350f22430c9fd7a1759e336cc9f3ca1939
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769652"
---
# <a name="register-a-subscription"></a><span data-ttu-id="9a987-103">Bir aboneliğe kaydolma</span><span class="sxs-lookup"><span data-stu-id="9a987-103">Register a subscription</span></span>

<span data-ttu-id="9a987-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="9a987-104">**Applies To**</span></span>

- <span data-ttu-id="9a987-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9a987-105">Partner Center</span></span>

<span data-ttu-id="9a987-106">Mevcut bir [aboneliği](subscription-resources.md) Azure ayırmalarını sıralamak için etkin olacak şekilde kaydettirin.</span><span class="sxs-lookup"><span data-stu-id="9a987-106">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="9a987-107">Bir Azure ayırması satın almak için, en az bir tane mevcut CSP Azure aboneliğiniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="9a987-107">To purchase an Azure reservation you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="9a987-108">Bu yöntem, mevcut CSP Azure aboneliğinizi kaydetmenizi sağlar ve bunu Azure ayırmaları satın almak üzere etkinleştirir.</span><span class="sxs-lookup"><span data-stu-id="9a987-108">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9a987-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9a987-109">Prerequisites</span></span>

- <span data-ttu-id="9a987-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9a987-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9a987-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9a987-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9a987-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9a987-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9a987-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9a987-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9a987-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9a987-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9a987-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9a987-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9a987-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="9a987-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9a987-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="9a987-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9a987-118">Abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="9a987-118">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="9a987-119">C\#</span><span class="sxs-lookup"><span data-stu-id="9a987-119">C\#</span></span>

<span data-ttu-id="9a987-120">Müşterinin aboneliğini kaydetmek için, müşteriyi tanımlamak üzere [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) YÖNTEMINI Müşteri kimliğiyle çağırarak abonelik işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="9a987-120">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="9a987-121">Ardından, kaydolduğunuz aboneliği tanımlamak için abonelik KIMLIĞIYLE birlikte [**Subscription. Byıd ()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9a987-121">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="9a987-122">Son olarak, aboneliği kaydetmek ve abonelik kayıt durumunu almak için kullanılabilecek bir URI almak için **kayıt. Register ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9a987-122">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="9a987-123">Daha fazla bilgi için bkz. [abonelik kayıt durumunu Al](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="9a987-123">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="9a987-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9a987-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9a987-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9a987-125">Request syntax</span></span>

| <span data-ttu-id="9a987-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9a987-126">Method</span></span>    | <span data-ttu-id="9a987-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9a987-127">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9a987-128">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="9a987-128">**POST**</span></span>  | <span data-ttu-id="9a987-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/kayıtlar http/1.1</span><span class="sxs-lookup"><span data-stu-id="9a987-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="9a987-130">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="9a987-130">URI parameters</span></span>

<span data-ttu-id="9a987-131">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a987-131">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="9a987-132">Ad</span><span class="sxs-lookup"><span data-stu-id="9a987-132">Name</span></span>                    | <span data-ttu-id="9a987-133">Tür</span><span class="sxs-lookup"><span data-stu-id="9a987-133">Type</span></span>       | <span data-ttu-id="9a987-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9a987-134">Required</span></span> | <span data-ttu-id="9a987-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9a987-135">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="9a987-136">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="9a987-136">customer-id</span></span>             | <span data-ttu-id="9a987-137">string</span><span class="sxs-lookup"><span data-stu-id="9a987-137">string</span></span>     | <span data-ttu-id="9a987-138">Yes</span><span class="sxs-lookup"><span data-stu-id="9a987-138">Yes</span></span>      | <span data-ttu-id="9a987-139">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="9a987-139">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="9a987-140">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="9a987-140">subscription-id</span></span>         | <span data-ttu-id="9a987-141">string</span><span class="sxs-lookup"><span data-stu-id="9a987-141">string</span></span>     | <span data-ttu-id="9a987-142">Yes</span><span class="sxs-lookup"><span data-stu-id="9a987-142">Yes</span></span>      | <span data-ttu-id="9a987-143">Aboneliği tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="9a987-143">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="9a987-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9a987-144">Request headers</span></span>

<span data-ttu-id="9a987-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9a987-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9a987-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9a987-146">Request body</span></span>

<span data-ttu-id="9a987-147">Yok.</span><span class="sxs-lookup"><span data-stu-id="9a987-147">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9a987-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9a987-148">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-id>/subscriptions/<subscription-id>/registrations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 1029
Expect: 100-continue
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="9a987-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9a987-149">REST response</span></span>

<span data-ttu-id="9a987-150">Başarılı olursa, yanıt, abonelik kayıt durumunu almak için kullanılabilecek bir URI içeren bir **konum** üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="9a987-150">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="9a987-151">Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="9a987-151">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="9a987-152">Durumu alma hakkında bir örnek için bkz. [abonelik kayıt durumunu alma](get-subscription-registration-status.md).</span><span class="sxs-lookup"><span data-stu-id="9a987-152">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9a987-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9a987-153">Response success and error codes</span></span>

<span data-ttu-id="9a987-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9a987-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9a987-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9a987-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9a987-156">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9a987-156">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9a987-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9a987-157">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
