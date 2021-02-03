---
title: İş ortağı faturalandırma profili alma
description: Ortağın faturalandırma profilini temsil eden bir nesne alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 94c5ff8fc351282ca3b4721511f02ba6a0cc403c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769839"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="98385-103">İş ortağı faturalandırma profili alma</span><span class="sxs-lookup"><span data-stu-id="98385-103">Get partner billing profile</span></span>

<span data-ttu-id="98385-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="98385-104">**Applies To**</span></span>

- <span data-ttu-id="98385-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98385-105">Partner Center</span></span>
- <span data-ttu-id="98385-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98385-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="98385-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98385-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="98385-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="98385-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="98385-109">Ortağın faturalandırma profilini temsil eden bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="98385-109">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="98385-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="98385-110">Prerequisites</span></span>

- <span data-ttu-id="98385-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="98385-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="98385-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="98385-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="98385-113">C\#</span><span class="sxs-lookup"><span data-stu-id="98385-113">C\#</span></span>

<span data-ttu-id="98385-114">Bir iş ortağı Faturalandırma profili almak için **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın ve **billingprofile** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="98385-114">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="98385-115">Son olarak [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="98385-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="98385-116">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="98385-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="98385-117">**Proje**: partnercentersdk. FeaturesSamples **sınıfı**: GetBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="98385-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="98385-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="98385-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="98385-119">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="98385-119">Request syntax</span></span>

| <span data-ttu-id="98385-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="98385-120">Method</span></span>  | <span data-ttu-id="98385-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="98385-121">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="98385-122">**Al**</span><span class="sxs-lookup"><span data-stu-id="98385-122">**GET**</span></span> | <span data-ttu-id="98385-123">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/faturalandırma http/1.1</span><span class="sxs-lookup"><span data-stu-id="98385-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="98385-124">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="98385-124">Request headers</span></span>

<span data-ttu-id="98385-125">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="98385-125">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="98385-126">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="98385-126">Request body</span></span>

<span data-ttu-id="98385-127">Yok.</span><span class="sxs-lookup"><span data-stu-id="98385-127">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="98385-128">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="98385-128">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="98385-129">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="98385-129">REST response</span></span>

<span data-ttu-id="98385-130">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Billingprofile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="98385-130">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="98385-131">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="98385-131">Response success and error codes</span></span>

<span data-ttu-id="98385-132">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="98385-132">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="98385-133">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="98385-133">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="98385-134">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="98385-134">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="98385-135">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="98385-135">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 568
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
Date: Tue, 22 Mar 2016 17:10:02 GMT

{
    "companyName":"TEST_TEST_BugBash1",
    "address":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"1 Microsoft Way",
        "addressLine2":"","postalCode":"98052"
    },
    "primaryContact":{
        "firstName":"James",
        "lastName":"Burk",
        "phoneNumber":"2066017143"
    },
    "purchaseOrderNumber":"9888",
    "taxId":"12-345678",
    "billingCurrency":"USD",
    "profileType":"BillingProfile",
    "links":{
        "self":{
            "uri":"/profiles/billing",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"BillingProfile"
    }
}
```
