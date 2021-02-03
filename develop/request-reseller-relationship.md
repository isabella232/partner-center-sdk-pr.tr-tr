---
title: İlişki isteği URL’sini alma
description: Bir müşteriye göndermek için bir ilişki isteği URL 'SI alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 5f899734b774ff460e005e20df8658275b2ce9d5
ms.sourcegitcommit: d4e652e3b73c6137704d43d4a472cc5aa5549f11
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/09/2020
ms.locfileid: "97770274"
---
# <a name="retrieve-a-relationship-request-url"></a><span data-ttu-id="6eed6-103">İlişki isteği URL’sini alma</span><span class="sxs-lookup"><span data-stu-id="6eed6-103">Retrieve a relationship request URL</span></span>

<span data-ttu-id="6eed6-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="6eed6-104">**Applies To**</span></span>

- <span data-ttu-id="6eed6-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6eed6-105">Partner Center</span></span>
- <span data-ttu-id="6eed6-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6eed6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="6eed6-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="6eed6-107">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="6eed6-108">Bir müşteriye göndermek için bir ilişki isteği URL 'SI alma.</span><span class="sxs-lookup"><span data-stu-id="6eed6-108">How to retrieve a relationship request URL to send to a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6eed6-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6eed6-109">Prerequisites</span></span>

- <span data-ttu-id="6eed6-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="6eed6-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6eed6-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="6eed6-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="6eed6-112">C\#</span><span class="sxs-lookup"><span data-stu-id="6eed6-112">C\#</span></span>

<span data-ttu-id="6eed6-113">İlişki isteği URL 'sini almak için, önce iş ortağının müşteri işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ' ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eed6-113">To retrieve a relationship request URL, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="6eed6-114">Ardından, bir Kullanıcı ilişki isteği işlemlerine bir arabirim almak için [**Relationshiprequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) özelliğini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eed6-114">Next, use the [**RelationshipRequest**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.relationshiprequest) property to get an interface to customer relationship request operations.</span></span> <span data-ttu-id="6eed6-115">Son olarak, URL 'YI almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="6eed6-115">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.relationshiprequests.icustomerrelationshiprequest.getasync) method to retrieve the URL.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var customerRelationshipRequest = partnerOperations.Customers.RelationshipRequest.Get();
```

<span data-ttu-id="6eed6-116">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6eed6-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6eed6-117">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetCustomerRelationshipRequest.cs</span><span class="sxs-lookup"><span data-stu-id="6eed6-117">**Project**: Partner Center SDK Samples **Class**: GetCustomerRelationshipRequest.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6eed6-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6eed6-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6eed6-119">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="6eed6-119">Request syntax</span></span>

| <span data-ttu-id="6eed6-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6eed6-120">Method</span></span>  | <span data-ttu-id="6eed6-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6eed6-121">Request URI</span></span>                                                                            |
|---------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="6eed6-122">**Al**</span><span class="sxs-lookup"><span data-stu-id="6eed6-122">**GET**</span></span> | <span data-ttu-id="6eed6-123">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/relationshiprequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="6eed6-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/relationshiprequests HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6eed6-124">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6eed6-124">Request headers</span></span>

<span data-ttu-id="6eed6-125">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="6eed6-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6eed6-126">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6eed6-126">Request body</span></span>

<span data-ttu-id="6eed6-127">Yok</span><span class="sxs-lookup"><span data-stu-id="6eed6-127">None</span></span>

### <a name="request-example"></a><span data-ttu-id="6eed6-128">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6eed6-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/relationshiprequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="6eed6-129">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6eed6-129">REST response</span></span>

<span data-ttu-id="6eed6-130">Başarılı olursa, yanıt [Relationshiprequest](relationships-resources.md#relationshiprequest) nesnesini içerir.</span><span class="sxs-lookup"><span data-stu-id="6eed6-130">If successful, the response contains the [RelationshipRequest](relationships-resources.md#relationshiprequest) object.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6eed6-131">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6eed6-131">Response success and error codes</span></span>

<span data-ttu-id="6eed6-132">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="6eed6-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6eed6-133">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6eed6-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6eed6-134">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="6eed6-134">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6eed6-135">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6eed6-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 196
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 02971f0f-1029-47b2-9fdb-1932f0987470
MS-RequestId: ee519026-4c67-4113-bec7-a38aca621bf0
MS-CV: jbYZRWjU3E262f8o.0
MS-ServerId: 030020643
Date: Fri, 19 May 2017 22:32:07 GMT

{
    "url": "https://admin.microsoft.com/Adminportal/Home?invType=ResellerRelationship&partnerId=3b33e682-00c3-41ee-9dd2-a548adf56438&msppId=0&DAP=false#/BillingAccounts/partner-invitation",
    "attributes": {
        "objectType": "RelationshipRequest"
    }
}
```
