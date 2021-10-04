---
title: Verilen bir müşteri için fazla kullanılabilirlik güncelleştirmeleri
description: Bir müşteri için fazla kullanılabilirlik güncelleştirmeleri.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: BrentSerbus
ms.author: brserbus
ms.openlocfilehash: 58590a1882cfe94ddd9779f9e9f766f3e62cffd6
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/02/2021
ms.locfileid: "129383454"
---
# <a name="update-overage"></a>Fazlalık güncelleştirme

**Uygulandığı Yer**

- İş Ortağı Merkezi

**Uygun roller**

- Genel yönetici
- Yönetici aracısı

> [!Note] 
> Yeni Ticaret değişiklikleri şu anda yalnızca Microsoft 365/Dynamics 365 yeni ticaret deneyimi teknik önizlemesinde yer alan iş ortakları tarafından kullanılabilir.

Bir tüketim aboneliğine verilen bir müşteri için fazla kullanımı ayarlamak için kullanılır. Fazlalıkları kaldırmak için false olarak ayarlandırarak da kullanılabilir. Fazla kullanım, müşteri hizmetleri belirtilen sınırların ötesinde kullanıyorsa hizmetleri kullanmaya devam eder. Fazla kullanımı, tüketim aboneliğinin, tahakkuk eden ve tüketilen ödeme olarak ödemesi olduğunu tanımlar.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

- Müşteri kimliği ( `customer-tenant-id` ). Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard) İş Ortağı Merkezi'den **CSP'yi** ve ardından **Müşteriler'i seçin.** Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.** Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın. Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.

- Geçiş yapılan abonelik için bir abonelik kimliği.

## <a name="rest-request"></a>REST isteği
[PUT] /customers/{customer-tenant-id}/subscriptions/overage
### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem   | İstek URI'si                                                                                                                         |
|----------|-------------------------------------------------------------------------------------------------------------------------------------|
| **AL**  | [*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1 |

### <a name="uri-parameter"></a>URI parametresi

Müşterinin fazla kullanımlarını iade etmek için aşağıdaki sorgu parametrelerini kullanın.

| Ad                    | Tür     | Gerekli | Açıklama                                       |
|-------------------------|----------|----------|---------------------------------------------------|
| **customer-tenant-id**  | **guid** | Y        | Müşterinin kiracısına karşılık gelen GUID.             |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi


| Ad                    | Tür     | Description                                       |
|-------------------------|----------|---------------------------------------------------|
| **azureEntitlementId**  | **guid** | Fazla kullanımın tüketim aboneliğini tanımlayan GUID.             |
| **partnerId**  | **guid** | Dolaylı Kurumsal Bayinin MPN Kimliği. Yalnızca iki katmanlı model (Dolaylı Sağlayıcı) için geçerlidir.            |

| **overageEnabled**   |  **bool** | Belirli bir tüketim aboneliği için fazla kullanımın etkin olup olmadığını tanımlar.             |


### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/customers/{customer-tenant-id}/subscriptions/overage HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
X-Locale: en-US

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "overageEnabled": true
}

```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem müşteri için fazlalık döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 138
Content-Type: application/json
MS-CorrelationId: 81b08ffe-4cf8-49cd-82db-5c2fb0a8e132
MS-RequestId: 18752a69-1aa1-4ef7-8f9d-eb3681b2d70a
Date: Fri, 26 Feb 2021 20:42:26 GMT

{
    "azureEntitlementId": "ea1c26b7-8c99-42bb-ba7d-c535831fae8e",
    "partnerId": "5357563",
    "type": "PhoneServices",
    "overageEnabled": true,
    "links": {
        "overage": {
            "uri": "/customers/f62cf10b-8f76-4fc4-9774-c5291f8faf86/subscriptions/overage",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Overage"
    }
}
```
