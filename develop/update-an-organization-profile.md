---
title: Kuruluş profili güncelleştirme
description: Bir kuruluşun faturalandırma profilini güncelleştirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 0ef736a722cde16f95ed6dfdbdab278c98fcf738
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530064"
---
# <a name="update-an-organization-profile"></a><span data-ttu-id="bdeee-103">Kuruluş profili güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="bdeee-103">Update an organization profile</span></span>

<span data-ttu-id="bdeee-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="bdeee-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="bdeee-105">Bir ortağın faturalandırma profilini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="bdeee-105">Updates a partner's billing profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bdeee-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="bdeee-106">Prerequisites</span></span>

- <span data-ttu-id="bdeee-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="bdeee-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="bdeee-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="bdeee-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="bdeee-109">C\#</span><span class="sxs-lookup"><span data-stu-id="bdeee-109">C\#</span></span>

<span data-ttu-id="bdeee-110">Kuruluş profilinizi güncelleştirmek için, profili alın ve gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="bdeee-110">To update your organization profile, retrieve the profile and make any necessary changes.</span></span> <span data-ttu-id="bdeee-111">Ardından, **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın ve **OrganizationProfile** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="bdeee-111">Then, use your **IAggregatePartner.Profiles** collection and call the **OrganizationProfile** property.</span></span> <span data-ttu-id="bdeee-112">Son olarak **Update ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="bdeee-112">Finally, call the **Update()** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

OrganizationProfile organizationProfile = partnerOperations.Profiles.OrganizationProfile.Get();

// Generating a random phone number to update in the organization profile
organizationProfile.DefaultAddress.PhoneNumber = ((long)(new Random().NextDouble() * 9000000000) + 1000000000).ToString(CultureInfo.InvariantCulture);

OrganizationProfile updatedOrganizationProfile = partnerOperations.Profiles.OrganizationProfile.Update(organizationProfile);
```

<span data-ttu-id="bdeee-113">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="bdeee-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="bdeee-114">**Project**: partnercentersdk. featuressamples **sınıfı**: updateorganizationprofile. cs</span><span class="sxs-lookup"><span data-stu-id="bdeee-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateOrganizationProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="bdeee-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="bdeee-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="bdeee-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="bdeee-116">Request syntax</span></span>

| <span data-ttu-id="bdeee-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="bdeee-117">Method</span></span>  | <span data-ttu-id="bdeee-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="bdeee-118">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="bdeee-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="bdeee-119">**PUT**</span></span> | <span data-ttu-id="bdeee-120">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/kuruluş http/1.1</span><span class="sxs-lookup"><span data-stu-id="bdeee-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/organization HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="bdeee-121">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="bdeee-121">Request headers</span></span>

<span data-ttu-id="bdeee-122">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="bdeee-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="bdeee-123">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="bdeee-123">Request body</span></span>

<span data-ttu-id="bdeee-124">Yok.</span><span class="sxs-lookup"><span data-stu-id="bdeee-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="bdeee-125">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="bdeee-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/organization HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Content-Length: 624
Expect: 100-continue

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

## <a name="rest-response"></a><span data-ttu-id="bdeee-126">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="bdeee-126">REST response</span></span>

<span data-ttu-id="bdeee-127">Başarılı olursa, bu yöntem yanıt gövdesinde bir **OrganizationProfile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="bdeee-127">If successful, this method returns an **OrganizationProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="bdeee-128">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="bdeee-128">Response success and error codes</span></span>

<span data-ttu-id="bdeee-129">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="bdeee-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="bdeee-130">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="bdeee-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="bdeee-131">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="bdeee-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="bdeee-132">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="bdeee-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 648
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: fe76387b-9658-47d7-939d-0c70032ef589
Date: Mon, 21 Mar 2016 05:48:41 GMT

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
