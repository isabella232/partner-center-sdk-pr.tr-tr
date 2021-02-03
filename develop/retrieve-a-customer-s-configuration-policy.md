---
title: Müşterinin yapılandırma ilkesini alma
description: Belirtilen müşteri için belirtilen yapılandırma ilkesini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d5d4ee83d1a66f33872d8b1f1327f47eeb4465e
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769790"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="be9cc-103">Müşterinin yapılandırma ilkesini alma</span><span class="sxs-lookup"><span data-stu-id="be9cc-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="be9cc-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="be9cc-104">**Applies To**</span></span>

- <span data-ttu-id="be9cc-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="be9cc-105">Partner Center</span></span>
- <span data-ttu-id="be9cc-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="be9cc-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="be9cc-107">Belirtilen müşteri için belirtilen yapılandırma ilkesini alma.</span><span class="sxs-lookup"><span data-stu-id="be9cc-107">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be9cc-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="be9cc-108">Prerequisites</span></span>

- <span data-ttu-id="be9cc-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="be9cc-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="be9cc-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="be9cc-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="be9cc-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="be9cc-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="be9cc-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="be9cc-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="be9cc-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="be9cc-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="be9cc-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="be9cc-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="be9cc-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="be9cc-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="be9cc-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="be9cc-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="be9cc-117">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="be9cc-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="be9cc-118">C\#</span><span class="sxs-lookup"><span data-stu-id="be9cc-118">C\#</span></span>

<span data-ttu-id="be9cc-119">Belirtilen müşteriye yönelik bir yapılandırma ilkesi almak için, önce belirtilen müşterideki işlemlere bir arabirim almak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="be9cc-119">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="be9cc-120">Ardından, belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke KIMLIĞIYLE [**Configurationpolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="be9cc-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="be9cc-121">Son olarak, yapılandırma ilkesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="be9cc-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="be9cc-122">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="be9cc-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="be9cc-123">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="be9cc-123">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="be9cc-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="be9cc-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="be9cc-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="be9cc-125">Request syntax</span></span>

| <span data-ttu-id="be9cc-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="be9cc-126">Method</span></span>  | <span data-ttu-id="be9cc-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="be9cc-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="be9cc-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="be9cc-128">**GET**</span></span> | <span data-ttu-id="be9cc-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="be9cc-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="be9cc-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="be9cc-130">URI parameter</span></span>

<span data-ttu-id="be9cc-131">İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="be9cc-131">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="be9cc-132">Ad</span><span class="sxs-lookup"><span data-stu-id="be9cc-132">Name</span></span>        | <span data-ttu-id="be9cc-133">Tür</span><span class="sxs-lookup"><span data-stu-id="be9cc-133">Type</span></span>   | <span data-ttu-id="be9cc-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be9cc-134">Required</span></span> | <span data-ttu-id="be9cc-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be9cc-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="be9cc-136">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="be9cc-136">customer-id</span></span> | <span data-ttu-id="be9cc-137">string</span><span class="sxs-lookup"><span data-stu-id="be9cc-137">string</span></span> | <span data-ttu-id="be9cc-138">Yes</span><span class="sxs-lookup"><span data-stu-id="be9cc-138">Yes</span></span>      | <span data-ttu-id="be9cc-139">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="be9cc-139">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="be9cc-140">ilke kimliği</span><span class="sxs-lookup"><span data-stu-id="be9cc-140">policy-id</span></span>   | <span data-ttu-id="be9cc-141">string</span><span class="sxs-lookup"><span data-stu-id="be9cc-141">string</span></span> | <span data-ttu-id="be9cc-142">Yes</span><span class="sxs-lookup"><span data-stu-id="be9cc-142">Yes</span></span>      | <span data-ttu-id="be9cc-143">İlkeyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="be9cc-143">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="be9cc-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="be9cc-144">Request headers</span></span>

<span data-ttu-id="be9cc-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="be9cc-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="be9cc-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="be9cc-146">Request body</span></span>

<span data-ttu-id="be9cc-147">Yok</span><span class="sxs-lookup"><span data-stu-id="be9cc-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="be9cc-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="be9cc-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="be9cc-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="be9cc-149">REST response</span></span>

<span data-ttu-id="be9cc-150">Başarılı olursa, yanıt istenen [Configurationpolicy](device-deployment-resources.md#configurationpolicy) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="be9cc-150">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="be9cc-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="be9cc-151">Response success and error codes</span></span>

<span data-ttu-id="be9cc-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="be9cc-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="be9cc-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="be9cc-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="be9cc-154">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="be9cc-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="be9cc-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="be9cc-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 443
MS-CorrelationId: abe150cf-c677-435c-b5d5-b34899a6d1ec
MS-RequestId: ab3abfe7-dce7-46c0-ab20-4fd49bc3e2f7
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:08:27 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API 1",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-07-25T11:03:03.8457116-07:00",
    "lastModifiedDate": "2017-07-25T11:04:00.8149974-07:00",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
