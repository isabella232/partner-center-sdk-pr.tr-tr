---
title: Belirli bir iş ortağı için virgülle ayrılmış biçimdeki kenar boşluklarının listesini alır.
description: Belirli bir iş ortağı için virgülle ayrılmış biçimdeki kenar boşluklarının listesini alır.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 6328ab962b2f210cee76b585ce2cf883c41eac3f
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646413"
---
# <a name="download-margins"></a>İndirme kenar boşlukları


**Uygulama hedefi**: Iş Ortağı Merkezi 

**Uygun roller**: genel yönetici | Yönetim Aracısı

İş ortakları, belirli bir iş ortağı için etkin kenar boşluklarının listesini alabilir. Bu yöntem, iş ortağı ve kullanılabilir başlangıç ve bitiş tarihlerine göre kenar boşlukları döndürür. İndirme kenar boşlukları, verileri virgülle ayrılmış bir biçimde döndürür.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.


## <a name="rest-request"></a>REST isteği
[GET]/v1/kenar boşlukları

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **AL**  | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Margins/Download http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/margins/download HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem a.csv dosya olarak fiyat listesini dosya akışı olarak döndürür

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt, başarı veya başarısızlık ve daha fazla hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve daha fazla parametreyi okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

"id","productId","publisherName","productTitle","productType"","marginPercentage","startDate","endDate","status","statusDate"
"97620c21cc32_97cdce68-cce4-42aa-9410-233fd0269502","DZH318Z08L40","Market Place Test","Software As A Service Support Preview App","SaaS","10.0","2021-08-04T23:16:22.4736653Z","2022-03-31T23:59:59Z","live","2021-08-04T23:16:22.4736653Z"

```
