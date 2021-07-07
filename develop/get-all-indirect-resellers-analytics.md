---
title: Tüm dolaylı satıcı analiz bilgilerini alma
description: Tüm dolaylı kurumsal bayi analiz bilgilerini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 4252f5fcbbcb038f382408074c8fd6ede3fd1f58
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760751"
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

| Parametre                             | Tür     | Açıklama                              |
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
| Orderby                              | string    | Her yükleme için sonuç veri değerlerini sipariş alan bir deyim. Söz dizimi `...&orderby=field[order],field [order],...` şeklindedir. alan parametresi aşağıdaki dizelerden biri olabilir:<br/><br/>                &quot;partnerTenantId&quot;<br/>                &quot;id&quot;<br/>                &quot;Adı&quot;<br/>                &quot;Pazar&quot;<br/>                &quot;firstSubscriptionCreationDate&quot;<br/>               &quot;latestSubscriptionCreationDate&quot;<br/>                &quot;firstSubscriptionEndDate&quot;<br/>               &quot;latestSubscriptionEndDate&quot;<br/>                &quot;firstSubscriptionSuspendedDate&quot;<br/>                &quot;latestSubscriptionSuspendedDate&quot;<br/>               &quot;firstSubscriptionDeprovisionedDate&quot;<br/>                &quot;latestSubscriptionDeprovisionedDate&quot;<br/>                &quot;subscriptionCount&quot;<br/>                &quot;licenseCount&quot;<br/><br/>   Order *parametresi* isteğe bağlıdır ve her alan için artan veya azalan düzen belirtmek için veya `asc` `desc` olabilir. Varsayılan değer: `asc`.<br/><br/>    **Örnek:**<br/>                `...&orderby=market,subscriptionCount`                                       |                   
| Groupby                              | string    | Yalnızca belirtilen alanlara veri toplaması uygulanan bir deyim. Aşağıdaki alanları belirtebilirsiniz:<br/><br/>         *partnerTenantId*<br/>    *id*<br/>               *Ad*<br/>                *Pazar*<br/>                *firstSubscriptionCreationDate*<br/>                *latestSubscriptionCreationDate*<br/>                *firstSubscriptionEndDate*<br/>                *latestSubscriptionEndDate*<br/>                *firstSubscriptionSuspendedDate*<br/>                *latestSubscriptionSuspendedDate*<br/>                *firstSubscriptionDeprovisionedDate*<br/>                *latestSubscriptionDeprovisionedDate*<br/><br/>                 Döndürülen veri satırları yan tümcesinde belirtilen `groupby` alanları ve aşağıdaki alanları içerir:<br/><br/>            *indirectResellerCount*<br/>                *licenseCount*<br/>                *subscriptionCount*<br/><br/>            `groupby`parametresiyle `aggregationLevel` birlikte kullanılabilir.<br/><br/>            **Örnek:**</br>               `...&groupby=ageGroup,market&aggregationLevel=week`                         |

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

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

Başarılı olursa, yanıt gövdesi dolaylı kurumsal bayi [kaynaklarının bir koleksiyonunu](partner-center-analytics-resources.md#csp-program-indirect-resellers-analytics) içerir.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir. Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Hata Kodları.](error-codes.md)

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
