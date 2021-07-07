---
title: İlke ile cihaz listesini güncelleştirme
description: Belirtilen müşteri için bir yapılandırma ilkesiyle bir cihaz listesini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 35b35873eb253b0929bfc01662b0beb9b31d0c6b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530081"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="ca58c-103">İlke ile cihaz listesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="ca58c-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="ca58c-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ca58c-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="ca58c-105">Belirtilen müşteri için bir yapılandırma ilkesiyle bir cihaz listesini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="ca58c-105">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ca58c-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ca58c-106">Prerequisites</span></span>

- <span data-ttu-id="ca58c-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ca58c-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="ca58c-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="ca58c-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="ca58c-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="ca58c-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="ca58c-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ca58c-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="ca58c-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="ca58c-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ca58c-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="ca58c-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ca58c-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="ca58c-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ca58c-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="ca58c-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="ca58c-115">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="ca58c-115">The policy identifier.</span></span>

- <span data-ttu-id="ca58c-116">Güncelleştirilecek cihazların cihaz tanımlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="ca58c-116">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="ca58c-117">C\#</span><span class="sxs-lookup"><span data-stu-id="ca58c-117">C\#</span></span>

<span data-ttu-id="ca58c-118">Belirtilen yapılandırma ilkesiyle bir cihaz listesini güncelleştirmek için ilk olarak [KeyValuePair/DotNet/API/System. Collections. Generic. KeyValuePair -2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) türünde bir [list/DotNet/api/System. Collections. Generic. List -1) oluşturun ve aşağıdaki kod örneğinde gösterildiği gibi, uygulanacak ilkeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="ca58c-118">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="ca58c-119">İlkenin ilke tanımlayıcısına ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="ca58c-119">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="ca58c-120">Ardından, ilke ile, her bir cihaz için, cihaz tanımlayıcısını ve uygulanacak ilkeyi içeren listeyi belirterek ilkeyle güncelleştirileceği [**cihaz**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) nesnelerinin bir listesini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ca58c-120">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="ca58c-121">Ardından, bir [**Devicepolicyupdaterequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) nesnesi örneği oluşturun ve [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) özelliğini cihaz nesneleri listesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="ca58c-121">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="ca58c-122">Cihaz İlkesi güncelleştirme isteğini işlemek için, belirtilen müşterideki işlemlere bir arabirim almak üzere [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini Müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="ca58c-122">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="ca58c-123">Ardından, müşteri cihaz koleksiyonu işlemlerine bir arabirim almak için [**Devicepolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="ca58c-123">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="ca58c-124">Son olarak, cihazları ilkeyle güncelleştirmek için DevicePolicyUpdateRequest nesnesiyle birlikte [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="ca58c-124">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedConfigurationPolicyId;
string selectedDeviceId;

// Indicate the policy to apply to the list of devices.
List<KeyValuePair<PolicyCategory, string>>
    policyToBeAdded = new List<KeyValuePair<PolicyCategory, string>>
{
    new KeyValuePair<PolicyCategory, string>
        (PolicyCategory.OOBE, selectedConfigurationPolicyId)
};

// Create a list of devices to be updated with a policy.
List<Device> devices = new List<Device>
{
    new Device
    {
        Id = selectedDeviceId,
        Policies=policyToBeAdded
    }
};

// Instantiate a DevicePolicyUpdateRequest object.
DevicePolicyUpdateRequest
    devicePolicyUpdateRequest = new DevicePolicyUpdateRequest
{
    Devices = devices
};

// Process the DevicePolicyUpdateRequest.
var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DevicePolicy.Update(devicePolicyUpdateRequest);
```

<span data-ttu-id="ca58c-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="ca58c-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="ca58c-126">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: updatedevicespolicy. cs</span><span class="sxs-lookup"><span data-stu-id="ca58c-126">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="ca58c-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="ca58c-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ca58c-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="ca58c-128">Request syntax</span></span>

| <span data-ttu-id="ca58c-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="ca58c-129">Method</span></span>    | <span data-ttu-id="ca58c-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="ca58c-130">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="ca58c-131">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="ca58c-131">**PATCH**</span></span> | <span data-ttu-id="ca58c-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicepolicyupdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="ca58c-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="ca58c-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="ca58c-133">URI parameter</span></span>

<span data-ttu-id="ca58c-134">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca58c-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="ca58c-135">Ad</span><span class="sxs-lookup"><span data-stu-id="ca58c-135">Name</span></span>        | <span data-ttu-id="ca58c-136">Tür</span><span class="sxs-lookup"><span data-stu-id="ca58c-136">Type</span></span>   | <span data-ttu-id="ca58c-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="ca58c-137">Required</span></span> | <span data-ttu-id="ca58c-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="ca58c-138">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="ca58c-139">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="ca58c-139">customer-id</span></span> | <span data-ttu-id="ca58c-140">string</span><span class="sxs-lookup"><span data-stu-id="ca58c-140">string</span></span> | <span data-ttu-id="ca58c-141">Yes</span><span class="sxs-lookup"><span data-stu-id="ca58c-141">Yes</span></span>      | <span data-ttu-id="ca58c-142">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="ca58c-142">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="ca58c-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="ca58c-143">Request headers</span></span>

<span data-ttu-id="ca58c-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="ca58c-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="ca58c-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="ca58c-145">Request body</span></span>

<span data-ttu-id="ca58c-146">İstek gövdesi bir [Devicepolicyupdaterequest](device-deployment-resources.md#devicepolicyupdaterequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="ca58c-146">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="ca58c-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="ca58c-147">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/DevicePolicyUpdates HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 363
Expect: 100-continue
Connection: Keep-Alive

{
    "Devices": [{
            "Id": "9993-8627-3608-6844-6369-4361-72",
            "SerialNumber": null,
            "ProductKey": null,
            "HardwareHash": null,
            "Policies": [{
                    "Key": "o_o_b_e",
                    "Value": "15a04610-9229-4e80-94e0-0e826a09c9e2"
                }
            ],
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DevicePolicyUpdateRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="ca58c-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="ca58c-148">REST response</span></span>

<span data-ttu-id="ca58c-149">Başarılı olursa, yanıt, bu toplu işlemin durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="ca58c-149">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="ca58c-150">Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="ca58c-150">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ca58c-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ca58c-151">Response success and error codes</span></span>

<span data-ttu-id="ca58c-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="ca58c-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ca58c-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ca58c-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ca58c-154">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="ca58c-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="ca58c-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="ca58c-155">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/a15f3996-620a-4404-9f1f-4c2de78de0de
MS-CorrelationId: 49b1e7b2-82e7-4403-b63b-8765269b448d
MS-RequestId: 1b658428-5afa-46d4-af86-c9c6af5634e2
MS-CV: rCXyd8Z/lUSxUd0P.0
MS-ServerId: 020021921
Date: Thu, 28 Sep 2017 21:33:05 GMT
```
