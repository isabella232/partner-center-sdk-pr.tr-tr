---
title: Microsoft müşteri anlaşması şablonu için bir indirme bağlantısı alın
description: Microsoft Müşteri Sözleşmesi şablonu için bir indirme bağlantısı alın.
ms.date: 02/12/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: cychua
ms.author: cychua
ms.openlocfilehash: fccb9e3d4a837f3e8043f8c7ae1e3911d819afd7
ms.sourcegitcommit: d20e7d572fee09a83a4b23a92da7ff09cfebe75a
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111906529"
---
# <a name="get-a-download-link-for-the-microsoft-customer-agreement-template"></a>Microsoft müşteri anlaşması şablonu için bir indirme bağlantısı alın

**Uygulama hedefi**: Iş Ortağı Merkezi

**Şu şekilde geçerlidir**: 21Vianet tarafından çalıştırılan Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

**AgreementDocument** kaynağı şu anda yalnızca Microsoft genel bulutundaki Iş Ortağı Merkezi tarafından desteklenmektedir.

Bu makalede, müşterinin ülkesine ve diline bağlı olarak Microsoft müşteri anlaşması şablonunu indirme bağlantısının nasıl yapılacağı açıklanır.

## <a name="prerequisites"></a>Önkoşullar

- Iş ortağı merkezi .NET SDK kullanıyorsanız sürüm 1,14 veya daha yeni bir sürümü gereklidir.

- [Iş ortağı merkezi kimlik doğrulamasında](./partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryo yalnızca uygulama + kullanıcı kimlik doğrulamasını destekler.

- Müşterinin Microsoft müşteri anlaşması şablonunun geçerli olduğu ülke.

- Microsoft müşteri anlaşması şablonunun yerelleştirilmesi gereken dil.

> [!IMPORTANT]
>
> - Microsoft Müşteri Sözleşmesi ülkeye özeldir. Microsoft müşteri anlaşması şablonunu indirmek için bir bağlantı istendiğinde, müşterinin konumuna göre doğru ülkeyi belirttiğinizden emin olun. ya da desteklenen ülkelerin listesi, [Desteklenen ülkeler ve diller listesine](#list-of-supported-countries-and-languages)bakın.
>
> - Bazı ülkelerde, Microsoft Müşteri Sözleşmesi birden çok dilde kullanılabilir. En iyi müşteri deneyimi için müşterinin ihtiyaçlarına en iyi eşleşen dili seçin. Desteklenen dillerin listesi için [Desteklenen ülkeler ve diller listesine](#list-of-supported-countries-and-languages)bakın.
> - Bu yöntem yalnızca Microsoft Müşteri anlaşmasıyla desteklenir.

## <a name="net"></a>.NET

Microsoft müşteri anlaşması şablonunu indirmek için bir bağlantı almak üzere:

1. Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın. Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir. Daha fazla bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).

   ```csharp
   // IAggregatePartner partnerOperations;

   string agreementType = "MicrosoftCustomerAgreement";

   AgreementMetaData microsoftCustomerAgreementDetails = partnerOperations.AgreementDetails.   ByAgreementType(agreementType).Get().Items.Single();
   ```

2. Iaggregatepartner. AgreementTemplates koleksiyonunu kullanın.

3. **Byıd** metodunu çağırın ve Microsoft Müşteri sözleşmesinin **TemplateId** 'sini belirtin.

4. **Belge** özelliğini getir.

5. **Bycountry** yöntemini çağırın ve Sözleşme şablonunun geçerli olduğu müşterinin ülkesini belirtin. Yöntem belirtilmemişse sorgu *bizim* için varsayılan olarak olur. Desteklenen ülke kodlarının listesi için [Desteklenen ülkeler ve diller listesine](#list-of-supported-countries-and-languages)bakın. Bu yöntem, **büyük/küçük harfe duyarlıdır**.

6. **Bylanguage** metodunu çağırın ve anlaşma şablonunun yerelleştirilmesi gereken dili belirtin. Yöntem belirtilmemişse sorgu varsayılan olarak *en-US* olur veya belirtilen ülke kodu belirtilen ülkede desteklenmez. Desteklenen dil kodlarının listesi için [Desteklenen ülkeler ve diller listesine](#list-of-supported-countries-and-languages)bakın.

7. **Get** veya **GetAsync** yöntemini çağırın.

   ```csharp
   // IAggregatePartner partnerOperations;

   string customerCountry = "US";

   string languageForLocalization = "en-US";

   var agreementDocument = partnerOperations.   AgreementTemplates.ById   (microsoftCustomerAgreementDetails.   TemplateId).Document.ByCountry   (customerCountry).ByLanguage   (languageForLocalization).Get();
   ```

[Konsol test uygulaması](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples) projesinden [Getagreementdetails](https://github.com/PartnerCenterSamples/Partner-Center-SDK-Samples/blob/master/Source/Partner%20Center%20SDK%20Samples/Agreements/GetAgreementDetails.cs) sınıfında, bir bütün örnek bulunabilir.

## <a name="rest-request"></a>REST isteği

Microsoft müşteri anlaşması şablonunu indirmek için bir bağlantı almak üzere:

1. Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alın. Microsoft Müşteri sözleşmesinin **TemplateId** 'sini edinmeniz gerekir. Daha fazla bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](get-customer-agreement-metadata.md).

2. Bir [ **AgreementDocument** KAYNAĞıNı](./agreement-document-resources.md)getirmek için REST isteği oluşturun. Örnek için, [istek sözdizimi](#request-syntax) örneğine bakın. Aşağıdaki bilgileri belirtmeniz gerekir:

    - Microsoft Müşteri sözleşmesinin **TemplateId 'si** .
    - Microsoft müşteri anlaşması şablonunun geçerli olduğu ülke.
    - Microsoft müşteri anlaşması şablonunun yerelleştirilmesi gereken dil.

### <a name="request-syntax"></a>İstek sözdizimi

Bu kaynak için aşağıdaki istek sözdizimini kullanın:

| Yöntem | İstek URI'si |
|--------|---------------------------------------------------------------------|
| GET | [*\{ BaseUrl \}*](partner-center-rest-urls.md)/v1/agreementtemplates/{Agreement-Template-id}/Document? Language = {Language} &ülke = {Country} http/1.1 |

### <a name="uri-parameters"></a>URI parametreleri

İsteğinizle birlikte aşağıdaki URI parametrelerini kullanabilirsiniz:

| Ad                   | Tür   | Gerekli | Açıklama                                 |
|------------------------|--------|----------|---------------------------------------------|
| Sözleşme-şablon kimliği  | string | Yes      | Anlaşma türünün benzersiz tanımlayıcısı. Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini alarak Microsoft Müşteri Sözleşmesi için TemplateId 'yi edinebilirsiniz. Daha fazla bilgi için bkz. [Microsoft Müşteri Sözleşmesi için anlaşma meta verilerini edinme](./get-customer-agreement-metadata.md). Bu parametre, **büyük/küçük harfe duyarlıdır**.|
| ülke                | dize | No       | Anlaşma şablonunun geçerli olduğu ülkeyi belirtir. Parametre belirtilmemişse sorgu *bizim* için varsayılan olarak olur. Desteklenen ülke kodlarının listesi için [Desteklenen ülkeler ve diller listesine](#list-of-supported-countries-and-languages)bakın.|
| language               | dize | No       | Sözleşme şablonunun yerelleştirilmesi gereken dili gösterir. Parametre belirtilmemişse sorgu varsayılan olarak *en-US* , belirtilen ülke için de belirtilen ülke kodu desteklenmez. Desteklenen ülke kodlarının listesi için [Desteklenen ülkeler ve diller listesine](#list-of-supported-countries-and-languages)bakın.|

### <a name="request-headers"></a>İstek üst bilgileri

Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).

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

Başarılı olursa, bu yöntem yanıt gövdesinde bir [ **AgreementDocument** kaynağı](./agreement-document-resources.md) döndürür.

Kaynakta, anlaşma şablonunu indirmek için kullanılabilecek bir URL dizesi içeren bir **Downloaduri** özelliği vardır. Sorgu yaptığınızda farklı bir bağlantı döndürülür. Bu bağlantı beş dakika sonra dolar.

### <a name="response-success-and-error-codes"></a>Yanıt başarısı ve hata kodları

Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.

Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın. Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).

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

## <a name="list-of-supported-countries-and-languages"></a>Desteklenen ülkeler ve dillerin listesi

> [!IMPORTANT]
> Ülke kodu özelliği büyük/küçük harfe duyarlıdır. Lütfen aşağıdaki tabloda belirtilen doğru büyük/küçük harfleri kullandığınızdan emin olun.

| Ülke                   | Ülke kodu   | Desteklenen dil kodları |
|------------------------|--------|----------|
| Åland Adaları | Ax | en-US |
| Afganistan | AF | en-US |
| Arnavutluk | AL | en-US |
| Cezayir | DZ | en-US, fr-FR, en-US |
| Amerikan Samoası | AS | en-US |
| Andorra | AD | en-US |
| Angola | AO | en-US, pt-PT |
| Anguilla | Yapay Zeka | en-US |
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
| Bulgaristan | BG | en-US, bg-BG |
| Burkina Faso | BF | en-US |
| Burundi | BI | en-US |
| Fildişi Sahili (Côte d'Ivoire) | CI | en-US, fr-FR |
| Cabo Verde | CV | en-US, pt-PT |
| Kamboçya | KH | en-US |
| Kamerun | CM | en-US, fr-FR |
| Kanada | CA | en-US, fr-FR |
| Cayman Adaları | KY | en-US, en-US |
| Orta Afrika Cumhuriyeti | CF | en-US |
| Çad | TD | en-US |
| Şili | CL | en-US, es-ES |
| Christmas Adası | CX | en-US |
| Cocos (Keeling) Adaları | CC | en-US |
| Kolombiya | CO | en-US, es-ES |
| Komorlar | Km | en-US |
| Kongo (KDC) | CD | en-US |
| Kongo Cumhuriyeti | Cg | en-US |
| Cook Adaları | Ck | en-US |
| Kosta Rika | CR | en-US, es-ES |
| Hırvatistan | HR | en-US, hr-HR |
| Curaçao | Cw | en-US |
| Kıbrıs | CY | en-US |
| Çekya | CZ | en-US, cs-CZ |
| Danimarka | DK | en-US, da-DK |
| Cibuti | Dj | en-US |
| Dominika | DM | en-US |
| Dominik Cumhuriyeti | DO | en-US, es-ES |
| Ekvador | EC | en-US |
| Mısır | EG | en-US, ar-SA |
| El Salvador | SV | en-US, es-ES |
| Ekvator Ginesi | Gq | en-US |
| Eritre | ER | en-US |
| Estonya | EE | en-US, et-EE |
| eSwatini | SZ | en-US |
| Etiyopya | ET | en-US |
| Falkland Adaları | FK | en-US |
| Faroe Adaları | INFO | en-US |
| Fiji | FJ | en-US |
| Finlandiya | FI | en-US, Fi-FI |
| Fransa | GS | en-US, fr-FR |
| Fransız Guyanası | GF | en-US, fr-FR  |
| Fransız Polinezyası | PF | en-US |
| Fransız Güney Toprakları | The | en-US |
| Gabon | GA | en-US |
| Gambiya | GM | en-US |
| Gürcistan | GE | en-US |
| Almanya | DE | en-US, de-DE |
| Gana | GH | en-US |
| Cebelitarık | ANACAĞı | en-US |
| Yunanistan | GR | en-US, el-GR |
| Grönland | G | en-US |
| Grenada | GD | en-US |
| Guadeloupe | GP | en-US |
| Guam | GU | en-US |
| Guatemala | GT | en-US, ES-ES |
| Guernsey | GG | en-US |
| Gine | GN | en-US |
| Gine-Bissau | GW | en-US |
| Guyana | GY | en-US |
| Haiti | HT | en-US |
| Heard Adası ve McDonald Adaları | HM | en-US |
| Honduras | HN | en-US, ES-ES |
| Hong Kong ÖİB | HK | en-US, zh-HK |
| Macaristan | HU | en-US, HU-HU |
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
| Uruguay | UY | en-US, es-ES |
| Özbekistan | UZ | en-US, ru-RU |
| Vanuatu | Vu | en-US |
| Vatikan | VA | en-US |
| Venezuela | VE | en-US, es-ES |
| Vietnam | VN | en-US, vi-VN |
| Wallis veUçsuzuna | WF | en-US |
| Yemen | YE | en-US, ar-SA |
| Zambiya | ZM | en-US |
| Zimbabve | ZW | en-US |
