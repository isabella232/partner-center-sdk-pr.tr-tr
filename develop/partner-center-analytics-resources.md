---
title: İş Ortağı Merkezi Analizi
description: İş Ortağı Merkezi Analytics genel API belgeleri.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d7d252a415524c6573c1bf62b8b9c1518a1b9f
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548099"
---
# <a name="partner-center-analytics---resources"></a>İş Ortağı Merkezi Analizi - Kaynaklar

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

Analiz API'si, Kullanıcı Deneyimi'ne sunulan verilere program aracılığıyla erişmeye olanak sağlar.

## <a name="prerequisites"></a>Önkoşullar

- kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md) Bu senaryolar yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.

## <a name="csp-program-azure-usage-analytics"></a>CSP programı: Azure kullanım analizi

Aşağıdaki senaryoda Analiz API'sini kullanarak Azure kullanım analizi bilgilerini İş Ortağı Merkezi nasıl alınabilirsiniz?

- [Tüm Azure kullanım analizi bilgilerini alma](get-all-azure-usage-analytics.md)

Bu senaryo, azure kullanım kaynakları koleksiyonunda analiz [bilgilerini](#azure-usage-resource) döndürür.

## <a name="azure-usage-resource"></a>Azure kullanım kaynağı

Azure kullanımı için tüm analitik verileri temsil eder.

| Özellik | Tür | Açıklama |
|----------|------|-------------|
| CustomerTenantId | string | Müşteri kiracı tanımlayıcısı. |
| Müşteriadı | string | Müşteri adı. |
| subscriptionId | string | Abonelik tanımlayıcısı. |
| subscriptionName | string | Abonelik adı. |
| usageDate | string | Kullanım tarihi. |
| resourceLocation | string | Örneğin, veri merkezinin konumu( Batı Avrupa). |
| meterCategory | string | Ölçüm kategorisi, örneğin veri yönetimi. |
| meterSubcategory | string | Ölçüm alt kategorisi, örneğin coğrafi olarak yedekli. |
| meterUnit | string | Gigabayt veya saat gibi ölçüm birimi. |
| reservationOrderId | string | Azure VM Ayrılmış Örneği için rezervasyon siparişi. |
| reservationId | string | Belirli bir RI sırasına göre ayrılmış örnekler. |
| Servicetype | string | Sanal makine türünü gösterir. Örneğin, Standard_E4s_v3. |
| miktar | long | Ölçüm biriminde kullanılan sayıları gösterir. |

## <a name="csp-program-indirect-resellers-analytics"></a>CSP programı: dolaylı kurumsal bayi analizi

Aşağıdaki senaryoda, analiz API'sini kullanarak tüm dolaylı kurumsal bayi İş Ortağı Merkezi bilgilerini nasıl alasınız?

- [Tüm dolaylı satıcı analiz bilgilerini alma](get-all-indirect-resellers-analytics.md)

Bu senaryo, analiz bilgilerini dolaylı kurumsal bayi kaynakları [koleksiyonunda](#indirect-resellers-resource) döndürür.

## <a name="indirect-resellers-resource"></a>Dolaylı kurumsal bayiler kaynağı

Dolaylı kurumsal bayiler için tüm analitik verileri temsil eder.

| Özellik | Tür | Açıklama |
|----------|------|-------------|
| partnerTenantId | string | Dolaylı kurumsal bayi verilerini almak istediğiniz iş ortağının Kiracı Kimliği. |
| kimlik | string | Dolaylı kurumsal bayi kimliği. |
| name | string | Dolaylı kurumsal bayi verilerini almak istediğiniz iş ortağının adı. |
| Pazar | string | Dolaylı kurumsal bayi verilerini almak istediğiniz iş ortağının Marketi. |
| firstSubscriptionCreationDate | UTC tarih saat biçiminde dize | Dolaylı kurumsal bayi verilerini almak istediğiniz ilk aboneliğin oluşturma tarihi. |
| latestSubscriptionCreationDate | UTC tarih saat biçiminde dize | En son aboneliğin oluşturma tarihi. |
| firstSubscriptionEndDate | UTC tarih saat biçiminde dize | Herhangi bir abonelik ilk kez sona erer. |
| latestSubscriptionEndDate | UTC tarih saat biçiminde dize | Herhangi bir aboneliğin son bitiş tarihi. |
| firstSubscriptionSuspendedDate | UTC tarih saat biçiminde dize | Herhangi bir abonelik ilk kez askıya alınmıştır. |
| latestSubscriptionSuspendedDate | UTC tarih saat biçiminde dize | Herhangi bir aboneliğin askıya alınarak son tarihi. |
| firstSubscriptionDeprovisionedDate | UTC tarih saat biçiminde dize | İlk kez bir aboneliğinvision'ları silindi. |
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

|         Özellik          |              Tür              |                                                                      Açıklama                                                                       |
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
|     Abonelik sayısı     |             sayı             |                        Abonelik sayısı. Note: Bu değer yalnızca bir toplama sorgusunun yanıtında görüntülenir.                         |

## <a name="search-analytics"></a>Arama Analizi

> [!NOTE]
> CSP program üyeliği, arama analizlerini almak için gerekli değildir.

Aşağıdaki senaryoda, tüm Iş ortağı merkezi arama Analizi bilgilerinizi almak için Analytics API 'sinin nasıl kullanılacağı gösterilmektedir.

- [Tüm arama analizi bilgilerini alma](get-all-search-analytics.md)

Bu senaryo, analiz bilgilerinizi bir [arama](#search-resource) kaynakları koleksiyonunda döndürür.

## <a name="search-resource"></a>Kaynak ara

Bir arama için tüm analitik verileri temsil eder.

| Özellik | Tür | Açıklama |
|----------|------|-------------|
| Tadı | string | Faturalama şirket adı. |
| contactButtonClicked | Boole | İletişim düğmesinin tıklandığını gösterir. |
| keywordCountry | string | Aramada belirtilen ülke. |
| Ayrıntılar görüntülendi | Boole | Arama ayrıntılarının görüntülenip görüntülenmediğini belirtir. |
| Keywordindutryfocus | string | Örneğin, Sağlık Hizmetleri içinde arama yapmak için sektör. |
| Mpnıd | string | Microsoft İş Ortağı Ağı (MPN) KIMLIĞI. Doğrudan satıcı için, bu parametre ortağın MPN KIMLIĞI olur. Dolaylı bir satıcı için, bu parametre dolaylı satıcıdan MPN KIMLIĞI olacaktır. |
| partnerMarket | string | İş ortağının işletmeyi yürüttüğü yerel ayar. |
| keywordProduct | string | Aramada belirtilen ürün. |
| referralSubmitted | Boole | Başvurunun gönderilip gönderilmediğini belirtir. |
| searchDate | UTC Tarih saat biçiminde dize | Arama sorgusunun gerçekleştiği tarih. |
| keywordSearchText | string | Aramada belirtilen metin. |
| searchResultPageViews | long | Arama sonucunda ortağın kaç kez geldiği. Yalnızca toplamada bir yanıtın parçası.
| Contacttıklamalar | long | İletişim düğmesinin tıklandığı zaman sayısı. Yalnızca toplamada bir yanıtın parçası.
| referralCount | long | Aramadan oluşturulan başvuruların sayısı. Yalnızca toplamada bir yanıtın parçası.
| profileViews | long | İş ortağı profilinin kaç kez görüntülendiğini. Yalnızca toplamada bir yanıtın parçası.

## <a name="referrals-analytics"></a>Başvuru Analizi

> [!NOTE]
> Başvuru analizlerini almak için CSP program üyeliği gerekli değildir.

Aşağıdaki senaryoda, tüm Iş ortağı merkezi başvuru Analizi bilgilerinizi almak için Analytics API 'sinin nasıl kullanılacağı gösterilmektedir.

- [Tüm başvuru analizi bilgilerini alma](get-all-referrals-analytics.md)

Bu senaryo, bir [başvuru](#referrals-resource) kaynakları koleksiyonundaki analiz bilgilerinizi döndürür.

> [!NOTE]
> Başvuru analizi, 21Vianet tarafından işletilen Iş Ortağı Merkezi tarafından kullanılamaz.

## <a name="referrals-resource"></a>Başvuru kaynağı

Bir başvuru için tüm analitik verileri temsil eder.

| Özellik | Tür | Açıklama |
|----------|------|-------------|
| kimlik | string | Müşteri kiracı tanımlayıcısı.  |
| durum | string | Başvurunun bir müşteriye işaret olup olmadığını gösterir.  |
| customerMarket | string | Müşterinin iş üzerinde kullandığı ülke/bölge. |
| customerName | string | Müşterinin adı. |
| customerOrgSize | string | Müşterinin kuruluşundaki çalışanların sayısını gösteren bir Aralık. Örneğin, "10to50employees". |
| acceptedDate | UTC Tarih saat biçiminde dize | Başvurunun kabul edildiği tarih. |
| Bildiren Geddate | UTC Tarih saat biçiminde dize | Başvurunun alındığı tarih. |
| archivedDate | UTC Tarih saat biçiminde dize | Başvurunun arşivlendiği tarih. |
| declinedDate | UTC tarih saat biçiminde dize | Referans reddedildi tarihi. |
| expiredDate | UTC tarih saat biçiminde dize | Referans süresinin dolma tarihi. |
| lostDate | UTC tarih saat biçiminde dize | Referansların kaybedil olduğu tarih. |
| missedDate | UTC tarih saat biçiminde dize | Referansların at olduğu tarih. |
| createdDate | UTC tarih saat biçiminde dize | Referans oluşturma tarihi. |
| skippedDate | UTC tarih saat biçiminde dize | Referans atlanma tarihi. |
| wonDate | UTC tarih saat biçiminde dize | Referans kazan olduğu tarih. |
| partnerMarket | string |  İş ortağının iş yaptığı ülke/bölge. |
