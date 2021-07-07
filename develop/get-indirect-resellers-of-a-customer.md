---
title: Müşterinin dolaylı satıcılarını alma
description: Belirtilen müşteriyle ilişkisi olan dolaylı kurumsal bayilerin listesini alma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 8697c40c22d5c19979c066b8d3a1de733e211f71
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446250"
---
# <a name="get-indirect-resellers-of-a-customer"></a><span data-ttu-id="6f866-103">Müşterinin dolaylı satıcılarını alma</span><span class="sxs-lookup"><span data-stu-id="6f866-103">Get indirect resellers of a customer</span></span>

<span data-ttu-id="6f866-104">Belirtilen müşteriyle ilişkisi olan dolaylı kurumsal bayilerin listesini alma.</span><span class="sxs-lookup"><span data-stu-id="6f866-104">How to get a list of the indirect resellers that have a relationship with a specified customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6f866-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6f866-105">Prerequisites</span></span>

- <span data-ttu-id="6f866-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6f866-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6f866-107">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="6f866-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="6f866-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="6f866-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="6f866-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="6f866-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="6f866-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="6f866-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="6f866-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="6f866-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="6f866-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="6f866-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="6f866-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="6f866-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="6f866-114">C\#</span><span class="sxs-lookup"><span data-stu-id="6f866-114">C\#</span></span>

<span data-ttu-id="6f866-115">Belirtilen müşterinin ilişkisi olan dolaylı kurumsal bayilerin listesini almak için önce [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) özelliğinden müşteri kimliğini sağlayarak müşteri koleksiyonu işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="6f866-115">To retrieve a list of indirect resellers with whom the specified customer has a relationship, first get an interface to customer collection operations for the specific customer from the [**partnerOperations.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.relationships) property by providing the customer ID to identify the customer.</span></span> <span data-ttu-id="6f866-116">Ardından dolaylı kurumsal bayilerin listesini almak için [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) veya [**Get \_ Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="6f866-116">Then call the [**Relationships.Get**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.get) or [**Get\_Async**](/dotnet/api/microsoft.store.partnercenter.relationships.icustomerrelationshipcollection.getasync) method to get the list of indirect resellers.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;

 var indirectResellers = partnerOperations.Customers[customerId].Relationships.Get();
```

<span data-ttu-id="6f866-117">**Örnek:** [Konsol test uygulaması](console-test-app.md)**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** GetIndirectResellersOfCustomer.cs</span><span class="sxs-lookup"><span data-stu-id="6f866-117">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetIndirectResellersOfCustomer.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6f866-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6f866-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6f866-119">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="6f866-119">Request syntax</span></span>

| <span data-ttu-id="6f866-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6f866-120">Method</span></span>  | <span data-ttu-id="6f866-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6f866-121">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="6f866-122">**Al**</span><span class="sxs-lookup"><span data-stu-id="6f866-122">**GET**</span></span> | <span data-ttu-id="6f866-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6f866-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/relationships HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="6f866-124">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="6f866-124">URI parameter</span></span>

<span data-ttu-id="6f866-125">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f866-125">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="6f866-126">Ad</span><span class="sxs-lookup"><span data-stu-id="6f866-126">Name</span></span>        | <span data-ttu-id="6f866-127">Tür</span><span class="sxs-lookup"><span data-stu-id="6f866-127">Type</span></span>   | <span data-ttu-id="6f866-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="6f866-128">Required</span></span> | <span data-ttu-id="6f866-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="6f866-129">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="6f866-130">customer-id</span><span class="sxs-lookup"><span data-stu-id="6f866-130">customer-id</span></span> | <span data-ttu-id="6f866-131">string</span><span class="sxs-lookup"><span data-stu-id="6f866-131">string</span></span> | <span data-ttu-id="6f866-132">Yes</span><span class="sxs-lookup"><span data-stu-id="6f866-132">Yes</span></span>      | <span data-ttu-id="6f866-133">Müşteriyi tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="6f866-133">A GUID formatted string that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6f866-134">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6f866-134">Request headers</span></span>

<span data-ttu-id="6f866-135">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6f866-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6f866-136">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6f866-136">Request body</span></span>

<span data-ttu-id="6f866-137">Yok.</span><span class="sxs-lookup"><span data-stu-id="6f866-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6f866-138">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6f866-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/c501c3c4-d776-40ef-9ecf-9cefb59442c1/relationships HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c9251710-5a30-4cd3-891a-c42d550af9a8
MS-CorrelationId: a96f326c-a392-44f4-bcfe-43152a756ba8
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="6f866-139">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6f866-139">REST response</span></span>

<span data-ttu-id="6f866-140">Başarılı olursa, yanıt gövdesi kurumsal bayileri tanımlamak için [bir PartnerRelationship](relationships-resources.md) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="6f866-140">If successful, the response body contains a collection of [PartnerRelationship](relationships-resources.md) resources to identify the resellers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6f866-141">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6f866-141">Response success and error codes</span></span>

<span data-ttu-id="6f866-142">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="6f866-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6f866-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6f866-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6f866-144">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6f866-144">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6f866-145">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6f866-145">Response example</span></span>

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
