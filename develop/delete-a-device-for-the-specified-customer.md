---
title: Belirtilen müşteri için bir cihazı silme
description: Belirtilen müşteriye ait olan bir cihazı silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 69b5440f2cf07d3cb4ecd5addf429acd64530257
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769388"
---
# <a name="delete-a-device-for-the-specified-customer"></a><span data-ttu-id="2b804-103">Belirtilen müşteri için bir cihazı silme</span><span class="sxs-lookup"><span data-stu-id="2b804-103">Delete a device for the specified customer</span></span>

<span data-ttu-id="2b804-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="2b804-104">**Applies to:**</span></span>

- <span data-ttu-id="2b804-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2b804-105">Partner Center</span></span>
- <span data-ttu-id="2b804-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2b804-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="2b804-107">Bu makalede, belirtilen müşteriye ait olan bir cihazın nasıl silineceği açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="2b804-107">This article explains how to delete a device that belongs to a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2b804-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2b804-108">Prerequisites</span></span>

- <span data-ttu-id="2b804-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2b804-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2b804-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2b804-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2b804-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2b804-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2b804-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2b804-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2b804-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2b804-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2b804-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2b804-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2b804-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="2b804-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2b804-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="2b804-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2b804-117">Cihaz toplu işlem tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2b804-117">The device batch identifier.</span></span>

- <span data-ttu-id="2b804-118">Cihaz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2b804-118">The device identifier.</span></span>

## <a name="c"></a><span data-ttu-id="2b804-119">C\#</span><span class="sxs-lookup"><span data-stu-id="2b804-119">C\#</span></span>

<span data-ttu-id="2b804-120">Belirtilen müşteri için bir cihazı silmek için:</span><span class="sxs-lookup"><span data-stu-id="2b804-120">To delete a device for the specified customer:</span></span>

1. <span data-ttu-id="2b804-121">Müşterinin işlemlerine bir arabirim almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2b804-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to retrieve an interface to operations on the customer.</span></span>

2. <span data-ttu-id="2b804-122">Belirtilen toplu işlem için bir arabirim almak üzere cihaz toplu kimliğiyle [**devicebatch. byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2b804-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method with the device batch identifier to get an interface to operations for the specified batch.</span></span>

3. <span data-ttu-id="2b804-123">Belirtilen cihazdaki işlem arabirimini almak için [**Devices. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="2b804-123">Call the [**Devices.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.byid) method to get an interface to operation on the specified device.</span></span>

4. <span data-ttu-id="2b804-124">Cihazı Batch 'ten silmek için [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) veya [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2b804-124">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.delete) or [**DeleteAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevice.deleteasync) method to delete the device from the batch.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;
string selectedDeviceId;

partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.ById(selectedDeviceId).Delete();
```

<span data-ttu-id="2b804-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2b804-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2b804-126">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: DeleteDevice.cs</span><span class="sxs-lookup"><span data-stu-id="2b804-126">**Project**: Partner Center SDK Samples **Class**: DeleteDevice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2b804-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2b804-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2b804-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2b804-128">Request syntax</span></span>

| <span data-ttu-id="2b804-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2b804-129">Method</span></span>     | <span data-ttu-id="2b804-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2b804-130">Request URI</span></span>                                                                                                                        |
|------------|------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2b804-131">DELETE</span><span class="sxs-lookup"><span data-stu-id="2b804-131">DELETE</span></span>     | <span data-ttu-id="2b804-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicebatches/{devicebatch-ID}/Devices/{Device-id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="2b804-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices/{device-id} HTTP/1.1</span></span>  |

#### <a name="uri-parameters"></a><span data-ttu-id="2b804-133">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="2b804-133">URI parameters</span></span>

<span data-ttu-id="2b804-134">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b804-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="2b804-135">Ad</span><span class="sxs-lookup"><span data-stu-id="2b804-135">Name</span></span>           | <span data-ttu-id="2b804-136">Tür</span><span class="sxs-lookup"><span data-stu-id="2b804-136">Type</span></span>   | <span data-ttu-id="2b804-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2b804-137">Required</span></span> | <span data-ttu-id="2b804-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2b804-138">Description</span></span>                                                        |
|----------------|--------|----------|--------------------------------------------------------------------|
| <span data-ttu-id="2b804-139">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="2b804-139">customer-id</span></span>    | <span data-ttu-id="2b804-140">string</span><span class="sxs-lookup"><span data-stu-id="2b804-140">string</span></span> | <span data-ttu-id="2b804-141">Yes</span><span class="sxs-lookup"><span data-stu-id="2b804-141">Yes</span></span>      | <span data-ttu-id="2b804-142">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="2b804-142">A GUID-formatted string that identifies the customer.</span></span>              |
| <span data-ttu-id="2b804-143">devicebatch kimliği</span><span class="sxs-lookup"><span data-stu-id="2b804-143">devicebatch-id</span></span> | <span data-ttu-id="2b804-144">string</span><span class="sxs-lookup"><span data-stu-id="2b804-144">string</span></span> | <span data-ttu-id="2b804-145">Yes</span><span class="sxs-lookup"><span data-stu-id="2b804-145">Yes</span></span>      | <span data-ttu-id="2b804-146">Cihazı içeren toplu işlemin cihaz toplu iş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2b804-146">The device batch identifier of the batch that contains the device.</span></span> |
| <span data-ttu-id="2b804-147">cihaz kimliği</span><span class="sxs-lookup"><span data-stu-id="2b804-147">device-id</span></span>      | <span data-ttu-id="2b804-148">string</span><span class="sxs-lookup"><span data-stu-id="2b804-148">string</span></span> | <span data-ttu-id="2b804-149">Yes</span><span class="sxs-lookup"><span data-stu-id="2b804-149">Yes</span></span>      | <span data-ttu-id="2b804-150">Cihaz tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2b804-150">The device identifier.</span></span>                                             |

### <a name="request-headers"></a><span data-ttu-id="2b804-151">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2b804-151">Request headers</span></span>

<span data-ttu-id="2b804-152">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2b804-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2b804-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2b804-153">Request body</span></span>

<span data-ttu-id="2b804-154">Yok</span><span class="sxs-lookup"><span data-stu-id="2b804-154">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2b804-155">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2b804-155">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="2b804-156">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2b804-156">REST response</span></span>

<span data-ttu-id="2b804-157">Başarılı olursa, yanıt **204 içerik** durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="2b804-157">If successful, the response returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2b804-158">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2b804-158">Response success and error codes</span></span>

<span data-ttu-id="2b804-159">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2b804-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2b804-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2b804-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2b804-161">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2b804-161">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2b804-162">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2b804-162">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 394d96d0-05b2-4b02-b907-0697632ee3bb
MS-RequestId: 8b3e6f78-220b-4177-861b-33d6f38f7b97
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:58:53 GMT
```
