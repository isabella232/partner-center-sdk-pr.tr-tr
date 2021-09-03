---
title: Yeni bir ticari aboneliğe geçiş
description: Müşterinin yeni Commmerce aboneliğini belirtilen bir hedef aboneliğe yükseltir.
ms.date: 02/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 2bbf2f63cec416e4d4b4a671d2e2b2914b5f5713
ms.sourcegitcommit: e1db965e8c7b4fe3aaa0ecd6cefea61973ca2232
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/03/2021
ms.locfileid: "123457324"
---
# <a name="transition-a-new-commerce-subscription"></a>Yeni bir ticari aboneliğe geçiş

**Uygulama hedefi**: Iş Ortağı Merkezi

**Uygun roller**

- Genel yönetici
- Yönetim Aracısı

> [!Note] 
> Yeni ticaret değişiklikleri şu anda yalnızca M365/D365 yeni ticaret deneyimi teknik önizlemesinin parçası olan iş ortakları tarafından kullanılabilir.

Müşterinin yeni Commmerce aboneliğini bir hedef aboneliğe yükseltmek için kullanılır. İlk olarak, SKU 'Ları yükseltme için kullanılabilir hale getirmek için uygun geçişleri alın. Sonra geçişi yürütmek için geçiş sonrası. Bu yöntemler hem geleneksel hem de yeni ticaret kaynağı aboneliklerini destekler.  

## <a name="get-transition-eligibilities"></a>Geçiş elizlikler al

Belirli bir müşteri, abonelik ve istenen tür için uygun geçişlerin listesini döndürür.

### <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- İlk abonelik için bir abonelik KIMLIĞI.

### <a name="rest-request"></a>REST isteği

#### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **AL**  | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Subscriptions/{Subscription-id}/geçişli tioneligılıklara? eligibilityType = {ım, ZAMANLANDı} http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Uygun geçişleri döndürmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                    | Tür     | Gerekli | Açıklama                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Müşteri-Kiracı kimliği**  | **guid** | Y        | Müşterinin kiracısına karşılık gelen bir GUID.             |
| **alt bilgisayar kimliği** | **guid** | Y        | İlk aboneliğe karşılık gelen bir GUID. |
| **eligibilityType**       | **string** | Y        | Dönüştürme ne zaman yürütüleceğini, anında veya zamanlanacağını açıklar.  |

#### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

#### <a name="request-body"></a>İstek gövdesi

Hiçbiri

#### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/{subscription-Id}/transitionEligibilities?eligibilityType=immediate HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US
```

### <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde uygun geçişlerin listesini döndürür.

#### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

#### <a name="eligibility-errors"></a>Uygunluk hataları

Hata açıklamaları ve anlamı.

| Hata açıklaması | Anlamı  |
|-------------------------|----------|
|Abonelik geçirilemez-kaynak abonelik etkin değil. | Özgün alt durum etkin değil |
|Abonelik geçirilemez-kaynak abonelik henüz sağlanmadı. | Özgün Sub FulfillmentState başarılı değil |
|Geçiş türü uyumlu değil-AzureAD abonelik eşlemesi gerekiyor. | GetSubscriptionUpgradeConflicts çağrılırken Legacycannotconvertsubscriptionıd hatası |
|Geçiş türü uyumlu değil-lisans aktarımı için çakışan abonelikler var. | Herhangi bir AAD hizmetinin abonelik kimlikleri farklı bir abonelikten varsa, bunu çakışma listesine ekleyin (eski veya modern satın alma akışından yapılan satınalmaları içerir) |

#### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "totalCount": 2,
    "items": [
        {
            "catalogItemId": "CFQ7TTC0KZCR:0001:CFQ7TTC0K71H",
            "title": "Microsoft 365 E5 Test Sku Title",
            "description": "Microsoft 365 E5 Test Sku Description",
            "quantity": 1,
            "eligibilities": [
{
                    "isEligible": true,
                    "transitionType": "transition_only",
                    "errors": []
                },
                
{
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        },
        {
            "catalogItemId": "CFQ7TTC0L4M3:0001:CFQ7TTC0K78T",
            "title": "Business Premium Test Sku Title",
            "description": "Business Premium Test Sku Description",
            "quantity": 1,
            "eligibilities": [
                {
                    "isEligible": false,
                    "transitionType": "transition_with_license_transfer",
                    "errors": [
                        {
                            "code": 3,
                            "description": "Subscription cannot be transitioned because there are conflicting services."
                        }
                    ]
                }
            ],
            "attributes": {
                "objectType": "TransitionEligibility"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```

## <a name="post-transition"></a>Geçiş sonrası

Belirli bir müşteri ve abonelik için bir geçiş isteği gönderir. Başlatma durumuyla geçişi döndürür.

### <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

- Bir müşteri KIMLIĞI ( `customer-tenant-id` ). Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz. Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin. Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin. Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın. Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .

- İlk abonelik için bir abonelik KIMLIĞI.

### <a name="rest-request"></a>REST isteği

#### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **YAYINLA**  | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{/toın-ID}/geçişleri http/1.1 |


#### <a name="uri-parameter"></a>URI parametresi

Bir geçişi yürütmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                    | Tür     | Gerekli | Açıklama                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **Müşteri-Kiracı kimliği**  | **guid** | Y        | Müşterinin kiracısına karşılık gelen GUID.             |
| **subscriptoin-Id** | **guid** | Y        | İlk aboneliğe karşılık gelen GUID. |

#### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

#### <a name="request-body"></a>İstek gövdesi

İstek **gövdesinde** tam bir Geçiş kaynağı gereklidir.

#### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customerId}/subscriptions/{subscriptionId}/transitions HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "toCatalogItemId": "CFQ7TTC0KZ59:0001:CFQ7TTC0KZ59",
    "quantity": 5,
    "transitionType": "transition_with_license_transfer",
    "events": []
}
```

### <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem ilk olaylarla birlikte bir Geçiş kaynağı döndürür.

#### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

#### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "FromCatalogItemId": "CFQ7TTC0LDPB:0001:CFQ7TTC0LGNT",
    "ToCatalogItemId": "CFQ7TTC0LF8S:0001:CFQ7TTC0K9G9",
    "quantity": 1,
    "transitionType": "transition_with_license_transfer",
    "Events": [
        {
            "name": "Conversion",
            "status": "Started ",
            "timestamp": "2021-01-08T18:01:14.7488618Z",
            "attributes":
            {
                "objectType": "TransitionEvent"
            }
        }
    ],
    "attributes":
    {
        "objectType": "Transition"
    }
}
```
