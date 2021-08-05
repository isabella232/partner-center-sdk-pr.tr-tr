---
title: İş Ortağı Merkezi kimlik doğrulaması
description: İş Ortağı Merkezi kimlik doğrulaması için Azure AD'yi ve İş Ortağı Merkezi API'lerini kullanmak için kimlik doğrulama ayarlarınızı doğru yapılandırmanız gerekir.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 75d60ca983cd5b8fe53134ec7481319b153e128a
ms.sourcegitcommit: 07b9a11f5c615ed1e716081392032cea2124bd98
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 08/04/2021
ms.locfileid: "115104202"
---
# <a name="partner-center-authentication"></a>İş Ortağı Merkezi kimlik doğrulaması

**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government

İş Ortağı Merkezi kimlik doğrulaması için Azure Active Directory’yi kullanır. İş Ortağı Merkezi API’si, SDK veya PowerShell modülüyle etkileşim kurarken Azure AD uygulamasını doğru yapılandırmalı ve ardından erişim belirteci istemelisiniz. Yalnızca uygulama veya uygulama + kullanıcı kimlik doğrulaması kullanılarak alınan erişim belirteçleri, İş Ortağı Merkezi. Ancak dikkate alınacak iki önemli öğe vardır

- Uygulama + kullanıcı kimlik doğrulaması kullanarak İş Ortağı Merkezi API'sine erişirken çok faktörlü kimlik doğrulamasını kullanın. Bu değişiklikle ilgili daha fazla bilgi için [bkz. Güvenli uygulama modelini etkinleştirme.](enable-secure-app-model.md)

- API'nin tüm işlemleri İş Ortağı Merkezi uygulama kimlik doğrulamasını desteklemez. Uygulama + kullanıcı kimlik doğrulamasını kullanmanın gerekli olduğu bazı senaryolar vardır. Her *makalenin Önkoşullar* başlığı [altında,](scenarios.md)yalnızca uygulama kimlik doğrulamasının, uygulama + kullanıcı kimlik doğrulamasının veya her ikisinin de destekçisi olup olmadığının yer alan belgeleri bulabilirsiniz.

## <a name="initial-setup"></a>İlk kurulum

1. Başlamak için hem birincil hesap hesabınız hem de bir tümleştirme korumalı alanı İş Ortağı Merkezi olduğundan emin İş Ortağı Merkezi gerekir. Daha fazla bilgi için [bkz. API erişimi İş Ortağı Merkezi hesapları ayarlama.](set-up-api-access-in-partner-center.md) Hem birincil hesabınız hem de tümleştirme korumalı alan hesabınız için Azure AAD Uygulama kayıt kimliği ve Gizli Anahtar (yalnızca Uygulama kimliği için gizli anahtar gereklidir) not edin.

2. Azure AD'de oturum Azure portal. Diğer **uygulamalara izinler'de,** **Windows Azure Active Directory** için izinleri Temsilci İzinleri  olarak ayarlayın ve hem Oturum açma kullanıcısı olarak dizine eriş'i hem de Oturum açma ve kullanıcı **profilini okuma'yi seçin.**

3. Uygulama Azure portal **ekleyin.** Microsoft İş Ortağı Merkezi uygulaması olan "Microsoft İş Ortağı Merkezi" araması. Temsilci **İzinlerini API'sini** **Erişim İş Ortağı Merkezi ayarlayın.** Microsoft Bulut Almanya için İş Ortağı Merkezi veya İş Ortağı Merkezi için Microsoft Cloud for US Government kullanıyorsanız, bu adım zorunludur. Genel bir örneği İş Ortağı Merkezi, bu adım isteğe bağlıdır. CSP İş Ortakları, İş Ortağı Merkezi portalında Uygulama Yönetimi özelliğini kullanarak genel örnek için bu İş Ortağı Merkezi atlar.

## <a name="app-only-authentication"></a>Yalnızca uygulama kimlik doğrulaması

İş Ortağı Merkezi REST API, .NET API, Java API veya PowerShell modülüne erişmek için yalnızca uygulama kimlik doğrulamasını kullanmak için aşağıdaki yönergeleri kullanarak bunu yapabilirsiniz.

## <a name="net-app-only-authentication"></a>.NET (yalnızca uygulama kimlik doğrulaması)

```csharp
public static IAggregatePartner GetPartnerCenterTokenUsingAppCredentials()
{
    IPartnerCredentials partnerCredentials =
        PartnerCredentials.Instance.GenerateByApplicationCredentials(
            PartnerApplicationConfiguration.ApplicationId,
            PartnerApplicationConfiguration.ApplicationSecret,
            PartnerApplicationConfiguration.ApplicationDomain);

    // Create operations instance with partnerCredentials.
    return PartnerService.Instance.CreatePartnerOperations(partnerCredentials);
}
```

## <a name="java-app-only-authentication"></a>Java (yalnızca uygulama kimlik doğrulaması)

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

```java
public IAggregatePartner getAppPartnerOperations()
{
    IPartnerCredentials appCredentials =
        PartnerCredentials.getInstance().generateByApplicationCredentials(
        PartnerApplicationConfiguration.getApplicationId(),
        PartnerApplicationConfiguration.getApplicationSecret(),
        PartnerApplicationConfiguration.getApplicationDomain());

    return PartnerService.getInstance().createPartnerOperations( appCredentials );
}
```

## <a name="rest-app-only-authentication"></a>REST (yalnızca uygulama kimlik doğrulaması)

### <a name="rest-request"></a>REST isteği

```http
POST https://login.microsoftonline.com/{tenantId}/oauth2/token HTTP/1.1
Accept: application/json
return-client-request-id: true
Content-Type: application/x-www-form-urlencoded; charset=utf-8
Host: login.microsoftonline.com
Content-Length: 194
Expect: 100-continue

resource=https%3A%2F%2Fgraph.windows.net&client_id={client-id-here}&client_secret={client-secret-here}&grant_type=client_credentials
```

### <a name="rest-response"></a>REST yanıtı

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a>Uygulama + Kullanıcı kimlik doğrulaması

Geçmişte kaynak [sahibi parola](https://tools.ietf.org/html/rfc6749#section-4.3) kimlik bilgileri izni, İş Ortağı Merkezi REST API, .NET API, Java API veya PowerShell modülüyle kullanım için erişim belirteci isteğinde bulunurdu. Bu yöntem, istemci tanımlayıcısı ve kullanıcı kimlik bilgileri Azure Active Directory bir erişim belirteci isteğinde Azure Active Directory için kullanıldı. Ancak, uygulama + kullanıcı kimlik doğrulaması İş Ortağı Merkezi çok faktörlü kimlik doğrulaması gerektirdiği için bu yaklaşım artık çalışmaz. Bu gereksinime uymak için Microsoft, çok faktörlü kimlik doğrulaması kullanarak Bulut Çözümü Sağlayıcısı (CSP) iş ortaklarının ve denetim masası satıcılarının (CPV) kimlik doğrulamasını sağlamak için güvenli, ölçeklenebilir bir çerçeve ortaya verdi. Bu çerçeve, Güvenli Uygulama Modeli olarak bilinir ve bir onay işlemi ve yenileme belirteci kullanılarak erişim belirteci isteği oluşur.

### <a name="partner-consent"></a>İş ortağı onayı

İş ortağı onay işlemi, iş ortağının çok faktörlü kimlik doğrulaması kullanarak kimlik doğrulaması, uygulamaya onaylar ve yenileme belirteci gibi güvenli bir depoda depolandığı etkileşimli bir Azure Key Vault. Bu işlem için tümleştirme amacıyla ayrılmış bir hesap kullanılması önerilir.

> [!IMPORTANT]
> İş ortağı onay sürecinde kullanılan hizmet hesabı için uygun çok faktörlü kimlik doğrulaması çözümünün etkinleştirilmesi gerekir. Değilse, sonuçta elde edilen yenileme belirteci güvenlik gereksinimleriyle uyumlu olmaz.

### <a name="samples-for-app--user-authentication"></a>Uygulama + Kullanıcı kimlik doğrulaması örnekleri

İş ortağı onay işlemi çeşitli yollarla yapılabilir. İş ortaklarının gerekli işlemleri nasıl gerçekleştireceklerini anlarına yardımcı olmak için aşağıdaki örnekleri geliştirdik. Ortamınıza uygun çözümü uygulayan, kodlama standartlarınız ve güvenlik ilkelerinize uygun bir çözüm geliştirmeniz önemlidir.

## <a name="net-appuser-authentication"></a>.NET (uygulama+kullanıcı kimlik doğrulaması)

İş [ortağı onayı](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) örnek projesi, onay almak, yenileme belirteci ASP.NET ve bu web sitesini Azure Key Vault. Bu örnek için gerekli önkoşulları oluşturmak üzere aşağıdaki adımları gerçekleştirin.

1. Azure portal veya aşağıdaki PowerShell komutlarını Azure Key Vault bir örnek oluşturun. Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirerek emin olun. Kasa adı benzersiz olmalıdır.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [Hızlı başlangıç: Azure Key Vault Azure portal](/azure/key-vault/quick-create-portal) veya Hızlı [Başlangıç: PowerShell](/azure/key-vault/quick-create-powershell)kullanarak gizli dizi ayarlama ve Azure Key Vault'den gizli dizi alma. Ardından bir gizli dizi ayarlayın ve alın.

2. Azure portal veya aşağıdaki komutları kullanarak bir Azure AD Uygulaması ve anahtar oluşturun.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Uygulama tanımlayıcısı ve gizli değerlerini not edin çünkü bunlar aşağıdaki adımlarda kullanılacaktır.

3. Yeni oluşturulan Azure AD uygulamasına aşağıdaki komutları kullanarak gizli dizileri Azure portal izinlerini verin.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. İş Ortağı Merkezi için yapılandırılmış bir Azure AD İş Ortağı Merkezi. Bu adımı tamamlamak için aşağıdaki eylemleri gerçekleştirin.

    - İş Ortağı Merkezi [Panosu'nın](https://partner.microsoft.com/pcv/apiintegration/appmanagement) Uygulama yönetimi özelliğine göz atma
    - Yeni bir Azure AD *uygulaması oluşturmak* için Yeni web uygulaması ekle'yi seçin.

    Uygulama Kimliği, *Hesap *Kimliği*** ve Anahtar  değerlerini belgeleyenin çünkü bunlar aşağıdaki adımlarda kullanılacaktır.

5. Aşağıdaki komutu [kullanarak Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) Visual Studio deposunu kopya edin.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. dizininde *bulunan PartnerConsent* projesini `Partner-Center-DotNet-Samples\secure-app-model\keyvault` açın.

7. Uygulama ayarlarında bulunan uygulama ayarlarını [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!--
        Endpoint address for the instance of Azure KeyVault. This is
        the DNS Name for the instance of Key Vault that you provisioned.
     -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- App ID that is given access for KeyVault to store refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate
        to your environment. The following application secret is for sample
        application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

    > [!IMPORTANT]
    > Uygulama gizli dizileri gibi hassas bilgiler yapılandırma dosyalarında depolanmaz. Bu örnek bir uygulama olduğu için burada yapıldı. Üretim uygulamanız ile sertifika tabanlı kimlik doğrulamasını kesinlikle öneririz. Daha fazla bilgi için [bkz. Uygulama kimlik doğrulaması için sertifika kimlik bilgileri.]( /azure/active-directory/develop/active-directory-certificate-credentials)

8. Bu örnek projeyi çalıştırsanız kimlik doğrulaması istenir. Kimlik doğrulama başarılı olduktan sonra Azure AD'den erişim belirteci istenmektedir. Azure AD'den döndürülen bilgiler, yapılandırmanın yapılandırılmış örneğinde depolanan bir yenileme belirteci Azure Key Vault.

## <a name="java-appuser-authentication"></a>Java (uygulama+kullanıcı kimlik doğrulaması)

İş [ortağı onayı](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) örnek projesi, JSP kullanılarak geliştirilen bir web sitesinin, onayı yakalamak, yenileme belirteci talep etmek ve Azure Key Vault. Bu örnek için gerekli önkoşulları oluşturmak üzere aşağıdakini gerçekleştirin.

1. Azure portal veya aşağıdaki PowerShell komutlarını Azure Key Vault bir örnek oluşturun. Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirerek emin olun. Kasa adı benzersiz olmalıdır.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [Hızlı başlangıç: Azure Key Vault Azure portal](/azure/key-vault/quick-create-portal) veya Hızlı [Başlangıç: PowerShell](/azure/key-vault/quick-create-powershell)kullanarak gizli dizi ayarlama ve Azure Key Vault'den gizli dizi alma.

2. Azure portal veya aşağıdaki komutları kullanarak bir Azure AD Uygulaması ve anahtar oluşturun.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Aşağıdaki adımlarda kullanılacak olan uygulama tanımlayıcısı ve gizli değerleri belgeleyenin.

3. Yeni oluşturulan Azure AD uygulamasına aşağıdaki komutları kullanarak gizli dizileri Azure portal izinlerini verin.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. İş Ortağı Merkezi için yapılandırılmış bir Azure AD İş Ortağı Merkezi. Bu adımı tamamlamak için aşağıdaki işlemleri gerçekleştirin.

    - İş Ortağı Merkezi [Panosu'nın](https://partner.microsoft.com/pcv/apiintegration/appmanagement) Uygulama yönetimi özelliğine göz atma
    - Yeni bir Azure AD *uygulaması oluşturmak* için Yeni web uygulaması ekle'yi seçin.

    Uygulama Kimliği, *Hesap *Kimliği*** ve Anahtar  değerlerini belgeleyenin çünkü bunlar aşağıdaki adımlarda kullanılacaktır.

5. Aşağıdaki komutu [kullanarak Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalama

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. dizininde *bulunan PartnerConsent* projesini `Partner-Center-Java-Samples\secure-app-model\keyvault` açın.

7. web.xmldosyasında bulunan uygulama [ ayarlarını ](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) doldurmak

    ```xml
    <filter>
        <filter-name>AuthenticationFilter</filter-name>
        <filter-class>com.microsoft.store.samples.partnerconsent.security.AuthenticationFilter</filter-class>
        <init-param>
            <param-name>client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_base_url</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_id</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_client_secret</param-name>
            <param-value></param-value>
        </init-param>
        <init-param>
            <param-name>keyvault_certifcate_path</param-name>
            <param-value></param-value>
        </init-param>
    </filter>
    ```

    > [!IMPORTANT]
    > Uygulama gizli dizileri gibi hassas bilgiler yapılandırma dosyalarında depolanmaz. Bu örnek bir uygulama olduğu için burada yapıldı. Üretim uygulamanız ile sertifika tabanlı kimlik doğrulaması kullanmanızı kesinlikle öneririz. Daha fazla bilgi için [bkz. Key Vault Sertifika kimlik doğrulaması.](https://github.com/Azure-Samples/key-vault-java-certificate-authentication)

8. Bu örnek projeyi çalıştırsanız kimlik doğrulaması istenir. Kimlik doğrulama başarılı olduktan sonra Azure AD'den erişim belirteci istenmektedir. Azure AD'den döndürülen bilgiler, yapılandırmanın yapılandırılmış örneğinde depolanan bir yenileme belirteci Azure Key Vault.

## <a name="cloud-solution-provider-authentication"></a>Bulut Çözümü Sağlayıcısı doğrulaması

Bulut Çözümü Sağlayıcısı iş ortakları, iş ortağı onay işlemiyle elde edilen yenileme [belirteci](#partner-consent) kullanabilir.

### <a name="samples-for-cloud-solution-provider-authentication"></a>Kimlik doğrulaması Bulut Çözümü Sağlayıcısı örnekleri

İş ortaklarının gerekli işlemleri nasıl gerçekleştireceklerini anlarına yardımcı olmak için aşağıdaki örnekleri geliştirdik. Ortamınıza uygun çözümü uygulayan, kodlama standartlarınız ve güvenlik ilkelerinize uygun bir çözüm geliştirmeniz önemlidir.

## <a name="net-csp-authentication"></a>.NET (CSP kimlik doğrulaması)

1. Henüz bunu yapmadıysanız, iş ortağı onay [işlemini gerçekleştirin.](#partner-consent)

2. Aşağıdaki komutu [kullanarak Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) Visual Studio deposunu kopyalama

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. dizininde `CSPApplication` bulunan projeyi `Partner-Center-DotNet-Samples\secure-app-model\keyvault` açın.

4. App.configdosyasında [ bulunan uygulama ayarlarını ](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) güncelleştirin.

    ```xml
    <!-- AppID that represents CSP application -->
    <add key="ida:CSPApplicationId" value="" />
    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CSPApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) dosyasında **bulunan PartnerId** ve **CustomerId** değişkenleri için uygun değerleri ayarlayın.

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Bu örnek projeyi çalıştırarak iş ortağı onay işlemi sırasında alınan yenileme belirteci elde eder. Ardından, iş ortağı adına İş Ortağı Merkezi SDK'sı için bir erişim belirteci talep eder. Son olarak, Belirtilen müşteri adına Microsoft Graph için bir erişim belirteci talep eder.

## <a name="java-csp-authentication"></a>Java (CSP kimlik doğrulaması)

1. Henüz bunu yapmadıysanız, iş ortağı onay [işlemini gerçekleştirin.](#partner-consent)

2. aşağıdaki komutu [kullanarak Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) Visual Studio deposunu kopyalama

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. dizininde `cspsample` bulunan projeyi `Partner-Center-Java-Samples\secure-app-model\keyvault` açın.

4. [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) dosyasında bulunan uygulama ayarlarını güncelleştirin.

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. Bu örnek projeyi çalıştırarak iş ortağı onay işlemi sırasında alınan yenileme belirteci elde eder. Ardından, iş ortağı adına İş Ortağı Merkezi SDK'sı için bir erişim belirteci talep eder.

6. İsteğe bağlı - Azure Resource Manager ve Microsoft Graph müşteri adına nasıl etkileşim kuracaklarını görmek için *RunAzureTask* ve *RunGraphTask* işlev çağrılarının açıklamalarını geri almak.

## <a name="control-panel-provider-authentication"></a>Denetim Masası Sağlayıcısı kimlik doğrulaması

Denetim masası satıcılarının, desteklemektedir her iş ortağının iş ortağı onay [işlemini gerçekleştirmesi](#partner-consent) gerekir. Bu tamamlandıktan sonra, bu işlem aracılığıyla alınan yenileme belirteci, İş Ortağı Merkezi REST API .NET API'sini erişmek için kullanılır.

### <a name="samples-for-cloud-panel-provider-authentication"></a>Bulut Paneli Sağlayıcısı kimlik doğrulaması örnekleri

Denetim masası satıcılarının her gerekli işlemi nasıl gerçekleştireceklerini anlarına yardımcı olmak için aşağıdaki örnekleri geliştirdik. Ortamınıza uygun çözümü uygulayan, kodlama standartlarınız ve güvenlik ilkelerinize uygun bir çözüm geliştirmeniz önemlidir.

## <a name="net-cpv-authentication"></a>.NET (CPV kimlik doğrulaması)

1. İş ortaklarının uygun onayı Bulut Çözümü Sağlayıcısı bir süreç geliştirin ve dağıtın. Bir örnek hakkında daha fazla bilgi için bkz. [iş ortağı onayı.](#partner-consent)

    > [!IMPORTANT]
    > Bir iş ortağından Bulut Çözümü Sağlayıcısı kimlik bilgileri depolanmaz. İş ortağı onay işlemi aracılığıyla alınan yenileme belirteci depolanmış ve herhangi bir Microsoft API'si ile etkileşim kurmak için erişim belirteçleri isteğinde bulunmak için kullanılmalıdır.

2. Aşağıdaki komutu [kullanarak Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) Visual Studio deposunu kopyalama

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. dizininde `CPVApplication` bulunan projeyi `Partner-Center-DotNet-Samples\secure-app-model\keyvault` açın.

4. App.configdosyasında [ bulunan uygulama ayarlarını ](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) güncelleştirin.

    ```xml
    <!-- AppID that represents Control panel vendor application -->
    <add key="ida:CPVApplicationId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:CPVApplicationSecret" value="" />

    <!-- Endpoint address for the instance of Azure KeyVault -->
    <add key="KeyVaultEndpoint" value="" />

    <!-- AppID that is given access for keyvault to store the refresh tokens -->
    <add key="ida:KeyVaultClientId" value="" />

    <!--
        Please use certificate as your client secret and deploy the certificate to your environment.
        The following application secret is for sample application only. please do not use secret directly from the config file.
    -->
    <add key="ida:KeyVaultClientSecret" value="" />
    ```

5. [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) dosyasında **bulunan PartnerId** ve **CustomerId** değişkenleri için uygun değerleri ayarlayın.

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. Bu örnek projeyi çalıştırarak belirtilen iş ortağı için yenileme belirteci alır. Ardından, İş Ortağı Merkezi ve Azure AD Graph iş ortağı adına erişim belirteci talep eder. Gerçekleştirdiği bir sonraki görev, müşteri kiracısına izin verilmesinin silinmesi ve oluşturulmasıdır. Denetim masası satıcısı ile müşteri arasında ilişki yoktur, bu izinlerin İş Ortağı Merkezi API'si kullanılarak İş Ortağı Merkezi gerekir. Aşağıdaki örnekte bunu nasıl gerçekleştirin?

    ```csharp
    JObject contents = new JObject
    {
        // Provide your application display name
        ["displayName"] = "CPV Marketplace",

        // Provide your application id
        ["applicationId"] = CPVApplicationId,

        // Provide your application grants
        ["applicationGrants"] = new JArray(
            JObject.Parse("{\"enterpriseApplicationId\": \"00000002-0000-0000-c000-000000000000\", \"scope\":\"Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All\"}"), // for Azure AD Graph access,  Directory.Read.All
            JObject.Parse("{\"enterpriseApplicationId\": \"797f4846-ba00-4fd7-ba43-dac1f8f63013\", \"scope\":\"user_impersonation\"}")) // for Azure Resource Manager access
    };

    /**
     * The following steps have to be performed once per customer tenant if your application is
     * a control panel vendor application and requires customer tenant Azure AD Graph access.
     **/

    // delete the previous grant into customer tenant
    JObject consentDeletion = await ApiCalls.DeleteAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents/{1}", CustomerId, CPVApplicationId));

    // create new grants for the application given the setting in application grants payload.
    JObject consentCreation = await ApiCalls.PostAsync(
        tokenPartnerResult.Item1,
        string.Format("https://api.partnercenter.microsoft.com/v1/customers/{0}/applicationconsents", CustomerId),
        contents.ToString());
    ```

Bu izinler belirlendikten sonra örnek, müşteri adına Azure AD Graph işlemleri gerçekleştirir.

## <a name="java-cpv-authentication"></a>Java (CPV kimlik doğrulaması)

1. İş ortaklarının uygun onayı Bulut Çözümü Sağlayıcısı bir süreç geliştirin ve dağıtın. Daha fazla bilgi ve örnek için bkz. iş [ortağı onayı.](#partner-consent)

    > [!IMPORTANT]
    > Bir iş ortağından Bulut Çözümü Sağlayıcısı kimlik bilgileri depolanmaz. İş ortağı onay işlemi aracılığıyla alınan yenileme belirteci depolanmış ve herhangi bir Microsoft API'si ile etkileşim kurmak için erişim belirteçleri isteğinde bulunmak için kullanılmalıdır.

2. Aşağıdaki komutu [kullanarak Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalama

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. dizininde `cpvsample` bulunan projeyi `Partner-Center-Java-Samples\secure-app-model\keyvault` açın.

4. [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) dosyasında bulunan uygulama ayarlarını güncelleştirin.

    ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    partnercenter.displayName=
    ```

    değerinin `partnercenter.displayName` market uygulamanıza görünen adı olması gerekir.

5. [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) dosyasında **bulunan partnerId** ve **customerId** değişkenleri için uygun değerleri ayarlayın.

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. Bu örnek projeyi çalıştırarak belirtilen iş ortağı için yenileme belirteci alır. Ardından, iş ortağı adına İş Ortağı Merkezi erişim belirteci talep eder. Gerçekleştirdiği bir sonraki görev, müşteri kiracısına izin verilmesinin silinmesi ve oluşturulmasıdır. Denetim masası satıcısı ile müşteri arasında ilişki yoktur, bu izinlerin İş Ortağı Merkezi API'si kullanılarak İş Ortağı Merkezi gerekir. Aşağıdaki örnekte, izinlerin nasıl ver naslı olduğu gösterir.

    ```java
    ApplicationGrant azureAppGrant = new ApplicationGrant();

    azureAppGrant.setEnterpriseApplication("797f4846-ba00-4fd7-ba43-dac1f8f63013");
    azureAppGrant.setScope("user_impersonation");

    ApplicationGrant graphAppGrant = new ApplicationGrant();

    graphAppGrant.setEnterpriseApplication("00000002-0000-0000-c000-000000000000");
    graphAppGrant.setScope("Domain.ReadWrite.All,User.ReadWrite.All,Directory.Read.All");

    ApplicationConsent consent = new ApplicationConsent();

    consent.setApplicationGrants(Arrays.asList(azureAppGrant, graphAppGrant));
    consent.setApplicationId(properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID));
    consent.setDisplayName(properties.getProperty(PropertyName.PARTNER_CENTER_DISPLAY_NAME));

    // Deletes the existing grant into the customer it is present.
    partnerOperations.getServiceClient().delete(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents/{1}",
            customerId,
            properties.getProperty(PropertyName.PARTNER_CENTER_CLIENT_ID)));

    // Consent to the defined applications and the respective scopes.
    partnerOperations.getServiceClient().post(
        partnerOperations,
        new TypeReference<ApplicationConsent>(){},
        MessageFormat.format(
            "customers/{0}/applicationconsents",
            customerId),
        consent);
    ```

Azure Resource Manager ve Microsoft Graph müşteri adına etkileşim kurma hakkında bilgi almak için *RunAzureTask* ve *RunGraphTask* işlev çağrılarının açıklamalarını geri almak.
