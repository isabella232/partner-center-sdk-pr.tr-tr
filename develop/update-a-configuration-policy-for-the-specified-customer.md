---
title: Belirtilen müşteri için yeni bir yapılandırma ilkesini güncelleştirme
description: Belirtilen müşteri için belirtilen yapılandırma ilkesini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5e008f41a44f2b7cf3ddfd705505175c69bbad38
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530250"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="aa255-103">Belirtilen müşteri için yeni bir yapılandırma ilkesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="aa255-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="aa255-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="aa255-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="aa255-105">Belirtilen müşteri için belirtilen yapılandırma ilkesini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="aa255-105">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="aa255-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="aa255-106">Prerequisites</span></span>

- <span data-ttu-id="aa255-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="aa255-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="aa255-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="aa255-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="aa255-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="aa255-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="aa255-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="aa255-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="aa255-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="aa255-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="aa255-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="aa255-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="aa255-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="aa255-113">On the customer's Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="aa255-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="aa255-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="aa255-115">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="aa255-115">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="aa255-116">C\#</span><span class="sxs-lookup"><span data-stu-id="aa255-116">C\#</span></span>

<span data-ttu-id="aa255-117">Belirtilen müşteri için varolan bir yapılandırma ilkesini güncelleştirmek üzere, aşağıdaki kod parçacığında gösterildiği gibi yeni bir [**Configurationpolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="aa255-117">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="aa255-118">Bu yeni nesnedeki değerler varolan nesnede karşılık gelen değerleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="aa255-118">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="aa255-119">Ardından, belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="aa255-119">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="aa255-120">Ardından, belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke KIMLIĞIYLE [**Configurationpolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="aa255-120">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="aa255-121">Son olarak, yapılandırma ilkesini güncelleştirmek için [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) veya [**patchasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="aa255-121">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;

ConfigurationPolicy configPolicyToBeUpdated = new ConfigurationPolicy()
{
    Name= "Test Config Policy",
    Id = selectedConfigurationPolicyId,
    PolicySettings = new List<PolicySettingsType>() {
        PolicySettingsType.OobeUserNotLocalAdmin,
        PolicySettingsType.RemoveOemPreinstalls }
};

ConfigurationPolicy updatedConfigurationPolicy =
    partnerOperations.Customers.ById(selectedCustomerId).ConfigurationPolicies.ById(selectedConfigurationPolicyId).Patch(configPolicyToBeUpdated);
```

<span data-ttu-id="aa255-122">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="aa255-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="aa255-123">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: updateconfigurationpolicy. cs</span><span class="sxs-lookup"><span data-stu-id="aa255-123">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="aa255-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="aa255-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="aa255-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="aa255-125">Request syntax</span></span>

| <span data-ttu-id="aa255-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="aa255-126">Method</span></span>  | <span data-ttu-id="aa255-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="aa255-127">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="aa255-128">**PUT**</span><span class="sxs-lookup"><span data-stu-id="aa255-128">**PUT**</span></span> | <span data-ttu-id="aa255-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="aa255-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="aa255-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="aa255-130">URI parameter</span></span>

<span data-ttu-id="aa255-131">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="aa255-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="aa255-132">Ad</span><span class="sxs-lookup"><span data-stu-id="aa255-132">Name</span></span>        | <span data-ttu-id="aa255-133">Tür</span><span class="sxs-lookup"><span data-stu-id="aa255-133">Type</span></span>   | <span data-ttu-id="aa255-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="aa255-134">Required</span></span> | <span data-ttu-id="aa255-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aa255-135">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="aa255-136">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="aa255-136">customer-id</span></span> | <span data-ttu-id="aa255-137">string</span><span class="sxs-lookup"><span data-stu-id="aa255-137">string</span></span> | <span data-ttu-id="aa255-138">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-138">Yes</span></span>      | <span data-ttu-id="aa255-139">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="aa255-139">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="aa255-140">ilke kimliği</span><span class="sxs-lookup"><span data-stu-id="aa255-140">policy-id</span></span>   | <span data-ttu-id="aa255-141">string</span><span class="sxs-lookup"><span data-stu-id="aa255-141">string</span></span> | <span data-ttu-id="aa255-142">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-142">Yes</span></span>      | <span data-ttu-id="aa255-143">Güncelleştirilecek ilkeyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="aa255-143">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="aa255-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="aa255-144">Request headers</span></span>

<span data-ttu-id="aa255-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="aa255-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="aa255-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="aa255-146">Request body</span></span>

<span data-ttu-id="aa255-147">İstek gövdesi, ilke bilgilerini sağlayan bir nesne içermelidir.</span><span class="sxs-lookup"><span data-stu-id="aa255-147">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="aa255-148">Ad</span><span class="sxs-lookup"><span data-stu-id="aa255-148">Name</span></span>            | <span data-ttu-id="aa255-149">Tür</span><span class="sxs-lookup"><span data-stu-id="aa255-149">Type</span></span>             | <span data-ttu-id="aa255-150">Gerekli</span><span class="sxs-lookup"><span data-stu-id="aa255-150">Required</span></span> | <span data-ttu-id="aa255-151">Güncelleştirilebilir</span><span class="sxs-lookup"><span data-stu-id="aa255-151">Updatable</span></span> | <span data-ttu-id="aa255-152">Açıklama</span><span class="sxs-lookup"><span data-stu-id="aa255-152">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="aa255-153">kimlik</span><span class="sxs-lookup"><span data-stu-id="aa255-153">id</span></span>              | <span data-ttu-id="aa255-154">string</span><span class="sxs-lookup"><span data-stu-id="aa255-154">string</span></span>           | <span data-ttu-id="aa255-155">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-155">Yes</span></span>      | <span data-ttu-id="aa255-156">Hayır</span><span class="sxs-lookup"><span data-stu-id="aa255-156">No</span></span>        | <span data-ttu-id="aa255-157">İlkeyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="aa255-157">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="aa255-158">name</span><span class="sxs-lookup"><span data-stu-id="aa255-158">name</span></span>            | <span data-ttu-id="aa255-159">string</span><span class="sxs-lookup"><span data-stu-id="aa255-159">string</span></span>           | <span data-ttu-id="aa255-160">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-160">Yes</span></span>      | <span data-ttu-id="aa255-161">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-161">Yes</span></span>       | <span data-ttu-id="aa255-162">İlkenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="aa255-162">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="aa255-163">category</span><span class="sxs-lookup"><span data-stu-id="aa255-163">category</span></span>        | <span data-ttu-id="aa255-164">string</span><span class="sxs-lookup"><span data-stu-id="aa255-164">string</span></span>           | <span data-ttu-id="aa255-165">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-165">Yes</span></span>      | <span data-ttu-id="aa255-166">Hayır</span><span class="sxs-lookup"><span data-stu-id="aa255-166">No</span></span>        | <span data-ttu-id="aa255-167">İlke kategorisi.</span><span class="sxs-lookup"><span data-stu-id="aa255-167">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="aa255-168">açıklama</span><span class="sxs-lookup"><span data-stu-id="aa255-168">description</span></span>     | <span data-ttu-id="aa255-169">dize</span><span class="sxs-lookup"><span data-stu-id="aa255-169">string</span></span>           | <span data-ttu-id="aa255-170">Hayır</span><span class="sxs-lookup"><span data-stu-id="aa255-170">No</span></span>       | <span data-ttu-id="aa255-171">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-171">Yes</span></span>       | <span data-ttu-id="aa255-172">İlke açıklaması.</span><span class="sxs-lookup"><span data-stu-id="aa255-172">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="aa255-173">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="aa255-173">devicesAssigned</span></span> | <span data-ttu-id="aa255-174">sayı</span><span class="sxs-lookup"><span data-stu-id="aa255-174">number</span></span>           | <span data-ttu-id="aa255-175">Hayır</span><span class="sxs-lookup"><span data-stu-id="aa255-175">No</span></span>       | <span data-ttu-id="aa255-176">Hayır</span><span class="sxs-lookup"><span data-stu-id="aa255-176">No</span></span>        | <span data-ttu-id="aa255-177">Cihaz sayısı.</span><span class="sxs-lookup"><span data-stu-id="aa255-177">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="aa255-178">policySettings</span><span class="sxs-lookup"><span data-stu-id="aa255-178">policySettings</span></span>  | <span data-ttu-id="aa255-179">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="aa255-179">array of strings</span></span> | <span data-ttu-id="aa255-180">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-180">Yes</span></span>      | <span data-ttu-id="aa255-181">Yes</span><span class="sxs-lookup"><span data-stu-id="aa255-181">Yes</span></span>       | <span data-ttu-id="aa255-182">İlke ayarları: "none", " \_ OEM \_ ön yüklemelerini kaldır", "OOBE \_ user \_ yerel yönetici değil", " \_ \_ \_ hızlı ayarları atla", "OEM kaydını atla", " \_ \_ \_ EULA 'yı atla \_ ".</span><span class="sxs-lookup"><span data-stu-id="aa255-182">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="aa255-183">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="aa255-183">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/policies/56edf752-ee77-4fd8-b7f5-df1f74a3a9ac HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 256
Content-Type: application/json
Host: api.partnercenter.microsoft.com

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"]
}
```

## <a name="rest-response"></a><span data-ttu-id="aa255-184">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="aa255-184">REST response</span></span>

<span data-ttu-id="aa255-185">Başarılı olursa, yanıt gövdesi yeni ilke için [Configurationpolicy](device-deployment-resources.md#configurationpolicy) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="aa255-185">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="aa255-186">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="aa255-186">Response success and error codes</span></span>

<span data-ttu-id="aa255-187">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="aa255-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="aa255-188">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="aa255-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="aa255-189">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="aa255-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="aa255-190">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="aa255-190">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 421
Content-Type: application/json; charset=utf-8
MS-CorrelationId: f9fd5973-6ad8-4585-aadc-f2b0443fe27b
MS-RequestId: cb1fa1f3-1381-45d9-99c5-511e5d3efa7c
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 18:10:29 GMT

{
    "id": "56edf752-ee77-4fd8-b7f5-df1f74a3a9ac",
    "name": "Windows test policy",
    "category": "o_o_b_e",
    "description": "Test policy creation from API",
    "devicesAssigned": 0,
    "policySettings": ["skip_express_settings"],
    "createdDate": "2017-01-01T00:00:00",
    "lastModifiedDate": "2017-07-25T18:10:15",
    "attributes": {
        "objectType": "ConfigurationPolicy"
    }
}
```
