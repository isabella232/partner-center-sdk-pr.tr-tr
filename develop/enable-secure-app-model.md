---
title: Güvenli uygulama modelini etkinleştirme
description: Iş ortağı merkezi ve Denetim Masası uygulamalarınızın güvenliğini sağlayın.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 3e153e1e7d4e38580d8cb39a3996e56365ff5fbe
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769304"
---
# <a name="enabling-the-secure-application-model-framework"></a>Güvenlik Uygulama Modeli çerçevesini etkinleştirme

**Uygulama hedefi:**

- İş Ortağı Merkezi

Microsoft, Microsoft Azure Multi-Factor Authentication (MFA) mimarisi aracılığıyla bulut çözümü sağlayıcısı (CSP) iş ortaklarının ve Denetim Masası satıcılarının (CPV) kimlik doğrulaması için güvenli ve ölçeklenebilir bir çerçeve sunuyor.

Iş Ortağı Merkezi API Tümleştirmesi çağrıları için güvenliği yükseltmek üzere yeni modeli kullanabilirsiniz. Bu, tüm taraflara (Microsoft, CSP iş ortakları ve CPVs 'ler dahil), altyapı ve müşteri verilerini güvenlik risklerinden korumalarına yardımcı olur.

## <a name="scope"></a>Kapsam

Bu makalede aşağıdaki aktörlerin kaygıları vardır:

- CPV’ler
  - CPV, CSP iş ortakları tarafından İş Ortağı Merkezi API’leriyle tümleştirilmek üzere kullanılacak uygulamalar geliştiren bağımsız yazılım satıcısıdır.
  - CPV, İş Ortağı Merkezi panosuna veya API’lerine doğrudan erişimi olan bir CSP iş ortağı değildir.

- CSP dolaylı sağlayıcıları ve uygulama KIMLIĞI + Kullanıcı kimlik doğrulaması kullanan CSP Direct iş ortakları ve doğrudan Iş Ortağı Merkezi API 'Leri ile tümleştirin.

## <a name="security-requirements"></a>Güvenlik gereksinimleri

Güvenlik gereksinimleriyle ilgili ayrıntılar için bkz. [Iş ortağı güvenlik gereksinimleri](/partner-center/partner-security-requirements).

## <a name="secure-application-model"></a>Güvenli uygulama modeli

Market uygulamalarının Microsoft API 'Leri çağırmak için CSP iş ortağı ayrıcalıklarının kimliğine bürünmesi gerekir. Bu hassas uygulamalardaki güvenlik saldırıları müşteri verilerinin tehlikeye çıkmasına neden olabilir.

Yeni kimlik doğrulama çerçevesiyle ilgili genel bilgiler ve Ayrıntılar için [güvenli uygulama modeli çerçevesi](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) belgesini indirin. Bu belgede, Market uygulamalarının güvenliği tehlikeye atmayı ve güçlü hale getirmek için ilkeler ve en iyi uygulamalar ele alınmaktadır.

## <a name="samples"></a>Örnekler

Aşağıdaki genel bakış belgeleri ve örnek kod, iş ortaklarının güvenli uygulama modeli çerçevesini nasıl uygulayabileceğini açıklamaktadır:

- [CPV genel bakış belgesi](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [CSP genel bakış belgesi](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET örnekleri](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java örnekleri](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [REST yönergeleri ve örnekleri](#rest)
- [PowerShell yönergeleri ve örnekleri](#powershell)

## <a name="rest"></a>REST

Örnek kodla güvenli uygulama modeli çerçevesiyle REST çağrıları yapmak için şu adımları izleyin:

1. [Web uygulaması oluşturma](#create-a-web-app)

2. [Yetkilendirme kodu al](#get-authorization-code)

3. [Yenileme belirteci al](#get-refresh-token)

4. [Bir erişim belirteci alma](#get-access-token)

5. [İş Ortağı Merkezi API çağrısı yapma](#make-partner-center-api-calls)

> [!TIP]
> Bir yetkilendirme kodu ve yenileme belirteci almak için Iş Ortağı Merkezi PowerShell modülünü kullanabilirsiniz. Adım 2 ve 3 ' ün yerine bu seçeneği belirleyebilirsiniz. Daha fazla bilgi için [PowerShell bölümüne ve örneklerine](#powershell)bakın.

### <a name="create-a-web-app"></a>Web uygulaması oluşturma

REST çağrıları yapmadan önce Iş Ortağı Merkezi 'nde bir Web uygulaması oluşturmanız ve kaydetmeniz gerekir.

1. [Azure portalında](https://portal.azure.com) oturum açın.

2. Azure Active Directory (Azure AD) uygulaması oluşturun.

3. *Uygulamanızın gereksinimlerine bağlı olarak* aşağıdaki kaynaklara atanmış uygulama izinleri verin. Gerekirse, uygulama kaynakları için daha fazla temsilci izinleri ekleyebilirsiniz.

   1. **Microsoft Iş Ortağı Merkezi** (Bazı kiracılar bunu **samplebecapp** olarak gösterir)

   2. **Azure Yönetim API 'leri** (Azure API 'lerini çağırmayı planlıyorsanız)

   3. **Windows Azure Active Directory**

4. Uygulamanızın giriş URL 'sinin canlı bir Web uygulamasının çalıştığı bir uç noktaya ayarlandığından emin olun. Bu uygulamanın Azure AD oturum açma çağrısından [Yetkilendirme kodunu](#get-authorization-code) kabul etmesi gerekir. Örneğin, [aşağıdaki bölümdeki](#get-authorization-code)örnek kodda, Web uygulaması ' de çalışır `https://localhost:44395/` .

5. Web uygulamanızın Azure AD 'deki ayarlarından aşağıdaki bilgilere göz atalım:

   - Uygulama Kimliği
   - Uygulama gizli dizisi

> [!NOTE]
> [Uygulama gizli anahtarı olarak bir sertifika kullanmanız](/azure/active-directory/develop/active-directory-certificate-credentials)önerilir. Ancak, Azure portal bir uygulama anahtarı da oluşturabilirsiniz. [Aşağıdaki bölümdeki](#get-authorization-code) örnek kod bir uygulama anahtarı kullanır.

### <a name="get-authorization-code"></a>Yetkilendirme kodunu alma

Web uygulamanızın Azure AD oturum açma çağrısından kabul etmesi için bir yetkilendirme kodu almanız gerekir:

1. Şu URL 'de Azure AD 'de oturum açın: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Iş Ortağı Merkezi API çağrılarını (bir Yönetim Aracısı veya satış aracısı hesabı gibi) yapacağınız kullanıcı hesabıyla oturum açmanız gerekir.

2. **Uygulama kimliğini** Azure AD uygulama KIMLIĞINIZ (GUID) ile değiştirin.

3. İstendiğinde, MFA yapılandırılmış kullanıcı hesabınızla oturum açın.

4. İstendiğinde, oturum açma bilgilerinizi doğrulamak için ek MFA bilgilerini (telefon numarası veya e-posta adresi) girin.

5. Oturum açtıktan sonra tarayıcı, yetkilendirme kodunuzla Web uygulaması uç noktanıza yapılan çağrıyı yeniden yönlendirir. Örneğin, aşağıdaki örnek kod öğesine yeniden yönlendirir `https://localhost:44395/` .

#### <a name="authorization-code-call-trace"></a>Yetkilendirme kodu çağrısı izleme

```http
POST https://localhost:44395/ HTTP/1.1
Origin: https://login.microsoftonline.com
Upgrade-Insecure-Requests: 1
Content-Type: application/x-www-form-urlencoded
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8
Referrer: https://login.microsoftonline.com/kmsi
Accept-Encoding: gzip, deflate, br
Accept-Language: en-US,en;q=0.9
Cookie: OpenIdConnect.nonce.hOMjjrivcxzuI4YqAw4uYC%2F%2BILFk4%2FCx3kHTHP3lBvA%3D=dHVyRXdlbk9WVUZFdlFONVdiY01nNEpUc0JRR0RiYWFLTHhQYlRGNl9VeXJqNjdLTGV3cFpIWFg1YmpnWVdQUURtN0dvMkdHS2kzTm02NGdQS09veVNEbTZJMDk1TVVNYkczYmstQmlKUzFQaTBFMEdhNVJGVHlES2d3WGlCSlVlN1c2UE9sd2kzckNrVGN2RFNULWdHY2JET3RDQUxSaXRfLXZQdG00RnlUM0E1TUo1YWNKOWxvQXRwSkhRYklQbmZUV3d3eHVfNEpMUUthMFlQUFgzS01RS2NvMXYtbnV4UVJOYkl4TTN0cw%3D%3D

code=AuthorizationCodeValue&id_token=IdTokenValue&<rest of properties for state>
```

### <a name="get-refresh-token"></a>Yenileme belirtecini al

Daha sonra bir yenileme belirteci almak için yetkilendirme kodunuzu kullanmanız gerekir:

1. Azure AD oturum açma uç noktasına yetkilendirme kodu ile bir POST çağrısı yapın `https://login.microsoftonline.com/CSPTenantID/oauth2/token` . Bir örnek için, aşağıdaki [örnek çağrıya](#sample-refresh-call)bakın.

2. Döndürülen yenileme belirtecini unutmayın.

3. Yenileme belirtecini Azure Key Vault olarak depolayın. Daha fazla bilgi için [Key Vault API belgelerine](/rest/api/keyvault/)bakın.

> [!IMPORTANT]
> Yenileme belirteci Key Vault’ta [gizli dizi olarak depolanmalıdır](/rest/api/keyvault/setsecret/setsecret).

#### <a name="sample-refresh-call"></a>Örnek yenileme çağrısı

Yer tutucu isteği:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

İstek gövdesi:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

Yer tutucu yanıtı:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Yanıt gövdesi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a>Erişim belirteci al

Iş Ortağı Merkezi API 'Lerine çağrı yapmadan önce bir erişim belirteci almalısınız. Erişim belirtecinin genellikle çok sınırlı bir yaşam süresi (örneğin, bir saatten kısa) olması nedeniyle, bir erişim belirteci almak için bir yenileme belirteci kullanmanız gerekir.

Yer tutucu isteği:

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

İstek gövdesi:

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

Yer tutucu yanıtı:

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

Yanıt gövdesi:

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a>Iş Ortağı Merkezi API çağrıları yapma

Iş Ortağı Merkezi API 'Lerini çağırmak için erişim belirtecinizi kullanmanız gerekir. Aşağıdaki örnek çağrıya bakın.

#### <a name="example-partner-center-api-call"></a>Örnek Iş Ortağı Merkezi API çağrısı

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

[Iş Ortağı Merkezi PowerShell modülünü](https://www.powershellgallery.com/packages/PartnerCenter) , bir erişim belirteci için bir yetkilendirme kodu alışverişi yapmak üzere gerekli altyapıyı azaltmak için kullanabilirsiniz. Bu yöntem, [Iş ortağı MERKEZI Rest çağrıları](#rest)yapmak için isteğe bağlıdır.

Bu işlem hakkında daha fazla bilgi için bkz. [App model PowerShell Için güvenli uygulama](/powershell/partnercenter/secure-app-model) .

1. Azure AD ve Iş Ortağı Merkezi PowerShell modüllerini yükler.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Onay işlemini gerçekleştirmek ve gerekli yenileme belirtecini yakalamak için **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** komutunu kullanın.

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > **Web/API** türünde BIR Azure AD uygulaması kullanıldığından, **ServicePrincipal** parametresi **New-partneraccesstoken** komutuyla birlikte kullanılır. Bu tür bir uygulama, erişim belirteci isteğine bir istemci tanımlayıcısı ve gizli anahtar eklenmesini gerektirir. **Get-Credential** komutu çağrıldığında, bir Kullanıcı adı ve parola girmeniz istenir. Uygulama tanımlayıcısını Kullanıcı adı olarak girin. Parola olarak uygulama gizli anahtarını girin. **New-PartnerAccessToken** komutu çağrıldığında, kimlik bilgilerini yeniden girmeniz istenir. Kullanmakta olduğunuz hizmet hesabının kimlik bilgilerini girin. Bu hizmet hesabı, uygun izinlere sahip bir iş ortağı hesabı olmalıdır.

3. Yenileme belirteci değerini kopyalayın.

    ```powershell
    $token.RefreshToken | clip
    ```

Yenileme belirteci değerini, Azure Key Vault gibi güvenli bir depoda depolamanız gerekir. PowerShell ile güvenli uygulama modülünü kullanma hakkında daha fazla bilgi için bkz. [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) makalesi.
