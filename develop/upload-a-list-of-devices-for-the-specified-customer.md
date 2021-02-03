---
title: Belirtilen müşteri için mevcut bir toplu işe ait cihaz listesini karşıya yükleme
description: Belirtilen müşteri için mevcut bir toplu işe cihaz hakkındaki bilgilerin bir listesini karşıya yükleme. Bu, cihazları zaten oluşturulmuş bir cihaz toplu işi ile ilişkilendirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d01ac1a42c50416487167070be9d104562300baf
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769743"
---
# <a name="upload-a-list-of-devices-to-an-existing-batch-for-the-specified-customer"></a><span data-ttu-id="5b873-104">Belirtilen müşteri için mevcut bir toplu işe ait cihaz listesini karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="5b873-104">Upload a list of devices to an existing batch for the specified customer</span></span>

<span data-ttu-id="5b873-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="5b873-105">**Applies To**</span></span>

- <span data-ttu-id="5b873-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5b873-106">Partner Center</span></span>
- <span data-ttu-id="5b873-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5b873-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5b873-108">Belirtilen müşteri için mevcut bir toplu işe cihaz hakkındaki bilgilerin bir listesini karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="5b873-108">How to upload a list of information about devices to an existing batch for the specified customer.</span></span> <span data-ttu-id="5b873-109">Bu, cihazları zaten oluşturulmuş bir cihaz toplu işi ile ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="5b873-109">This associates the devices with a device batch already created.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5b873-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5b873-110">Prerequisites</span></span>

- <span data-ttu-id="5b873-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5b873-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5b873-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5b873-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5b873-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5b873-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5b873-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5b873-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5b873-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5b873-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5b873-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5b873-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5b873-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="5b873-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5b873-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="5b873-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5b873-119">Cihaz toplu işlem tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5b873-119">The device batch identifier.</span></span>

- <span data-ttu-id="5b873-120">Ayrı cihazlarla ilgili bilgileri sağlayan cihaz kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="5b873-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="5b873-121">C\#</span><span class="sxs-lookup"><span data-stu-id="5b873-121">C\#</span></span>

<span data-ttu-id="5b873-122">Mevcut bir cihaz toplu işinde cihaz listesini karşıya yüklemek için, [**cihaz**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) türünde yeni bir [list/DotNet/api/System. Collections. Generic. List -1) örneği oluşturun ve listeyi cihazlarla doldurun.</span><span class="sxs-lookup"><span data-stu-id="5b873-122">To upload a list of devices to an existing device batch, first, instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="5b873-123">Doldurulmuş özelliklerin aşağıdaki birleşimleri, her bir cihazı tanımlamak için en azından gereklidir:</span><span class="sxs-lookup"><span data-stu-id="5b873-123">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

- <span data-ttu-id="5b873-124">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="5b873-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>

- <span data-ttu-id="5b873-125">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="5b873-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="5b873-126">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="5b873-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>

- <span data-ttu-id="5b873-127">Yalnızca [**Hardwarehash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="5b873-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>

- <span data-ttu-id="5b873-128">Yalnızca [**ürün**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="5b873-128">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>

- <span data-ttu-id="5b873-129">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="5b873-129">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

<span data-ttu-id="5b873-130">Ardından, belirtilen müşterideki işlemlere bir arabirim almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5b873-130">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="5b873-131">Ardından, belirtilen toplu işlem için bir arabirim almak üzere cihaz toplu kimliğiyle [**devicebatch. byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5b873-131">Next, call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span> <span data-ttu-id="5b873-132">Son olarak, cihazları cihaz toplu işe eklemek için cihazların listesiyle birlikte Device [**. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5b873-132">Finally, call the [**Devices.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.createasync) method with the list of devices to add the devices to the device batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash1234",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    },

    new Device
    {
        HardwareHash = "DummyHash12345",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "2R9-ZNP67"
    }
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Create(devicesToBeUploaded);
```

<span data-ttu-id="5b873-133">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5b873-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5b873-134">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CreateDevices.cs</span><span class="sxs-lookup"><span data-stu-id="5b873-134">**Project**: Partner Center SDK Samples **Class**: CreateDevices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5b873-135">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5b873-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5b873-136">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5b873-136">Request syntax</span></span>

| <span data-ttu-id="5b873-137">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5b873-137">Method</span></span>   | <span data-ttu-id="5b873-138">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5b873-138">Request URI</span></span>                                                                                                            |
|----------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5b873-139">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="5b873-139">**POST**</span></span> | <span data-ttu-id="5b873-140">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicebatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="5b873-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5b873-141">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="5b873-141">URI parameter</span></span>

<span data-ttu-id="5b873-142">İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b873-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="5b873-143">Ad</span><span class="sxs-lookup"><span data-stu-id="5b873-143">Name</span></span>           | <span data-ttu-id="5b873-144">Tür</span><span class="sxs-lookup"><span data-stu-id="5b873-144">Type</span></span>   | <span data-ttu-id="5b873-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5b873-145">Required</span></span> | <span data-ttu-id="5b873-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5b873-146">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="5b873-147">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="5b873-147">customer-id</span></span>    | <span data-ttu-id="5b873-148">string</span><span class="sxs-lookup"><span data-stu-id="5b873-148">string</span></span> | <span data-ttu-id="5b873-149">Yes</span><span class="sxs-lookup"><span data-stu-id="5b873-149">Yes</span></span>      | <span data-ttu-id="5b873-150">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="5b873-150">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="5b873-151">devicebatch kimliği</span><span class="sxs-lookup"><span data-stu-id="5b873-151">devicebatch-id</span></span> | <span data-ttu-id="5b873-152">string</span><span class="sxs-lookup"><span data-stu-id="5b873-152">string</span></span> | <span data-ttu-id="5b873-153">Yes</span><span class="sxs-lookup"><span data-stu-id="5b873-153">Yes</span></span>      | <span data-ttu-id="5b873-154">Cihaz toplu işini tanımlayan bir dize tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5b873-154">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5b873-155">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5b873-155">Request headers</span></span>

<span data-ttu-id="5b873-156">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5b873-156">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5b873-157">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5b873-157">Request body</span></span>

<span data-ttu-id="5b873-158">İstek gövdesi bir [cihaz](device-deployment-resources.md#device) nesneleri dizisi içermelidir.</span><span class="sxs-lookup"><span data-stu-id="5b873-158">The request body must contain an array of [Device](device-deployment-resources.md#device) objects.</span></span> <span data-ttu-id="5b873-159">Bir cihazı tanımlamaya yönelik aşağıdaki alan birleşimleri kabul edilir:</span><span class="sxs-lookup"><span data-stu-id="5b873-159">The following combinations of fields for identifying a device are accepted:</span></span>

- <span data-ttu-id="5b873-160">hardwareHash + productKey.</span><span class="sxs-lookup"><span data-stu-id="5b873-160">hardwareHash + productKey.</span></span>
- <span data-ttu-id="5b873-161">hardwareHash + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="5b873-161">hardwareHash + serialNumber.</span></span>
- <span data-ttu-id="5b873-162">hardwareHash + productKey + serialNumber.</span><span class="sxs-lookup"><span data-stu-id="5b873-162">hardwareHash + productKey + serialNumber.</span></span>
- <span data-ttu-id="5b873-163">yalnızca hardwareHash.</span><span class="sxs-lookup"><span data-stu-id="5b873-163">hardwareHash only.</span></span>
- <span data-ttu-id="5b873-164">Yalnızca ürün.</span><span class="sxs-lookup"><span data-stu-id="5b873-164">productKey only.</span></span>
- <span data-ttu-id="5b873-165">serialNumber + oemManufacturerName + modelName.</span><span class="sxs-lookup"><span data-stu-id="5b873-165">serialNumber + oemManufacturerName + modelName.</span></span>

### <a name="request-example"></a><span data-ttu-id="5b873-166">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5b873-166">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches/Test/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 482
Expect: 100-continue

[{
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash1234",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }, {
        "Id": null,
        "SerialNumber": "2R9-ZNP67",
        "ProductKey": "00329-00000-0003-AA606",
        "HardwareHash": "DummyHash12345",
        "Policies": null,
        "CreatedBy": null,
        "UploadedDate": "0001-01-01T00:00:00",
        "AllowedOperations": null,
        "Attributes": {
            "ObjectType": "Device"
        }
    }
]
```

## <a name="rest-response"></a><span data-ttu-id="5b873-167">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5b873-167">REST response</span></span>

<span data-ttu-id="5b873-168">Başarılı olursa, yanıt, cihaz yükleme durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="5b873-168">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="5b873-169">Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="5b873-169">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5b873-170">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5b873-170">Response success and error codes</span></span>

<span data-ttu-id="5b873-171">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5b873-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5b873-172">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5b873-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5b873-173">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5b873-173">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5b873-174">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5b873-174">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/16c00110-e79a-433d-aa28-f69dd60df671
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: e286d69b-7f5f-4098-8999-21d3b54e4e47
MS-CV: OBkGN9pSN0a5xvua.0
MS-ServerId: 101112012
Date: Thu, 28 Sep 2017 20:08:46 GMT
```
