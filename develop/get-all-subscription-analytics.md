---
title: Tüm abonelik analizi bilgilerini alma
description: Tüm abonelik Analizi bilgilerini alma.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: e1f16c92569a02bc51c96a85ecb642fbeb76a9a7
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760258"
---
# <a name="get-all-subscription-analytics-information"></a>Tüm abonelik analizi bilgilerini alma

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Bu makalede, müşterileriniz için tüm abonelik Analizi bilgilerinin nasıl alınacağı açıklanır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem | İstek URI'si |
|--------|-------------|
| **Al** | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri http/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Aşağıdaki tabloda isteğe bağlı parametreler ve açıklamaları listelenmektedir:

| Parametre | Tür |  Açıklama |
|-----------|------|--------------|
| top | int | İstekte döndürülecek veri satır sayısı. Değer belirtilmezse, en büyük değer ve varsayılan değer `10000` . Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir. |
| Atla | int | Sorgudaki atlanacak satır sayısı. Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın. Örneğin, `top=10000` ve `skip=0` ilk 10000 veri satırını alır `top=10000` ve `skip=10000` sonraki 10000 veri satırını alır. |
| filtre | string | Yanıttaki satırları filtreleyen bir veya daha fazla deyim. Her filtre ekstresi, yanıt gövdesinden bir alan adı ve **`eq`** , **`ne`** veya belirli alanlar için, işleci ile ilişkili bir değer içerir **`contains`** . Deyimler, veya kullanılarak birleştirilebilir **`and`** **`or`** . Dize değerleri, **filtre** parametresindeki tek tırnak işaretleriyle çevrelenmelidir. Filtrelenebilir alanların listesi ve bu alanlarla Desteklenen işleçler için aşağıdaki bölüme bakın. |
| aggregationLevel | string | Toplam verilerinin alınacağı zaman aralığını belirtir. Şu dizelerden biri olabilir: **gün**, **hafta** veya **ay**. Değer belirtilmezse, varsayılan olarak **Dadterange** olur. Bu parametre yalnızca, **GroupBy** parametresinin bir parçası olarak bir tarih alanı geçirildiğinde geçerlidir. |
| Ölçütü | string | Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [**abonelik**](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
{
    "customerTenantId": "76906668-27FC-4F5B-A35C-75A9823E13AF",
    "customerName": "TESTORG65656565",
    "customerMarket": "US",
    "id": "4BF546B2-8998-4838-BEE2-5F1BBE65A04F",
    "status": "ACTIVE",
    "productName": "OFFICE 365 BUSINESS PREMIUM",
    "subscriptionType": "Office",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "FULL OFFICE SUITE",
    "partnerName": "Partner Name",
    "providerName": "Provider Name",
    "creationDate": "2016-02-04T19:29:38.037",
   "effectiveStartDate": "2016-02-04T00:00:00",
    "commitmentEndDate": "2019-02-10T00:00:00",
    "currentStateEndDate": "2019-02-10T00:00:00",
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": "2018-02-10T02:39:57.729",
    "licenseCount": 2,
    "churnRisk": "High",
    "billingCycleName": "MONTHLY"

}
```

## <a name="see-also"></a>Ayrıca bkz.

- [İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
