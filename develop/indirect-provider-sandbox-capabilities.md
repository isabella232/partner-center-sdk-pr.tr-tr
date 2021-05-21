---
title: Sanal alanda CSP dolaylı sağlayıcı özellikleri
description: Dolaylı sağlayıcılar, test amaçları için korumalı alanda dolaylı satıcılar oluşturabilir.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244610"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Dolaylı satıcı hesapları oluşturmak için CSP dolaylı sağlayıcısı korumalı alanı özellikleri 

**Şunlara uygulanır**

- İş Ortağı Merkezi

**Uygun roller**

- Dolaylı sağlayıcı

CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı Bayi Sandbox hesabı oluşturabilir.


## <a name="prerequisites"></a>Önkoşullar 

Partner Center dolaylı sağlayıcısı (katman 2) korumalı alan kimlik bilgileri. Sandbox senaryosu hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Korumalı alan dolaylı sağlayıcısı – Iş Ortağı Merkezi Kullanıcı arabirimini kullanarak korumalı alan dolaylı satıcısı oluşturma 

 Bu, korumalı alan dolaylı sağlayıcılarına, Iş Ortağı Merkezi portalından korumalı alan dolaylı satıcı hesabı oluşturma yeteneği sağlayan yalnızca korumalı bir özelliktir.

Aşağıdaki senaryolar, Iş Ortağı Merkezi kullanıcı arabirimi aracılığıyla korumalı satıcıların dolaylı satıcılarına yönelik olarak ne yapabilecekleri, dolaylı sağlayıcılardır: 

1. CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı Bayi Sandbox hesabı oluşturabilir.
2. CSP dolaylı satıcıları, müşteriyi dolaylı sağlayıcılara göre görüntüleyebilir. 

1. CSP dolaylı satıcıları, yönetici temsilcisi izinlerini kullanarak müşteri hesabını yönetebilir.

1. CSP dolaylı sağlayıcıları, CSP dolaylı satıcılarını davet edebilir.
 
1. CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı satıcı Sandbox hesabını silebilir.

    a.  Korumalı alan dolaylı sağlayıcısı, korumalı alan dolaylı satıcılarından ilişkiyi siler.

    b.  Dolaylı satıcının diğer sağlayıcılarla başka bir ilişkiye sahip olup olmadığını denetleyin. Bu durumda, yalnızca söz konusu dolaylı sağlayıcıyla ilişki kaldırılır.

    c. Bu, IR için tek ilişkisidir, IR silinir.

1. CSP Indirect Provider bir dosyayı CSP Indirect Reseller.

    a. Bu, Korumalı Alan Dolaylı Sağlayıcılarının Korumalı Alan Dolaylı Kurumsal Bayilerini silmesini sağlayan yalnızca korumalı alan özelliğidir.
     
1. Korumalı Alan Dolaylı Kurumsal Bayiyi silmek için önkullar:

    1. Korumalı Alan Dolaylı Kurumsal Bayi'nin her müşterisi için abonelikleri askıya alın.

    1. Dolaylı Kurumsal Bayi'nin tüm müşterilerini silin.

1. Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen 5 Korumalı Alan Dolaylı Kurumsal Bayi sınırı. Korumalı Alan Dolaylı kurumsal bayisi silindikten sonra kota sıfırlanır.

### <a name="pre-requisites"></a>Ön koşullar

- Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen 5 Korumalı Alan Dolaylı Kurumsal Bayi sınırı. 

- MPN ID ülke ve Dolaylı Kurumsal Bayi Korumalı Alanı ülke aynı ise birden çok Dolaylı Kurumsal Bayi Korumalı Alanı hesabı oluşturmak için aynı MPN Kimliği kullanılabilir. Kullanılabilir bir test MPN Kimliğiniz varsa, bunu kullanabilir veya Yammer kanalımız üzerinden MPN kimliklerinin bir [listesini eldeabilirsiniz.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ) Yammer'a erişiminiz yoksa Yammer sizden erişim istemeyi sorar.
 
- Korumalı Alan Dolaylı Sağlayıcısı başına yalnızca 75 müşteriye izin verilir

## <a name="create-csp-indirect-reseller-sandbox-account"></a>Korumalı CSP Indirect Reseller hesabı oluşturma

1. Katman 2 İş Ortağı Merkezi hesabı aracılığıyla oturum açın. 

2. Sol menüden Dolaylı Kurumsal Bayiler'e gidin. 

3. "Kurumsal Bayi Korumalı Alanı Ekle" düğmesine tıklayın. 

4. Hesap kayıt formunu doldurun. Bu kendi kendine açık bir ifadedir ancak Dolaylı Kurumsal Bayi için korumalı alan hesabı oluşturmakta olduğunu unutmayın. Bu hesap için bir yok etme işlemi olmayacaktır ve siz hesap kaydı tamamlana kadar hemen etkinleştirilir.  

5. Hesap oluşturulduktan sonra portalda Dolaylı Kurumsal Bayi korumalı alan hesabı için Genel Yönetici kimlik bilgilerini alırsınız. Bunu hemen kaydetmeyi unutmayın, aksi takdirde dolaylı satıcı korumalı alanı olarak oturum açamazsınız. 

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

3. Silmek istediğiniz dolaylı satıcı korumalı alan hesabının yanındaki **satıcı korumalı** alanı bağlantısını Sil ' e tıklayın. Dolaylı satıcı korumalı alan hesabı kalıcı olarak silinir ve kurtarılamaz. 

## <a name="api-references"></a>API başvuruları

- Dolaylı satıcı oluştur 
- Dolaylı Bayi Sil 

 

 