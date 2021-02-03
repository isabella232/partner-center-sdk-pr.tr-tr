---
title: İş ortağı MPN kimliğine göre bir müşterinin aboneliğini alma
description: Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c95488b62449e1ab6bd2eeefea58d6686c291f4c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769712"
---
# <a name="get-a-customers-subscriptions-by-partner-mpn-id"></a><span data-ttu-id="f88c8-103">İş ortağı MPN kimliğine göre bir müşterinin aboneliğini alma</span><span class="sxs-lookup"><span data-stu-id="f88c8-103">Get a customer's subscriptions by partner MPN ID</span></span>

<span data-ttu-id="f88c8-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="f88c8-104">**Applies To**</span></span>

- <span data-ttu-id="f88c8-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f88c8-105">Partner Center</span></span>
- <span data-ttu-id="f88c8-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f88c8-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f88c8-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f88c8-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f88c8-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f88c8-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f88c8-109">Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini alma.</span><span class="sxs-lookup"><span data-stu-id="f88c8-109">How to get a list of subscriptions provided by a given partner to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f88c8-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f88c8-110">Prerequisites</span></span>

- <span data-ttu-id="f88c8-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f88c8-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f88c8-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="f88c8-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f88c8-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f88c8-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f88c8-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f88c8-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f88c8-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f88c8-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f88c8-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f88c8-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f88c8-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f88c8-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="f88c8-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="f88c8-119">İş ortağı Microsoft İş Ortağı Ağı (MPN) tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="f88c8-119">A partner Microsoft Partner Network (MPN) identifier.</span></span>

## <a name="c"></a><span data-ttu-id="f88c8-120">C\#</span><span class="sxs-lookup"><span data-stu-id="f88c8-120">C\#</span></span>

<span data-ttu-id="f88c8-121">Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-121">To get a list of subscriptions provided by a given partner to a specified customer, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="f88c8-122">Ardından, [**abonelikler**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) özelliğinden müşteri aboneliği koleksiyonu işlemlerine yönelik bir arabirim alın ve iş ortağını tanımlamak ve iş ortağı abonelik işlemlerine bir arabirim almak için MPN kimliğiyle [**bypartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-122">Then get an interface to customer subscription collection operations from the [**Subscriptions**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.subscriptions) property, and call the [**ByPartner**](/dotnet/api/microsoft.store.partnercenter.subscriptions.isubscriptioncollection.bypartner) method with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="f88c8-123">Son olarak, koleksiyonu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientireentitycollectionretrievaloperations-2.getasync) method to get the collection.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string partnerMpnId;

var customerSubscriptionsByMpnId = partnerOperations.Customers.ById(customerId).Subscriptions.ByPartner(partnerMpnId).Get();
```

<span data-ttu-id="f88c8-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f88c8-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f88c8-125">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetSubscriptionsByMpnid.cs</span><span class="sxs-lookup"><span data-stu-id="f88c8-125">**Project**: Partner Center SDK Samples **Class**: GetSubscriptionsByMpnid.cs</span></span>

## <a name="java"></a><span data-ttu-id="f88c8-126">Java</span><span class="sxs-lookup"><span data-stu-id="f88c8-126">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f88c8-127">Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE **ıaggregatepartner. getCustomers. Byıd** işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-127">To get a list of subscriptions provided by a given partner to a specified customer, first use the **IAggregatePartner.getCustomers.byId** function with the customer ID to identify the customer.</span></span> <span data-ttu-id="f88c8-128">Ardından, **Getabonelikler** işlevinden müşteri aboneliği koleksiyonu işlemlerine bir arabirim alın ve iş ortağını tanımlamak ve iş ortağı abonelik işlemlerine bir arabirim almak için MPN kimliğiyle **bypartner** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-128">Then get an interface to customer subscription collection operations from the **getSubscriptions** function, and call the **byPartner** function with the MPN ID to identify the partner and retrieve an interface to partner subscription operations.</span></span> <span data-ttu-id="f88c8-129">Son olarak, koleksiyonu almak için **Get** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-129">Finally, call the **get** function to get the collection.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String partnerMpnId;

ResourceCollection<Subscription> customerSubscriptionsByMpnId = partnerOperations.getCustomers().byId(customerId).getSubscriptions().byPartner(partnerMpnId).get();
```

## <a name="powershell"></a><span data-ttu-id="f88c8-130">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f88c8-130">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="f88c8-131">Belirli bir iş ortağı tarafından belirtilen bir müşteriye sağlanan Aboneliklerin listesini almak için [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="f88c8-131">To get a list of subscriptions provided by a given partner to a specified customer, execute the [**Get-PartnerCustomerSubscription**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomerSubscription.md) command.</span></span> <span data-ttu-id="f88c8-132">Müşteriyi belirlemek için müşteri KIMLIĞINI belirtin ve **CustomerID** parametresini kullanarak **MPNıD** parametresini MPN kimliğiyle doldurun ve iş ortağını belirleyin.</span><span class="sxs-lookup"><span data-stu-id="f88c8-132">Specify the customer ID to identify the customer using the **CustomerId** parameter, and populate the **MpnId** parameter with the MPN ID to identify the partner.</span></span>

```powershell
# $customerId
# $partnerMpnId

Get-PartnerCustomerSubscription -CustomerId $customerId -MpnId $partnerMpnId
```

## <a name="rest-request"></a><span data-ttu-id="f88c8-133">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f88c8-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f88c8-134">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f88c8-134">Request syntax</span></span>

| <span data-ttu-id="f88c8-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f88c8-135">Method</span></span>  | <span data-ttu-id="f88c8-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f88c8-136">Request URI</span></span> |
|---------|----------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f88c8-137">**Al**</span><span class="sxs-lookup"><span data-stu-id="f88c8-137">**GET**</span></span> | <span data-ttu-id="f88c8-138">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/abonelikler? MPN \_ ID = {MPN-id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f88c8-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/subscriptions?mpn\_id={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="f88c8-139">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="f88c8-139">URI parameters</span></span>

<span data-ttu-id="f88c8-140">Müşteriyi ve ortağı belirlemek için aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-140">Use the following path and query parameters to identify the customer and partner.</span></span>

| <span data-ttu-id="f88c8-141">Ad</span><span class="sxs-lookup"><span data-stu-id="f88c8-141">Name</span></span>        | <span data-ttu-id="f88c8-142">Tür</span><span class="sxs-lookup"><span data-stu-id="f88c8-142">Type</span></span>   | <span data-ttu-id="f88c8-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f88c8-143">Required</span></span> | <span data-ttu-id="f88c8-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f88c8-144">Description</span></span>                                                 |
|-------------|--------|----------|-------------------------------------------------------------|
| <span data-ttu-id="f88c8-145">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="f88c8-145">customer-id</span></span> | <span data-ttu-id="f88c8-146">string</span><span class="sxs-lookup"><span data-stu-id="f88c8-146">string</span></span> | <span data-ttu-id="f88c8-147">Yes</span><span class="sxs-lookup"><span data-stu-id="f88c8-147">Yes</span></span>      | <span data-ttu-id="f88c8-148">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="f88c8-148">A GUID formatted string that identifies the customer.</span></span>       |
| <span data-ttu-id="f88c8-149">MPN kimliği</span><span class="sxs-lookup"><span data-stu-id="f88c8-149">mpn-id</span></span>      | <span data-ttu-id="f88c8-150">int</span><span class="sxs-lookup"><span data-stu-id="f88c8-150">int</span></span>    | <span data-ttu-id="f88c8-151">Yes</span><span class="sxs-lookup"><span data-stu-id="f88c8-151">Yes</span></span>      | <span data-ttu-id="f88c8-152">Ortağı tanımlayan Microsoft İş Ortağı Ağı KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="f88c8-152">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f88c8-153">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f88c8-153">Request headers</span></span>

<span data-ttu-id="f88c8-154">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f88c8-154">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f88c8-155">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f88c8-155">Request body</span></span>

<span data-ttu-id="f88c8-156">Yok.</span><span class="sxs-lookup"><span data-stu-id="f88c8-156">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="f88c8-157">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f88c8-157">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions?mpn_id=4847383 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="f88c8-158">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f88c8-158">REST response</span></span>

<span data-ttu-id="f88c8-159">Başarılı olursa, yanıt gövdesi [abonelik](subscription-resources.md) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f88c8-159">If successful, the response body contains the collection of [Subscription](subscription-resources.md) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f88c8-160">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f88c8-160">Response success and error codes</span></span>

<span data-ttu-id="f88c8-161">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="f88c8-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f88c8-162">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f88c8-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f88c8-163">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f88c8-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f88c8-164">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f88c8-164">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 985
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: d0e38dfd-a2c5-4a14-ac06-12d30f0ec54e
MS-CV: LdFhumtx6Ea0Kl5Z.0
MS-ServerId: 101112202
Date: Thu, 13 Apr 2017 20:58:08 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
            "offerId": "DB2E705F-B82A-4024-A3D5-D88E12F2DB35",
            "offerName": "Intune Device",
            "friendlyName": "new offer purchase",
            "quantity": 5,
            "unitType": "Licenses",
            "creationDate": "2017-04-10T23:02:26.02Z",
            "effectiveStartDate": "2017-04-10T00:00:00Z",
            "commitmentEndDate": "2018-05-07T00:00:00Z",
            "status": "active",
            "autoRenewEnabled": true,
            "isTrial": false,
            "billingType": "license",
            "billingCycle": "monthly",
            "partnerId": "4847383",
            "contractType": "subscription",
            "links": {
                "offer": {
                    "uri": "/offers/DB2E705F-B82A-4024-A3D5-D88E12F2DB35?country=US",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/subscriptions/42226ED6-070A-4E0F-B80C-4CDFB3E97AA7",
                    "method": "GET",
                    "headers": []
                }
            },
            "orderId": "3EDDCAC6-63B2-4C40-B0B6-F47E18301492",
            "attributes": {
                "etag": "eyJpZCI6IjQyMjI2ZWQ2LTA3MGEtNGUwZi1iODBjLTRjZGZiM2U5N2FhNyIsInZlcnNpb24iOjF9",
                "objectType": "Subscription"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="see-also"></a><span data-ttu-id="f88c8-165">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="f88c8-165">See also</span></span>

- [<span data-ttu-id="f88c8-166">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="f88c8-166">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
