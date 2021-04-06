---
title: İş ortağı yasal iş profili alma
description: Geçerli iş profilinizi almak için API 'Leri nasıl kullanacağınızı öğrenin.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1d488c8deb9f01110e92327035ce0c3c023fcb46
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500031"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="58740-103">İş ortağı yasal iş profili alma</span><span class="sxs-lookup"><span data-stu-id="58740-103">Get the partner legal business profile</span></span>

<span data-ttu-id="58740-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="58740-104">**Applies To**</span></span>

- <span data-ttu-id="58740-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="58740-105">Partner Center</span></span>
- <span data-ttu-id="58740-106">21Vianet tarafından çalıştırılan İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="58740-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="58740-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="58740-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="58740-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="58740-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="58740-109">İş ortağının yasal iş profilini alma.</span><span class="sxs-lookup"><span data-stu-id="58740-109">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58740-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="58740-110">Prerequisites</span></span>

- <span data-ttu-id="58740-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="58740-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="58740-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="58740-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="58740-113">C\#</span><span class="sxs-lookup"><span data-stu-id="58740-113">C\#</span></span>

<span data-ttu-id="58740-114">İş ortağı yasal iş profilini almak için ilk olarak **ıaggregatepartner. Profiles** özelliğinden iş ortağı profili işlemleri koleksiyonuna bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="58740-114">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="58740-115">Ardından, yasal iş profili işlemlerine bir arabirim almak için **LegalBusinessProfile** özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="58740-115">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="58740-116">Son olarak, profili almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="58740-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="58740-117">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="58740-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="58740-118">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetLegalBusinessProfile. cs</span><span class="sxs-lookup"><span data-stu-id="58740-118">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="58740-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="58740-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="58740-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="58740-120">Request syntax</span></span>

| <span data-ttu-id="58740-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="58740-121">Method</span></span>  | <span data-ttu-id="58740-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="58740-122">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="58740-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="58740-123">**GET**</span></span> | <span data-ttu-id="58740-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="58740-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="58740-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="58740-125">Request headers</span></span>

<span data-ttu-id="58740-126">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="58740-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="58740-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="58740-127">Request body</span></span>

<span data-ttu-id="58740-128">Yok.</span><span class="sxs-lookup"><span data-stu-id="58740-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="58740-129">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="58740-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness?vettingVersion=Current HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="58740-130">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="58740-130">REST response</span></span>

<span data-ttu-id="58740-131">Başarılı olursa, bu yöntem yanıt gövdesinde bir **LegalBusinessProfile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="58740-131">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="58740-132">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="58740-132">Response success and error codes</span></span>

<span data-ttu-id="58740-133">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="58740-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="58740-134">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="58740-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="58740-135">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="58740-135">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="58740-136">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="58740-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1151
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 98a091a0-67db-4eeb-ae0d-7e8b2e39c1d2
MS-RequestId: 7391249f-cba0-467c-b026-7b3a60196422
MS-CV: MEgCpJUoGUeXG+4a.0
MS-ServerId: 030011719
Date: Tue, 21 Mar 2017 17:29:52 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550100"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550100"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Buffalo",
        "state": "NY",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052"
    },
    "companyApproverEmail": "gena@lucernepublishing.com",
    "vettingStatus": "authorized",
    "vettingSubStatus": "none",
    "profileType": "LegalBusinessProfile",
    "links": {
        "self": {
            "uri": "/profiles/legalbusiness",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "LegalBusinessProfile"
    }
}
```
