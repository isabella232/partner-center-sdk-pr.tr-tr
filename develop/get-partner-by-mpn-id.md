---
title: İş ortağı MPN kimliğini doğrulama
description: Ortağın MPN profilini C \# veya Iş ortağı merkezi REST API aracılığıyla isteyerek bir ortağın Microsoft iş ortağı ağı tanımlayıcısını (MPN kimliği) nasıl doğrulayacağınızı öğrenin.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 6ef7bcb35274a6bcbaddbe0553ca0cb4dc1b2f9c
ms.sourcegitcommit: 8a5c37376a29e29fe0002a980082d4acc6b91131
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 11/11/2020
ms.locfileid: "97769940"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a><span data-ttu-id="00caa-103">C veya Iş Ortağı Merkezi aracılığıyla iş ortağı MPN KIMLIĞINI doğrulayın \# REST API</span><span class="sxs-lookup"><span data-stu-id="00caa-103">Verify a partner MPN ID via C\# or the Partner Center REST API</span></span>

<span data-ttu-id="00caa-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="00caa-104">**Applies To**</span></span>

- <span data-ttu-id="00caa-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="00caa-105">Partner Center</span></span>
- <span data-ttu-id="00caa-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="00caa-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="00caa-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="00caa-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="00caa-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="00caa-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="00caa-109">Ortağın Microsoft İş Ortağı Ağı tanımlayıcısını doğrulama (MPN KIMLIĞI).</span><span class="sxs-lookup"><span data-stu-id="00caa-109">How to verify a partner's Microsoft Partner Network identifier (MPN ID).</span></span>

<span data-ttu-id="00caa-110">Burada gösterilen teknik, iş ortağının MPN profilini iş ortağı merkezinden isteyerek ortağın Microsoft İş Ortağı Ağı tanımlayıcısını doğrular.</span><span class="sxs-lookup"><span data-stu-id="00caa-110">The technique shown here verifies the partner's Microsoft Partner Network identifier by requesting the partner's MPN profile from partner center.</span></span> <span data-ttu-id="00caa-111">İstek başarılı olursa tanımlayıcı geçerli kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="00caa-111">The identifier is considered valid if the request succeeds.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="00caa-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="00caa-112">Prerequisites</span></span>

- <span data-ttu-id="00caa-113">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="00caa-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="00caa-114">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="00caa-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="00caa-115">Doğrulanacak iş ortağı MPN KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="00caa-115">The partner MPN ID to verify.</span></span> <span data-ttu-id="00caa-116">Bu değeri atlarsanız istek, oturum açmış ortağın MPN profilini alır.</span><span class="sxs-lookup"><span data-stu-id="00caa-116">If you omit this value, the request retrieves the MPN profile of the signed-in partner.</span></span>

## <a name="c"></a><span data-ttu-id="00caa-117">C\#</span><span class="sxs-lookup"><span data-stu-id="00caa-117">C\#</span></span>

<span data-ttu-id="00caa-118">Ortağın MPN KIMLIĞINI doğrulamak için, önce [**ıaggregatepartner. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) özelliğinden iş ortağı profili toplama işlemlerine bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="00caa-118">To verify a partner's MPN ID, first retrieve an interface to partner profile collection operations from the [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) property.</span></span> <span data-ttu-id="00caa-119">Ardından [**Mpnprofile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) özelliğinden MPN profil işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="00caa-119">Then get an interface to MPN profile operations from the [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) property.</span></span> <span data-ttu-id="00caa-120">Son olarak, MPN profilini almak için MPN KIMLIĞIYLE [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="00caa-120">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods with the MPN ID to retrieve the MPN profile.</span></span> <span data-ttu-id="00caa-121">Get veya GetAsync çağrısından MPN KIMLIĞINI atlarsanız, istek, oturum açmış ortağın MPN profilini almaya çalışır.</span><span class="sxs-lookup"><span data-stu-id="00caa-121">If you omit the MPN ID from the Get or GetAsync call, the request attempts to retrieve the MPN profile of the signed-in partner.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

<span data-ttu-id="00caa-122">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="00caa-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="00caa-123">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: VerifyPartnerMpnId.cs</span><span class="sxs-lookup"><span data-stu-id="00caa-123">**Project**: Partner Center SDK Samples **Class**: VerifyPartnerMpnId.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="00caa-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="00caa-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="00caa-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="00caa-125">Request syntax</span></span>

| <span data-ttu-id="00caa-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="00caa-126">Method</span></span>  | <span data-ttu-id="00caa-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="00caa-127">Request URI</span></span>                                                                         |
|---------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="00caa-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="00caa-128">**GET**</span></span> | <span data-ttu-id="00caa-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/MPN? Mpnıd = {MPN-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="00caa-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="00caa-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="00caa-130">URI parameter</span></span>

<span data-ttu-id="00caa-131">Ortağı tanımlamak için aşağıdaki sorgu parametresini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="00caa-131">Provide the following query parameter to identify the partner.</span></span> <span data-ttu-id="00caa-132">Bu sorgu parametresini atlarsanız istek, oturum açmış ortağın MPN profilini döndürür.</span><span class="sxs-lookup"><span data-stu-id="00caa-132">If you omit this query parameter, the request returns the MPN profile of the signed-in partner.</span></span>

| <span data-ttu-id="00caa-133">Ad</span><span class="sxs-lookup"><span data-stu-id="00caa-133">Name</span></span>   | <span data-ttu-id="00caa-134">Tür</span><span class="sxs-lookup"><span data-stu-id="00caa-134">Type</span></span> | <span data-ttu-id="00caa-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="00caa-135">Required</span></span> | <span data-ttu-id="00caa-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="00caa-136">Description</span></span>                                                 |
|--------|------|----------|-------------------------------------------------------------|
| <span data-ttu-id="00caa-137">MPN kimliği</span><span class="sxs-lookup"><span data-stu-id="00caa-137">mpn-id</span></span> | <span data-ttu-id="00caa-138">int</span><span class="sxs-lookup"><span data-stu-id="00caa-138">int</span></span>  | <span data-ttu-id="00caa-139">No</span><span class="sxs-lookup"><span data-stu-id="00caa-139">No</span></span>       | <span data-ttu-id="00caa-140">Ortağı tanımlayan Microsoft İş Ortağı Ağı KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="00caa-140">A Microsoft Partner Network ID that identifies the partner.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="00caa-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="00caa-141">Request headers</span></span>

<span data-ttu-id="00caa-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="00caa-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="00caa-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="00caa-143">Request body</span></span>

<span data-ttu-id="00caa-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="00caa-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="00caa-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="00caa-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="00caa-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="00caa-146">REST response</span></span>

<span data-ttu-id="00caa-147">Başarılı olursa, yanıt gövdesi iş ortağı için [Mpnprofile](profile-resources.md#mpnprofile) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="00caa-147">If successful, the response body contains the [MpnProfile](profile-resources.md#mpnprofile) resource for the partner.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="00caa-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="00caa-148">Response success and error codes</span></span>

<span data-ttu-id="00caa-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="00caa-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="00caa-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="00caa-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="00caa-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="00caa-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example-success"></a><span data-ttu-id="00caa-152">Yanıt örneği (başarılı)</span><span class="sxs-lookup"><span data-stu-id="00caa-152">Response example (success)</span></span>

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

### <a name="response-example-failure"></a><span data-ttu-id="00caa-153">Yanıt örneği (hata)</span><span class="sxs-lookup"><span data-stu-id="00caa-153">Response example (failure)</span></span>

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
