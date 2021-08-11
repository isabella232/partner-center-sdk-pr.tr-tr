---
title: İş Ortağı Merkezi REST API’si değişiklik günlüğü
description: Bu sayfada rest API'lerinde İş Ortağı Merkezi listeleniyor
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: f74f59969bf8d73c6e6e8b39900a53c337a2af715c168b59009792beddf43159
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115993291"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Rest API'leri için Aralık 2020 İş Ortağı Merkezi değişiklikleri

Rest API'leri için İş Ortağı Merkezi buradan kontrol edin.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Eğitim fiyatlandırması Uygunluk API'leri iyileştirmeleri



### <a name="what-has-changed"></a>Neler değişti?

Şu anda İş Ortağı Merkezi API'si, Eğitim müşterilerinin uygunluğunu doğrulamak için GET ve PUT niteliklerini içerir. GET Nitelik API'sini hiçbir değişiklik olmayacaktır. Ancak PUT Nitelik API'sini bir dönüş durumu ekledik.

- GET - değişmez.
- PUT - dönüş durumu eklenir.

Bu API'ler Şubat 2021'in sonunda, aşağıda açıklandığı gibi yeni API'ler ile değiştirilene kadar sona erer.

### <a name="scenarios-impacted"></a>Etkilene senaryolar:

Belirli SKUS'larda eğitim fiyatlandırması için müşteri uygunluğu

### <a name="detail-descriptions"></a>Ayrıntı açıklamaları

İki yeni GET ve POST Nitelik API'si tanıtacak. Yeni API'ler Nitelik **değil** Nitelikler'i **kullanacak.** API'ler FY21 Q2'de test için kullanılabilir.

#### <a name="get-qualifications"></a>GET Nitelikleri

```http
GET {customer_id}/qualifications
```

#### <a name="response-example"></a>Yanıt örneği:

```json
{
  "Qualification": "Education",
  "VettingStatus": "Denied",
  "VettingReason": "Not an education customer",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

#### <a name="response-fields"></a>Yanıt alanları: 

- VettingStatus değerleri: Approved, Denied, InReview vb.

- VettingReason değerleri:
   - Eğitim Müşterisi Değil
   - Artık Eğitim Müşterisi değil
   - Eğitim Müşterisi Değil - Gözden GeçirmeDen Sonra
   - Eğitim Müşterisi olma kısıtlaması
   - Akademik Etki Alanı Değil
   - Uygun Bir Kitaplık Değil
   - Uygun bir Yer Değil
 
#### <a name="post-qualifications"></a>POST Nitelikleri

```http
POST {customer_id}/qualifications
    [
            "Qualification": "Education"
    ]
```

#### <a name="response-example"></a>Yanıt örneği:

```JSON
{
  "Qualification": "Education",
  "VettingStatus": "InReview",
  "VettingCreatedDate": "07/09/2020: 00:00:00" //UTC
}
```

## <a name="next-steps"></a>Sonraki adımlar

[İş Ortağı Merkezi REST API'si referansı](partner-center-rest-api-reference.md)
