---
title: ortağın Government Community Cloud doğrulama kodlarını al
description: iş ortağının Government Community Cloud doğrulama kodlarını alma.
ms.date: 11/08/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 04bccf587628337004a5825b534048945f791839
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111873879"
---
# <a name="get-a-partners-validation-codes"></a>İş ortağının doğrulama kodlarını alma

bu makalede bir iş ortağının Government Community Cloud doğrulama kodları koleksiyonunu nasıl alacağınız açıklanır. Kamu topluluk bulutu 'nda bir müşteri oluşturmak için bir doğrulama kodu gerekir.

kuruluşunuzun veya müşterinin kuruluşunun CSP için Office 365 Kamu GCC onaylanmasından ilgileniyorsanız, bkz. [csp iş ortağı ve müşteri uygunluk ölçütlerine yönelik Office 365 Kamu GCC](/partner-center/csp-gcc-validate).

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Form doldurulduktan sonra doğrulama onaylandı [](https://products.office.com/government/eligibility-validation?ReqType=CSPPartner).

- Nitelikleri olmayan bir müşteri.

## <a name="c"></a>C\#

Bir iş ortağının doğrulama kodlarının tümünün listesini almak için **Getvalidationcodes**' ı çağırın.

``` csharp
// create the partner operations
IAggregatePartner partnerOperations = PartnerService.Instance.CreatePartnerOperations(credentials);

var gccValidations = partnerOperations.Validations.GetValidationCodes();
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                          |
|---------|------------------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/All/doğrulamaları http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/all/validations HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde [**Validationcode**](utility-resources.md#validationcode) kaynaklarının bir listesini döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 434
Content-Type: application/json
MS-CorrelationId: 283b9b70-963a-4159-9920-f2bdf7ab7fce
MS-RequestId: 7266f5f6-30ca-4672-9eb6-6c9d6dd0e9d3

[
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc.",
    "validationId": "12345",
    "maxCreates": 5,
    "remainingCreates": 4,
    "eTag": "W/\"datetime'2018-10-10T18%3A49%3A58.727348Z'\""
  },
  {
    "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d",
    "organizationName": "Contoso, Inc. Finance Department",
    "validationId": "987654",
    "maxCreates": 5,
    "remainingCreates": 5,
    "eTag": "W/\"datetime'2018-10-19T17%3A51%3A45.6584512Z'\""
  }
]
```
