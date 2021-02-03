---
title: İş Ortağı Merkezi REST API’si değişiklik günlüğü
description: Bu sayfada Iş Ortağı Merkezi REST API 'Lerinde yapılan değişiklikler listelenir
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.topic: reference
ms.date: 12/15/2020
ms.openlocfilehash: 79359414276a1259117a8f506bbfae4441cdcbed
ms.sourcegitcommit: f8ca3a14a763013fefafd3262d0a740881d1d7b1
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/17/2020
ms.locfileid: "97770282"
---
# <a name="december-2020-changes-to-partner-center-rest-apis"></a>Iş Ortağı Merkezi REST API 'Lerinde Aralık 2020 değişiklikleri

Iş Ortağı Merkezi REST API 'Lerinde yapılan değişiklikler için buraya bakın.

## <a name="enhancements-to-education-pricing-eligibility-apis"></a>Eğitim Fiyatlandırma uygunluğu API 'Lerine yönelik geliştirmeler



### <a name="what-has-changed"></a>Ne değişti?

Şu anda Iş Ortağı Merkezi API 'sinin eğitim müşterilerinin uygunluğunu doğrulamak için GET ve PUT nitelikleri vardır. Nitelik al API 'sinde hiçbir değişiklik olmayacaktır. Ancak, YERLEŞTIRME API 'sine bir dönüş durumu ekledik.

- GET-değişmez. [Geçerli API makalesi](get-a-customer-s-qualification.md)
- PUT-Return Case eklenecektir. [Geçerli API makalesi](update-a-customer-s-qualification.md)

Bu API 'Ler, aşağıda açıklandığı gibi yeni API 'Ler ile değiştirilerek, Şubat 2021 ' un sonunda kullanımdan kaldırılacaktır.

### <a name="scenarios-impacted"></a>Etkilenen senaryolar:

Select SKU 'Larında eğitim fiyatlandırması için Müşteri uygunluğu

### <a name="detail-descriptions"></a>Ayrıntı açıklamaları

İki yeni GET ve POST nitelikleri API 'si tanıtılacaktır. Yeni API 'Ler **nitelik** değil, **nitelikleri** kullanacaktır. API 'Ler, FY21 S2 'de test için kullanılabilir olacaktır.

#### <a name="get-qualifications"></a>Nitelikleri al

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

- VettingStatus değerleri: onaylandı, reddedildi, ınreview, vb.

- VettingReason değerleri:
   - Eğitim müşterisi değil
   - Artık eğitim müşterisi yok
   - Eğitim müşterisi değil-Inceleme sonrası
   - Eğitim müşterisi olacak şekilde kısıtlıdır
   - Akademik etki alanı değil
   - Uygun bir kitaplık değil
   - Uygun Museum değil
 
#### <a name="post-qualifications"></a>GÖNDERI nitelikleri

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
