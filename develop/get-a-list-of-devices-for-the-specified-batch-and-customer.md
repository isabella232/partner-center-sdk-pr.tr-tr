---
title: Belirtilen toplu iş ve müşteri için cihazların bir listesini alma
description: Bir müşteri için belirtilen cihaz toplu işleminde cihaz ve cihaz ayrıntıları koleksiyonu alma.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 36fe3b97612adfd26c1b498f31b90f743bf774cb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769550"
---
# <a name="get-a-list-of-devices-for-the-specified-batch-and-customer"></a><span data-ttu-id="1cf10-103">Belirtilen toplu iş ve müşteri için cihazların bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="1cf10-103">Get a list of devices for the specified batch and customer</span></span>

<span data-ttu-id="1cf10-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="1cf10-104">**Applies to:**</span></span>

- <span data-ttu-id="1cf10-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1cf10-105">Partner Center</span></span>
- <span data-ttu-id="1cf10-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1cf10-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="1cf10-107">Bu makalede, belirli bir müşteri için belirtilen cihaz toplu işlemindeki cihazların bir koleksiyonunun nasıl alınacağını açıklanır.</span><span class="sxs-lookup"><span data-stu-id="1cf10-107">This article describes how to retrieve a collection of devices in a specified device batch for a specified customer.</span></span> <span data-ttu-id="1cf10-108">Her cihaz kaynağı cihaz hakkındaki ayrıntıları içerir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-108">Each device resource contains details about the device.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1cf10-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1cf10-109">Prerequisites</span></span>

- <span data-ttu-id="1cf10-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1cf10-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1cf10-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="1cf10-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="1cf10-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1cf10-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1cf10-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1cf10-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1cf10-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1cf10-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1cf10-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1cf10-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1cf10-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="1cf10-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="1cf10-118">Bir cihaz toplu iş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1cf10-118">A device batch identifier.</span></span>

## <a name="c"></a><span data-ttu-id="1cf10-119">C\#</span><span class="sxs-lookup"><span data-stu-id="1cf10-119">C\#</span></span>

<span data-ttu-id="1cf10-120">Belirtilen müşteri için belirtilen cihaz toplu işlemindeki cihazların bir koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="1cf10-120">To retrieve a collection of the devices in a specified device batch for the specified customer:</span></span>

1. <span data-ttu-id="1cf10-121">Belirtilen müşterideki işlemlere bir arabirim almak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-121">Call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span>

2. <span data-ttu-id="1cf10-122">Belirtilen toplu iş için cihaz toplu işlem koleksiyonu işlemlerine bir arabirim almak üzere [**devicebatch. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-122">Call the [**DeviceBatches.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.byid) method to get an interface to device batch collection operations for the specified batch.</span></span>

3. <span data-ttu-id="1cf10-123">Batch için cihaz koleksiyonu işlemlerine bir arabirim almak üzere [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) özelliğini alın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-123">Retrieve the [**Devices**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatch.devices) property to get an interface to device collection operations for the batch.</span></span>

4. <span data-ttu-id="1cf10-124">Cihazların koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicecollection.getasync) method to retrieve the collection of devices.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string selectedCustomerId;
string selectedDeviceBatchId;

var devices =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.ById(selectedDeviceBatchId).Devices.Get();
```

<span data-ttu-id="1cf10-125">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="1cf10-125">For an example, see the following:</span></span>

- <span data-ttu-id="1cf10-126">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="1cf10-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="1cf10-127">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="1cf10-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="1cf10-128">Sınıf: **GetDevices.cs**</span><span class="sxs-lookup"><span data-stu-id="1cf10-128">Class: **GetDevices.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="1cf10-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1cf10-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1cf10-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1cf10-130">Request syntax</span></span>

| <span data-ttu-id="1cf10-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1cf10-131">Method</span></span>  | <span data-ttu-id="1cf10-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1cf10-132">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1cf10-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="1cf10-133">**GET**</span></span> | <span data-ttu-id="1cf10-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/devicebatches/{devicebatch-ID}/Devices http/1.1</span><span class="sxs-lookup"><span data-stu-id="1cf10-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches/{devicebatch-id}/devices HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="1cf10-135">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="1cf10-135">URI parameters</span></span>

<span data-ttu-id="1cf10-136">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-136">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="1cf10-137">Ad</span><span class="sxs-lookup"><span data-stu-id="1cf10-137">Name</span></span>           | <span data-ttu-id="1cf10-138">Tür</span><span class="sxs-lookup"><span data-stu-id="1cf10-138">Type</span></span>   | <span data-ttu-id="1cf10-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1cf10-139">Required</span></span> | <span data-ttu-id="1cf10-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1cf10-140">Description</span></span>                                           |
|----------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="1cf10-141">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="1cf10-141">customer-id</span></span>    | <span data-ttu-id="1cf10-142">string</span><span class="sxs-lookup"><span data-stu-id="1cf10-142">string</span></span> | <span data-ttu-id="1cf10-143">Yes</span><span class="sxs-lookup"><span data-stu-id="1cf10-143">Yes</span></span>      | <span data-ttu-id="1cf10-144">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="1cf10-144">A GUID-formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="1cf10-145">devicebatch kimliği</span><span class="sxs-lookup"><span data-stu-id="1cf10-145">devicebatch-id</span></span> | <span data-ttu-id="1cf10-146">string</span><span class="sxs-lookup"><span data-stu-id="1cf10-146">string</span></span> | <span data-ttu-id="1cf10-147">Yes</span><span class="sxs-lookup"><span data-stu-id="1cf10-147">Yes</span></span>      | <span data-ttu-id="1cf10-148">Cihaz toplu işini tanımlayan bir dize tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="1cf10-148">A string identifier that identifies the device batch.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1cf10-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1cf10-149">Request headers</span></span>

<span data-ttu-id="1cf10-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1cf10-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1cf10-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1cf10-151">Request body</span></span>

<span data-ttu-id="1cf10-152">Yok</span><span class="sxs-lookup"><span data-stu-id="1cf10-152">None</span></span>

### <a name="request-example"></a><span data-ttu-id="1cf10-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1cf10-153">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/testbatch/devices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="1cf10-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1cf10-154">REST response</span></span>

<span data-ttu-id="1cf10-155">Başarılı olursa, yanıt gövdesi [cihaz](device-deployment-resources.md#device) kaynaklarının Sayfalanmış bir koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-155">If successful, the response body contains a paged collection of [Device](device-deployment-resources.md#device) resources.</span></span> <span data-ttu-id="1cf10-156">Koleksiyonda bir sayfada 100 cihaz bulunur.</span><span class="sxs-lookup"><span data-stu-id="1cf10-156">The collection contains 100 devices in a page.</span></span> <span data-ttu-id="1cf10-157">100 cihazlarındaki bir sonraki sayfayı almak için, yanıt gövdesinde continuationToken, sonraki isteğe bir MS-ContinuationToken üst bilgisi olarak eklenmelidir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-157">To retrieve the next page of 100 devices, the continuationToken in the response body must be included in the subsequent request as an MS-ContinuationToken header.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1cf10-158">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1cf10-158">Response success and error codes</span></span>

<span data-ttu-id="1cf10-159">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1cf10-159">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1cf10-160">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1cf10-160">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1cf10-161">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1cf10-161">For a full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1cf10-162">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1cf10-162">Response example</span></span>

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
