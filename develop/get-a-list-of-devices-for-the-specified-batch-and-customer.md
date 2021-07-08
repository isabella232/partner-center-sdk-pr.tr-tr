---
title: Belirtilen toplu iş ve müşteri için cihazların bir listesini alma
description: Bir müşteri için belirtilen cihaz toplu işsinde cihaz koleksiyonunu ve cihaz ayrıntılarını alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 28af1f568f755ba4c50cfac21529d6c677656c8e
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874270"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="814e9-103">Belirtilen toplu iş ve müşteri için cihazların bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="814e9-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="814e9-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için destek</span><span class="sxs-lookup"><span data-stu-id="814e9-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="814e9-105">Bu makalede, belirtilen bir müşteri için belirtilen bir cihaz toplu iş içinde cihaz koleksiyonunun nasıl alın açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="814e9-105">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="814e9-106">Her cihaz kaynağı, cihazla ilgili ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="814e9-106">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="814e9-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="814e9-107">Prerequisites</span></span>

- <span data-ttu-id="814e9-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="814e9-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="814e9-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="814e9-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="814e9-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="814e9-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="814e9-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="814e9-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="814e9-112">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="814e9-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="814e9-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="814e9-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="814e9-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="814e9-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="814e9-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="814e9-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="814e9-116">Cihaz toplu iş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="814e9-116">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="814e9-117">C\#</span><span class="sxs-lookup"><span data-stu-id="814e9-117">C\#</span></span>

<span data-ttu-id="814e9-118">Belirtilen müşteri için belirtilen bir cihaz toplu iş içinde cihazların koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="814e9-118">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="814e9-119">Belirtilen müşteri üzerinde işlemlere bir arabirim almak için müşteri kimliğiyle [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="814e9-119">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="814e9-120">Belirtilen toplu iş için cihaz toplu toplama işlemlerine arabirim almak üzere [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="814e9-120">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="814e9-121">Toplu iş için cihaz toplama işlemlerine bir arabirim almak için [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="814e9-121">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="814e9-122">Cihaz koleksiyonunu [**almak**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) [**için Get veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="814e9-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="814e9-123">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="814e9-123">For an example, see the following:</span></span>

- <span data-ttu-id="814e9-124">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="814e9-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="814e9-125">Project: **İş Ortağı Merkezi SDK'sı Örnekleri**</span><span class="sxs-lookup"><span data-stu-id="814e9-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="814e9-126">Sınıf: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="814e9-126">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="814e9-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="814e9-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="814e9-128">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="814e9-128">Request syntax</span></span>

| <span data-ttu-id="814e9-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="814e9-129">Method</span></span>  | <span data-ttu-id="814e9-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="814e9-130">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="814e9-131">**Al**</span><span class="sxs-lookup"><span data-stu-id="814e9-131">**GET**</span></span> | <span data-ttu-id="814e9-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="814e9-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="814e9-133">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="814e9-133">URI parameters</span></span>

<span data-ttu-id="814e9-134">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="814e9-134">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="814e9-135">Ad</span><span class="sxs-lookup"><span data-stu-id="814e9-135">Name</span></span>           | <span data-ttu-id="814e9-136">Tür</span><span class="sxs-lookup"><span data-stu-id="814e9-136">Type</span></span>   | <span data-ttu-id="814e9-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="814e9-137">Required</span></span> | <span data-ttu-id="814e9-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="814e9-138">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="814e9-139">customer-id</span><span class="sxs-lookup"><span data-stu-id="814e9-139">customer-id</span></span>    | <span data-ttu-id="814e9-140">string</span><span class="sxs-lookup"><span data-stu-id="814e9-140">string</span></span> | <span data-ttu-id="814e9-141">Yes</span><span class="sxs-lookup"><span data-stu-id="814e9-141">Yes</span></span>      | <span data-ttu-id="814e9-142">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="814e9-142">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="814e9-143">devicebatch-id</span><span class="sxs-lookup"><span data-stu-id="814e9-143">devicebatch-id</span></span> | <span data-ttu-id="814e9-144">string</span><span class="sxs-lookup"><span data-stu-id="814e9-144">string</span></span> | <span data-ttu-id="814e9-145">Yes</span><span class="sxs-lookup"><span data-stu-id="814e9-145">Yes</span></span>      | <span data-ttu-id="814e9-146">Cihaz toplu işlemini tanımlayan bir dize tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="814e9-146">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="814e9-147">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="814e9-147">Request headers</span></span>

<span data-ttu-id="814e9-148">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="814e9-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="814e9-149">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="814e9-149">Request body</span></span>

<span data-ttu-id="814e9-150">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="814e9-150">None</span></span>

### <a name="request-example"></a><span data-ttu-id="814e9-151">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="814e9-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="814e9-152">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="814e9-152">REST response</span></span>

<span data-ttu-id="814e9-153">Başarılı olursa, yanıt gövdesi Cihaz kaynaklarının sayfalı [bir koleksiyonunu](device-deployment-resources.md#device) içerir.</span><span class="sxs-lookup"><span data-stu-id="814e9-153">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="814e9-154">Koleksiyon, bir sayfada 100 cihaz içerir.</span><span class="sxs-lookup"><span data-stu-id="814e9-154">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="814e9-155">100 cihazların sonraki sayfasını almak için yanıt gövdesinde continuationToken, sonraki istekte bir üst bilgi olarak MS-ContinuationToken gerekir.</span><span class="sxs-lookup"><span data-stu-id="814e9-155">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="814e9-156">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="814e9-156">Response success and error codes</span></span>

<span data-ttu-id="814e9-157">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="814e9-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="814e9-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="814e9-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="814e9-159">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="814e9-159">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="814e9-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="814e9-160">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1742
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 2,
    "items":
    [{
            "id": "7c141ea9-2816-4e15-a819-53f6856499ff",
            "serialNumber": "2R9-ZNP67",
            "productKey": "00329-00000-0003-AA6069",
            "modelName": "Precision WorkStation T7500",
            "oemManufacturerName":"Dell Inc.",
            "policies":[{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate":"2017-08-09T14:43:26.0092288-07:00",
            " attributes": {
                "objectType": "Device"
            }
        }, {
            "id": "e528a62f-5031-49f4-bea7-5fafe47388fd",
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "modelName": "HP Z420 Workstation",
            "oemManufacturerName": "Hewlett-Packard",
            "policies": [{
                    "key": "o_o_b_e",
                    "value": null
                }
            ],
            "uploadedDate": "2017-08-09T14:35:51.3126144-07:00",
            "attributes": {
                "objectType": "Device"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
