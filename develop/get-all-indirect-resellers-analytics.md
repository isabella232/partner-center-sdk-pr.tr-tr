---
title: Tüm dolaylı satıcı analiz bilgilerini alma
description: Tüm dolaylı kurumsal bayi analiz bilgilerini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 7a38fbf2c94bad5213a65159759ace54b9dd4595d5532ea97f2449f0ac5b41cd
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994073"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Tüm dolaylı satıcı analiz bilgilerini alma

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Müşterileriniz için tüm dolaylı kurumsal bayi analiz bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek söz dizimi

| Yöntem  | İstek URI'si |
|---------|-------------|
| **Al** | [*\{ baseURL \}*](partner-center-rest-urls.md)/partner/v1/analytics/indirectresellers HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

| Parametre                             | Tür     | Description                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| partnerTenantId                       | string   | Dolaylı kurumsal bayi verilerini almak istediğiniz iş ortağının Kiracı Kimliği. |
| kimlik                                    | string   | Dolaylı kurumsal bayi kimliği                                                                 |
| name                                  | string   | Dolaylı kurumsal bayi verilerini almak istediğiniz iş ortağının adı.      |
| Pazar                                | string   | Dolaylı kurumsal bayi verilerini almak istediğiniz iş ortağının Marketi.    |
| firstSubscriptionCreationDate         | UTC tarih saat biçiminde dize  | Dolaylı kurumsal bayi verilerini almak istediğiniz ilk aboneliğin oluşturma tarihi.  |
| latestSubscriptionCreationDate        | UTC tarih saat biçiminde dize  | En son aboneliğin oluşturma tarihi.                 |
| firstSubscriptionEndDate              | UTC tarih saat biçiminde dize  | Herhangi bir abonelik ilk kez sona erer.                        |
| latestSubscriptionEndDate             | UTC tarih saat biçiminde dize  | Herhangi bir aboneliğin son bitiş tarihi.                  |
| firstSubscriptionSuspendedDate        | UTC tarih saat dizesi         | Herhangi bir abonelik ilk kez askıya alınmıştır.                    |
| latestSubscriptionSuspendedDate       | UTC tarih saat biçiminde dize  | Herhangi bir aboneliğin askıya alınarak son tarihi.              |
| firstSubscriptionDeprovisionedDate    | UTC tarih saat biçiminde dize  | İlk kez bir aboneliğinvision'ları silindi.                |
| latestSubscriptionDeprovisionedDate   | UTC tarih saat biçiminde dize  | Herhangi bir aboneliğin onaysız olduğu en son tarih.          |
| subscriptionCount                     | double   | Eklenen tüm değerli kurumsal bayiler için abonelik sayısı                                     |
| licenseCount                          | double   | Eklenen tüm değerli kurumsal bayiler için lisans sayısı.                                         |
| indirectResellerCount                 | double   | Dolaylı kurumsal bayi sayısı                                                             |
|  top                                  | string   | İstekte geri dönecek veri satırlarının sayısı. Belirtilmezse en büyük değer ve varsayılan değer 10000'tir. Sorguda daha fazla satır varsa yanıt gövdesi, sonraki veri sayfasını talep etmek için kullanabileceğiniz bir sonraki bağlantı içerir.  |
| Atla                                  | int      | Sorguda atlana satır sayısı. Büyük veri kümelerini sayfalara yapmak için bu parametreyi kullanın. Örneğin, **`top=10000 and skip=0`** verilerin ilk 10000 satırı alınır, sonraki 10000 satır veri alınır ve **`top=10000 and skip=10000`** bu şekilde devam ediyor.              |
| filtre                                | string   | *İsteğin* filtre parametresi, yanıtta satırları filtreleen bir veya daha fazla deyim içerir. Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir ve **`eq`** **`ne`** deyimleri veya kullanılarak bir **`and`** araya **`or`** olabilir. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>     *partnerTenantId*<br/> *id*<br/> *Ad*<br/>                *Pazar*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Örnek:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Örnek:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | string    | Toplama verilerini almak için zaman aralığını belirtir. Şu dizelerden biri olabilir: &quot; &quot; gün, &quot; hafta veya &quot; &quot; &quot; ay. Belirtilmezse, varsayılan gün &quot; &quot; olur.<br/><br/>                                 `aggregationLevel` olmadan `aggregationLevel` desteklenmiyor. `aggregationLevel` , içinde mevcut **olan tüm tarih** alanlara uygulanır `aggregationLevel`                         |
| Orderby                              | string    | Her bir yüklemenin sonuç verileri değerlerini sıralayan bir ifade. Söz dizimi `...&orderby=field[order],field [order],...` şeklindedir. Alan parametresi aşağıdaki dizelerden biri olabilir:<br/><br/>                &quot;Partnertenantıd&quot;<br/>                &quot;id&quot;<br/>                &quot;ada&quot;<br/>                &quot;pazara&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;Abonelik sayısı&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   *Order* parametresi isteğe bağlıdır ve veya, her bir `asc` `desc` alan için artan veya azalan sıralama belirtmek için ya da olabilir. Varsayılan değer: `asc`.<br/><br/>    **Örnek:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| ölçütü                              | string    | Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>         *Partnertenantıd*<br/>    *id*<br/>               *Ad*<br/>                *pazara*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 Döndürülen veri satırları, `groupby` yan tümcesinde belirtilen alanları ve aşağıdaki alanları içerir:<br/><br/>            *ındirectresellercount*<br/>                *licenseCount*<br/>                *Abonelik sayısı*<br/><br/>            `groupby`Parametresi parametresiyle birlikte kullanılabilir `aggregationLevel` .<br/><br/>            **Örnek:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/indirectresellers HTTP 1.1
Authorization: Bearer <token>
Accept: application/json
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, yanıt gövdesi [dolaylı satıcıların](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) kaynakları koleksiyonunu içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [hata kodları](error-codes.md).

### <a name="response-example"></a>Yanıt örneği

```http
{
    "partnerTenantId": "AAAAAAAA-BBBB-CCCC-DDDD-EEEEEEEEEEEE",
    "id": "1111111",
    "name": "RESELLER NAME",
    "market": "US",
    "firstSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "latestSubscriptionCreationDate": "2016-10-18T19:16:25.107",
    "firstSubscriptionEndDate": "2018-11-07T00:00:00",
    "latestSubscriptionEndDate": "2018-11-07T00:00:00",
    "firstSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "latestSubscriptionSuspendedDate": "0001-01-01T00:00:00",
    "firstSubscriptionDeprovisionedDate": "0001-01-01T00:00:00",
    "latestSubscriptionDeprovisionedEndDate": "0001-01-01T00:00:00",
    "subscriptionCount": 10,
    "licenseCount": 20
}
```

## <a name="see-also"></a>Ayrıca bkz.

- [İş Ortağı Merkezi Analizi - Kaynaklar](partner-center-analytics-resources.md)
