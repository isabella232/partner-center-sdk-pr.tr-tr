---
title: Microsoft Müşteri Sözleşmesinin müşteri kabulünün onayını alma
description: Bu makalede, Microsoft Müşteri sözleşmesinin müşteri kabulünün nasıl doğrulanacağı açıklanır.
ms.date: 09/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 55f63311e7bb1857fdc6c4b3d68446674542ba98
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769437"
---
# <a name="get-confirmation-of-customer-acceptance-of-microsoft-customer-agreement"></a>Microsoft Müşteri Sözleşmesinin müşteri kabulünün onayını alma

**Uygulama hedefi:**

- İş Ortağı Merkezi

**Sözleşme** kaynağı şu anda yalnızca *Microsoft genel bulutundaki* iş ortağı Merkezi tarafından desteklenmektedir. Bu kaynak için geçerlidir:

- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, bir müşterinin Microsoft Müşteri Sözleşmesi 'nin kabul edilmesine ilişkin onay (ler) i nasıl alabileceğiniz açıklanmaktadır.

## <a name="prerequisites"></a>Önkoşullar

- Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.

- [Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="net"></a>.NET

Daha önce sağlanmış olan müşteri kabulünün onayını almak için:

- Belirtilen müşteri tanımlayıcısıyla **ıaggregatepartner. Customers** koleksiyonunu ve Call **byıd** metodunu kullanın.

- **Byagreementtype** metodunu çağırarak **anlaşmalar** özelliğini getirin ve sonuçları Microsoft Müşteri sözleşmesine filtreleyin.

- **Get** veya **GetAsync** metodunu çağırın.

```csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

string agreementType = "MicrosoftCustomerAgreement";

var customerAgreements = partnerOperations.Customers.ById(selectedCustomerId).Agreements.ByAgreementType(agreementType).Get();
```

Tüm örnek, [konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [getcustomersözleşmeleri](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetCustomerAgreements.cs) sınıfında bulunabilir.

## <a name="rest-request"></a>REST isteği

Daha önce sağlanmış olan müşteri kabulünün onayını almak için:

1. Müşterinin [anlaşmalar](./agreement-resources.md) koleksiyonunu almak IÇIN bir rest isteği oluşturun.

2. Sonuçların kapsamını yalnızca Microsoft Müşteri anlaşmasıyla sınırlamak için **agreementType** sorgu parametresini kullanın.

### <a name="request-syntax"></a>İstek sözdizimi

Aşağıdaki istek sözdizimini kullanın:

| Yöntem | İstek URI'si                                                                                      |
|--------|--------------------------------------------------------------------------------------------------|
| GET    | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/sözleşmeleri? agreementType = {Agreement-Type} http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

İsteğinizle birlikte aşağıdaki URI parametrelerini kullanabilirsiniz:

| Ad             | Tür | Gerekli | Açıklama                                                                               |
|------------------|------|----------|-------------------------------------------------------------------------------------------|
| Müşteri-Kiracı kimliği | GUID | Yes | Değer, bir müşteriyi belirtmenizi sağlayan bir GUID biçimli **Customertenantıd** 'dir. |
| anlaşma türü | dize | No | Bu parametre tüm anlaşma meta verilerini döndürür. Sorgu yanıtının belirli anlaşma türüne kapsamını atamak için bu parametreyi kullanın. Desteklenen değerler şunlardır: <br/><br/> **Microsoftcloudagreement** yalnızca *microsoftcloudagreement* türünün anlaşma meta verilerini içerir.<br/><br/> **Microsoftcustomeragreement** yalnızca *microsoftcustomeragreement* türünde anlaşma meta verilerini içerir.<br/><br/> **\*** Bu, tüm anlaşma meta verilerini döndürür. ( **\*** Kodunuz, beklenmeyen anlaşma türlerini işlemek için gerekli mantığa sahip değilse kullanmayın.)<br/><br/> **Note:** URI parametresi belirtilmemişse, sorgu geri uyumluluk için varsayılan olarak **Microsoftcloudagreement** olur. Microsoft, Sözleşme meta verilerini dilediğiniz zaman yeni anlaşma türleriyle ortaya çıkarabilir.  |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/14876998-c0dc-46e6-9d0c-65a57a6c32ec/agreements?agreementType=MicrosoftCustomerAgreement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde **anlaşma** kaynaklarının bir koleksiyonunu döndürür.

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
    "totalCount": 2,
    "items":
    [
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber":"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-26T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        },
        {
            "primaryContact":
            {
                "firstName":"Tania",
                "lastName":"Carr",
                "email":"SomeEmail@example.com"
                "phoneNumber:"1234567890"
            },
            "templateId":"117a77b0-9360-443b-8795-c6dedc750cf9",
            "dateAgreed":"2019-08-27T00:00:00",
            "type":"MicrosoftCustomerAgreement",
            "agreementLink":"https://aka.ms/customeragreement"
        }
    ]
}
```
