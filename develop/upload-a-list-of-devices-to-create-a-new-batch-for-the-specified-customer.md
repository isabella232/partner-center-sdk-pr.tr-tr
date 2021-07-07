---
title: Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihaz listesini karşıya yükleme
description: Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihazlarla ilgili bilgilerin listesini karşıya yükleme. Bu, sıfır Touch dağıtımda kayıt için bir cihaz toplu işi oluşturur ve cihazları ve cihaz toplu işlemini belirtilen müşteriyle ilişkilendirir.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 285af12034562262c99b2aa3b139e948b0fdd462
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529741"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="3953c-104">Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihaz listesini karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="3953c-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="3953c-105">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3953c-105">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="3953c-106">Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihazlarla ilgili bilgilerin listesini karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="3953c-106">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="3953c-107">Bu, sıfır Touch dağıtımda kayıt için bir cihaz toplu işi oluşturur ve cihazları ve cihaz toplu işlemini belirtilen müşteriyle ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="3953c-107">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3953c-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3953c-108">Prerequisites</span></span>

- <span data-ttu-id="3953c-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3953c-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3953c-110">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="3953c-110">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="3953c-111">Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="3953c-111">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="3953c-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3953c-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3953c-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3953c-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3953c-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="3953c-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3953c-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3953c-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3953c-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="3953c-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3953c-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="3953c-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3953c-118">Ayrı cihazlarla ilgili bilgileri sağlayan cihaz kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="3953c-118">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="3953c-119">C\#</span><span class="sxs-lookup"><span data-stu-id="3953c-119">C\#</span></span>

<span data-ttu-id="3953c-120">Yeni bir cihaz toplu işi oluşturmak üzere cihaz listesini karşıya yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="3953c-120">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="3953c-121">[**Cihaz**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) türünde yeni bir [list/DotNet/api/System. Collections. Generic. List -1) örneği oluşturun ve listeyi cihazlarla doldurun.</span><span class="sxs-lookup"><span data-stu-id="3953c-121">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="3953c-122">Doldurulmuş özelliklerin aşağıdaki birleşimleri, her bir cihazı tanımlamak için en azından gereklidir:</span><span class="sxs-lookup"><span data-stu-id="3953c-122">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="3953c-123">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="3953c-123">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="3953c-124">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="3953c-124">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="3953c-125">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="3953c-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="3953c-126">Yalnızca [**Hardwarehash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="3953c-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="3953c-127">Yalnızca [**ürün**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="3953c-127">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="3953c-128">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="3953c-128">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="3953c-129">Bir [**Devicebatchcreationrequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) nesnesi örneği oluşturun ve [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) özelliğini seçtiğiniz bir benzersiz ad ve [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) özelliğini, yüklenecek cihazların listesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3953c-129">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="3953c-130">Belirtilen müşterideki işlemlere bir arabirim almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak cihaz toplu oluşturma isteğini işleyin.</span><span class="sxs-lookup"><span data-stu-id="3953c-130">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="3953c-131">Toplu işi oluşturmak için cihaz toplu oluşturma isteğiyle [**devicebatch. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="3953c-131">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

```csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;

List<Device> devicesToBeUploaded = new List<Device>
{
    new Device
    {
        HardwareHash = "DummyHash123",
        ProductKey = "00329-00000-0003-AA606",
        SerialNumber = "1R9-ZNP67"
    }
};

DeviceBatchCreationRequest
    newDeviceBatch = new DeviceBatchCreationRequest
{
    BatchId = "SDKTestDeviceBatch",
    Devices = devicesToBeUploaded
};

var trackingLocation =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Create(newDeviceBatch);
```

<span data-ttu-id="3953c-132">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3953c-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3953c-133">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: createdevicebatch. cs</span><span class="sxs-lookup"><span data-stu-id="3953c-133">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3953c-134">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3953c-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3953c-135">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3953c-135">Request syntax</span></span>

| <span data-ttu-id="3953c-136">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3953c-136">Method</span></span>   | <span data-ttu-id="3953c-137">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3953c-137">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="3953c-138">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="3953c-138">**POST**</span></span> | <span data-ttu-id="3953c-139">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/deviceyığınları http/1.1</span><span class="sxs-lookup"><span data-stu-id="3953c-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="3953c-140">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="3953c-140">URI parameter</span></span>

<span data-ttu-id="3953c-141">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3953c-141">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="3953c-142">Ad</span><span class="sxs-lookup"><span data-stu-id="3953c-142">Name</span></span>        | <span data-ttu-id="3953c-143">Tür</span><span class="sxs-lookup"><span data-stu-id="3953c-143">Type</span></span>   | <span data-ttu-id="3953c-144">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3953c-144">Required</span></span> | <span data-ttu-id="3953c-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3953c-145">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="3953c-146">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="3953c-146">customer-id</span></span> | <span data-ttu-id="3953c-147">string</span><span class="sxs-lookup"><span data-stu-id="3953c-147">string</span></span> | <span data-ttu-id="3953c-148">Yes</span><span class="sxs-lookup"><span data-stu-id="3953c-148">Yes</span></span>      | <span data-ttu-id="3953c-149">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="3953c-149">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="3953c-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3953c-150">Request headers</span></span>

<span data-ttu-id="3953c-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3953c-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3953c-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3953c-152">Request body</span></span>

<span data-ttu-id="3953c-153">İstek gövdesi bir [Devicebatchcreationrequest](device-deployment-resources.md#devicebatchcreationrequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="3953c-153">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="3953c-154">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3953c-154">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
    "BatchId": "SDKTestDeviceBatch",
    "Devices": [{
            "Id": null,
            "SerialNumber": "1R9-ZNP67",
            "ProductKey": "00329-00000-0003-AA606",
            "HardwareHash": "DummyHash123",
            "Policies": null,
            "CreatedBy": null,
            "UploadedDate": "0001-01-01T00:00:00",
            "AllowedOperations": null,
            "Attributes": {
                "ObjectType": "Device"
            }
        }
    ],
    "Attributes": {
        "ObjectType": "DeviceBatchCreationRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="3953c-155">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3953c-155">REST response</span></span>

<span data-ttu-id="3953c-156">Başarılı olursa, yanıt, cihaz yükleme durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="3953c-156">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="3953c-157">Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="3953c-157">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3953c-158">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3953c-158">Response success and error codes</span></span>

<span data-ttu-id="3953c-159">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3953c-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3953c-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3953c-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3953c-161">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3953c-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="3953c-162">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3953c-162">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: /customers/c7f3c849-129f-4b85-a96d-4f8e88b315a3/batchJobStatus/beba2053-5401-46ff-9223-7e841ed78fbf
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2017 20:35:35 GMT
```
