---
title: Microsoft Ulusal bulut için Iş Ortağı Merkezi için uygulama ayrıntılarını kaydetme
description: Microsoft National Cloud için Iş Ortağı Merkezi 'nin uygulama geliştiricilerinin, Azure portal aracılığıyla Azure AD ile uygulamaları hakkındaki ayrıntıları nasıl ve neden kaydetmesi gerektiğini öğrenin.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770146"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a>Microsoft National Cloud için Iş Ortağı Merkezi 'nin Azure portal aracılığıyla uygulama ayrıntılarını kaydedin

**Uygulama hedefi:**

- Microsoft Bulut Almanya için İş Ortağı Merkezi
- Microsoft Cloud for US Government için İş Ortağı Merkezi

Geliştiricilerin, Azure portal aracılığıyla Azure AD ile uygulamaları hakkındaki ayrıntıları kaydetmesi gerekir. Bu, yalnızca belirtilen uygulamaların iş ortağı ve müşteri verilerine bağlanabildiğinden emin olmanıza yardımcı olur.

ABD hükümeti için Microsoft Bulut Iş Ortağı Merkezi için, şu anda uygulamaları PowerShell aracılığıyla yönetmeniz gerekir. Daha fazla bilgi için [Azure PowerShell başvuru belgelerine](/powershell/module/Azuread/#applications)bakın.

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

ABD hükümeti için Microsoft Bulut için Microsoft Bulut Almanya veya Iş Ortağı Merkezi için Iş Ortağı Merkezi için bir uygulama oluşturduğunuzda aşağıdaki ek gereksinimleri unutmayın.

## <a name="web-apps"></a>Web uygulamaları

Web Apps için, uygulama KIMLIĞINIZI kaydetmek üzere aşağıdaki yordamları kullanın.

### <a name="create-or-update-web-app"></a>Web uygulaması oluştur veya güncelleştir

1. Uygulamanızı kaydetmek için [Azure portal uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin. Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.

2. **Yeni kayıt** seçeneğini belirleyin. Daha fazla bilgi için bkz. [hızlı başlangıç: Microsoft Identity platformu ile uygulama kaydetme](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-web-app"></a>Web uygulaması için API erişim izinlerini yapılandırma

1. Uygulamanızı seçin. Web uygulamasının **Ayarlar** ' a gidin.

2. **API erişimi** bölümünde **gerekli izinleri** seçin

3. Windows Azure Active Directory izinleri için:

    1. **Windows Azure Active Directory izinleri**' ni seçin.

    2. **Uygulamalar izinler**' de, dizin verilerini oku ' nı seçin.

    3. İzinleri kaydedin.

4. Web uygulamanızın **Özellikler** BÖLÜMÜNDEKI uygulama kimliği ' ni aklınızda yapın.

### <a name="add-a-secret-key-to-your-app"></a>Uygulamanıza gizli anahtar ekleme

1. Web uygulamanızın **anahtarlar** bölümüne gidin.

2. Anahtar açıklaması girin ve gereken süreyi 1 veya 2 yıl olarak seçin.

3. Gizli anahtar değerini kaydedin ve kopyalayın. **Bu sayfadan ayrıldığınızda bu değer tekrar gösterilmeyecektir.**

Web uygulaması yapılandırmasından aşağıdaki ayrıntılara sahip olmanız gerekir:

- Uygulama Kimliği
- Uygulama gizli dizisi

### <a name="register-the-web-app-in-partner-center"></a>Web uygulamasını Iş Ortağı Merkezi 'ne kaydetme

1. ' Da oturum açın [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .

2. **Pano**' yı ve ardından **Hesap ayarları**' nı ve ardından **uygulama yönetimi**' ni seçin.

3. **Web uygulaması** bölümünde **var olan uygulamayı kaydet**' i seçin.

4. Azure portal içinde oluşturduğunuz Web uygulamasını seçin.

5. **Uygulamanızı kaydet**' i seçin.

## <a name="native-apps"></a>Yerel uygulamalar

Yerel uygulamaların Iş Ortağı Merkezi 'ne kayıtlı olması gerekmez. Ancak bu uygulamaların Iş Ortağı Merkezi API 'Lerine erişim sağlayacak şekilde yapılandırılması gerekir.

>[!NOTE]
>Azure portal yerel bir uygulama oluşturmadan önce, iş ortağı kiracısındaki Yönetici Kullanıcı kimlik bilgilerini kullanarak Iş Ortağı Merkezi ' nde oturum açın. Bu, uygulama izinlerini etkinleştirmek için Kiracıdaki ayarları oluşturur.

### <a name="create-native-app"></a>Yerel uygulama oluştur

1. Uygulamanızı kaydetmek için [Azure portal uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin. Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.

2. **Yeni kayıt** seçeneğini belirleyin. Daha fazla bilgi için bkz. [hızlı başlangıç: Microsoft Identity platformu ile uygulama kaydetme](/azure/active-directory/develop/quickstart-register-app).

### <a name="configure-api-access-permissions-for-native-app"></a>Yerel uygulama için API erişim izinlerini yapılandırma

1. Uygulamanızı seçin. **Ayarlar**' a gidin.

2. API erişimi ' nde **gerekli izinler**' i seçin.

3. **Windows Azure Active Directory izinleri**' ni seçin. **Temsilci izinleri**' nde şu izinleri seçin:

    - **Oturum açma ve kullanıcı profilini okuma**
    - **Dizin verilerini oku**
    - **Dizine oturum açmış kullanıcı olarak erişin**
    - **Tüm grupları oku**

4. İzinleri kaydedin.

5. **Gerekli Izinlere** **Ekle** ' yi seçin.

6. **API seçin** öğesini seçin.

    1. Arama kutusuna **Microsoft Iş Ortağı Merkezi** ' ni girin ve sonuçlar listesinden seçin.

    2. **Seç**’i seçin.

7. **Izinleri Seç ' i** seçin.

    1. **Erişim Iş Ortağı Merkezi PPE**'yi seçin.
    
    2. **Seç**’i seçin.

8. **Bitti**’yi seçin.

>[!IMPORTANT]
> Uygulamanızın özelliklerindeki uygulama KIMLIĞI ' ni aklınızda yapın.

Yerel uygulamaları Iş Ortağı Merkezi 'ne kaydetmeniz gerekmez, ancak yerel uygulamanın yönetici onaylı olması gerekir. Yerel uygulamanızın uygulama KIMLIĞI ' ni aklınızda edin.
