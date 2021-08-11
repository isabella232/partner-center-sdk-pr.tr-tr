---
title: Microsoft Bulut Sözleşmesi için anlaşma meta verilerini alma
description: Bu makalede, veri kaynağı için sözleşme meta verilerini Microsoft Bulut Anlaşması.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 55a09752844f74caaf878f1e2dcfe3d8a70a283c5e0e9daefba89c558405690a
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994124"
---
# <a name="get-agreement-metadata-for-microsoft-cloud-agreement"></a>Microsoft Bulut Sözleşmesi için anlaşma meta verilerini alma

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

**AgreementMetaData** kaynağı şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde destekleneblir.

## <a name="prerequisites"></a>Önkoşullar

- İş Ortağı Merkezi .NET SDK kullanıyorsanız sürüm 1.9 veya daha yenisi gereklidir.

- İş Ortağı Merkezi Java SDK'sı kullanıyorsanız sürüm 1.8 veya daha yeni bir sürüm gereklidir.

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](./partner-center-authentication.md) Bu senaryo uygulama + kullanıcı kimlik doğrulamasını destekler.

## <a name="net-version-114-or-newer"></a>.NET (sürüm 1.14 veya daha yenisi)

Aşağıdakiler için sözleşme meta verilerini Microsoft Bulut Anlaşması:

1. İlk olarak **IAggregatePartner.AgreementDetails koleksiyonunu** alın.

2. Koleksiyonda **veri filtrelemek için ByAgreementType** yöntemini Microsoft Bulut Anlaşması.

3. Son olarak **Get veya** **GetAsync yöntemini** arayın.

```csharp
// IAggregatePartner partnerOperations;

string agreementType = "MicrosoftCloudAgreement";

var microsoftCloudAgreementDetails = partnerOperations.AgreementDetails.ByAgreementType(agreementType).Get().Items.Single();
```

Eksiksiz bir örnek, konsol test uygulaması [projesinden GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) [sınıfında](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) bulunabilir.

## <a name="net-version-19---113"></a>.NET (sürüm 1.9 - 1.13)

Aşağıdakiler için sözleşme meta verilerini Microsoft Bulut Anlaşması:

İlk olarak **IAggregatePartner.AgreementDetails** koleksiyonunu alın ve ardından **Get** veya **GetAsync** yöntemlerini çağırın. Ardından koleksiyon içindeki öğe için arama Microsoft Bulut Anlaşması:

```csharp
// IAggregatePartner partnerOperations;

var agreements = partnerOperations.AgreementDetails.Get();

AgreementMetaData microsoftCloudAgreement = agreements.Items.FirstOrDefault (agr => agr.AgreementType == AgreementType.MicrosoftCloudAgreement);
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Aşağıdakiler için sözleşme meta verilerini Microsoft Bulut Anlaşması:

İlk olarak **IAggregatePartner.getAgreementDetails** işlevini ve ardından **get işlevini** çağırma. Ardından koleksiyon içindeki öğe için arama Microsoft Bulut Anlaşması:

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

Eksiksiz bir örnek, konsol test uygulaması [projesinden GetAgreementDetails](https://github.com/microsoft/Partner-Center-Java-Samples/blob/master/sdk/src/main/java/com/microsoft/store/partnercenter/samples/agreements/GetAgreementDetails.java) [sınıfında](https://github.com/Microsoft/Partner-Center-Java-Samples) bulunabilir.

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Aşağıdakiler için sözleşme meta verilerini Microsoft Bulut Anlaşması:

[**Get-PartnerAgreementDetail komutunu**](/powershell/module/partnercenter/get-partneragreementdetail) kullanın. Ardından koleksiyon içindeki öğe için arama Microsoft Bulut Anlaşması:

```powershell
Get-PartnerAgreementDetail | Where-Object {$_.AgreementType -eq 'MicrosoftCloudAgreement'} | Select-Object -First 1
```

## <a name="rest-request"></a>REST isteği

Bu verilerin sözleşme meta verilerini Microsoft Bulut Anlaşması önce **AgreementMetaData** koleksiyonunu almak için bir REST İsteği oluşturun. Ardından koleksiyonda, veri türüne karşılık gelen öğeyi Microsoft Bulut Anlaşması.

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si                                                         |
|--------|---------------------------------------------------------------------|
| GET    | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreements HTTP/1.1 |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, bu yöntem yanıt gövdesinde **AgreementMetaData** kaynaklarının bir koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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

Yanıtta, söz konusu kaynağa karşılık gelen kaynağı Microsoft Bulut Anlaşması **agreementType** özelliği "MicrosoftCloudAgreement" değerine sahip olan kaynağı seçin.
