---
title: İş Ortağı Merkezi’nde API erişimini ayarlama
description: Sanal İş Ortağı Merkezi SDK'sı için geliştirme hesapları ayarlayın ve tümleştirme korumalı alanı içinde test olun.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2c564baa9b626ff6ce21f9bcc517902d7cf99244
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547436"
---
# <a name="set-up-api-access-in-partner-center"></a>İş Ortağı Merkezi’nde API erişimini ayarlama

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government | İş Ortağı Merkezi Microsoft Bulut Almanya için destek

Bu makalede, bu hesaplara karşı geliştirmesi gereken hesaplar İş Ortağı Merkezi SDK'sı. Bu makalede tümleştirme korumalı alanı hesabı oluşturma [ve tümleştirme korumalı alanda](#integration-sandbox-account) test oluşturma da açıklanmıştır.

>[!NOTE]
>API'lere erişim elde etmek için kiracınız CSP kiracısı olmalı ve dolaylı sağlayıcı veya Doğrudan fatura iş ortağınız olması gerekir.

## <a name="account-definitions"></a>Hesap tanımları

API tümleştirmenizi tümleştirmenize ve test etmeye yardımcı olmak İş Ortağı Merkezi iki tür hesabı destekler:

### <a name="primary-partner-account"></a>Birincil İş Ortağı hesabı

Bu hesap, gerçek müşteriler için gerçek siparişler oluşturabilirsiniz. Birincil hesapta oturum asanız, İş Ortağı Merkezi SDK'sı veya İş Ortağı Panosu kullanıcı arabirimini kullanarak herhangi bir değişiklik veya işlem yaptısanız, bunlar gerçek müşteriler için resmi siparişler olarak kabul edilir. Bunlar faturanıza yansır ve bunlar için ödeme sizin şirketiniz tarafından sorumludur.

### <a name="integration-sandbox-account"></a>Tümleştirme korumalı alanı hesabı

Bu hesap, genel olarak dağıtmadan önce kodunuzu ve İş Ortağı Merkezi api'leriyle tümleştirmesini test etmek için. Tümleştirme korumalı alanı hesabında oturum asanız yaptığınız değişiklikler ve işlemler faturada görünür, ancak fatura tutarını ödemeniz gerek değildir. Fatura pdf dosyası şu şekilde bir sorumluluk reddine sahip olur: "ÖDEMEYİN. BU BIR KORUMALı ALAN FATURASıDıR VE HERHANGI BIR IŞLEM GEREKMEZ."

Tümleştirme korumalı alanı hesabı ve birincil hesap birbirinden bağımsız olarak hareket eder ve yönetici hesaplarını, kullanıcı hesaplarını, müşterileri, siparişleri, abonelikleri veya diğer verileri paylaşmaz.

Tümleştirme korumalı alanı sınırlı sayıda müşteri, sipariş, abonelik, lisans vb. ile işlemleri destekler.

İlkeyle, tümleştirme korumalı alanı hesapları yalnızca tümleştirme testi amaçlarına yöneliktir.

Varsayılan olarak tümleştirme korumalı alan hesabı yoktur. Bu hesabı kullanmayı planlıyorsanız kendiniz bir tane İş Ortağı Merkezi SDK'sı.

## <a name="set-up-your-accounts"></a>Hesaplarınızı ayarlama

Bu bölümde, iş ortağı hesabı için birincil İş Ortağı hesabının ve tümleştirme korumalı alanı hesabının nasıl ayar İş Ortağı Merkezi SDK'sı.

### <a name="create-an-integration-sandbox"></a>Tümleştirme korumalı alanı oluşturma

1. Genel yönetici hesabıyla (birincil İş ortağı hesabınız) İş Ortağı Panosu'nda oturum açın.

2. İş ortağı **Ayarlar** (dişli simgesi) İş ortağı **ayarları'ı seçin.**

3. Tümleştirme **korumalı alanı sekmesini** seçin.

    >[!NOTE]
    >Tümleştirme korumalı alanı seçeneğini görmüyorsanız genel yönetici hesabınız yok olabilir. Ayrıca bir tümleştirme korumalı alanı hesabı kullanıyor ve tümleştirme korumalı alanı zaten ayarlanmış olabilir.

4. Tümleştirme korumalı alan yönetici hesabının iletişim bilgilerini girin. Ardından Hesap **oluştur'a seçin.** Hesabın oluşturularak ilgili onay iletisi için birkaç dakika bekleyin.

5. Onay mesajını gördüğünüzde İş Ortağı Panosu'nın oturumlarını açın.

6. Yeni tümleştirme korumalı alan yönetici hesabınızla yeniden oturum açın. Kimlik bilgileriniz için biçimi **username@domain** ve belirttiğiniz parolayı kullanmayı mutlaka kullanın.

7. Korumalı **alan hesabı kurulumunu tamamlamak** için Geçerli **Görevler'in** üzerinde Hesabı Ayarla'ya seçin.

### <a name="enable-api-access"></a>API erişimini etkinleştirme

Hesabınız ayarlandıktan sonra, İş Ortağı Merkezi SDK'sını tümleştirme korumalı alanıyla kullanabilmek için öncelikle API erişimini etkinleştirmeniz gerekir. Hem birincil İş Ortağı hesabınız hem de tümleştirme korumalı alanı hesabınız için API erişimini ayrı ayrı etkinleştirmelisiniz.

1. Genel yönetici hesabı kullanarak İş Ortağı Panosunda oturum açın.

2. İş ortağı **Ayarlar** (dişli simgesi) İş ortağı **ayarları'ı seçin.**

3. Hesap ayarları **sayfasında Uygulama** yönetimi'ne **tıklayın.**

4. Henüz bir uygulamanız yoksa yeni bir web uygulaması ekleyin. Mevcut bir web uygulamanız varsa Anahtar ekle **düğmesini** seçin.

5. Uygulama kayıt bilgilerini, özellikle  de bir web uygulaması oluşturuyorsanız Anahtar'a kopyalayın ve güvenli bir yerde depolar.

6. İş Ortağı Panosu'da oturum açın.

7. Tümleştirme korumalı alanı hesabınızla yeniden oturum açın. Tümleştirme korumalı alanda API erişimini etkinleştirmek için 2-5. adımları tekrarlayın.

## <a name="write-and-test-code"></a>Kod yazma ve test

Tümleştirme korumalı alanı içinde kod yazabilir ve kodu testebilirsiniz. Azure AD ile kimlik doğrulamasını ayarlamak [için İş Ortağı Merkezi](partner-center-authentication.md) bilgilere ihtiyacınız vardır.

| Öğe adı | Öğe konumu |
| --------- | ------------- |
| Uygulama Kimliği / İstemci Kimliği | İş ortağı **Ayarlar** (dişli simgesi) İş ortağı **ayarları'ı seçin.** Hesap ayarları **sayfasında Uygulama** Yönetimi'ne **tıklayın.** Uygulama Kimliği/İstemci Kimliği, Kayıtlı uygulama Uygulama **Kimliği olarak listelenir.** |
| Anahtar | API erişimini etkinleştirme bölümünde bir web uygulaması [oluşturduysanız,](#enable-api-access)bu, 5. adımda kaydedilen anahtardır. |
| Etki alanı | Tümleştirme korumalı alanının etki alanı. |

## <a name="run-tested-code"></a>Test edilen kodu çalıştırma

Çözümlerinizi gerçek müşteri verileriyle kullanmak için tümleştirme korumalı alan kimlik bilgilerinizle birincil İş Ortağı hesabı kimlik bilgilerinize değişmeniz gerekir.

Test edilen kodunuzu birincil İş Ortağı hesabında kullanmaya hazırsanız bir Azure AD güvenlik belirteci alasınız. Bu güvenlik belirteci, İş Ortağı Merkezi, anahtar ve etki alanınıza (tümleştirme korumalı alan uygulamanız, anahtarınız ve etki alanınız yerine) dayalıdır.

1. Birincil kimlik bilgilerinizi [İş Ortağı Merkezi Azure](partner-center-authentication.md) AD güvenlik belirteci almak için kimlik doğrulaması İş Ortağı Merkezi izleyin. (Tümleştirme korumalı alanınız için Azure AD güvenlik belirteci almak üzere daha önce bu adımları izlediniz.)

2. Kodundaki tümleştirme güvenlik belirteci yerine birincil İş Ortağı hesabınız için yeni güvenlik belirteci girin.
