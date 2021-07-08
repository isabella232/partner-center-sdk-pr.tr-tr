---
title: Müşteri siparişlerinin tümünü alma
description: Belirtilen müşteri için tüm siparişlerin bir koleksiyonunu alır.
ms.date: 06/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: e8f23e90cbb5afb45e519e2c58fd0d3b9ea2de6a
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760309"
---
# <a name="get-all-of-a-customers-orders"></a><span data-ttu-id="79e3d-103">Müşteri siparişlerinin tümünü alma</span><span class="sxs-lookup"><span data-stu-id="79e3d-103">Get all of a customer's orders</span></span>

<span data-ttu-id="79e3d-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="79e3d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="79e3d-105">Belirtilen müşteri için tüm siparişlerin bir koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="79e3d-105">Gets a collection of all the orders for a specified customer.</span></span> <span data-ttu-id="79e3d-106">Bir siparişin gönderildiği ve müşterinin siparişlerinin koleksiyonunda görüneceği zaman arasında 15 dakikaya varan bir gecikme vardır.</span><span class="sxs-lookup"><span data-stu-id="79e3d-106">There is a delay of up to 15 minutes between the time an order is submitted and when it will appear in a collection of a customer's orders.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="79e3d-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="79e3d-107">Prerequisites</span></span>

- <span data-ttu-id="79e3d-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="79e3d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="79e3d-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="79e3d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="79e3d-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="79e3d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="79e3d-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="79e3d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="79e3d-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="79e3d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="79e3d-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="79e3d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="79e3d-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="79e3d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="79e3d-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="79e3d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="79e3d-116">C\#</span><span class="sxs-lookup"><span data-stu-id="79e3d-116">C\#</span></span>

<span data-ttu-id="79e3d-117">Müşterinin tüm siparişlerinin bir koleksiyonunu elde etmek için:</span><span class="sxs-lookup"><span data-stu-id="79e3d-117">To obtain a collection of all of a customer's orders:</span></span>

1. <span data-ttu-id="79e3d-118">[**Iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="79e3d-118">Use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span>

2. <span data-ttu-id="79e3d-119">[**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğini çağırın, ardından [**Get ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) yöntemleri gelir.</span><span class="sxs-lookup"><span data-stu-id="79e3d-119">Call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var orders = partnerOperations.Customers.ById(selectedCustomerId).Orders.Get();
```

<span data-ttu-id="79e3d-120">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="79e3d-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="79e3d-121">**Project**: partnersdk. featuresamples **sınıfı**: getorders. cs</span><span class="sxs-lookup"><span data-stu-id="79e3d-121">**Project**: PartnerSDK.FeatureSamples **Class**: GetOrders.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="79e3d-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="79e3d-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="79e3d-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="79e3d-123">Request syntax</span></span>

| <span data-ttu-id="79e3d-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="79e3d-124">Method</span></span>  | <span data-ttu-id="79e3d-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="79e3d-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="79e3d-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="79e3d-126">**GET**</span></span> | <span data-ttu-id="79e3d-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="79e3d-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders HTTP/1.1</span></span>  |

#### <a name="uri-parameter"></a><span data-ttu-id="79e3d-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="79e3d-128">URI parameter</span></span>

<span data-ttu-id="79e3d-129">Tüm siparişleri almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="79e3d-129">Use the following query parameter to get all orders.</span></span>

| <span data-ttu-id="79e3d-130">Ad</span><span class="sxs-lookup"><span data-stu-id="79e3d-130">Name</span></span>                   | <span data-ttu-id="79e3d-131">Tür</span><span class="sxs-lookup"><span data-stu-id="79e3d-131">Type</span></span>     | <span data-ttu-id="79e3d-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="79e3d-132">Required</span></span> | <span data-ttu-id="79e3d-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="79e3d-133">Description</span></span>                                               |
|------------------------|----------|----------|-----------------------------------------------------------|
| <span data-ttu-id="79e3d-134">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="79e3d-134">customer-tenant-id</span></span>     | <span data-ttu-id="79e3d-135">string</span><span class="sxs-lookup"><span data-stu-id="79e3d-135">string</span></span>   | <span data-ttu-id="79e3d-136">Yes</span><span class="sxs-lookup"><span data-stu-id="79e3d-136">Yes</span></span>      | <span data-ttu-id="79e3d-137">Müşteriye karşılık gelen GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="79e3d-137">A GUID formatted string corresponding to the customer.</span></span>    |

### <a name="request-headers"></a><span data-ttu-id="79e3d-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="79e3d-138">Request headers</span></span>

<span data-ttu-id="79e3d-139">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="79e3d-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="79e3d-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="79e3d-140">Request body</span></span>

<span data-ttu-id="79e3d-141">Yok.</span><span class="sxs-lookup"><span data-stu-id="79e3d-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="79e3d-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="79e3d-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0e5fc923-8e3c-4560-9100-ce7283c3e081
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="79e3d-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="79e3d-143">REST response</span></span>

<span data-ttu-id="79e3d-144">Başarılı olursa, bu yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="79e3d-144">If successful, this method returns a collection of [Order](order-resources.md) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="79e3d-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="79e3d-145">Response success and error codes</span></span>

<span data-ttu-id="79e3d-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="79e3d-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="79e3d-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="79e3d-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="79e3d-148">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="79e3d-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="79e3d-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="79e3d-149">Response example</span></span>

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
