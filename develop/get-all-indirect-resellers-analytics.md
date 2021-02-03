---
title: Tüm dolaylı satıcı analiz bilgilerini alma
description: Tüm dolaylı satıcılar analiz bilgilerini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 9f9c030278ba8fef9090f7be89064ac6054129ef
ms.sourcegitcommit: d53d300dc7fb01aeb4ef85bf2e3a6b80f868dc57
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/14/2020
ms.locfileid: "97769443"
---
# <a name="get-all-indirect-resellers-analytics-information"></a>Tüm dolaylı satıcı analiz bilgilerini alma

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Müşterileriniz için tüm dolaylı satıcılar analiz bilgilerini alma.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="rest-request"></a>REST isteği

### <a name="request-syntax"></a>İstek sözdizimi

| Yöntem  | İstek URI'si |
|---------|-------------|
| **Al** | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/ındirectsatıcıları http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

| Parametre                             | Tür     | Description                              |
|:--------------------------------------|:---------|:-----------------------------------------|
| Partnertenantıd                       | string   | Dolaylı satıcıların verilerini almak istediğiniz ortağın kiracı KIMLIĞI. |
| kimlik                                    | string   | Dolaylı satıcı KIMLIĞI                                                                 |
| name                                  | string   | Dolaylı satıcıların verilerini almak istediğiniz iş ortağının adı.      |
| pazara                                | string   | Dolaylı satıcıların verilerini almak istediğiniz iş ortağının pazarı.    |
| firstSubscriptionCreationDate         | UTC Tarih saat biçiminde dize  | Dolaylı satıcıların verilerini almak istediğiniz ilk aboneliğin Oluşturulma tarihi.  |
| latestSubscriptionCreationDate        | UTC Tarih saat biçiminde dize  | En son aboneliğin Oluşturulma tarihi.                 |
| firstSubscriptionEndDate              | UTC Tarih saat biçiminde dize  | Herhangi bir aboneliğin sonlandırılması ilk kez.                        |
| latestSubscriptionEndDate             | UTC Tarih saat biçiminde dize  | Herhangi bir aboneliğin sonlandıralındığı en son tarih.                  |
| firstSubscriptionSuspendedDate        | UTC Tarih saat içinde dize         | Abonelikler ilk kez askıya alındı.                    |
| latestSubscriptionSuspendedDate       | UTC Tarih saat biçiminde dize  | Herhangi bir aboneliğin askıya alındığı en son tarih.              |
| firstSubscriptionDeprovisionedDate    | UTC Tarih saat biçiminde dize  | İlk kez bir abonelik sağlanmamıştır.                |
| latestSubscriptionDeprovisionedDate   | UTC Tarih saat biçiminde dize  | Herhangi bir aboneliğin sağlaması kaldırılmış olan en son tarih.          |
| Abonelik sayısı                     | double   | Tüm değer eklenmiş satıcıların abonelik sayısı                                     |
| licenseCount                          | double   | Tüm değer eklenmiş satıcıların lisans sayısı.                                         |
| ındirectresellercount                 | double   | Dolaylı satıcıların sayısı                                                             |
|  top                                  | string   | İstekte döndürülecek veri satır sayısı. Belirtilen en büyük değer ve varsayılan değer 10000 ' dir. Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.  |
| Atla                                  | int      | Sorgudaki atlanacak satır sayısı. Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın. Örneğin, **`top=10000 and skip=0`** ilk 10000 veri satırını alır, **`top=10000 and skip=10000`** sonraki 10000 veri satırını alır ve bu şekilde devam eder.              |
| filtre                                | string   | İsteğin *filtre* parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor. Her deyim, veya işleçleriyle ilişkili bir alan ve değer içerir **`eq`** **`ne`** ve deyimler or kullanılarak birleştirilebilir **`and`** **`or`** . Aşağıdaki alanları belirtebilirsiniz:<br/><br/>     *Partnertenantıd*<br/> *id*<br/> *Ad*<br/>                *pazara*<br/> *firstSubscriptionCreationDate*<br/> *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>         **Örnek:**<br/>              `.../indirectresellers?filter=market eq 'US'`<br/><br/>            **Örnek:**<br/>                `.../indirectresellers?filter=market eq 'US' or (firstSubscriptionCreationDate le cast('2018-01-01',Edm.DateTimeOffset) and firstSubscriptionCreationDate le cast('2018-04-01',Edm.DateTimeOffset))` |              
| aggregationLevel                     | string    | Toplam verilerinin alınacağı zaman aralığını belirtir. Şu dizelerden biri olabilir: &quot; gün &quot; , &quot; hafta &quot; veya &quot; ay &quot; . Belirtilmemişse, varsayılan olarak gün olur &quot; &quot; .<br/><br/>                                 `aggregationLevel` , olmadan desteklenmez `aggregationLevel` . `aggregationLevel` içinde bulunan tüm **datefields** için geçerlidir `aggregationLevel`                         |
| OrderBy                              | string    | Her bir yüklemenin sonuç verileri değerlerini sıralayan bir ifade. Söz dizimi `...&orderby=field[order],field [order],...` şeklindedir. Alan parametresi aşağıdaki dizelerden biri olabilir:<br/><br/>                &quot;Partnertenantıd&quot;<br/>                &quot;id&quot;<br/>                &quot;ada&quot;<br/>                &quot;pazara&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;Abonelik sayısı&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   *Order* parametresi isteğe bağlıdır ve veya, her bir `asc` `desc` alan için artan veya azalan sıralama belirtmek için ya da olabilir. Varsayılan değer: `asc`.<br/><br/>    **Örnek:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
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
