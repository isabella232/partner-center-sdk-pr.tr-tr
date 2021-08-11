---
title: İş ortağı MPN kimliğini doğrulama
description: C veya Microsoft İş Ortağı Ağı aracılığıyla iş ortağının MPN profilini isteğinde bulundurarak iş ortağının Microsoft İş Ortağı Ağı tanımlayıcısını (MPN \# KIMLIĞI) doğrulamayı İş Ortağı Merkezi REST API.
ms.date: 09/29/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 223f0da94f5a1c12b4f6de32184296b88ab5f443a69feac89152acc1aa9ccbd6
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995926"
---
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>C veya ağ üzerinden iş ortağı MPN \# kimliğini İş Ortağı Merkezi REST API

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

İş ortağının kimlik doğrulama Microsoft İş Ortağı Ağı (MPN KIMLIĞI).

Burada gösterilen teknik, iş ortağının mpN profilini Microsoft İş Ortağı Ağı iş ortağının mpN profilini İş Ortağı Merkezi. İstek başarılı olursa tanımlayıcı geçerli kabul edilir.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Doğrulan iş ortağı MPN kimliği. Bu değeri atlarsanız istek, oturum alıkan iş ortağının MPN profilini verir.

## <a name="c"></a>C\#

Bir iş ortağının MPN kimliğini doğrulamak için, önce [**IAggregatePartner.Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) özelliğinden iş ortağı profili toplama işlemlerine bir arabirim alın. Ardından [**MpnProfile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) özelliğinden MPN profil işlemlerine bir arabirim elde etmek. Son olarak, MPN profilini almak için MPN Kimliği ile [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) yöntemlerini çağırabilirsiniz. Get veya GetAsync çağrısından MPN kimliğini atlarsanız, istek oturum açma iş ortağının MPN profilini almaya çalışır.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** VerifyPartnerMpnId.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Al** | [*{baseURL}*](partner-center-rest-urls.md)/v1/profiles/mpn?mpnId={mpn-id} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

İş ortağını tanımlamak için aşağıdaki sorgu parametresini girin. Bu sorgu parametresini atlarsanız istek, oturum alıkan iş ortağının MPN profilini döndürür.

| Ad   | Tür | Gerekli | Açıklama                                                 |
|--------|------|----------|-------------------------------------------------------------|
| mpn-id | int  | No       | İş Microsoft İş Ortağı Ağı tanımlayan bir kimlik. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

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

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi iş ortağı [için MpnProfile](profile-resources.md#mpnprofile) kaynağını içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example-success"></a>Yanıt örneği (başarılı)

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

### <a name="response-example-failure"></a>Yanıt örneği (hata)

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
