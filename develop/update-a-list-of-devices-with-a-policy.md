---
title: İlke ile cihaz listesini güncelleştirme
description: Belirtilen müşteri için bir yapılandırma ilkesiyle bir cihaz listesini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 04c2ef33116335db40bd2934dc7e33d57f015097
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769754"
---
# <a name="update-a-list-of-devices-with-a-policy"></a><span data-ttu-id="93860-103">İlke ile cihaz listesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="93860-103">Update a list of devices with a policy</span></span>

<span data-ttu-id="93860-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="93860-104">**Applies To**</span></span>

- <span data-ttu-id="93860-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="93860-105">Partner Center</span></span>
- <span data-ttu-id="93860-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="93860-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="93860-107">Belirtilen müşteri için bir yapılandırma ilkesiyle bir cihaz listesini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="93860-107">How to update a list of devices with a configuration policy for the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93860-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="93860-108">Prerequisites</span></span>

- <span data-ttu-id="93860-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="93860-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="93860-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="93860-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="93860-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="93860-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="93860-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93860-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="93860-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="93860-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="93860-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="93860-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="93860-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="93860-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="93860-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="93860-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="93860-117">İlke tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="93860-117">The policy identifier.</span></span>

- <span data-ttu-id="93860-118">Güncelleştirilecek cihazların cihaz tanımlayıcıları.</span><span class="sxs-lookup"><span data-stu-id="93860-118">The device identifiers of the devices to update.</span></span>

## <a name="c"></a><span data-ttu-id="93860-119">C\#</span><span class="sxs-lookup"><span data-stu-id="93860-119">C\#</span></span>

<span data-ttu-id="93860-120">Belirtilen yapılandırma ilkesiyle bir cihaz listesini güncelleştirmek için ilk olarak [KeyValuePair/DotNet/API/System. Collections. Generic. KeyValuePair -2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)String) türünde bir [list/DotNet/api/System. Collections. Generic. List -1) oluşturun ve aşağıdaki kod örneğinde gösterildiği gibi, uygulanacak ilkeyi ekleyin.</span><span class="sxs-lookup"><span data-stu-id="93860-120">To update a list of devices with the specified configuration policy, first, instantiate a [List/dotnet/api/system.collections.generic.list-1) of type [KeyValuePair/dotnet/api/system.collections.generic.keyvaluepair-2)[**(PolicyCategory,**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.policycategory)string) and add the policy to apply, as shown in the following code example.</span></span> <span data-ttu-id="93860-121">İlkenin ilke tanımlayıcısına ihtiyacınız olacak.</span><span class="sxs-lookup"><span data-stu-id="93860-121">You will need the policy identifier of the policy.</span></span>

<span data-ttu-id="93860-122">Ardından, ilke ile, her bir cihaz için, cihaz tanımlayıcısını ve uygulanacak ilkeyi içeren listeyi belirterek ilkeyle güncelleştirileceği [**cihaz**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) nesnelerinin bir listesini oluşturun.</span><span class="sxs-lookup"><span data-stu-id="93860-122">Then, create a list of [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) objects to be updated with the policy, specifying the device identifier and the list that contains the policy to apply, for each device.</span></span> <span data-ttu-id="93860-123">Ardından, bir [**Devicepolicyupdaterequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) nesnesi örneği oluşturun ve [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) özelliğini cihaz nesneleri listesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="93860-123">Next, instantiate a [**DevicePolicyUpdateRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicepolicyupdaterequest) object and set the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of device objects.</span></span>

<span data-ttu-id="93860-124">Cihaz İlkesi güncelleştirme isteğini işlemek için, belirtilen müşterideki işlemlere bir arabirim almak üzere [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini Müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="93860-124">To process the device policy update request, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="93860-125">Ardından, müşteri cihaz koleksiyonu işlemlerine bir arabirim almak için [**Devicepolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="93860-125">Then, retrieve the [**DevicePolicy**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicepolicy) property to get an interface to customer device collection operations.</span></span> <span data-ttu-id="93860-126">Son olarak, cihazları ilkeyle güncelleştirmek için DevicePolicyUpdateRequest nesnesiyle birlikte [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="93860-126">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.icustomerdevicecollection.update) method with the DevicePolicyUpdateRequest object to update the devices with the policy.</span></span>

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

<span data-ttu-id="93860-127">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="93860-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="93860-128">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdateDevicesPolicy.cs</span><span class="sxs-lookup"><span data-stu-id="93860-128">**Project**: Partner Center SDK Samples **Class**: UpdateDevicesPolicy.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="93860-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="93860-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="93860-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="93860-130">Request syntax</span></span>

| <span data-ttu-id="93860-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="93860-131">Method</span></span>    | <span data-ttu-id="93860-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="93860-132">Request URI</span></span>                                                                                         |
|-----------|-----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="93860-133">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="93860-133">**PATCH**</span></span> | <span data-ttu-id="93860-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicepolicyupdates http/1.1</span><span class="sxs-lookup"><span data-stu-id="93860-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/DevicePolicyUpdates HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="93860-135">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="93860-135">URI parameter</span></span>

<span data-ttu-id="93860-136">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="93860-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="93860-137">Ad</span><span class="sxs-lookup"><span data-stu-id="93860-137">Name</span></span>        | <span data-ttu-id="93860-138">Tür</span><span class="sxs-lookup"><span data-stu-id="93860-138">Type</span></span>   | <span data-ttu-id="93860-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93860-139">Required</span></span> | <span data-ttu-id="93860-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93860-140">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="93860-141">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="93860-141">customer-id</span></span> | <span data-ttu-id="93860-142">string</span><span class="sxs-lookup"><span data-stu-id="93860-142">string</span></span> | <span data-ttu-id="93860-143">Yes</span><span class="sxs-lookup"><span data-stu-id="93860-143">Yes</span></span>      | <span data-ttu-id="93860-144">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="93860-144">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="93860-145">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="93860-145">Request headers</span></span>

<span data-ttu-id="93860-146">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="93860-146">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="93860-147">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="93860-147">Request body</span></span>

<span data-ttu-id="93860-148">İstek gövdesi bir [Devicepolicyupdaterequest](device-deployment-resources.md#devicepolicyupdaterequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="93860-148">The request body must contain a [DevicePolicyUpdateRequest](device-deployment-resources.md#devicepolicyupdaterequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="93860-149">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="93860-149">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="93860-150">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="93860-150">REST response</span></span>

<span data-ttu-id="93860-151">Başarılı olursa, yanıt, bu toplu işlemin durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="93860-151">If successful, the response contains a **Location** header that has a URI that can be used to retrieve the status of this batch process.</span></span> <span data-ttu-id="93860-152">Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="93860-152">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="93860-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="93860-153">Response success and error codes</span></span>

<span data-ttu-id="93860-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="93860-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="93860-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="93860-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="93860-156">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="93860-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="93860-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="93860-157">Response example</span></span>

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
