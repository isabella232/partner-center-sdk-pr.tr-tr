---
title: Belirtilen müşteri için bir cihazı silme
description: Belirtilen müşteriye ait olan bir cihazı silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1e05ceb8615d6f84c1df101c542342f9a6eb04b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973086"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="7b3b8-103">Belirtilen müşteri için bir cihazı silme</span><span class="sxs-lookup"><span data-stu-id="7b3b8-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="7b3b8-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7b3b8-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="7b3b8-105">Bu makalede, belirtilen müşteriye ait olan bir cihazın nasıl silineceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-105">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7b3b8-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7b3b8-106">Prerequisites</span></span>

- <span data-ttu-id="7b3b8-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7b3b8-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7b3b8-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="7b3b8-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="7b3b8-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="7b3b8-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="7b3b8-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="7b3b8-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="7b3b8-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="7b3b8-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="7b3b8-115">Cihaz toplu işlem tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-115">The device batch identifier.</span></span>

- <span data-ttu-id="7b3b8-116">Cihaz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-116">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="7b3b8-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7b3b8-117">C\#</span></span>

<span data-ttu-id="7b3b8-118">Belirtilen müşteri için bir cihazı silmek için:</span><span class="sxs-lookup"><span data-stu-id="7b3b8-118">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="7b3b8-119">Müşterinin işlemlerine bir arabirim almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="7b3b8-120">Belirtilen toplu işlem için bir arabirim almak üzere cihaz toplu kimliğiyle [**devicebatch. byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="7b3b8-121">Belirtilen cihazdaki işlem arabirimini almak için [**Devices. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-121">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="7b3b8-122">Cihazı Batch 'ten silmek için [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) veya [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-122">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="7b3b8-123">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7b3b8-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7b3b8-124">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: deletedevice. cs</span><span class="sxs-lookup"><span data-stu-id="7b3b8-124">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7b3b8-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7b3b8-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7b3b8-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7b3b8-126">Request syntax</span></span>

| <span data-ttu-id="7b3b8-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7b3b8-127">Method</span></span>     | <span data-ttu-id="7b3b8-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7b3b8-128">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7b3b8-129">DELETE</span><span class="sxs-lookup"><span data-stu-id="7b3b8-129">DELETE</span></span>     | <span data-ttu-id="7b3b8-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicebatches/{devicebatch-ID}/Devices/{Device-id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7b3b8-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="7b3b8-131">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="7b3b8-131">URI parameters</span></span>

<span data-ttu-id="7b3b8-132">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="7b3b8-133">Ad</span><span class="sxs-lookup"><span data-stu-id="7b3b8-133">Name</span></span>           | <span data-ttu-id="7b3b8-134">Tür</span><span class="sxs-lookup"><span data-stu-id="7b3b8-134">Type</span></span>   | <span data-ttu-id="7b3b8-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7b3b8-135">Required</span></span> | <span data-ttu-id="7b3b8-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7b3b8-136">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="7b3b8-137">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="7b3b8-137">customer-id</span></span>    | <span data-ttu-id="7b3b8-138">string</span><span class="sxs-lookup"><span data-stu-id="7b3b8-138">string</span></span> | <span data-ttu-id="7b3b8-139">Yes</span><span class="sxs-lookup"><span data-stu-id="7b3b8-139">Yes</span></span>      | <span data-ttu-id="7b3b8-140">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-140">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="7b3b8-141">devicebatch kimliği</span><span class="sxs-lookup"><span data-stu-id="7b3b8-141">devicebatch-id</span></span> | <span data-ttu-id="7b3b8-142">string</span><span class="sxs-lookup"><span data-stu-id="7b3b8-142">string</span></span> | <span data-ttu-id="7b3b8-143">Yes</span><span class="sxs-lookup"><span data-stu-id="7b3b8-143">Yes</span></span>      | <span data-ttu-id="7b3b8-144">Cihazı içeren toplu işlemin cihaz toplu iş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-144">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="7b3b8-145">cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="7b3b8-145">device-id</span></span>      | <span data-ttu-id="7b3b8-146">string</span><span class="sxs-lookup"><span data-stu-id="7b3b8-146">string</span></span> | <span data-ttu-id="7b3b8-147">Yes</span><span class="sxs-lookup"><span data-stu-id="7b3b8-147">Yes</span></span>      | <span data-ttu-id="7b3b8-148">Cihaz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-148">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="7b3b8-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7b3b8-149">Request headers</span></span>

<span data-ttu-id="7b3b8-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7b3b8-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7b3b8-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7b3b8-151">Request body</span></span>

<span data-ttu-id="7b3b8-152">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="7b3b8-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="7b3b8-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7b3b8-153">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices/7b11cd8b-dd1e-4840-8c4a-84215e4de782 HTTP/1.1
Authorization: Bearer <token>
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Content-Length: 0
Content-Type: application/json
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7b3b8-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7b3b8-154">REST response</span></span>

<span data-ttu-id="7b3b8-155">Başarılı olursa, yanıt **204 içerik** durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-155">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7b3b8-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7b3b8-156">Response success and error codes</span></span>

<span data-ttu-id="7b3b8-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7b3b8-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b3b8-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7b3b8-159">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7b3b8-159">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7b3b8-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7b3b8-160">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
