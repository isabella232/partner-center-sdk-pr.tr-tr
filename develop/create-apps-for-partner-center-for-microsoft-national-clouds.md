---
title: Microsoft Ulusal Bulut için İş Ortağı Merkezi ayrıntılarını kaydetme
description: Microsoft Ulusal Bulut için İş Ortağı Merkezi geliştiricilerin uygulamalarıyla ilgili ayrıntıları Azure AD'ye kaydetmeleri gerektiğini ve bu ayrıntıları nasıl Azure portal.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: bd9df37b83ced71c88da93ccaf52e7f3a970318a552c246997eb1334def9ff81
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115991523"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Azure portal aracılığıyla Microsoft Ulusal İş Ortağı Merkezi için uygulama ayrıntılarını Azure portal

**Için geçerlidir:** İş Ortağı Merkezi Microsoft Bulut Almanya | İş Ortağı Merkezi için Microsoft Cloud for US Government

Geliştiricilerin uygulamalarıyla ilgili ayrıntıları Azure AD'ye kaydetmek için Azure portal. Bu, yalnızca belirtilen uygulamaların iş ortağı ve müşteri verilerine bağlanamalarını sağlamaya yardımcı olur.

Uygulama İş Ortağı Merkezi için Microsoft Cloud for US Government şu anda Uygulamaları PowerShell aracılığıyla yönetmeniz gerekir. Daha fazla bilgi için [bkz. Azure PowerShell belgeleri.](/powershell/module/Azuread/#applications)

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Microsoft Bulut Almanya için veya Microsoft Bulut Almanya için İş Ortağı Merkezi bir uygulama gereksinimlerini İş Ortağı Merkezi dikkat Microsoft Cloud for US Government.

## <a name="web-apps"></a>Web uygulamaları

Web uygulamaları için, uygulama kimliğinizi kaydetmek için aşağıdaki yordamları kullanın.

### <a name="create-or-update-web-app"></a>Web uygulaması oluşturma veya güncelleştirme

1. Azure portal [- Uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin. Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.

2. Yeni **kayıt'ı seçin.** Daha fazla bilgi için [bkz. Hızlı Başlangıç: Uygulamayı](/azure/active-directory/develop/quickstart-register-app)Microsoft kimlik platformu.

### <a name="configure-api-access-permissions-for-web-app"></a>Web uygulaması için API erişim izinlerini yapılandırma

1. Uygulamanızı seçin. Web **Ayarlar'a** gidin.

2. **API Erişimi bölümünde** Gerekli izinler'i **seçin**

3. Daha Windows Azure Active Directory izinleri için:

    1. İzinleri **Windows Azure Active Directory seçin.**

    2. Uygulama **izinleri'nin** altında Dizin verilerini oku'ya tıklayın.

    3. İzinleri kaydedin.

4. Web uygulamanın Özellikler **bölümündeki uygulama** kimliğini not edin.

### <a name="add-a-secret-key-to-your-app"></a>Uygulamanıza gizli anahtar ekleme

1. Web **uygulamanın** Anahtarlar bölümüne gidin.

2. Anahtar açıklamasını girin ve ihtiyacınız olan süreyi 1 veya 2 yıl olarak seçin.

3. Gizli anahtar değerini kaydedin ve kopyalayın. **Bu sayfadan ayrılarak bu değer tekrar gösterilmez.**

Web uygulaması yapılandırmasında aşağıdaki ayrıntılara sahipsiniz:

- Uygulama Kimliği
- Uygulama gizli dizisi

### <a name="register-the-web-app-in-partner-center"></a>Web uygulamasını İş Ortağı Merkezi

1. [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) adresinde oturum açın.

2. **Pano'ya** ve ardından Hesap **Yönetimi'Ayarlar,** ardından Uygulama **Yönetimi'ne seçin.**

3. Web Uygulaması **bölümünde Mevcut** uygulamayı **kayded'i seçin.**

4. Web sitesinde oluşturduğunuz web uygulamasını Azure portal.

5. Uygulamanızı **kaydetme'yi seçin.**

## <a name="native-apps"></a>Yerel uygulamalar

Yerel uygulamaların yerel uygulamalara kayıtlı İş Ortağı Merkezi. Ancak bu uygulamaların api'lere erişim sağlamak için İş Ortağı Merkezi gerekir.

>[!NOTE]
>Yerel uygulama oluşturmadan önce Azure portal kiracıdan yönetici İş Ortağı Merkezi kimlik bilgilerini kullanarak oturum açın. Bu, uygulama izinlerini etkinleştirmek için kiracıda ayarları oluşturur.

### <a name="create-native-app"></a>Yerel uygulama oluşturma

1. Azure portal [- Uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin. Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.

2. Yeni **kayıt'ı seçin.** Daha fazla bilgi için [bkz. Hızlı Başlangıç: Uygulamayı](/azure/active-directory/develop/quickstart-register-app)Microsoft kimlik platformu.

### <a name="configure-api-access-permissions-for-native-app"></a>Yerel uygulama için API erişim izinlerini yapılandırma

1. Uygulamanızı seçin. Ayarlar. 

2. API Erişimi'ne Gerekli **izinler'i seçin.**

3. İzinleri **Windows Azure Active Directory seçin.** Temsilcili **izinler'de** şu izinleri seçin:

    - **Oturum açma ve kullanıcı profilini okuma**
    - **Dizin verilerini oku**
    - **Dizine oturum açmış kullanıcı olarak erişin**
    - **Tüm grupları okuma**

4. İzinleri kaydedin.

5. Gerekli **izinler'de** **Ekle'yi seçin.**

6. **API seçin** öğesini seçin.

    1. Arama kutusuna **Microsoft** İş Ortağı Merkezi yazın ve sonuçlar listesinden seçin.

    2. **Seç**’i seçin.

7. İzin **seç'i seçin.**

    1. **PPE'İş Ortağı Merkezi Erişim'i seçin.**
    
    2. **Seç**’i seçin.

8. **Bitti**’yi seçin.

>[!IMPORTANT]
> Uygulamanın Özellikler'deki uygulama kimliğini not edin.

Yerel uygulamaları yerel uygulamalara kaydetmeniz İş Ortağı Merkezi, ancak yerel uygulamanın yönetici onayına sahip olması gerekir. Yerel uygulamanın uygulama kimliğini not edin.
