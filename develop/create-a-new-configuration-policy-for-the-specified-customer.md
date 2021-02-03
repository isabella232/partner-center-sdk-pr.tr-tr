---
title: Yeni bir müşteri yapılandırma ilkesi oluştur
description: Belirli bir müşteri için yeni bir yapılandırma ilkesi oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 21a0bfde7f931371ff09d6c27de0281a4ed3b3cb
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770165"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="23183-104">Belirtilen müşteri için yeni bir yapılandırma ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="23183-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="23183-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="23183-105">**Applies to:**</span></span>

- <span data-ttu-id="23183-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="23183-106">Partner Center</span></span>
- <span data-ttu-id="23183-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="23183-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="23183-108">Belirtilen müşteri için yeni bir yapılandırma ilkesi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="23183-108">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23183-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="23183-109">Prerequisites</span></span>

- <span data-ttu-id="23183-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="23183-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="23183-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="23183-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="23183-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="23183-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="23183-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="23183-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="23183-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="23183-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="23183-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="23183-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="23183-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="23183-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="23183-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="23183-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="23183-118">C\#</span><span class="sxs-lookup"><span data-stu-id="23183-118">C\#</span></span>

<span data-ttu-id="23183-119">Belirtilen müşteri için yeni bir yapılandırma ilkesi oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="23183-119">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="23183-120">Aşağıdaki kod parçacığında gösterildiği gibi yeni bir [**Configurationpolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="23183-120">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="23183-121">Ardından, belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="23183-121">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="23183-122">Yapılandırma ilkesi toplama işlemlerine bir arabirim almak için [**Configurationpolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="23183-122">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="23183-123">Yapılandırma ilkesini oluşturmak için [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="23183-123">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="23183-124">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="23183-124">C\# example</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var configurationPolicyToCreate = new ConfigurationPolicy
{
    Name = "Test Config Policy",
    Description = "This configuration policy is created by the SDK samples",
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.SkipEula }
};

var createdConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.Create(configurationPolicyToCreate);
```

<span data-ttu-id="23183-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="23183-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="23183-126">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="23183-126">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="23183-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="23183-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="23183-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="23183-128">Request syntax</span></span>

| <span data-ttu-id="23183-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="23183-129">Method</span></span>   | <span data-ttu-id="23183-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="23183-130">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="23183-131">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="23183-131">**POST**</span></span> | <span data-ttu-id="23183-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies http/1.1</span><span class="sxs-lookup"><span data-stu-id="23183-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="23183-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="23183-133">URI parameter</span></span>

<span data-ttu-id="23183-134">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="23183-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="23183-135">Ad</span><span class="sxs-lookup"><span data-stu-id="23183-135">Name</span></span>        | <span data-ttu-id="23183-136">Tür</span><span class="sxs-lookup"><span data-stu-id="23183-136">Type</span></span>   | <span data-ttu-id="23183-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="23183-137">Required</span></span> | <span data-ttu-id="23183-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23183-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="23183-139">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="23183-139">customer-id</span></span> | <span data-ttu-id="23183-140">string</span><span class="sxs-lookup"><span data-stu-id="23183-140">string</span></span> | <span data-ttu-id="23183-141">Yes</span><span class="sxs-lookup"><span data-stu-id="23183-141">Yes</span></span>      | <span data-ttu-id="23183-142">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="23183-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="23183-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="23183-143">Request headers</span></span>

<span data-ttu-id="23183-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="23183-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="23183-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="23183-145">Request body</span></span>

<span data-ttu-id="23183-146">İstek gövdesi, aşağıdaki tabloda açıklandığı gibi yapılandırma ilkesi bilgilerini içeren bir nesne içermelidir:</span><span class="sxs-lookup"><span data-stu-id="23183-146">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="23183-147">Ad</span><span class="sxs-lookup"><span data-stu-id="23183-147">Name</span></span>           | <span data-ttu-id="23183-148">Tür</span><span class="sxs-lookup"><span data-stu-id="23183-148">Type</span></span>             | <span data-ttu-id="23183-149">Gerekli</span><span class="sxs-lookup"><span data-stu-id="23183-149">Required</span></span> | <span data-ttu-id="23183-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23183-150">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="23183-151">name</span><span class="sxs-lookup"><span data-stu-id="23183-151">name</span></span>           | <span data-ttu-id="23183-152">string</span><span class="sxs-lookup"><span data-stu-id="23183-152">string</span></span>           | <span data-ttu-id="23183-153">Yes</span><span class="sxs-lookup"><span data-stu-id="23183-153">Yes</span></span>      | <span data-ttu-id="23183-154">İlkenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="23183-154">The friendly name of the policy.</span></span> |
| <span data-ttu-id="23183-155">category</span><span class="sxs-lookup"><span data-stu-id="23183-155">category</span></span>       | <span data-ttu-id="23183-156">string</span><span class="sxs-lookup"><span data-stu-id="23183-156">string</span></span>           | <span data-ttu-id="23183-157">Yes</span><span class="sxs-lookup"><span data-stu-id="23183-157">Yes</span></span>      | <span data-ttu-id="23183-158">İlke kategorisi.</span><span class="sxs-lookup"><span data-stu-id="23183-158">The policy category.</span></span>             |
| <span data-ttu-id="23183-159">açıklama</span><span class="sxs-lookup"><span data-stu-id="23183-159">description</span></span>    | <span data-ttu-id="23183-160">dize</span><span class="sxs-lookup"><span data-stu-id="23183-160">string</span></span>           | <span data-ttu-id="23183-161">No</span><span class="sxs-lookup"><span data-stu-id="23183-161">No</span></span>       | <span data-ttu-id="23183-162">İlke açıklaması.</span><span class="sxs-lookup"><span data-stu-id="23183-162">The policy description.</span></span>          |
| <span data-ttu-id="23183-163">policySettings</span><span class="sxs-lookup"><span data-stu-id="23183-163">policySettings</span></span> | <span data-ttu-id="23183-164">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="23183-164">array of strings</span></span> | <span data-ttu-id="23183-165">Yes</span><span class="sxs-lookup"><span data-stu-id="23183-165">Yes</span></span>      | <span data-ttu-id="23183-166">İlke ayarları.</span><span class="sxs-lookup"><span data-stu-id="23183-166">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="23183-167">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="23183-167">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com//v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 212
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="23183-168">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="23183-168">REST response</span></span>

<span data-ttu-id="23183-169">Başarılı olursa, yanıt gövdesi yeni ilke için [Configurationpolicy](device-deployment-resources.md#configurationpolicy) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="23183-169">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="23183-170">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="23183-170">Response success and error codes</span></span>

<span data-ttu-id="23183-171">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="23183-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="23183-172">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="23183-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="23183-173">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="23183-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="23183-174">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="23183-174">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 404
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4beda413-74fc-4839-b74f-f580c353ab45
MS-RequestId: 0dfadf74-aa66-49ed-9a67-b3b78d9297cc
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:07:36 GMT

{
    "id": "40cdb858-edcc-44d7-9083-d6a36d43bd3f",
    "name": "Windows 10 Enterprise E5",
    "category": "o_o_b_e",
    "description": "test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["oobe_user_not_local_admin", "skip_express_settings"],
    "createdDate": "2017-07-25T18:07:36",
    "lastModifiedDate": "2017-07-25T18:07:36",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
