---
title: İş Ortağı Merkezi Analizi
description: İş ortağı merkezi analizi ortak API 'SI belgeleri.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9028d5e2bdeb2637e35133b2c6dda739e0024ccc2838368a5276b1482af78d7f
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115997847"
---
# <a name="partner-center-analytics---resources"></a>İş Ortağı Merkezi Analizi - Kaynaklar

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

Analiz API 'SI, kullanıcı deneyiminde sunulmakta olan verilere programlı bir şekilde erişmenize olanak tanır.

## <a name="prerequisites"></a>Önkoşullar

- [Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri. Bu senaryolar yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="csp-program-azure-usage-analytics"></a>CSP programı: Azure Kullanım Analizi

Aşağıdaki senaryoda, tüm Iş Ortağı Merkezi Azure kullanım analizi bilgilerinizi almak için Analytics API 'sinin nasıl kullanılacağı gösterilmektedir.

- [Tüm Azure kullanım analizi bilgilerini alma](get-all-azure-usage-analytics.md)

Bu senaryo, analiz bilgilerinizi bir [Azure kullanım](#azure-usage-resource) kaynakları koleksiyonunda döndürür.

## <a name="azure-usage-resource"></a>Azure kullanım kaynağı

Azure kullanımı için tüm analitik verileri temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| CustomerTenantId | string | Müşteri kiracı tanımlayıcısı. |
| customerName | string | Müşteri adı. |
| subscriptionId | string | Abonelik tanımlayıcısı. |
| subscriptionName | string | Abonelik adı. |
| usageDate | string | Kullanım tarihi. |
| resourceLocation | string | Veri merkezinin konumu, Batı Avrupa, örneğin. |
| meterCategory | string | Ölçüm kategorisi, örneğin veri yönetimi. |
| meterSubcategory | string | Ölçüm alt kategorisi, örneğin, coğrafi olarak yedekli. |
| meterUnit | string | Ölçüm birimi (gigabayt veya saat gibi). |
| reservationOrderId | string | Azure VM ayrılmış örneği için rezervasyon sıralaması. |
| reservationId | string | Belirli bir RI sıralaması altında ayrılmış örnekler. |
| Türü | string | Sanal makine türünü gösterir. Örneğin, Standard_E4s_v3. |
| miktar | long | Ölçüm biriminde kullanılan sayıları gösterir. |

## <a name="csp-program-indirect-resellers-analytics"></a>CSP programı: dolaylı satıcılar Analizi

Aşağıdaki senaryoda, tüm Partner Center dolaylı satıcılar Analytics bilgilerinizi almak için Analytics API 'sinin nasıl kullanılacağı gösterilmektedir.

- [Tüm dolaylı satıcı analiz bilgilerini alma](get-all-indirect-resellers-analytics.md)

Bu senaryo, bir [dolaylı satıcılar](#indirect-resellers-resource) kaynakları koleksiyonundaki analiz bilgilerinizi döndürür.

## <a name="indirect-resellers-resource"></a>Dolaylı satıcılar kaynağı

Dolaylı satıcıların tüm analitik verilerini temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| Partnertenantıd | string | Dolaylı satıcıların verilerini almak istediğiniz ortağın kiracı KIMLIĞI. |
| kimlik | string | Dolaylı satıcı KIMLIĞI. |
| name | string | Dolaylı satıcıların verilerini almak istediğiniz iş ortağının adı. |
| pazara | string | Dolaylı satıcıların verilerini almak istediğiniz iş ortağının pazarı. |
| firstSubscriptionCreationDate | UTC Tarih saat biçiminde dize | Dolaylı satıcıların verilerini almak istediğiniz ilk aboneliğin Oluşturulma tarihi. |
| latestSubscriptionCreationDate | UTC Tarih saat biçiminde dize | En son aboneliğin Oluşturulma tarihi. |
| firstSubscriptionEndDate | UTC Tarih saat biçiminde dize | Herhangi bir aboneliğin sonlandırılması ilk kez. |
| latestSubscriptionEndDate | UTC Tarih saat biçiminde dize | Herhangi bir aboneliğin sonlandıralındığı en son tarih. |
| firstSubscriptionSuspendedDate | UTC Tarih saat biçiminde dize | Abonelikler ilk kez askıya alındı. |
| latestSubscriptionSuspendedDate | UTC Tarih saat biçiminde dize | Herhangi bir aboneliğin askıya alındığı en son tarih. |
| firstSubscriptionDeprovisionedDate | UTC Tarih saat biçiminde dize | İlk kez bir abonelik sağlanmamıştır. |
| latestSubscriptionDeprovisionedDate | UTC Tarih saat biçiminde dize | Herhangi bir aboneliğin sağlaması kaldırılmış olan en son tarih. |
| Abonelik sayısı | double | Tüm değer eklenmiş satıcıların abonelik sayısı |
| licenseCount | double | Tüm değer eklenmiş satıcıların lisans sayısı |
| ındirectresellercount | double | Dolaylı satıcıların sayısı |

## <a name="csp-program-subscription-analytics"></a>CSP programı: abonelik Analizi

Aşağıdaki senaryolarda, tüm Iş Ortağı Merkezi abonelik Analizi bilgilerinizi almak, bir arama sorgusuyla filtrelemek veya tarihlere ya da koşullara göre gruplamak için Analytics API 'sinin nasıl kullanılacağı gösterilmektedir.

- [Tüm abonelik analizi bilgilerini alma](get-all-subscription-analytics.md)
- [Bir arama sorgusuyla filtrelenmiş abonelik analizi bilgilerini alma](get-subscription-analytics-by-search-query.md)
- [Tarih veya koşullara göre gruplanmış abonelik analizi bilgilerini alma](get-subscription-analytics-grouped-by-dates-or-terms.md)

Bu senaryoların hepsi, bir [abonelik](#subscription-resource) kaynakları koleksiyonunda analiz bilgilerinizi geri döndürür.

## <a name="subscription-resource"></a>Abonelik kaynağı

Bir abonelik için tüm analitik verileri temsil eder.

|         Özellik          |              Tür              |                                                                      Description                                                                       |
|---------------------------|--------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
|     Customertenantıd      |             string             |                                              Müşteri kiracısını tanımlayan GUID biçimli bir dize.                                              |
|       customerName        |             string             |                                                               Müşterinin adı.                                                                |
|      customerMarket       |             string             |                                                 Müşterinin iş üzerinde kullandığı ülke/bölge.                                                 |
|            kimlik             |             string             |                                                              Abonelik tanımlayıcısı.                                                              |
|          durum           |             string             |                                          Abonelik durumu: "ETKIN", "askıya ALıNDı" veya "SAĞLAMASı KALDıRıLDı".                                           |
|        productName        |             string             |                                                                Ürünün adı.                                                                |
|     subscriptionType      |             string             |       Abonelik türü. **Note**: Bu alan, büyük/küçük harfe duyarlıdır. desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer.                                          |
|         iş ortağı kimliği         |             string             | Microsoft İş Ortağı Ağı (MPN) KIMLIĞI. Doğrudan satıcı için, bu parametre ortağın MPN KIMLIĞI olur. Dolaylı bir satıcı için, bu parametre dolaylı satıcıdan MPN KIMLIĞI olacaktır. |
|       friendlyName        |             string             |                                                             Aboneliğin adı.                                                              |
|        partnerName        |             string             |                                              Aboneliğin satın alındığı ortağın adı                                               |
|       Adı        |             string             |            Abonelik işlemi dolaylı satıcı için olduğunda, sağlayıcı adı aboneliği satın alan dolaylı sağlayıcıdır.             |
|    effectiveStartDate     | UTC Tarih saat biçiminde dize |                                                           Aboneliğin başladığı tarih.                                                            |
|     commitmentEndDate     | UTC Tarih saat biçiminde dize |                                                            Aboneliğin bitiş tarihi.                                                             |
|    currentStateEndDate    | UTC Tarih saat biçiminde dize |                                           Aboneliğin geçerli durumunun değiştirileceği tarih.                                            |
| Trialtopaıdconversiondate | UTC Tarih saat biçiminde dize |                                 Aboneliğin deneme sürümünden ücretli olarak dönüştürdüğü tarih. Varsayılan değer boştur.                                 |
|      trialStartDate       | UTC Tarih saat biçiminde dize |                                Abonelik için deneme süresinin başladığı tarih. Varsayılan değer boştur.                                 |
|       trialEndDate        | UTC Tarih saat biçiminde dize |                                  Abonelik deneme süresinin sona erdiği tarih. Varsayılan değer boştur.                                  |
|       lastUsageDate       | UTC Tarih saat biçiminde dize |                                        Aboneliğin son kullanıldığı tarih. Varsayılan değer boştur.                                        |
|     deprovisionedDate     | UTC Tarih saat biçiminde dize |                                      Aboneliğin sağlaması kaldırılmış olan tarih. Varsayılan değer boştur.                                      |
|      lastRenewalDate      | UTC Tarih saat biçiminde dize |                                       Aboneliğin son yenilenme tarihi. Varsayılan değer boştur.                                       |
|       licenseCount        |             sayı             |                                                             Toplam lisans sayısı.                                                              |
|     Abonelik sayısı     |             sayı             |                        Abonelik sayısı. Not: Bu değer yalnızca bir toplama sorgusunun yanıtlarında görünür.                         |

## <a name="search-analytics"></a>Arama analizi

> [!NOTE]
> Arama analizini almak için CSP programı üyeliği gerekli değildir.

Aşağıdaki senaryoda, analiz api'sini kullanarak tüm arama analizi İş Ortağı Merkezi nasıl alınabilirsiniz?

- [Tüm arama analizi bilgilerini alma](get-all-search-analytics.md)

Bu senaryo, analiz bilgilerinizi Arama kaynakları [koleksiyonunda](#search-resource) döndürür.

## <a name="search-resource"></a>Kaynak ara

Arama için tüm analitik verileri temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| Şirketadı | string | Faturalama şirketi adı. |
| contactButtonClicked | Boole | Kişi düğmesinin tıklandı olup olduğunu gösterir. |
| keywordCountry | string | Aramada belirtilen ülke. |
| detailsViewed | Boole | Arama ayrıntılarının görüntü olup olduğunu gösterir. |
| keywordIndustryFocus | string | Sağlık gibi içinde aranan sektör. |
| mpnId | string | Microsoft İş Ortağı Ağı (MPN) kimliği. Doğrudan bayi için bu parametre, iş ortağının MPN kimliği olur. Dolaylı kurumsal bayi için bu parametre, dolaylı kurumsal bayinin MPN kimliği olur. |
| partnerMarket | string | İş ortağının iş yürüttrenin bulunduğu yerel olarak. |
| keywordProduct | string | Aramada belirtilen ürün. |
| referralSubmitted | Boole | Bir referans gönder olup yapılmamış olduğunu gösterir. |
| searchDate | UTC tarih saat biçiminde dize | Arama sorgusunun meydana geldiği tarih. |
| keywordSearchText | string | Aramada belirtilen metin. |
| searchResultPageViews | long | İş ortağının arama sonucunda kaç kez geldiği. Yanıtın yalnızca toplamada bir parçası.
| contactClicks | long | Kişi düğmesine kaç kez tıklandı? Yanıtın yalnızca toplamada bir parçası.
| referralCount | long | Aramadan oluşturulan referans sayısı. Yanıtın yalnızca toplamada bir parçası.
| profileViews | long | İş ortağı profilinin görüntüleme sayısı. Yanıtın yalnızca toplamada bir parçası.

## <a name="referrals-analytics"></a>Referans analizi

> [!NOTE]
> Referans analizini almak için CSP program üyeliği gerekli değildir.

Aşağıdaki senaryoda, tüm referans analizi bilgilerini almak için Analiz API'sini İş Ortağı Merkezi nasıl kullanabileceğiniz gösterir.

- [Tüm başvuru analizi bilgilerini alma](get-all-referrals-analytics.md)

Bu senaryo, bir Referans kaynakları koleksiyonunda analiz [bilgilerini](#referrals-resource) döndürür.

> [!NOTE]
> Referans analizi, 21Vianet tarafından İş Ortağı Merkezi için kullanılamaz.

## <a name="referrals-resource"></a>Referans kaynağı

Referans için tüm analitik verileri temsil eder.

| Özellik | Tür | Description |
|----------|------|-------------|
| kimlik | string | Müşteri kiracı tanımlayıcısı.  |
| durum | string | Referans bir müşteriye yönlendirildi mi?  |
| customerMarket | string | Müşterinin iş yaptığı ülke/bölge. |
| Müşteriadı | string | Müşterinin adı. |
| customerOrgSize | string | Müşterinin kuruluşunda çalışan sayısını gösteren bir aralık. Örneğin, "10to50employees". |
| acceptedDate | UTC tarih saat biçiminde dize | Referans kabul edilen tarih. |
| acknowledgedDate | UTC tarih saat biçiminde dize | Referans kabul tarihi. |
| archivedDate | UTC tarih saat biçiminde dize | Referans arşivlenen tarih. |
| declinedDate | UTC tarih saat biçiminde dize | Referans reddedildi tarihi. |
| expiredDate | UTC tarih saat biçiminde dize | Referans süresinin dolma tarihi. |
| lostDate | UTC tarih saat biçiminde dize | Referansların kaybedil olduğu tarih. |
| missedDate | UTC tarih saat biçiminde dize | Referansların at olduğu tarih. |
| createdDate | UTC tarih saat biçiminde dize | Referans oluşturma tarihi. |
| skippedDate | UTC tarih saat biçiminde dize | Referans atlanma tarihi. |
| wonDate | UTC tarih saat biçiminde dize | Referans kazan olduğu tarih. |
| partnerMarket | string |  İş ortağının iş yaptığı ülke/bölge. |
