---
title: Destek profili güncelleştirme
description: Kullanıcının destek profilini güncelleştirir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 605c509eeb18f301144fec6287c9611d5a5acfe2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769593"
---
# <a name="update-support-profile"></a><span data-ttu-id="9eec9-103">Destek profili güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9eec9-103">Update support profile</span></span>

<span data-ttu-id="9eec9-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="9eec9-104">**Applies To**</span></span>

- <span data-ttu-id="9eec9-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9eec9-105">Partner Center</span></span>
- <span data-ttu-id="9eec9-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9eec9-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="9eec9-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9eec9-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9eec9-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9eec9-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9eec9-109">Kullanıcının destek profilini güncelleştirir.</span><span class="sxs-lookup"><span data-stu-id="9eec9-109">Updates a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9eec9-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9eec9-110">Prerequisites</span></span>

- <span data-ttu-id="9eec9-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9eec9-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9eec9-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9eec9-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="9eec9-113">C\#</span><span class="sxs-lookup"><span data-stu-id="9eec9-113">C\#</span></span>

<span data-ttu-id="9eec9-114">Destek profilinizi güncelleştirmek için öncelikle [destek profilinizi alın](get-support-profile.md) ve istediğiniz değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="9eec9-114">To update your support profile, first [get your support profile](get-support-profile.md) and make any changes you wish.</span></span> <span data-ttu-id="9eec9-115">Ardından, [**ıpartneroperations. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9eec9-115">Then, use your [**IPartnerOperations.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) collection.</span></span> <span data-ttu-id="9eec9-116">[**Supportprofile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) özelliğini çağırın, ardından [**Update ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) veya [**UpdateAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9eec9-116">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Update()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.update) or [**UpdateAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.updateasync) method.</span></span>

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

<span data-ttu-id="9eec9-117">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9eec9-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9eec9-118">**Proje**: partnercentersdk. FeaturesSamples **sınıfı**: UpdateSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="9eec9-118">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: UpdateSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9eec9-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9eec9-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9eec9-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9eec9-120">Request syntax</span></span>

| <span data-ttu-id="9eec9-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9eec9-121">Method</span></span>  | <span data-ttu-id="9eec9-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9eec9-122">Request URI</span></span>                                                                     |
|---------|---------------------------------------------------------------------------------|
| <span data-ttu-id="9eec9-123">**PUT**</span><span class="sxs-lookup"><span data-stu-id="9eec9-123">**PUT**</span></span> | <span data-ttu-id="9eec9-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/supportprofile http/1.1</span><span class="sxs-lookup"><span data-stu-id="9eec9-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/supportprofile HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9eec9-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9eec9-125">Request headers</span></span>

<span data-ttu-id="9eec9-126">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9eec9-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9eec9-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9eec9-127">Request body</span></span>

<span data-ttu-id="9eec9-128">Tam destek profili kaynağı.</span><span class="sxs-lookup"><span data-stu-id="9eec9-128">The full support profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="9eec9-129">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9eec9-129">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9eec9-130">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9eec9-130">REST response</span></span>

<span data-ttu-id="9eec9-131">Başarılı olursa, bu yöntem yanıt gövdesinde güncelleştirilmiş **supportprofile** nesne özellikleri döndürür.</span><span class="sxs-lookup"><span data-stu-id="9eec9-131">If successful, this method returns updated **SupportProfile** object properties in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9eec9-132">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9eec9-132">Response success and error codes</span></span>

<span data-ttu-id="9eec9-133">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9eec9-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9eec9-134">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9eec9-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9eec9-135">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9eec9-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9eec9-136">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9eec9-136">Response example</span></span>

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
