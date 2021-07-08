---
title: KIMLIĞE göre hizmet isteği ayrıntılarını alın.
description: KIMLIĞE göre mevcut bir müşteri hizmeti isteğinin ayrıntılarını alma.
ms.date: 02/06/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 66488cf9592d630cb1f0237d379e8df5ead6a3a8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548779"
---
# <a name="get-service-request-details-by-id"></a><span data-ttu-id="c5579-103">Kimliğe göre hizmet isteği ayrıntılarını alma</span><span class="sxs-lookup"><span data-stu-id="c5579-103">Get service request details by ID</span></span>

<span data-ttu-id="c5579-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c5579-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c5579-105">Hizmet isteği tanımlayıcısını kullanarak mevcut bir müşteri hizmeti isteğinin ayrıntılarını alma.</span><span class="sxs-lookup"><span data-stu-id="c5579-105">How to retrieve the details of an existing customer service request using the service request identifier.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c5579-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c5579-106">Prerequisites</span></span>

- <span data-ttu-id="c5579-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c5579-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c5579-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c5579-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="c5579-109">Bir hizmet isteği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="c5579-109">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="c5579-110">C\#</span><span class="sxs-lookup"><span data-stu-id="c5579-110">C\#</span></span>

<span data-ttu-id="c5579-111">Mevcut bir müşteri hizmeti isteğinin ayrıntılarını almak için, [**ıvicerequestcollection. Byıd**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) metodunu çağırın ve belirli [**servicerequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) nesnesine bir arabirim tanımlamak ve döndürmek için bir [**ServiceRequest.ID**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) geçirin.</span><span class="sxs-lookup"><span data-stu-id="c5579-111">To retrieve the details of an existing customer service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method, and pass in a [**ServiceRequest.Id**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest.id#Microsoft_Store_PartnerCenter_Models_ServiceRequests_ServiceRequest_Id) to identify and return an interface to the specific [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="c5579-112">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c5579-112">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c5579-113">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c5579-113">Request syntax</span></span>

| <span data-ttu-id="c5579-114">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c5579-114">Method</span></span>    | <span data-ttu-id="c5579-115">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c5579-115">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="c5579-116">**Al**</span><span class="sxs-lookup"><span data-stu-id="c5579-116">**GET**</span></span> | <span data-ttu-id="c5579-117">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c5579-117">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="c5579-118">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="c5579-118">URI parameter</span></span>

<span data-ttu-id="c5579-119">Belirtilen hizmet isteğini almak için aşağıdaki URI parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c5579-119">Use the following URI parameter to get the specified service request.</span></span>

| <span data-ttu-id="c5579-120">Ad</span><span class="sxs-lookup"><span data-stu-id="c5579-120">Name</span></span>                  | <span data-ttu-id="c5579-121">Tür</span><span class="sxs-lookup"><span data-stu-id="c5579-121">Type</span></span>     | <span data-ttu-id="c5579-122">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c5579-122">Required</span></span> | <span data-ttu-id="c5579-123">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c5579-123">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="c5579-124">**servicerequest kimliği**</span><span class="sxs-lookup"><span data-stu-id="c5579-124">**servicerequest-id**</span></span> | <span data-ttu-id="c5579-125">**guid**</span><span class="sxs-lookup"><span data-stu-id="c5579-125">**guid**</span></span> | <span data-ttu-id="c5579-126">Y</span><span class="sxs-lookup"><span data-stu-id="c5579-126">Y</span></span>        | <span data-ttu-id="c5579-127">Hizmet isteğini tanımlayan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="c5579-127">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c5579-128">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c5579-128">Request headers</span></span>

<span data-ttu-id="c5579-129">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c5579-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c5579-130">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c5579-130">Request body</span></span>

<span data-ttu-id="c5579-131">Yok.</span><span class="sxs-lookup"><span data-stu-id="c5579-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c5579-132">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c5579-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="c5579-133">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c5579-133">REST response</span></span>

<span data-ttu-id="c5579-134">Başarılı olursa, bu yöntem yanıt gövdesinde bir **hizmet isteği** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="c5579-134">If successful, this method returns a **Service Request** resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c5579-135">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c5579-135">Response success and error codes</span></span>

<span data-ttu-id="c5579-136">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c5579-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c5579-137">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c5579-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c5579-138">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c5579-138">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c5579-139">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c5579-139">Response example</span></span>

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
