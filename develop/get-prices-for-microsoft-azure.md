---
title: Microsoft Azure için fiyat alma
description: Bir Azure teklifinin gerçek zamanlı fiyatlarıyla Azure Rate Card'a nasıl sahip oluruz? Azure fiyatlandırması oldukça dinamiktir ve sık sık değişir.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8b69e9e3d8e6e4c4e447b308c890c4c054e6a1e5221bb523a5caca041d1ea115
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115989126"
---
# <a name="get-prices-for-microsoft-azure"></a>Microsoft Azure için fiyat alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bir Azure [teklifinin gerçek zamanlı](azure-rate-card-resources.md) fiyatlarıyla Azure Rate Card'a nasıl sahip oluruz? Azure fiyatlandırması oldukça dinamiktir ve sık sık değişir.

Kullanımı izlemek ve bireysel müşterilerin aylık faturanızı ve faturalarını tahmin etmeye yardımcı olmak için bu Azure Rate Card sorgusunu birleştirebilir ve Microsoft Azure için fiyatları almak için Azure için müşterinin kullanım kayıtlarını al isteği [gönderebilirsiniz.](get-a-customer-s-utilization-record-for-azure.md)

Fiyatlar pazara ve para birimine göre farklılık gösterir ve bu API konumu dikkate alır. Varsayılan olarak API, İş Ortağı Merkezi ve tarayıcınızın dilinde iş ortağı profili ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir. Konum tanıma, özellikle de birden çok pazarda satışları tek, merkezi bir ofisten yönetirken oldukça alakalıdır. Daha fazla bilgi için [bkz. URI parametreleri.](#uri-parameters)

## <a name="c"></a>C\#

Azure Rate Card'ı almak için [**IAzureRateCard.Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) yöntemini çağırarak Azure fiyatlarını içeren [**bir AzureRateCard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) kaynağı bulun.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Örnek:** [Konsol test uygulaması](console-test-app.md). **Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** GetAzureRateCard.cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Azure Rate Card'ı almak için **IAzureRateCard.get** işlevini çağırarak Azure fiyatlarını içeren fiyat kartı ayrıntılarını iade edin.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Azure Kartını almak için, Azure fiyatlarını içeren fiyat kartı ayrıntılarını iade etmek için [**Get-PartnerAzureRateCard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) komutunu yürütün.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si                                                        |
|---------|--------------------------------------------------------------------|
| **Al** | *{baseURL}*/v1/ratecards/azure?currency={currency}&region={region} |

### <a name="uri-parameters"></a>URI parametreleri

| Ad     | Tür   | Gerekli | Açıklama                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | dize | No       | Kaynak oranlarının sağlanacak para birimi için isteğe bağlı üç harfli ISO kodu `EUR` (örneğin). Varsayılan değer: `USD`. |
| region   | dize | No       | Isteğe bağlı iki harfli ISO ülke/bölge kodu, teklifin satın alınarak pazar olduğunu gösterir `FR` (örneğin). Varsayılan değer: `US`.        |

İsteğe bağlı X-Locale üst bilgilerini [isteğinize](headers.md#rest-request-headers) dahilebilirsiniz. X-Locale üst bilgisi dahil değil, varsayılan değer ("en-US") kullanılır.

- İsteğinize para birimi ve bölge parametreleri sağlarsanız yanıtın dilini belirlemek için X-Locale değeri kullanılır.

- İsteğinize bölge ve para birimi parametreleri sağlanmıyorsa yanıtın bölgesi, para birimi ve dili belirlemek için X-Locale değeri kullanılır.

### <a name="request-header"></a>İstek üst bilgisi

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/ratecards/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 07ced227-3f32-4eeb-8062-f0bef849a9bc
MS-CorrelationId: a687bc47-8d08-4b78-aff6-5a59aa2055c2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

İstek başarılı olursa bir Azure Rate [Card kaynağı](azure-rate-card-resources.md) döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

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
    "locale": "en",
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
