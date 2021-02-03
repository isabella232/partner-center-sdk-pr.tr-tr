---
title: Kuruluş profili alma
description: Ortağın kuruluş profilini temsil eden bir nesne alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 132a1e0efa3efea69d4bf649e55b412e300b0685
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769868"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="c2ea6-103">Kuruluş profili alma</span><span class="sxs-lookup"><span data-stu-id="c2ea6-103">Get an organization profile</span></span>

<span data-ttu-id="c2ea6-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="c2ea6-104">**Applies To**</span></span>

- <span data-ttu-id="c2ea6-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-105">Partner Center</span></span>
- <span data-ttu-id="c2ea6-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="c2ea6-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="c2ea6-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="c2ea6-109">Ortağın kuruluş profilini temsil eden bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-109">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c2ea6-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c2ea6-110">Prerequisites</span></span>

- <span data-ttu-id="c2ea6-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c2ea6-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="c2ea6-113">C\#</span><span class="sxs-lookup"><span data-stu-id="c2ea6-113">C\#</span></span>

<span data-ttu-id="c2ea6-114">Kuruluş profilinizi almak için **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın ve **OrganizationProfile** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-114">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="c2ea6-115">Son olarak [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-115">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="c2ea6-116">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-116">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="c2ea6-117">**Proje**: partnercentersdk. FeaturesSamples **sınıfı**: GetOrganizationProfile.cs</span><span class="sxs-lookup"><span data-stu-id="c2ea6-117">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="c2ea6-118">Java</span><span class="sxs-lookup"><span data-stu-id="c2ea6-118">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="c2ea6-119">Kuruluş profilinizi almak için **ıaggregatepartner. getProfiles** işlevinizi kullanın ve **Getorganizationprofile** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-119">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="c2ea6-120">Son olarak **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-120">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="c2ea6-121">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c2ea6-121">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="c2ea6-122">Kuruluş profilinizi almak için [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-122">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="c2ea6-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c2ea6-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c2ea6-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-124">Request syntax</span></span>

| <span data-ttu-id="c2ea6-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c2ea6-125">Method</span></span>  | <span data-ttu-id="c2ea6-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c2ea6-126">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="c2ea6-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="c2ea6-127">**GET**</span></span> | <span data-ttu-id="c2ea6-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/kuruluş http/1.1</span><span class="sxs-lookup"><span data-stu-id="c2ea6-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c2ea6-129">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c2ea6-129">Request headers</span></span>

<span data-ttu-id="c2ea6-130">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c2ea6-131">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c2ea6-131">Request body</span></span>

<span data-ttu-id="c2ea6-132">Yok.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-132">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="c2ea6-133">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c2ea6-133">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="c2ea6-134">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c2ea6-134">REST response</span></span>

<span data-ttu-id="c2ea6-135">Başarılı olursa, bu yöntem yanıt gövdesinde bir **OrganizationProfile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-135">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c2ea6-136">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c2ea6-136">Response success and error codes</span></span>

<span data-ttu-id="c2ea6-137">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c2ea6-138">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c2ea6-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c2ea6-139">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c2ea6-139">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c2ea6-140">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c2ea6-140">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
Date: Tue, 22 Mar 2016 17:11:06 GMT

{
    "id":<id>,
    "companyName":"TEST_TEST_BugBash1",
    "defaultAddress":{
        "country":"US",
        "city":"Redmond",
        "state":"WA",
        "addressLine1":"Two Microsoft Way",
        "addressLine2":"",
        "postalCode":"98052",
        "firstName":"Test",
        "lastName":"Account",
        "phoneNumber":""
    },
    "tenantId":<tenantID>,
    "domain":"testtestbugbash1.onmicrosoft.com",
    "email":"test-partner@microsoft.com",
    "language":"es",
    "culture":"es-US",
    "profileType":"OrganizationProfile",
    "links":{
        "self":{
            "uri":"/profiles/organization",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "etag":<etag>,
        "objectType":"OrganizationProfile"
    }
}
```
