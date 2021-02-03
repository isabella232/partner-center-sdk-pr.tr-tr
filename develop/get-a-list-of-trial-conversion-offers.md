---
title: Deneme dönüştürme tekliflerinin bir listesini alma
description: Deneme dönüştürme tekliflerinin bir listesini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e1eadecde9efa0b59fc7790bd474889bb32821dc
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769539"
---
# <a name="get-a-list-of-trial-conversion-offers"></a><span data-ttu-id="34b13-103">Deneme dönüştürme tekliflerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="34b13-103">Get a list of trial conversion offers</span></span>

<span data-ttu-id="34b13-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="34b13-104">**Applies To**</span></span>

- <span data-ttu-id="34b13-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="34b13-105">Partner Center</span></span>

<span data-ttu-id="34b13-106">Deneme dönüştürme tekliflerinin bir listesini alma.</span><span class="sxs-lookup"><span data-stu-id="34b13-106">How to retrieve a list of trial conversion offers.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34b13-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="34b13-107">Prerequisites</span></span>

- <span data-ttu-id="34b13-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="34b13-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="34b13-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="34b13-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="34b13-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="34b13-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="34b13-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34b13-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="34b13-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="34b13-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="34b13-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="34b13-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="34b13-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="34b13-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="34b13-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="34b13-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="34b13-116">Etkin deneme aboneliği için abonelik KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="34b13-116">A subscription ID for an active trial subscription.</span></span>

## <a name="c"></a><span data-ttu-id="34b13-117">C\#</span><span class="sxs-lookup"><span data-stu-id="34b13-117">C\#</span></span>

<span data-ttu-id="34b13-118">Kullanılabilir deneme dönüştürmeleri listesini almak için, müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanarak başlayın.</span><span class="sxs-lookup"><span data-stu-id="34b13-118">To get a list of trial conversions available, start by using the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="34b13-119">Ardından, deneme aboneliği KIMLIĞIYLE [**abonelikler. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırarak abonelik işlemlerine yönelik bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="34b13-119">Then, get an interface to subscription operations by calling the [**Subscriptions.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the trial subscription ID.</span></span> <span data-ttu-id="34b13-120">Ardından [**dönüşümler özelliğini kullanarak, dönüşümler üzerinde**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) kullanılabilir işlemlere bir arabirim elde edin ve ardından kullanılabilir [**dönüştürme**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) tekliflerinin bir koleksiyonunu almak Için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="34b13-120">Next, use the [**Conversions**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscription.conversions) property to obtain an interface to the available operations on conversions, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptionconversioncollection.getasync) method to retrieve a collection of available [**Conversion**](/dotnet/api/microsoft.store.partnercenter.models.subscriptions.conversion) offers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string subscriptionId;

// Get the available conversions.
var conversions =
    partnerOperations.Customers.ById(customerId).Subscriptions.ById(subscriptionId).Conversions.Get();
```

## <a name="rest-request"></a><span data-ttu-id="34b13-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="34b13-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="34b13-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="34b13-122">Request syntax</span></span>

| <span data-ttu-id="34b13-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="34b13-123">Method</span></span>  | <span data-ttu-id="34b13-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="34b13-124">Request URI</span></span>                                                                                                                 |
|---------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="34b13-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="34b13-125">**GET**</span></span> | <span data-ttu-id="34b13-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Subscriptions/{Subscription-id}/dönüşümler http/1.1</span><span class="sxs-lookup"><span data-stu-id="34b13-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="34b13-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="34b13-127">URI parameter</span></span>

<span data-ttu-id="34b13-128">Müşteri ve deneme aboneliğini belirlemek için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="34b13-128">Use the following path parameters to identify the customer and trial subscription.</span></span>

| <span data-ttu-id="34b13-129">Ad</span><span class="sxs-lookup"><span data-stu-id="34b13-129">Name</span></span>            | <span data-ttu-id="34b13-130">Tür</span><span class="sxs-lookup"><span data-stu-id="34b13-130">Type</span></span>   | <span data-ttu-id="34b13-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="34b13-131">Required</span></span> | <span data-ttu-id="34b13-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34b13-132">Description</span></span>                                                     |
|-----------------|--------|----------|-----------------------------------------------------------------|
| <span data-ttu-id="34b13-133">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="34b13-133">customer-id</span></span>     | <span data-ttu-id="34b13-134">string</span><span class="sxs-lookup"><span data-stu-id="34b13-134">string</span></span> | <span data-ttu-id="34b13-135">Yes</span><span class="sxs-lookup"><span data-stu-id="34b13-135">Yes</span></span>      | <span data-ttu-id="34b13-136">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="34b13-136">A GUID formatted string that identifies the customer.</span></span>           |
| <span data-ttu-id="34b13-137">abonelik kimliği</span><span class="sxs-lookup"><span data-stu-id="34b13-137">subscription-id</span></span> | <span data-ttu-id="34b13-138">string</span><span class="sxs-lookup"><span data-stu-id="34b13-138">string</span></span> | <span data-ttu-id="34b13-139">Yes</span><span class="sxs-lookup"><span data-stu-id="34b13-139">Yes</span></span>      | <span data-ttu-id="34b13-140">Deneme aboneliğini tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="34b13-140">A GUID formatted string that identifies the trial subscription.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="34b13-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="34b13-141">Request headers</span></span>

<span data-ttu-id="34b13-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="34b13-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="34b13-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="34b13-143">Request body</span></span>

<span data-ttu-id="34b13-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="34b13-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="34b13-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="34b13-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/subscriptions/488745B5-2086-4912-802C-6ABB9F7C3638/conversions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e17f5bc6-24bf-4cbe-b632-d7fc6cec3058
MS-CorrelationId: 8daa6d54-72ab-4d6b-9c7d-9266d3734a47
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="34b13-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="34b13-146">REST response</span></span>

<span data-ttu-id="34b13-147">Başarılı olursa, yanıt gövdesi bir [dönüştürme](conversions-resources.md#conversionresult) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="34b13-147">If successful, the response body contains a collection of [Conversion](conversions-resources.md#conversionresult) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="34b13-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="34b13-148">Response success and error codes</span></span>

<span data-ttu-id="34b13-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="34b13-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="34b13-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="34b13-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="34b13-151">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="34b13-151">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="34b13-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="34b13-152">Response example</span></span>

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
