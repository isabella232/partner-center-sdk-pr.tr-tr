---
title: Pazara göre teklif kategorilerinin bir listesini alma
description: Belirli bir ülke/bölgedeki tüm teklif kategorilerini ve tüm Microsoft bulutları için yerel ayarları içeren bir koleksiyon almayı öğrenin.
ms.date: 07/25/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 05aad095c6cb8eaee4cbf7ce976ca1b4b7a408c4
ms.sourcegitcommit: f72173df911aee3ab29b008637190b4d85ffebfe
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/06/2021
ms.locfileid: "106500065"
---
# <a name="get-a-list-of-offer-categories-by-market"></a>Pazara göre teklif kategorilerinin bir listesini alma

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Bu makalede, belirli bir ülke/bölge ve yerel ayarda yer alan tüm teklif kategorilerini içeren bir koleksiyonun nasıl alınacağı açıklanır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.

## <a name="c"></a>C\#

Belirli bir ülke/bölge ve yerel ayarda teklif kategorilerinin bir listesini almak için:

1. Belirtilen bağlamda [**with ()**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner.with) yöntemini çağırmak Için [**ıaggregatepartner. Operations**](/dotnet/api/microsoft.store.partnercenter.iaggregatepartner) koleksiyonunuzu kullanın.

2. Elde edilen nesnenin [**Offercategories**](/dotnet/api/microsoft.store.partnercenter.ipartner.offercategories) özelliğini inceleyin.

``` csharp
// IAggregatePartner partnerOperations;

ResourceCollection<OfferCategory> offerCategoryResults = partnerOperations.With(RequestContextFactory.Instance.Create()).OfferCategories.ByCountry("US").Get();
```

Bir örnek için aşağıdakilere bakın:

- Örnek: [konsol test uygulaması](console-test-app.md)
- Proje: **Partnersdk. FeatureSample**
- Sınıf: **Partnersdk. FeatureSample**

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| **Al** | [*{BaseUrl}*](partner-center-rest-urls.md)/v1/offercategories? ülke = {ülke-KIMLIĞI} http/1.1 |

#### <a name="uri-parameter"></a>URI parametresi

Bu tablo teklif kategorilerini almak için gerekli sorgu parametrelerini listeler.

| Ad           | Tür       | Gerekli | Açıklama            |
|----------------|------------|----------|------------------------|
| **ülke kimliği** | **string** | Y        | Ülke/bölge KIMLIĞI. |

### <a name="request-headers"></a>İstek üst bilgileri

Dize olarak biçimlendirilen bir **yerel ayar kimliği** gereklidir.

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/offercategories?country=<country-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
X-Locale: <locale-id>
Connection: Keep-Alive
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt gövdesinde **Offercategory** kaynaklarının bir koleksiyonunu döndürür.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 1184
Content-Type: application/json
MS-CorrelationId: 47882653-eaed-4a2e-a552-1070a3fa1089
MS-RequestId: 4fb54bd5-a4c3-4fac-955f-9b6e3436d606
Date: Thu, 26 Nov 2015 00:07:10 GMT

{
    "totalCount": 4,
    "items": [{
        "id": "Enterprise_Key",
        "name": "Enterprise",
        "rank": 20,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "SmallBusiness_Key",
        "name": "SmallBusiness",
        "rank": 30,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Government_Key",
        "name": "Government",
        "rank": 40,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    },
    {
        "id": "Internal_Key",
        "name": "Internal",
        "rank": 100,
        "locale": "en-us",
        "country": "US",
        "attributes": {
            "objectType": "OfferCategory"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
