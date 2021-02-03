---
title: İş Ortağı Merkezi’nde API erişimini ayarlama
description: Iş Ortağı Merkezi SDK 'sında geliştirme ve tümleştirme korumalı alanında test için hesapları ayarlayın.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2020
ms.locfileid: "97769418"
---
# <a name="set-up-api-access-in-partner-center"></a>İş Ortağı Merkezi’nde API erişimini ayarlama

**Uygulama hedefi:**

- İş Ortağı Merkezi
- 21Vianet tarafından çalıştırılan iş ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi
- Microsoft Bulut Almanya için İş Ortağı Merkezi

Bu makalede, Iş Ortağı Merkezi SDK 'sına karşı geliştirme yapmanız gereken hesaplar açıklanmaktadır. Bu makalede ayrıca Integration Sandbox [hesabının](#integration-sandbox-account) nasıl oluşturulacağı ve tümleştirme korumalı alanında nasıl test kurulacağı açıklanmaktadır.

>[!NOTE]
>API 'lere erişim sağlamak için kiracınızın bir CSP kiracısı olması ve dolaylı bir sağlayıcı ya da doğrudan fatura ortağı olmanız gerekir.

## <a name="account-definitions"></a>Hesap tanımları

Iş Ortağı Merkezi, API tümleştirmenizi tümleştirmenize ve test etmenize yardımcı olmak için iki hesap türünü destekler:

### <a name="primary-partner-account"></a>Birincil Iş ortağı hesabı

Bu hesap, gerçek müşteriler için gerçek siparişler oluşturduğunuz yerdir. Birincil hesapta oturum açtığınızda, Iş Ortağı Merkezi SDK 'sını veya Iş ortağı panosu Kullanıcı arabirimini kullanarak herhangi bir değişiklik veya işlem yaparsanız, bunlar gerçek müşteriler için resmi siparişler olarak değerlendirilir. Bunlar faturanızda yansıtılır ve şirketiniz bu ücret ödemekten sorumludur.

### <a name="integration-sandbox-account"></a>Tümleştirme korumalı alanı hesabı

Bu hesap, büyük çapta dağıtmadan önce kodunuzun test edilmesine ve Iş Ortağı Merkezi API 'Leriyle tümleştirilmesine yöneliktir. Tümleştirme korumalı alanı hesabında oturum açtığınızda yaptığınız değişiklikler ve işlemler faturanızda görünür, ancak fatura tutarını ödemek zorunda değilsiniz. Fatura PDF 'sine "ödeme yapmayın" olarak bir vazgeçme belgesi sunulacaktır. BU BIR KORUMALı ALAN FATURADıR VE HERHANGI BIR EYLEM GEREKMEZ. "

Tümleştirme korumalı alanı hesabı ve birincil hesap bağımsız olarak davranır ve yönetici hesaplarını, Kullanıcı hesaplarını, müşterileri, siparişleri, abonelikleri veya diğer verileri paylaşmazlar.

Tümleştirme korumalı alanı, sınırlı sayıda müşteri, sipariş, abonelik, lisans vb. ile işlemleri destekler.

İlkeye göre, tümleştirme korumalı alanı hesapları yalnızca tümleştirme testi amaçlıdır.

Varsayılan olarak tümleştirme korumalı alan hesabı yoktur. Iş Ortağı Merkezi SDK 'sını kullanmayı planlıyorsanız bir tane oluşturmanız gerekir.

## <a name="set-up-your-accounts"></a>Hesaplarınızı ayarlama

Bu bölümde, Iş Ortağı Merkezi SDK 'Sı için bir birincil Iş ortağı hesabının ve bir tümleştirme korumalı alanı hesabının nasıl ayarlanacağı açıklanmaktadır.

### <a name="create-an-integration-sandbox"></a>Tümleştirme korumalı alanı oluşturma

1. Genel yönetici hesabıyla (birincil Iş ortağı hesabınız) Iş ortağı panosunda oturum açın.

2. **Ayarlar** menüsünde (dişli simgesi), **iş ortağı ayarları**' nı seçin.

3. **Tümleştirme korumalı alanı** sekmesini seçin.

    >[!NOTE]
    >Tümleştirme korumalı alanı seçeneğini görmüyorsanız, genel yönetici hesabınız olmayabilir. Aynı zamanda bir tümleştirme korumalı alanı hesabı kullanıyor olabilirsiniz ve bir tümleştirme korumalı alanı zaten ayarlanmış olabilir.

4. Integration Sandbox yönetici hesabı için iletişim bilgilerini girin. Ardından **Hesap oluştur**' u seçin. Hesabın oluşturulduğunu belirten bir onay iletisi için birkaç dakika bekleyin.

5. Onay iletisini görbaşladıktan sonra Iş ortağı panosunun oturumunu kapatın.

6. Yeni tümleştirme korumalı alanı Yönetici hesabınızla yeniden oturum açın. **username@domain** Kimlik bilgilerinizin biçimini, yeni belirttiğiniz parolayla birlikte kullandığınızdan emin olun.

7. Korumalı alan hesabı kurulumunu gerçekleştirmek için **geçerli görevlerin** yukarısında **hesabı ayarla** ' yı seçin.

### <a name="enable-api-access"></a>API erişimini etkinleştir

Hesabınız ayarlandıktan sonra, İş Ortağı Merkezi SDK'sını tümleştirme korumalı alanıyla kullanabilmek için öncelikle API erişimini etkinleştirmeniz gerekir. Hem birincil İş Ortağı hesabınız hem de tümleştirme korumalı alanı hesabınız için API erişimini ayrı ayrı etkinleştirmelisiniz.

1. Genel yönetici hesabı kullanarak Iş ortağı panosunda oturum açın.

2. **Ayarlar** menüsünde (dişli simgesi), **iş ortağı ayarları**' nı seçin.

3. **Hesap ayarları** sayfasında, **uygulama yönetimi**' ni seçin.

4. Zaten mevcut bir uygulamanız yoksa, yeni bir Web uygulaması ekleyin. Mevcut bir Web uygulamanız varsa **anahtar Ekle** düğmesini seçin.

5. Uygulama kayıt bilgilerini, özellikle de bir Web uygulaması oluşturuyorsanız ve güvenli bir yerde depoluyorsanız bu **anahtarı** kopyalayın.

6. Iş ortağı panosunun oturumunu kapatın.

7. Tümleştirme korumalı alanı hesabınızla yeniden oturum açın. Tümleştirme korumalı alanında API erişimini etkinleştirmek için 2-5 arasındaki adımları yineleyin.

## <a name="write-and-test-code"></a>Kod yazın ve test edin

Tümleştirme korumalı alanında kod ve test kodu yazabilirsiniz. Azure AD ile [Iş ortağı merkezi kimlik doğrulamasını ayarlamak](partner-center-authentication.md) için aşağıdaki bilgilere ihtiyacınız vardır.

| Öğe adı | Öğe konumu |
| --------- | ------------- |
| Uygulama KIMLIĞI/Istemci KIMLIĞI | **Ayarlar** menüsünde (dişli simgesi), **iş ortağı ayarları**' nı seçin. **Hesap ayarları** sayfasında, **uygulama yönetimi**' ni seçin. Uygulama KIMLIĞI/Istemci KIMLIĞI **kayıtlı uygulama uygulama kimliği** olarak listelenir. |
| Anahtar | [API erişimini etkinleştir](#enable-api-access)bölümünde bir Web uygulaması oluşturduysanız, bu, 5. adımda kaydettiğiniz anahtardır. |
| Etki alanı | Tümleştirme korumalı alanı için etki alanı. |

## <a name="run-tested-code"></a>Sınanan kodu Çalıştır

Çözümünüzü gerçek müşteri verileriyle birlikte kullanmak için, tümleştirme korumalı alanı kimlik bilgilerinizle birincil Iş ortağı hesabı kimlik bilgilerinizle değişiklik yapmanız gerekir.

Birincil Iş ortağı hesabınızda test ettiğiniz kodu kullanmaya hazırsanız, bir Azure AD güvenlik belirteci almalısınız. Bu güvenlik belirteci, Iş Ortağı Merkezi uygulamanızı, anahtarınızı ve etki alanınızı temel alır (Tümleştirme korumalı alanı uygulamanız, anahtar ve etki alanınız yerine).

1. Birincil Iş ortağı merkezi kimlik bilgilerinizi kullanarak bir Azure AD güvenlik belirteci almak için [Iş ortağı merkezi kimlik doğrulaması](partner-center-authentication.md) içindeki adımları izleyin. (Daha önce tümleştirme korumalı alanınız için bir Azure AD güvenlik belirteci almak üzere bu adımları izlediyseniz.)

2. Kodunuzda tümleştirme güvenlik belirtecini, birincil Iş ortağı hesabınızın yeni güvenlik belirteciyle değiştirin.
