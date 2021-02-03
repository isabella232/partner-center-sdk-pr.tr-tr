---
title: Microsoft Azure İş Ortağı Paylaşılan Hizmetleri için fiyat alma
description: Microsoft Azure Iş ortağı paylaşılan hizmetleri fiyatlarına sahip bir Azure ücret kartı alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: cd396c35b6b89de4d0f092ba4da738a2ed0ac633
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769905"
---
# <a name="get-prices-for-microsoft-azure-partner-shared-services"></a>Microsoft Azure İş Ortağı Paylaşılan Hizmetleri için fiyat alma

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Microsoft Azure Iş ortağı paylaşılan hizmetleri fiyatlarına sahip bir [Azure ücret kartı](azure-rate-card-resources.md) alma.

Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun. Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir. Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir.

## <a name="example-code"></a>Örnek kod

## <a name="c"></a>C\#

Azure fiyat kartını edinmek için, Azure fiyatlarını içeren bir [**Azursilinebilir tecard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) kaynağı döndürmek üzere [**ıazursilinebilir Tecard. getshared**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.getshared) metodunu çağırın.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.GetShared();
```

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Azure fiyat kartını edinmek için, Azure fiyatlarını içeren hız kartı ayrıntılarını döndürmek üzere **ıazursilinebilir Tecard. getShared** işlevini çağırın.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().getShared();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Azure kartını almak için [**Get-Partnerazursilinebilir Tecard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) komutunu yürütün ve Azure fiyatlarını içeren hız kartı ayrıntılarını döndürmek Için **SharedServices** parametresini belirtin.

```powershell
Get-PartnerAzureRateCard -SharedServices
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                               |
|---------|---------------------------------------------------------------------------|
| **Al** | *{BaseUrl}*/v1/ratecards/Azure-Shared? para birimi = {currency} &bölgesi = {Region} |

### <a name="uri-parameters"></a>URI parametreleri

| Ad     | Tür   | Gerekli | Açıklama                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | dize | No       | Kaynak tarifelerinin sağlandığı para birimi için isteğe bağlı üç harfli ISO kodu (örneğin `EUR` ). Varsayılan değer, iş ortağı profilindeki Pazar ile ilişkili para birimidir. |
| region   | dize | No       | Teklifin satın alındığı pazarı belirten, isteğe bağlı iki harfli ISO ülke/bölge kodu (örneğin `FR` ). Varsayılan değer, iş ortağı profilinde ayarlanan ülke/bölge kodudur.        |

İsteğe bağlı X-locale üstbilgisi isteğe dahil ise, bu değer yanıttaki Ayrıntılar için kullanılan dili belirler.

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure-shared HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

İstek başarılı olursa, bir [Azure ücret kartı](azure-rate-card-resources.md) kaynağı döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1545508
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57b25659-fc00-4215-87e7-2b09bac6845d
MS-RequestId: 870118d0-adbb-41a3-82d2-a3d45ade3c73
MS-CV: CYBB8PXMsEukJBIn.0
MS-ServerId: 201021413
Date: Wed, 01 Feb 2017 00:13:45 GMT

{
    "locale": "en-US",
    "currency": "USD",
    "isTaxIncluded": false,
    "meters": [{
            "id": "4b836326-7e19-46e6-8bce-1b19bb6cd91e",
            "name": "Unlimited Data - 1 Gbps",
            "rates": {
                "0": 7395.0
            },
            "tags": [],
            "category": "Networking",
            "subcategory": "ExpressRoute",
            "region": "Zone 2",
            "unit": "Connections",
            "includedQuantity": 0.0,
            "effectiveDate": "2015-09-01T00:00:00Z"
        }, {
            "id": "1e8f6d9f-8b40-4c97-80cc-cff87a290a93",
            "name": "Compute Hours",
            "rates": {
                "0": 3.9729
            },
            "tags": [],
            "category": "Cloud Services",
            "subcategory": "Standard_L16 Cloud Services",
            "region": "AU East",
            "unit": "1 Hour",
            "includedQuantity": 0.0,
            "effectiveDate": "2016-09-01T00:00:00Z"
        }, {
            "id": "7a2639ce-ae47-4413-9837-6b4f4b78be3d",
            "name": "Compute Hours",
            "rates": {
                "0": 0.1122
            },
            "tags": [],
            "category": "Virtual Machines",
            "subcategory": "Standard_D1_v2 VM (Windows)",
            "region": "BR South",
            "unit": "Hours",
            "includedQuantity": 0.0,
            "effectiveDate": "2017-01-01T00:00:00Z"
        }
    ],
    "offerTerms": [{
            "name": "Overage discount",
            "discount": 0.15,
            "excludedMeterIds": ["53cc0061-0fe2-4249-bf62-e1008c811f5c", "c82dbd27-c978-43a7-ad41-525a90d8962b"],
            "effectiveDate": "2014-01-01T00:00:00"
        }
    ],
    "attributes": {
        "objectType": "AzureRateCard"
    }
}
```
