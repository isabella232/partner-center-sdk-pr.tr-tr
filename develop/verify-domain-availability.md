---
title: Etki alanı kullanılabilirliğini doğrulama
description: Bir etki alanının kullanılabilir olup olmadığını belirleme.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e2b8f0438516cc0aff9c4d8159c22de43ec582e4
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111530285"
---
# <a name="verify-domain-availability"></a>Etki alanı kullanılabilirliğini doğrulama

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bir etki alanının kullanılabilir olup olmadığını belirleme.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Bir etki alanı `contoso.onmicrosoft.com` (örneğin).

## <a name="c"></a>C\#

Bir etki alanının kullanılabilir olup olduğunu doğrulamak için önce [**IAggregatePartner.Domains'i**](/dotnet/api/microsoft.store.partnercenter.ipartner.domains) çağırarak etki alanı işlemlerine bir arabirim alın. Ardından, kontrol [**etmek için etki alanıyla ByDomain**](/dotnet/api/microsoft.store.partnercenter.domains.idomaincollection.bydomain) yöntemini arayın. Bu yöntem, belirli bir etki alanı için kullanılabilir işlemler için bir arabirim sağlar. Son olarak, etki [**alanının zaten**](/dotnet/api/microsoft.store.partnercenter.domains.idomain.exists) var olup olduğunu görmek için Exists yöntemini çağırabilirsiniz.

``` csharp
// IAggregatePartner partnerOperations;
// const string domain = "contoso.onmicrosoft.com";

bool result = partnerOperations.Domains.ByDomain(domain).Exists();
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Örnekleri **Sınıfı:** CheckDomainAvailability.cs

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                              |
|----------|--------------------------------------------------------------------------|
| **Kafa** | [*{baseURL}*](partner-center-rest-urls.md)/v1/domains/{domain} HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Etki alanı kullanılabilirliğini doğrulamak için aşağıdaki sorgu parametresini kullanın.

| Ad       | Tür       | Gerekli | Açıklama                                   |
|------------|------------|----------|-----------------------------------------------|
| **Etki alanı** | **string** | Y        | Kontrol etmek için etki alanını tanımlayan bir dize. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Etki alanı mevcutsa kullanılamaz ve 200 Tamam yanıt durum kodu döndürülür. Etki alanı bulunamasa kullanılabilir ve 404 Bulunamadı yanıt durum kodu döndürülür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example-for-when-the-domain-is-already-in-use"></a>Etki alanı zaten kullanımda olduğunda için yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 0
MS-CorrelationId: ec57501a-a4c3-45ee-ab2b-da4250545fc9
MS-RequestId: cf5b00d6-9240-431c-a973-cc06c904e5bf
MS-CV: 7UXAHds8J0mNUCSp.0
MS-ServerId: 201022015
Date: Tue, 31 Jan 2017 22:22:35 GMT
```

### <a name="response-example-for-when-the-domain-is-available"></a>Etki alanının kullanılabilir olduğu zaman için yanıt örneği

```http
HTTP/1.1 404 Not Found
Content-Length: 0
MS-CorrelationId: 54770745-17f0-433c-bd7b-0265e5b38f98
MS-RequestId: 1169a4cd-3be7-4e29-9cb3-0f78ffa2e91e
MS-CV: RRmc+bEw9U2e97CC.0
MS-ServerId: 202010406
Date: Tue, 31 Jan 2017 22:36:01 GMT
```
