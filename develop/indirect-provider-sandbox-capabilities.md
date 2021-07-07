---
title: Korumalı Alanda CSP Dolaylı sağlayıcı özellikleri
description: Dolaylı sağlayıcılar, test amacıyla Korumalı Alanda dolaylı kurumsal bayiler oluşturabilir.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445910"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a>Dolaylı kurumsal bayi hesapları oluşturmak için CSP Dolaylı sağlayıcı korumalı alan özellikleri 

**Uygun roller:** Dolaylı sağlayıcı

CSP Indirect Providers, CSP Indirect Reseller portalında kendi Katman 2 Korumalı Alan hesabı aracılığıyla İş Ortağı Merkezi oluşturabilir.


## <a name="prerequisites"></a>Önkoşullar 

İş Ortağı Merkezi Dolaylı Sağlayıcı (Katman 2) korumalı alan kimlik bilgileri. Korumalı alan senaryosu hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler. 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Korumalı Alan Dolaylı Sağlayıcısı – Sanal ağ kullanıcı arabirimini kullanarak İş Ortağı Merkezi Dolaylı Kurumsal Bayi oluşturma 

 Bu, Korumalı Alan Dolaylı Sağlayıcılarının İş Ortağı Merkezi portal aracılığıyla Korumalı Alan Dolaylı Kurumsal Bayi hesabı oluşturmasını sağlayan yalnızca korumalı İş Ortağı Merkezi özelliktir.

Aşağıdaki senaryolar, Dolaylı sağlayıcıların Korumalı Alan'daki dolaylı kurumsal bayiler için İş Ortağı Merkezi arabirimidir: 

1. CSP Indirect Providers, CSP Indirect Reseller portalında kendi Katman 2 Korumalı Alan hesabı aracılığıyla İş Ortağı Merkezi oluşturabilir.
2. CSP Indirect Resellers, Dolaylı Sağlayıcılar tarafından müşteriyi görüntülemeyi sağlar. 

1. CSP Indirect Resellers, temsilcili yönetici izinlerini kullanarak müşteri hesabını yönetebilir.

1. CSP Dolaylı Sağlayıcıları CSP Dolaylı Kurumsal Bayileri davet ediyor olabilir.
 
1. CSP Dolaylı Sağlayıcıları, CSP Indirect Reseller portalında kendi Katman 2 Korumalı Alan hesabı aracılığıyla İş Ortağı Merkezi silebilir.

    a.  Korumalı Alan Dolaylı Sağlayıcısı Korumalı Alan Dolaylı Kurumsal Bayi ile ilişkiyi silse de Dolaylı Kurumsal Bayinin diğer sağlayıcılarla başka bir ilişkisi olup ola bir ilişkisi olup değildir. Öyleyse, yalnızca ilgili Dolaylı sağlayıcıyla ilişki kaldırılır.

    c. Dolaylı Kurumsal Bayi için tek ilişki bu ise Dolaylı Kurumsal Bayi silinir.

1. CSP Dolaylı Sağlayıcıları bir hesabı CSP Indirect Reseller.

    a. Bu, Korumalı Alan Dolaylı Sağlayıcılarının Korumalı Alan Dolaylı Kurumsal Bayilerini silmesini sağlayan yalnızca korumalı alan özelliğidir.
     
1. Korumalı Alan Dolaylı Kurumsal Bayiyi silmek için önkullar:

    1. Korumalı Alan Dolaylı Kurumsal Bayi'nin her müşterisi için abonelikleri askıya alın.

    1. Dolaylı Kurumsal Bayi'nin tüm müşterilerini silin.

1. Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen beş Korumalı Alan Dolaylı Kurumsal Bayi sınırı. Korumalı Alan Dolaylı kurumsal bayisi silindikten sonra kota sıfırlanır.

### <a name="pre-requisites"></a>Ön koşullar

- Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen beş Korumalı Alan Dolaylı Kurumsal Bayi sınırı. 

- MPN ID ülke ve Dolaylı Kurumsal Bayi Korumalı Alanı ülke aynı ise birden çok Dolaylı Kurumsal Bayi Korumalı Alanı hesabı oluşturmak için aynı MPN Kimliği kullanılabilir. Kullanılabilir bir test MPN Kimliğiniz varsa, bunu kullanabilir veya mpN kimliklerinin listesini Yammer [kanalımız aracılığıyla eldeebilirsiniz.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ) Erişim iznine sahip değil Yammer Yammer erişim istemeniz gerekir.
 
- Korumalı Alan Dolaylı Sağlayıcısı başına yalnızca 75 müşteriye izin verilir

## <a name="create-csp-indirect-reseller-sandbox-account"></a>Korumalı CSP Indirect Reseller hesabı oluşturma

1. Katman 2 İş Ortağı Merkezi hesabı aracılığıyla oturum açın. 

2. Sol menüden Dolaylı Kurumsal Bayiler'e gidin. 

3. Kurumsal Bayi **Korumalı Alanı Ekle düğmesini** seçin. 

4. Hesap kayıt formunu doldurun. Bu kendi kendine açık bir ifadedir ancak Dolaylı Kurumsal Bayi için korumalı alan hesabı oluşturmakta olduğunu unutmayın. Bu hesap için bir yok etme işlemi olmayacaktır ve siz hesap kaydı tamamlana kadar hemen etkinleştirilir.  

5. Hesap oluşturulduktan sonra portalda Dolaylı Kurumsal Bayi korumalı alan hesabı için Genel Yönetici kimlik bilgilerini alırsınız. Hemen kaydetmeyi unutmayın; aksi takdirde Dolaylı Kurumsal Bayi Korumalı Alanı olarak oturum açamayacaksınız. 

6. Dolaylı Kurumsal Bayi Korumalı Alanı'nın İş Ortağı Merkezi kimlik bilgilerini kullanarak oturum açma ve yeniden oturum açma. Dolaylı Kurumsal Bayi olarak sahip olduğunuz özellikleri keşfedin. Bazı şeyler:  

    - Profilleri yönetme  

    - Kullanıcıları ve rolleri yönetme 

    - Dolaylı Sağlayıcıları Yönetme 

    - CSP Korumalı Alan müşterilerini yönetme 

    - İlişkileri yönetme
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a>Sandbox Indirect Provider – İş Ortağı Merkezi kullanıcı arabirimini kullanarak Sandbox Indirect Reseller'ı silin

 Bu yalnızca Korumalı Alan özelliğidir ve Korumalı Alan Dolaylı Sağlayıcılarının mevcut Korumalı Alan Dolaylı Kurumsal Bayi hesabını portal üzerinden İş Ortağı Merkezi sağlar. 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a>Korumalı alan Dolaylı kurumsal bayiyi silmek için önkullar:

Kendi CSP Indirect Reseller Katman 2 Korumalı Alan hesabınızla CSP Indirect Provider bir korumalı alan hesabı.  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a>Korumalı CSP Indirect Reseller hesabını silme

1. Katman 2 İş Ortağı Merkezi kullanarak oturum açın. 

2. Sol menüden Dolaylı Kurumsal Bayiler'e gidin. 

3. Silmek **istediğiniz Dolaylı Kurumsal Bayi** Korumalı Alanı hesabının yanındaki Kurumsal Bayi Korumalı Alanı Sil bağlantısını seçin. Dolaylı Kurumsal Bayi Korumalı Alanı hesabı kalıcı olarak silinir ve kurtarılamaz. 

## <a name="api-references"></a>API başvuruları

- Dolaylı Kurumsal Bayi oluşturma 
- Dolaylı Kurumsal Bayiyi silme 

 

 