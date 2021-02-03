---
title: Aktarım oluştur
description: Bir müşteri için aboneliklerin aktarımını oluşturma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768830"
---
# <a name="create-a-transfer"></a>Aktarım oluştur

**Uygulama hedefi:**

- İş Ortağı Merkezi

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/aktarımlar http/1.1                    |

### <a name="uri-parameter"></a>URI parametresi

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad            | Tür     | Gerekli | Açıklama                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **müşteri kimliği** | string   | Yes      | Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.             |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Bu tablo, istek gövdesinde [Transferentity](transfer-entity-resources.md) özelliklerini açıklar.

| Özellik              | Tür          | Gerekli  | Açıklama                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| kimlik                    | dize        | No    | TransferEntity başarıyla oluşturulduktan sonra sağlanan bir transferEntity tanımlayıcısı.                               |
| createdTime           | DateTime      | No    | TransferEntity oluşturulduğu tarih-saat biçiminde. TransferEntity başarıyla oluşturulduktan sonra uygulandı.      |
| Zamanı      | DateTime      | No    | TransferEntity 'ın son güncelleştirilme tarihi, tarih-saat biçiminde. TransferEntity başarıyla oluşturulduktan sonra uygulandı. |
| lastModifiedUser      | dize        | No    | Transfer varlığını son güncelleştiren Kullanıcı. TransferEntity başarıyla oluşturulduktan sonra uygulandı.                          |
| customerName          | dize        | No    | İsteğe bağlı. Abonelikleri aktarılmakta olan müşterinin adı.                                              |
| Customertenantıd      | dize        | No    | Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği. TransferEntity başarıyla oluşturulduktan sonra uygulandı.         |
| partnertenantıd       | dize        | No    | Ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.                                                                   |
| sourcePartnerName     | dize        | No    | İsteğe bağlı. Aktarımı başlatan iş ortağının kuruluşun adı.                                           |
| Sourcepartnertenantıd | string        | Yes   | Aktarımı başlatan ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.                                           |
| targetPartnerName     | dize        | No    | İsteğe bağlı. Aktarımın hedeflediği iş ortağının kuruluşun adı.                                         |
| Targetpartnertenantıd | string        | Yes   | Aktarımın hedeflediği ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.                                  |
| LineItems             | Nesne dizisi | Yes| Bir [Transferlineıtem](transfer-entity-resources.md#transferlineitem) kaynakları dizisi.                                   |
| durum                | dize        | No    | TransferEntity durumu. Olası değerler şunlardır. "etkin" (silinebilir/gönderilebilir) ve "tamamlandı" (daha önce tamamlanmış). TransferEntity başarıyla oluşturulduktan sonra uygulandı.|

Bu tablo, istek gövdesinde [Transferlineıtem](transfer-entity-resources.md#transferlineitem) özelliklerini açıklar.

|      Özellik       |            Tür             | Gerekli | Açıklama                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| kimlik                   | dize                     | No       | Aktarım satırı öğesi için benzersiz bir tanımlayıcı. TransferEntity başarıyla oluşturulduktan sonra uygulandı.|
| subscriptionId       | string                     | Yes      | Abonelik tanımlayıcısı.                                                                         |
| miktar             | int                        | No       | Lisans veya örnek sayısı.                                                                 |
| Bilimlingcycle         | Nesne                     | No       | Geçerli dönem için ayarlanan faturalandırma dönemi türü.                                                |
| friendlyName         | dize                     | No       | İsteğe bağlı. Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                |
| partnerIdOnRecord    | dize                     | No       | Aktarım kabul edildiğinde gerçekleşen Satınalmadaki iş ortağı kimliği (MPNıD).              |
| OfferId              | dize                     | No       | Teklif tanımlayıcısı.                                                                                |
| Addonıtems           | **Transferlineıtem** nesnelerinin listesi | No | Aktarılmakta olan, aktarılan temel abonelikle birlikte aktarılacak olan bir transferEntity satır öğeleri koleksiyonu. TransferEntity başarıyla oluşturulduktan sonra uygulandı.|
| Transferhatası        | dize                     | No       | Bir hata durumunda transferEntity kabul edildikten sonra uygulandı.                                        |
| durum               | dize                     | No       | TransferEntity içindeki LineItem 'ın durumu.                                                    |

### <a name="request-example"></a>İstek örneği

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [Transferenity](transfer-entity-resources.md) kaynağını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
