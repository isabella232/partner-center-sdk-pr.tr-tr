---
title: Cihaz toplu karşıya yükleme durumu alma
description: Belirli bir müşteri için bir cihaz toplu karşıya yükleme işleminin durumunu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fb887ba257d6fbe68f95ae4b59d701ac4c934860
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769796"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="d98f6-103">Cihaz toplu karşıya yükleme durumu alma</span><span class="sxs-lookup"><span data-stu-id="d98f6-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="d98f6-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="d98f6-104">**Applies To**</span></span>

- <span data-ttu-id="d98f6-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d98f6-105">Partner Center</span></span>
- <span data-ttu-id="d98f6-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d98f6-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="d98f6-107">Belirli bir müşteri için bir cihaz toplu karşıya yükleme işleminin durumunu alma.</span><span class="sxs-lookup"><span data-stu-id="d98f6-107">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d98f6-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d98f6-108">Prerequisites</span></span>

- <span data-ttu-id="d98f6-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d98f6-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d98f6-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="d98f6-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="d98f6-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d98f6-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d98f6-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d98f6-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d98f6-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="d98f6-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d98f6-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d98f6-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d98f6-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="d98f6-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d98f6-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="d98f6-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d98f6-117">Cihaz toplu işi gönderildiğinde konum üstbilgisinde döndürülen toplu iş izleme tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="d98f6-117">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="d98f6-118">Daha fazla bilgi için bkz. [belirtilen müşteri için cihaz listesini karşıya yükleme](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="d98f6-118">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="d98f6-119">C\#</span><span class="sxs-lookup"><span data-stu-id="d98f6-119">C\#</span></span>

<span data-ttu-id="d98f6-120">Bir cihaz toplu karşıya yükleme işleminin durumunu almak için, önce belirtilen müşterideki işlemlere bir arabirim almak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d98f6-120">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="d98f6-121">Ardından, toplu karşıya yükleme durum işlemlerine bir arabirim almak için toplu izleme KIMLIĞIYLE [**Batchuploadstatus. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="d98f6-121">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="d98f6-122">Son olarak, durumu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d98f6-122">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="d98f6-123">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d98f6-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d98f6-124">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetBatchUploadStatus.cs</span><span class="sxs-lookup"><span data-stu-id="d98f6-124">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d98f6-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d98f6-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d98f6-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d98f6-126">Request syntax</span></span>

| <span data-ttu-id="d98f6-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d98f6-127">Method</span></span>  | <span data-ttu-id="d98f6-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d98f6-128">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d98f6-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="d98f6-129">**GET**</span></span> | <span data-ttu-id="d98f6-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/batchjobstatus/{batchtracking-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d98f6-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d98f6-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d98f6-131">URI parameter</span></span>

<span data-ttu-id="d98f6-132">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d98f6-132">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="d98f6-133">Ad</span><span class="sxs-lookup"><span data-stu-id="d98f6-133">Name</span></span>             | <span data-ttu-id="d98f6-134">Tür</span><span class="sxs-lookup"><span data-stu-id="d98f6-134">Type</span></span>   | <span data-ttu-id="d98f6-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d98f6-135">Required</span></span> | <span data-ttu-id="d98f6-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d98f6-136">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d98f6-137">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="d98f6-137">customer-id</span></span>      | <span data-ttu-id="d98f6-138">string</span><span class="sxs-lookup"><span data-stu-id="d98f6-138">string</span></span> | <span data-ttu-id="d98f6-139">Yes</span><span class="sxs-lookup"><span data-stu-id="d98f6-139">Yes</span></span>      | <span data-ttu-id="d98f6-140">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="d98f6-140">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="d98f6-141">batchtracking kimliği</span><span class="sxs-lookup"><span data-stu-id="d98f6-141">batchtracking-id</span></span> | <span data-ttu-id="d98f6-142">string</span><span class="sxs-lookup"><span data-stu-id="d98f6-142">string</span></span> | <span data-ttu-id="d98f6-143">Yes</span><span class="sxs-lookup"><span data-stu-id="d98f6-143">Yes</span></span>      | <span data-ttu-id="d98f6-144">Bir cihaz toplu karşıya yükleme durumunu almak için kullanılan GUID biçimli bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="d98f6-144">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="d98f6-145">Bu KIMLIK, cihaz toplu işi başarıyla gönderildiğinde konum üst bilgisinde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="d98f6-145">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d98f6-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d98f6-146">Request headers</span></span>

<span data-ttu-id="d98f6-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d98f6-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d98f6-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d98f6-148">Request body</span></span>

<span data-ttu-id="d98f6-149">Yok</span><span class="sxs-lookup"><span data-stu-id="d98f6-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="d98f6-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d98f6-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="d98f6-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d98f6-151">REST response</span></span>

<span data-ttu-id="d98f6-152">Başarılı olursa, yanıt bir [Batchuploaddetails](device-deployment-resources.md#batchuploaddetails) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="d98f6-152">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d98f6-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d98f6-153">Response success and error codes</span></span>

<span data-ttu-id="d98f6-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="d98f6-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d98f6-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d98f6-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d98f6-156">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d98f6-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d98f6-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d98f6-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 400
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "batchTrackingId": "0127ed8e-ff72-4983-a3d8-e8d8bd378932",
    "status": "finished",
    "startedTime": "2017-07-25T10:00:00",
    "completedTime": "2017-07-25T10:10:00",
    "devicesStatus": [{
            "serialNumber": "1234567890",
            "productKey": "12345-67890-09876-54321-13579",
            "status": "finished_with_errors",
            "errorCode": "808",
            "errorDescription": "ZtdDeviceAssignedToOtherTenant",
            "attributes": {
                "objectType": "DeviceUploadDetails"
            }
        }
    ],
    "attributes": {
        "objectType": "BatchUploadDetails"
    }
}
```
