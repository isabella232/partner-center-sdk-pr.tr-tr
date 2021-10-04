---
title: İş Ortağı Merkezi REST hata kodları
description: Iş Ortağı Merkezi API 'Lerinden hata kodlarının ve başarı yanıtlarının açıklaması.
ms.date: 10/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a26d8bebb79074df1bc962d061d3fd975e5e8e7f
ms.sourcegitcommit: 856c14b6b351697e3b3d33f1fe376adbb80517c5
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/02/2021
ms.locfileid: "129378770"
---
# <a name="partner-center-rest-error-codes"></a>İş Ortağı Merkezi REST hata kodları

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Iş Ortağı Merkezi REST API 'Leri, bir durum kodu içeren bir JSON nesnesi döndürür. Bu kod, isteğinizin başarılı olup olmadığını veya neden başarısız olduğunu gösterir.

## <a name="success-responses"></a>Başarı yanıtları

**2xx** durum kodu, istemci isteğinin başarılı bir şekilde alındığını, anladığını ve kabul edildiğini gösterir.

## <a name="http-status-codes"></a>HTTP durum kodu

Aşağıdaki **4xx** ve **5xx** durum kodları bir hatayı gösterir:

- 400: Hatalı istek
- 401: yetkisiz
- 403: yasak
- 404: bulunamadı
- 405: yönteme izin verilmiyor
- 406: kabul edilemez
- 408: istek zaman aşımı
- 409: çakışma, hata kodu
- 412: önkoşul başarısız oldu
- 429: çok fazla istek
- 500: iç sunucu hatası
- 501: uygulanmadı
- 502: Hatalı ağ geçidi
- 503: hizmet kullanılamıyor
- 504: ağ geçidi zaman aşımı

## <a name="error-responses"></a>Hata yanıtları

**4xx** veya **5xx** durum koduna sahip herhangi bir yanıt, bu kodun hata koşullarından ayrıntıları içeren bir hata iletisi içerir.

Aşağıdaki tablo ve kod örneği bir hata yanıtının şemasını açıklar:

| Ad        | Tür   | Description                                                                                                                                            |
|-------------|--------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| kod        | string | Her zaman döndürülür. Oluşan hata türünü gösterir. Null olmayan.                                                                                  |
| açıklama | string | Her zaman döndürülür. Ayrıntıları ayrıntılı olarak açıklar ve hata ayıklama bilgilerini sağlar. Null olmayan, boş olmayan. Maksimum uzunluk 1024 karakterdir. |
| veriler        | array  | Yalnızca bazı hata türleri için döndürülür. Hata nesnelerinin listesi.                                                                                           |
| kaynak      | dize | Her zaman döndürülür. Hatanın kaynağı.                                                                                                              |

```json
{
  "code": <string>,
  "description": <string>,
  "data": [

  ],
  "source": <string>
}
WWW-Authenticate: OAuth realm=urn:cpsvc:cpid:{some cid}
```

## <a name="error-codes"></a>Hata kodları

API 'Ler tarafından döndürülen hata kodları aşağıda verilmiştir:

| HTTP durumu         | HTTP hata kodu | Hata kodu | Description     |
|---------------------|-----------------|------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Tamam | 200 | 400072 | Bu öğe kullanılamıyor. [Daha fazla bilgi edinin](https://go.microsoft.com/fwlink/p/?linkid=2164140) |
| NotImplemented      | 501       | 0          | Özel durum tanımlı değil       |
| Yetkisiz        | 401       | 400        | Erişim reddedildi         |
| NotFound      | 404       | 1000       | Bulunamadı       |
| Yasak     | 403       | 2006       | İş ortağı teklif için geçerli değil          |
| Işlemindeki hatalı istek          | 400       | 2012       | ticari ve Azure Active Directory abonelik kimlikleri arasında dönüştürme yapılamıyor.          |
| Yasak     | 403       | 2030       | İş ortağı ülkede satıeklendi          |
| Yasak     | 403       | 2032       | Erişim reddedildi         |
| Yasak     | 403       | 2091       | Teklif artık satın alma için kullanılamıyor        |
| Işlemindeki hatalı istek          | 400       | 2100       | Teklif API 'SI, KIMLIĞI olan öğeyi desteklemez {0} . Ürünleri ve/veya SKU 'Larını kullanmayı deneyin      |
| Işlemindeki hatalı istek          | 400       | 3000       | Geçersiz özellik      |
| Yasak     | 403       | 20002      | İş ortağı {0} kimliğinin müşteri kimliğiyle ticari bir ilişkisi {1} yoktur.          |
| NotFound      | 404       | 20003      | Kimliği {0} bulunamadı.     |
| BadRequest          | 400       | 27007      | Geçersiz yükseltme kodu         |
| BadRequest          | 400       | 60000      | Müşteri lisans geçişi başarısız oldu     |
| NotFound      | 404       | 60002      | Kullanıcı nesnesi kimliği bulunamadı       |
| NotFound      | 404       | 60003      | Kiracı bulunamadı      |
| BadRequest          | 400       | 2001       | Abonelik askıya alınırken abonelik miktarı artırılabilir veya azaltılabilir          |
| BadRequest          | 400       | 2002       | Abonelik miktarı minimum ve izin verilen maksimum miktar içinde değil     |
| BadRequest          | 400       | 2006       | Teklif için aboneliklerde {0} güncelleştirmelere izin verilmiyor     |
| BadRequest          | 400       | 2011       | Kimliği ve {0} silinmiş durumu olan abonelik güncelleştirilemez.         |
| BadRequest          | 400       | 2054       | Mevcut aboneliğin faturalama döngüsü, güncelleştirme aboneliği işlemi kullanılarak güncelleştirilemez. Update-Order işlemi kullanma                |
| BadRequest          | 400       | 2055       | Etag artık geçerli değil     |
| BadRequest          | 400       | 2071       | MPN Kimliği geçerli bir Danışman değil     |
| NotFound      | 404       | 2072       | Dolaylı Sağlayıcının MPN Kimliği Kayıtta İş Ortağı olarak geçerli değil          |
| Yasak     | 403       | 2085       | Teklif satın almaya uygun değil               |
| BadRequest          | 400       | 4018       | Bu sipariş işnemiyor      |
| BadRequest          | 400       | 6000       | Sipariş etkin değil bir veya daha fazla abonelik içerdiği için faturalama döngüsü değiştirilenedi         |
| BadRequest          | 400       | 6001       | Siparişin Teklif Kimliklerinden biri faturalama terimini desteklemey olduğundan faturalama döngüsü değiştirilenedi     |
| Yasak     | 403       | 13605      | Bu satın alma işlemini tamamlayamadan önce müşterinin Microsoft Müşteri Sözleşmesi onaylayan bir iş ortağı onayı sağlanmalıdır veya Microsoft Müşteri Sözleşmesi Microsoft Yönetim Merkezi'nde satın alma işlemini kabul etmiş olması gerekir           |
| NotFound      | 404       | 20000      | Sipariş kimliği bulunamadı          |
| BadRequest          | 400       | 27006      | Teklif Kimliği için kullanım sınırı aşıldı      |
| Çakışma      | 409       | 27009      | Üst abonelik Etkin değilken alt abonelik etkinleştirilene     |
| BadRequest          | 400       | 600002     | Kuruluş kayıt kimliği değeri desteklenmiyor  <br/><br/>Müşterinin şirketi/kuruluşu aşağıdaki ülkelerden biri  içinde yer alıyorsa ancak organizationRegistrationNumber belirtmeye çalıştısa bu hata oluşur. Etkilenen ülkeler:<br/><br/>- Arjantin (AM) <br/>- Rusya (AZ)<br/>- Tümce (BY)<br/>- Devam etti (HU)<br/>- Enstantane (KZ)<br/>- Kyrgyzstan (KG)<br/>- Zaman (MD)<br/>- Rusya (RU)<br/>- Tajikistan (TJ)<br/>- Özbekistan (UZ)<br/>- Rusya (UA) |
| BadRequest          | 400       | 600049     | Kuruluş kayıt kimliği bilgileri eksik <br/><br/>Müşterinin şirketi/kuruluşu aşağıdaki ülkelerden birinin içinde bulunuyorsa ve organizationRegistrationNumber sağlanmazsa bu hata oluşur. Etkilenen ülkeler:<br/><br/>- Arjantin (AM) <br/>- Rusya (AZ)<br/>- Tümce (BY)<br/>- Devam etti (HU)<br/>- Enstantane (KZ)<br/>- Kyrgyzstan (KG)<br/>- Zaman (MD)<br/>- Rusya (RU)<br/>- Tajikistan (TJ)<br/>- Özbekistan (UZ)<br/>- Rusya (UA)       |
| BadRequest          | 400       | 600050     | Kuruluş kayıt kimliği bilgileri geçersiz ve \{ 0 biçiminde olmalıdır\} <br/><br/>OrganizationRegistrationNumber, müşterinin bulunduğu ülke için geçerli değilse bu hata oluşur. \{\}0, hatanın beklenen normal ifade biçimine sahip olur. Örneğin: `Organization registration ID information is invalid and should be of the format ^(\\d{7}|\\d{10})$`.          |
| BadRequest          | 400       | 600051     | Müşteri telefon numarası eksik <br/><br/>Müşterinin şirketi/kuruluşu aşağıdaki ülkelerden birinin içinde bulunuyorsa ancak billingProfile.defaultAddress.phoneNumber sağlanmazsa bu hata oluşur. Etkilenen ülkeler:<br/><br/>- Arjantin (AM) <br/>- Rusya (AZ)<br/>- Tümce (BY)<br/>- Devam etti (HU)<br/>- Enstantane (KZ)<br/>- Kyrgyzstan (KG)<br/>- Zaman (MD)<br/>- Rusya (RU)<br/>- Tajikistan (TJ)<br/>- Özbekistan (UZ)<br/>- Rusya (UA)       |
| Yetkisiz        | 401       | 800001     | İstek bağlamında İş Ortağı Belirteci eksik             |
| BadRequest          | 400       | 800002     | Geçersiz istek girişi       |
| InternalServerError | 500       | 800003     | Beklenmeyen hizmet hatası          |
| BadRequest          | 400       | 800004     | Geçersiz teklif kimliği      |
| InternalServerError | 500       | 800005     | Oluşturma siparişi başarılı değil          |
| NotFound      | 404       | 800007     | Sağlama bilgileri alınamadı          |
| NotFound      | 404       | 800008     | Sepet kimliği alınamadı        |
| BadRequest          | 400       | 800009     | Sepet öğesinde hata       |
| BadRequest          | 400       | 800010     | Bu katalog öğesi için envanter kullanılamıyor     |
| BadRequest          | 400       | 800011     | Bu abonelik geçerli bir Azure aboneliği değil        |
| BadRequest          | 400       | 800012     | Bu abonelik etkin bir abonelik değil      |
| BadRequest          | 400       | 800013     | Bu abonelik RI satın alma için etkinleştirilmedi     |
| Çakışma      | 409       | 800014     | Bu sipariş için istenen bir bekleyen ayarlama var     |
| NotFound      | 404       | 800015     | MPN KIMLIĞI bulunamadı         |
| Işlemindeki hatalı istek          | 400       | 800016     | MPN KIMLIĞI geçerli bir dolaylı satıcı değil              |
| Işlemindeki hatalı istek          | 400       | 800017     | Bu katalog öğesi için miktar kullanılamıyor        |
| Işlemindeki hatalı istek          | 400       | 800018     | Korumalı alan sınırı karşılanmadı          |
| Yasak     | 403       | 800019     | Korumalı olmayan kiracıların yazılım abonelikleri ve kalıcı yazılım dışındaki satınalmaları iptal edebilmesine izin verilmez        |
| Yasak     | 403       | 800020     | Katalog öğesi satın alma için uygun değil.       |
| Işlemindeki hatalı istek          | 400       | 800021     | Bu abonelik geçerli bir abonelik değil        |
| Işlemindeki hatalı istek          | 400       | 800022     | Bu işlem için uygun olabilirsiniz. Yardım için desteğe başvurun          |
| Yasak     | 403       | 800023     | Kredi satırınızın bu satın alma için en düşük eşiğe ulaşması nedeniyle bu işlem için uygun değilsiniz. Siparişinizi güncelleştirin (veya) yardım için desteğe başvurun       |
| Işlemindeki hatalı istek          | 400       | 800024     | Bu işlem için uygun değilsiniz            |
| Işlemindeki hatalı istek          | 400       | 800025     | Kredi satırınızın bu satın alma için en düşük eşiğe ulaşması nedeniyle bu işlem için uygun değilsiniz. Siparişinizi güncelleştirin (veya) yardım için desteğe başvurun       |
| Işlemindeki hatalı istek          | 400       | 800026     | Bu işlem için uygun değilsiniz            |
| Yasak     | 403       | 800027     | Katalog öğesi ekleme veya kaldırma miktarı için uygun değil      |
| Yasak     | 403       | 800028     | İlk satın alma dönemi, satın alma/güncelleştirme için artık kullanılamaz         |
| Işlemindeki hatalı istek          | 400       | 800029     | Eklenti belirtilen üst abonelikle ilgili değil         |
| Işlemindeki hatalı istek          | 400       | 800030     | Bu abonelik kayıtlı değil     |
| InternalServerError | 500       | 800031     | Satın alma sistemi desteklenmiyor     |
| ExpectationFailed   | 417       | 800036     | Ön koşul başarısız oldu        |
| NotFound      | 404       | 800037     | Varlık KIMLIĞI bulunamadı          |
| NotFound      | 404       | 800038     | Futurebillingınfo varlığı bulunamadı       |
| Yasak     | 403       | 800039     | Satıcı programı durumu etkin değil                |
| Işlemindeki hatalı istek          | 400       | 800040     | Varlık durumu, öğesinden olarak değiştirilemez {0}{1}       |
| Işlemindeki hatalı istek          | 400       | 800041     | Bu öğe zaten etkinleştirildi                 |
| Işlemindeki hatalı istek          | 400       | 800042     | Desteklenmez         |
| Yasak     | 403       | 800043     | Fiyatlandırma bilgilerine erişim izni verilmedi         |
| Çakışma      | 409       | 800060     | Siparişiniz devam ediyor. Birkaç dakika içinde en son siparişler için sipariş geçmişinizi denetleyin           |
| Işlemindeki hatalı istek          | 400       | 800061     | Sipariş iptal edilemez         |
| Işlemindeki hatalı istek          | 400       | 800062     | Bu işlem için uygun değilsiniz            |
| Işlemindeki hatalı istek          | 400       | 800063     | Bu sipariş {0} iptal edilemez. Abonelikleri askıya almak için/Customers/ {1} /Subscriptions/Patch kullanın \<subscriptionId\>          |
| Çakışma      | 409       | 800064     | Sepet {0} başka bir istek tarafından işleniyor       |
| Işlemindeki hatalı istek          | 400       | 800065     | Zaten gönderilmiş bir sepet kullanıma alınamıyor {0} .      |
| Yasak     | 403       | 800066     | İstenen abonelik sayısı, müşteri başına izin verilen maksimum abonelik sayısını aştı       |
| Yasak     | 403       | 800067     | İstenen bilgisayar sayısı, abonelik başına izin verilen en fazla bilgisayar sayısını aştı          |
| Yasak     | 403       | 800068     | İstenen abonelik sayısı, iş ortağı başına izin verilen maksimum Azure aboneliği sayısını aştı        |
| Yasak     | 403       | 800069     | Sipariş başarısız risk yönetimi denetimi      |
| Işlemindeki hatalı istek          | 400       | 800070     | Teklif belirtilen ülkede kullanılamıyor      |
| Işlemindeki hatalı istek          | 400       | 800071     | Satır öğe numarası 0 ile satır öğesi sayısı arasında olmalıdır        |
| Işlemindeki hatalı istek          | 400       | 800071     | Satır öğe numarası 0 ile satır öğesi sayısı arasında olmalıdır        |
| Işlemindeki hatalı istek          | 400       | 800072     | Aboneliğin SyncState 'i tamamlanmadıysa faturalandırma çevrimi değiştirilemez     |
| Yasak     | 403       | 800073     | Müşteri hesabınız Şu anda gözden geçirme aşamasındadır. Birkaç gün sonra yeniden kontrol edin. Bu süre boyunca haence 'niz için teşekkürler. Daha fazla bilgi {0}              |
| Yasak     | 403       | 800074     | Müşteri hesabınız Şu anda gözden geçirme aşamasındadır. Birkaç gün sonra yeniden kontrol edin. Bu süre boyunca haence 'niz için teşekkürler. Daha fazla bilgi {0}              |
| Yasak     | 403       | 800075     | doğru. Daha fazla bilgi için bkz. {0Müşterinizin hesabınız onaylanmamış. Bu müşteriye yönelik işlemlere izin verilmiyor. Müşteri hesabı bilgilerini doğrulayın}        |
| NotFound      | 404       | 800076     | Abonelik geçmişi bulunamadı          |
| Yasak     | 403       | 800077     | Bilgisayar tabanlı SaaS 'nin iptal edilmesi, yama sıralaması aracılığıyla desteklenmez. Bunun yerine düzeltme aboneliğini kullanın.       |
| Işlemindeki hatalı istek          | 400       | 800078     | Aktarım, geçersiz abonelikle oluşturulamıyor       |
| Işlemindeki hatalı istek          | 400       | 800080     | Abonelik bir Mint hesabıyla ilişkilendirilmediği takdirde faturalandırma çevrimi değiştirilemez        |
| BadRequest          | 400       | 800081     | Abonelik etkinleştirmeden önce güncelleştirilemeden önce abonelik güncelleştirilemeden önce          |
| BadRequest          | 400       | 800082     | güncelleştirilebilir. Biraz sonra yeniden deneyinAsubscription hazır değil      |
| InternalServerError | 500       | 800083     | Kullanılabilirlik birden fazla dahil edilen miktar seçeneğine sahiptir         |
| InternalServerError | 500       | 800084     | Desteklenmeyen süre {0}          |
| BadRequest          | 400       | 800085     | Aboneliğin faturalama döngüsü, özgün sipariş faturalama döngüsüyle eşle değil        |
| BadRequest          | 400       | 800086     | Müşteri kiracısı teklif için gerekli etiketlere sahip değil        |
| InternalServerError | 500       | 800087     | Satır öğesiyle ilgili bir sorun var.                |
| Yasak     | 403       | 800088     | İstenen yer {0} sayısı/sn, CatalogID için abonelik başına izin verilen {1} kalan boş alan sınırını aştı - {2}       |
| Yasak     | 403       | 800089     | İstenen varlık sayısı {0} müşteri başına izin verilen kalan varlık sınırını {1} aştı         |
| BadRequest          | 400       | 800090     | Abonelik miktarı azaltılamay            |
| BadRequest          | 400       | 800091     | Askıya alınmış durumu olan bir abonelik güncelleştirildi         |
| BadRequest          | 400       | 800092     | Yazılım Güvencesi programı kapsamında satın alınan abonelik için lisans miktarı Yazılım Güvencesi artıramaz         |
| BadRequest          | 400       | 800093     | Abonelik otomatik olarak yenilenmeye uygun değil        |
| InternalServerError | 500       | 800094     | Aboneliği güncelleştirme başarılı değil                |
| BadRequest          | 400       | 800095     | Bu abonelik için yer miktarını güncelleştire miyim?      |
| BadRequest          | 400       | 800096     | Bu aboneliğin durumu güncelleştirile değil       |
| BadRequest          | 400       | 800097     | Bu abonelik için faturalama döngüsü güncelleştirile değil      |
| BadRequest          | 400       | 800098     | Bu abonelik için kayıtta iş ortağı güncelleştirilesin mi?        |
| NotFound      | 404       | 800111     | Verilen yetkilendirme kimliğine sahip Azure aboneliği bulunamadı.       |
| Yasak     | 403       | 800115     | Fazla çalışma zaten başka bir kiracıya atanmıştır. Sahiplik sorularını çözmek için müşterinize ulaşın.       |
| Yasak     | 403       | 800114     | Bu müşteri için fazlalıkları yönetmeye uygun değilsiniz.       |
| Yasak     | 403       | 800112     | Müşterinin eski Azure abonelikleri olduğu için fazla kullanım ayar olamaz.       |
| NotFound      | 404       | 900100     | Aktarım isteği bulunamadı        |
| Çakışma      | 409       | 900101     | Özgün aktarım devam ettikçe bu {0} aktarıma izin verilmez         |
| BadRequest          | 400       | 900102     | Aktarım için aktarım isteği işlenemiyor {1}{0}         |
| InternalServerError | 500       | 900103     | Aktarım sırası başarılı değil        |
| Çakışma      | 409       | 900104     | Aktarım {0} başka bir istek tarafından işleniyor         |
| Yasak     | 403       | 900105     | Askıya alınmış durumda bir veya daha fazla Azure aboneliğiniz var. Bunlar Azure planına yapılamaz          |
| NotFound      | 404       | 900106     | Yükseltme isteği bulunamadı      |
| Işlemindeki hatalı istek          | 400       | 900107     | Azure Katalog öğesi bulunamadığı için Azure yükseltmesi işlenemiyor          |
| Yasak     | 403       | 900108     | Müşterinin Azure abonelikleri olmadığından Azure yükseltmesi işlenemiyor.      |
| Çakışma      | 409       | 900109     | Özgün yükseltme devam ettiğinden bu yükseltmeye izin verilmiyor {0}     |
| Işlemindeki hatalı istek          | 400       | 900110     | Tamamlanan yükseltme için yükseltme isteği işlenemiyor {0}     |
| Işlemindeki hatalı istek          | 400       | 900111     | Belirtilen yükseltme KIMLIĞI müşteriye ait değil {0} . Müşteri, yükseltme KIMLIĞIYLE eşlendi {1}     |
| Çakışma      | 409       | 900112     | Yükseltme isteği {0} bekleme durumunda olduğundan bu satınalmaya izin verilmez        |
| Çakışma      | 409       | 900113     | Yükseltme isteği devam ettiğinden bu satınalmaya izin verilmiyor {0}       |
| Çakışma      | 409       | 900114     | Yükseltme isteği başarısız olduğu için bu satınalmaya izin verilmiyor {0}         |
| Yasak     | 403       | 900115     | Etkin durumda bir veya daha fazla Azure aboneliğiniz olduğundan Azure planı askıya alınmış duruma taşınamıyor        |
| Işlemindeki hatalı istek          | 400       | 900116     | Sıra oluşturulamıyor. Sandbox hesapları altında kaç Azure planının oluşturulayaabileceği bir sınır vardır      |
| Işlemindeki hatalı istek          | 400       | 900117     | {0}Gün iptal etme pencerenizi geçirtiniz. Satın alma işlemini iptal edemedik               |
| Işlemindeki hatalı istek          | 400       | 900118     | Geçersiz müşteri KIMLIĞI         |
| Yasak     | 403       | 900119     | Azure Iş ortağı paylaşılan hizmetleri için Azure yükseltmesi işlenemiyor         |
| Yasak     | 403       | 900120     | Azure yükseltmesi işlenemiyor      |
| Yasak     | 403       | 900121     | Kredi sınırı yetersiz olduğundan sipariş işlenemiyor, lütfen ucmwrcsp@microsoft.com daha fazla yardım için iletişime geçin        |
| NotFound      | 404       | 900122     | Danışman teklifi bulunamadı     |
| Yasak     | 403       | 900123     | Microsoft Iş ortağı sözleşmesi dolaylı satıcı tarafından kabul edilmedi         |
| Yasak     | 403       | 900124     | Şirketiniz Microsoft Iş ortağı sözleşmesi 'Ni (MPA) kabul etmedi. Tam işlem yeteneklerini sürdürmesini sağlamak için CSP hesabının genel Yöneticisi MPA 'yı kabul etmelidir. {0}Genel yöneticinizle arama yapın ve {1} tam işlem özelliklerini sürdürmeleri IÇIN panoda MPa 'yı imzalayıp          |
| Işlemindeki hatalı istek          | 400       | 900125     | Danışman iş ortağı bilgileri istek bağlamında bulunamadı     |
| Işlemindeki hatalı istek          | 400       | 900126     | Enum ayrıştırılamadı: {0} daha fazla bilgi için lütfen şu adresi ziyaret edin: {1}       |
| Işlemindeki hatalı istek          | 400       | 900127     | Bu işlem bu ortamda desteklenmiyor        |
| Işlemindeki hatalı istek          | 400       | 900128     | Tarifeli bir faturalandırma planıyla SaaS aboneliği satın almak için bir Azure planı gerekir                 |
| Işlemindeki hatalı istek          | 400       | 900129     | Belirtilen Azure plan KIMLIĞI bulunamadı veya bunun altında etkin bir Azure aboneliği yok. Tarifeli bir faturalandırma planına sahip bir SaaS ürünü satın almak için etkin abonelikler içeren bir Azure planı gerekir         |
| Yasak     | 403       | 900130     | Son zamanlarda bir veya daha fazla Azure aboneliği satın alındı, bu abonelikler Şu anda geçirilemez. Lütfen daha sonra tekrar deneyin               |
| Işlemindeki hatalı istek          | 400       | 900131     | Müşterinin eski Azure abonelikleri olduğundan bu aktarım isteği başlatılamaz              |
| Işlemindeki hatalı istek          | 400       | 900132     | Azure planı etkin olmadığından, bu aktarım isteği başlatılamıyor, lütfen Azure planını etkinleştirin     |
| Işlemindeki hatalı istek          | 400       | 900133     | Müşteri Azure planı satın alınmadığından bu aktarım isteği başlatılamaz       |
| Işlemindeki hatalı istek          | 400       | 900134     | Azure planı satın alınabilir alınırken olmadığı için bu aktarım isteği başlatılamaz     |
| InternalServerError | 500       | 900135     | Aktarım isteği başlatılamadı. Lütfen daha sonra tekrar deneyin         |
| Işlemindeki hatalı istek          | 400       | 900136     | İstekte kaynak iş ortağı e-postası/etki alanı ayrıntıları eksik olduğu için aktarım başlatılamaz            |
| Yasak     | 403       | 900137     | Aktarım iş ortağı olarak oluşturulamıyor: {0} Bu özellik için etkin değil      |
| Yasak     | 403       | 900138     | İş ortağı tarafından oluşturulamıyor: {0} Ulusal bulut {1} desteklenmiyor         |
| Yasak     | 403       | 900139     | Aktarım isteği kabul edilemiyor. Lütfen Azure abonelikleri olmadan aktarım oluşturmak için iş ortağı isteyin        |
| NotFound      | 404       | 900140     | kiracı kimliği {0} ve kaynak sağlama kimliği olan bir müşteri için Azure Active Directory abonelikleri alınamıyor{1}     |
| Işlemindeki hatalı istek          | 400       | 900141     | Bu işlem desteklenmiyor         |
| Işlemindeki hatalı istek          | 400       | 900142     | Katalog öğesi KIMLIĞI yok      |
| Işlemindeki hatalı istek          | 400       | 900143     | İstek şu {0} {1} kimliğe sahip bir müşteri için ProductID:, skuid: ile tüm kullanılabilirliği alamadı: {3}     |
| Işlemindeki hatalı istek          | 400       | 900144     | Sağlama SKU 'SU KIMLIĞI yok               |
| Işlemindeki hatalı istek          | 400       | 900145     | Azure ayırmaları aboneliklerle aktarılmadığından, faturalandırma sahipliğinin aktarılması için bu istek tamamlanamaz. Seçiminizdeki aboneliklerle ilişkili Azure ayırmalarını iptal edip yeniden deneyin.         |
| Işlemindeki hatalı istek          | 400       | 900146     | Üçüncü taraf Market ürünleri aboneliklerle aktarılmadığından, faturalandırma sahipliğinin aktarılmasıyla ilgili bu istek tamamlanamaz. Üçüncü taraf Market ürünlerini seçiminizden kaldırın ve yeniden deneyin.       |
| Işlemindeki hatalı istek          | 400       | 900147     | Geçerli iş ortağıyla ilişkili geçerli bir etki alanı belirtin       |
| Işlemindeki hatalı istek          | 400       | 900148     | İstek, talep eden iş ortağıyla eşleşen kaynak iş ortağı ayrıntıları nedeniyle başarısız oldu                |
| Yasak     | 403       | 900149     | {0} program durumu etkin değil.       |
| Yasak     | 403       | 900150     | Sağlanan rolün istenen işlemi gerçekleştirme hakları yok      |
| InternalServerError | 500       | 900192     | Bir sorun oluştu. Lütfen bir süre sonra yeniden deneyin.       |
| BadRequest          | 400       | 900203     | CatalogItemId: {0} onay kabulü gerektirir.        |
| BadRequest          | 400       | 600049     | Kuruluş kayıt kimliği bilgileri eksik. Müşterinin şirketi/kuruluşu şu ülkelerde bulunuyorsa bu hata ortaya çıkacaktır: Arjantin(AM), Arjantin(AZ), Sonra(BY), Dale(HU),Havuz(KZ), Kyrgyzstan(KG), Veri(MD), Rusya(RU), Tajikistan(TJ), Uzbekistan(UZ), Uz), Yer (UA)ancak organizationRegistrationNumber geçiriliyor.      |
| BadRequest          | 400       | 600050     | Kuruluş kayıt kimliği bilgileri geçersiz ve biçiminde `{0}` olmalıdır. Geçirilen organizationRegistrationNumber, müşterinin bulunduğu ülke için geçerli değilse bu hata oluştu. {0} , hatanın beklenen normal ifade biçimine sahip olur. Örneğin: Kuruluş kayıt kimliği bilgileri geçersiz ve biçiminde olmalıdır `^(\\d{7}|\\d{10})$`          |
| BadRequest          | 400       | 600051     | Müşteri telefon numarası eksik. Müşterinin şirketi/kuruluşu şu ülkelerde bulunuyorsa bu hataya neden olur: Arjantin(AM), Arjantin(AZ), Yazıcı(BY),Havuz(HU), GZ), Kyrgyzstan(KG), Veri(MD), Rusya(RU), Tajikistan(TJ), Uzbekistan(UZ), Uz), Yer (UA) ancak billingProfile.defaultAddress.phoneNumber değeri geçiriliyor.       |
| BadRequest          | 400       | 600002     | Kuruluş kayıt kimliği değeri desteklenmiyor. Müşterinin şirketi/kuruluşu şu ülkelerde yer alıyorsa bu hata ortaya çıkacaktır: Arjantin(AM), Arjantin(AZ), Sonra(BY), Dale(HU), GZ), Kyrgyzstan(KG), Veri(MD), Rusya(RU), Tajikistan(TJ), Özbekistan(UZ), Uz), Deniz (UA), ancak organizationRegistrationNumber belirtmeye çalıştılar.       |
