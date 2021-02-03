---
title: Tarih veya koşullara göre gruplandırılmış abonelik analizlerini al
description: Tarih veya koşullara göre gruplanmış abonelik Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769052"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a>Tarih veya koşullara göre gruplandırılmış abonelik analizlerini al

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Müşterilerinizin tarihlere veya terimlere göre gruplanmış abonelik Analizi bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si |
|--------|-------------|
| **Al** | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri? GroupBy = {groupby_queries} |

### <a name="uri-parameters"></a>URI parametreleri

Kuruluşunuzu tanımlamak ve sonuçları gruplandırmak için aşağıdaki gerekli yol parametrelerini kullanın.

| Ad | Tür | Gerekli | Açıklama |
|------|------|----------|-------------|
| groupby_queries | dizeler ve tarih saat çiftleri | Yes | Sonucu filtrelemek için hüküm ve tarihler. |

### <a name="groupby-syntax"></a>GroupBy sözdizimi

Group By parametresi bir dizi virgülle ayrılmış, alan değeri olarak oluşturulmalıdır.

Kodlanamayan bir örnek şuna benzer:

```http
?groupby=termField1,dateField1,termField2
```

Aşağıdaki tabloda Group by için desteklenen alanların listesi gösterilmektedir.

| Alan | Tür | Description |
|-------|------|-------------|
| Customertenantıd | string | Müşteri kiracısını tanımlayan GUID biçimli bir dize. |
| customerName | string | Müşterinin adı. |
| customerMarket | string | Müşterinin iş üzerinde kullandığı ülke/bölge. |
| kimlik | string | Aboneliği tanımlayan GUID biçimli bir dize. |
| durum | string | Abonelik durumu. Desteklenen değerler şunlardır: "ETKIN", "askıya ALıNDı" veya "SAĞLAMASı KALDıRıLDı". |
| productName | string | Ürünün adı. |
| subscriptionType | string | Abonelik türü. Note: Bu alan, büyük/küçük harfe duyarlıdır. Desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS". |
| autoRenewEnabled | Boole | Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer. |
| iş ortağı kimliği  | string | MPN KIMLIĞI. Doğrudan satıcı için, bu parametre ortağın MPN KIMLIĞI olur. Dolaylı bir satıcı için, bu parametre dolaylı satıcıdan MPN KIMLIĞI olacaktır. |
| friendlyName | string | Aboneliğin adı. |
| partnerName | string | Aboneliğin satın alındığı ortağın adı |
| Adı | string | Abonelik işlemi dolaylı satıcı için olduğunda, sağlayıcı adı aboneliği satın alan dolaylı sağlayıcıdır.
| creationDate | UTC Tarih saat biçiminde dize | Aboneliğin oluşturulduğu tarih. |
| effectiveStartDate | UTC Tarih saat biçiminde dize | Aboneliğin başladığı tarih. |
| commitmentEndDate | UTC Tarih saat biçiminde dize | Aboneliğin bitiş tarihi. |
| currentStateEndDate | UTC Tarih saat biçiminde dize | Aboneliğin geçerli durumunun değiştirileceği tarih. |
| Trialtopaıdconversiondate | UTC Tarih saat biçiminde dize | Aboneliğin deneme sürümünden ücretli olarak dönüştürdüğü tarih. Varsayılan değer boştur. |
| trialStartDate | UTC Tarih saat biçiminde dize | Abonelik için deneme süresinin başladığı tarih. Varsayılan değer boştur. |
| lastUsageDate | UTC Tarih saat biçiminde dize | Aboneliğin son kullanıldığı tarih. Varsayılan değer boştur. |
| deprovisionedDate | UTC Tarih saat biçiminde dize | Aboneliğin sağlaması kaldırılmış olan tarih. Varsayılan değer boştur. |
| lastRenewalDate | UTC Tarih saat biçiminde dize | Aboneliğin son yenilenme tarihi. Varsayılan değer boştur. |

### <a name="filter-fields"></a>Filtre alanları

Aşağıdaki tablo, isteğe bağlı filtre alanlarını ve açıklamalarını listelemektedir:

| Alan | Tür |  Description |
|-------|------|--------------|
| top | int | İstekte döndürülecek veri satır sayısı. Değer belirtilmezse, en büyük değer ve varsayılan değer 10000 ' dir. Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir. |
| Atla | int | Sorgudaki atlanacak satır sayısı. Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın. Örneğin, top = 10000 ve Skip = 0 verilerin ilk 10000 satırını alır, top = 10000 ve Skip = 10000, sonraki 10000 satırlık verileri alır. |
| filtre | string | Yanıttaki satırları filtreleyen bir veya daha fazla deyim. Her filtre ekstresi, yanıt gövdesinden bir alan adı ve **`eq`** , **`ne`** veya belirli alanlar için, işleci ile ilişkili bir değer içerir **`contains`** . Deyimler, veya kullanılarak birleştirilebilir **`and`** **`or`** . Dize değerleri, filtre parametresindeki tek tırnak işaretleriyle çevrelenmelidir. Filtrelenebilir alanların listesi ve bu alanlarla Desteklenen işleçler için aşağıdaki bölüme bakın. |
| aggregationLevel | string | Toplam verilerinin alınacağı zaman aralığını belirtir. Şu dizelerden biri olabilir: **gün**, **hafta** veya **ay**. Değer belirtilmezse, varsayılan olarak **Dadterange** olur. **Note**: Bu parametre yalnızca, GroupBy parametresinin bir parçası olarak bir tarih alanı geçirildiğinde geçerlidir. |
| Ölçütü | string | Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi belirtilen hüküm ve tarihlere göre gruplanmış bir [abonelik](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a>Ayrıca bkz.

[İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
