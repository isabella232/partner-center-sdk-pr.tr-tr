---
title: Yeni müşteri yapılandırma ilkesi oluşturma
description: Belirli bir müşteri İş Ortağı Merkezi yapılandırma ilkesi oluşturmak için api'leri kullanmayı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 05/23/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 530ff72862204bda093385252450f4eb81b63160
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973692"
---
# <a name="create-a-new-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="1763d-104">Belirtilen müşteri için yeni bir yapılandırma ilkesi oluşturma</span><span class="sxs-lookup"><span data-stu-id="1763d-104">Create a new configuration policy for the specified customer</span></span>

<span data-ttu-id="1763d-105">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek</span><span class="sxs-lookup"><span data-stu-id="1763d-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="1763d-106">Belirtilen müşteri için yeni bir yapılandırma ilkesi oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1763d-106">How to create a new configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1763d-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1763d-107">Prerequisites</span></span>

- <span data-ttu-id="1763d-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="1763d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1763d-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="1763d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1763d-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1763d-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1763d-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="1763d-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1763d-112">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="1763d-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1763d-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="1763d-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1763d-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="1763d-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1763d-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="1763d-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1763d-116">C\#</span><span class="sxs-lookup"><span data-stu-id="1763d-116">C\#</span></span>

<span data-ttu-id="1763d-117">Belirtilen müşteriye yeni bir yapılandırma ilkesi oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="1763d-117">To create a new configuration policy for the specified customer:</span></span>

1. <span data-ttu-id="1763d-118">Aşağıdaki kod parçacığında gösterildiği gibi yeni bir [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) nesnesi örneği oluşturma.</span><span class="sxs-lookup"><span data-stu-id="1763d-118">Instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="1763d-119">Ardından, belirtilen müşteri üzerinde işlemlere arabirim almak için müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="1763d-119">Then call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="1763d-120">Yapılandırma ilkesi toplama işlemlerine bir arabirim almak için [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="1763d-120">Retrieve the [**ConfigurationPolicies**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.configurationpolicies) property to get an interface to configuration policy collection operations.</span></span>

3. <span data-ttu-id="1763d-121">Yapılandırma ilkesi [**oluşturmak**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) için [**Create veya CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="1763d-121">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.genericoperations.ientitycreateoperations-2.createasync) method to create the configuration policy.</span></span>

### <a name="c-example"></a><span data-ttu-id="1763d-122">C \# örneği</span><span class="sxs-lookup"><span data-stu-id="1763d-122">C\# example</span></span>

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

<span data-ttu-id="1763d-123">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1763d-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1763d-124">**Project:** İş Ortağı Merkezi SDK'sı **Örnekleri Sınıfı:** CreateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="1763d-124">**Project**: Partner Center SDK Samples **Class**: CreateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1763d-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1763d-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1763d-126">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="1763d-126">Request syntax</span></span>

| <span data-ttu-id="1763d-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1763d-127">Method</span></span>   | <span data-ttu-id="1763d-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1763d-128">Request URI</span></span>                                                                              |
|----------|------------------------------------------------------------------------------------------|
| <span data-ttu-id="1763d-129">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="1763d-129">**POST**</span></span> | <span data-ttu-id="1763d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="1763d-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="1763d-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1763d-131">URI parameter</span></span>

<span data-ttu-id="1763d-132">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1763d-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="1763d-133">Ad</span><span class="sxs-lookup"><span data-stu-id="1763d-133">Name</span></span>        | <span data-ttu-id="1763d-134">Tür</span><span class="sxs-lookup"><span data-stu-id="1763d-134">Type</span></span>   | <span data-ttu-id="1763d-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1763d-135">Required</span></span> | <span data-ttu-id="1763d-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1763d-136">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1763d-137">customer-id</span><span class="sxs-lookup"><span data-stu-id="1763d-137">customer-id</span></span> | <span data-ttu-id="1763d-138">string</span><span class="sxs-lookup"><span data-stu-id="1763d-138">string</span></span> | <span data-ttu-id="1763d-139">Yes</span><span class="sxs-lookup"><span data-stu-id="1763d-139">Yes</span></span>      | <span data-ttu-id="1763d-140">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="1763d-140">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1763d-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1763d-141">Request headers</span></span>

<span data-ttu-id="1763d-142">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="1763d-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1763d-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1763d-143">Request body</span></span>

<span data-ttu-id="1763d-144">İstek gövdesi, aşağıdaki tabloda açıklandığı gibi yapılandırma ilkesi bilgilerine sahip bir nesne içermesi gerekir:</span><span class="sxs-lookup"><span data-stu-id="1763d-144">The request body must contain an object with the configuration policy information as described in the following table:</span></span>

| <span data-ttu-id="1763d-145">Ad</span><span class="sxs-lookup"><span data-stu-id="1763d-145">Name</span></span>           | <span data-ttu-id="1763d-146">Tür</span><span class="sxs-lookup"><span data-stu-id="1763d-146">Type</span></span>             | <span data-ttu-id="1763d-147">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1763d-147">Required</span></span> | <span data-ttu-id="1763d-148">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1763d-148">Description</span></span>                      |
|----------------|------------------|----------|----------------------------------|
| <span data-ttu-id="1763d-149">name</span><span class="sxs-lookup"><span data-stu-id="1763d-149">name</span></span>           | <span data-ttu-id="1763d-150">string</span><span class="sxs-lookup"><span data-stu-id="1763d-150">string</span></span>           | <span data-ttu-id="1763d-151">Yes</span><span class="sxs-lookup"><span data-stu-id="1763d-151">Yes</span></span>      | <span data-ttu-id="1763d-152">İlkenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="1763d-152">The friendly name of the policy.</span></span> |
| <span data-ttu-id="1763d-153">category</span><span class="sxs-lookup"><span data-stu-id="1763d-153">category</span></span>       | <span data-ttu-id="1763d-154">string</span><span class="sxs-lookup"><span data-stu-id="1763d-154">string</span></span>           | <span data-ttu-id="1763d-155">Yes</span><span class="sxs-lookup"><span data-stu-id="1763d-155">Yes</span></span>      | <span data-ttu-id="1763d-156">İlke kategorisi.</span><span class="sxs-lookup"><span data-stu-id="1763d-156">The policy category.</span></span>             |
| <span data-ttu-id="1763d-157">açıklama</span><span class="sxs-lookup"><span data-stu-id="1763d-157">description</span></span>    | <span data-ttu-id="1763d-158">dize</span><span class="sxs-lookup"><span data-stu-id="1763d-158">string</span></span>           | <span data-ttu-id="1763d-159">No</span><span class="sxs-lookup"><span data-stu-id="1763d-159">No</span></span>       | <span data-ttu-id="1763d-160">İlke açıklaması.</span><span class="sxs-lookup"><span data-stu-id="1763d-160">The policy description.</span></span>          |
| <span data-ttu-id="1763d-161">policySettings</span><span class="sxs-lookup"><span data-stu-id="1763d-161">policySettings</span></span> | <span data-ttu-id="1763d-162">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="1763d-162">array of strings</span></span> | <span data-ttu-id="1763d-163">Yes</span><span class="sxs-lookup"><span data-stu-id="1763d-163">Yes</span></span>      | <span data-ttu-id="1763d-164">İlke ayarları.</span><span class="sxs-lookup"><span data-stu-id="1763d-164">The policy settings.</span></span>             |

### <a name="request-example"></a><span data-ttu-id="1763d-165">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1763d-165">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="1763d-166">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1763d-166">REST response</span></span>

<span data-ttu-id="1763d-167">Başarılı olursa, yanıt gövdesi yeni ilke [için ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="1763d-167">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1763d-168">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1763d-168">Response success and error codes</span></span>

<span data-ttu-id="1763d-169">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="1763d-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1763d-170">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1763d-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1763d-171">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="1763d-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1763d-172">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1763d-172">Response example</span></span>

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
