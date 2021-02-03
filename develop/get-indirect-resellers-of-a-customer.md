---
title: Müşterinin dolaylı satıcılarını alma
description: Belirtilen müşteriyle ilişkisi olan dolaylı satıcıların listesini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d69abf9530548f110820ca04fefb698e0e37556c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769689"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="93f2e-103">Müşterinin dolaylı satıcılarını alma</span><span class="sxs-lookup"><span data-stu-id="93f2e-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="93f2e-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="93f2e-104">**Applies To**</span></span>

- <span data-ttu-id="93f2e-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="93f2e-105">Partner Center</span></span>

<span data-ttu-id="93f2e-106">Belirtilen müşteriyle ilişkisi olan dolaylı satıcıların listesini alma.</span><span class="sxs-lookup"><span data-stu-id="93f2e-106">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="93f2e-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="93f2e-107">Prerequisites</span></span>

- <span data-ttu-id="93f2e-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="93f2e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="93f2e-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="93f2e-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="93f2e-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="93f2e-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="93f2e-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="93f2e-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="93f2e-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="93f2e-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="93f2e-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="93f2e-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="93f2e-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="93f2e-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="93f2e-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="93f2e-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="93f2e-116">C\#</span><span class="sxs-lookup"><span data-stu-id="93f2e-116">C\#</span></span>

<span data-ttu-id="93f2e-117">Belirtilen müşterinin bir ilişkisi olan dolaylı satıcıların listesini almak için önce müşteriyi tanımlamak üzere müşteri KIMLIĞINI sağlayarak [**partneroperations. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) özelliğinden belirli müşteri için müşteri koleksiyonu işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="93f2e-117">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="93f2e-118">Daha sonra [**ilişkileri çağırın.**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) dolaylı satıcıların listesini almak için [**\_ zaman uyumsuz**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) yöntemi alın veya alın.</span><span class="sxs-lookup"><span data-stu-id="93f2e-118">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="93f2e-119">**Örnek**: [konsol test uygulaması](console-test-app.md)**PROJESI**: iş ortağı Merkezi SDK örnekleri **sınıfı**: GetIndirectResellersOfCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="93f2e-119">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="93f2e-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="93f2e-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="93f2e-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="93f2e-121">Request syntax</span></span>

| <span data-ttu-id="93f2e-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="93f2e-122">Method</span></span>  | <span data-ttu-id="93f2e-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="93f2e-123">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="93f2e-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="93f2e-124">**GET**</span></span> | <span data-ttu-id="93f2e-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Relationships http/1.1</span><span class="sxs-lookup"><span data-stu-id="93f2e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="93f2e-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="93f2e-126">URI parameter</span></span>

<span data-ttu-id="93f2e-127">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="93f2e-127">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="93f2e-128">Ad</span><span class="sxs-lookup"><span data-stu-id="93f2e-128">Name</span></span>        | <span data-ttu-id="93f2e-129">Tür</span><span class="sxs-lookup"><span data-stu-id="93f2e-129">Type</span></span>   | <span data-ttu-id="93f2e-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="93f2e-130">Required</span></span> | <span data-ttu-id="93f2e-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="93f2e-131">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="93f2e-132">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="93f2e-132">customer-id</span></span> | <span data-ttu-id="93f2e-133">string</span><span class="sxs-lookup"><span data-stu-id="93f2e-133">string</span></span> | <span data-ttu-id="93f2e-134">Yes</span><span class="sxs-lookup"><span data-stu-id="93f2e-134">Yes</span></span>      | <span data-ttu-id="93f2e-135">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="93f2e-135">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="93f2e-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="93f2e-136">Request headers</span></span>

<span data-ttu-id="93f2e-137">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="93f2e-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="93f2e-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="93f2e-138">Request body</span></span>

<span data-ttu-id="93f2e-139">Yok.</span><span class="sxs-lookup"><span data-stu-id="93f2e-139">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="93f2e-140">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="93f2e-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="93f2e-141">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="93f2e-141">REST response</span></span>

<span data-ttu-id="93f2e-142">Başarılı olursa, yanıt gövdesi satıcıları tanımlamak için bir [Iş ortağı ilişki](relationships-resources.md) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="93f2e-142">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="93f2e-143">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="93f2e-143">Response success and error codes</span></span>

<span data-ttu-id="93f2e-144">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="93f2e-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="93f2e-145">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="93f2e-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="93f2e-146">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="93f2e-146">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="93f2e-147">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="93f2e-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 264
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CV: plJP3ufU0UqXMeuh.0
MS-ServerId: 020021921
Date: Fri, 07 Apr 2017 23:42:11 GMT

{
    "totalCount": 1,
    "items": [{
            "id": "484e548c-f5f3-4528-93a9-c16c6373cb59",
            "name": "First Up Consultants",
            "relationshipType": "is_indirect_cloud_solution_provider_of",
            "mpnId": "4847383",
            "attributes": {
                "objectType": "PartnerRelationship"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
