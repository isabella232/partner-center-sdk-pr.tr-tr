---
title: Ürünlerin bir listesini alma (müşteriye göre)
description: Müşterinin bir ürün koleksiyonunu almak için bir müşteri tanımlayıcısı kullanabilirsiniz.
ms.assetid: ''
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: a7cb2430aa93beb89e4d1f9b8c89a016d66624ca
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874202"
---
# <a name="get-a-list-of-products-by-customer"></a>Ürünlerin bir listesini alma (müşteriye göre)

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Mevcut bir müşteriye yönelik ürünlerin bir koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si                                                                                                              |
|--------|--------------------------------------------------------------------------------------------------------------------------|
| POST   | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Products? targetView = {targetview} http/1.1 |

#### <a name="request-uri-parameters"></a>İstek URI parametreleri

| Ad               | Tür | Gerekli | Açıklama                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| **Müşteri-Kiracı kimliği** | GUID | Yes | Değer, bir müşteriyi belirtmenize olanak tanıyan bir tanımlayıcı olan GUID biçimli bir **Müşteri-kiracı kimliğidir**. |
| **targetView** | string | Yes | Kataloğun hedef görünümünü tanımlar. Desteklenen değerler şunlardır: <br/><br/>Tüm Azure öğelerini içeren **Azure**<br/><br/>Tüm Azure ayırma öğelerini içeren **Azurereservations**<br/><br/>Tüm sanal makine (VM) rezervasyon öğelerini içeren **Azurereservationsvm**<br/><br/>tüm SQL ayırma öğelerini içeren **azurereservationssql**<br/><br/>tüm Cosmos veritabanı ayırma öğelerini içeren **azurereservationscosmosdb**<br/><br/>Microsoft Azure aboneliklerine (**MS-azr-0145p**) ve Azure planlarına yönelik öğeler içeren **MicrosoftAzure**<br/><br/>Ticari Market ürünleri dahil tüm çevrimiçi hizmet öğelerini içeren **OnlineServices**<br/><br/>Tüm yazılım öğelerini içeren **yazılım**<br/><br/>Tüm yazılım SUSE Linux öğelerini içeren **SoftwareSUSELinux**<br/><br/>Tüm kalıcı yazılım öğelerini içeren **Softwarekalıcı**<br/><br/>Tüm yazılım aboneliği öğelerini içeren **SoftwareSubscriptions**  |

### <a name="request-header"></a>İstek üst bilgisi

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

Belirli bir müşteri tarafından kullanılabilen Azure kullanım tabanlı ürünlerin bir listesini isteyin. yalnızca Microsoft Azure (MS-azr-0145p) ve Azure planlarına yönelik ürünler, genel buluttaki müşteriler için döndürülür:

```http
GET https://api.partnercenter.microsoft.com/v1/customers/65543400-f8b0-4783-8530-6d35ab8c6801/products?targetView=MicrosoftAzure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 83643f5e-5dfd-4375-88ed-054412460dc8
MS-CorrelationId: b1939cb2-e83d-4fb0-989f-514fb741b734
```

## <a name="rest-response"></a>Rest yanıtı

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Partner Center hata kodları](error-codes.md).

Bu yöntem aşağıdaki hata kodlarını döndürür:

| HTTP durum kodu | Hata kodu   | Açıklama                     |
|------------------|--------------|---------------------------------|
| 403 | 400036 | İstenen targetView 'a erişime izin verilmiyor. |

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1909
Content-Type: application/json; charset=utf-8
MS-CorrelationId: cad955c2-8efc-47fe-b112-548ff002ba18
MS-RequestId: ae7288e2-2673-4ad4-8c12-7aad818d5949

{
    "totalCount": 2,
    "items": [
        {
            "id": "MS-AZR-0145P",
            "productId": "9DEA7946-EC2C-441E-9FFD-E3B275F7E838",
            "title": "Microsoft Azure",
            "description": "Azure Cloud Solution Provider offer for Partner and Resellers",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "monthly"
            ],
            "purchasePrerequisites": [
                "MicrosoftCloudAgreement"
            ],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "billingType": "usage",
                "category": "Enterprise",
                "isAddon": false,
                "prerequisiteSkus": [],
                "rank": 1413,
                "hasAddOns": false,
                "isAutoRenewable": false,
                "upgradeTargetOffers": null,
                "conversionTargetOffers": [],
                "unitType": "Usage-based",
                "limitUnitOfMeasure": "None",
                "limit": 0,
                "reselleeQualifications": [],
                "resellerQualifications": []
            },
            "links": {
                "availabilities": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/9DEA7946-EC2C-441E-9FFD-E3B275F7E838/skus/MS-AZR-0145P?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "id": "0001",
            "productId": "DZH318Z0BPS6",
            "title": "Microsoft Azure plan",
            "description": "Microsoft Azure plan (MS-AZR-0017G)",
            "minimumQuantity": 1,
            "maximumQuantity": 1,
            "isTrial": false,
            "supportedBillingCycles": [
                "one_time"
            ],
            "purchasePrerequisites": [
                "MicrosoftCustomerAgreement"
            ],
            "inventoryVariables": [],
            "provisioningVariables": [],
            "actions": [
                "Refund"
            ],
            "dynamicAttributes": {
                "isMicrosoftProduct": true,
                "pilotProgram": "modernazurepilot"
            },
            "links": {
                "availabilities": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001/availabilities?country=US&targetSegment=Commercial",
                    "method": "GET",
                    "headers": []
                },
                "self": {
                    "uri": "/products/DZH318Z0BPS6/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/e2a0c0f3-0f74-4d1c-808c-dfa511481913/products/all/skus?targetView=MicrosoftAzure&targetSegment=Commercial",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
