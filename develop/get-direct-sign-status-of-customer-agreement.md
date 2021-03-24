---
title: Microsoft Müşteri Sözleşmesi için müşterinin doğrudan imzalama durumunu alın.
description: DirectSignedCustomerAgreementStatus kaynağını, müşterinin Microsoft Müşteri sözleşmesinin doğrudan imzalama (doğrudan kabul) durumunu almak için kullanabilirsiniz.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 267e3aa63a94c5045977ad566eb5061df3b59882
ms.sourcegitcommit: bbdb5f7c9ddd42c2fc4eaadbb67d61aeeae805ca
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/24/2021
ms.locfileid: "105030581"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Müşterinin doğrudan imzalanmasından (doğrudan kabulünün) Microsoft müşteri anlaşması 'nın durumunu alın

**Uygulama hedefi:**

- İş Ortağı Merkezi

**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.

Bu kaynak için *geçerli değildir* :

- 21Vianet tarafından çalıştırılan İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, bir müşterinin Microsoft Müşteri Sözleşmesi 'nin doğrudan kabulünün durumunu nasıl alabileceğiniz açıklanmaktadır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="c"></a>C\#

Müşterinin Microsoft Müşteri sözleşmesinin doğrudan kabulünün durumunu almak için, müşteri tanımlayıcısıyla [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın. Ardından [**ICustomerAgreementCollection**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) arabirimini almak için [**anlaşmalar**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) özelliğini kullanın. Son olarak, `GetDirectSignedCustomerAgreementStatus()` `GetDirectSignedCustomerAgreementStatusAsync()` durumu almak için veya çağırın.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Örnek**: [konsol örnek uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Proje**: Sdksamples **sınıfı**: GetDirectSignedCustomerAgreementStatus. cs

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
