---
title: Müşteri ilkelerinin bir listesini alma
description: Belirtilen müşterinin yapılandırma ilkelerinin bir koleksiyonunu alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 16886b1adca393ed2967f2a4fe74a379bef1c1c7
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769340"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="542a1-103">Müşteri ilkelerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="542a1-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="542a1-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="542a1-104">**Applies to:**</span></span>

- <span data-ttu-id="542a1-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="542a1-105">Partner Center</span></span>
- <span data-ttu-id="542a1-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="542a1-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="542a1-107">Bu makalede, belirtilen müşterinin yapılandırma ilkelerinin bir koleksiyonunun nasıl alınacağını açıklanır.</span><span class="sxs-lookup"><span data-stu-id="542a1-107">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="542a1-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="542a1-108">Prerequisites</span></span>

- <span data-ttu-id="542a1-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="542a1-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="542a1-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="542a1-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="542a1-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="542a1-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="542a1-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="542a1-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="542a1-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="542a1-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="542a1-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="542a1-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="542a1-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="542a1-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="542a1-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="542a1-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="542a1-117">C\#</span><span class="sxs-lookup"><span data-stu-id="542a1-117">C\#</span></span>

<span data-ttu-id="542a1-118">Müşterinin ilkelerinin tümünün listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="542a1-118">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="542a1-119">Belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="542a1-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="542a1-120">Yapılandırma ilkesi toplama işlemlerine bir arabirim almak için [**Configurationpolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="542a1-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="542a1-121">İlke koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="542a1-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="542a1-122">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="542a1-122">For an example, see the following:</span></span>

- <span data-ttu-id="542a1-123">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="542a1-123">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="542a1-124">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="542a1-124">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="542a1-125">Sınıf: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="542a1-125">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="542a1-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="542a1-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="542a1-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="542a1-127">Request syntax</span></span>

| <span data-ttu-id="542a1-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="542a1-128">Method</span></span>  | <span data-ttu-id="542a1-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="542a1-129">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="542a1-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="542a1-130">**GET**</span></span> | <span data-ttu-id="542a1-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="542a1-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="542a1-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="542a1-132">URI parameter</span></span>

<span data-ttu-id="542a1-133">İsteği oluştururken aşağıdaki yol parametresini kullanın:</span><span class="sxs-lookup"><span data-stu-id="542a1-133">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="542a1-134">Ad</span><span class="sxs-lookup"><span data-stu-id="542a1-134">Name</span></span>        | <span data-ttu-id="542a1-135">Tür</span><span class="sxs-lookup"><span data-stu-id="542a1-135">Type</span></span>   | <span data-ttu-id="542a1-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="542a1-136">Required</span></span> | <span data-ttu-id="542a1-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="542a1-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="542a1-138">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="542a1-138">customer-id</span></span> | <span data-ttu-id="542a1-139">string</span><span class="sxs-lookup"><span data-stu-id="542a1-139">string</span></span> | <span data-ttu-id="542a1-140">Yes</span><span class="sxs-lookup"><span data-stu-id="542a1-140">Yes</span></span>      | <span data-ttu-id="542a1-141">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="542a1-141">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="542a1-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="542a1-142">Request headers</span></span>

<span data-ttu-id="542a1-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="542a1-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="542a1-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="542a1-144">Request body</span></span>

<span data-ttu-id="542a1-145">Yok</span><span class="sxs-lookup"><span data-stu-id="542a1-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="542a1-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="542a1-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
Content-Length:0
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="542a1-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="542a1-147">REST response</span></span>

<span data-ttu-id="542a1-148">Başarılı olursa, yanıt gövdesi [Configurationpolicy](device-deployment-resources.md#configurationpolicy) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="542a1-148">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="542a1-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="542a1-149">Response success and error codes</span></span>

<span data-ttu-id="542a1-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="542a1-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="542a1-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="542a1-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="542a1-152">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="542a1-152">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="542a1-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="542a1-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1221
Content-Type: application/json; charset=utf-8
MS-CorrelationId: d5ff2573-3ef8-4553-aac4-4b73d97dce1b
MS-RequestId: 6eb7383d-eeb5-44d7-8570-e0ed12c0547a
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:49 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "8c7d25aa-2dbb-409c-a1f0-f55bd9108fa9",
            "name": "Windows 10 Enterprise E3",
            "category": "o_o_b_e",
            "description": "P462017 description",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-04-27T11:30:34.1944704-07:00",
            "lastModifiedDate": "2017-04-27T11:30:34.1944704-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
            "name": "Test policy",
            "category": "o_o_b_e",
            "description": "Test policy creation from API 1",
            "devicesAssigned": 0,
            "policySettings": ["skip_express_settings"],
            "createdDate": "2017-07-25T11:03:03.8457088-07:00",
            "lastModifiedDate": "2017-07-25T11:04:00.8150016-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }, {
            "id": "a96b5fd9-0f3a-419a-b55c-a8aecd6b1f00",
            "name": "Windows 10 Enterprise E5",
            "category": "o_o_b_e",
            "description": "test policy creation from API",
            "devicesAssigned": 0,
            "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
            "createdDate": "2017-07-25T11:07:36.1501184-07:00",
            "lastModifiedDate": "2017-07-25T11:07:36.1501184-07:00",
            "attributes": {
                "objectType": "ConfigurationPolicy"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
