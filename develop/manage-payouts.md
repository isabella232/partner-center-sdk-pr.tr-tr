---
title: Ödeme Hizmeti API'sini kullanarak ödemeleri yönetme
description: Ödeme verilerine erişmek İş Ortağı Merkezi Ödeme Hizmeti API'sini kullanmayı öğrenin
ms.date: 06/23/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: jasongroce
ms.author: sabaja
ms.openlocfilehash: b9bdc6da64a79f4f35466fb62662b086a8e1ab3cadc99c7ca685303752f9d166
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115996410"
---
# <a name="manage-payouts-using-the-payout-service-api"></a>Ödeme Hizmeti API'sini kullanarak ödemeleri yönetme

Bu makalede, kullanıcı arabirimi yerine Ödeme Hizmeti API'leri aracılığıyla ödeme verilerine nasıl İş Ortağı Merkezi açıklanmıştır. Bu API'ler, veri dışarı aktarma özelliğinin veri dışarı aktarma özelliğini İş Ortağı Merkezi. [](https://partner.microsoft.com/dashboard/payouts/reports/incentiveexport)

## <a name="available-apis"></a>Kullanılabilir API’ler

İş Ortağı Ödemeleri'nde tüm [kullanılabilir API'lere bakın.](/rest/api/partner-center/partner-payouts)

## <a name="prerequisites"></a>Önkoşullar

- [Uygulamayı AAD/Microsoft Identity](/graph/auth-register-app-v2) ile Azure portal ve uygulamaya uygun sahipler ve roller ekleyin.
- yükleme [Visual Studio.](https://visualstudio.microsoft.com/downloads/)

## <a name="register-an-application-with-the-microsoft-identity-platform"></a>Microsoft kimlik platformuna uygulama kaydetme

Bu [Microsoft kimlik platformu,](/azure/active-directory/develop/v2-overview) kullanıcı ve müşterinizin Microsoft kimliklerini veya sosyal hesaplarını kullanarak oturum açmasını sağlayan ve kendi API'leriniz veya Microsoft Graph gibi Microsoft API'leriniz için yetkili erişim sağlayan uygulamalar derlemenize yardımcı Graph.

1. Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak [Azure portalında](https://portal.azure.com/) oturum açın.

   Hesabınız birden fazla kiracıya erişim veriyorsa, sağ üst köşeden hesap seçin ve portal oturumlarınızı doğru Azure AD kiracısına ayarlayın.

2. Sol gezinti bölmesinde, Azure Active Directory hizmetini seçin ve **Uygulama kayıtları** yeni kayıt **seçeneğini kullanın.** Uygulama **kaydetme** sayfası görüntülenir.

   :::image type="content" source="./images/manage-payouts/new-app-registration.png" alt-text="Uygulama kaydetme ekranındaki Uygulama kaydetmeyi gösteren ekran Azure portal.":::

3. Uygulama kayıt bilgilerini girin:

   - Ad: Uygulama kullanıcılarına görüntülenecek anlamlı bir uygulama adı girin.
   - Desteklenen hesap türleri: Uygulamanıza hangi hesapların destekley olduğunu seçin.

    | **Desteklenen hesap türleri**                             | **Açıklama**                                                                                            |
    |---------------------------------------------------------|------------------------------------------------------------------------------------------------------------|
    | Yalnızca bu kuruluş dizininde yer alan hesaplar          | Bir iş kolu uygulaması (LOB) oluşturuyorsanız bu seçeneği belirtin. Uygulamayı bir dizine kaydetmiyorsanız bu seçenek kullanılamaz. Bu seçenek, yalnızca Azure AD tek kiracılı hesaba eşlenir.  Uygulamayı bir dizinin dışında kaydetmedikçe bu seçenek varsayılan seçenektir. Uygulamanın bir dizin dışında kaydedildiği durumlarda, varsayılan seçenek Azure çok kiracılı ve kişisel Microsoft kişisel hesaplarıdır.             |
    | Herhangi bir kuruluş dizinindeki hesaplar                | Tüm iş ve eğitim müşterilerini hedeflemek istiyorsanız bu seçeneği belirleyin.  Bu seçenek, bir yalnızca Azure AD çok kiracılı hesaba eşlenir. Uygulamayı yalnızca Azure AD tek kiracılı olarak kaydettiyseniz, Kimlik doğrulaması dikey penceresinden Azure AD çok kiracılı olacak şekilde ve tekrar tek kiracılı olarak güncelleştirebilirsiniz.                                                                                                                                                  |
    | Herhangi bir kuruluş dizinindeki hesaplar ve kişisel Microsoft hesapları | En geniş müşteri kümesini hedeflemek için bu seçeneği belirleyin. Bu seçenek Azure AD çok kiracılı ve kişisel Microsoft hesaplarına eşlenir.  Uygulamayı Azure AD çok kiracılı ve kişisel Microsoft hesapları olarak kaydettiyebilirsiniz, kullanıcı arabiriminde bu seçimi değiştiremezsiniz. Bunun yerine, desteklenen hesap türlerini değiştirmek için uygulama bildirimi düzenleyicisini kullanmanız gerekir.                                                                          |

   - *(isteğe bağlı)* Yeniden yönlendirme URI'si: Web veya Genel istemci (mobil & masaüstü) olarak, kendi uygulama türlerinizi seçin ve ardından uygulamanıza yönelik yeniden yönlendirme URI'sini (veya yanıt URL'sini) girin. (Yeniden yönlendirme URL'si, kullanıcı kimlik doğrulamasının ardından kimlik doğrulama yanıtının gönderilmesidir.) 

      Web uygulamaları için, uygulamanızın temel URL'sini girin. Örneğin `http://localhost:31544` yerel makinenizde çalışan bir web uygulamasının URL'si olabilir. Kullanıcılar, bir web istemci uygulamasında oturum açmak için bu URL'yi kullanır.
      Genel istemci uygulamaları için, Azure AD'nin belirteç yanıtlarını döndürmek üzere kullandığı URI'yi girin. Uygulamanıza özgü bir değer girin, örn. `myapp://auth`.

4. **Kaydet**’i seçin. Azure AD, uygulamanıza benzersiz bir uygulama (istemci) kimliği atar ve uygulamanın genel bakış sayfası yüklenir.

   :::image type="content" source="./images/manage-payouts/register-an-application.png" alt-text="<alternatif metin>":::

5. Uygulamanıza özellikler eklemek için markalama, sertifikalar ve gizli diziler, API izinleri ve daha fazlası gibi diğer yapılandırma seçeneklerini kullanabilirsiniz.

## <a name="platform-specific-properties"></a>Platforma özgü özellikler

Aşağıdaki tabloda, farklı türlerde uygulamalar için yapılandırmanız ve kopyalamanız gereken özellikler yer alır. **Atanan,** Azure AD tarafından atanan değeri kullanmanız gerektiği anlamına gelir.

| Uygulama türü              | Platform | Uygulama (istemci) kimliği | İstemci Gizli Anahtarı | Yeniden yönlendirme URI'si/URL'si | Örtülü Flow                                                         |
|-----------------------|----------|-------------------------|---------------|------------------|-----------------------------------------------------------------------|
| Yerel/Mobil         | Yerel   | Atanmış                | No            | Atanmış         | No                                                                    |
| Web App               | Web      | Atanmış                | Yes           | Yes              | İsteğe bağlı Açık Bağlan ara yazılımı varsayılan olarak karma akışı kullanır (Evet) |
| Tek Sayfalı Uygulama (SPA) | Web      | Atanmış                | Yes           | Yes              | Evet, SPA'lar açık kimlik Bağlan açık kimlik Flow                            |
| Hizmet/Daemon        | Web      | Atanmış                | Yes           | Yes              | Hayır                                                                    |

## <a name="create-a-service-principal"></a>Hizmet sorumlusu oluşturma

Aboneliğiniz içinde kaynaklara erişmek için uygulamaya bir rol atamanız gerekir. Hangi rolün uygulama için doğru izinleri sunduğuna karar verme konusunda yardım için [bkz. Azure yerleşik rolleri.](/azure/role-based-access-control/built-in-roles)

> [!NOTE]
> Kapsamı abonelik, kaynak grubu veya kaynak düzeyinde ayarlayabilirsiniz. İzinler daha düşük kapsam düzeylerine devralınmış olur. Örneğin, bir kaynak grubu için Okuyucu rolüne uygulama eklemek, kaynak grubunu ve içerdiği tüm kaynakları okuyabiliyor demektir.

1. Uygulama Azure portal, uygulamayı atamak için kapsam düzeyini seçin. Örneğin, abonelik kapsamında bir rol atamak için Abonelikler'i bulun ve **seçin** veya giriş sayfasında **Abonelikler'i** seçin.

   :::image type="content" source="./images/manage-payouts/search-for-subscriptions.png" alt-text="Abonelikler ekran aramanızı gösteren ekran görüntüsü.":::

2. Uygulamayı atamak istediğiniz aboneliği seçin.

   :::image type="content" source="./images/manage-payouts/internal-testing-subscription.png" alt-text="İç Test bayrağının true olarak ayarlandı olduğu Abonelikler ekran görüntüsü.":::

> [!NOTE]
> İstediğiniz aboneliği görmüyorsanız genel abonelikler filtresini seçin ve portal için istediğiniz aboneliğin seçildiğinden emin olun.

3. Erişim **denetimi (IAM) öğesini** ve ardından Rol ataması **ekle'yi seçin.**

4. Uygulamaya atamak istediğiniz rolü seçin. Örneğin, uygulamanın örnekleri yeniden başlatma, başlatma ve durdurma gibi eylemleri yürütmesine izin vermek için Katkıda Bulunan rolünü seçin. Kullanılabilir roller hakkında daha [fazla bilgi okuyun.](/azure/role-based-access-control/built-in-roles)

   Varsayılan olarak, Azure AD uygulamaları kullanılabilir seçeneklerde görüntülenmez. Uygulamanızı bulmak için ad üzerinde arama ve sonuçlardan uygulamayı seçin. Aşağıdaki ekran `example-app` görüntüsünde, kayıtlı AAD uygulamasıdır.

   :::image type="content" source="./images/manage-payouts/add-role-assignment.png" alt-text="Test uygulaması için rol ataması eklemek için kullanıcı arabirimini gösteren ekran görüntüsü.":::

5. **Kaydet**’i seçin. Daha sonra, bu kapsam için bir role sahip kullanıcılar listesinden uygulamanıza bakabilirsiniz.

   Betiklerinizi veya uygulamalarınızı çalıştırmak için hizmet sorumlularınızı kullanmaya başlayabilirsiniz. Hizmet sorumlunuza ilişkin izinleri yönetmek için bkz. kullanıcı onayı durumu, izinleri gözden geçirme, oturum açma bilgileri ve daha fazlası), Enterprise [uygulamalarınızı](https://portal.azure.com)Azure portal.

## <a name="set-up-api-permissions"></a>API izinlerini ayarlama

Bu bölümde, gerekli API izinlerini ayarlama hakkında yönerge verilmiştir. API izinlerini ayarlama hakkında daha İş Ortağı Merkezi için bkz. [Partner API doğrulaması.](/partner/develop/api-authentication)

**Api'ye Graph izni ver**

1. Dosyanın [Uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) açın Azure portal.

2. Bir uygulama seçin [veya henüz yoksa](/azure/active-directory/develop/quickstart-register-app) bir uygulama oluşturun.

3. Uygulamanın Genel Bakış sayfasının Yönet altında API **İzinleri'ne** **ve** ardından İzin **ekle'ye tıklayın.**

4. Kullanılabilir **API'Graph Listesinden Microsoft** Graph'yi seçin.

5. Temsilcili **izinler'i seçin** ve gerekli izinleri ekleyin. Daha fazla bilgi için [bkz. Uygulama erişimini yapılandırma.](/azure/active-directory/develop/quickstart-configure-app-access-web-apis)

   :::image type="content" source="./images/manage-payouts/graph-request-api-permissions.png" alt-text="Microsoft Azure portal'nin seçili olduğu Graph ekran görüntüsü.":::

**AAD uygulaması aracılığıyla API'İş Ortağı Merkezi API'ye erişim izni**

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
