---
title: Abonelik sağlama durumunu alma
description: Bir müşteri aboneliği için abonelik sağlama durumunu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f8797fa494cd77f11a1179d6406ca021f0d7788c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548711"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="c88a1-103">Abonelik sağlama durumunu alma</span><span class="sxs-lookup"><span data-stu-id="c88a1-103">Get subscription provisioning status</span></span>

<span data-ttu-id="c88a1-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c88a1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c88a1-105">Bir müşteri aboneliği için abonelik sağlama durumunu alma.</span><span class="sxs-lookup"><span data-stu-id="c88a1-105">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c88a1-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c88a1-106">Prerequisites</span></span>

- <span data-ttu-id="c88a1-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c88a1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c88a1-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c88a1-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c88a1-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="c88a1-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="c88a1-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c88a1-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="c88a1-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="c88a1-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="c88a1-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="c88a1-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="c88a1-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="c88a1-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="c88a1-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="c88a1-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="c88a1-115">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="c88a1-115">A subscription identifier.</span></span>

- <span data-ttu-id="c88a1-116">Bu işlemi gerçekleştirmek için abonelikte yönetici temsilcisi izinleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="c88a1-116">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="c88a1-117">C\#</span><span class="sxs-lookup"><span data-stu-id="c88a1-117">C\#</span></span>

<span data-ttu-id="c88a1-118">Bir aboneliğin sağlama durumunu almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="c88a1-118">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="c88a1-119">Ardından, abonelik KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="c88a1-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="c88a1-120">Ardından, geçerli aboneliğin sağlama durumu işlemlerine bir arabirim almak için [**Provisioningstatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) özelliğini kullanın ve ardından [**subscriptionprovisioningstatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) nesnesini almak Için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c88a1-120">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="c88a1-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c88a1-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c88a1-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c88a1-122">Request syntax</span></span>

| <span data-ttu-id="c88a1-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c88a1-123">Method</span></span>  | <span data-ttu-id="c88a1-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c88a1-124">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c88a1-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="c88a1-125">**GET**</span></span> | <span data-ttu-id="c88a1-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/provisioningstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="c88a1-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="c88a1-127">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="c88a1-127">URI parameters</span></span>

<span data-ttu-id="c88a1-128">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c88a1-128">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="c88a1-129">Ad</span><span class="sxs-lookup"><span data-stu-id="c88a1-129">Name</span></span>            | <span data-ttu-id="c88a1-130">Tür</span><span class="sxs-lookup"><span data-stu-id="c88a1-130">Type</span></span>   | <span data-ttu-id="c88a1-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c88a1-131">Required</span></span> | <span data-ttu-id="c88a1-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c88a1-132">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="c88a1-133">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="c88a1-133">customer-id</span></span>     | <span data-ttu-id="c88a1-134">string</span><span class="sxs-lookup"><span data-stu-id="c88a1-134">string</span></span> | <span data-ttu-id="c88a1-135">Yes</span><span class="sxs-lookup"><span data-stu-id="c88a1-135">Yes</span></span>      | <span data-ttu-id="c88a1-136">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="c88a1-136">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="c88a1-137">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="c88a1-137">subscription-id</span></span> | <span data-ttu-id="c88a1-138">string</span><span class="sxs-lookup"><span data-stu-id="c88a1-138">string</span></span> | <span data-ttu-id="c88a1-139">Yes</span><span class="sxs-lookup"><span data-stu-id="c88a1-139">Yes</span></span>      | <span data-ttu-id="c88a1-140">Aboneliği tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="c88a1-140">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c88a1-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c88a1-141">Request headers</span></span>

<span data-ttu-id="c88a1-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c88a1-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c88a1-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c88a1-143">Request body</span></span>

<span data-ttu-id="c88a1-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="c88a1-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c88a1-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c88a1-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="c88a1-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c88a1-146">REST response</span></span>

<span data-ttu-id="c88a1-147">Başarılı olursa, yanıt gövdesi bir [Subscriptionprovisioningstatus](subscription-resources.md#subscriptionprovisioningstatus) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="c88a1-147">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c88a1-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c88a1-148">Response success and error codes</span></span>

<span data-ttu-id="c88a1-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c88a1-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c88a1-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c88a1-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c88a1-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c88a1-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c88a1-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c88a1-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: InswEQre402koceL.0
MS-ServerId: 030020344
Date: Thu, 20 Apr 2017 19:23:39 GMT

{
    "skuId": "6FD2C87F-B296-42F0-B197-1E91E994B900",
    "status": "success",
    "quantity": 5,
    "endDate": "2018-05-10T00:00:00Z",
    "attributes": {
        "objectType": "SubscriptionProvisioningStatus"
    }
}
```

## <a name="remarks"></a><span data-ttu-id="c88a1-153">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="c88a1-153">Remarks</span></span>

- <span data-ttu-id="c88a1-154">Lisans değişikliği ataması sırasında, [Subscriptionprovisioningstatus](subscription-resources.md#subscriptionprovisioningstatus) içindeki durum alanı "bekliyor" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="c88a1-154">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="c88a1-155">Durum alanı 15 dakikada bir güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="c88a1-155">The status field is updated every 15 minutes.</span></span>
