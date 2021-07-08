---
title: Microsoft Azure için fiyat alma
description: Azure teklifi için gerçek zamanlı fiyatlara sahip bir Azure ücret kartı alma. Azure fiyatlandırması oldukça dinamik ve sık sık değişir.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4f66ab19ef3723fbaa27acff941cf48683a7c25c
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548796"
---
# <a name="get-prices-for-microsoft-azure"></a>Microsoft Azure için fiyat alma

**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Azure teklifi için gerçek zamanlı fiyatlara sahip bir [Azure ücret kartı](azure-rate-card-resources.md) alma. Azure fiyatlandırması oldukça dinamik ve sık sık değişir.

kullanımı izlemek ve aylık faturanızı ve tek tek müşterilerin ücretini tahmin etmeye yardımcı olmak için, [azure için bir müşterinin kullanım kayıtlarını almaya](get-a-customer-s-utilization-record-for-azure.md)yönelik bir istekle Microsoft Azure fiyatlarını almak üzere bu Azure fiyatı kartı sorgusunu birleştirebilirsiniz.

Fiyatlar Pazar ve para birimine göre farklılık gösterir ve bu API 'nin yerini göz önünde bulundurun. Varsayılan olarak, API iş ortağı merkezi ve tarayıcı dilinizde ortak profil ayarlarınızı kullanır ve bu ayarlar özelleştirilebilir. Bu durum, özellikle birden çok pazardaki satışları tek bir merkezi bir ofiste yönetiyorsanız ilgilidir. Daha fazla bilgi için bkz. [URI parametreleri](#uri-parameters).

## <a name="c"></a>C\#

Azure fiyat kartını edinmek için, Azure fiyatlarını içeren [**Azursilinebilir tecard**](/dotnet/api/microsoft.store.partnercenter.models.ratecards.azureratecard) kaynağını döndürmek üzere [**ıazursilinebilir Tecard. Get**](/dotnet/api/microsoft.store.partnercenter.ratecards.iazureratecard.get) yöntemini çağırın.

```csharp
// IAggregatePartner partnerOperations;

var azureRateCard = partner.RateCards.Azure.Get();
```

**Örnek**: [konsol test uygulaması](console-test-app.md). **Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: GetAzureRateCard. cs

## <a name="java"></a>Java

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

Azure fiyat kartını edinmek için **ıazursilinebilir Tecard. Get** Işlevini çağırıp Azure fiyatlarını içeren ücret kartı ayrıntılarını döndürün.

```java
// IAggregatePartner partnerOperations;

AzureRateCard azureRateCard = partner.getRateCards().getAzure().get();
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Azure kartını almak için [**Get-Partnerazursilinebilir Tecard**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerAzureRateCard.md) komutunu çalıştırarak Azure fiyatlarını içeren ücret kartı ayrıntılarını döndürün.

```powershell
Get-PartnerAzureRateCard
```

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                        |
|---------|--------------------------------------------------------------------|
| **Al** | *{BaseUrl}*/v1/ratecards/Azure? para birimi = {currency} &bölgesi = {Region} |

### <a name="uri-parameters"></a>URI parametreleri

| Ad     | Tür   | Gerekli | Açıklama                                                                                                                                                                               |
|----------|--------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| currency | dize | No       | Kaynak tarifelerinin sağlandığı para birimi için isteğe bağlı üç harfli ISO kodu (örneğin `EUR` ). Varsayılan değer: `USD`. |
| region   | dize | No       | Teklifin satın alındığı pazarı belirten, isteğe bağlı iki harfli ISO ülke/bölge kodu (örneğin `FR` ). Varsayılan değer: `US`.        |

İsteğe bağlı X-locale [üst bilgisini](headers.md#rest-request-headers) isteğinize dahil edebilirsiniz. X-locale üst bilgisini eklemezseniz, varsayılan değer ("en-US") kullanılır.

- İsteğiniz için para birimi ve bölge parametreleri sağlarsanız, yanıtın dilini belirlemekte X-locale değeri kullanılır.

- İsteğiniz içinde bölge ve para birimi parametreleri sağlamazsanız, yanıtın bölge, para birimi ve dilini belirlemekte X-locale değeri kullanılır.

### <a name="request-header"></a>İstek üst bilgisi

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

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
