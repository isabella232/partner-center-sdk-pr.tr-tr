---
title: Bir hizmet isteğini güncelleştirme
description: Bir müşterinin Microsoft'a müşteri adına Bulut Çözümü Sağlayıcısı mevcut müşteri hizmetleri isteğini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: efa7b2a98b6f95a763ca6e3811c43cc655c18e2b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530098"
---
# <a name="update-a-service-request"></a><span data-ttu-id="e50b6-103">Bir hizmet isteğini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="e50b6-103">Update a service request</span></span>

<span data-ttu-id="e50b6-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="e50b6-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="e50b6-105">Bir müşterinin Microsoft'a müşteri adına Bulut Çözümü Sağlayıcısı mevcut müşteri hizmetleri isteğini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="e50b6-105">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="e50b6-106">Bu İş Ortağı Merkezi önce bir müşteri [seçerek gerçekleştirebilirsiniz.](get-a-customer-by-name.md)</span><span class="sxs-lookup"><span data-stu-id="e50b6-106">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="e50b6-107">Ardından, sol **kenar çubuğuna** Hizmet yönetimi'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="e50b6-107">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="e50b6-108">Destek **istekleri üst bilgisi** altında söz konusu hizmet isteğini seçin.</span><span class="sxs-lookup"><span data-stu-id="e50b6-108">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="e50b6-109">Tamamlamak için hizmet isteğinde istediğiniz değişiklikleri yapın ve Gönder'i **seçin.**</span><span class="sxs-lookup"><span data-stu-id="e50b6-109">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="e50b6-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="e50b6-110">Prerequisites</span></span>

- <span data-ttu-id="e50b6-111">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="e50b6-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="e50b6-112">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="e50b6-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="e50b6-113">Hizmet isteği kimliği.</span><span class="sxs-lookup"><span data-stu-id="e50b6-113">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="e50b6-114">C\#</span><span class="sxs-lookup"><span data-stu-id="e50b6-114">C\#</span></span>

<span data-ttu-id="e50b6-115">Müşterinin hizmet isteğini güncelleştirmek için [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) yöntemini hizmet isteği kimliğiyle çağırarak hizmet isteği arabirimini tanıyın ve geri girin.</span><span class="sxs-lookup"><span data-stu-id="e50b6-115">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request ID to identify and return the service request interface.</span></span> <span data-ttu-id="e50b6-116">Ardından hizmet isteğini [**güncelleştirmek için IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) veya [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="e50b6-116">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="e50b6-117">Güncelleştirilmiş değerleri sağlamak için yeni, boş bir [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) nesnesi oluşturun ve yalnızca değiştirmek istediğiniz özellik değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="e50b6-117">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="e50b6-118">Ardından patch veya PatchAsync yöntemine çağrıda bu nesneyi iletir.</span><span class="sxs-lookup"><span data-stu-id="e50b6-118">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="e50b6-119">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="e50b6-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="e50b6-120">**Project:** İş Ortağı Merkezi SDK'sı **Sınıfı:** UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="e50b6-120">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="e50b6-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="e50b6-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="e50b6-122">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="e50b6-122">Request syntax</span></span>

| <span data-ttu-id="e50b6-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="e50b6-123">Method</span></span>    | <span data-ttu-id="e50b6-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="e50b6-124">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="e50b6-125">**Yama**</span><span class="sxs-lookup"><span data-stu-id="e50b6-125">**PATCH**</span></span> | <span data-ttu-id="e50b6-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="e50b6-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="e50b6-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="e50b6-127">URI parameter</span></span>

<span data-ttu-id="e50b6-128">Hizmet isteğini güncelleştirmek için aşağıdaki URI parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="e50b6-128">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="e50b6-129">Ad</span><span class="sxs-lookup"><span data-stu-id="e50b6-129">Name</span></span>                  | <span data-ttu-id="e50b6-130">Tür</span><span class="sxs-lookup"><span data-stu-id="e50b6-130">Type</span></span>     | <span data-ttu-id="e50b6-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="e50b6-131">Required</span></span> | <span data-ttu-id="e50b6-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="e50b6-132">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="e50b6-133">**servicerequest-id**</span><span class="sxs-lookup"><span data-stu-id="e50b6-133">**servicerequest-id**</span></span> | <span data-ttu-id="e50b6-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="e50b6-134">**guid**</span></span> | <span data-ttu-id="e50b6-135">Y</span><span class="sxs-lookup"><span data-stu-id="e50b6-135">Y</span></span>        | <span data-ttu-id="e50b6-136">Hizmet isteğini tanımlayan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="e50b6-136">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="e50b6-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="e50b6-137">Request headers</span></span>

<span data-ttu-id="e50b6-138">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="e50b6-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="e50b6-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="e50b6-139">Request body</span></span>

<span data-ttu-id="e50b6-140">İstek gövdesi bir [ServiceRequest kaynağı içermeli.](service-request-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e50b6-140">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="e50b6-141">Yalnızca güncelleştirilen değerler gereklidir.</span><span class="sxs-lookup"><span data-stu-id="e50b6-141">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="e50b6-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="e50b6-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/servicerequests/616122292874576 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f9a030bd-e492-4c1a-9c70-021f18234981
MS-CorrelationId: fd969070-4e5f-4c6b-a3c6-1941283b39ae
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 508
Expect: 100-continue

{
    "Id": null,
    "Title": null,
    "Description": null,
    "Severity": "unknown",
    "SupportTopicId": null,
    "SupportTopicName": null,
    "Status": "none",
    "Organization": null,
    "PrimaryContact": null,
    "LastUpdatedBy": null,
    "ProductName": null,
    "ProductId": null,
    "CreatedDate": "0001-01-01T00:00:00",
    "LastModifiedDate": "0001-01-01T00:00:00",
    "LastClosedDate": "0001-01-01T00:00:00",
    "NewNote": {
        "CreatedByName": null,
        "CreatedDate": null,
        "Text": "Sample Note"
    },
    "Notes": null,
    "CountryCode": null,
    "FileLinks": null,
    "Attributes": {
        "ObjectType": "ServiceRequest"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="e50b6-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="e50b6-143">REST response</span></span>

<span data-ttu-id="e50b6-144">Başarılı olursa, bu yöntem yanıt **gövdesinde güncelleştirilmiş** özelliklere sahip bir Hizmet İsteği kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="e50b6-144">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="e50b6-145">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="e50b6-145">Response success and error codes</span></span>

<span data-ttu-id="e50b6-146">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="e50b6-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="e50b6-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="e50b6-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="e50b6-148">Tam liste için bkz. [REST İş Ortağı Merkezi Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="e50b6-148">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="e50b6-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="e50b6-149">Response example</span></span>

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
