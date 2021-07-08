---
title: Kuruluş profili alma
description: Ortağın kuruluş profilini temsil eden bir nesne alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 1c7272761612e573388d4facea1a78808a5bad52
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760564"
---
# <a name="get-an-organization-profile"></a><span data-ttu-id="90c2f-103">Kuruluş profili alma</span><span class="sxs-lookup"><span data-stu-id="90c2f-103">Get an organization profile</span></span>

<span data-ttu-id="90c2f-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="90c2f-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="90c2f-105">Ortağın kuruluş profilini temsil eden bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="90c2f-105">Gets an object representing the partner's organization profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="90c2f-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="90c2f-106">Prerequisites</span></span>

- <span data-ttu-id="90c2f-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="90c2f-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="90c2f-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="90c2f-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="90c2f-109">C\#</span><span class="sxs-lookup"><span data-stu-id="90c2f-109">C\#</span></span>

<span data-ttu-id="90c2f-110">Kuruluş profilinizi almak için **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın ve **OrganizationProfile** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="90c2f-110">To get your organization profile, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="90c2f-111">Son olarak [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="90c2f-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.iorganizationprofile.getasync) methods.</span></span>

```csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();
```

<span data-ttu-id="90c2f-112">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="90c2f-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="90c2f-113">**Project**: partnercentersdk. featuressamples **sınıfı**: getorganizationprofile. cs</span><span class="sxs-lookup"><span data-stu-id="90c2f-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetOrganizationProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="90c2f-114">Java</span><span class="sxs-lookup"><span data-stu-id="90c2f-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="90c2f-115">Kuruluş profilinizi almak için **ıaggregatepartner. getProfiles** işlevinizi kullanın ve **Getorganizationprofile** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="90c2f-115">To get your organization profile, use your **IAggregatePartner.getProfiles** function and call the **getOrganizationProfile** function.</span></span> <span data-ttu-id="90c2f-116">Son olarak **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="90c2f-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.getProfiles().getOrganizationProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="90c2f-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="90c2f-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="90c2f-118">Kuruluş profilinizi almak için [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="90c2f-118">To get your organization profile, execute the [**Get-PartnerOrganizationProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerOrganizationProfile.md) command.</span></span>

```powershell
Get-PartnerOrganizationProfile
```

## <a name="rest-request"></a><span data-ttu-id="90c2f-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="90c2f-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="90c2f-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="90c2f-120">Request syntax</span></span>

| <span data-ttu-id="90c2f-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="90c2f-121">Method</span></span>  | <span data-ttu-id="90c2f-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="90c2f-122">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="90c2f-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="90c2f-123">**GET**</span></span> | <span data-ttu-id="90c2f-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/kuruluş http/1.1</span><span class="sxs-lookup"><span data-stu-id="90c2f-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="90c2f-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="90c2f-125">Request headers</span></span>

<span data-ttu-id="90c2f-126">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="90c2f-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="90c2f-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="90c2f-127">Request body</span></span>

<span data-ttu-id="90c2f-128">Yok.</span><span class="sxs-lookup"><span data-stu-id="90c2f-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="90c2f-129">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="90c2f-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b85cb7ab-cc2e-4966-93f0-cf0d8377a93f
MS-CorrelationId: 1bb03149-88d2-4bc2-9cc1-d6e83890fa9e
```

## <a name="rest-response"></a><span data-ttu-id="90c2f-130">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="90c2f-130">REST response</span></span>

<span data-ttu-id="90c2f-131">Başarılı olursa, bu yöntem yanıt gövdesinde bir **OrganizationProfile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="90c2f-131">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="90c2f-132">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="90c2f-132">Response success and error codes</span></span>

<span data-ttu-id="90c2f-133">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="90c2f-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="90c2f-134">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="90c2f-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="90c2f-135">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="90c2f-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="90c2f-136">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="90c2f-136">Response example</span></span>

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
