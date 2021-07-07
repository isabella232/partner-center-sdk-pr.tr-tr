---
title: Bir aboneliğe kaydolma
description: Azure rezervasyonlarını sipariş etmek için etkinleştirilmesi için mevcut bir aboneliği kaydetme.
ms.date: 07/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d26a7c77f60e6ef817cde80b9e97c88bd8bdc786
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446624"
---
# <a name="register-a-subscription"></a><span data-ttu-id="70dd9-103">Bir aboneliğe kaydolma</span><span class="sxs-lookup"><span data-stu-id="70dd9-103">Register a subscription</span></span>

<span data-ttu-id="70dd9-104">Azure [rezervasyonlarını sipariş](subscription-resources.md) etmek için etkinleştirilmesi için mevcut bir Aboneliği kaydetme.</span><span class="sxs-lookup"><span data-stu-id="70dd9-104">Register an existing [Subscription](subscription-resources.md) so that it is enabled for ordering Azure reservations.</span></span>

<span data-ttu-id="70dd9-105">Azure rezervasyonu satın almak için en az bir CSP Azure aboneliğinizin olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="70dd9-105">To purchase an Azure reservation, you must have at least one existing CSP Azure subscription.</span></span> <span data-ttu-id="70dd9-106">Bu yöntem, mevcut CSP Azure aboneliğinizi kaydederek Azure rezervasyonları satın almak için etkinleştirmenize olanak sağlar.</span><span class="sxs-lookup"><span data-stu-id="70dd9-106">This method allows you to register your existing CSP Azure subscription, enabling it for purchasing Azure reservations.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="70dd9-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="70dd9-107">Prerequisites</span></span>

- <span data-ttu-id="70dd9-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="70dd9-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="70dd9-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="70dd9-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="70dd9-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="70dd9-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="70dd9-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="70dd9-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="70dd9-112">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="70dd9-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="70dd9-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="70dd9-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="70dd9-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="70dd9-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="70dd9-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="70dd9-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="70dd9-116">Abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="70dd9-116">A subscription ID.</span></span>

## <a name="c"></a><span data-ttu-id="70dd9-117">C\#</span><span class="sxs-lookup"><span data-stu-id="70dd9-117">C\#</span></span>

<span data-ttu-id="70dd9-118">Müşterinin aboneliğini kaydetmek için müşteri kimliğini kullanarak [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="70dd9-118">To register a customer's subscription, retrieve an interface to subscription operations by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="70dd9-119">Ardından, kaydetmekte olduğunu aboneliği tanımlamak için [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) yöntemini abonelik kimliğiyle birlikte çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="70dd9-119">Then, call the [**Subscription.ById()**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.byid) method with the subscription ID to identify the subscription that you are registering.</span></span>

<span data-ttu-id="70dd9-120">Son olarak, aboneliği kaydetmek ve abonelik kayıt durumunu almak için uri'yi almak için **Registration.Register()** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="70dd9-120">Finally, call the **Registration.Register()** method to register the subscription and retrieve a URI that can be used to get the subscription registration status.</span></span> <span data-ttu-id="70dd9-121">Daha fazla bilgi için [bkz. Abonelik kayıt durumunu alma.](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="70dd9-121">For more information, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerId;
// var selectedSubscriptionId;

// Retrieve the subscription registration details.
var subscriptionRegistrationDetails = partnerOperations.Customers.ById(selectedCustomerId).Subscriptions.ById(selectedSubscriptionId).Registration.Register();
```

## <a name="rest-request"></a><span data-ttu-id="70dd9-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="70dd9-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="70dd9-123">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="70dd9-123">Request syntax</span></span>

| <span data-ttu-id="70dd9-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="70dd9-124">Method</span></span>    | <span data-ttu-id="70dd9-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="70dd9-125">Request URI</span></span>                                                                                                                        |
|-----------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="70dd9-126">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="70dd9-126">**POST**</span></span>  | <span data-ttu-id="70dd9-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="70dd9-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="70dd9-128">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="70dd9-128">URI parameters</span></span>

<span data-ttu-id="70dd9-129">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="70dd9-129">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="70dd9-130">Ad</span><span class="sxs-lookup"><span data-stu-id="70dd9-130">Name</span></span>                    | <span data-ttu-id="70dd9-131">Tür</span><span class="sxs-lookup"><span data-stu-id="70dd9-131">Type</span></span>       | <span data-ttu-id="70dd9-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="70dd9-132">Required</span></span> | <span data-ttu-id="70dd9-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="70dd9-133">Description</span></span>                                                   |
|-------------------------|------------|----------|---------------------------------------------------------------|
| <span data-ttu-id="70dd9-134">customer-id</span><span class="sxs-lookup"><span data-stu-id="70dd9-134">customer-id</span></span>             | <span data-ttu-id="70dd9-135">string</span><span class="sxs-lookup"><span data-stu-id="70dd9-135">string</span></span>     | <span data-ttu-id="70dd9-136">Yes</span><span class="sxs-lookup"><span data-stu-id="70dd9-136">Yes</span></span>      | <span data-ttu-id="70dd9-137">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="70dd9-137">A GUID formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="70dd9-138">subscription-id</span><span class="sxs-lookup"><span data-stu-id="70dd9-138">subscription-id</span></span>         | <span data-ttu-id="70dd9-139">string</span><span class="sxs-lookup"><span data-stu-id="70dd9-139">string</span></span>     | <span data-ttu-id="70dd9-140">Yes</span><span class="sxs-lookup"><span data-stu-id="70dd9-140">Yes</span></span>      | <span data-ttu-id="70dd9-141">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="70dd9-141">A GUID formatted string that identifies the subscription.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="70dd9-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="70dd9-142">Request headers</span></span>

<span data-ttu-id="70dd9-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="70dd9-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="70dd9-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="70dd9-144">Request body</span></span>

<span data-ttu-id="70dd9-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="70dd9-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="70dd9-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="70dd9-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="70dd9-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="70dd9-147">REST response</span></span>

<span data-ttu-id="70dd9-148">Başarılı olursa yanıt, abonelik **kayıt durumunu** almak için URI'ye sahip bir Konum üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="70dd9-148">If successful, the response contains a **Location** header with a URI that can be used to retrieve the subscription registration status.</span></span> <span data-ttu-id="70dd9-149">Bu URI'yi diğer ilgili REST API'leriyle kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="70dd9-149">Save this URI for use with other related REST APIs.</span></span> <span data-ttu-id="70dd9-150">Durumu alma örneği için bkz. [Abonelik kayıt durumunu alma.](get-subscription-registration-status.md)</span><span class="sxs-lookup"><span data-stu-id="70dd9-150">For an example of how to retrieve the status, see [Get subscription registration status](get-subscription-registration-status.md).</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="70dd9-151">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="70dd9-151">Response success and error codes</span></span>

<span data-ttu-id="70dd9-152">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="70dd9-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="70dd9-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="70dd9-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="70dd9-154">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="70dd9-154">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="70dd9-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="70dd9-155">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/<customer-id>/subscriptions/<subscription-id>/registrationstatus
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
```
