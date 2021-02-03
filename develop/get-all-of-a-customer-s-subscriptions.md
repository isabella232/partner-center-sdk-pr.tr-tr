---
title: Müşterinin aboneliğini alma
description: Müşterinin aboneliklerinin bir koleksiyonunu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a037e4a81fccbff0a02b0bdf6d93478ee15fd50f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769718"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="5b567-103">Müşterinin aboneliğini alma</span><span class="sxs-lookup"><span data-stu-id="5b567-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="5b567-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="5b567-104">**Applies To**</span></span>

- <span data-ttu-id="5b567-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5b567-105">Partner Center</span></span>
- <span data-ttu-id="5b567-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5b567-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5b567-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5b567-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5b567-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5b567-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5b567-109">Müşterinin aboneliklerinin bir koleksiyonunu alma.</span><span class="sxs-lookup"><span data-stu-id="5b567-109">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b567-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5b567-110">Prerequisites</span></span>

- <span data-ttu-id="5b567-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5b567-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5b567-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5b567-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5b567-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b567-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5b567-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b567-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5b567-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5b567-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5b567-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5b567-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5b567-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="5b567-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5b567-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="5b567-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5b567-119">C\#</span><span class="sxs-lookup"><span data-stu-id="5b567-119">C\#</span></span>

<span data-ttu-id="5b567-120">Müşterinin aboneliklerinin tümünün bir listesini almak için, önce müşteriyi tanımlamak üzere [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri tanımlayıcısıyla birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b567-120">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="5b567-121">Ardından, abonelik koleksiyonu işlemlerine bir arabirim almak için [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b567-121">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="5b567-122">Son olarak, müşterinin abonelikler koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5b567-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="5b567-123">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b567-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5b567-124">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetSubscriptions.cs</span><span class="sxs-lookup"><span data-stu-id="5b567-124">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5b567-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5b567-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5b567-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5b567-126">Request syntax</span></span>

| <span data-ttu-id="5b567-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5b567-127">Method</span></span>  | <span data-ttu-id="5b567-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5b567-128">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5b567-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="5b567-129">**GET**</span></span> | <span data-ttu-id="5b567-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/abonelikler http/1.1</span><span class="sxs-lookup"><span data-stu-id="5b567-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5b567-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="5b567-131">URI parameter</span></span>

<span data-ttu-id="5b567-132">Bu tablo, tüm abonelikleri almak için gerekli sorgu parametresini listeler.</span><span class="sxs-lookup"><span data-stu-id="5b567-132">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="5b567-133">Ad</span><span class="sxs-lookup"><span data-stu-id="5b567-133">Name</span></span>               | <span data-ttu-id="5b567-134">Tür</span><span class="sxs-lookup"><span data-stu-id="5b567-134">Type</span></span>   | <span data-ttu-id="5b567-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5b567-135">Required</span></span> | <span data-ttu-id="5b567-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5b567-136">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="5b567-137">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="5b567-137">customer-tenant-id</span></span> | <span data-ttu-id="5b567-138">string</span><span class="sxs-lookup"><span data-stu-id="5b567-138">string</span></span> | <span data-ttu-id="5b567-139">Yes</span><span class="sxs-lookup"><span data-stu-id="5b567-139">Yes</span></span>      | <span data-ttu-id="5b567-140">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="5b567-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5b567-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5b567-141">Request headers</span></span>

<span data-ttu-id="5b567-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5b567-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5b567-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5b567-143">Request body</span></span>

<span data-ttu-id="5b567-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="5b567-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5b567-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5b567-145">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="5b567-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5b567-146">REST response</span></span>

<span data-ttu-id="5b567-147">Başarılı olursa, bu yöntem yanıt gövdesinde bir [abonelik](subscription-resources.md) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="5b567-147">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5b567-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5b567-148">Response success and error codes</span></span>

<span data-ttu-id="5b567-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5b567-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5b567-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b567-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5b567-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5b567-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5b567-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5b567-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 73754
Content-Type: application/json
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
Date: Wed, 25 Nov 2015 05:43:06 GMT

{
    "totalCount": 37,
    "items": [{
        "id": "83ef9d05-4169-4ef9-9657-0e86b1eab1de",
        "entitlementId": "a356ac8c-e310-44f4-bf85-C7f29044af99",
        "friendlyName": "nickname",
        "quantity": 1,
        "unitType": "none",
        "creationDate": "2015-11-25T06: 41: 12Z",
        "effectiveStartDate": "2015-11-24T08: 00: 00Z",
        "commitmentEndDate": "2016-12-12T08: 00: 00Z",
        "status": "active",
        "autoRenewEnabled": false,
        "billingType": "none",
        "contractType": "subscription",
        "links": {
            "offer": {
                "uri": "/v1/offers/0CCA44D6-68E9-4762-94EE-31ECE98783B9",
                "method": "GET",
                "headers": []
            },
            "self": {
                "uri": "/subscriptions?key=<key>",
                "method": "GET",
                "headers": []
            }
        },
        "orderId": "6183db3d-6318-4e52-877e-25806e4971be",
        "attributes": {
            "etag": "<etag>",
            "objectType": "Subscription"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
