---
title: İş ortağı yasal iş profili alma
description: Yasal iş profilinizi almak için API'leri kullanmayı öğrenin.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ba0654e364674bc2db129a0904d411c6fb67cbb9
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549068"
---
# <a name="get-the-partner-legal-business-profile"></a><span data-ttu-id="d8de3-103">İş ortağı yasal iş profili alma</span><span class="sxs-lookup"><span data-stu-id="d8de3-103">Get the partner legal business profile</span></span>

<span data-ttu-id="d8de3-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="d8de3-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d8de3-105">İş ortağının yasal iş profilini elde etmek.</span><span class="sxs-lookup"><span data-stu-id="d8de3-105">How to get a partner's legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8de3-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d8de3-106">Prerequisites</span></span>

- <span data-ttu-id="d8de3-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d8de3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d8de3-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d8de3-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d8de3-109">C\#</span><span class="sxs-lookup"><span data-stu-id="d8de3-109">C\#</span></span>

<span data-ttu-id="d8de3-110">İş ortağı yasal iş profilini almak için, önce **IAggregatePartner.Profiles** özelliğinden iş ortağı profili işlemlerinin koleksiyonuna bir arabirim elde etmek.</span><span class="sxs-lookup"><span data-stu-id="d8de3-110">To get the partner legal business profile, first get an interface to the collection of partner profile operations from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="d8de3-111">Ardından yasal iş profili işlemlerine bir arabirim almak için **LegalBusinessProfile** özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="d8de3-111">Then, get the value of the **LegalBusinessProfile** property to retrieve an interface to legal business profile operations.</span></span> <span data-ttu-id="d8de3-112">Son olarak, [**profili almak**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) için Get veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8de3-112">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.getasync) method to retrieve the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var billingProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();
```

<span data-ttu-id="d8de3-113">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8de3-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d8de3-114">**Project:** İş Ortağı Merkezi SDK'sı Örnekleri **Sınıfı:** GetLegalBusinessProfile.cs</span><span class="sxs-lookup"><span data-stu-id="d8de3-114">**Project**: Partner Center SDK Samples **Class**: GetLegalBusinessProfile.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d8de3-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d8de3-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d8de3-116">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="d8de3-116">Request syntax</span></span>

| <span data-ttu-id="d8de3-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d8de3-117">Method</span></span>  | <span data-ttu-id="d8de3-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d8de3-118">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="d8de3-119">**Al**</span><span class="sxs-lookup"><span data-stu-id="d8de3-119">**GET**</span></span> | <span data-ttu-id="d8de3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d8de3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d8de3-121">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d8de3-121">Request headers</span></span>

<span data-ttu-id="d8de3-122">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d8de3-122">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d8de3-123">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d8de3-123">Request body</span></span>

<span data-ttu-id="d8de3-124">Yok.</span><span class="sxs-lookup"><span data-stu-id="d8de3-124">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d8de3-125">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d8de3-125">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d8de3-126">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d8de3-126">REST response</span></span>

<span data-ttu-id="d8de3-127">Başarılı olursa, bu yöntem yanıt **gövdesinde bir LegalBusinessProfile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="d8de3-127">If successful, this method returns a **LegalBusinessProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d8de3-128">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d8de3-128">Response success and error codes</span></span>

<span data-ttu-id="d8de3-129">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="d8de3-129">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d8de3-130">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8de3-130">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d8de3-131">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d8de3-131">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d8de3-132">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d8de3-132">Response example</span></span>

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
