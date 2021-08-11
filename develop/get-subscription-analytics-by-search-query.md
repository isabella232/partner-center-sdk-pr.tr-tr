---
title: Arama sorgusuna abonelik Analizi al
description: Bir arama sorgusuyla filtrelenmiş abonelik Analizi bilgilerini alma.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dc6ef8d2136c5ffac3278a372980e9a601ef49bb485ef54187865fc9431b3404
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115995688"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a>Bir arama sorgusuyla filtrelenmiş abonelik analizi bilgilerini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bir arama sorgusuyla filtrelenmiş müşterileriniz için abonelik Analizi bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si |
|--------|-------------|
| **Al** | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri? Filter = {filter_string} |

### <a name="uri-parameters"></a>URI parametreleri

Kuruluşunuzu tanımlamak ve aramayı filtrelemek için aşağıdaki gerekli yol parametresini kullanın.

| Ad | Tür | Gerekli | Açıklama |
|------|------|----------|-------------|
| filter_string | string | Yes | Abonelik analizinden uygulanacak filtre. Bu parametrede kullanılacak söz dizimi, alanlar ve işleçler için filtre söz dizimini ve filtre alanları bölümlerine bakın. |

### <a name="filter-syntax"></a>Filtre sözdizimi

Filter parametresi bir dizi alan, değer ve işleç birleşimi olarak oluşturulmalıdır. Birden çok bileşim, **`and`** veya işleçleri kullanılarak birleştirilebilir **`or`** .

Kodlanamayan bir örnek şuna benzer:

- Dizisinde `?filter=Field operator 'Value'`
- Boolean `?filter=Field operator Value`
- Vardır `?filter=contains(field,'value')`

### <a name="filter-fields"></a>Filtre alanları

İsteğin filtre parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor. Her bir ifade, **`eq`** veya işleçleriyle ilişkili bir alan ve değer içerir **`ne`** . Bazı alanlar,,, **`contains`** , **`gt`** **`lt`** **`ge`** ve **`le`** işleçlerini da destekler. Deyimler, **`and`** veya işleçleri kullanılarak birleştirilebilir **`or`** .

Filtre dizelerinin örnekleri aşağıda verilmiştir:

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

Aşağıdaki tabloda, filtre parametresi için desteklenen alanların ve destek işleçlerinin listesi gösterilmektedir. Dize değerleri tek tırnak işareti içine alınmalıdır.

| Parametre | Desteklenen işleçler | Description |
|-----------|---------------------|-------------|
| autoRenewEnabled | `eq`, `ne` | Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer. |
| commitmentEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Aboneliğin bitiş tarihi. |
| creationDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Aboneliğin oluşturulduğu tarih. |
| currentStateEndDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Aboneliğin geçerli durumunun değiştirileceği tarih. |
| customerMarket | `eq`, `ne` | Müşterinin iş üzerinde kullandığı ülke/bölge. |
| customerName | `contains` | Müşterinin adı. |
| Customertenantıd | `eq`, `ne` | Müşteri kiracısını tanımlayan GUID biçimli bir dize. |
| deprovisionedDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Aboneliğin sağlaması kaldırılmış olan tarih. Varsayılan değer boştur. |
| effectiveStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Aboneliğin başladığı tarih. |
| friendlyName | `contains` | Aboneliğin adı. |
| kimlik | `eq`, `ne` | Aboneliği tanımlayan GUID biçimli bir dize. |
| lastRenewalDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Aboneliğin son yenilenme tarihi. Varsayılan değer boştur. |
| lastUsageDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Aboneliğin son kullanıldığı tarih. Varsayılan değer boştur. |
| iş ortağı kimliği | `eq`, `ne` | MPN KIMLIĞI. Doğrudan satıcı için bu değer ortağın MPN KIMLIĞI olacaktır. Dolaylı bir satıcı için, bu değer dolaylı satıcının MPN KIMLIĞI olacaktır. |
| partnerName | string | Aboneliğin satın alındığı ortağın adı |
| productName | `contains`, `eq`, `ne` | Ürünün adı. |
| Adı | string | Abonelik işlemi dolaylı satıcı için olduğunda, sağlayıcı adı aboneliği satın alan dolaylı sağlayıcıdır.|
| durum | `eq`, `ne` | Abonelik durumu. Desteklenen değerler şunlardır: "ETKIN", "askıya ALıNDı" veya "SAĞLAMASı KALDıRıLDı". |
| subscriptionType | `eq`, `ne` | Abonelik türü. **Note**: Bu alan, büyük/küçük harfe duyarlıdır. desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| trialStartDate | `eq`, `ne`, `gt`, `lt`, `ge`, `le` | Abonelik için deneme süresinin başladığı tarih. Varsayılan değer boştur. |
| Trialtopaıdconversiondate | `eq`, `ne`, `gt`, `lt`, `ge`, `le`  | Aboneliğin deneme sürümünden ücretli olarak dönüştürdüğü tarih. Varsayılan değer boştur. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa yanıt gövdesi, filtre ölçütlerine [uyan bir](partner-center-analytics-resources.md#subscription-resource) Abonelik kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a>Ayrıca bkz.

- [İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
