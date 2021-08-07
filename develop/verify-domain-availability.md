---
title: Etki alanı kullanılabilirliğini doğrulama
description: Bir etki alanının kullanıma hazır olup olmadığını belirleme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 3515216127219908aeefb2e070b138e75dc1f0e72b1f57f07f1dbff65ab79558
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989058"
---
# <a name="verify-domain-availability"></a>Etki alanı kullanılabilirliğini doğrulama

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bir etki alanının kullanıma hazır olup olmadığını belirleme.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir etki alanı (örneğin `contoso.onmicrosoft.com` ).

## <a name="c"></a>C\#

Bir etki alanının kullanılabilir olup olmadığını doğrulamak için, önce etki alanı işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Domains**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) ' ı çağırın. Ardından, denetlenecek etki alanı ile [**bydomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) yöntemini çağırın. Bu yöntem, belirli bir etki alanı için kullanılabilir işlemlere bir arabirim alır. Son olarak, etki alanının zaten mevcut olup olmadığını görmek için [**EXISTS**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) metodunu çağırın.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: checkdomainavaılabılıty. cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                              |
|----------|--------------------------------------------------------------------------|
| **BAŞLı** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Domains/{Domain} http/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Etki alanı kullanılabilirliğini doğrulamak için aşağıdaki sorgu parametresini kullanın.

| Ad       | Tür       | Gerekli | Açıklama                                   |
|------------|------------|----------|-----------------------------------------------|
| **alanını** | **string** | Y        | Denetlenecek etki alanını tanımlayan bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
HEAD https://api.partnercenter.microsoft.com/v1/domains/contoso.onmicrosoft.com HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

Etki alanı varsa, kullanım için kullanılamaz ve 200 Tamam yanıt durum kodu döndürülür. Etki alanı bulunmazsa, kullanılabilir ve 404 yanıt durum kodu döndürülür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Etki alanı zaten kullanımda olduğunda yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Etki alanı kullanılabilir olduğunda yanıt örneği

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
