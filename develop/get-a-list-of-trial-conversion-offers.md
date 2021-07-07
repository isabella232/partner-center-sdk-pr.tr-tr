---
title: Deneme dönüştürme tekliflerinin bir listesini alma
description: Deneme dönüştürme tekliflerinin listesini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 981910560faf7b7957b28e643c09a003826b9cff
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873930"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="51e95-103">Deneme dönüştürme tekliflerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="51e95-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="51e95-104">Deneme dönüştürme tekliflerinin listesini alma.</span><span class="sxs-lookup"><span data-stu-id="51e95-104">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51e95-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="51e95-105">Prerequisites</span></span>

- <span data-ttu-id="51e95-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="51e95-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="51e95-107">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="51e95-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="51e95-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="51e95-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="51e95-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="51e95-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="51e95-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="51e95-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="51e95-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="51e95-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="51e95-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="51e95-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="51e95-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="51e95-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="51e95-114">Etkin bir deneme aboneliği için abonelik kimliği.</span><span class="sxs-lookup"><span data-stu-id="51e95-114">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="51e95-115">C\#</span><span class="sxs-lookup"><span data-stu-id="51e95-115">C\#</span></span>

<span data-ttu-id="51e95-116">Kullanılabilir deneme dönüştürmelerinin listesini almak için, müşteri kimliğini kullanarak müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak müşteriyi tanıyın.</span><span class="sxs-lookup"><span data-stu-id="51e95-116">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="51e95-117">Ardından, deneme aboneliği kimliğiyle [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="51e95-117">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="51e95-118">Ardından Dönüştürmeler [**özelliğini**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) kullanarak dönüştürmeler üzerinde kullanılabilir işlemlere bir arabirim elde edin ve ardından kullanılabilir Dönüştürme tekliflerinin koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) [**yöntemini**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51e95-118">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="51e95-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="51e95-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="51e95-120">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="51e95-120">Request syntax</span></span>

| <span data-ttu-id="51e95-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="51e95-121">Method</span></span>  | <span data-ttu-id="51e95-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="51e95-122">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="51e95-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="51e95-123">**GET**</span></span> | <span data-ttu-id="51e95-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="51e95-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="51e95-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="51e95-125">URI parameter</span></span>

<span data-ttu-id="51e95-126">Müşteri ve deneme aboneliğini tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="51e95-126">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="51e95-127">Ad</span><span class="sxs-lookup"><span data-stu-id="51e95-127">Name</span></span>            | <span data-ttu-id="51e95-128">Tür</span><span class="sxs-lookup"><span data-stu-id="51e95-128">Type</span></span>   | <span data-ttu-id="51e95-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="51e95-129">Required</span></span> | <span data-ttu-id="51e95-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="51e95-130">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="51e95-131">customer-id</span><span class="sxs-lookup"><span data-stu-id="51e95-131">customer-id</span></span>     | <span data-ttu-id="51e95-132">string</span><span class="sxs-lookup"><span data-stu-id="51e95-132">string</span></span> | <span data-ttu-id="51e95-133">Yes</span><span class="sxs-lookup"><span data-stu-id="51e95-133">Yes</span></span>      | <span data-ttu-id="51e95-134">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="51e95-134">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="51e95-135">subscription-id</span><span class="sxs-lookup"><span data-stu-id="51e95-135">subscription-id</span></span> | <span data-ttu-id="51e95-136">string</span><span class="sxs-lookup"><span data-stu-id="51e95-136">string</span></span> | <span data-ttu-id="51e95-137">Yes</span><span class="sxs-lookup"><span data-stu-id="51e95-137">Yes</span></span>      | <span data-ttu-id="51e95-138">Deneme aboneliğini tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="51e95-138">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="51e95-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="51e95-139">Request headers</span></span>

<span data-ttu-id="51e95-140">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="51e95-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="51e95-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="51e95-141">Request body</span></span>

<span data-ttu-id="51e95-142">Yok.</span><span class="sxs-lookup"><span data-stu-id="51e95-142">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="51e95-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="51e95-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="51e95-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="51e95-144">REST response</span></span>

<span data-ttu-id="51e95-145">Başarılı olursa, yanıt gövdesi Bir Dönüştürme kaynakları [koleksiyonu](conversions-resources.md#conversionresult) içerir.</span><span class="sxs-lookup"><span data-stu-id="51e95-145">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="51e95-146">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="51e95-146">Response success and error codes</span></span>

<span data-ttu-id="51e95-147">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="51e95-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="51e95-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="51e95-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="51e95-149">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="51e95-149">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="51e95-150">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="51e95-150">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 305
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CV: feJByqU1X0ObaTQr.0
MS-ServerId: 030011719
Date: Thu, 15 Jun 2017 23:10:01 GMT

 {
    "totalCount": 1,
    "items": [{
            "offerId": "C0BD2E08-11AC-4836-BDC7-3712E744922F",
            "targetOfferId": "031C9E47-4802-4248-838E-778FB1D2CC05",
            "orderId": "D51A052E-043C-4A2A-AA37-2BB938CEF6C1",
            "quantity": 25,
            "billingCycle": "monthly",
            "attributes": {
                "objectType": "Conversion"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
