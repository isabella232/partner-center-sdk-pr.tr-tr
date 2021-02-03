---
title: Abonelik sağlama durumunu alma
description: Bir müşteri aboneliği için abonelik sağlama durumunu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38544aa380ba0a6a8804ae45f7d8ae7cb431d3ba
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769844"
---
# <a name="get-subscription-provisioning-status"></a><span data-ttu-id="8cd9e-103">Abonelik sağlama durumunu alma</span><span class="sxs-lookup"><span data-stu-id="8cd9e-103">Get subscription provisioning status</span></span>

<span data-ttu-id="8cd9e-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="8cd9e-104">**Applies To**</span></span>

- <span data-ttu-id="8cd9e-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8cd9e-105">Partner Center</span></span>
- <span data-ttu-id="8cd9e-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8cd9e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="8cd9e-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8cd9e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="8cd9e-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8cd9e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8cd9e-109">Bir müşteri aboneliği için abonelik sağlama durumunu alma.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-109">How to get the subscription provisioning status for a customer subscription.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cd9e-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8cd9e-110">Prerequisites</span></span>

- <span data-ttu-id="8cd9e-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8cd9e-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8cd9e-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="8cd9e-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="8cd9e-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="8cd9e-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="8cd9e-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="8cd9e-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="8cd9e-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="8cd9e-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="8cd9e-119">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-119">A subscription identifier.</span></span>

- <span data-ttu-id="8cd9e-120">Bu işlemi gerçekleştirmek için abonelikte yönetici temsilcisi izinleri gereklidir.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-120">Delegated admin permissions on the subscription are required to perform this operation.</span></span>

## <a name="c"></a><span data-ttu-id="8cd9e-121">C\#</span><span class="sxs-lookup"><span data-stu-id="8cd9e-121">C\#</span></span>

<span data-ttu-id="8cd9e-122">Bir aboneliğin sağlama durumunu almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-122">To get the provisioning status of a subscription, begin by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="8cd9e-123">Ardından, abonelik KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırarak abonelik işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-123">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the subscription ID.</span></span> <span data-ttu-id="8cd9e-124">Ardından, geçerli aboneliğin sağlama durumu işlemlerine bir arabirim almak için [**Provisioningstatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) özelliğini kullanın ve ardından [**subscriptionprovisioningstatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) nesnesini almak Için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-124">Next, use the [**ProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.provisioningstatus) property to obtain an interface to the current subscription's provisioning status operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionprovisioningstatus.getasync) method to retrieve the [**SubscriptionProvisioningStatus**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.subscriptionprovisioningstatus) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations.
// string customerId;
// string subscriptionId;

// Retrieve a subscription's provisioning status.
var provisioningStatus = partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionID).ProvisioningStatus.Get();
```

## <a name="rest-request"></a><span data-ttu-id="8cd9e-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8cd9e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8cd9e-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8cd9e-126">Request syntax</span></span>

| <span data-ttu-id="8cd9e-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8cd9e-127">Method</span></span>  | <span data-ttu-id="8cd9e-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8cd9e-128">Request URI</span></span>                                                                                                                        |
|---------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="8cd9e-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="8cd9e-129">**GET**</span></span> | <span data-ttu-id="8cd9e-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/provisioningstatus http/1.1</span><span class="sxs-lookup"><span data-stu-id="8cd9e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/provisioningstatus HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="8cd9e-131">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="8cd9e-131">URI parameters</span></span>

<span data-ttu-id="8cd9e-132">Müşteriyi ve aboneliği tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-132">Use the following path parameters to identify the customer and subscription.</span></span>

| <span data-ttu-id="8cd9e-133">Ad</span><span class="sxs-lookup"><span data-stu-id="8cd9e-133">Name</span></span>            | <span data-ttu-id="8cd9e-134">Tür</span><span class="sxs-lookup"><span data-stu-id="8cd9e-134">Type</span></span>   | <span data-ttu-id="8cd9e-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="8cd9e-135">Required</span></span> | <span data-ttu-id="8cd9e-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="8cd9e-136">Description</span></span>                                               |
|-----------------|--------|----------|-----------------------------------------------------------|
| <span data-ttu-id="8cd9e-137">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="8cd9e-137">customer-id</span></span>     | <span data-ttu-id="8cd9e-138">string</span><span class="sxs-lookup"><span data-stu-id="8cd9e-138">string</span></span> | <span data-ttu-id="8cd9e-139">Yes</span><span class="sxs-lookup"><span data-stu-id="8cd9e-139">Yes</span></span>      | <span data-ttu-id="8cd9e-140">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-140">A GUID formatted string that identifies the customer.</span></span>     |
| <span data-ttu-id="8cd9e-141">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="8cd9e-141">subscription-id</span></span> | <span data-ttu-id="8cd9e-142">string</span><span class="sxs-lookup"><span data-stu-id="8cd9e-142">string</span></span> | <span data-ttu-id="8cd9e-143">Yes</span><span class="sxs-lookup"><span data-stu-id="8cd9e-143">Yes</span></span>      | <span data-ttu-id="8cd9e-144">Aboneliği tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-144">A GUID formatted string that identifies the subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8cd9e-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8cd9e-145">Request headers</span></span>

<span data-ttu-id="8cd9e-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8cd9e-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8cd9e-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="8cd9e-147">Request body</span></span>

<span data-ttu-id="8cd9e-148">Yok.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-148">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8cd9e-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8cd9e-149">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/34828C05-C16C-4D6F-9CFC-4D2650EF19A1/provisioningstatus HTTP/1.1
Accept: application/json, text/plain, */*
Authorization: Bearer <token>
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="8cd9e-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8cd9e-150">REST response</span></span>

<span data-ttu-id="8cd9e-151">Başarılı olursa, yanıt gövdesi bir [Subscriptionprovisioningstatus](subscription-resources.md#subscriptionprovisioningstatus) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-151">If successful, the response body contains a [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8cd9e-152">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8cd9e-152">Response success and error codes</span></span>

<span data-ttu-id="8cd9e-153">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-153">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8cd9e-154">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-154">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8cd9e-155">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8cd9e-155">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8cd9e-156">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="8cd9e-156">Response example</span></span>

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

## <a name="remarks"></a><span data-ttu-id="8cd9e-157">Açıklamalar</span><span class="sxs-lookup"><span data-stu-id="8cd9e-157">Remarks</span></span>

- <span data-ttu-id="8cd9e-158">Lisans değişikliği ataması sırasında, [Subscriptionprovisioningstatus](subscription-resources.md#subscriptionprovisioningstatus) içindeki durum alanı "bekliyor" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-158">During a license change assignment, the status field in [SubscriptionProvisioningStatus](subscription-resources.md#subscriptionprovisioningstatus) is set to "pending".</span></span>

- <span data-ttu-id="8cd9e-159">Durum alanı her on beş dakikada bir güncelleştirilir.</span><span class="sxs-lookup"><span data-stu-id="8cd9e-159">The status field is updated every fifteen minutes.</span></span>
