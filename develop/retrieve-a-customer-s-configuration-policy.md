---
title: Müşterinin yapılandırma ilkesini alma
description: Belirtilen müşteri için belirtilen yapılandırma ilkesi nasıl alınır?
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f9a8cb435c63d8d02c3b4633abc8723353116f37
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547504"
---
# <a name="retrieve-a-customers-configuration-policy"></a><span data-ttu-id="18140-103">Müşterinin yapılandırma ilkesini alma</span><span class="sxs-lookup"><span data-stu-id="18140-103">Retrieve a customer's configuration policy</span></span>

<span data-ttu-id="18140-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek</span><span class="sxs-lookup"><span data-stu-id="18140-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="18140-105">Belirtilen müşteri için belirtilen yapılandırma ilkesi nasıl alınır?</span><span class="sxs-lookup"><span data-stu-id="18140-105">How to retrieve the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="18140-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="18140-106">Prerequisites</span></span>

- <span data-ttu-id="18140-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="18140-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="18140-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="18140-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="18140-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="18140-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="18140-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="18140-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="18140-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="18140-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="18140-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="18140-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="18140-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="18140-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="18140-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="18140-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="18140-115">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="18140-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="18140-116">C\#</span><span class="sxs-lookup"><span data-stu-id="18140-116">C\#</span></span>

<span data-ttu-id="18140-117">Belirtilen müşteriye yönelik bir yapılandırma ilkesi almak için, önce [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle çağırarak belirtilen müşteri üzerinde işlemlere bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="18140-117">To retrieve a configuration policy for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="18140-118">Ardından, belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke kimliğiyle [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="18140-118">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="18140-119">Son olarak, [**yapılandırma ilkesi almak**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) için Get veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="18140-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.getasync) method to retrieve the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy retrievedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Get();
```

<span data-ttu-id="18140-120">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="18140-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="18140-121">**Project:** İş Ortağı Merkezi SDK'sı Örnekler **Sınıfı:** GetConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="18140-121">**Project**: Partner Center SDK Samples **Class**: GetConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="18140-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="18140-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="18140-123">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="18140-123">Request syntax</span></span>

| <span data-ttu-id="18140-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="18140-124">Method</span></span>  | <span data-ttu-id="18140-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="18140-125">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="18140-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="18140-126">**GET**</span></span> | <span data-ttu-id="18140-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="18140-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="18140-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="18140-128">URI parameter</span></span>

<span data-ttu-id="18140-129">İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="18140-129">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="18140-130">Ad</span><span class="sxs-lookup"><span data-stu-id="18140-130">Name</span></span>        | <span data-ttu-id="18140-131">Tür</span><span class="sxs-lookup"><span data-stu-id="18140-131">Type</span></span>   | <span data-ttu-id="18140-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="18140-132">Required</span></span> | <span data-ttu-id="18140-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="18140-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="18140-134">customer-id</span><span class="sxs-lookup"><span data-stu-id="18140-134">customer-id</span></span> | <span data-ttu-id="18140-135">string</span><span class="sxs-lookup"><span data-stu-id="18140-135">string</span></span> | <span data-ttu-id="18140-136">Yes</span><span class="sxs-lookup"><span data-stu-id="18140-136">Yes</span></span>      | <span data-ttu-id="18140-137">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="18140-137">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="18140-138">policy-id</span><span class="sxs-lookup"><span data-stu-id="18140-138">policy-id</span></span>   | <span data-ttu-id="18140-139">string</span><span class="sxs-lookup"><span data-stu-id="18140-139">string</span></span> | <span data-ttu-id="18140-140">Yes</span><span class="sxs-lookup"><span data-stu-id="18140-140">Yes</span></span>      | <span data-ttu-id="18140-141">İlkeyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="18140-141">A GUID-formatted string that identifies the policy.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="18140-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="18140-142">Request headers</span></span>

<span data-ttu-id="18140-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="18140-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="18140-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="18140-144">Request body</span></span>

<span data-ttu-id="18140-145">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="18140-145">None</span></span>

### <a name="request-example"></a><span data-ttu-id="18140-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="18140-146">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="18140-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="18140-147">REST response</span></span>

<span data-ttu-id="18140-148">Başarılı olursa yanıt, istenen [ConfigurationPolicy kaynağını](device-deployment-resources.md#configurationpolicy) içerir.</span><span class="sxs-lookup"><span data-stu-id="18140-148">If successful, the response contains the requested [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="18140-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="18140-149">Response success and error codes</span></span>

<span data-ttu-id="18140-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="18140-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="18140-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="18140-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="18140-152">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="18140-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="18140-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="18140-153">Response example</span></span>

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
