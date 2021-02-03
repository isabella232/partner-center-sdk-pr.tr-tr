---
title: CSP Müşteri Vitrini Oluşturucusu Hızlı Başlangıç Kılavuzu
description: CSP Customer storefront Builder kullanarak bulut çözümü sağlayıcısı (CSP) tekliflerini satmaya yönelik bir çevrimiçi Market oluşturun.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d64deff9b002b861c9f48d076feb5841af727e3d
ms.sourcegitcommit: 57620e249e218edc4af7c83c2ce8a3008a4adf4e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/04/2020
ms.locfileid: "97769208"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>CSP Müşteri Vitrini Oluşturucusu Hızlı Başlangıç Kılavuzu

**Uygulama hedefi:**

- İş Ortağı Merkezi

CSP Customer storefront Builder kullanarak bulut çözümü sağlayıcısı (CSP) tekliflerini satmaya yönelik bir çevrimiçi Market oluşturun.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>CSP Customer storefront Builder 'a giriş

CSP müşteri storefront Oluşturucusu, iş ortaklarının, müşterilerine CSP teklifleri satmak için kolayca çevrimiçi bir market oluşturmalarına yardımcı olur. Çoğu iş ortağı ve küçük satış kuruluşları, çevrimiçi bir market geliştirme yerine satışa odaklanmak ister. Iş Ortağı Merkezi SDK örnek uygulaması, bir Web sitesi oluşturup dağıtmak için yazılım geliştirme becerileri gerektirir. CSP Customer storefront Builder ile kendi web sitenizi hızlı ve kolay bir şekilde oluşturabilirsiniz. Web sitesini örnek kod olarak da indirebilir veya bir Transact Web sitesiyle doğrudan Azure aboneliğinize dağıtabilirsiniz.

Bu web sitesi, iş ortakları tarafından tamamen aittir, desteklenir ve sürdürülür ve Microsoft, Web sitesinden hiçbir veri veya telemetri toplamaz. CSP müşteri storefront Oluşturucusu, iş ortağı için, [ödeme kartı sektör verileri güvenlik standardı](https://www.pcisecuritystandards.org/) (PCI DSS) ile tam uyumlu bir Web sitesi oluşturur.

CSP Customer storefront Builder Kodu, [Iş Ortağı Merkezi SDK EULA 'sında](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)bulunan lisansa tabidir.

>[!NOTE]
>Storefront Web sitesi yönetimi, bakım ve Web sitesi oluşturma işleminden kaynaklanan sorunlardan siz sorumlusunuz. [Iş ortağı MERKEZI SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)'daki koşulları okuyun ve anlayın.

Ek bilgi için, aşağıdaki makalelere bakın: [CSP müşteri web storefront](csp-customer-web-storefront.md) ve [konsol test uygulaması](console-test-app.md).

## <a name="considerations"></a>Dikkat edilmesi gerekenler

CSP Customer storefront Builder, Web sitesi oluşturmanın hızlı bir yolu olarak hazırlanmıştır. Planlamada aşağıdaki noktalara dikkat edin:

- Microsoft ve Iş Ortağı Merkezi dağıtıldıktan sonra, iş ortağı web sitesinin veya CSP müşteri storefront Oluşturucusu 'na eklenen bilgilerin bir kopyasını korumaz.

- İş Ortağı Merkezi, bir iş ortağının Azure aboneliklerine yalnızca bir CSP Customer storefront Web sitesi dağıtabilir.

- Bu web sitesi dağıtıldıktan sonra, iş ortağı tarafından tam olarak sahipli ve yönetilir. Microsoft 'un bu Web sitesine veya Web sitesiyle ilgili herhangi bir veriye erişimi yoktur. İş ortakları, Web sitesinin bakımı ve yönetiminden sorumludur. Microsoft, CSP Customer storefront Builder veya CSP Customer storefront Builder kullanılarak oluşturulan herhangi bir Web sitesi ile ilgili canlı bir Web sitesi ya da diğer destek sağlamacaktır.

- İş Ortağı Merkezi, yeni veya değiştirilmiş SDK veya API özellikleriyle bu Web sitesini doğrudan erişemez veya yükseltemiyor. Yeni özellik veya geliştirmelerin, yeni Iş Ortağı Merkezi SDK veya API özellikleri ekleme dahil olmak üzere iş ortakları tarafından sahip, geliştirilmiş ve yönetilen olması gerekir.

- Bu CSP Customer storefront Builder Şu anda bir PayPal Pro/PayU para (Hindistan için) hesabına ödeme yapılandırma olanağı sağlıyor. İş ortaklarının ödeme işlemcisini değiştirmesi gerekiyorsa, bu kodun tercih ettiği ödeme yöntemini desteklemesi için kodu değiştirmesi gerekir.

- CSP Customer storefront Builder 'a eklenen ödeme ile ilgili tüm bilgiler, Iş Ortağı Merkezi 'nde depolanmaz veya korunmaz.

- PayPal ödeme yapılandırması, PayPal 'in kullanılabildiği tüm coğrafi bölgelerde çalışacaktır. PayPal kullanılabilirliği ve desteği yalnızca PayPal tarafından denetlenir ve PayPal tarafından herhangi bir zamanda durdurulmuş olabilir.

- PayU ödeme yapılandırması, yalnızca Hindistan 'da çalışır. PayU kullanılabilirliği ve desteği yalnızca PayU tarafından denetlenir ve PayU tarafından herhangi bir zamanda sonlandırılabilir.

- [Iş ortağı MERKEZI SDK EULA](https://partnercenter.microsoft.com/partner/EULA_Partner_Center_SDK)'daki koşulları okuyun ve anlayın.

## <a name="using-the-csp-customer-storefront-builder"></a>CSP Customer storefront Builder 'ı kullanma

Iş Ortağı Merkezi 'ndeki CSP iş ortağı yöneticileri, doğrudan Iş Ortağı Merkezi 'nden bir CSP müşterisi storefront dağıtabilir. En düşük çabayla, ortağın kiracısına yeni bir Web sitesi dağıtılabilir. Dağıtım yapıldıktan sonra, iş ortakları, marka, teklif ve ödemeyle ilgili bilgileri yapılandırmak için Web sitesini kullanabilir ve sonra Web sitesi URL adresini müşterilerle paylaşabilir.

Storefront Web sitesi oluşturma işlemi şu şekilde yapılır:

1. [Web sitesini dağıtma](#deploy)

2. [Storefront yapılandırma](#configure)

3. [Storefront üzerinde Transact](#transact)

### <a name="deploy"></a>Dağıtma

Dağıtım seçenekleri:

- GitHub 'dan [Iş Ortağı Merkezi storefront örnek kodunu](https://github.com/Microsoft/Partner-Center-Storefront) indirin
- Yapılandırılmış Web sitesini dağıtmak için Azure ile tümleştirin
- Mevcut bir abonelikte dağıtın veya kendi aboneliğinizi getirin

### <a name="configure"></a>Yapılandırma

Bir storefront özelleştirmek için geliştirme becerileri gerekmez.

Yapılandırmak için Iş ortağı merkezi yönetici kimlik bilgilerinizle oturum açın:

- **Marka**: şirket adı, logo, kişiler ve daha fazlası.

- **Teklifler**: tüm CSP tekliflerini görüntüleyin. Müşterilerinizin görüntüleyebileceği ve satın alabileceğiniz teklifleri seçebilirsiniz. Ayrıca teklif bilgilerini kişiselleştirebilir ve fiyatlarınızı ekleyebilirsiniz.

- **PayPal ödeme yapılandırması**: PayPal ödeme hesabı bilgilerinizi ekleyin. PayPal hesabınız yoksa [https://www.paypal.com](https://www.paypal.com) Yeni bir hesap ziyaret edebilir ve yeni bir hesap oluşturabilirsiniz. Bu hesap, PayPal için, müşteriler tarafından yapılan ödemeleri alacak şekilde kullanılacaktır. *Microsoft, iş ortakları ve PayPal arasındaki ilişkiden sorumlu değildir. PayPal kullanımı, iş ortağının veya iş ortağının müşterilerinin ek koşulları kabul etmesi için gerekli olabilir.*

- (*Hindistan için*) **PayU ödeme yapılandırması**: PayU para ödeme hesabı bilgilerinizi ekleyin. Bir PayU para hesabınız yoksa [https://www.payumoney.com/](https://www.payumoney.com/) Yeni bir hesap ziyaret edebilir ve yeni bir hesap oluşturabilirsiniz. Bu hesap PayU 'nin müşteriler tarafından yapılan ödemeleri alacağı şekilde kullanılacaktır. *Microsoft, iş ortakları ve PayU arasındaki ilişkiden sorumlu değildir. PayU kullanımı, iş ortağının veya iş ortağının müşterilerinin ek koşulları kabul etmesi için gerekli olabilir.*

### <a name="transact"></a>İşlem

- Dağıtımdan sonra müşteriler hemen satın alabilir ve Transact.

- Müşteriler, Iş Ortağı Merkezi SDK ile tümleştirilmiş iş ortağı portalından doğrudan satın alabilir.

#### <a name="customer-countries"></a>Müşteri ülkeleri

Müşteriler bu ülkelere ait olabilir:

| Ülke Kodu | Ülke Adı   |
|--------------|----------------|
| AU           | Avustralya      |
| AT           | Avusturya        |
| BE           | Belçika        |
| BG           | Bulgaristan       |
| CA           | Kanada         |
| HR           | Hırvatistan        |
| CY           | Kıbrıs         |
| CZ           | Çek Cumhuriyeti |
| DK           | Danimarka        |
| EE           | Estonya        |
| FI           | Finlandiya        |
| GS           | Fransa         |
| DE           | Almanya        |
| GR           | Yunanistan         |
| HU           | Macaristan        |
| IS           | İzlanda        |
| IN           | Hindistan          |
| IE           | İrlanda        |
| BT           | İtalya          |
| JP           | Japonya          |
| LV           | Letonya         |
| LI           | Liechtenstein  |
| LT           | Litvanya      |
| LU           | Lüksemburg     |
| MT           | Malta          |
| MC           | Monako         |
| NL           | Hollanda    |
| NZ           | Yeni Zelanda    |
| NO           | Norveç         |
| SATıNALMA           | Polonya         |
| PT           | Portekiz       |
| RO           | Romanya        |
| SK           | Slovakya       |
| SL           | Slovenya       |
| ES           | İspanya          |
| SE           | İsveç         |
| CH           | İsviçre    |
| GB           | Birleşik Krallık |
| ABD           | Birleşik Devletler  |

## <a name="partner-experience-scenarios"></a>İş ortağı deneyimi senaryoları

### <a name="deployment-scenario"></a>Dağıtım senaryosu

Gelişmiş veya özelleştirilmiş bir CSP müşteri storefront dağıtmak için:

- Ek özelleştirmeler yapmak için [Iş Ortağı Merkezi storefront örnek kodunu](https://github.com/Microsoft/Partner-Center-Storefront) indirin.

- Geliştirmek için Microsoft Visual Studio 2015 (veya üzeri) kullanın.

- Ek değişiklikler ve geliştirmeler için derleyin (yetkilendirmeler, sertifikalar, bildirim değişiklikleri ve diğer öğeler dahil).

### <a name="configuration-scenario"></a>Yapılandırma senaryosu

- Yeni oluşturulan Web sitesi bir iş ortağı kiracısına bağlanır ve bu iş ortağı kiracının tüm yönetim hesaplarına erişimi vardır.

  - İş ortakları, Iş ortağı merkezi yönetici kimlik bilgilerini kullanarak bu yeni Web sitesinde oturum açabilir.

- Storefront uygulaması şu anda Fransızca, Ispanyolca, Felemenkçe, Almanca, Japonca ve Ingilizce 'yi desteklemektedir. (İngilizce, geri dönüş dili olarak hizmet verir.)

  - Storefront, ortağın iş ortağı merkezindeki iş ortağının profilinden varsayılan yerel ayarını kullanarak yerel ayarı yapılandırır. Bu yerel ayar, depoda para birimlerini, tarih biçimlerini ve yerelleştirilmiş teklifleri yapılandırmak için kullanılır.

- İş ortakları marka, teklif ve PayPal ya da PayU (Hindistan için) ödeme bilgilerini yapılandırabilir.

- İş ortakları şirket adını, Şirket logosunu, başlık görüntüsünü, satışları ve destek kişilerini ve daha fazlasını güncelleştirebilir.

- İş ortakları, bölgelerine göre kullanılabilir tüm CSP tekliflerini görebilir.

  - İş ortakları, tüm müşterilerine hangi teklifleri göstermek istediğinizi seçebilir.

  - CSP iş ortağı bir veya daha fazla teklif seçebilir ve ad, miktar, özellik açıklaması ve fiyat ' ı güncelleştirebilir.
  - Fiyat, yıllık fiyatıdır. Müşteriler yıllık olarak abone olur.

- İş ortakları, (a) tüm mevcut ve gelecekteki müşteriler ya da (b) belirli müşteriler için önceden onaylanmış işlemleri yapılandırabilir.

  - Önceden onaylanan müşterilerin yeni abonelikler eklerken, var olan aboneliklerde ek lisanslar satın alması veya bir aboneliği yenilemeleri durumunda portal üzerinde ödeme yapması gerekmez.

  - Önceden onaylanmış müşteriler, bu işlemler sırasında ödeme için PayPal veya PayU 'ya (Hindistan için) yeniden yönlendirilmeyecektir.

  - Önceden onaylanmış müşteri işlemleri, bir ortağın, önceden onaylanmış müşterilerine çevrimdışı faturalandırma ve faturalandırma yapmasına izin verir.

- Bir CSP iş ortağı PayPal Istemci KIMLIĞI ve gizli dizisi gibi PayPal hesap bilgilerini girişi yapabilir. CSP iş ortağı Ayrıca, bir korumalı alan veya canlı hesap kullanarak test etmek isteyip istemediğinizi de seçebilir.

  - İş ortakları, bu bilgileri [https://developer.paypal.com/](https://developer.paypal.com/) **uygulamalarımın & kimlik bilgileriyle** bulabilir. Bu bilgileri geçerli bir uygulamadan veya PayPal 'de yeni bir uygulama oluşturarak da alabilirsiniz.
  - Henüz bir tane yoksa yeni bir PayPal hesabı oluşturun. Bu hesap, PayPal için, müşteriler tarafından yapılan ödemeleri alacak şekilde kullanılacaktır.

    - PayPal iş hesabını açmak için bkz [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) ..

    - PayPal korumalı alan hesabı oluşturmak için bkz [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) ..

- (Hindistan için) bir CSP iş ortağı PayU Istemci KIMLIĞI ve parolası gibi PayU para hesabı bilgilerini girişi yapabilir. İş ortakları hakkında daha fazla bilgi bulabilir [https://developer.payumoney.com/](https://developer.payumoney.com/) .

  - Henüz yoksa, yeni bir PayU para hesabı oluşturun. Bir PayU para hesabını açmak için, adresini ziyaret edin [https://www.payumoney.com/merchant-account/#/](https://www.payumoney.com/merchant-account/#/) . Bu hesap PayU 'nin müşteriler tarafından yapılan ödemeleri alacağı şekilde kullanılacaktır.

## <a name="customer-experience-scenarios"></a>Müşteri deneyimi senaryoları

### <a name="new-customer-sign-up-scenario"></a>Yeni müşteri kaydolma senaryosu

- Varsayılan olarak, Web sitesi genel kullanıma sunulmuştur ve giriş sayfasında iş ortağının kataloğunu gösterir.

- Müşteriler artık çok sayıda [Müşteri ülkelerine](#customer-countries)ait olabilir.

- Bu odak Avrupa 'daki ücretsiz Ticaret Birliği (EFTA) ülkelerinde, Kuzey Amerika, Japonya, Hindistan, Avustralya ve Yeni Zelanda bölgelerinde yer alır.
  - Bu özellik, Iş Ortağı Merkezi SDK 'sında bölgesel yetkilendirme desteğini kullanır.

- Müşteriler, katalogdan satın alma için bir teklif seçebilir.
  - Müşteri adlarını, adreslerini ve etki alanıyla ilgili bilgileri ekleyebilirler.

- Müşteriler PayPal veya PayU (Hindistan için) kullanıma alma deneyimine yönlendirilir. Müşteriler, aşağıdakileri kullanarak ödeme sağlayabilir:
  - Mevcut PayPal veya PayU (Hindistan için) hesabı
  - Bu kişilerin ülkesinde PayPal veya PayU tarafından desteklenen komik araçlar (Hindistan için). Bunlar, kredi kartları, banka kartları ve banka hesaplarını geçerli olarak içerebilir.

- Bu müşteri için bir müşteri kiracının oluşturulması. Kiracı siparişi başarıyla oluşturulduktan sonra müşterilere hesap Kullanıcı adı, parola ve abonelik ayrıntıları verilir.
  - Müşteriler Kullanıcı adını ve parolayı kaydederek daha fazla satın alma işlemleri için oturum açabilir.
  - Her abonelik bir yıl boyunca satın alınır ve müşteriler abonelik bitiş tarihinden önce 30 gün içinde yenileyebilirler.

### <a name="view-prior-purchases-scenario"></a>Önceki satın alma senaryosunu görüntüleyin

- Müşteri, müşteri kiracısı Kullanıcı adı ve parolasıyla oturum açar ve **emirlerim** bölümüne gider.

- Müşteriler, satın alınan abonelikleri görüntüleyebilecekleri ve gerekirse güncelleştirmeler yapabileceğiniz **siparişler** sayfasına gidebilir.

- Müşteriler, Iş Ortağı Merkezi 'nde tutuldukları dahil olmak üzere tüm abonelikleri (lisans tabanlı ve kullanım tabanlı) görüntüleyebilecekleri **Aboneliklerim** sayfasına gidebilir.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Mevcut abonelikler senaryosuna lisans ekleme

- Müşteriler, **mevcut** aboneliklere daha fazla lisans ekleyebilir. Müşteriler, abonelik yılı sırasında dilediğiniz zaman daha fazla lisans ekleyebilir.

- Her eklenen lisans Aboneliğin bitiş tarihini değiştirmez. Bununla birlikte, aboneliğin fiyatı, lisansı eklediğiniz tarihe ve bu tarihin yılda bulunduğu konuma göre değişir. Fiyatlandırma, gün başına eşit olarak dağıtılır ve yalnızca yılın kalan günleri için ücretlendirilir.

### <a name="add-more-subscriptions-scenario"></a>Daha fazla abonelik ekleyin senaryosu

- Müşteriler istediğiniz zaman herhangi bir **sayıda abonelik satın** **alabilir.**

- Bir müşteri bir abonelik seçebilir, bir miktar ekleyebilir ve işlemi tamamlamaya ve aboneliği hemen kullanmaya başlayabilirler. Müşteri önceden onaylanmış bir müşterisiyse, abonelik hemen kullanılabilir ve müşteriye ödeme için bir fatura gönderilir.

### <a name="renew-subscription-scenario"></a>Aboneliği Yenile senaryosu

- Bir müşteri, abonelik bitiş tarihinden önce son 30 gün içinde bir aboneliği yenileyebilirler.

- Bu yalnızca son 30 gün içinde kullanılabilir.

- Son 30 gün içinde yenilenmezse abonelik, bu müşteri kiracının abonelikleri listesinden kaldırılır.

- Yenileme sırasında miktarı güncelleştiremezsiniz.

### <a name="payments-scenario"></a>Ödemeler senaryosu

- Müşteri işlemler için yönetici tarafından önceden onaylanırsa, yukarıdaki senaryolar için ödeme deneyimi sunulmaz. Bunun yerine, iş ortağı fatura ödemesini önceden onaylanan müşteriye gönderebilir.

- Tüm yeni satın almalar için daha fazla lisans ekleyebilir, abonelik ekleyebilir ve yenileme işlemleri yapabilirsiniz. Müşteri, bu Web sitesini PayPal veya PayU aracılığıyla kullanarak bir iş ortağı ödeyebilir (Hindistan için).

- Bu web sitesi PayPal veya PayU (Hindistan için) ile tümleşiktir ve iş ortaklarının müşterilerinin ödemelerini kabul etmesine olanak tanır. PayPal veya PayU (Hindistan için), bu miktarı bir iş ortağının hesabında alacaklandırır. PayPal veya PayU (Hindistan için) banka hesabı yönetimi, bu Web sitesinin dışındadır ve sırasıyla PayPal.com veya PayUmoney.com üzerinde yönetilir.

- Bu, PayPal.com veya PayUmoney.com adresinden PayPal orPayU (Hindistan için) ödeme yapılandırmasını yapılandıran iş ortaklarına bağımlıdır. Microsoft bu bilgileri veya bu seçeneği kullanmanın sonucu olan gerçek ödeme işlemlerini kaydetmez.

### <a name="prorated-pricing-scenario"></a>Eşit olarak dağıtılmış fiyatlandırma senaryosu

- Bu web sitesi, müşterilerin mevcut bir aboneliğe daha fazla lisans eklemesi durumunda eşit oranda dağıtılmış fiyatlandırmayı destekler.

- Her aboneliğin süresi bir yıl sonra dolar ve abonelik satın alındıktan sonra değiştirilemez.

- Aboneliğin bitiş tarihi, ek lisanslar eklenerek değişmeyecektir. Müşteriler bitiş tarihine kadar kalan gün sayısı üzerinden ücretlendirilecektir. Örneğin, günde bir abonelik ücreti $365 ise ve iki güne de bir lisans eklerseniz, yeni lisansın fiyatı $364 olacaktır. Daha sonra 10 gün daha daha bir lisans eklerseniz, Fiyat $354 olur.
