---
title: İş ortağı faturalandırma profili alma
description: İş ortağının faturalama profilini temsil eden bir nesnesi alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 225d8ea2d92933838ae47eaf3308276aa1f1684c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548983"
---
# <a name="get-partner-billing-profile"></a><span data-ttu-id="6bd20-103">İş ortağı faturalandırma profili alma</span><span class="sxs-lookup"><span data-stu-id="6bd20-103">Get partner billing profile</span></span>

<span data-ttu-id="6bd20-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="6bd20-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="6bd20-105">İş ortağının faturalama profilini temsil eden bir nesnesi alır.</span><span class="sxs-lookup"><span data-stu-id="6bd20-105">Gets an object representing the partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6bd20-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="6bd20-106">Prerequisites</span></span>

- <span data-ttu-id="6bd20-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="6bd20-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="6bd20-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="6bd20-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="6bd20-109">C\#</span><span class="sxs-lookup"><span data-stu-id="6bd20-109">C\#</span></span>

<span data-ttu-id="6bd20-110">bir iş ortağı faturalama profili almak için **IAggregatePartner.Profiles** koleksiyonu kullanın ve **BillingProfile özelliğini** arayın.</span><span class="sxs-lookup"><span data-stu-id="6bd20-110">To get a partner billing profile, use your **IAggregatePartner.Profiles** collection and call the **BillingProfile** property.</span></span> <span data-ttu-id="6bd20-111">Son olarak [**Get() veya**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) [**GetAsync() yöntemlerini**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) arayın.</span><span class="sxs-lookup"><span data-stu-id="6bd20-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.ibillingprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

BillingProfile billingProfile = partnerOperations.Profiles.BillingProfile.Get();
```

<span data-ttu-id="6bd20-112">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="6bd20-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="6bd20-113">**Project:** PartnerCenterSDK.FeaturesSamples **Sınıfı:** GetBillingProfile.cs</span><span class="sxs-lookup"><span data-stu-id="6bd20-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetBillingProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="6bd20-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="6bd20-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="6bd20-115">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="6bd20-115">Request syntax</span></span>

| <span data-ttu-id="6bd20-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="6bd20-116">Method</span></span>  | <span data-ttu-id="6bd20-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="6bd20-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="6bd20-118">**Al**</span><span class="sxs-lookup"><span data-stu-id="6bd20-118">**GET**</span></span> | <span data-ttu-id="6bd20-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="6bd20-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/billing HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="6bd20-120">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="6bd20-120">Request headers</span></span>

<span data-ttu-id="6bd20-121">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="6bd20-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="6bd20-122">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="6bd20-122">Request body</span></span>

<span data-ttu-id="6bd20-123">Yok.</span><span class="sxs-lookup"><span data-stu-id="6bd20-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="6bd20-124">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="6bd20-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/billing HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a0dd6cde-b24c-413c-af24-416446dc5599
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="6bd20-125">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="6bd20-125">REST response</span></span>

<span data-ttu-id="6bd20-126">Başarılı olursa, bu yöntem yanıt **gövdesinde bir BillingProfile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="6bd20-126">If successful, this method returns a **BillingProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="6bd20-127">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="6bd20-127">Response success and error codes</span></span>

<span data-ttu-id="6bd20-128">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="6bd20-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="6bd20-129">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="6bd20-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="6bd20-130">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="6bd20-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="6bd20-131">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="6bd20-131">Response example</span></span>

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
