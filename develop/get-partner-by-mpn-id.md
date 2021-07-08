---
title: İş ortağı MPN kimliğini doğrulama
description: Ortağın MPN profilini C \# veya Iş ortağı merkezi REST API aracılığıyla isteyerek bir ortağın Microsoft iş ortağı ağı tanımlayıcısını (MPN kimliği) nasıl doğrulayacağınızı öğrenin.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6bd51850c7bc5a099a34f9c028a58e247c2600a3
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548830"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="77766-103">C veya Iş Ortağı Merkezi aracılığıyla iş ortağı MPN KIMLIĞINI doğrulayın \# REST API</span><span class="sxs-lookup"><span data-stu-id="77766-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="77766-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="77766-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="77766-105">Ortağın Microsoft İş Ortağı Ağı tanımlayıcısını doğrulama (MPN KIMLIĞI).</span><span class="sxs-lookup"><span data-stu-id="77766-105">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="77766-106">Burada gösterilen teknik, iş ortağının MPN profilini iş ortağı merkezinden isteyerek ortağın Microsoft İş Ortağı Ağı tanımlayıcısını doğrular.</span><span class="sxs-lookup"><span data-stu-id="77766-106">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="77766-107">İstek başarılı olursa tanımlayıcı geçerli kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="77766-107">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77766-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="77766-108">Prerequisites</span></span>

- <span data-ttu-id="77766-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="77766-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="77766-110">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="77766-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="77766-111">Doğrulanacak iş ortağı MPN KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="77766-111">The partner MPN ID to verify.</span></span> <span data-ttu-id="77766-112">Bu değeri atlarsanız istek, oturum açmış ortağın MPN profilini alır.</span><span class="sxs-lookup"><span data-stu-id="77766-112">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="77766-113">C\#</span><span class="sxs-lookup"><span data-stu-id="77766-113">C\#</span></span>

<span data-ttu-id="77766-114">Ortağın MPN KIMLIĞINI doğrulamak için, önce [**ıaggregatepartner. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) özelliğinden iş ortağı profili toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="77766-114">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="77766-115">Ardından [**Mpnprofile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) özelliğinden MPN profil işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="77766-115">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="77766-116">Son olarak, MPN profilini almak için MPN KIMLIĞIYLE [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="77766-116">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="77766-117">Get veya GetAsync çağrısından MPN KIMLIĞINI atlarsanız, istek, oturum açmış ortağın MPN profilini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="77766-117">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="77766-118">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="77766-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="77766-119">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: doğrulama ypartnermpnıd. cs</span><span class="sxs-lookup"><span data-stu-id="77766-119">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="77766-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="77766-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="77766-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="77766-121">Request syntax</span></span>

| <span data-ttu-id="77766-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="77766-122">Method</span></span>  | <span data-ttu-id="77766-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="77766-123">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="77766-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="77766-124">**GET**</span></span> | <span data-ttu-id="77766-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/MPN? Mpnıd = {MPN-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="77766-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="77766-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="77766-126">URI parameter</span></span>

<span data-ttu-id="77766-127">Ortağı tanımlamak için aşağıdaki sorgu parametresini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="77766-127">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="77766-128">Bu sorgu parametresini atlarsanız istek, oturum açmış ortağın MPN profilini döndürür.</span><span class="sxs-lookup"><span data-stu-id="77766-128">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="77766-129">Ad</span><span class="sxs-lookup"><span data-stu-id="77766-129">Name</span></span>   | <span data-ttu-id="77766-130">Tür</span><span class="sxs-lookup"><span data-stu-id="77766-130">Type</span></span> | <span data-ttu-id="77766-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="77766-131">Required</span></span> | <span data-ttu-id="77766-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="77766-132">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="77766-133">MPN kimliği</span><span class="sxs-lookup"><span data-stu-id="77766-133">mpn-id</span></span> | <span data-ttu-id="77766-134">int</span><span class="sxs-lookup"><span data-stu-id="77766-134">int</span></span>  | <span data-ttu-id="77766-135">Hayır</span><span class="sxs-lookup"><span data-stu-id="77766-135">No</span></span>       | <span data-ttu-id="77766-136">Ortağı tanımlayan Microsoft İş Ortağı Ağı KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="77766-136">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="77766-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="77766-137">Request headers</span></span>

<span data-ttu-id="77766-138">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="77766-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="77766-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="77766-139">Request body</span></span>

<span data-ttu-id="77766-140">Yok.</span><span class="sxs-lookup"><span data-stu-id="77766-140">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="77766-141">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="77766-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn?mpnId=9999999 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="77766-142">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="77766-142">REST response</span></span>

<span data-ttu-id="77766-143">Başarılı olursa, yanıt gövdesi iş ortağı için [Mpnprofile](profile-resources.md#mpnprofile) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="77766-143">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="77766-144">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="77766-144">Response success and error codes</span></span>

<span data-ttu-id="77766-145">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="77766-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="77766-146">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="77766-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="77766-147">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="77766-147">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="77766-148">Yanıt örneği (başarılı)</span><span class="sxs-lookup"><span data-stu-id="77766-148">Response example (success)</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 159
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: e39e0ddf-3fd0-4b7e-bb4e-8aebe242d3ee
MS-CV: s2GvkNgZsUSadxQX.0
MS-ServerId: 030011719
Date: Thu, 13 Apr 2017 18:13:40 GMT

{
    "mpnId": "4391507",
    "profileType": "MpnProfile",
    "links": {
        "self": {
            "uri": "/profiles/mpn",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "MpnProfile"
    }
}
```

### <a name="response-example-failure"></a><span data-ttu-id="77766-149">Yanıt örneği (hata)</span><span class="sxs-lookup"><span data-stu-id="77766-149">Response example (failure)</span></span>

```http
HTTP/1.1 404 Not Found
Content-Length: 124
Content-Type: application/json; charset=utf-8
MS-CorrelationId: e937630b-8341-4d70-8f73-450d32ee0189
MS-RequestId: 560df6b9-6e53-4954-aed7-133477ac1194
MS-CV: sLRFZMWm+EKuL47u.0
MS-ServerId: 102030524
Date: Thu, 13 Apr 2017 18:26:51 GMT

{
    "code": 3000,
    "description": "Partner Organization with partner_id 9999999 could not be found",
    "data": [],
    "source": "PartnerFD"
}
```
