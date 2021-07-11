---
title: Ödeme hizmeti API 'sini kullanarak ödemeleri yönetme
description: Iş Ortağı Merkezi ödeme hizmeti API 'sini, ödeme verilerine erişmek için nasıl kullanacağınızı öğrenin
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: jasongroce
ms.author: sabaja
ms.openlocfilehash: 014a1e6a14b538b7557d58710b9132dd9e37de21
ms.sourcegitcommit: 7e2d2805c4cdd61785b1cdcca99cad10d5683153
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/10/2021
ms.locfileid: "113592484"
---
# <a name="manage-payouts-using-the-payout-service-api"></a>Ödeme hizmeti API 'sini kullanarak ödemeleri yönetme

Bu makalede, Iş Ortağı Merkezi kullanıcı arabirimi yerine, ödeme verilerine ödeme hizmeti API 'Leri aracılığıyla nasıl erişebileceğiniz açıklanır. Bu API 'Ler, Iş Ortağı Merkezi 'nde [veri dışarı aktarma](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport) özelliğinin yeteneğini sağlamak için programlı bir yol sağlar.

## <a name="available-apis"></a>Kullanılabilir API’ler

[Ortak ödemeler](/rest/api/partner-center/partner-payouts)sırasında kullanılabilir tüm API 'leri görüntüleyin.

## <a name="prerequisites"></a>Önkoşullar

- Azure portal [AAD/Microsoft kimliği ile bir uygulamayı kaydedin](/graph/auth-register-app-v2) ve uygulamaya uygun sahipleri ve rolleri ekleyin.
- [Visual Studio](https://visualstudio.microsoft.com/downloads/)'i yükler.

## <a name="register-an-application-with-the-microsoft-identity-platform"></a>Microsoft kimlik platformuna uygulama kaydetme

[Microsoft kimlik platformu](/azure/active-directory/develop/v2-overview) , kullanıcılarınızın ve müşterilerinizin Microsoft kimliklerini veya sosyal hesaplarını kullanarak oturum açmasını ve kendi apı 'lerinize veya Microsoft Graph gibi microsoft apı 'lerine yetkili erişim sağlamasına yardımcı olur.

1. Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak [Azure portalında](https://portal.azure.com/) oturum açın.

   Hesabınız birden fazla kiracıya erişim veriyorsa, sağ üst köşedeki hesabınızı seçin ve Portal oturumunuzu doğru Azure AD kiracısına ayarlayın.

2. sol gezinti bölmesinde Azure Active Directory hizmeti, sonra **Uygulama kayıtları** ve ardından **yeni kayıt**' ı seçin. **Uygulama kaydetme** sayfası görüntülenir.

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Azure portal uygulama kaydetme ekranını gösteren ekran görüntüsü.":::

3. Uygulamanızın kayıt bilgilerini girin:

   - Ad: uygulamanın kullanıcılarına gösterilecek anlamlı bir uygulama adı girin.
   - Desteklenen hesap türleri: uygulamanızın destekleyeceği hesapları seçin.

    | **Desteklenen hesap türleri**                             | **Açıklama**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Yalnızca bu kuruluş dizinindeki hesaplar          | Bir iş kolu uygulaması (LOB) oluşturuyorsanız bu seçeneği belirtin. Uygulamayı bir dizine kaydetmiyorsanız bu seçenek kullanılamaz. Bu seçenek, yalnızca Azure AD tek kiracılı hesaba eşlenir.  Uygulamayı bir dizinin dışına kaydetmiyorsanız Bu seçenek varsayılandır. Uygulamanın bir dizin dışında kaydedildiği durumlarda, varsayılan seçenek Azure çok kiracılı ve kişisel Microsoft kişisel hesaplarıdır.             |
    | Herhangi bir kuruluş dizinindeki hesaplar                | Tüm iş ve eğitim müşterilerini hedeflemek istiyorsanız bu seçeneği belirleyin.  Bu seçenek, bir yalnızca Azure AD çok kiracılı hesaba eşlenir. Uygulamayı yalnızca Azure AD tek kiracılı olarak kaydettiyseniz, Kimlik doğrulaması dikey penceresinden Azure AD çok kiracılı olacak şekilde ve tekrar tek kiracılı olarak güncelleştirebilirsiniz.                                                                                                                                                  |
    | Herhangi bir kuruluş dizinindeki hesaplar ve kişisel Microsoft hesapları | En geniş müşteri kümesini hedeflemek için bu seçeneği belirleyin. Bu seçenek Azure AD çok kiracılı ve kişisel Microsoft hesaplarına eşlenir.  Uygulamayı Azure AD çok kiracılı ve kişisel Microsoft hesapları olarak kaydettiniz, bu seçimi Kullanıcı arabiriminde değiştiremezsiniz. Bunun yerine, desteklenen hesap türlerini değiştirmek için uygulama bildirimi düzenleyicisini kullanmanız gerekir.                                                                          |

   - *(isteğe bağlı)* Yeniden yönlendirme URI 'SI: oluşturmakta olduğunuz uygulamanın türünü, Web veya ortak istemciyi (mobil & Masaüstü) seçin ve ardından uygulamanızın yeniden yönlendirme URI 'sini (veya yanıt URL 'SI) girin. (Yeniden yönlendirme URL 'SI, kimlik doğrulama yanıtının Kullanıcı kimliğini doğruladıktan sonra gönderileceği yerdir.) 

      Web uygulamaları için, uygulamanızın temel URL'sini girin. Örneğin `http://localhost:31544` yerel makinenizde çalışan bir web uygulamasının URL'si olabilir. Kullanıcılar, bir web istemci uygulamasında oturum açmak için bu URL'yi kullanır.
      Genel istemci uygulamaları için, Azure AD'nin belirteç yanıtlarını döndürmek üzere kullandığı URI'yi girin. Uygulamanıza özgü bir değer girin, örn. `myapp://auth`.

4. **Kaydet**’i seçin. Azure AD uygulamanıza benzersiz bir uygulama (istemci) KIMLIĞI atar ve uygulamanın genel bakış sayfası yüklenir.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<alt metin>":::

5. Uygulamanıza özellik eklemek istiyorsanız, marka, sertifikalar ve gizlilikler, API izinleri ve daha fazlasını içeren diğer yapılandırma seçeneklerini belirleyebilirsiniz.

## <a name="platform-specific-properties"></a>Platforma özgü özellikler

Aşağıdaki tabloda, farklı türlerde uygulamalar için yapılandırmanız ve kopyalamanız gereken özellikler gösterilmektedir. **Atanmış** , Azure AD tarafından atanan değeri kullanmanız gerektiği anlamına gelir.

| Uygulama türü              | Platform | Uygulama (istemci) kimliği | İstemci Gizli Anahtarı | Yeniden yönlendirme URI 'si/URL 'SI | Örtük Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Yerel/mobil         | Yerel   | Atanmış                | No            | Atanmış         | No                                                                    |
| Web App               | Web      | Atanmış                | Yes           | Yes              | isteğe bağlı açık kimlik Bağlan ara yazılım varsayılan olarak karma akışı kullanır (evet) |
| Tek sayfalı uygulama (SPA) | Web      | Atanmış                | Yes           | Yes              | evet maça açık kimlik Bağlan örtülü Flow kullanın                            |
| Hizmet/Daemon        | Web      | Atanmış                | Yes           | Yes              | Hayır                                                                    |

## <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma

Aboneliğinizdeki kaynaklara erişmek için uygulamaya bir rol atamanız gerekir. Uygulama için doğru izinleri hangi rolün sunduğunu belirleyen yardım için bkz. [Azure yerleşik rolleri](/azure/role-based-access-control/built-in-roles).

> [!NOTE]
> Kapsamı, abonelik, kaynak grubu veya kaynak düzeyinde ayarlayabilirsiniz. İzinler, daha düşük kapsam düzeylerine devralınır. Örneğin, bir kaynak grubu için okuyucu rolüne bir uygulama eklemek, kaynak grubunu ve içerdiği kaynakları okuyabileceği anlamına gelir.

1. Azure portal, uygulamanın atanacağı kapsam düzeyini seçin. Örneğin, abonelik kapsamında bir rol atamak için, **abonelikleri** arayıp seçin ya da giriş sayfasında **abonelikler** ' i seçin.

   :::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Abonelikler ekran aramasını gösteren ekran görüntüsü.":::

2. Uygulamanın atanacağı aboneliği seçin.

   :::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="Iç test bayrağı true olarak ayarlanan abonelikler ekranını gösteren ekran görüntüsü.":::

> [!NOTE]
> Aradığınız aboneliği görmüyorsanız, genel abonelikler filtresini seçin ve Portal için istediğiniz aboneliğin seçildiğinden emin olun.

3. **Erişim denetimi (IAM)** öğesini seçin ve ardından **rol ataması Ekle**' yi seçin.

4. Uygulamaya atamak istediğiniz rolü seçin. Örneğin, uygulamanın yeniden başlatma gibi eylemleri yürütmesine izin vermek için örnekleri başlatın ve durdurun, katkıda bulunan rolünü seçin. [Kullanılabilir roller](/azure/role-based-access-control/built-in-roles)hakkında daha fazla bilgi edinin.

   Varsayılan olarak, Azure AD uygulamaları kullanılabilir seçeneklerde gösterilmez. Uygulamanızı bulmak için ad üzerinde arama yapın ve sonuçlardan seçim yapın. Aşağıdaki ekran görüntüsünde, `example-app` KAYDETTIĞINIZ AAD uygulaması.

   :::image type="content" source="./images/manage-payouts/add-role-assignment.png" alt-text="Test uygulaması için rol ataması eklemek için kullanıcı arabirimini gösteren ekran görüntüsü.":::

5. **Kaydet**’i seçin. Daha sonra, bu kapsam için bir role sahip kullanıcılar listesinden uygulamalarınızı görebilir.

   Betiklerinizi veya uygulamalarınızı çalıştırmak için hizmet sorumlularınızı kullanmaya başlayabilirsiniz. Hizmet sorumlunuza ilişkin izinleri yönetmek için bkz. kullanıcı onayı durumu, izinleri gözden geçirme, oturum açma bilgileri ve daha fazlası), Enterprise [uygulamalarınızı](https://portal.azure.com)Azure portal.

## <a name="set-up-api-permissions"></a>API izinlerini ayarlama

Bu bölümde, gerekli API izinlerini ayarlama hakkında yönerge verilmiştir. API izinlerini ayarlama hakkında daha İş Ortağı Merkezi için bkz. [Partner API doğrulaması.](/partner/develop/api-authentication)

**Api'ye Graph izni ver**

1. Dosyanın [Uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) açın Azure portal.

2. Bir uygulama seçin [veya henüz yoksa](/azure/active-directory/develop/quickstart-register-app) bir uygulama oluşturun.

3. Uygulamanın Genel Bakış sayfasının Yönet altında API **İzinleri'ne** **ve** ardından İzin **ekle'ye tıklayın.**

4. Kullanılabilir **API Graph Microsoft** Graph'yi seçin.

5. Temsilcili **izinler'i seçin** ve gerekli izinleri ekleyin. Daha fazla bilgi için [bkz. Uygulama erişimini yapılandırma.](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)

   :::image type="content" source="./images/manage-payouts/graph-request-api-permissions.png" alt-text="Microsoft Azure portal'nin seçili olduğu Graph ekran görüntüsü.":::

**AAD uygulaması aracılığıyla API'İş Ortağı Merkezi API erişimine onay**

6. Uygulamanız için **API izinleri'ne** tıklayın, ardından API izinleri isteği ekranından İzin ekle'yi ve ardından kuruluşum tarafından kullanan **API'ler'i seçin.**

7. Microsoft İş **Ortağı (Microsoft Geliştirme Merkezi) API'si (4990cffe-04e8-4e8b-808a-1175604b879f)** araması.

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="Microsoft İş Ortağı'nın seçili olduğu API izinleri ekran görüntüsü.":::

8. Temsilci İzinleri'ne **İş Ortağı Merkezi.**

   :::image type="content" source="./images/manage-payouts/partner-api-request-permissions.png" alt-text="API izinleri isteği ekranındaKimlik için İş Ortağı Merkezi İzinler'i gösteren ekran görüntüsü.":::

9. **API'ler** için Yönetici onayı ver.

   :::image type="content" source="./images/manage-payouts/api-permissions.png" alt-text="API izinleri ekranında Yönetici Onayı iki durumlu düğmeyi gösteren ekran görüntüsü.":::

   Yönetici onayı durum ekranında Yönetici onayı'nın etkinleştirildiğinden emin olun.

   :::image type="content" source="./images/manage-payouts/admin-consent-verification.png" alt-text="Yönetici onayı durum ekranı gösteren ekran görüntüsü":::

10. Kimlik Doğrulaması **bölümünde** Genel istemci akışlarına izin **ver seçeneğinin Evet** olarak ayarlanmış olduğundan emin **olun.**

    :::image type="content" source="./images/manage-payouts/allow-public-client-flows.png" alt-text="Genel istemci akışlarına izin ver'in Evet olarak ayar olduğu Kimlik doğrulaması ekranı gösteren ekran görüntüsü.":::

## <a name="run-the-sample-code-in-visual-studio"></a>Örnek kodu Visual Studio

API'nin ödeme ve işlem geçmişi için nasıl kullanılana bir örnek kod, İş Ortağı [Merkezi-Ödeme](https://github.com/microsoft/Partner-Center-Payout-APIs) API'leri GitHub bulunabilir.

### <a name="sample-code-notes"></a>Örnek kod notları

- İstemci gizli dizilerinin ve Sertifikaların Kimlik Doğrulaması: Hizmet sorumlusu oluşturma bölümündeki İki seçenekli bölümünde [Azure portal](/azure/active-directory/develop/howto-create-service-principal-portal) yapılandırma gerekli değildir.
- Çok faktörlü kimlik doğrulaması (MFA) olan hesaplar şu anda desteklenmiyor ve hataya neden olacak.
- Ödeme API'si yalnızca kullanıcı/parola tabanlı kimlik bilgilerini destekler.

## <a name="next-steps"></a>Sonraki adımlar

- [Kaynaklara erişen bir Azure AD uygulaması ve hizmet sorumlusu oluşturmak için portalı kullanma](/azure/active-directory/develop/howto-create-service-principal-portal)
- [Microsoft kimlik platformuna uygulama kaydetme](/graph/auth-register-app-v2)
- [Web API'lerine erişmek için istemci uygulaması yapılandırma](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)
