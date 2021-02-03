---
title: Tüm başvuru analizi bilgilerini alma
description: Tüm başvuru Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: b470c59cecf8b214e6d90a244e928e5d15ebd3e0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769082"
---
# <a name="get-all-referrals-analytics-information"></a>Tüm başvuru analizi bilgilerini alma

**Uygulama hedefi**

- İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Müşterileriniz için tüm başvuru Analizi bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si |
|---------|-------------|
| **Al** | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/başvuruları http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

| Parametre | Tür | Description |
|-----------|------|-------------|
| filtre | string | Filtre koşuluyla eşleşen verileri döndürür.</br> **Örnek:**</br>  `.../referrals?filter=field eq 'value'` |
| ölçütü | string | Hem hüküm hem de tarihleri destekler. Demet sayısını sınırlandırmak için kısa devre mantığı.</br> **Örnek:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | string | *AggregationLevel* parametresi bir *GroupBy* gerektirir. *AggregationLevel* parametresi, *GroupBy* içinde bulunan tüm tarih alanları için geçerlidir.</br> **Örnek:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | string | Sayfa sınırı 10000 ' dir. 10000 'den küçük bir değer alır.</br> **Örnek:**</br> `.../referrals?top=100`</br> |
| Atla | string | Atlanacak satır sayısı.</br> **Örnek:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/referrals HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [başvuru](partner-center-analytics-resources.md#referrals-resource) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
{
  "id": "112310",
  "status": "Accepted",
  "customerMarket": "US",
  "customerName": "Best Customer Ever",
  "customerOrgSize": "10to50employees",
  "acceptedDate": "2018-02-07T23:43:19",
  "acknowledgedDate": "2018-02-07T23:40:50",
  "archivedDate": null,
  "declinedDate": null,
  "expiredDate": null,
  "lostDate": null,
  "missedDate": null,
  "createdDate": "2018-02-04T23:08:59",
  "skippedDate": null,
  "wonDate": null,
  "partnerMarket": "US"
}
```

## <a name="see-also"></a>Ayrıca bkz.

- [İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
