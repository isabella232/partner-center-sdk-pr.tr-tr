---
title: Belirtilen müşteri için yeni bir yapılandırma ilkesini güncelleştirme
description: Belirtilen müşteri için belirtilen yapılandırma ilkesini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bf3b6f4db7516779c157b647725368ff0e4a570
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769791"
---
# <a name="update-a-configuration-policy-for-the-specified-customer"></a><span data-ttu-id="12346-103">Belirtilen müşteri için yeni bir yapılandırma ilkesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="12346-103">Update a configuration policy for the specified customer</span></span>

<span data-ttu-id="12346-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="12346-104">**Applies To**</span></span>

- <span data-ttu-id="12346-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="12346-105">Partner Center</span></span>
- <span data-ttu-id="12346-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="12346-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="12346-107">Belirtilen müşteri için belirtilen yapılandırma ilkesini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="12346-107">How to update the specified configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="12346-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="12346-108">Prerequisites</span></span>

- <span data-ttu-id="12346-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="12346-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="12346-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="12346-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="12346-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="12346-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="12346-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="12346-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="12346-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="12346-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="12346-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="12346-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="12346-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="12346-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="12346-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="12346-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="12346-117">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="12346-117">The policy identifier.</span></span>

## <a name="c"></a><span data-ttu-id="12346-118">C\#</span><span class="sxs-lookup"><span data-stu-id="12346-118">C\#</span></span>

<span data-ttu-id="12346-119">Belirtilen müşteri için varolan bir yapılandırma ilkesini güncelleştirmek üzere, aşağıdaki kod parçacığında gösterildiği gibi yeni bir [**Configurationpolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="12346-119">To update an existing configuration policy for the specified customer, instantiate a new [**ConfigurationPolicy**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.configurationpolicy) object as shown in the following code snippet.</span></span> <span data-ttu-id="12346-120">Bu yeni nesnedeki değerler varolan nesnede karşılık gelen değerleri değiştirir.</span><span class="sxs-lookup"><span data-stu-id="12346-120">The values in this new object replace the corresponding values in the existing object.</span></span> <span data-ttu-id="12346-121">Ardından, belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="12346-121">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="12346-122">Ardından, belirtilen ilke için yapılandırma ilkesi işlemlerine bir arabirim almak üzere ilke KIMLIĞIYLE [**Configurationpolicies. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="12346-122">Next, call the [**ConfigurationPolicies.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicycollection.byid) method with the policy ID to retrieve an interface to configuration policy operations for the specified policy.</span></span> <span data-ttu-id="12346-123">Son olarak, yapılandırma ilkesini güncelleştirmek için [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) veya [**patchasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="12346-123">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.iconfigurationpolicy.patchasync) method to update the configuration policy.</span></span>

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

<span data-ttu-id="12346-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="12346-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="12346-125">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdateConfigurationPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="12346-125">**Project**: Partner Center SDK Samples **Class**: UpdateConfigurationPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="12346-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="12346-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="12346-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="12346-127">Request syntax</span></span>

| <span data-ttu-id="12346-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="12346-128">Method</span></span>  | <span data-ttu-id="12346-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="12346-129">Request URI</span></span>                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="12346-130">**PUT**</span><span class="sxs-lookup"><span data-stu-id="12346-130">**PUT**</span></span> | <span data-ttu-id="12346-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/policies/{Policy-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="12346-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/policies/{policy-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="12346-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="12346-132">URI parameter</span></span>

<span data-ttu-id="12346-133">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="12346-133">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="12346-134">Ad</span><span class="sxs-lookup"><span data-stu-id="12346-134">Name</span></span>        | <span data-ttu-id="12346-135">Tür</span><span class="sxs-lookup"><span data-stu-id="12346-135">Type</span></span>   | <span data-ttu-id="12346-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="12346-136">Required</span></span> | <span data-ttu-id="12346-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="12346-137">Description</span></span>                                                   |
|-------------|--------|----------|---------------------------------------------------------------|
| <span data-ttu-id="12346-138">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="12346-138">customer-id</span></span> | <span data-ttu-id="12346-139">string</span><span class="sxs-lookup"><span data-stu-id="12346-139">string</span></span> | <span data-ttu-id="12346-140">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-140">Yes</span></span>      | <span data-ttu-id="12346-141">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="12346-141">A GUID-formatted string that identifies the customer.</span></span>         |
| <span data-ttu-id="12346-142">ilke kimliği</span><span class="sxs-lookup"><span data-stu-id="12346-142">policy-id</span></span>   | <span data-ttu-id="12346-143">string</span><span class="sxs-lookup"><span data-stu-id="12346-143">string</span></span> | <span data-ttu-id="12346-144">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-144">Yes</span></span>      | <span data-ttu-id="12346-145">Güncelleştirilecek ilkeyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="12346-145">A GUID-formatted string that identifies the policy to update.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="12346-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="12346-146">Request headers</span></span>

<span data-ttu-id="12346-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="12346-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="12346-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="12346-148">Request body</span></span>

<span data-ttu-id="12346-149">İstek gövdesi, ilke bilgilerini sağlayan bir nesne içermelidir.</span><span class="sxs-lookup"><span data-stu-id="12346-149">The request body must contain an object that provides the policy information.</span></span>

| <span data-ttu-id="12346-150">Ad</span><span class="sxs-lookup"><span data-stu-id="12346-150">Name</span></span>            | <span data-ttu-id="12346-151">Tür</span><span class="sxs-lookup"><span data-stu-id="12346-151">Type</span></span>             | <span data-ttu-id="12346-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="12346-152">Required</span></span> | <span data-ttu-id="12346-153">Güncelleştirilebilir</span><span class="sxs-lookup"><span data-stu-id="12346-153">Updatable</span></span> | <span data-ttu-id="12346-154">Description</span><span class="sxs-lookup"><span data-stu-id="12346-154">Description</span></span>                                                                                                                                              |
|-----------------|------------------|----------|-----------|----------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="12346-155">kimlik</span><span class="sxs-lookup"><span data-stu-id="12346-155">id</span></span>              | <span data-ttu-id="12346-156">string</span><span class="sxs-lookup"><span data-stu-id="12346-156">string</span></span>           | <span data-ttu-id="12346-157">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-157">Yes</span></span>      | <span data-ttu-id="12346-158">Hayır</span><span class="sxs-lookup"><span data-stu-id="12346-158">No</span></span>        | <span data-ttu-id="12346-159">İlkeyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="12346-159">The GUID-formatted string that identifies the policy.</span></span>                                                                                                    |
| <span data-ttu-id="12346-160">name</span><span class="sxs-lookup"><span data-stu-id="12346-160">name</span></span>            | <span data-ttu-id="12346-161">string</span><span class="sxs-lookup"><span data-stu-id="12346-161">string</span></span>           | <span data-ttu-id="12346-162">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-162">Yes</span></span>      | <span data-ttu-id="12346-163">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-163">Yes</span></span>       | <span data-ttu-id="12346-164">İlkenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="12346-164">The friendly name of the policy.</span></span>                                                                                                                         |
| <span data-ttu-id="12346-165">category</span><span class="sxs-lookup"><span data-stu-id="12346-165">category</span></span>        | <span data-ttu-id="12346-166">string</span><span class="sxs-lookup"><span data-stu-id="12346-166">string</span></span>           | <span data-ttu-id="12346-167">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-167">Yes</span></span>      | <span data-ttu-id="12346-168">Hayır</span><span class="sxs-lookup"><span data-stu-id="12346-168">No</span></span>        | <span data-ttu-id="12346-169">İlke kategorisi.</span><span class="sxs-lookup"><span data-stu-id="12346-169">The policy category.</span></span>                                                                                                                                     |
| <span data-ttu-id="12346-170">açıklama</span><span class="sxs-lookup"><span data-stu-id="12346-170">description</span></span>     | <span data-ttu-id="12346-171">dize</span><span class="sxs-lookup"><span data-stu-id="12346-171">string</span></span>           | <span data-ttu-id="12346-172">No</span><span class="sxs-lookup"><span data-stu-id="12346-172">No</span></span>       | <span data-ttu-id="12346-173">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-173">Yes</span></span>       | <span data-ttu-id="12346-174">İlke açıklaması.</span><span class="sxs-lookup"><span data-stu-id="12346-174">The policy description.</span></span>                                                                                                                                  |
| <span data-ttu-id="12346-175">devicesAssigned</span><span class="sxs-lookup"><span data-stu-id="12346-175">devicesAssigned</span></span> | <span data-ttu-id="12346-176">sayı</span><span class="sxs-lookup"><span data-stu-id="12346-176">number</span></span>           | <span data-ttu-id="12346-177">Hayır</span><span class="sxs-lookup"><span data-stu-id="12346-177">No</span></span>       | <span data-ttu-id="12346-178">Hayır</span><span class="sxs-lookup"><span data-stu-id="12346-178">No</span></span>        | <span data-ttu-id="12346-179">Cihaz sayısı.</span><span class="sxs-lookup"><span data-stu-id="12346-179">The number of devices.</span></span>                                                                                                                                   |
| <span data-ttu-id="12346-180">policySettings</span><span class="sxs-lookup"><span data-stu-id="12346-180">policySettings</span></span>  | <span data-ttu-id="12346-181">dize dizisi</span><span class="sxs-lookup"><span data-stu-id="12346-181">array of strings</span></span> | <span data-ttu-id="12346-182">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-182">Yes</span></span>      | <span data-ttu-id="12346-183">Yes</span><span class="sxs-lookup"><span data-stu-id="12346-183">Yes</span></span>       | <span data-ttu-id="12346-184">İlke ayarları: "none", " \_ OEM \_ ön yüklemelerini kaldır", "OOBE \_ user \_ yerel yönetici değil", " \_ \_ \_ hızlı ayarları atla", "OEM kaydını atla", " \_ \_ \_ EULA 'yı atla \_ ".</span><span class="sxs-lookup"><span data-stu-id="12346-184">The policy settings: "none","remove\_oem\_preinstalls","oobe\_user\_not\_local\_admin","skip\_express\_settings","skip \_oem\_registration,"skip\_eula".</span></span> |

### <a name="request-example"></a><span data-ttu-id="12346-185">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="12346-185">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="12346-186">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="12346-186">REST response</span></span>

<span data-ttu-id="12346-187">Başarılı olursa, yanıt gövdesi yeni ilke için [Configurationpolicy](device-deployment-resources.md#configurationpolicy) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="12346-187">If successful, the response body contains the [ConfigurationPolicy](device-deployment-resources.md#configurationpolicy) resource for the new policy.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="12346-188">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="12346-188">Response success and error codes</span></span>

<span data-ttu-id="12346-189">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="12346-189">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="12346-190">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="12346-190">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="12346-191">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="12346-191">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="12346-192">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="12346-192">Response example</span></span>

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
