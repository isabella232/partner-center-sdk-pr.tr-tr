---
title: Müşteri ilkelerinin bir listesini alma
description: Belirtilen müşterinin yapılandırma ilkelerinin koleksiyonunu alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: bf6ace0d2425e28d80c4f2310878c2d2a9e2a876
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874593"
---
# <a name="get-a-list-of-a-customers-policies"></a><span data-ttu-id="2e1ed-103">Müşteri ilkelerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="2e1ed-103">Get a list of a customer's policies</span></span>

<span data-ttu-id="2e1ed-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek</span><span class="sxs-lookup"><span data-stu-id="2e1ed-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="2e1ed-105">Bu makalede, belirtilen müşterinin yapılandırma ilkelerinin bir koleksiyonunun nasıl alın açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-105">This article describes how to retrieve a collection of the specified customer's configuration policies.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e1ed-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2e1ed-106">Prerequisites</span></span>

- <span data-ttu-id="2e1ed-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="2e1ed-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e1ed-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2e1ed-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e1ed-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2e1ed-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="2e1ed-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2e1ed-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="2e1ed-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2e1ed-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="2e1ed-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2e1ed-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2e1ed-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="2e1ed-115">C\#</span><span class="sxs-lookup"><span data-stu-id="2e1ed-115">C\#</span></span>

<span data-ttu-id="2e1ed-116">Bir müşterinin tüm ilkelerinin listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="2e1ed-116">To get a list of all of a customer's policies:</span></span>

1. <span data-ttu-id="2e1ed-117">Belirtilen müşteri üzerinde işlemlere bir arabirim almak için müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-117">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="2e1ed-118">Yapılandırma ilkesi toplama işlemlerine bir arabirim almak için [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-118">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>
3. <span data-ttu-id="2e1ed-119">İlke [**koleksiyonunu**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) almak [**için Get veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.getasync) method to retrieve the collection of policies.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

var configPolicies = partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Get();
```

<span data-ttu-id="2e1ed-120">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="2e1ed-120">For an example, see the following:</span></span>

- <span data-ttu-id="2e1ed-121">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="2e1ed-121">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="2e1ed-122">Project: **İş Ortağı Merkezi SDK'sı Örnekleri**</span><span class="sxs-lookup"><span data-stu-id="2e1ed-122">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="2e1ed-123">Sınıf: **GetAllConfigurationPolicies.cs**</span><span class="sxs-lookup"><span data-stu-id="2e1ed-123">Class: **GetAllConfigurationPolicies.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="2e1ed-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2e1ed-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e1ed-125">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="2e1ed-125">Request syntax</span></span>

| <span data-ttu-id="2e1ed-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2e1ed-126">Method</span></span>  | <span data-ttu-id="2e1ed-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2e1ed-127">Request URI</span></span>                                                                              |
|---------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e1ed-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="2e1ed-128">**GET**</span></span> | <span data-ttu-id="2e1ed-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="2e1ed-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="2e1ed-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="2e1ed-130">URI parameter</span></span>

<span data-ttu-id="2e1ed-131">İsteği oluştururken aşağıdaki yol parametresini kullanın:</span><span class="sxs-lookup"><span data-stu-id="2e1ed-131">Use the following path parameter when creating the request:</span></span>

| <span data-ttu-id="2e1ed-132">Ad</span><span class="sxs-lookup"><span data-stu-id="2e1ed-132">Name</span></span>        | <span data-ttu-id="2e1ed-133">Tür</span><span class="sxs-lookup"><span data-stu-id="2e1ed-133">Type</span></span>   | <span data-ttu-id="2e1ed-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2e1ed-134">Required</span></span> | <span data-ttu-id="2e1ed-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e1ed-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="2e1ed-136">customer-id</span><span class="sxs-lookup"><span data-stu-id="2e1ed-136">customer-id</span></span> | <span data-ttu-id="2e1ed-137">string</span><span class="sxs-lookup"><span data-stu-id="2e1ed-137">string</span></span> | <span data-ttu-id="2e1ed-138">Yes</span><span class="sxs-lookup"><span data-stu-id="2e1ed-138">Yes</span></span>      | <span data-ttu-id="2e1ed-139">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2e1ed-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2e1ed-140">Request headers</span></span>

<span data-ttu-id="2e1ed-141">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="2e1ed-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2e1ed-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2e1ed-142">Request body</span></span>

<span data-ttu-id="2e1ed-143">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="2e1ed-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2e1ed-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2e1ed-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2e1ed-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2e1ed-145">REST response</span></span>

<span data-ttu-id="2e1ed-146">Başarılı olursa yanıt gövdesi [ConfigurationPolicy kaynaklarının koleksiyonunu](device-deployment-resources.md#configurationpolicy) içerir.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-146">If successful, the response body contains the collection of [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e1ed-147">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2e1ed-147">Response success and error codes</span></span>

<span data-ttu-id="2e1ed-148">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2e1ed-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e1ed-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e1ed-150">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="2e1ed-150">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2e1ed-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2e1ed-151">Response example</span></span>

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
