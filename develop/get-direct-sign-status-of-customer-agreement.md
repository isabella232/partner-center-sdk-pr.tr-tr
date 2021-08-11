---
title: Oturum açma için müşterinin doğrudan imzalama durumunu Microsoft Müşteri Sözleşmesi.
description: DirectSignedCustomerAgreementStatus kaynağını kullanarak müşterinin doğrudan imzalama (doğrudan kabul) durumunu Microsoft Müşteri Sözleşmesi.
ms.date: 02/11/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 544965ab05e3956aa5b7b6fa2ef9656ff33990ef9c8d91422797132a814b85f1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993359"
---
# <a name="get-the-status-of-a-customers-direct-signing-direct-acceptance-of-microsoft-customer-agreement"></a>Müşterinin doğrudan imzalama (doğrudan kabul) durumunu Microsoft Müşteri Sözleşmesi

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

**DirectSignedCustomerAgreementStatus** kaynağı şu anda yalnızca Microsoft genel İş Ortağı Merkezi kaynak tarafından de desteklene bir kaynaktır.

Bu makalede, bir müşterinin doğrudan kabul durumunu nasıl ala bir Microsoft Müşteri Sözleşmesi.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="c"></a>C\#

Müşterinin doğrudan Microsoft Müşteri Sözleşmesi kabul durumunu almak için müşteri tanımlayıcısıyla [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini arayın. Ardından [**Agreements özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.agreements) kullanarak [**ICustomerAgreementCollection arabirimini**](/dotnet/api/microsoft.store.partnercenter.agreements.icustomeragreementcollection) alın. Son olarak, durumu `GetDirectSignedCustomerAgreementStatus()` almak `GetDirectSignedCustomerAgreementStatusAsync()` için veya çağrısı.

``` csharp
// IAggregatePartner partnerOperations;
// string customerId;
var customerDirectSigningStatus = partnerOperations.Customers.ById(selectedCustomerId).Agreements.GetDirectSignedCustomerAgreementStatus();
```

**Örnek:** [Konsol Örnek Uygulaması](https://github.com/microsoft/Partner-Center-DotNet-Samples). **Project:** SdkSamples **Sınıfı**: GetDirectSignedCustomerAgreementStatus.cs

## <a name="rest-request"></a>REST isteği

Müşterinin doğrudan kabul durumunu almak için Microsoft Müşteri Sözleşmesi için [DirectSignedCustomerAgreementStatus'u](./customer-agreement-direct-sign-status-resource.md) almak için bir REST isteği oluşturun.

### <a name="request-syntax"></a>İstek söz dizimi

Aşağıdaki istek söz dizimlerini kullanın:

| Yöntem | İstek URI'si                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directSignedMicrosoftCustomerAgreementStatus HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

İsteğiniz ile aşağıdaki URI parametrelerini kullanabilirsiniz:

| Ad             | Tür | Gerekli | Açıklama                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| customer-tenant-id | GUID | Yes | Değer, bir müşterinin kiracı kimliğini belirtmenize olanak sağlayan GUID biçimli bir **CustomerTenantId** değeridir. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, bu yöntem yanıt [ **gövdesinde bir DirectSignedCustomerAgreementStatus**](./customer-agreement-direct-sign-status-resource.md) kaynağı döndürür.

Kaynağın, müşterinin doğrudan imzalama (doğrudan kabul) durumunu belirten bir **isSigned** özelliği vardır.

- true **değeri,** sözleşmenin doğrudan müşteri tarafından imzalandı (kabul edildi) olduğunu gösterir.

- false **değeri,** sözleşmenin doğrudan müşteri *tarafından* imzalanmaz (kabul edilir) olduğunu gösterir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 20
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b

{"isSigned":true}
```
