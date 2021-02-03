---
title: Destek profili alma
description: Kullanıcının destek profilini temsil eden bir nesne alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b8b0fa533aaba74418985ea02cbb13bd722cede2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769808"
---
# <a name="get-support-profile"></a><span data-ttu-id="9e768-103">Destek profili alma</span><span class="sxs-lookup"><span data-stu-id="9e768-103">Get support profile</span></span>

<span data-ttu-id="9e768-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="9e768-104">**Applies To**</span></span>

- <span data-ttu-id="9e768-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9e768-105">Partner Center</span></span>
- <span data-ttu-id="9e768-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9e768-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="9e768-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9e768-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="9e768-108">Kullanıcının destek profilini temsil eden bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="9e768-108">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9e768-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9e768-109">Prerequisites</span></span>

- <span data-ttu-id="9e768-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9e768-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9e768-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9e768-111">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="9e768-112">C\#</span><span class="sxs-lookup"><span data-stu-id="9e768-112">C\#</span></span>

<span data-ttu-id="9e768-113">Destek profilinizi almak için **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e768-113">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="9e768-114">[**Supportprofile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) özelliğini çağırın, ardından [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) yöntemleri gelir.</span><span class="sxs-lookup"><span data-stu-id="9e768-114">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="9e768-115">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9e768-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9e768-116">**Proje**: partnercentersdk. FeaturesSamples **sınıfı**: GetSupportProfile.cs</span><span class="sxs-lookup"><span data-stu-id="9e768-116">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9e768-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9e768-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9e768-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9e768-118">Request syntax</span></span>

| <span data-ttu-id="9e768-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9e768-119">Method</span></span>  | <span data-ttu-id="9e768-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9e768-120">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="9e768-121">**Al**</span><span class="sxs-lookup"><span data-stu-id="9e768-121">**GET**</span></span> | <span data-ttu-id="9e768-122">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/support http/1.1</span><span class="sxs-lookup"><span data-stu-id="9e768-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9e768-123">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9e768-123">Request headers</span></span>

<span data-ttu-id="9e768-124">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9e768-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9e768-125">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9e768-125">Request body</span></span>

<span data-ttu-id="9e768-126">Yok.</span><span class="sxs-lookup"><span data-stu-id="9e768-126">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9e768-127">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9e768-127">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="9e768-128">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9e768-128">REST response</span></span>

<span data-ttu-id="9e768-129">Başarılı olursa, bu yöntem yanıt gövdesinde bir **supportprofile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="9e768-129">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9e768-130">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9e768-130">Response success and error codes</span></span>

<span data-ttu-id="9e768-131">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9e768-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9e768-132">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9e768-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9e768-133">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9e768-133">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9e768-134">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9e768-134">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 502
Content-Type: application/json
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
Date: Wed, 25 Nov 2015 07:16:17 GMT

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
