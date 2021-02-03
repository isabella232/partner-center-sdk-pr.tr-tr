---
title: Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihaz listesini karşıya yükleme
description: Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihazlarla ilgili bilgilerin listesini karşıya yükleme. Bu, sıfır Touch dağıtımda kayıt için bir cihaz toplu işi oluşturur ve cihazları ve cihaz toplu işlemini belirtilen müşteriyle ilişkilendirir.
ms.date: 08/08/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0b48971b862418136c42e78ae973a5aea27404a1
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769737"
---
# <a name="upload-a-list-of-devices-to-create-a-new-batch-for-the-specified-customer"></a><span data-ttu-id="6f80b-104">Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihaz listesini karşıya yükleme</span><span class="sxs-lookup"><span data-stu-id="6f80b-104">Upload a list of devices to create a new batch for the specified customer</span></span>

<span data-ttu-id="6f80b-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="6f80b-105">**Applies to:**</span></span>

- <span data-ttu-id="6f80b-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6f80b-106">Partner Center</span></span>
- <span data-ttu-id="6f80b-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6f80b-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="6f80b-108">Belirtilen müşteri için yeni bir toplu iş oluşturmak üzere cihazlarla ilgili bilgilerin listesini karşıya yükleme.</span><span class="sxs-lookup"><span data-stu-id="6f80b-108">How to upload a list of information about devices to create a new batch for the specified customer.</span></span> <span data-ttu-id="6f80b-109">Bu, sıfır Touch dağıtımda kayıt için bir cihaz toplu işi oluşturur ve cihazları ve cihaz toplu işlemini belirtilen müşteriyle ilişkilendirir.</span><span class="sxs-lookup"><span data-stu-id="6f80b-109">This creates a device batch for enrollment in zero-touch deployment, and associates the devices and the device batch with the specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f80b-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6f80b-110">Prerequisites</span></span>

- <span data-ttu-id="6f80b-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6f80b-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6f80b-112">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="6f80b-112">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="6f80b-113">Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="6f80b-113">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="6f80b-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f80b-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6f80b-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f80b-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6f80b-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="6f80b-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6f80b-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="6f80b-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6f80b-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="6f80b-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6f80b-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="6f80b-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="6f80b-120">Ayrı cihazlarla ilgili bilgileri sağlayan cihaz kaynaklarının listesi.</span><span class="sxs-lookup"><span data-stu-id="6f80b-120">The list of device resources that provide the information about the individual devices.</span></span>

## <a name="c"></a><span data-ttu-id="6f80b-121">C\#</span><span class="sxs-lookup"><span data-stu-id="6f80b-121">C\#</span></span>

<span data-ttu-id="6f80b-122">Yeni bir cihaz toplu işi oluşturmak üzere cihaz listesini karşıya yüklemek için:</span><span class="sxs-lookup"><span data-stu-id="6f80b-122">To upload a list of devices to create a new device batch:</span></span>

1. <span data-ttu-id="6f80b-123">[**Cihaz**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) türünde yeni bir [list/DotNet/api/System. Collections. Generic. List -1) örneği oluşturun ve listeyi cihazlarla doldurun.</span><span class="sxs-lookup"><span data-stu-id="6f80b-123">Instantiate a new [List/dotnet/api/system.collections.generic.list-1) of type [**Device**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device) and populate the list with the devices.</span></span> <span data-ttu-id="6f80b-124">Doldurulmuş özelliklerin aşağıdaki birleşimleri, her bir cihazı tanımlamak için en azından gereklidir:</span><span class="sxs-lookup"><span data-stu-id="6f80b-124">The following combinations of populated properties are required at a minimum for identifying each device:</span></span>

   - <span data-ttu-id="6f80b-125">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span><span class="sxs-lookup"><span data-stu-id="6f80b-125">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey).</span></span>
   - <span data-ttu-id="6f80b-126">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="6f80b-126">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="6f80b-127">[**Donanım karması**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash)  +  [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey)  +  [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span><span class="sxs-lookup"><span data-stu-id="6f80b-127">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) + [**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) + [**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber).</span></span>
   - <span data-ttu-id="6f80b-128">Yalnızca [**Hardwarehash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) .</span><span class="sxs-lookup"><span data-stu-id="6f80b-128">[**HardwareHash**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.hardwarehash) only.</span></span>
   - <span data-ttu-id="6f80b-129">Yalnızca [**ürün**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) .</span><span class="sxs-lookup"><span data-stu-id="6f80b-129">[**ProductKey**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.productkey) only.</span></span>
   - <span data-ttu-id="6f80b-130">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber)  +  [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername)  +  [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span><span class="sxs-lookup"><span data-stu-id="6f80b-130">[**SerialNumber**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.serialnumber) + [**OemManufacturerName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.oemmanufacturername) + [**ModelName**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.device.modelname).</span></span>

2. <span data-ttu-id="6f80b-131">Bir [**Devicebatchcreationrequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) nesnesi örneği oluşturun ve [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) özelliğini seçtiğiniz bir benzersiz ad ve [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) özelliğini, yüklenecek cihazların listesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="6f80b-131">Instantiate a [**DeviceBatchCreationRequest**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest) object and set the [**BatchId**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.batchid) property to a unique name of your choosing, and the [**Devices**](/dotnet/api/microsoft.store.partnercenter.models.devicesdeployment.devicebatchcreationrequest.devices) property to the list of devices to upload.</span></span>

3. <span data-ttu-id="6f80b-132">Belirtilen müşterideki işlemlere bir arabirim almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak cihaz toplu oluşturma isteğini işleyin.</span><span class="sxs-lookup"><span data-stu-id="6f80b-132">Process the device batch creation request by calling the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the specified customer.</span></span>

4. <span data-ttu-id="6f80b-133">Toplu işi oluşturmak için cihaz toplu oluşturma isteğiyle [**devicebatch. Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="6f80b-133">Call the [**DeviceBatches.Create**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection) method with the device batch creation request to create the batch.</span></span>

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

<span data-ttu-id="6f80b-134">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6f80b-134">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6f80b-135">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CreateDeviceBatch.cs</span><span class="sxs-lookup"><span data-stu-id="6f80b-135">**Project**: Partner Center SDK Samples **Class**: CreateDeviceBatch.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6f80b-136">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6f80b-136">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6f80b-137">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6f80b-137">Request syntax</span></span>

| <span data-ttu-id="6f80b-138">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6f80b-138">Method</span></span>   | <span data-ttu-id="6f80b-139">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6f80b-139">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="6f80b-140">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="6f80b-140">**POST**</span></span> | <span data-ttu-id="6f80b-141">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/deviceyığınları http/1.1</span><span class="sxs-lookup"><span data-stu-id="6f80b-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="6f80b-142">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="6f80b-142">URI parameter</span></span>

<span data-ttu-id="6f80b-143">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f80b-143">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="6f80b-144">Ad</span><span class="sxs-lookup"><span data-stu-id="6f80b-144">Name</span></span>        | <span data-ttu-id="6f80b-145">Tür</span><span class="sxs-lookup"><span data-stu-id="6f80b-145">Type</span></span>   | <span data-ttu-id="6f80b-146">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6f80b-146">Required</span></span> | <span data-ttu-id="6f80b-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6f80b-147">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="6f80b-148">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="6f80b-148">customer-id</span></span> | <span data-ttu-id="6f80b-149">string</span><span class="sxs-lookup"><span data-stu-id="6f80b-149">string</span></span> | <span data-ttu-id="6f80b-150">Yes</span><span class="sxs-lookup"><span data-stu-id="6f80b-150">Yes</span></span>      | <span data-ttu-id="6f80b-151">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="6f80b-151">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6f80b-152">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6f80b-152">Request headers</span></span>

<span data-ttu-id="6f80b-153">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6f80b-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6f80b-154">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6f80b-154">Request body</span></span>

<span data-ttu-id="6f80b-155">İstek gövdesi bir [Devicebatchcreationrequest](device-deployment-resources.md#devicebatchcreationrequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="6f80b-155">The request body must contain a [DeviceBatchCreationRequest](device-deployment-resources.md#devicebatchcreationrequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="6f80b-156">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6f80b-156">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="6f80b-157">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6f80b-157">REST response</span></span>

<span data-ttu-id="6f80b-158">Başarılı olursa, yanıt, cihaz yükleme durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="6f80b-158">If successful, the response contains a **Location** header that has a URI that can be used to retrieve device upload status.</span></span> <span data-ttu-id="6f80b-159">Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="6f80b-159">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6f80b-160">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6f80b-160">Response success and error codes</span></span>

<span data-ttu-id="6f80b-161">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="6f80b-161">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6f80b-162">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f80b-162">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6f80b-163">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6f80b-163">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

#### <a name="response-example"></a><span data-ttu-id="6f80b-164">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6f80b-164">Response example</span></span>

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
