---
title: Aktarım oluşturma
description: Müşteri için abonelik aktarımı oluşturma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8414bbcfa0940742339eeba24b3b6a16ddfb6e3424670a4c064cbd995ba50851
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991591"
---
# <a name="create-a-transfer"></a>Aktarım oluşturma

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| **Yayınla** | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1                    |

### <a name="uri-parameter"></a>URI parametresi

Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.

| Ad            | Tür     | Gerekli | Açıklama                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| **customer-id** | string   | Yes      | Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id.             |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Bu tabloda istek [gövdesinde TransferEntity](transfer-entity-resources.md) özellikleri açık edilmektedir.

| Özellik              | Tür          | Gerekli  | Açıklama                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| kimlik                    | dize        | No    | transferEntity'nin başarıyla oluşturulmasının ardından sağlanan bir transferEntity tanımlayıcısı.                               |
| createdTime           | DateTime      | No    | transferEntity'nin tarih-saat biçiminde oluşturulma tarihi. transferEntity başarıyla oluşturularak uygulanır.      |
| lastModifiedTime      | DateTime      | No    | transferEntity'nin en son güncelleştirilen tarih-saat biçiminde olduğu tarih. transferEntity başarıyla oluşturularak uygulanır. |
| lastModifiedUser      | dize        | No    | transferEntity'i en son güncelleştirilen kullanıcı. transferEntity başarıyla 1.000.000'in oluşturulmasının ardından uygulanır.                          |
| Müşteriadı          | dize        | No    | İsteğe bağlı. Abonelikleri aktarılan müşterinin adı.                                              |
| customerTenantId      | dize        | No    | Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id. transferEntity başarıyla oluşturularak uygulanır.         |
| partnertenantid       | dize        | No    | İş ortağını tanımlayan GUID biçimlendirilmiş iş ortağı kimliği.                                                                   |
| sourcePartnerName     | dize        | No    | İsteğe bağlı. Aktarımı başlatan iş ortağının kuruluş adı.                                           |
| sourcePartnerTenantId | string        | Yes   | Aktarımı başlatan iş ortağını tanımlayan GUID biçimli iş ortağı kimliği.                                           |
| targetPartnerName     | dize        | No    | İsteğe bağlı. Aktarımın hedeflen olduğu iş ortağının kuruluş adı.                                         |
| targetPartnerTenantId | string        | Yes   | Aktarımın hedeflene iş ortağını tanımlayan GUID biçimli iş ortağı kimliği.                                  |
| lineItems             | Nesne dizisi | Yes| [TransferLineItem kaynakları](transfer-entity-resources.md#transferlineitem) dizisi.                                   |
| durum                | dize        | No    | transferEntity durumu. Olası değerler "Etkin" (silinebilir/gönderebilirsiniz) ve "Tamamlandı" (zaten tamamlandı) değerleridir. transferEntity başarıyla oluşturularak uygulanır.|

Bu tablo, istek [gövdesinin TransferLineItem](transfer-entity-resources.md#transferlineitem) özelliklerini açıklar.

|      Özellik       |            Tür             | Gerekli | Açıklama                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| kimlik                   | dize                     | No       | Aktarım satırı öğesi için benzersiz tanımlayıcı. transferEntity başarıyla oluşturularak uygulanır.|
| subscriptionId       | string                     | Yes      | Abonelik tanımlayıcısı.                                                                         |
| miktar             | int                        | No       | Lisans veya örnek sayısı.                                                                 |
| billingCycle         | Nesne                     | No       | Geçerli dönem için ayarlanmış faturalama dönemi türü.                                                |
| Friendlyname         | dize                     | No       | İsteğe bağlı. Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.                |
| partnerIdOnRecord    | dize                     | No       | Aktarım kabul edilirken yapılan satın almada Kayıtta PartnerId (MPN KIMLIĞI).              |
| offerId              | dize                     | No       | Teklif tanımlayıcısı.                                                                                |
| addonItems           | **TransferLineItem nesnelerinin** listesi | No | Aktarılan temel abonelikle birlikte aktaracak eklentiler için transferEntity satır öğeleri koleksiyonu. transferEntity başarıyla oluşturularak uygulanır.|
| transferError        | dize                     | No       | Bir hata varsa transferEntity kabul edildikten sonra uygulanır.                                        |
| durum               | dize                     | No       | transferEntity'de lineitem durumu.                                                    |

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

Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [TransferEnity](transfer-entity-resources.md) kaynağını döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

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
