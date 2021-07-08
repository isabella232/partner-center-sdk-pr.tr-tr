---
title: Microsoft İş Ortağı Ağı profil alma
description: Ortağın MPN profilini temsil eden bir nesne alır.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 38c12a9a9755b9838b7742d9f38c5cbd52b81210
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548864"
---
# <a name="get-microsoft-partner-network-profile"></a><span data-ttu-id="58740-103">Microsoft İş Ortağı Ağı profil alma</span><span class="sxs-lookup"><span data-stu-id="58740-103">Get Microsoft Partner Network profile</span></span>

<span data-ttu-id="58740-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="58740-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="58740-105">Ortağın MPN profilini temsil eden bir nesne alır.</span><span class="sxs-lookup"><span data-stu-id="58740-105">Gets an object representing the partner's MPN profile.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="58740-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="58740-106">Prerequisites</span></span>

- <span data-ttu-id="58740-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="58740-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="58740-108">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="58740-108">This scenario supports authentication with App+User credentials only.</span></span>

## <a name="c"></a><span data-ttu-id="58740-109">C\#</span><span class="sxs-lookup"><span data-stu-id="58740-109">C\#</span></span>

<span data-ttu-id="58740-110">Bir iş ortağı ağ profili almak için **ıaggregatepartner. Profiles** koleksiyonunuzu kullanın ve **mpnprofile** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="58740-110">To get a partner network profile, use your **IAggregatePartner.Profiles** collection and call the **MpnProfile** property.</span></span> <span data-ttu-id="58740-111">Son olarak [**Get ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="58740-111">Finally, call the [**Get()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;

var mpnProfile = partnerOperations.Profiles.MpnProfile.Get();
```

<span data-ttu-id="58740-112">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="58740-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="58740-113">**Project**:P artnercentersdk. featuressamples **sınıfı**: getmpnprofile. cs</span><span class="sxs-lookup"><span data-stu-id="58740-113">**Project**:PartnerCenterSDK.FeaturesSamples **Class**: GetMPNProfile.cs</span></span>

## <a name="java"></a><span data-ttu-id="58740-114">Java</span><span class="sxs-lookup"><span data-stu-id="58740-114">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="58740-115">Bir iş ortağı ağ profili almak için **ıaggregatepartner. getProfiles** işlevinizi kullanın ve **Getmpnprofile** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="58740-115">To get a partner network profile, use your **IAggregatePartner.getProfiles** function and call the **getMpnProfile** function.</span></span> <span data-ttu-id="58740-116">Son olarak **Get ()** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="58740-116">Finally, call the **get()** function.</span></span>

```java
// IAggregatePartner partnerOperations;

MpnProfile mpnProfile = partnerOperations.getProfiles().getMpnProfile().get();
```

## <a name="powershell"></a><span data-ttu-id="58740-117">PowerShell</span><span class="sxs-lookup"><span data-stu-id="58740-117">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="58740-118">Bir iş ortağı ağ profili almak için [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) komutunu yürütün.</span><span class="sxs-lookup"><span data-stu-id="58740-118">To get a partner network profile, execute the [**Get-PartnerMpnProfile**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerMpnProfile.md) command.</span></span>

```powershell
Get-PartnerMpnProfile
```

## <a name="rest-request"></a><span data-ttu-id="58740-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="58740-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="58740-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="58740-120">Request syntax</span></span>

| <span data-ttu-id="58740-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="58740-121">Method</span></span>  | <span data-ttu-id="58740-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="58740-122">Request URI</span></span>                                                          |
|---------|----------------------------------------------------------------------|
| <span data-ttu-id="58740-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="58740-123">**GET**</span></span> | <span data-ttu-id="58740-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/MPN http/1.1</span><span class="sxs-lookup"><span data-stu-id="58740-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="58740-125">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="58740-125">Request headers</span></span>

<span data-ttu-id="58740-126">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="58740-126">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="58740-127">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="58740-127">Request body</span></span>

<span data-ttu-id="58740-128">Yok.</span><span class="sxs-lookup"><span data-stu-id="58740-128">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="58740-129">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="58740-129">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/profiles/mpn HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="58740-130">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="58740-130">REST response</span></span>

<span data-ttu-id="58740-131">Başarılı olursa, bu yöntem yanıt gövdesinde bir **Mpnprofile** nesnesi döndürür.</span><span class="sxs-lookup"><span data-stu-id="58740-131">If successful, this method returns a **MPNProfile** object in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="58740-132">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="58740-132">Response success and error codes</span></span>

<span data-ttu-id="58740-133">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="58740-133">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="58740-134">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="58740-134">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="58740-135">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="58740-135">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="58740-136">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="58740-136">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cb9f3209-d020-4bf9-871c-e1f1c75348f8
MS-RequestId: 76879323-92d1-437e-90dd-c84dbb9f7dec
Date: Mon, 21 Mar 2016 05:51:29 GMT

{
    "mpnId":"<mpnID>",
    "profileType":"MpnProfile",
    "links":{
        "self":{
            "uri":"/profiles/mpn",
            "method":"GET",
            "headers":[]
        }
    },
    "attributes":{
        "objectType":"MpnProfile"
    }
}
```
