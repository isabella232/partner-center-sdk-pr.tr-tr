---
title: Bir hizmet isteğini güncelleştirme
description: Bir bulut çözümü sağlayıcısı 'nın müşterinin adına Microsoft ile dosyalandığı mevcut bir müşteri hizmeti isteğini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a1df0d1f5fa4630b346d1c8b9cffabb86ce34cfb
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769742"
---
# <a name="update-a-service-request"></a><span data-ttu-id="7e576-103">Bir hizmet isteğini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="7e576-103">Update a service request</span></span>

<span data-ttu-id="7e576-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="7e576-104">**Applies To**</span></span>

- <span data-ttu-id="7e576-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7e576-105">Partner Center</span></span>
- <span data-ttu-id="7e576-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7e576-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7e576-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7e576-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7e576-108">Bir bulut çözümü sağlayıcısı 'nın müşterinin adına Microsoft ile dosyalandığı mevcut bir müşteri hizmeti isteğini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="7e576-108">How to update an existing customer service request that a Cloud Solution Provider has filed with Microsoft on the customer's behalf.</span></span>

<span data-ttu-id="7e576-109">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="7e576-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="7e576-110">Sonra sol kenar çubuğundan **hizmet yönetimi** ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="7e576-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="7e576-111">**Destek istekleri** üst bilgisi altında, söz konusu hizmet isteğini seçin.</span><span class="sxs-lookup"><span data-stu-id="7e576-111">Under the **Support requests** header, select the service request in question.</span></span> <span data-ttu-id="7e576-112">Son olarak, hizmet isteğinde istenen değişiklikleri yapıp Gönder ' i seçin **.**</span><span class="sxs-lookup"><span data-stu-id="7e576-112">To finish, make the desired changes to the service request then select **Submit.**</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7e576-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7e576-113">Prerequisites</span></span>

- <span data-ttu-id="7e576-114">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7e576-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7e576-115">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7e576-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7e576-116">Bir hizmet isteği KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7e576-116">A service request ID.</span></span>

## <a name="c"></a><span data-ttu-id="7e576-117">C\#</span><span class="sxs-lookup"><span data-stu-id="7e576-117">C\#</span></span>

<span data-ttu-id="7e576-118">Bir müşterinin hizmet isteğini güncelleştirmek için, hizmet isteği arabirimini tanımlamak ve döndürmek üzere hizmet isteği kimliğiyle [**ıvicerequestcollection. Byıd**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7e576-118">To update a customer's service request, call the [**IServiceRequestCollection.ById**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.byid) method with the service request id to identify and return the service request interface.</span></span> <span data-ttu-id="7e576-119">Ardından, hizmet isteğini güncelleştirmek için [**ıvicerequest. Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) veya [**patchasync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="7e576-119">Then call the [**IServiceRequest.Patch**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patch) or [**PatchAsync**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequest.patchasync) method to update the service request.</span></span> <span data-ttu-id="7e576-120">Güncelleştirilmiş değerleri sağlamak için yeni ve boş bir [**servicerequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) nesnesi oluşturun ve yalnızca değiştirmek istediğiniz özellik değerlerini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7e576-120">To provide the updated values, create a new, empty [**ServiceRequest**](/dotnet/api/microsoft.store.partnercenter.models.servicerequests.servicerequest) object and set only the property values that you want to change.</span></span> <span data-ttu-id="7e576-121">Sonra bu nesneyi düzeltme ekine veya PatchAsync metoduna çağrı içinde geçirin.</span><span class="sxs-lookup"><span data-stu-id="7e576-121">Then pass that object in the call to the Patch or PatchAsync method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// ServiceRequest existingServiceRequest;

ServiceRequest updatedServiceRequest = partnerOperations.ServiceRequests.ById(existingServiceRequest.Id).Patch(new ServiceRequest
{
   NewNote = note
});
```

<span data-ttu-id="7e576-122">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="7e576-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="7e576-123">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdatePartnerServiceRequest.cs</span><span class="sxs-lookup"><span data-stu-id="7e576-123">**Project**: Partner Center SDK Samples **Class**: UpdatePartnerServiceRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7e576-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7e576-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7e576-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7e576-125">Request syntax</span></span>

| <span data-ttu-id="7e576-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7e576-126">Method</span></span>    | <span data-ttu-id="7e576-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7e576-127">Request URI</span></span>                                                                                 |
|-----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="7e576-128">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="7e576-128">**PATCH**</span></span> | <span data-ttu-id="7e576-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7e576-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/servicerequests/{servicerequest-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7e576-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="7e576-130">URI parameter</span></span>

<span data-ttu-id="7e576-131">Hizmet isteğini güncelleştirmek için aşağıdaki URI parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e576-131">Use the following URI parameter to update the service request.</span></span>

| <span data-ttu-id="7e576-132">Ad</span><span class="sxs-lookup"><span data-stu-id="7e576-132">Name</span></span>                  | <span data-ttu-id="7e576-133">Tür</span><span class="sxs-lookup"><span data-stu-id="7e576-133">Type</span></span>     | <span data-ttu-id="7e576-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7e576-134">Required</span></span> | <span data-ttu-id="7e576-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7e576-135">Description</span></span>                                 |
|-----------------------|----------|----------|---------------------------------------------|
| <span data-ttu-id="7e576-136">**servicerequest kimliği**</span><span class="sxs-lookup"><span data-stu-id="7e576-136">**servicerequest-id**</span></span> | <span data-ttu-id="7e576-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="7e576-137">**guid**</span></span> | <span data-ttu-id="7e576-138">Y</span><span class="sxs-lookup"><span data-stu-id="7e576-138">Y</span></span>        | <span data-ttu-id="7e576-139">Hizmet isteğini tanımlayan bir GUID.</span><span class="sxs-lookup"><span data-stu-id="7e576-139">A GUID that identifies the service request.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7e576-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7e576-140">Request headers</span></span>

<span data-ttu-id="7e576-141">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7e576-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7e576-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7e576-142">Request body</span></span>

<span data-ttu-id="7e576-143">İstek gövdesi bir [servicerequest](service-request-resources.md) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="7e576-143">The request body should contain a [ServiceRequest](service-request-resources.md) resource.</span></span> <span data-ttu-id="7e576-144">Yalnızca gerekli değerler güncellenmelidir.</span><span class="sxs-lookup"><span data-stu-id="7e576-144">The only required values are those to be updated.</span></span>

### <a name="request-example"></a><span data-ttu-id="7e576-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7e576-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="7e576-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7e576-146">REST response</span></span>

<span data-ttu-id="7e576-147">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş özelliklerle bir **hizmet isteği** kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="7e576-147">If successful, this method returns a **Service Request** resource with updated properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7e576-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7e576-148">Response success and error codes</span></span>

<span data-ttu-id="7e576-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7e576-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7e576-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7e576-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7e576-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7e576-151">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7e576-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7e576-152">Response example</span></span>

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
