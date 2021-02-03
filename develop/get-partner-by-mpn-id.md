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
# <a name="verify-a-partner-mpn-id-via-c-or-the-partner-center-rest-api"></a>C veya Iş Ortağı Merkezi aracılığıyla iş ortağı MPN KIMLIĞINI doğrulayın \# REST API

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Ortağın Microsoft İş Ortağı Ağı tanımlayıcısını doğrulama (MPN KIMLIĞI).

Burada gösterilen teknik, iş ortağının MPN profilini iş ortağı merkezinden isteyerek ortağın Microsoft İş Ortağı Ağı tanımlayıcısını doğrular. İstek başarılı olursa tanımlayıcı geçerli kabul edilir.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Doğrulanacak iş ortağı MPN KIMLIĞI. Bu değeri atlarsanız istek, oturum açmış ortağın MPN profilini alır.

## <a name="c"></a>C\#

Ortağın MPN KIMLIĞINI doğrulamak için, önce [**ıaggregatepartner. Profiles**](/dotnet/api/microsoft.store.partnercenter.ipartner.profiles) özelliğinden iş ortağı profili toplama işlemlerine bir arabirim alın. Ardından [**Mpnprofile**](/dotnet/api/microsoft.store.partnercenter.profiles.ipartnerprofilecollection.mpnprofile) özelliğinden MPN profil işlemlerine yönelik bir arabirim alın. Son olarak, MPN profilini almak için MPN KIMLIĞIYLE [**Get**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.profiles.impnprofile.getasync) yöntemlerini çağırın. Get veya GetAsync çağrısından MPN KIMLIĞINI atlarsanız, istek, oturum açmış ortağın MPN profilini almaya çalışır.

``` csharp
// IAggregatePartner partnerOperations;
// string partnerMpnId;

var partnerProfile = partnerOperations.Profiles.MpnProfile.Get(partnerMpnId);
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: VerifyPartnerMpnId.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                         |
|---------|-------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Profiles/MPN? Mpnıd = {MPN-ID} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Ortağı tanımlamak için aşağıdaki sorgu parametresini sağlayın. Bu sorgu parametresini atlarsanız istek, oturum açmış ortağın MPN profilini döndürür.

| Ad   | Tür | Gerekli | Açıklama                                                 |
|--------|------|----------|-------------------------------------------------------------|
| MPN kimliği | int  | No       | Ortağı tanımlayan Microsoft İş Ortağı Ağı KIMLIĞI. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

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

Başarılı olursa, yanıt gövdesi iş ortağı için [Mpnprofile](profile-resources.md#mpnprofile) kaynağını içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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
