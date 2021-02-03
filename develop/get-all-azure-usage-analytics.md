---
title: Tüm Azure kullanım analizi bilgilerini alma
description: Tüm Azure kullanım analizi bilgilerini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c281dcdeb93771a69a388ad64e1127b24156c809
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769442"
---
# <a name="get-all-azure-usage-analytics-information"></a>Tüm Azure kullanım analizi bilgilerini alma

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Müşterileriniz için tüm Azure kullanım analizi bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si |
|---------|-------------|
| **Al** | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analysistics/Usage/Azure http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

|Parametre        |Tür                        |Description               |
|:----------------|:---------------------------|:-------------------------|
|top              | string                     | İstekte döndürülecek veri satır sayısı. Belirtilen en büyük değer ve varsayılan değer 10000 ' dir. Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.                        |
|Atla             | int                        | Sorgudaki atlanacak satır sayısı. Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın. Örneğin, `top=10000 and skip=0` ilk 10000 veri satırını alır, `top=10000 and skip=10000` sonraki 10000 veri satırını alır ve bu şekilde devam eder.                       |
|filtre           | string                     | İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor. Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir `eq` `ne` ve deyimler or kullanılarak birleştirilebilir `and` `or` . Aşağıdaki dizeleri belirtebilirsiniz:<br/><br/>                                                       `customerTenantId`<br/> `customerName`<br/> `subscriptionId`<br/> `subscriptionName`<br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>**Örnek:**<br/> `.../usage/azure?filter=meterCategory eq 'Data Management'`<br/><br/> **Örnek:**<br/>`.../usage/azure?filter=meterCategory eq 'Data Management' or (usageDate le cast('2018-01-01', Edm.DateTimeOffset) and usageDate le cast('2018-04-01', Edm.DateTimeOffset))`                        |
|aggregationLevel | string                    | Toplam verilerinin alınacağı zaman aralığını belirtir. Aşağıdaki dizelerden biri olabilir: `day` , `week` , veya `month` . Belirtilmemişse, varsayılan olur `day` .<br/><br/>                                              `aggregationLevel`Parametresi, olmadan desteklenmez `groupby` . `aggregationLevel`Parametresi, içinde bulunan tüm tarih alanları için geçerlidir `groupby` .                                                      |
|OrderBy          |string                     | Her bir yüklemenin sonuç verileri değerlerini sıralayan bir ifade. Söz dizimi `...&orderby=field [order],field [order],...` şeklindedir. `field`Parametresi aşağıdaki dizelerden biri olabilir:<br/><br/>                    `customerTenantId`<br/>`customerName`<br/>`subscriptionId`<br/>`subscriptionName`<br/>`usageDate`<br/>`resourceLocation`<br/>`meterCategory`<br/>`meterSubcategory`<br/>`meterUnit`<br/> `reservationOrderId` <br/> `reservationId`<br/> `consumptionMeterId` <br/> `serviceType` <br/><br/> *Order* parametresi isteğe bağlıdır ve `asc` `desc` sırasıyla her bir alan için artan veya azalan sıralama belirtmek için ya da olabilir. Varsayılan değer: `asc`.<br/><br/>**Örnek:**<br/> `...&orderby=meterCategory,meterUnit`                                                                                           |
|ölçütü          |string                    | Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>                                                                                                                     `customerTenantId`<br/>`customerName`<br/> `subscriptionId` <br/> `subscriptionName` <br/> `usageDate` <br/> `resourceLocation` <br/> `meterCategory` <br/> `meterSubcategory` <br/> `meterUnit` <br/> `reservationOrderId` <br/> `reservationId` <br/> `consumptionMeterId` <br/> `serviceType` <br/><br/>Döndürülen veri satırları, parametresinde belirtilen alanları ve `groupby` *miktarı* içerir.<br/><br/>`groupby`Parametresi parametresiyle birlikte kullanılabilir `aggregationLevel` .<br/><br/>**Örnek:**<br/>`...&groupby=meterCategory,meterUnit` |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/usage/azure HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi bir [Azure kullanım](partner-center-analytics-resources.md#csp-program-azure-usage-analytics) kaynakları koleksiyonu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
{
  "customerTenantId": "39A1DFAC-4969-4F31-AF94-D76588189CFE",
  "customerName": "A",
  "subscriptionId": "EC649980-D623-49F5-B7C1-80CC772B83A8",
  "subscriptionName": "AZURE PURCHSE SAMPLE APP",
  "usageDate": "2018-05-27T00:00:00",
  "resourceLocation": "useast",
  "meterCategory": "Data Management",
  "meterSubcategory": "None",
  "meterUnit": "10,000s",
  "reservationOrderId": "",
  "reservationId": "",
  "consumptionMeterId": "",
  "serviceType": "",
  "quantity": 20
}
```

## <a name="see-also"></a>Ayrıca bkz.

- [İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
