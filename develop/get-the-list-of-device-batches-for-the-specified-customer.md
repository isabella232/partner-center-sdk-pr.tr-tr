---
title: Belirtilen müşteri için cihaz toplu işlemlerinin bir listesini alma
description: Belirtilen müşteri için bir cihaz toplu işi koleksiyonu alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ea5797bbaff4d4eafd1e63428556ab784bcb0ee2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769809"
---
# <a name="get-a-list-of-device-batches-for-the-specified-customer"></a><span data-ttu-id="f50c1-103">Belirtilen müşteri için cihaz toplu işlemlerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="f50c1-103">Get a list of device batches for the specified customer</span></span>

<span data-ttu-id="f50c1-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="f50c1-104">**Applies To**</span></span>

- <span data-ttu-id="f50c1-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f50c1-105">Partner Center</span></span>
- <span data-ttu-id="f50c1-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f50c1-106">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="f50c1-107">Belirtilen müşteri için bir cihaz toplu işi koleksiyonu alma.</span><span class="sxs-lookup"><span data-stu-id="f50c1-107">How to retrieve a collection of device batches for the specified customer.</span></span>

<span data-ttu-id="f50c1-108">Her bir cihaz toplu işi, sıfır dokunma dağıtımına kaydedilmiş cihazlarla ilgili Özet durum bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="f50c1-108">Each device batch contains summary status information about devices that have been enrolled in zero-touch deployment.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f50c1-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f50c1-109">Prerequisites</span></span>

- <span data-ttu-id="f50c1-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f50c1-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f50c1-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="f50c1-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="f50c1-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f50c1-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f50c1-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f50c1-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f50c1-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f50c1-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f50c1-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f50c1-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f50c1-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="f50c1-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f50c1-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="f50c1-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f50c1-118">C\#</span><span class="sxs-lookup"><span data-stu-id="f50c1-118">C\#</span></span>

<span data-ttu-id="f50c1-119">Belirtilen müşteriye ait cihaz toplu işleri koleksiyonunu almak için, önce belirtilen müşteri üzerinde işlemlere bir arabirim almak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f50c1-119">To get the collection of device batches for the specified customer, first call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to retrieve an interface to operations on the specified customer.</span></span> <span data-ttu-id="f50c1-120">Ardından, cihaz toplu işlem koleksiyonu işlemlerine bir arabirim almak için [**devicebatch**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="f50c1-120">Then, retrieve the value of the [**DeviceBatches**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.devicebatches) property to get an interface to device batch collection operations.</span></span> <span data-ttu-id="f50c1-121">Son olarak, koleksiyonu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f50c1-121">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.devicesdeployment.idevicesbatchcollection.getasync) method to retrieve the collection.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

var devicesBatches =
    partnerOperations.Customers.ById(selectedCustomerId).DeviceBatches.Get();
```

<span data-ttu-id="f50c1-122">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f50c1-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f50c1-123">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetDevicesBatches.cs</span><span class="sxs-lookup"><span data-stu-id="f50c1-123">**Project**: Partner Center SDK Samples **Class**: GetDevicesBatches.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f50c1-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f50c1-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f50c1-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f50c1-125">Request syntax</span></span>

| <span data-ttu-id="f50c1-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f50c1-126">Method</span></span>  | <span data-ttu-id="f50c1-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f50c1-127">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f50c1-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="f50c1-128">**GET**</span></span> | <span data-ttu-id="f50c1-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/deviceyığınları http/1.1</span><span class="sxs-lookup"><span data-stu-id="f50c1-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/deviceBatches HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f50c1-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="f50c1-130">URI parameter</span></span>

<span data-ttu-id="f50c1-131">İsteği oluştururken aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f50c1-131">Use the following path parameters when creating the request.</span></span>

| <span data-ttu-id="f50c1-132">Ad</span><span class="sxs-lookup"><span data-stu-id="f50c1-132">Name</span></span>        | <span data-ttu-id="f50c1-133">Tür</span><span class="sxs-lookup"><span data-stu-id="f50c1-133">Type</span></span>   | <span data-ttu-id="f50c1-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f50c1-134">Required</span></span> | <span data-ttu-id="f50c1-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f50c1-135">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="f50c1-136">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="f50c1-136">customer-id</span></span> | <span data-ttu-id="f50c1-137">string</span><span class="sxs-lookup"><span data-stu-id="f50c1-137">string</span></span> | <span data-ttu-id="f50c1-138">Yes</span><span class="sxs-lookup"><span data-stu-id="f50c1-138">Yes</span></span>      | <span data-ttu-id="f50c1-139">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="f50c1-139">A GUID-formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="f50c1-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f50c1-140">Request headers</span></span>

<span data-ttu-id="f50c1-141">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f50c1-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f50c1-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f50c1-142">Request body</span></span>

<span data-ttu-id="f50c1-143">Yok</span><span class="sxs-lookup"><span data-stu-id="f50c1-143">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f50c1-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f50c1-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/47021739-3426-40bf-9601-61b4b6d7c793/deviceBatches HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f50c1-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f50c1-145">REST response</span></span>

<span data-ttu-id="f50c1-146">Başarılı olursa, yanıt gövdesi [Devicebatch](device-deployment-resources.md#devicebatch) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f50c1-146">If successful, the response body contains the collection of [DeviceBatch](device-deployment-resources.md#devicebatch) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f50c1-147">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f50c1-147">Response success and error codes</span></span>

<span data-ttu-id="f50c1-148">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="f50c1-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f50c1-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f50c1-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f50c1-150">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f50c1-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f50c1-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f50c1-151">Response example</span></span>

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
