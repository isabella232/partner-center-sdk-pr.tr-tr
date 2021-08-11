---
title: Güvenli uygulama modelini etkinleştirme
description: Uygulamalarınızı İş Ortağı Merkezi denetim masası uygulamalarının güvenliğini sağlama.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 9974237f7d4234b782a5b17a65fd52b9024315f848b721c73f4e1d59b69b2930
ms.sourcegitcommit: 63ef5995314ef22f29768132dff2acf45914ea84
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/06/2021
ms.locfileid: "115994804"
---
# <a name="enabling-the-secure-application-model-framework"></a>Güvenlik Uygulama Modeli çerçevesini etkinleştirme

Microsoft, Microsoft Azure Active Directory Multi-Factor Authentication (MFA) mimarisi aracılığıyla bulut çözümü sağlayıcısı (CSP) iş ortaklarının ve denetim masası satıcılarının (CPV) kimliklerini doğrulamaya Microsoft Azure Active Directory güvenli ve ölçeklenebilir bir çerçeve sunmaktadır.

Yeni modeli kullanarak API tümleştirme çağrılarına İş Ortağı Merkezi yükseltebilirsiniz. Bu, tüm tarafların (Microsoft, CSP iş ortakları ve CPV'ler dahil) altyapılarını ve müşteri verilerini güvenlik risklerinden korumalarına yardımcı olur.

## <a name="scope"></a>Kapsam

Bu makale aşağıdaki aktörlerle ilgilidir:

- CPV’ler
  - CPV, CSP iş ortakları tarafından İş Ortağı Merkezi API’leriyle tümleştirilmek üzere kullanılacak uygulamalar geliştiren bağımsız yazılım satıcısıdır.
  - CPV, İş Ortağı Merkezi panosuna veya API’lerine doğrudan erişimi olan bir CSP iş ortağı değildir.

- Uygulama kimliği + kullanıcı kimlik doğrulaması kullanan ve doğrudan uygulama API'leriyle tümleştiren CSP dolaylı sağlayıcıları ve CSP İş Ortağı Merkezi iş ortakları.

## <a name="security-requirements"></a>Güvenlik gereksinimleri

Güvenlik gereksinimleri hakkında ayrıntılı bilgi için bkz. [İş Ortağı Güvenlik Gereksinimleri.](/partner-center/partner-security-requirements)

## <a name="secure-application-model"></a>Güvenli Uygulama Modeli

Market uygulamalarının Microsoft API'lerini çağıran CSP iş ortağı ayrıcalıklarının kimliğine bürünmeleri gerekir. Bu hassas uygulamalara yönelik güvenlik saldırıları müşteri verilerini tehlikeye atarak yol açabilirsiniz.

Yeni kimlik doğrulama çerçevesine genel bakış ve ayrıntılar için Güvenli Uygulama Modeli [belgesini](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) indirin. Bu belge, market uygulamalarını güvenlik tehlikeye atlarına karşı sürdürülebilir ve sağlam hale etmek için ilkeler ve en iyi yöntemleri kapsar.

## <a name="samples"></a>Örnekler

Aşağıdaki genel bakış belgeleri ve örnek kod, iş ortaklarının Güvenli Uygulama Modeli açıklar:

- [CPV genel bakış belgesi](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [CSP'ye genel bakış belgesi](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [.NET Örnekleri](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [Java Örnekleri](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [REST yönergeleri ve örnekleri](#rest)
- [PowerShell yönergeleri ve örnekleri](#powershell)

## <a name="rest"></a>REST

Güvenli Uygulama Modeli çerçevesini örnek kodla rest çağrısı yapmak için şu adımları izleyin:

1. [Web uygulaması oluşturma](#create-a-web-app)

2. [Yetkilendirme kodu al](#get-authorization-code)

3. [Yenileme belirteci alın](#get-refresh-token)

4. [Bir erişim belirteci alma](#get-access-token)

5. [İş Ortağı Merkezi API çağrısı yapma](#make-partner-center-api-calls)

> [!TIP]
> Yetkilendirme kodu ve İş Ortağı Merkezi almak için PowerShell modülünü kullanabilirsiniz. 2. ve 3. adımlar yerine bu seçeneği seçebilirsiniz. Daha fazla bilgi için [PowerShell bölümüne ve örneklerine bakın.](#powershell)

### <a name="create-a-web-app"></a>Web uygulaması oluşturma

REST çağrıları yapmadan önce bir web uygulamasını İş Ortağı Merkezi web uygulaması oluşturmanız ve kaydetmeniz gerekir.

1. [Azure Portal](https://portal.azure.com)’ında oturum açın.

2. Bir Azure Active Directory (Azure AD) uygulaması oluşturun.

3. Uygulama gereksinimlerine bağlı olarak aşağıdaki *kaynaklara temsilcili uygulama izinleri verin.* Gerekirse, uygulama kaynakları için daha fazla temsilcili izin ebilirsiniz.

   1. **Microsoft İş Ortağı Merkezi** (bazı kiracılar bunu **SampleBECApp olarak gösterir)**

   2. **Azure Yönetim API'leri** (Azure API'lerini çağırmayı planlıyorsanız)

   3. **Windows Azure Active Directory**

4. Uygulamanın giriş URL'sinin canlı bir web uygulamasının çalıştır bulunduğu uç nokta olarak ayarlanmış olduğundan emin olun. Bu uygulamanın Azure AD oturum [açma çağrısından](#get-authorization-code) yetkilendirme kodunu kabul etmesi gerekir. Örneğin, aşağıdaki bölümdeki örnek [kodda](#get-authorization-code)web uygulaması üzerinde `https://localhost:44395/` çalışıyor.

5. Azure AD'de web uygulamasının ayarlarından aşağıdaki bilgileri not edin:

   - Uygulama Kimliği
   - Uygulama gizli dizisi

> [!NOTE]
> Uygulama gizli anahtar [olarak bir sertifika kullanılması önerilir.](/azure/active-directory/develop/active-directory-certificate-credentials) Ancak, uygulama anahtarı da uygulama anahtarı Azure portal. Aşağıdaki bölümdeki [örnek kod bir](#get-authorization-code) uygulama anahtarı kullanır.

### <a name="get-authorization-code"></a>Yetkilendirme kodunu alma

Web uygulamanıza Azure AD oturum açma çağrısından kabul etmek için bir yetkilendirme kodu alalız:

1. Azure AD'de şu URL'de oturum açma: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) . Api çağrılarını (yönetici aracısı veya satış aracısı hesabı gibi) İş Ortağı Merkezi kullanıcı hesabıyla oturum açabilirsiniz.

2. **Application-Id yerine** Azure AD uygulama kimliğinizi (GUID) girin.

3. İstendiğinde, MFA yapılandırılmış şekilde kullanıcı hesabınızla oturum açın.

4. İstendiğinde oturum açma bilgilerinizi doğrulamak için ek MFA bilgileri (telefon numarası veya e-posta adresi) girin.

5. Oturum açtıktan sonra tarayıcı, yetkilendirme kodunuzla çağrıyı web uygulaması uç noktanıza yeniden yönlendirecek. Örneğin, aşağıdaki örnek kod olarak yeniden `https://localhost:44395/` yönlendirildi.

#### <a name="authorization-code-call-trace"></a>Yetkilendirme kodu çağrı izlemesi

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

### <a name="get-refresh-token"></a>Yenileme belirteci alın

Ardından yenileme belirteci almak için yetkilendirme kodunuzu kullansanız gerekir:

1. Yetkilendirme koduyla Azure AD oturum açma uç noktasına post `https://login.microsoftonline.com/CSPTenantID/oauth2/token` çağrısı yapın. Bir örnek için aşağıdaki örnek [çağrısına bakın.](#sample-refresh-call)

2. Döndürülen yenileme belirteci not alın.

3. Yenileme belirteci Azure Key Vault. Daha fazla bilgi için api [Key Vault bakın.](/rest/api/keyvault/)

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

Uygulama API'lerine çağrılar yapmak için önce bir erişim İş Ortağı Merkezi gerekir. Erişim belirteçleri genellikle çok sınırlı bir yaşam süresine sahip olduğundan (örneğin, bir saatten az) erişim belirteci almak için yenileme belirteci kullanasınız.

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

### <a name="make-partner-center-api-calls"></a>Api İş Ortağı Merkezi çağrıları yapma

İş Ortağı Merkezi API'lerini çağıran erişim belirtec İş Ortağı Merkezi gerekir. Aşağıdaki örnek çağrıya bakın.

#### <a name="example-partner-center-api-call"></a>Örnek İş Ortağı Merkezi API çağrısı

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a>PowerShell

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

Erişim belirteci İş Ortağı Merkezi yetkilendirme kodunu değiştirmesi için gerekli altyapıyı azaltmak üzere [powershell](https://www.powershellgallery.com/packages/PartnerCenter) modülünü kullanabilirsiniz. Bu yöntem, rest çağrılarını [İş Ortağı Merkezi için isteğe bağlıdır.](#rest)

Bu işlem hakkında daha fazla bilgi için PowerShell [ile Uygulama Modeli](/powershell/partnercenter/secure-app-model) belgelerine bakın.

1. Azure AD'ye ve İş Ortağı Merkezi PowerShell modüllerini yükleyin.

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. Onay işlemini gerçekleştirmek ve gerekli yenileme belirteci yakalamak için **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** komutunu kullanın.

    ```powershell
    $credential = Get-Credential

    $token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > **Web/API** türüne sahip bir Azure AD uygulaması kullanıldığından **ServicePrincipal** parametresi **New-PartnerAccessToken** komutuyla birlikte kullanılır. Bu tür bir uygulama, erişim belirteci isteğine bir istemci tanımlayıcısı ve gizli kodun dahilsini gerektirir. **Get-Credential komutu** çağrıldığında kullanıcı adı ve parola girmeniz istenir. Kullanıcı adı olarak uygulama tanımlayıcısını girin. Parola olarak uygulama gizli parolasını girin. **New-PartnerAccessToken** komutu çağrıldığında, kimlik bilgilerini yeniden girmeniz istenir. Kullanmakta olan hizmet hesabının kimlik bilgilerini girin. Bu hizmet hesabı, uygun izinlere sahip bir iş ortağı hesabı olması gerekir.

3. Yenileme belirteci değerini kopyalayın.

    ```powershell
    $token.RefreshToken | clip
    ```

Yenileme belirteci değerini, yenileme belirteci gibi güvenli bir Azure Key Vault. PowerShell ile güvenli uygulama modülü hakkında daha fazla bilgi için çok faktörlü [kimlik doğrulaması makalesine](/powershell/partnercenter/multi-factor-auth) bakın.
