---
title: İş ortağı faturalandırma profili güncelleştirme
description: Bir ortağın faturalandırma profilini güncelleştirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 34e7d2396d6dbdd45a6cf87a3bda481f51326f1e
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769191"
---
# <a name="update-the-partner-billing-profile"></a><span data-ttu-id="2ee0c-103">İş ortağı faturalandırma profili güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="2ee0c-103">Update the partner billing profile</span></span>

<span data-ttu-id="2ee0c-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="2ee0c-104">**Applies To**</span></span>

- <span data-ttu-id="2ee0c-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2ee0c-105">Partner Center</span></span>
- <span data-ttu-id="2ee0c-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2ee0c-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2ee0c-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2ee0c-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2ee0c-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2ee0c-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2ee0c-109">Bir ortağın faturalandırma profilini güncelleştirir</span><span class="sxs-lookup"><span data-stu-id="2ee0c-109">Updates a partner's billing profile</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2ee0c-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2ee0c-110">Prerequisites</span></span>

- <span data-ttu-id="2ee0c-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2ee0c-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="2ee0c-113">C\#</span><span class="sxs-lookup"><span data-stu-id="2ee0c-113">C\#</span></span>

<span data-ttu-id="2ee0c-114">Bir iş ortağı faturalandırma profilini güncelleştirmek için mevcut profili alın.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-114">To update a partner billing profile, retrieve the existing profile.</span></span> <span data-ttu-id="2ee0c-115">Profili güncelleştirdikten sonra **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın ve **billingprofile** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-115">Once you have updated the profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="2ee0c-116">Son olarak **Update ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-116">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile existingBillingProfile = partnerOperations.Profiles.BillingProfile.Get();

// update the profile with a purchase order number
existingBillingProfile.PurchaseOrderNumber = new Random().Next(9000, 10000).ToString(CultureInfo.InvariantCulture);

BillingProfile updatedPartnerBillingProfile = partnerOperations.Profiles.BillingProfile.Update(existingBillingProfile);
```

<span data-ttu-id="2ee0c-117">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2ee0c-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2ee0c-118">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: UpdateBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="2ee0c-118">**Project**: Partner Center SDK Samples **Class**: UpdateBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2ee0c-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2ee0c-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2ee0c-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2ee0c-120">Request syntax</span></span>

| <span data-ttu-id="2ee0c-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2ee0c-121">Method</span></span>  | <span data-ttu-id="2ee0c-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2ee0c-122">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="2ee0c-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="2ee0c-123">**PUT**</span></span> | <span data-ttu-id="2ee0c-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/faturalandırma http/1.1</span><span class="sxs-lookup"><span data-stu-id="2ee0c-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2ee0c-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2ee0c-125">Request headers</span></span>

<span data-ttu-id="2ee0c-126">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2ee0c-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2ee0c-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2ee0c-127">Request body</span></span>

<span data-ttu-id="2ee0c-128">Yok.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="2ee0c-129">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2ee0c-129">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 613
Expect: 100-continue

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="2ee0c-130">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2ee0c-130">REST response</span></span>

<span data-ttu-id="2ee0c-131">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Billingprofile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-131">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2ee0c-132">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2ee0c-132">Response success and error codes</span></span>

<span data-ttu-id="2ee0c-133">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2ee0c-134">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2ee0c-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2ee0c-135">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2ee0c-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2ee0c-136">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2ee0c-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 9231559e-ed95-41e4-810b-e754ae32dc2f
Date: Mon, 21 Mar 2016 05:47:16 GMT

{
    "CompanyName":"TEST_TEST_BugBash1",
    "Address":{
        "Country":"US",
        "Region":null,
        "City":"Redmond",
        "State":"WA",
        "AddressLine1":"1 Microsoft Way",
        "AddressLine2":"","PostalCode":"98052",
        "FirstName":null,
        "LastName":null,
        "PhoneNumber":null
    },
    "PrimaryContact":{
        "FirstName":"Test",
        "LastName":"Customer",
        "Email":null,
        "PhoneNumber":""
    },
    "PurchaseOrderNumber":"9888",
    "TaxId":<TaxId>,
    "BillingCurrency":"USD",
    "Links":{
        "Self":{
            "Uri":"/profiles/billing",
            "Method":"GET","Headers":[]
        }
    },
    "Attributes":{
        "Etag":<etag>,
        "ObjectType":"BillingProfile"
    }
}
```
