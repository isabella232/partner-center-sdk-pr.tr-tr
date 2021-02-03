---
title: Microsoft Bulut Sözleşmesi için anlaşma meta verilerini alma
description: Bu makalede, Microsoft Bulut sözleşmesi için anlaşma meta verilerinin nasıl alınacağı açıklanmaktadır.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c6a404eb38c4c31d3e69bb598872b932d8985529
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769262"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Microsoft Bulut Sözleşmesi için anlaşma meta verilerini alma

**Uygulama hedefi**

- İş Ortağı Merkezi

> [!NOTE]
> **AgreementMetaData** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir. Şunları yapmak için geçerli değildir:
> - 21Vianet tarafından çalıştırılan iş ortağı Merkezi
> - Microsoft Bulut Almanya için İş Ortağı Merkezi
> - Microsoft Cloud for US Government için İş Ortağı Merkezi

## <a name="prerequisites"></a>Önkoşullar

- Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,9 veya daha yeni bir sürümü gereklidir.

- Iş ortağı merkezi Java SDK 'sını kullanıyorsanız sürüm 1,8 veya daha yeni bir sürümü gereklidir.

- [Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, uygulama + kullanıcı kimlik doğrulamasını destekler.

## <a name="net-version-114-or-newer"></a>.NET (sürüm 1,14 veya üzeri)

Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:

1. İlk olarak, **ıaggregatepartner. AgreementDetails** koleksiyonunu alın.

2. Koleksiyonu Microsoft Bulut sözleşmeye filtrelemek için **Byagreementtype** metodunu çağırın.

3. Son olarak, **Get** veya **GetAsync** yöntemini çağırın.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [Getagreementdetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) sınıfında, bir bütün örnek bulunabilir.

## <a name="net-version-19---113"></a>.NET (sürüm 1,9-1,13)

Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:

Önce **ıaggregatepartner. AgreementDetails** koleksiyonunu alın ve **Get** veya **GetAsync** yöntemlerini çağırın. Ardından, koleksiyon içinde Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:

Önce **ıaggregatepartner. getAgreementDetails** işlevini çağırın ve sonra **Get** işlevini çağırın. Ardından, koleksiyon içinde Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın:

```java
// IAggregatePartner partnerOperations;

ResourceCollection<AgreementMetaData> agreements = partnerOperations.getAgreements().get();

AgreementMetaData microsoftCloudAgreement;

for (AgreementMetaData metadata : agreements)
{
    if(metadata.getAgreementType() == AgreementType.MicrosoftCloudAgreement)
    {
        microsoftCloudAgreement = metadata;
    }
}
```

[Konsol test uygulaması](https://github.com/Microsoft/Partner-Center-Java-Samples) projesinden [Getagreementdetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) sınıfında, bir bütün örnek bulunabilir.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için:

[**Get-PartnerAgreementDetail**](/powershell/module/partnercenter/get-partneragreementdetail) komutunu kullanın. Ardından, koleksiyon içinde Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>REST isteği

Microsoft Bulut sözleşmesinin anlaşma meta verilerini almak için, önce **AgreementMetaData** koleksiyonunu almak üzere bir rest isteği oluşturun. Sonra koleksiyonda Microsoft Bulut sözleşmeye karşılık gelen öğeyi arayın.

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/SÖZLEŞMELERI http/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/agreements HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde bir **AgreementMetaData** kaynakları koleksiyonu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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
            "templateId": "998b88de-aa99-4388-a42c-1b3517d49490",
            "agreementType": "MicrosoftCloudAgreement",
            "agreementLink": "https://docs.microsoft.com/partner-center/agreements",
            "versionRank": 0
        }
    ],
    "links": {
        "self": {
            "uri": "/agreements",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

Microsoft Bulut sözleşmesine karşılık gelen yanıttaki kaynağı tanımlamak için, **agreementType** özelliği "MicrosoftCloudAgreement" değerine sahip olan kaynağı arayın.
