---
title: Müşterinin aboneliğini alma
description: Müşterinin aboneliklerinin koleksiyonunu nasıl alabilirsiniz?
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 01ac9e5169258d0ac263d5bbe8cff567c76f98ed
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760632"
---
# <a name="get-a-customers-subscriptions"></a><span data-ttu-id="94ff6-103">Müşterinin aboneliğini alma</span><span class="sxs-lookup"><span data-stu-id="94ff6-103">Get a customer's subscriptions</span></span>

<span data-ttu-id="94ff6-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="94ff6-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="94ff6-105">Müşterinin aboneliklerinin koleksiyonunu nasıl alabilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="94ff6-105">How to get a collection of a customer's subscriptions.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="94ff6-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="94ff6-106">Prerequisites</span></span>

- <span data-ttu-id="94ff6-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="94ff6-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="94ff6-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="94ff6-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="94ff6-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="94ff6-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="94ff6-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="94ff6-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="94ff6-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="94ff6-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="94ff6-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="94ff6-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="94ff6-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="94ff6-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="94ff6-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="94ff6-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="94ff6-115">C\#</span><span class="sxs-lookup"><span data-stu-id="94ff6-115">C\#</span></span>

<span data-ttu-id="94ff6-116">Bir müşterinin tüm aboneliklerinin listesini almak için önce [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri tanımlayıcısıyla birlikte kullanarak müşteriyi tanıyın.</span><span class="sxs-lookup"><span data-stu-id="94ff6-116">To get a list of all of a customer's subscriptions, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to identify the customer.</span></span> <span data-ttu-id="94ff6-117">Ardından Abonelikler [**özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) kullanarak abonelik toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="94ff6-117">Then use the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property to retrieve an interface to subscription collection operations.</span></span> <span data-ttu-id="94ff6-118">Son olarak, müşterinin abonelik koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) yöntemlerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="94ff6-118">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.getasync) methods to retrieve the customer's subscriptions collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

var customerSubscriptions = partnerOperations.Customers.ById(customerId).Subscriptions.Get();
```

<span data-ttu-id="94ff6-119">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="94ff6-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="94ff6-120">**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** GetSubscriptions.cs</span><span class="sxs-lookup"><span data-stu-id="94ff6-120">**Project**: Partner Center SDK Samples **Class**: GetSubscriptions.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="94ff6-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="94ff6-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="94ff6-122">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="94ff6-122">Request syntax</span></span>

| <span data-ttu-id="94ff6-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="94ff6-123">Method</span></span>  | <span data-ttu-id="94ff6-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="94ff6-124">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="94ff6-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="94ff6-125">**GET**</span></span> | <span data-ttu-id="94ff6-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="94ff6-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="94ff6-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="94ff6-127">URI parameter</span></span>

<span data-ttu-id="94ff6-128">Bu tabloda tüm abonelikleri almak için gerekli sorgu parametresi listelemektedir.</span><span class="sxs-lookup"><span data-stu-id="94ff6-128">This table lists the required query parameter to get all the subscriptions.</span></span>

| <span data-ttu-id="94ff6-129">Ad</span><span class="sxs-lookup"><span data-stu-id="94ff6-129">Name</span></span>               | <span data-ttu-id="94ff6-130">Tür</span><span class="sxs-lookup"><span data-stu-id="94ff6-130">Type</span></span>   | <span data-ttu-id="94ff6-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="94ff6-131">Required</span></span> | <span data-ttu-id="94ff6-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="94ff6-132">Description</span></span>                                           |
|--------------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="94ff6-133">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="94ff6-133">customer-tenant-id</span></span> | <span data-ttu-id="94ff6-134">string</span><span class="sxs-lookup"><span data-stu-id="94ff6-134">string</span></span> | <span data-ttu-id="94ff6-135">Yes</span><span class="sxs-lookup"><span data-stu-id="94ff6-135">Yes</span></span>      | <span data-ttu-id="94ff6-136">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="94ff6-136">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="94ff6-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="94ff6-137">Request headers</span></span>

<span data-ttu-id="94ff6-138">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="94ff6-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="94ff6-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="94ff6-139">Request body</span></span>

<span data-ttu-id="94ff6-140">Yok.</span><span class="sxs-lookup"><span data-stu-id="94ff6-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="94ff6-141">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="94ff6-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/subscriptions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b2d13828-2ca5-41d4-94fb-9946214f4244
MS-CorrelationId: c49004b1-224f-4d86-a607-6c8bcc52cfdd
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="94ff6-142">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="94ff6-142">REST response</span></span>

<span data-ttu-id="94ff6-143">Başarılı olursa, bu yöntem yanıt [gövdesinde Abonelik](subscription-resources.md) kaynakları koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="94ff6-143">If successful, this method returns a collection of [Subscription](subscription-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="94ff6-144">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="94ff6-144">Response success and error codes</span></span>

<span data-ttu-id="94ff6-145">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="94ff6-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="94ff6-146">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="94ff6-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="94ff6-147">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="94ff6-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="94ff6-148">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="94ff6-148">Response example</span></span>

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
