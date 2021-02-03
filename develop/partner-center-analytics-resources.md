---
title: İş Ortağı Merkezi Analizi
description: İş ortağı merkezi analizi ortak API 'SI belgeleri.
ms.date: 06/11/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4b14ee929f3020079f409be8817e077673d3219f
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768848"
---
# <a name="partner-center-analytics---resources"></a>İş Ortağı Merkezi Analizi - Kaynaklar

**Uygulama hedefi**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

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
|     subscriptionType      |             string             |       Abonelik türü. **Note**: Bu alan, büyük/küçük harfe duyarlıdır. Desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".       |
|     autoRenewEnabled      |            boolean             |                                         Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer.                                          |
|         iş ortağı kimliği         |             string             | MPN KIMLIĞI. Doğrudan satıcı için, bu parametre ortağın MPN KIMLIĞI olur. Dolaylı bir satıcı için, bu parametre dolaylı satıcıdan MPN KIMLIĞI olacaktır. |
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
|      lastRenewalDate      | UTC Tarih saat biçiminde dize |                                       Aboneliğin son yenilenme tarihi varsayılan değer null.                                       |
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

| Özellik | Tür | Description |
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

| Özellik | Tür | Description |
|----------|------|-------------|
| kimlik | string | Müşteri kiracı tanımlayıcısı.  |
| durum | string | Başvurunun bir müşteriye işaret olup olmadığını gösterir.  |
| customerMarket | string | Müşterinin iş üzerinde kullandığı ülke/bölge. |
| customerName | string | Müşterinin adı. |
| customerOrgSize | string | Müşterinin kuruluşundaki çalışanların sayısını gösteren bir Aralık. Örneğin, "10to50employees". |
| acceptedDate | UTC Tarih saat biçiminde dize | Başvurunun kabul edildiği tarih. |
| Bildiren Geddate | UTC Tarih saat biçiminde dize | Başvurunun alındığı tarih. |
| archivedDate | UTC Tarih saat biçiminde dize | Başvurunun arşivlendiği tarih. |
| declinedDate | UTC Tarih saat biçiminde dize | Başvurunun reddedildiğini belirten tarih. |
| expiredDate | UTC Tarih saat biçiminde dize | Başvurunun zaman aşımına erdiği tarih. |
| lostDate | UTC Tarih saat biçiminde dize | Başvurunun kaybedildiği tarih. |
| Hatalı bir tarih | UTC Tarih saat biçiminde dize | Başvurunun kaçırıldığı tarih. |
| createdDate | UTC Tarih saat biçiminde dize | Başvurunun oluşturulduğu tarih. |
| skippedDate | UTC Tarih saat biçiminde dize | Başvurunun atlandığı tarih. |
| Merak tarihi | UTC Tarih saat biçiminde dize | Başvurunun kazanıldığı tarih. |
| partnerMarket | string |  Ortağın iş kullandığı ülke/bölge. |
