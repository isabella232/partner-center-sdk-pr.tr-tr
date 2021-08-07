---
title: Tüm arama analizi bilgilerini alma
description: Tüm arama Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a420752264f4d3074ba8a569c931654fda3ad6363d8d5d8b6a7a3e32af126bd1
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990911"
---
# <a name="get-all-search-analytics-information"></a>Tüm arama analizi bilgilerini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Müşterileriniz için tüm arama Analizi bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si |
|---------|-------------|
| **Al** | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/Search http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

|    Parametre     |  Tür  |                                                                                                                   Description                                                                                                                    |
|------------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|      filtre      | string |                                                                     Filtre koşuluyla eşleşen verileri döndürür. </br> **Örnek:**</br> `.../search?filter=field eq 'value'`                                                                     |
|     ölçütü      | string |                                         Hem hüküm hem de tarihleri destekler. Demet sayısını sınırlandırmak için kısa devre mantığı. </br> **Örnek:**</br> `.../search?groupby=termField1,dateField1,termField2`                                         |
| aggregationLevel | string | *AggregationLevel* parametresi bir *GroupBy* gerektirir. *AggregationLevel* parametresi, *GroupBy* içinde bulunan tüm tarih alanları için geçerlidir. </br> **Örnek:**</br>  `.../search?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
|       top        | string |                                                                     Sayfa sınırı 10000 ' dir. 10000 'den küçük bir değer alır.  </br> **Örnek:**</br>  `.../search?top=100`                                                                     |
|       Atla       | string |                                                                                  Atlanacak satır sayısı. </br> **Örnek:**</br> `.../search?top=100&skip=100`                                                                                   |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/search HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [arama](partner-center-analytics-resources.md#search-resource) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
{
  "companyName": "my company",
  "contactButtonClicked": false,
  "keywordCountry": null,
  "detailsViewed": true,
  "keywordIndustryFocus": null,
  "mpnId": 2604568,
  "partnerMarket": "CN",
  "keywordProduct": null,
  "referralSubmitted": false,
  "searchDate": "2018-05-30",
  "keywordSearchText": " my company"
}
```

## <a name="see-also"></a>Ayrıca bkz.

- [İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
