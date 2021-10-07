---
title: Verilen iş ortağı için kenar boşluklarının listesini alır.
description: Verilen iş ortağı için kenar boşluklarının listesini alır.
ms.date: 09/30/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 3b36d2d560f3afe43af45e6001f6d407acf3f537
ms.sourcegitcommit: deb3207935fb5a74df515ed0fd4ffec90e6a143c
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/07/2021
ms.locfileid: "129646414"
---
# <a name="get-margins"></a>Kenar boşluklarını al

**Için geçerlidir:** İş Ortağı Merkezi 

**Uygun roller:** Genel yönetici | Yönetici aracısı

İş ortakları, verilen iş ortağı için etkin kenar boşluklarının listesini elde ediyor olabilir. Bu yöntem iş ortağına ve kullanılabilir başlangıç ve bitiş tarihlerine göre kenar boşlukları döndürür. 

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.


## <a name="rest-request"></a>REST isteği
[GET] /v1/margins

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **AL**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/margins HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Hiçbiri

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/margins HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem bir kenar boşlukları listesi döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu gösteren bir HTTP durum kodu ve daha fazla hata ayıklama bilgisi ile birlikte gelir. Bu kodu, hata türünü ve daha fazla parametreyi okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
  "pageSize": 1,
  "totalSize": 2,
  "results": [
    {
      "id": "97620c21cc32_97cdce68-cce4-42aa-9410-233fd0269502",
      "productId": "DZH318Z08L40",
      "publisherName": "Market Place Test",
      "productTitle": "Software As A Service Support Preview App",
      "productType": "SaaS",
      "marginPercentage": 10.0,
      "startDate": "2021-08-04T23:16:22.4736653Z",
      "endDate": "2022-03-31T23:59:59Z",
      "status": "live",
      "statusDate": "2021-08-04T23:16:22.4736653Z"
    },
    {
      "id": "9f342f8c8f59_3be201f5-256d-4488-bd5c-6ffdeb9877ea",
      "productId": "DZH318Z08L40",
      "publisherName": "Market Place Test",
      "productTitle": "Software As A Service Support Preview App",
      "productType": "SaaS",
      "marginPercentage": 1.0,
      "startDate": "2021-08-05T21:44:35.8870924Z",
      "endDate": "2022-03-31T23:59:59Z",
      "status": "live",
      "statusDate": "2021-08-05T21:44:35.8870924Z"
    }
  ]
}
```
