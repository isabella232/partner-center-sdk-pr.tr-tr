---
title: Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma
description: Bu makalede, Microsoft Müşteri Sözleşmesi için anlaşma meta verilerinin nasıl alınacağı açıklanmaktadır.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: c3ebecc51859c9d2240d319d823f7e555eaecc27
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769431"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma

**Uygulama hedefi:**

- İş Ortağı Merkezi

Microsoft Müşteri Sözleşmesi için anlaşma meta verileri şu anda yalnızca *Microsoft genel bulutundaki* Iş Ortağı Merkezi tarafından desteklenmektedir. Şunları yapmak için geçerlidir:

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Aşağıdakileri yapabilmeniz için Microsoft Müşteri Sözleşmesi 'nin anlaşma meta verilerini almalısınız:

- [Müşterinin Microsoft Müşteri sözleşmesinin kabul edildiğini onaylama](./confirm-customer-consent-customer-agreement.md)
- [Microsoft müşteri anlaşması şablonu için bir indirme bağlantısı alma](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Önkoşullar

- Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.

- [Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.

## <a name="net-version-114-or-newer"></a>.NET (sürüm 1,14 veya üzeri)

Microsoft Müşteri Sözleşmesi sözleşmesi meta verilerini almak için:

1. İlk olarak, **ıaggregatepartner. AgreementDetails** koleksiyonunu alın.

2. Koleksiyonu Microsoft Müşteri anlaşmasıyla filtrelemek için **Byagreementtype** metodunu çağırın.

3. Son olarak, **Get** veya **GetAsync** yöntemini çağırın.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [Getagreementdetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) sınıfında, bir bütün örnek bulunabilir.

## <a name="rest-request"></a>REST isteği

Microsoft Müşteri Sözleşmesi sözleşmesi meta verilerini almak için:

1. [AgreementMetaData](./agreement-metadata-resources.md) koleksiyonunu almak IÇIN bir rest isteği oluşturun.

2. Sonucu yalnızca Microsoft Müşteri anlaşmasıyla sınırlamak için **agreementType** sorgu parametresini kullanın.

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/sözleşmeleri? agreementType = {Agreement-Type} http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

| Ad                   | Tür     | Gerekli | Açıklama                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| anlaşma türü | dize | No | Sorgu yanıtının belirli anlaşma türüne kapsamını atamak için bu parametreyi kullanın. Desteklenen değerler şunlardır: <br/><br/>Yalnızca *microsoftcloudagreement* türünde Sözleşme meta verilerini Içeren **Microsoftcloufegreement**<br/><br/>Yalnızca *microsoftcustomeragreement* türünde Sözleşme meta verilerini Içeren **microsoftcustomeragreement** .<br/><br/>**\*** Bu, tüm anlaşma meta verilerini döndürür. (Microsoft, **\*** herhangi bir zamanda yeni anlaşma türleriyle anlaşma meta verileri getirebileceğinden, kodunuzun tanıdık anlaşma türlerini işlemek için gerekli çalışma zamanı mantığına sahip olmadığı yapmayın.)<br/><br/> **Note:** URI parametresi belirtilmemişse, sorgu geri uyumluluk için varsayılan olarak **Microsoftcloudagreement** olur.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir [ **AgreementMetaData** kaynakları](./agreement-metadata-resources.md) koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "totalCount": 1,
    "items": [
        {
            "templateId": "117a77b0-9360-443b-8795-c6dedc750cf9",
            "agreementType": "MicrosoftCustomerAgreement",
            "agreementLink": "https://aka.ms/customeragreement",
            "versionRank": 0
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
