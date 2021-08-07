---
title: Sanal alanda CSP dolaylı sağlayıcı özellikleri
description: Dolaylı sağlayıcılar, test amaçları için korumalı alanda dolaylı satıcılar oluşturabilir.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: 07608fb5f2d2a3ffc418188e0ac1ff367e3c5691aa241554a4a954de8c4f2005
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115990683"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Dolaylı satıcı hesapları oluşturmak için CSP dolaylı sağlayıcısı korumalı alanı özellikleri 

**Uygun roller**: dolaylı sağlayıcı

CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı Bayi Sandbox hesabı oluşturabilir.


## <a name="prerequisites"></a>Önkoşullar 

Partner Center dolaylı sağlayıcısı (katman 2) korumalı alan kimlik bilgileri. Sandbox senaryosu hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Korumalı alan dolaylı sağlayıcısı – Iş Ortağı Merkezi Kullanıcı arabirimini kullanarak korumalı alan dolaylı satıcısı oluşturma 

 Bu, korumalı alan dolaylı sağlayıcılarına, Iş Ortağı Merkezi portalı aracılığıyla korumalı alan dolaylı satıcı hesabı oluşturma yeteneği sağlayan, yalnızca korumalı bir özelliktir.

Aşağıdaki senaryolar, Iş Ortağı Merkezi kullanıcı arabirimi aracılığıyla korumalı satıcıların dolaylı satıcılarına yönelik olarak ne yapabilecekleri, dolaylı sağlayıcılardır: 

1. CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı Bayi Sandbox hesabı oluşturabilir.
2. CSP dolaylı satıcıları, müşteriyi dolaylı sağlayıcılara göre görüntüleyebilir. 

1. CSP dolaylı satıcıları, yönetici temsilcisi izinlerini kullanarak müşteri hesabını yönetebilir.

1. CSP dolaylı sağlayıcıları, CSP dolaylı satıcılarını davet edebilir.
 
1. CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı satıcı Sandbox hesabını silebilir.

    a.  Korumalı alan dolaylı sağlayıcısı, korumalı alan dolaylı satıcısı ile ilişkiyi sildiğinde, dolaylı satıcının diğer sağlayıcılarla başka bir ilişkiye sahip olup olmadığını kontrol edin. Bu durumda, yalnızca söz konusu dolaylı sağlayıcıyla ilişki kaldırılır.

    c. Bu, dolaylı satıcı için tek ilişkisidir ve dolaylı satıcı silinir.

1. CSP dolaylı sağlayıcıları, bir CSP dolaylı satıcısı silebilir.

    a. Bu, korumalı alan dolaylı sağlayıcılarının korumalı alan dolaylı satıcılarını silmesine izin veren yalnızca korumalı bir özelliktir.
     
1. Korumalı alan dolaylı satıcılarını silmenin önkoşulları:

    1. Korumalı alan dolaylı satıcısının her bir müşterisi için abonelikleri askıya alın.

    1. Dolaylı satıcıdan oluşan tüm müşterileri silin.

1. Korumalı alan dolaylı sağlayıcısı başına beş korumalı alan dolaylı satıcıya izin verilen sınır. Korumalı alan dolaylı satıcısı silindikten sonra kota sıfırlanır.

### <a name="pre-requisites"></a>Ön koşullar

- Korumalı alan dolaylı sağlayıcısı başına beş korumalı alan dolaylı satıcıya izin verilen sınır. 

- MPN KIMLIK ülkesi ve dolaylı satıcı Sandbox ülkesi aynıysa, aynı MPN KIMLIĞI birden çok dolaylı satıcı Sandbox hesabı oluşturmak için kullanılabilir. kullanılabilir bir test mpn kimliğiniz varsa, bunu kullanabilir veya [Yammer kanalımızda]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 )mpn kimliklerinin bir listesini alabilirsiniz. Yammer erişiminiz yoksa, Yammer sizden erişim isteğinde bulunan bir sorun olacaktır.
 
- Sandbox dolaylı sağlayıcısı başına yalnızca 75 müşteriye izin verilir

## <a name="create-csp-indirect-reseller-sandbox-account"></a>CSP dolaylı Bayi Sandbox hesabı oluştur

1. Katman 2 Sandbox hesabınız aracılığıyla Iş Ortağı Merkezi ' nde oturum açın. 

2. Sol menüden dolaylı satıcılara gidin. 

3. **Satıcı korumalı alanı Ekle** düğmesini seçin. 

4. Hesap kayıt formunu girin. Kendi kendine açıklayıcı bir, ancak dolaylı bir satıcı için bir sandbox hesabı oluşturuyoruz. Bu hesap devre dışı bırakılır ve hesap kaydını tamamlayandan sonra etkinleştirilecektir.  

5. Hesap oluşturulduktan sonra, portalda dolaylı satıcı Sandbox hesabı için genel yönetici kimlik bilgilerini alırsınız. Bunu hemen kaydetmeyi unutmayın, aksi takdirde dolaylı satıcı korumalı alanı olarak oturum açamazsınız. 

6. Oturumu kapatın ve dolaylı satıcı korumalı alanının yeni kimlik bilgilerini kullanarak Iş Ortağı Merkezi 'nde yeniden oturum açın. Dolaylı bir satıcı olarak yapabileceğiniz özellikleri keşfedebilirsiniz. Bazı şeyler:  

    - Profilleri yönetme  

    - Kullanıcıları ve rolleri yönetme 

    - Dolaylı sağlayıcıları yönetme 

    - CSP korumalı alan müşterilerini yönetme 

    - İlişkileri yönetme
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Korumalı alan dolaylı sağlayıcısı – Iş Ortağı Merkezi Kullanıcı arabirimini kullanarak korumalı alan dolaylı satıcısı silme

 Bu, korumalı alan dolaylı sağlayıcılarının, Iş Ortağı Merkezi portalı aracılığıyla mevcut bir korumalı alan dolaylı satıcı hesabını silmesine izin veren yalnızca korumalı bir özelliktir. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>Korumalı alan dolaylı satıcılarını silmenin önkoşulları:

Kendi CSP dolaylı sağlayıcısı katman 2 Sandbox hesabınızla ilişkili mevcut CSP dolaylı satıcı korumalı alan hesabı.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>CSP dolaylı Bayi Sandbox hesabını Sil

1. Katman 2 Sandbox hesabınızı kullanarak Iş Ortağı Merkezi ' nde oturum açın. 

2. Sol menüden dolaylı satıcılara gidin. 

3. Silmek istediğiniz dolaylı satıcı korumalı alan hesabının yanındaki **satıcı korumalı alanını sil** bağlantısını seçin. Dolaylı satıcı korumalı alan hesabı kalıcı olarak silinir ve kurtarılamaz. 

## <a name="api-references"></a>API başvuruları

- Dolaylı satıcı oluştur 
- Dolaylı Bayi Sil 

 

 