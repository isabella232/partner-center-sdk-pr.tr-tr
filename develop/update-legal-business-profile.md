---
title: İş ortağı yasal iş profili güncelleştirme
description: İş ortağı yasal iş profilini güncelleştirme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: parthpandyaMSFT
ms.author: parthp
ms.openlocfilehash: 6c61b51ab0680e36daa99c11dc8e8c3506259d29
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769599"
---
# <a name="update-the-partner-legal-business-profile"></a><span data-ttu-id="13546-103">İş ortağı yasal iş profili güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="13546-103">Update the partner legal business profile</span></span>

<span data-ttu-id="13546-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="13546-104">**Applies To**</span></span>

- <span data-ttu-id="13546-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="13546-105">Partner Center</span></span>
- <span data-ttu-id="13546-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="13546-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="13546-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="13546-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="13546-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="13546-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="13546-109">İş ortağı yasal iş profilini güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="13546-109">How to update the partner legal business profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="13546-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="13546-110">Prerequisites</span></span>

- <span data-ttu-id="13546-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="13546-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="13546-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="13546-112">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="13546-113">C\#</span><span class="sxs-lookup"><span data-stu-id="13546-113">C\#</span></span>

<span data-ttu-id="13546-114">İş ortağı yasal iş profilini güncelleştirmek için önce bir **LegalBusinessProfile** nesnesi örneği oluşturun ve var olan profille doldurun.</span><span class="sxs-lookup"><span data-stu-id="13546-114">To update the partner legal business profile, first instantiate a **LegalBusinessProfile** object and populate it with the existing profile.</span></span> <span data-ttu-id="13546-115">Daha fazla bilgi için bkz. [iş ortağı yasal iş profilini edinme](get-legal-business-profile.md).</span><span class="sxs-lookup"><span data-stu-id="13546-115">For more information, see [Get the partner legal business profile](get-legal-business-profile.md).</span></span> <span data-ttu-id="13546-116">Ardından, değiştirmeniz gereken özellikleri güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="13546-116">Then, update the properties that you need to change.</span></span> <span data-ttu-id="13546-117">Aşağıdaki kod örneği, adresi ve birincil iletişim telefon numaralarını değiştirmeyi gösterir.</span><span class="sxs-lookup"><span data-stu-id="13546-117">The following code example illustrates changing the address and primary contact phone numbers.</span></span>

<span data-ttu-id="13546-118">Sonra, **ıaggregatepartner. Profiles** özelliğinden iş ortağı profili işlemleri koleksiyonuna bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="13546-118">Next, get an interface to the partner profile operations collection from the **IAggregatePartner.Profiles** property.</span></span> <span data-ttu-id="13546-119">Ardından, yasal iş profili işlemlerine bir arabirim almak için **LegalBusinessProfile** özelliğinin değerini alın.</span><span class="sxs-lookup"><span data-stu-id="13546-119">Then, retrieve the value of the **LegalBusinessProfile** property to get an interface to legal business profile operations.</span></span> <span data-ttu-id="13546-120">Son olarak, profili güncelleştirmek için değiştirilen nesneyle [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) veya [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="13546-120">Finally, call the [**Update**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.update) or [**UpdateAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.ilegalbusinessprofile.updateasync) method with the changed object to update the profile.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var legalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Get();

// Change the address and primary contact phone number.
legalBusinessProfile.Address.PhoneNumber = "4255550110";
legalBusinessProfile.PrimaryContact.PhoneNumber = "4255550110";

// Apply changes to the profile.
var updatedLegalBusinessProfile = partnerOperations.Profiles.LegalBusinessProfile.Update(legalBusinessProfile);
```

## <a name="rest-request"></a><span data-ttu-id="13546-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="13546-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="13546-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="13546-122">Request syntax</span></span>

| <span data-ttu-id="13546-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="13546-123">Method</span></span>  | <span data-ttu-id="13546-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="13546-124">Request URI</span></span>                                                                    |
|---------|--------------------------------------------------------------------------------|
| <span data-ttu-id="13546-125">**PUT**</span><span class="sxs-lookup"><span data-stu-id="13546-125">**PUT**</span></span> | <span data-ttu-id="13546-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/legalbusiness http/1.1</span><span class="sxs-lookup"><span data-stu-id="13546-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/legalbusiness HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="13546-127">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="13546-127">Request headers</span></span>

<span data-ttu-id="13546-128">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="13546-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="13546-129">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="13546-129">Request body</span></span>

<span data-ttu-id="13546-130">Yasal iş profili kaynağı.</span><span class="sxs-lookup"><span data-stu-id="13546-130">The legal business profile resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="13546-131">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="13546-131">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="13546-132">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="13546-132">REST response</span></span>

<span data-ttu-id="13546-133">Başarılı olursa, yanıt gövdesi güncelleştirilmiş **LegalBusinessProfile** içerir</span><span class="sxs-lookup"><span data-stu-id="13546-133">If successful, the response body contains the updated **LegalBusinessProfile**</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="13546-134">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="13546-134">Response success and error codes</span></span>

<span data-ttu-id="13546-135">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="13546-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="13546-136">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="13546-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="13546-137">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="13546-137">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="13546-138">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="13546-138">Response example</span></span>

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
