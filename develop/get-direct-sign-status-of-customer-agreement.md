---
title: Microsoft Müşteri Sözleşmesi için müşterinin doğrudan imzalama durumunu alın.
description: DirectSignedCustomerAgreementStatus kaynağını, müşterinin Microsoft Müşteri sözleşmesinin doğrudan imzalama (doğrudan kabul) durumunu almak için kullanabilirsiniz.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 3f1deb20a18bc6e7133cac91db528f2d1ad694e2
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768740"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Müşterinin doğrudan imzalanmasından (doğrudan kabulünün) Microsoft müşteri anlaşması 'nın durumunu alın

**Uygulama hedefi:**

- İş Ortağı Merkezi

**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.

Bu kaynak için *geçerli değildir* :

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, bir müşterinin Microsoft Müşteri Sözleşmesi 'nin doğrudan kabulünün durumunu nasıl alabileceğiniz açıklanmaktadır.

## <a name="rest-request"></a>REST isteği

Müşterinin Microsoft Müşteri sözleşmesinin doğrudan kabulünün durumunu almak için, müşteri için [DirectSignedCustomerAgreementStatus](./customer-agreement-direct-sign-status-resource.md) almak üzere bir rest isteği oluşturun.

### <a name="request-syntax"></a>İstek sözdizimi

Aşağıdaki istek sözdizimini kullanın:

| Yöntem | İstek URI'si                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/directSignedMicrosoftCustomerAgreementStatus http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

İsteğinizle birlikte aşağıdaki URI parametrelerini kullanabilirsiniz:

| Ad             | Tür | Gerekli | Açıklama                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| Müşteri-Kiracı kimliği | GUID | Yes | Değer, bir müşterinin kiracı KIMLIĞINI belirtmenize olanak tanıyan bir GUID biçimli **Customertenantıd** 'dir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir [ **DirectSignedCustomerAgreementStatus** kaynağı](./customer-agreement-direct-sign-status-resource.md) döndürür.

Kaynağın, müşterinin doğrudan imzalama (doğrudan kabul) durumunu gösteren bir **IsSigned** özelliği vardır.

- **Doğru** değeri, sözleşmenin doğrudan müşteri tarafından imzalanmış (kabul edildi) olduğunu gösterir.

- **False** değeri, sözleşmenin doğrudan müşteri tarafından *imzalanmadığını (* kabul edilmediğini) gösterir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
