---
title: Microsoft Müşteri Sözleşmesi şablonu için indirme bağlantısı oluşturma
description: Şablon için bir indirme Microsoft Müşteri Sözleşmesi edinebilirsiniz.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: 7757cd6a92c168e4209d2d3ac49746e4a0907021d260a7b49603a3706e8cfa5c
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994821"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Microsoft Müşteri Sözleşmesi şablonu için indirme bağlantısı oluşturma

**Için geçerlidir:** İş Ortağı Merkezi

**için geçerli değildir:** İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

**AgreementDocument kaynağı** şu anda yalnızca Microsoft İş Ortağı Merkezi bulut üzerinde kullanılabilir.

Bu makalede, müşterinin ülke ve diline göre Microsoft Müşteri Sözleşmesi şablonu indirme bağlantısının nasıl elde etmek istediğiniz açıklanmıştır.

## <a name="prerequisites"></a>Önkoşullar

- İş Ortağı Merkezi .NET SDK kullanıyorsanız sürüm 1.14 veya daha yenisi gereklidir.

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](./partner-center-authentication.md) Bu senaryo yalnızca App+User kimlik doğrulamasını destekler.

- Müşterinin uygulama şablonunun uygulandığı Microsoft Müşteri Sözleşmesi.

- Uygulama şablonunun yerel Microsoft Müşteri Sözleşmesi dili.

> [!IMPORTANT]
>
> - Bu Microsoft Müşteri Sözleşmesi ülkeye özgü bir veridir. Microsoft Müşteri Sözleşmesi şablonunu indirmek için bağlantı isteği Microsoft Müşteri Sözleşmesi, müşterinin konumunu temel alarak doğru ülkeyi belirttiğinizden emin olun. veya desteklenen ülkelerin listesi için [bkz. Desteklenen ülkeler ve diller listesi.](#list-of-supported-countries-and-languages)
>
> - Bazı ülkelerde, Microsoft Müşteri Sözleşmesi dillerde kullanılabilir. En iyi müşteri deneyimi için müşterinin ihtiyaçlarına en uygun dili seçin. Desteklenen dillerin listesi için bkz. [Desteklenen ülkeler ve diller listesi.](#list-of-supported-countries-and-languages)
> - Bu yöntem yalnızca Microsoft Müşteri Sözleşmesi.

## <a name="net"></a>.NET

Uygulama şablonunu indirme bağlantısını Microsoft Müşteri Sözleşmesi:

1. Veri kaynağı için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi. Uygulamanın **templateId'lerini** Microsoft Müşteri Sözleşmesi. Daha fazla bilgi için [bkz. Microsoft Müşteri Sözleşmesi.](get-customer-agreement-metadata.md)

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. IAggregatePartner.AgreementTemplates koleksiyonunu kullanın.

3. **ById yöntemini** çağırarak uygulamanın **templateId** Microsoft Müşteri Sözleşmesi.

4. Document **özelliğini** getirme.

5. **ByCountry yöntemini** çağırarak müşterinin anlaşma şablonunun geçerli olduğu ülkeyi belirtin. Yöntemi belirtilmezse *sorgu* varsayılan olarak ABD'ye kullanılır. Desteklenen ülke kodlarının listesi için bkz. [Desteklenen ülkeler ve diller listesi.](#list-of-supported-countries-and-languages) Bu yöntem **büyük/büyük/büyük harfe duyarlıdır.**

6. **ByLanguage yöntemini** çağırarak anlaşma şablonunun yerelleştirilmiş olması gereken dili belirtin. Yöntem belirtilmemişse veya belirtilen ülke kodu belirtilen ülke için desteklenmiyorsa sorgu varsayılan olarak *en-US* olur. Desteklenen dil kodlarının listesi için desteklenen ülkeler [ve diller listesi'ne bakın.](#list-of-supported-countries-and-languages)

7. **Get** veya **GetAsync yöntemini** çağırma.

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

Eksiksiz bir örnek, konsol test uygulaması [projesinden GetAgreementDetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) [sınıfında](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) bulunabilir.

## <a name="rest-request"></a>REST isteği

Uygulama şablonunu indirme bağlantısını Microsoft Müşteri Sözleşmesi:

1. Veri kaynağı için sözleşme meta verilerini Microsoft Müşteri Sözleşmesi. Uygulamanın **templateId'lerini** Microsoft Müşteri Sözleşmesi. Daha fazla bilgi için [bkz. Microsoft Müşteri Sözleşmesi.](get-customer-agreement-metadata.md)

2. [ **Bir AgreementDocument**](./agreement-document-resources.md)kaynağını getirmek için REST isteği oluşturun. Örnek için istek söz [dizimi örneğine](#request-syntax) bakın. Aşağıdaki bilgileri belirtmeniz gerekir:

    - Uygulamanın **templateId** Microsoft Müşteri Sözleşmesi.
    - Uygulama şablonunun Microsoft Müşteri Sözleşmesi ülke.
    - Uygulama şablonunun yerel Microsoft Müşteri Sözleşmesi dili.

### <a name="request-syntax"></a>İstek söz dizimi

Bu kaynak için aşağıdaki istek söz dizimlerini kullanın:

| Yöntem | İstek URI'si |
|--------|---------------------------------------------------------------------|
| GET | [*\{ baseURL \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{agreement-template-id}/document?language={language}&country={country} HTTP/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

İsteğiniz ile aşağıdaki URI parametrelerini kullanabilirsiniz:

| Ad                   | Tür   | Gerekli | Açıklama                                 |
|------------------------|--------|----------|---------------------------------------------|
| agreement-template-id  | string | Yes      | Anlaşma türünün benzersiz tanımlayıcısı. Microsoft Müşteri Sözleşmesi için templateId'Microsoft Müşteri Sözleşmesi. Daha fazla bilgi için [bkz. Microsoft Müşteri Sözleşmesi.](./get-customer-agreement-metadata.md) Bu parametre **büyük/büyük/büyük harfe duyarlıdır.**|
| ülke                | dize | No       | Anlaşma şablonunun uygulandığı ülkeyi gösterir. Parametresi *belirtilmezse sorgu* varsayılan olarak ABD olur. Desteklenen ülke kodlarının listesi için bkz. [Desteklenen ülkeler ve diller listesi.](#list-of-supported-countries-and-languages)|
| language               | dize | No       | Anlaşma şablonunun yerelleştirilmiş olması gereken dili gösterir. Parametresi belirtilmemişse veya içinde belirtilen ülke kodu belirtilen ülke için desteklenmiyorsa sorgu varsayılan olarak *en-US* olur. Desteklenen ülke kodlarının listesi için [bkz. Desteklenen ülkeler ve diller listesi.](#list-of-supported-countries-and-languages)|

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)

### <a name="request-body"></a>İstek gövdesi

Yok.

### <a name="request-example"></a>İstek örneği

```http
GET https://api.partnercenter.microsoft.com/v1/agreementtemplates/117a77b0-9360-443b-8795-c6dedc750cf9/document?language=en-US&country=US HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
```

## <a name="rest-response"></a>REST yanıtı

Başarılı olursa, bu yöntem yanıt [ **gövdesinde** bir AgreementDocument](./agreement-document-resources.md) kaynağı döndürür.

Kaynağın, anlaşma şablonunu indirmek için kullanılan bir URL dizesi içeren **bir downloadUri** özelliği vardır. Her sorguda farklı bir bağlantı döndürülür. Bu bağlantının süresi beş dakika sonra dolar.

### <a name="response-success-and-error-codes"></a>Yanıt başarı ve hata kodları

Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)

### <a name="response-example"></a>Yanıt örneği

```http
HTTP/1.1 200 OK
Content-Length: 620
Content-Type: application/json
MS-RequestId: 94e4e214-6b06-4fb7-96d1-94d559f9b47f
MS-CorrelationId: ab993325-1605-4cf4-bac4-fb584142a31b
{
    "displayUri":"https://wopihost.int.l2o.microsoft.com/v1/officehost/agreement/files/Preview...",
    "downloadUri":"https://l2oagreementintbn2.blob.core.windows.net/agreementscontainer/Preview...",
    "language":"en-US",
    "country":"US"
}
```

## <a name="list-of-supported-countries-and-languages"></a>Desteklenen ülkeler ve diller listesi

> [!IMPORTANT]
> Ülke kodu özelliği büyük/büyük/büyük harfe duyarlıdır. Lütfen aşağıdaki tabloda belirtilen doğru büyük/büyük/büyük/altta belirtilen büyük/alta doğru büyük/büyük/alta doğru büyük/büyük/altta belirtilen büyük/alta doğru büyük/alta doğru büyük

| Ülke                   | Ülke kodu   | Desteklenen dil kodu |
|------------------------|--------|----------|
| Åland Adaları | Ax | en-US |
| Afganistan | AF | en-US |
| Arnavutluk | AL | en-US |
| Cezayir | DZ | en-US, fr-FR, en-US |
| Amerikan Samoası | AS | en-US |
| Andorra | AD | en-US |
| Angola | AO | en-US, pt-PT |
| Anguilla | AI | en-US |
| Antarktika | Aq | en-US |
| Antigua ve Barbuda | AG | en-US |
| Arjantin | AR | en-US, es-ES |
| Ermenistan | AM | en-US |
| Aruba | AW | en-US |
| Avustralya | AU | en-US |
| Avusturya | AT | en-US, de-DE |
| Azerbaycan | AZ | en-US |
| Bahamalar | BS | en-US |
| Bahreyn | BH | en-US, ar-SA |
| Bangladeş | BD | en-US |
| Barbados | BB | en-US |
| Belarus | BY | en-US, ru-RU |
| Belçika | BE | en-US, nl-NL |
| Belize | BZ | en-US, es-ES |
| Benin | BJ | en-US |
| Bermuda | BM | en-US |
| Butan | BT | en-US |
| Bolivya | BO | en-US, es-ES |
| Bonaire | Bq | en-US |
| Bosna-Hersek | BA | en-US |
| Botsvana | BW | en-US |
| Bouvet Adası | Bv | en-US |
| Brezilya | BR | en-US, pt-BR |
| Britanya Hint Okyanusu Toprakları | ıo | en-US |
| Britanya Virjin Adaları | VG | en-US |
| Brunei | BN | en-US |
| Bulgaristan | BG | en-US, BG-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Fildişi Sahili (Côte d'Ivoire) | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, PT NK |
| Kamboçya | KH | en-US |
| Kamerun | CM | en-US, fr-FR |
| Kanada | CA | en-US, fr-FR |
| Cayman Adaları | KY | en-US, en-US |
| Orta Afrika Cumhuriyeti | CF | en-US |
| Çad | TD | en-US |
| Şili | CL | en-US, ES-ES |
| Christmas Adası | CX | en-US |
| Cocos (Keeling) Adaları | CC | en-US |
| Kolombiya | CO | en-US, ES-ES |
| Komorlar | KM | en-US |
| Kongo (KDC) | CD | en-US |
| Kongo Cumhuriyeti | ILETISI | en-US |
| Cook Adaları | STOKLAMA | en-US |
| Kosta Rika | CR | en-US, ES-ES |
| Hırvatistan | HR | en-US, HR-HR |
| Curaçao | FIILI | en-US |
| Kıbrıs | CY | en-US |
| Czechia | CZ | en-US, CS-CZ |
| Danimarka | DK | en-US, da-DK |
| Cibuti | DJ | en-US |
| Dominika | DM | en-US |
| Dominik Cumhuriyeti | DO | en-US, ES-ES |
| Ekvador | EC | en-US |
| Mısır | EG | en-US, ar-SA |
| El Salvador | SV | en-US, ES-ES |
| Ekvator Ginesi | GQ | en-US |
| Eritre | ER | en-US |
| Estonya | EE | en-US, et-EE |
| eSwatini | SZ | en-US |
| Etiyopya | ET | en-US |
| Falkland Adaları | Fk | en-US |
| Faroe Adaları | Fo | en-US |
| Fiji | FJ | en-US |
| Finlandiya | FI | en-US, fi-FI |
| Fransa | GS | en-US, fr-FR |
| Fransız Guyanası | GF | en-US, fr-FR  |
| Fransız Polinezyası | PF | en-US |
| Fransız Güney Toprakları | Tf | en-US |
| Gabon | GA | en-US |
| Gambiya | GM | en-US |
| Gürcistan | GE | en-US |
| Almanya | DE | en-US, de-DE |
| Gana | GH | en-US |
| Cebelitarık | Gı | en-US |
| Yunanistan | GR | en-US, el-GR |
| Grönland | Gl | en-US |
| Grenada | Gd | en-US |
| Guadeloupe | GP | en-US |
| Guam | GU | en-US |
| Guatemala | GT | en-US, es-ES |
| Guernsey | Gg | en-US |
| Gine | GN | en-US |
| Gine-Bissau | Gw | en-US |
| Guyana | GY | en-US |
| Haiti | HT | en-US |
| Heard Adası ve McDonald Adaları | Hm | en-US |
| Honduras | HN | en-US, es-ES |
| Hong Kong ÖİB | HK | en-US, zh-HK |
| Macaristan | HU | en-US, hu-HU |
| İzlanda | IS | en-US |
| Hindistan | IN | en-US, hi-IN |
| Endonezya | ID | en-US, id-ID |
| Irak | IQ | en-US, ar-SA |
| İrlanda | IE | en-US |
| Man Adası | Anlık İleti | en-US |
| İsrail | IL | en-US, he-IL |
| İtalya | BT | en-US, it-IT |
| Jamaika | JM | en-US |
| Jan Mayen | Xj | en-US |
| Japonya | JP | en-US, ja-JP |
| Jersey | Je | en-US |
| Ürdün | JO | en-US, ar-SA |
| Kazakistan | KZ | en-US, kk-KZ |
| Kenya | KE | en-US |
| Kiribati | KI | en-US |
| Güney Kore | KR | en-US, ko-KR |
| Kosova | Xk | en-US |
| Kuveyt | KW | en-US, ar-SA |
| Kırgızistan | KG | en-US, ru-RU |
| Laos | LA | en-US |
| Letonya | LV | en-US, lv-LV |
| Lübnan | LB | en-US, ar-SA |
| Lesotho | LS | en-US |
| Liberya | LR | en-US |
| Libya | LY | en-US, ar-SA |
| Liechtenstein | LI | en-US, de-DE |
| Litvanya | LT | en-US, lt-LT |
| Lüksemburg | LU | en-US, fr-FR |
| Makao ÖİB | MO | en-US, zh-HK |
| Kuzey Ve Kuzey Avrupa | MK | en-US |
| Madagaskar | MG | en-US |
| Malavi | MW | en-US |
| Malezya | MY | en-US, MS-MY |
| Maldivler | MV | en-US |
| Mali | ML | en-US |
| Malta | MT | en-US |
| Marshall Adaları | MH | en-US |
| Martinique | MQ | en-US |
| Moritanya | MR | en-US |
| Mauritius | MU | en-US, ar-SA |
| Mayotte | YT | en-US |
| Meksika | MX | en-US, ES-ES |
| Mikronezya | FM | en-US |
| Moldova | MD | en-US, RO-RO |
| Monako | MC | en-US, fr-FR |
| Moğolistan | MN | en-US |
| Karadağ | ME | en-US |
| Montserrat | MS | en-US |
| Fas | MA | en-US, fr-FR, en-US |
| Mozambik | MZ | en-US |
| Myanmar | MM | en-US |
| Namibya | NA | en-US |
| Nauru | NR | en-US |
| Nepal | NP | en-US |
| Hollanda | NL | en-US, nl-NL |
| Yeni Kaledonya | NC | en-US |
| Yeni Zelanda | NZ | en-US |
| Nikaragua | NI | en-US, ES-ES |
| Nijer | NE | en-US |
| Nijerya | NG | en-US |
| Niue | NU | en-US |
| Norfolk Adası | NF | en-US |
| Kuzey Mariana Adaları | MP | en-US |
| Norveç | NO | en-US, NB-NO |
| Umman | OM | en-US, ar-SA |
| Pakistan | PK | en-US |
| Palau | PW | en-US |
| Filistin Yönetimi | PS | en-US |
| Panama | PA | en-US, ES-ES |
| Papua Yeni Gine | PG | en-US |
| Paraguay | PY | en-US, ES-ES |
| Peru | PE | en-US, ES-ES |
| Filipinler | PH | en-US |
| Pitcairn Adaları | DÖNÜŞTÜRME | en-US |
| Polonya | PL | en-US, PL-PL |
| Portekiz | PT | en-US, PT NK |
| Porto Riko | PR | en-US, en-US |
| Katar | QA | en-US, ar-SA |
| Reunion | RE | en-US |
| Romanya | RO | en-US, RO-RO |
| Rusya | RU | en-US, ru-RU |
| Ruanda | RW | en-US, fr-FR |
| Sao Tome ve Principe | ST | en-US, fr-FR |
| Saba | X | en-US |
| Saint-Barthélemy | BL | en-US |
| Saint Kitts ve Nevis | KN | en-US |
| Saint Lucia | LC | en-US, en-US |
| Saint Martin | MF | en-US, en-US |
| Saint Pierre ve Miquelon | PM | en-US |
| Saint Vincent ve Grenadinler | VC | en-US |
| Samoa | WS | en-US |
| San Marino | SM | en-US |
| Suudi Arabistan | SA | en-US |
| Senegal | SN | en-US, fr-FR |
| Sırbistan | RS | en-US, sr-Latn-RS, en-US |
| Seyşeller | SC | en-US |
| Sierra Leone | SL | en-US |
| Singapur | SG | en-US, zh-SG |
| Sint Eustatius | KARMAŞıK | en-US |
| Sint Maarten | KÖK | en-US, en-US |
| Slovakya | SK | en-US, SK-SK |
| Slovenya | SI | en-US, SL-SI |
| Solomon Adaları | Ise | en-US |
| Somali | SO | en-US |
| Güney Afrika | ZA | en-US |
| Güney Georgia ve Güney Sandwich Adaları | NESNESIDIR | en-US |
| Güney Sudan | SS | en-US |
| İspanya | ES | en-US, ES-ES, en-US, en-US |
| Sri Lanka | LK | en-US |
| Saint Helena, Ascension ve Tristan da Cunha | SH | en-US |
| Surinam | SR | en-US |
| Svalbard | SJ | en-US |
| İsveç | SE | en-US, ZF-SE |
| İsviçre | CH | en-US, fr-FR, en-US, en-US |
| Tayvan | TW | en-US, zh-HK |
| Tacikistan | TJ | en-US |
| Tanzanya | TZ | en-US |
| Tayland | TH | en-US, TH-TH |
| Timor-Leste | TL | en-US |
| Togo | TG | en-US |
| Tokelau | TK | en-US |
| Tonga | TO | en-US |
| Trinidad ve Tobago | TT | en-US |
| Tunus | TN | en-US, fr-FR, en-US |
| Türkiye | TR | en-US, tr-TR |
| Türkmenistan | TM | en-US |
| Turks ve Caicos Adaları | TC | en-US |
| Tuvalu | TV | en-US |
| ABD harici Adaları | UM | en-US |
| ABD Virgin Adaları | VI | en-US |
| Uganda | UG | en-US |
| Ukrayna | UA | en-US, UK-UA |
| Birleşik Arap Emirlikleri | AE | en-US, ar-SA |
| Birleşik Krallık | GB | en-US |
| Birleşik Devletler | ABD | en-US |
| Uruguay | UY | en-US, ES-ES |
| Özbekistan | UZ | en-US, ru-RU |
| Vanuatu | Vu & lt | en-US |
| Vatikan | VA | en-US |
| Venezuela | VE | en-US, ES-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis ve Futuna | WF | en-US |
| Yemen | Vet | en-US, ar-SA |
| Zambiya | ZM | en-US |
| Zimbabve | ZW | en-US |
