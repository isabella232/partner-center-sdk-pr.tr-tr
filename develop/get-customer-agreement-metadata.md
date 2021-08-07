---
title: Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma
description: Bu makalede, veri kaynağı için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi.
ms.date: 8/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khakiali
ms.author: alikhaki
ms.openlocfilehash: 384fa227a103ed10dc2fd055afa7688d3b2a418504360eb4a5025615cf2a4f67
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989364"
---
# <a name="get-agreement-metadata-for-the-microsoft-customer-agreement"></a>Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alma

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

İş yüklerini Microsoft Müşteri Sözleşmesi meta verileri şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde desteklene bir hizmettir.

Şunların için önce Microsoft Müşteri Sözleşmesi meta verilerini alasiniz:

- [Müşterinin Microsoft Müşteri Sözleşmesi](./confirm-customer-consent-customer-agreement.md)
- [Microsoft Müşteri Sözleşmesi şablonu için indirme bağlantısı alma](./download-customer-agreement-template.md)

## <a name="prerequisites"></a>Önkoşullar

- İş Ortağı Merkezi .NET SDK kullanıyorsanız sürüm 1.14 veya daha yenisi gereklidir.

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](./partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik doğrulamasını destekler.

## <a name="net-version-114-or-newer"></a>.NET (sürüm 1.14 veya daha yenisi)

Aşağıdakiler için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi:

1. İlk olarak **IAggregatePartner.AgreementDetails koleksiyonunu** alın.

2. Koleksiyona filtre uygulama filtresi yapmak için **ByAgreementType** yöntemini Microsoft Müşteri Sözleşmesi.

3. Son olarak **Get veya** **GetAsync yöntemini** arayın.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCustomerAgreement";

var microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Eksiksiz bir örnek, konsol test uygulaması [projesinden GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) [sınıfında](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) bulunabilir.

## <a name="rest-request"></a>REST isteği

Aşağıdakiler için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi:

1. [AgreementMetaData](./agreement-metadata-resources.md) koleksiyonunu almak için bir REST isteği oluşturun.

2. AgreementType **sorgu** parametresini kullanarak sonucun kapsamını yalnızca Microsoft Müşteri Sözleşmesi.

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements?agreementType={agreement-type} HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

| Ad                   | Tür     | Gerekli | Açıklama                                                             |
|------------------------|----------|----------|-------------------------------------------------------------------------|
| sözleşme türü | dize | No | Sorgu yanıtını belirli sözleşme türüne göre kapsam olarak kullanmak için bu parametreyi kullanın. Desteklenen değerler: <br/><br/>**Yalnızca MicrosoftCloudAgreement** türünde sözleşme meta verilerini içeren *MicrosoftCloudAgreement*<br/><br/>**Yalnızca MicrosoftCustomerAgreement** türünde sözleşme meta verilerini içeren *MicrosoftCustomerAgreement*.<br/><br/>**\**_ tüm sözleşme meta verilerini döndürür. (_ kullanma* \* _ Microsoft herhangi bir zamanda yeni sözleşme türleriyle sözleşme meta verilerine sahip olabilir, çünkü kodunuzun yabancı anlaşma türlerini işlemek için gerekli çalışma zamanı mantığı *yoksa.) <br/> <br/> _* Not:** URI parametresi belirtilmezse, geriye dönük uyumluluk için sorgu **varsayılan olarak MicrosoftCloudAgreement** olur.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, bu yöntem yanıt gövdesinde [ **AgreementMetaData** kaynaklarının](./agreement-metadata-resources.md) bir koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
