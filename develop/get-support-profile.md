---
title: Destek profili alma
description: Kullanıcının destek profilini temsil eden bir nesne alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b112ccbbff731795c21f95845a08be9e9dfb6775
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548643"
---
# <a name="get-support-profile"></a><span data-ttu-id="8dd69-103">Destek profili alma</span><span class="sxs-lookup"><span data-stu-id="8dd69-103">Get support profile</span></span>

<span data-ttu-id="8dd69-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8dd69-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8dd69-105">Kullanıcının destek profilini temsil eden bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="8dd69-105">Gets an object representing a user's support profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8dd69-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8dd69-106">Prerequisites</span></span>

- <span data-ttu-id="8dd69-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8dd69-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8dd69-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="8dd69-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="8dd69-109">C\#</span><span class="sxs-lookup"><span data-stu-id="8dd69-109">C\#</span></span>

<span data-ttu-id="8dd69-110">Destek profilinizi almak için **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8dd69-110">To get your support profile, use your **IAggregatePartner.Profiles** collection.</span></span> <span data-ttu-id="8dd69-111">[**Supportprofile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) özelliğini çağırın, ardından [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) yöntemleri gelir.</span><span class="sxs-lookup"><span data-stu-id="8dd69-111">Call the [**SupportProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.isupportprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

SupportProfile supportProfile = partnerOperations.Profiles.SupportProfile.Get();
```

<span data-ttu-id="8dd69-112">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="8dd69-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="8dd69-113">**Project**: partnercentersdk. featuressamples **sınıfı**: getsupportprofile. cs</span><span class="sxs-lookup"><span data-stu-id="8dd69-113">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: GetSupportProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="8dd69-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8dd69-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8dd69-115">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8dd69-115">Request syntax</span></span>

| <span data-ttu-id="8dd69-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8dd69-116">Method</span></span>  | <span data-ttu-id="8dd69-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8dd69-117">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="8dd69-118">**Al**</span><span class="sxs-lookup"><span data-stu-id="8dd69-118">**GET**</span></span> | <span data-ttu-id="8dd69-119">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/support http/1.1</span><span class="sxs-lookup"><span data-stu-id="8dd69-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/support HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="8dd69-120">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8dd69-120">Request headers</span></span>

<span data-ttu-id="8dd69-121">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8dd69-121">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8dd69-122">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="8dd69-122">Request body</span></span>

<span data-ttu-id="8dd69-123">Yok.</span><span class="sxs-lookup"><span data-stu-id="8dd69-123">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8dd69-124">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8dd69-124">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/support HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07029132-385d-416f-a9a6-df5e9e4c78d3
MS-CorrelationId: 20604323-50bf-4738-9968-c5486ab32be0
```

## <a name="rest-response"></a><span data-ttu-id="8dd69-125">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8dd69-125">REST response</span></span>

<span data-ttu-id="8dd69-126">Başarılı olursa, bu yöntem yanıt gövdesinde bir **supportprofile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="8dd69-126">If successful, this method returns a **SupportProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8dd69-127">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8dd69-127">Response success and error codes</span></span>

<span data-ttu-id="8dd69-128">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="8dd69-128">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8dd69-129">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8dd69-129">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8dd69-130">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8dd69-130">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8dd69-131">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="8dd69-131">Response example</span></span>

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
