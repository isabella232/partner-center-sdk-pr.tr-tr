---
title: Müşteri siparişlerinin tümünü alma
description: Belirtilen müşteri için tüm siparişlerin bir koleksiyonunu alır.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 4d71cd138421704d94a55a9fe21e074d92638815
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769725"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="4ea36-103">Müşteri siparişlerinin tümünü alma</span><span class="sxs-lookup"><span data-stu-id="4ea36-103">Get all of a customer's orders</span></span>

<span data-ttu-id="4ea36-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="4ea36-104">**Applies to:**</span></span>

- <span data-ttu-id="4ea36-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ea36-105">Partner Center</span></span>
- <span data-ttu-id="4ea36-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ea36-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4ea36-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ea36-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4ea36-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ea36-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4ea36-109">Belirtilen müşteri için tüm siparişlerin bir koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="4ea36-109">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="4ea36-110">Bir siparişin gönderildiği ve müşterinin siparişlerinin koleksiyonunda görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="4ea36-110">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ea36-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4ea36-111">Prerequisites</span></span>

- <span data-ttu-id="4ea36-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4ea36-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4ea36-113">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4ea36-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4ea36-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4ea36-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4ea36-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ea36-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4ea36-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="4ea36-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4ea36-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4ea36-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4ea36-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="4ea36-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4ea36-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="4ea36-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="4ea36-120">C\#</span><span class="sxs-lookup"><span data-stu-id="4ea36-120">C\#</span></span>

<span data-ttu-id="4ea36-121">Müşterinin tüm siparişlerinin bir koleksiyonunu elde etmek için:</span><span class="sxs-lookup"><span data-stu-id="4ea36-121">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="4ea36-122">[**Iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="4ea36-122">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="4ea36-123">[**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğini çağırın, ardından [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) yöntemleri gelir.</span><span class="sxs-lookup"><span data-stu-id="4ea36-123">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="4ea36-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="4ea36-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="4ea36-125">**Proje**: partnersdk. Featuresamples **sınıfı**: GetOrders.cs</span><span class="sxs-lookup"><span data-stu-id="4ea36-125">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="4ea36-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4ea36-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4ea36-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4ea36-127">Request syntax</span></span>

| <span data-ttu-id="4ea36-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4ea36-128">Method</span></span>  | <span data-ttu-id="4ea36-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4ea36-129">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="4ea36-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="4ea36-130">**GET**</span></span> | <span data-ttu-id="4ea36-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="4ea36-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="4ea36-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="4ea36-132">URI parameter</span></span>

<span data-ttu-id="4ea36-133">Tüm siparişleri almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ea36-133">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="4ea36-134">Ad</span><span class="sxs-lookup"><span data-stu-id="4ea36-134">Name</span></span>                   | <span data-ttu-id="4ea36-135">Tür</span><span class="sxs-lookup"><span data-stu-id="4ea36-135">Type</span></span>     | <span data-ttu-id="4ea36-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4ea36-136">Required</span></span> | <span data-ttu-id="4ea36-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4ea36-137">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="4ea36-138">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="4ea36-138">customer-tenant-id</span></span>     | <span data-ttu-id="4ea36-139">string</span><span class="sxs-lookup"><span data-stu-id="4ea36-139">string</span></span>   | <span data-ttu-id="4ea36-140">Yes</span><span class="sxs-lookup"><span data-stu-id="4ea36-140">Yes</span></span>      | <span data-ttu-id="4ea36-141">Müşteriye karşılık gelen GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="4ea36-141">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="4ea36-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4ea36-142">Request headers</span></span>

<span data-ttu-id="4ea36-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4ea36-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4ea36-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4ea36-144">Request body</span></span>

<span data-ttu-id="4ea36-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="4ea36-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4ea36-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4ea36-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="4ea36-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4ea36-147">REST response</span></span>

<span data-ttu-id="4ea36-148">Başarılı olursa, bu yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="4ea36-148">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4ea36-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4ea36-149">Response success and error codes</span></span>

<span data-ttu-id="4ea36-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4ea36-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4ea36-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ea36-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4ea36-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4ea36-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4ea36-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4ea36-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 22463
Content-Type: application/json; charset=utf-8
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Date: Thu, 15 Mar 2018 20:44:40 GMT

{
    "totalCount": 2,
    "items": [
        {
            "id": "9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "one_time",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "DZH318Z0BQ4B:000Z:DZH318Z0DSPL",
                    "friendlyName": "Reserved_VM_Instance_Standard_D1_AP_East_1_Year",
                    "quantity": 1,
                    "links": {
                        "sku": {
                            "uri": "/products/DZH318Z0BQ4B/skus/000Z?country=US",
                            "method": "GET",
                            "headers": []
                        }
                    }
                }
            ],
            "creationDate": "2018-03-15T02:17:15.6455674Z",
            "status": "pending",
            "links": {
                "provisioningStatus": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1/provisioningstatus",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/9qg-ErcO-4MPbPqq_3MIQaS7bn8W6HfG1",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                 "objectType": "Order"
            }
        },
        {
            "id": "eeba9d00-7b46-443a-917e-22887a8fc993",
            "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
            "billingCycle": "monthly",
            "currencyCode": "USD",
            "lineItems": [
                {
                    "lineItemNumber": 0,
                    "offerId": "E59159FC-6F67-4599-B3CB-17FF4020F643",
                    "subscriptionId": "DB8C695B-1C3C-4C55-B697-771503DD46BF",
                    "friendlyName": "Azure Active Directory Premium P2",
                    "quantity": 1,
                    "links": {
                        "subscription": {
                            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF",
                            "method": "GET",
                            "headers": []
                        },
                        "sku": {
                            "uri": "/products/84A661C4-E949-4BD2-A560-ED7766FCAF2B/skus/E59159FC-6F67-4599-B3CB-17FF4020F643",
                            "method": "GET",
                            "headers": []
                        },
                        "provisioningStatus": {
                            "uri": "/subscriptions/DB8C695B-1C3C-4C55-B697-771503DD46BF/provisioningstatus",
                            "method": "GET",
                            "headers": []
                        }
                    }
            ],
            "creationDate": "2018-03-06T17:37:05.253-08:00",
            "status": "completed",
            "links": {
                "self": {
                    "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/eeba9d00-7b46-443a-917e-22887a8fc993",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "etag": "eyJpZCI6ImVlYmE5ZDAwLTdiNDYtNDQzYS05MTdlLTIyODg3YThmYzk5MyIsInZlcnNpb24iOjF9",
                "objectType": "Order"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
         "objectType": "Collection"
    }
}
```
