---
title: KIMLIĞE göre hizmet isteği ayrıntılarını alın.
description: KIMLIĞE göre mevcut bir müşteri hizmeti isteğinin ayrıntılarını alma.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c79fd3f5e5609a1893891e9b2a8078f8678497b3
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769899"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="01ec3-103">Kimliğe göre hizmet isteği ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="01ec3-103">Get service request details by ID</span></span>

<span data-ttu-id="01ec3-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="01ec3-104">**Applies To**</span></span>

- <span data-ttu-id="01ec3-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="01ec3-105">Partner Center</span></span>
- <span data-ttu-id="01ec3-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="01ec3-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="01ec3-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="01ec3-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="01ec3-108">Hizmet isteği tanımlayıcısını kullanarak mevcut bir müşteri hizmeti isteğinin ayrıntılarını alma.</span><span class="sxs-lookup"><span data-stu-id="01ec3-108">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="01ec3-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="01ec3-109">Prerequisites</span></span>

- <span data-ttu-id="01ec3-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="01ec3-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="01ec3-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="01ec3-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="01ec3-112">Bir hizmet isteği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="01ec3-112">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="01ec3-113">C\#</span><span class="sxs-lookup"><span data-stu-id="01ec3-113">C\#</span></span>

<span data-ttu-id="01ec3-114">Mevcut bir müşteri hizmeti isteğinin ayrıntılarını almak için, [**ıvicerequestcollection. Byıd**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) metodunu çağırın ve belirli [**servicerequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) nesnesine bir arabirim tanımlamak ve döndürmek için bir [**ServiceRequest.ID**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) geçirin.</span><span class="sxs-lookup"><span data-stu-id="01ec3-114">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest as ServiceRequest;

ServiceRequest serviceRequestDetails = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Get();

Console.WriteLine(string.Format("The primary contact for the service request {0} is {1} {2}.",
    serviceRequestDetails.Title,
    serviceRequestDetails.PrimaryContact.FirstName,
    serviceRequestDetails.PrimaryContact.LastName,
));
```

## <a name="rest-request"></a><span data-ttu-id="01ec3-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="01ec3-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="01ec3-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="01ec3-116">Request syntax</span></span>

| <span data-ttu-id="01ec3-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="01ec3-117">Method</span></span>    | <span data-ttu-id="01ec3-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="01ec3-118">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="01ec3-119">**Al**</span><span class="sxs-lookup"><span data-stu-id="01ec3-119">**GET**</span></span> | <span data-ttu-id="01ec3-120">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="01ec3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="01ec3-121">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="01ec3-121">URI parameter</span></span>

<span data-ttu-id="01ec3-122">Belirtilen hizmet isteğini almak için aşağıdaki URI parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="01ec3-122">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="01ec3-123">Ad</span><span class="sxs-lookup"><span data-stu-id="01ec3-123">Name</span></span>                  | <span data-ttu-id="01ec3-124">Tür</span><span class="sxs-lookup"><span data-stu-id="01ec3-124">Type</span></span>     | <span data-ttu-id="01ec3-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="01ec3-125">Required</span></span> | <span data-ttu-id="01ec3-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="01ec3-126">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="01ec3-127">**servicerequest kimliği**</span><span class="sxs-lookup"><span data-stu-id="01ec3-127">**servicerequest-id**</span></span> | <span data-ttu-id="01ec3-128">**guid**</span><span class="sxs-lookup"><span data-stu-id="01ec3-128">**guid**</span></span> | <span data-ttu-id="01ec3-129">Y</span><span class="sxs-lookup"><span data-stu-id="01ec3-129">Y</span></span>        | <span data-ttu-id="01ec3-130">Hizmet isteğini tanımlayan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="01ec3-130">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="01ec3-131">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="01ec3-131">Request headers</span></span>

<span data-ttu-id="01ec3-132">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="01ec3-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="01ec3-133">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="01ec3-133">Request body</span></span>

<span data-ttu-id="01ec3-134">Yok.</span><span class="sxs-lookup"><span data-stu-id="01ec3-134">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="01ec3-135">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="01ec3-135">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="01ec3-136">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="01ec3-136">REST response</span></span>

<span data-ttu-id="01ec3-137">Başarılı olursa, bu yöntem yanıt gövdesinde bir **hizmet isteği** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="01ec3-137">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="01ec3-138">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="01ec3-138">Response success and error codes</span></span>

<span data-ttu-id="01ec3-139">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="01ec3-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="01ec3-140">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="01ec3-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="01ec3-141">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="01ec3-141">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="01ec3-142">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="01ec3-142">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 566
Content-Type: application/json; charset=utf-8
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CV: rjLONPum/Uq94UQA.0
MS-ServerId: 030011719
Date: Mon, 09 Jan 2017 23:31:15 GMT

{
    "title": "TrialSR",
    "description": "Ignore this SR",
    "severity": "critical",
    "supportTopicId": "32444671",
    "supportTopicName": "Cannot manage my profile",
    "id": "616122292874576",
    "status": "open",
    "organization": {
        "id": "3b33e682-00c3-41ee-9dd2-a548adf56438",
        "name": "TEST_TEST_BugBash1"
    },
    "productId": "15960",
    "createdDate": "2016-12-22T20:31:17.24Z",
    "lastModifiedDate": "2017-01-09T23:31:15.373Z",
    "lastClosedDate": "0001-01-01T00:00:00",
    "notes": [{
            "createdByName": "Account",
            "createdDate": "2017-01-09T23:31:15.373",
            "text": "Sample Note"
        }
    ],
    "attributes": {
        "objectType": "ServiceRequest"
    }
}
```
