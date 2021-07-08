---
title: Cihaz toplu karşıya yükleme durumu alma
description: Belirli bir müşteri için bir cihaz toplu karşıya yükleme işleminin durumunu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: fd8726af41fe4399797f39a0790cf962fde64acc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548490"
---
# <a name="get-the-status-of-a-device-batch-upload"></a><span data-ttu-id="80314-103">Cihaz toplu karşıya yükleme durumu alma</span><span class="sxs-lookup"><span data-stu-id="80314-103">Get the status of a device batch upload</span></span>

<span data-ttu-id="80314-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="80314-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="80314-105">Belirli bir müşteri için bir cihaz toplu karşıya yükleme işleminin durumunu alma.</span><span class="sxs-lookup"><span data-stu-id="80314-105">How to get the status of a device batch upload for a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80314-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="80314-106">Prerequisites</span></span>

- <span data-ttu-id="80314-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="80314-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80314-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="80314-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="80314-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80314-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80314-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80314-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80314-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="80314-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80314-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="80314-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80314-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="80314-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80314-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="80314-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="80314-115">Cihaz toplu işi gönderildiğinde konum üstbilgisinde döndürülen toplu iş izleme tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="80314-115">The batch tracking identifier returned in the Location header when the device batch was submitted.</span></span> <span data-ttu-id="80314-116">daha fazla bilgi için, bkz. [belirtilen müşteri için cihazların listesini Upload](upload-a-list-of-devices-for-the-specified-customer.md).</span><span class="sxs-lookup"><span data-stu-id="80314-116">For more information, see [Upload a list of devices for the specified customer](upload-a-list-of-devices-for-the-specified-customer.md).</span></span>

## <a name="c"></a><span data-ttu-id="80314-117">C\#</span><span class="sxs-lookup"><span data-stu-id="80314-117">C\#</span></span>

<span data-ttu-id="80314-118">Bir cihaz toplu karşıya yükleme işleminin durumunu almak için, önce belirtilen müşterideki işlemlere bir arabirim almak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80314-118">To get the status of a device batch upload, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="80314-119">Ardından, toplu karşıya yükleme durum işlemlerine bir arabirim almak için toplu izleme KIMLIĞIYLE [**Batchuploadstatus. Byıd**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="80314-119">Then, call the [**BatchUploadStatus.ById**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatuscollection.byid) method with the batch tracking ID to get an interface to batch upload status operations.</span></span> <span data-ttu-id="80314-120">Son olarak, durumu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80314-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.ibatchjobstatus.getasync) method to retrieve the status.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedTrackingId;

var status =
    partnerOperations.Customers.ById(selectedCustomerId).BatchUploadStatus.ById(selectedTrackingId).Get();
```

<span data-ttu-id="80314-121">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80314-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80314-122">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getbatchuploadstatus. cs</span><span class="sxs-lookup"><span data-stu-id="80314-122">**Project**: Partner Center SDK Samples **Class**: GetBatchUploadStatus.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="80314-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="80314-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80314-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="80314-124">Request syntax</span></span>

| <span data-ttu-id="80314-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="80314-125">Method</span></span>  | <span data-ttu-id="80314-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="80314-126">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80314-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="80314-127">**GET**</span></span> | <span data-ttu-id="80314-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/batchjobstatus/{batchtracking-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="80314-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/batchJobStatus/{batchtracking-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="80314-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="80314-129">URI parameter</span></span>

<span data-ttu-id="80314-130">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="80314-130">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="80314-131">Ad</span><span class="sxs-lookup"><span data-stu-id="80314-131">Name</span></span>             | <span data-ttu-id="80314-132">Tür</span><span class="sxs-lookup"><span data-stu-id="80314-132">Type</span></span>   | <span data-ttu-id="80314-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="80314-133">Required</span></span> | <span data-ttu-id="80314-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="80314-134">Description</span></span>                                                                                                                                                                    |
|------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80314-135">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="80314-135">customer-id</span></span>      | <span data-ttu-id="80314-136">string</span><span class="sxs-lookup"><span data-stu-id="80314-136">string</span></span> | <span data-ttu-id="80314-137">Yes</span><span class="sxs-lookup"><span data-stu-id="80314-137">Yes</span></span>      | <span data-ttu-id="80314-138">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="80314-138">A GUID-formatted string that identifies the customer.</span></span>                                                                                                                          |
| <span data-ttu-id="80314-139">batchtracking kimliği</span><span class="sxs-lookup"><span data-stu-id="80314-139">batchtracking-id</span></span> | <span data-ttu-id="80314-140">string</span><span class="sxs-lookup"><span data-stu-id="80314-140">string</span></span> | <span data-ttu-id="80314-141">Yes</span><span class="sxs-lookup"><span data-stu-id="80314-141">Yes</span></span>      | <span data-ttu-id="80314-142">Bir cihaz toplu karşıya yükleme durumunu almak için kullanılan GUID biçimli bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="80314-142">A GUID-formatted identifier that is used to retrieve a device batch upload status.</span></span> <span data-ttu-id="80314-143">Bu KIMLIK, cihaz toplu işi başarıyla gönderildiğinde konum üst bilgisinde döndürülür.</span><span class="sxs-lookup"><span data-stu-id="80314-143">This ID is returned in the Location header when the device batch is successfully submitted.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80314-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="80314-144">Request headers</span></span>

<span data-ttu-id="80314-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="80314-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80314-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="80314-146">Request body</span></span>

<span data-ttu-id="80314-147">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="80314-147">None</span></span>

### <a name="request-example"></a><span data-ttu-id="80314-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="80314-148">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/batchjobstatus/0127ed8e-ff72-4983-a3d8-e8d8bd378932 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="80314-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="80314-149">REST response</span></span>

<span data-ttu-id="80314-150">Başarılı olursa, yanıt bir [Batchuploaddetails](device-deployment-resources.md#batchuploaddetails) kaynağı içerir.</span><span class="sxs-lookup"><span data-stu-id="80314-150">If successful, the response contains a [BatchUploadDetails](device-deployment-resources.md#batchuploaddetails) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80314-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="80314-151">Response success and error codes</span></span>

<span data-ttu-id="80314-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="80314-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80314-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="80314-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80314-154">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="80314-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80314-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="80314-155">Response example</span></span>

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
