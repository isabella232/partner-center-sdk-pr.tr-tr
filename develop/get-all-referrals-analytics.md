---
title: Tüm başvuru analizi bilgilerini alma
description: Tüm referans analizi bilgilerini nasıl elde edinebilirsiniz?
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: Kim-Davis
ms.author: kimnich
ms.openlocfilehash: 7deda4098ceb9eb4e1ee75056c53c754618bf3e2
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760615"
---
# <a name="get-all-referrals-analytics-information"></a>Tüm başvuru analizi bilgilerini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Müşterileriniz için tüm referans analizi bilgilerini nasıl elde edersiniz?

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si |
|---------|-------------|
| **Al** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/referanslar HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

| Parametre | Tür | Açıklama |
|-----------|------|-------------|
| filtre | string | Filtre koşuluyla eşleşen verileri döndürür.</br> **Örnek:**</br>  `.../referrals?filter=field eq 'value'` |
| Groupby | string | Hem terimleri hem de tarihleri destekler. Demet sayısını sınırlamak için kısa devre mantığı.</br> **Örnek:**</br>  `.../referrals?groupby=termField1,dateField1,termField2` |
| aggregationLevel | string | *aggregationLevel parametresi* bir *groupby gerektirir.* *aggregationLevel* parametresi, groupby içinde mevcut olan tüm tarih *alanlarına uygulanır.*</br> **Örnek:**</br> `.../referrals?groupby=termField1,dateField1,termField2&aggregationLevel=day` |
| top | string | Sayfa sınırı 10000'tir. 10000'den küçük herhangi bir değeri alır.</br> **Örnek:**</br> `.../referrals?top=100`</br> |
| Atla | string | Atlan satır sayısı.</br> **Örnek:**</br>  `.../referrals?top=100&skip=100` |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, yanıt gövdesi Bir Referans kaynakları [koleksiyonu](partner-center-analytics-resources.md#referrals-resource) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

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
