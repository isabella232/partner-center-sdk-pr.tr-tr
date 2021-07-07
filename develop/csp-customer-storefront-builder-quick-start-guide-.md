---
title: CSP Müşteri Vitrini Oluşturucusu Hızlı Başlangıç Kılavuzu
description: CSP Customer Storefront Builder'ı kullanarak bulut çözümü sağlayıcısı (CSP) tekliflerini satmak için çevrimiçi bir market oluşturun.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8550492c7a4201a955c7b051b453103628612f3e
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973358"
---
# <a name="csp-customer-storefront-builder-quick-start-guide"></a>CSP Müşteri Vitrini Oluşturucusu Hızlı Başlangıç Kılavuzu

CSP Customer Storefront Builder'ı kullanarak bulut çözümü sağlayıcısı (CSP) tekliflerini satmak için çevrimiçi bir market oluşturun.

## <a name="introduction-to-the-csp-customer-storefront-builder"></a>CSP Customer Storefront Builder'a giriş

CSP Customer Storefront Builder, iş ortaklarının müşterilerine CSP tekliflerini satmaları için kolayca çevrimiçi bir market oluşturmalarına yardımcı olur. Çoğu iş ortağı ve küçük satış kuruluşu, çevrimiçi bir market geliştirmek yerine satışa odaklanmak istiyor. Örnek İş Ortağı Merkezi SDK'sı web sitesi oluşturmak ve dağıtmak için yazılım geliştirme becerilerine ihtiyaç vardır. CSP Customer Storefront Builder ile hızlı ve kolay bir şekilde kendi web sitenizi oluşturabilirsiniz. Ayrıca örnek kod olarak web sitesini indirebilir veya Transact'e Hazır web sitesiyle doğrudan Azure aboneliğinize dağıtabilirsiniz.

Bu web sitesi tamamen iş ortakları tarafından sahip olunan, desteklenen ve bakımı yapılan bir web sitesidir ve Microsoft web sitesinden herhangi bir veri veya telemetri toplamaz. CSP Customer Storefront Builder, ödeme kartı sektör veri [](https://www.pcisecuritystandards.org/) güvenliği standardı (PCI DSS) ile tamamen uyumlu olan iş ortağı için bir web PCI DSS.

CSP Customer Storefront Builder kodu, [EULA'daki](/legal/partner-center/eula-partner-center-sdk)İş Ortağı Merkezi SDK'sı tabi olur.

>[!NOTE]
>Vitrin web sitesi yönetiminden, bakımdan ve web sitesi oluşturma sonucunda ortaya çıkan sorunlar sizin sorumluluğundadır. [İş Ortağı Merkezi SDK'sı EULA'daki terimleri okuyun ve anlıyoruz.](/legal/partner-center/eula-partner-center-sdk)

Ek bilgi için şu makalelere de bakın: [CSP müşteri web vitrini](csp-customer-web-storefront.md) ve [konsol test uygulaması](console-test-app.md).

## <a name="considerations"></a>Dikkat edilmesi gerekenler

CSP Customer Storefront Builder, web sitesi oluşturmanın hızlı bir yolu olarak tasarlanmıştır. Planlamanız sırasında aşağıdaki önemli noktalara dikkat edilmesi gerekir:

- Microsoft ve İş Ortağı Merkezi, dağıtıldıktan sonra iş ortağı web sitesinin bir kopyasını veya CSP Customer Storefront Builder'a eklenen bilgileri korumaz.

- İş Ortağı Merkezi csP Customer Storefront web sitesini yalnızca iş ortağının Azure abonelikleri için dağıtabilirsiniz.

- Bu web sitesi dağıtıldıktan sonra tamamen iş ortağına aittir ve iş ortağı tarafından yönetilir. Microsoft'un bu web sitesine veya web sitesiyle ilgili verilere erişimi yok. İş ortakları web sitesinin bakım ve yönetiminden sorumludur. Microsoft, CSP Customer Storefront Builder veya CSP Customer Storefront Builder kullanılarak oluşturulan herhangi bir web sitesi ile ilgili herhangi bir canlı web sitesi veya başka destek sağlamaz.

- İş Ortağı Merkezi yeni veya değiştirilmiş SDK ya da API özellikleriyle bu web sitesine doğrudan erişenin veya web sitesini yükseltesiniz. Yeni özellikler veya geliştirmeler, iş ortakları tarafından sahip olunmalı, geliştirilmeli ve yönetilmeli ve iş ortakları tarafından yönetilmeli ve yeni İş Ortağı Merkezi SDK'sı api özellikleri ekleme de dahil olmak üzere.

- Bu CSP Customer Storefront Builder şu anda bir PayPal Pro/PayU Money (Hindistan için) hesabına ödeme yapılandırma olanağı sağlar. İş ortaklarının ödeme işlemcisini değiştirmesi gerekirse, tercih ettiği ödeme yöntemini desteklemek için kodu değiştirmesi gerekir.

- CSP Customer Storefront Builder'a eklenen ödemeyle ilgili bilgiler, İş Ortağı Merkezi.

- PayPal yapılandırması, yapılandırmanın kullanılabilir olduğu tüm PayPal çalışır. PayPal kullanılabilirlik ve destek yalnızca PayPal tarafından denetlenmektedir ve herhangi bir zamanda kullanımdan kaldır PayPal.

- PayU ödeme yapılandırması şu anda yalnızca Hindistan'da çalışır. PayU kullanılabilirliği ve desteği yalnızca PayU tarafından denetlenmektedir ve PayU tarafından herhangi bir zamanda kullanımdan kaldırılaabilmektedir.

- [İş Ortağı Merkezi SDK'sı EULA'daki terimleri okuyun ve anlıyoruz.](/legal/partner-center/eula-partner-center-sdk)

## <a name="using-the-csp-customer-storefront-builder"></a>CSP Customer Storefront Builder'ı kullanma

İş Ortağı Merkezi CSP iş ortağı yöneticileri doğrudan İş Ortağı Merkezi. En az çabayla, iş ortağının kiracısına yeni bir web sitesi dağıtılabilir. İş ortakları dağıtıldıktan sonra web sitesini kullanarak markayı, teklifleri ve ödemeyle ilgili bilgileri yapılandırarak web sitesi URL adresini müşterilerle paylaşabilir.

Vitrin web sitesi oluşturma işlemi şunları yapmaktır:

1. [Web sitesini dağıtma](#deploy)

2. [Vitrini yapılandırma](#configure)

3. [Vitrinde işlem](#transact)

### <a name="deploy"></a>Dağıtma

Dağıtım seçenekleri:

- İş Ortağı Merkezi [storefront örnek kodunu GitHub](https://github.com/Microsoft/Partner-Center-Storefront)
- Yapılandırılmış web sitesini dağıtmak için Azure ile tümleştirin
- Mevcut bir abonelikte dağıtma veya kendi aboneliğinizi getirme

### <a name="configure"></a>Yapılandırma

Vitrini özelleştirmek için geliştirme becerisi gerekmez.

Şunları yapılandırmak için İş Ortağı Merkezi yönetici kimlik bilgilerinizle oturum açma:

- **Markalama:** şirket adı, logo, kişiler ve daha fazlası.

- **Teklifler:** Tüm CSP tekliflerini görüntüleme. Müşterilerinize hangi tekliflerin görüntüleye ve satın alınarak satın alınalarını seçerek. Ayrıca teklif bilgilerini kişiselleştirin ve fiyatınızı ekleyin.

- **PayPal yapılandırması:** Ödeme PayPal bilgilerini ekleyin. Bir hesap hesabınız yoksa PayPal yeni bir hesap [https://www.paypal.com](https://www.paypal.com) oluşturabilirsiniz. Bu hesap, müşteriler tarafından PayPal kredisi almak için kullanılacaktır. *İş ortakları ile iş ortakları arasındaki ilişkiDen Microsoft PayPal. Bu PayPal, iş ortağının veya iş ortağının müşterilerinin ek koşulları kabul etmiş olabilir.*

- (*Hindistan için*) **PayU Ödeme yapılandırması:** PayU Para ödeme hesabı bilgilerini ekleyin. PayU Money hesabınız yoksa, ziyaret edin ve yeni [https://www.payumoney.com/](https://www.payumoney.com/) bir hesap oluşturun. Bu hesap, Müşteriler tarafından yapılan ödemelerin kredisi için PayU için kullanılır. *İş ortakları ile PayU arasındaki ilişki Microsoft'un sorumluluğunda değildir. PayU'nun kullanımı, iş ortağının veya iş ortağının müşterilerinin ek koşulları kabul etmiş olabilir.*

### <a name="transact"></a>İşlem

- Dağıtımdan sonra müşteriler hemen satın alma ve işlemde olabilir.

- Müşteriler doğrudan iş ortağı portalıyla tümleştirilmiş iş ortağı portalını İş Ortağı Merkezi SDK'sı.

#### <a name="customer-countries"></a>Müşteri ülkeleri

Müşteriler şu ülkelere ait olabilir:

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

- geliştirmek için Microsoft Visual Studio 2015 (veya üzeri) kullanın.

- Ek değişiklikler ve geliştirmeler için derleyin (yetkilendirmeler, sertifikalar, bildirim değişiklikleri ve diğer öğeler dahil).

### <a name="configuration-scenario"></a>Yapılandırma senaryosu

- Yeni oluşturulan Web sitesi bir iş ortağı kiracısına bağlanır ve bu iş ortağı kiracının tüm yönetim hesaplarına erişimi vardır.

  - İş ortakları, Iş ortağı merkezi yönetici kimlik bilgilerini kullanarak bu yeni Web sitesinde oturum açabilir.

- Storefront uygulaması şu anda Fransızca, Ispanyolca, Felemenkçe, Almanca, Japonca ve Ingilizce 'yi desteklemektedir. (İngilizce, geri dönüş dili olarak hizmet verir.)

  - Storefront, ortağın iş ortağı merkezindeki iş ortağının profilinden varsayılan yerel ayarını kullanarak yerel ayarı yapılandırır. Bu yerel ayar, depoda para birimlerini, tarih biçimlerini ve yerelleştirilmiş teklifleri yapılandırmak için kullanılır.

- iş ortakları marka, teklif ve PayPal veya payu (hindistan için) ödeme bilgilerini yapılandırabilir.

- İş ortakları şirket adını, Şirket logosunu, başlık görüntüsünü, satışları ve destek kişilerini ve daha fazlasını güncelleştirebilir.

- İş ortakları, bölgelerine göre kullanılabilir tüm CSP tekliflerini görebilir.

  - İş ortakları, tüm müşterilerine hangi teklifleri göstermek istediğinizi seçebilir.

  - CSP iş ortağı bir veya daha fazla teklif seçebilir ve ad, miktar, özellik açıklaması ve fiyat ' ı güncelleştirebilir.
  - Fiyat, yıllık fiyatıdır. Müşteriler yıllık olarak abone olur.

- İş ortakları, (a) tüm mevcut ve gelecekteki müşteriler ya da (b) belirli müşteriler için önceden onaylanmış işlemleri yapılandırabilir.

  - Önceden onaylanan müşterilerin yeni abonelikler eklerken, var olan aboneliklerde ek lisanslar satın alması veya bir aboneliği yenilemeleri durumunda portal üzerinde ödeme yapması gerekmez.

  - önceden onaylanmış müşteriler, bu işlemler sırasında ödeme için PayPal veya payu (hindistan için) olarak yeniden yönlendirilmeyecektir.

  - Önceden onaylanmış müşteri işlemleri, bir ortağın, önceden onaylanmış müşterilerine çevrimdışı faturalandırma ve faturalandırma yapmasına izin verir.

- CSP iş ortağı, PayPal istemci kimliği ve gizli dizi gibi PayPal hesap bilgilerini girişi yapabilir. CSP iş ortağı Ayrıca, bir korumalı alan veya canlı hesap kullanarak test etmek isteyip istemediğinizi de seçebilir.

  - İş ortakları, bu bilgileri [https://developer.paypal.com/](https://developer.paypal.com/) **uygulamalarımın & kimlik bilgileriyle** bulabilir. Ayrıca, bu bilgileri geçerli bir uygulamadan veya PayPal yeni bir uygulama oluşturarak alabilirsiniz.
  - henüz yoksa yeni bir PayPal hesabı oluşturun. bu hesap, müşteriler tarafından yapılan ödemeleri kredi PayPal için kullanılacaktır.

    - PayPal iş hesabını açmak için bkz [https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register](https://developer.paypal.com/docs/classic/lifecycle/goingLive/#register) ..

    - PayPal bir korumalı alan hesabı oluşturmak için bkz [https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/](https://developer.paypal.com/docs/classic/lifecycle/ug_sandbox/) ..

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

- müşteriler PayPal veya payu (hindistan için) kullanıma alma deneyimine yönlendirilir. Müşteriler, aşağıdakileri kullanarak ödeme sağlayabilir:
  - mevcut PayPal veya payu (hindistan için) hesabı
  - PayPal veya payu (hindistan için) tarafından ülkenizde desteklenen komik araçlar. Bunlar, kredi kartları, banka kartları ve banka hesaplarını geçerli olarak içerebilir.

- Bu müşteri için bir müşteri kiracının oluşturulması. Kiracı siparişi başarıyla oluşturulduktan sonra müşterilere hesap Kullanıcı adı, parola ve abonelik ayrıntıları verilir.
  - Müşteriler, daha fazla satın alma için oturum açmış olarak kalmak için kullanıcı adını ve parolayı kaydedebilir.
  - Her abonelik bir yıl boyunca satın alınmaktadır ve müşteriler, abonelik bitiş tarihinden 30 gün önce yenilemektedir.

### <a name="view-prior-purchases-scenario"></a>Önceki satın alma senaryosunu görüntüleme

- Müşteri, Müşteri kiracısı kullanıcı adı ve parolasıyla oturum alır ve **Siparişlerim bölümüne** gider.

- Müşteriler, satın alınan **abonelikleri görüntüleyebilirsiniz** ve gerekirse güncelleştirmeler yapmak için Siparişlerim sayfasına gidin.

- Müşteriler, aboneliklerde **bakımı** yapılanlar dahil olmak üzere tüm abonelikleri (lisans tabanlı ve kullanım tabanlı) görüntüley oldukları Aboneliklerim sayfasına İş Ortağı Merkezi.

### <a name="add-licenses-to-existing-subscriptions-scenario"></a>Mevcut aboneliklere lisans ekleme senaryosu

- Siparişlerim **bölümünde** müşteriler mevcut aboneliklere daha fazla lisans ekleyebilir. Müşteriler abonelik yılı boyunca dilediğiniz zaman daha fazla lisans ekleyebilir.

- Eklenen her lisans, aboneliğin bitiş tarihini değiştirmez. Ancak aboneliğin fiyatı, lisansı ekley istediğiniz tarihe ve bu tarihin yıl içinde bulunduğu tarihe göre değişir. Fiyatlandırma, yalnızca yılın kalan günlerini ücretlendirmek için günlük olarak protrat edilir.

### <a name="add-more-subscriptions-scenario"></a>Daha fazla abonelik ekleme senaryosu

- Müşteriler, Siparişlerim bölümündeki Abonelik ekle bölümünden istediğiniz **zaman istediğiniz** sayıda abonelik **satın alabilir.**

- Müşteri bir abonelik seçer, miktar ekleyebilir ve işlemi tamamlamak için ödeme yapmak ve aboneliği hemen kullanmaya başlayabilir. Müşteri önceden onaylanmış bir müşteri ise abonelik hemen kullanılabilir ve ödeme için müşteriye bir fatura gönderilir.

### <a name="renew-subscription-scenario"></a>Abonelik yenileme senaryosu

- Müşteri, abonelik bitiş tarihinden önceki son 30 gün içinde aboneliği yeniler.

- Bu yalnızca son 30 gün içinde kullanılabilir.

- Son 30 gün içinde yenilenmezse, abonelik bu Müşteri kiracısı için abonelik listesinden kaldırılır.

- Yenileme sırasında miktarı güncelleştiresiniz.

### <a name="payments-scenario"></a>Ödemeler senaryosu

- Müşteri, yönetici tarafından işlemler için önceden onaylanırsa, yukarıdaki senaryolar için ödeme deneyimi sunlanmaz. Bunun yerine iş ortağı, ödeme için faturayı önceden onaylanmış müşteriye gönderebilir.

- Tüm yeni satın alma işlemleri için daha fazla lisans ekleyebilir, abonelik ekleyebilir ve yenileyebilirsiniz. Müşteri bu web sitesini kullanarak bir iş ortağına PayPal (Hindistan için) üzerinden ödemesi olabilir.

- Bu web sitesi, PayPal veya PayU (Hindistan için) ile tümleştirilmiştir ve iş ortaklarının müşterilerinden ödemeleri kabul etmelerini sağlar. PayPal veya PayU (Hindistan için) bu tutarı bir iş ortağının hesabında krediler. PayPal veya PayU (Hindistan için) Banka hesap yönetimi bu web sitesinin dışındadır ve sırasıyla PayPal.com veya PayUmoney.com yönetilir.

- Bu, iş ortaklarının PayPal.com veya PayPal adresinden ödeme yapılandırmasına veyaPayU (Hindistan için) ödeme yapılandırmasına PayUmoney.com. Microsoft bu bilgilerin veya bu seçeneğin kullanımından elde edilen gerçek ödeme işlemlerini kaydetmez.

### <a name="prorated-pricing-scenario"></a>Prorated fiyatlandırma senaryosu

- Bu web sitesi, müşterilerin mevcut aboneliğe daha fazla lisans eklemesi durumlarında prokratlı fiyatlandırmayı destekler.

- Her aboneliğin süresi bir yıl sonra dolar ve abonelik satın alındikten sonra değiştirilemez.

- Ek lisanslar ekleyerek aboneliğin bitiş tarihi değişmez. Müşteriler, bitiş tarihine kadar kalan gün sayısı için ücret tahsil edilecektir. Örneğin, ilk günde abonelik maliyeti 365 ABD doları ise ve iki. günde bir lisans daha eklersiniz, yeni lisansın fiyatı 364 ABD doları olur. 10 gün sonra bir lisans daha eklersiniz, fiyat 354 ABD doları olur.
