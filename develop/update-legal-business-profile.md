---
title: İş ortağı yasal iş profili güncelleştirme
description: İş ortağı yasal iş profilini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: cb9f5815e0019c5e9b648dfd865e9752f0afdf05
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530336"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="21909-103">İş ortağı yasal iş profili güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="21909-103">Update the partner legal business profile</span></span>

<span data-ttu-id="21909-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="21909-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="21909-105">İş ortağı yasal iş profilini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="21909-105">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21909-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="21909-106">Prerequisites</span></span>

- <span data-ttu-id="21909-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="21909-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="21909-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="21909-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="21909-109">C\#</span><span class="sxs-lookup"><span data-stu-id="21909-109">C\#</span></span>

<span data-ttu-id="21909-110">İş ortağı yasal iş profilini güncelleştirmek için öncelikle bir **LegalBusinessProfile** nesnesi örneği oluşturun ve bunu mevcut profille doldurmak.</span><span class="sxs-lookup"><span data-stu-id="21909-110">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="21909-111">Daha fazla bilgi için [bkz. İş ortağı yasal iş profilini al.](get-legal-business-profile.md)</span><span class="sxs-lookup"><span data-stu-id="21909-111">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="21909-112">Ardından, değiştirmeniz gereken özellikleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="21909-112">Then, update the properties that you need to change.</span></span> <span data-ttu-id="21909-113">Aşağıdaki kod örneği, adresin ve birincil iletişim telefon numaralarının değiştirilmesini göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="21909-113">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="21909-114">Ardından, **IAggregatePartner.Profiles** özelliğinden iş ortağı profili işlemleri koleksiyonuna bir arabirim elde etmek.</span><span class="sxs-lookup"><span data-stu-id="21909-114">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="21909-115">Ardından yasal iş profili işlemlerine bir arabirim almak için **LegalBusinessProfile** özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="21909-115">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="21909-116">Son olarak, [**profili güncelleştirmek**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) için değiştirilen nesneyle Update veya [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21909-116">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="21909-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="21909-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="21909-118">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="21909-118">Request syntax</span></span>

| <span data-ttu-id="21909-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="21909-119">Method</span></span>  | <span data-ttu-id="21909-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="21909-120">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="21909-121">**PUT**</span><span class="sxs-lookup"><span data-stu-id="21909-121">**PUT**</span></span> | <span data-ttu-id="21909-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="21909-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="21909-123">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="21909-123">Request headers</span></span>

<span data-ttu-id="21909-124">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="21909-124">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="21909-125">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="21909-125">Request body</span></span>

<span data-ttu-id="21909-126">Yasal iş profili kaynağı.</span><span class="sxs-lookup"><span data-stu-id="21909-126">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="21909-127">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="21909-127">Request example</span></span>

```http
PUT https://api.partnercenter.microsoft.com/v1/profiles/legalbusiness HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 806
Expect: 100-continue

{
    "CompanyName": "Lucerne Publishing",
    "Address": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": "Gena",
        "LastName": "Soto",
        "PhoneNumber": "4255550110"
    },
    "PrimaryContact": {
        "FirstName": "Gena",
        "LastName": "Soto",
        "Email": "gena@lucernepublishing.com",
        "PhoneNumber": "4255550110"
    },
    "CompanyApproverAddress": {
        "Country": "US",
        "Region": null,
        "City": "Redmond",
        "State": "WA",
        "AddressLine1": "123 Main Street",
        "AddressLine2": "",
        "PostalCode": "98052",
        "FirstName": null,
        "LastName": null,
        "PhoneNumber": null
    },
    "CompanyApproverEmail": "gena@lucernepublishing.com",
    "VettingStatus": "authorized",
    "VettingSubStatus": "none",
    "Links": {
        "Self": {
            "Uri": "/profiles/legalbusiness",
            "Method": "GET",
            "Headers": []
        }
    },
    "Attributes": {
        "ObjectType": "LegalBusinessProfile"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="21909-128">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="21909-128">REST response</span></span>

<span data-ttu-id="21909-129">Başarılı olursa yanıt gövdesi güncelleştirilmiş **LegalBusinessProfile dosyasını içerir**</span><span class="sxs-lookup"><span data-stu-id="21909-129">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="21909-130">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="21909-130">Response success and error codes</span></span>

<span data-ttu-id="21909-131">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="21909-131">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="21909-132">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="21909-132">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="21909-133">Tam liste için bkz. [İş Ortağı Merkezi kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="21909-133">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="21909-134">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="21909-134">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1157
Content-Type: application/json; charset=utf-8
MS-CorrelationId: aa2a0d8c-7a41-470f-97ae-b82e6c338ee4
MS-RequestId: 4549ac0c-0f1d-4d8f-b02f-6d36fadcccee
MS-CV: KZLU42qJ4EObO75q.0
MS-ServerId: 030020643
Date: Tue, 21 Mar 2017 22:03:15 GMT

{
    "companyName": "Lucerne Publishing",
    "address": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
        "addressLine1": "123 Main Street",
        "addressLine2": "",
        "postalCode": "98052",
        "firstName": "Gena",
        "lastName": "Soto",
        "phoneNumber": "4255550110"
    },
    "primaryContact": {
        "firstName": "Gena",
        "lastName": "Soto",
        "email": "gena@lucernepublishing.com",
        "phoneNumber": "4255550110"
    },
    "companyApproverAddress": {
        "country": "US",
        "city": "Redmond",
        "state": "WA",
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
