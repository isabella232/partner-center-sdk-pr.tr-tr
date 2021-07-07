---
title: Destek profili güncelleştirme
description: Bir kullanıcının destek profilini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 143328c5501f525d52911eead805d420f79b78ff
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530353"
---
# <a name="update-support-profile"></a><span data-ttu-id="746d4-103">Destek profili güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="746d4-103">Update support profile</span></span>

<span data-ttu-id="746d4-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="746d4-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="746d4-105">Bir kullanıcının destek profilini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="746d4-105">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="746d4-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="746d4-106">Prerequisites</span></span>

- <span data-ttu-id="746d4-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="746d4-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="746d4-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="746d4-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="746d4-109">C\#</span><span class="sxs-lookup"><span data-stu-id="746d4-109">C\#</span></span>

<span data-ttu-id="746d4-110">Destek profilinizi güncelleştirmek için önce [destek profilinizi oluşturun ve](get-support-profile.md) istediğiniz değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="746d4-110">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="746d4-111">Ardından [**IPartnerOperations.Profiles koleksiyonu kullanın.**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles)</span><span class="sxs-lookup"><span data-stu-id="746d4-111">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="746d4-112">[**SupportProfile özelliğini**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) ve ardından [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) veya [**UpdateAsync() yöntemini**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) arayın.</span><span class="sxs-lookup"><span data-stu-id="746d4-112">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// updated profile
SupportProfile newSupportProfile = new SupportProfile
{
   Email = supportProfile.Email,
   Website = supportProfile.Website,
   Telephone = new Random().Next(10000000, 99999999).ToString(CultureInfo.InvariantCulture)
};

SupportProfile updatedSupportProfile = partnerOperations.Profiles.SupportProfile.Update(newSupportProfile);
```

<span data-ttu-id="746d4-113">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="746d4-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="746d4-114">**Project:** PartnerCenterSDK.FeaturesSamples **Sınıfı:** UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="746d4-114">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="746d4-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="746d4-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="746d4-116">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="746d4-116">Request syntax</span></span>

| <span data-ttu-id="746d4-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="746d4-117">Method</span></span>  | <span data-ttu-id="746d4-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="746d4-118">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="746d4-119">**PUT**</span><span class="sxs-lookup"><span data-stu-id="746d4-119">**PUT**</span></span> | <span data-ttu-id="746d4-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="746d4-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="746d4-121">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="746d4-121">Request headers</span></span>

<span data-ttu-id="746d4-122">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="746d4-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="746d4-123">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="746d4-123">Request body</span></span>

<span data-ttu-id="746d4-124">Tam destek profili kaynağı.</span><span class="sxs-lookup"><span data-stu-id="746d4-124">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="746d4-125">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="746d4-125">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/supportprofile HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
Content-Type: application/json
Content-Length: 167
Expect: 100-continue

{
    "Email": "email@sample.com",
    "Telephone": "4255555555",
    "Website": "www.microsoft.com",
    "ProfileType": "support_profile",
    "Attributes": {
        "ObjectType": "PartnerSupportProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="746d4-126">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="746d4-126">REST response</span></span>

<span data-ttu-id="746d4-127">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş **SupportProfile** nesne özelliklerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="746d4-127">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="746d4-128">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="746d4-128">Response success and error codes</span></span>

<span data-ttu-id="746d4-129">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="746d4-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="746d4-130">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="746d4-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="746d4-131">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="746d4-131">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="746d4-132">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="746d4-132">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 603f3cd9-01b8-48f2-b65d-855a246f5bfd
Date: Wed, 25 Nov 2015 07:16:18 GMT

{
    "email": "email@sample.com",
    "telephone": "4255555555",
    "website": "www.microsoft.com",
    "profileType": "support_profile",
    "links": {
        "self": {
            "uri": "/v1/profiles/support",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "PartnerSupportProfile"
    }
}
```
