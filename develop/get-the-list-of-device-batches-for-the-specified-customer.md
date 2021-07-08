---
title: Belirtilen müşteri için cihaz toplu işlemlerinin bir listesini alma
description: Belirtilen müşteri için bir cihaz toplu işi koleksiyonu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9d020bbfa1faef0be423d2fef2d8982465dfa21f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548438"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="5e21b-103">Belirtilen müşteri için cihaz toplu işlemlerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="5e21b-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="5e21b-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5e21b-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="5e21b-105">Belirtilen müşteri için bir cihaz toplu işi koleksiyonu alma.</span><span class="sxs-lookup"><span data-stu-id="5e21b-105">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="5e21b-106">Her bir cihaz toplu işi, sıfır dokunma dağıtımına kaydedilmiş cihazlarla ilgili Özet durum bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="5e21b-106">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e21b-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5e21b-107">Prerequisites</span></span>

- <span data-ttu-id="5e21b-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5e21b-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5e21b-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5e21b-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5e21b-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5e21b-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5e21b-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e21b-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5e21b-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5e21b-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5e21b-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5e21b-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5e21b-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="5e21b-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5e21b-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="5e21b-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="5e21b-116">C\#</span><span class="sxs-lookup"><span data-stu-id="5e21b-116">C\#</span></span>

<span data-ttu-id="5e21b-117">Belirtilen müşteriye ait cihaz toplu işleri koleksiyonunu almak için, önce belirtilen müşteri üzerinde işlemlere bir arabirim almak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5e21b-117">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="5e21b-118">Ardından, cihaz toplu işlem koleksiyonu işlemlerine bir arabirim almak için [**devicebatch**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="5e21b-118">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="5e21b-119">Son olarak, koleksiyonu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5e21b-119">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="5e21b-120">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e21b-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5e21b-121">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getdevicestoplu iş. cs</span><span class="sxs-lookup"><span data-stu-id="5e21b-121">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5e21b-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5e21b-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5e21b-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5e21b-123">Request syntax</span></span>

| <span data-ttu-id="5e21b-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5e21b-124">Method</span></span>  | <span data-ttu-id="5e21b-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5e21b-125">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="5e21b-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="5e21b-126">**GET**</span></span> | <span data-ttu-id="5e21b-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/deviceyığınları http/1.1</span><span class="sxs-lookup"><span data-stu-id="5e21b-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5e21b-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="5e21b-128">URI parameter</span></span>

<span data-ttu-id="5e21b-129">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e21b-129">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="5e21b-130">Ad</span><span class="sxs-lookup"><span data-stu-id="5e21b-130">Name</span></span>        | <span data-ttu-id="5e21b-131">Tür</span><span class="sxs-lookup"><span data-stu-id="5e21b-131">Type</span></span>   | <span data-ttu-id="5e21b-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5e21b-132">Required</span></span> | <span data-ttu-id="5e21b-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e21b-133">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="5e21b-134">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="5e21b-134">customer-id</span></span> | <span data-ttu-id="5e21b-135">string</span><span class="sxs-lookup"><span data-stu-id="5e21b-135">string</span></span> | <span data-ttu-id="5e21b-136">Yes</span><span class="sxs-lookup"><span data-stu-id="5e21b-136">Yes</span></span>      | <span data-ttu-id="5e21b-137">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="5e21b-137">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5e21b-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5e21b-138">Request headers</span></span>

<span data-ttu-id="5e21b-139">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5e21b-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5e21b-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5e21b-140">Request body</span></span>

<span data-ttu-id="5e21b-141">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="5e21b-141">None</span></span>

### <a name="request-example"></a><span data-ttu-id="5e21b-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5e21b-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5e21b-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5e21b-143">REST response</span></span>

<span data-ttu-id="5e21b-144">Başarılı olursa, yanıt gövdesi [Devicebatch](device-deployment-resources.md#devicebatch) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="5e21b-144">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5e21b-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5e21b-145">Response success and error codes</span></span>

<span data-ttu-id="5e21b-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5e21b-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5e21b-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e21b-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5e21b-148">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5e21b-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5e21b-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5e21b-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 339
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 4a5002a2-0c1b-4e57-b491-dbcf19c0e7b8
MS-RequestId: 7b3e2e00-b330-4480-9d84-59ace713427f
MS-CV: YrLe3w6BbUSMt1fi.0
MS-ServerId: 030020344
Date: Tue, 25 Jul 2017 17:52:41 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "Test batch",
            "status": "finished",
            "creationDate": "2017-07-25T01:51:00",
            "devicesCount": 5,
            "devicesLink": {
                "uri": "/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches/Test batch/devices",
                "method": "GET",
                "headers": []
            },
            "attributes": {
                "objectType": "DeviceBatch"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
