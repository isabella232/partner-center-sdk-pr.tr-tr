---
title: Tüm abonelik analizi bilgilerini alma
description: Tüm abonelik analizi bilgilerini alma.
ms.date: 08/02/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: 5c93f36491851be11c700388201443f2e951122e4129786abc3e064091605b8d
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115992611"
---
# <a name="get-all-subscription-analytics-information"></a>Tüm abonelik analizi bilgilerini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Bu makalede, müşterileriniz için tüm abonelik analizi bilgilerini alma açıklanmıştır.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem | İstek URI'si |
|--------|-------------|
| **Al** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions HTTP/1.1 |

#### <a name="uri-parameters"></a>URI parametreleri

Aşağıdaki tabloda isteğe bağlı parametreler ve açıklamaları liste almaktadır:

| Parametre | Tür |  Description |
|-----------|------|--------------|
| top | int | İstekte geri dönecek veri satırlarının sayısı. Değer belirtilmezse, maksimum değer ve varsayılan değer `10000` olur. Sorguda daha fazla satır varsa yanıt gövdesi, sonraki veri sayfasını talep etmek için kullanabileceğiniz bir sonraki bağlantı içerir. |
| Atla | int | Sorguda atlana satır sayısı. Büyük veri kümelerini sayfalara yapmak için bu parametreyi kullanın. Örneğin, ilk 10000 veri satırı alınır ve sonraki `top=10000` `skip=0` `top=10000` `skip=10000` 10000 veri satırı alınır. |
| filtre | string | Yanıtta satırları filtreleen bir veya daha fazla deyim. Her filtre deyimi, yanıt gövdesinden bir alan adı ve , veya belirli alanlar **`eq`** **`ne`** için işleciyle ilişkili bir değer **`contains`** içerir. deyimleri veya kullanılarak **`and`** birleştirilmiş **`or`** olabilir. Dize değerlerinin filtre parametresinde tek tırnak içine **alınarak çevrelenmiş olması** gerekir. Filtrelenmiş alanların listesi ve bu alanlarda desteklenen işleçler için aşağıdaki bölüme bakın. |
| aggregationLevel | string | Toplama verilerini almak için zaman aralığını belirtir. Şu dizelerden biri olabilir: **gün,** **hafta** veya **ay.** Değer belirtilmezse varsayılan değer **dateRange'dır.** Bu parametre yalnızca **groupBy** parametresinin bir parçası olarak bir tarih alanı geçir kullanıldığında geçerlidir. |
| Groupby | string | Yalnızca belirtilen alanlara veri toplaması uygulanan bir deyim. |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, yanıt gövdesi Abonelik kaynaklarının bir [**koleksiyonunu**](partner-center-analytics-resources.md#subscription-resource) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

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
