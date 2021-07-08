---
title: İş Ortağı Merkezi kimlik doğrulaması
description: İş ortağı merkezi kimlik doğrulaması için Azure AD 'yi kullanır ve Iş Ortağı Merkezi API 'Lerini kullanmak için kimlik doğrulama ayarlarınızı doğru şekilde yapılandırmanız gerekir.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: e54feba7ea727bb7f7eff8de76dcdf28c8a453ee
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548082"
---
# <a name="partner-center-authentication"></a>İş Ortağı Merkezi kimlik doğrulaması

**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi

İş Ortağı Merkezi kimlik doğrulaması için Azure Active Directory’yi kullanır. İş Ortağı Merkezi API’si, SDK veya PowerShell modülüyle etkileşim kurarken Azure AD uygulamasını doğru yapılandırmalı ve ardından erişim belirteci istemelisiniz. Yalnızca uygulama kullanılarak alınan erişim belirteçleri veya uygulama + kullanıcı kimlik doğrulaması Iş Ortağı Merkezi ile kullanılabilir. Ancak, dikkate alınmaması gereken iki önemli öğe vardır

- Uygulama + kullanıcı kimlik doğrulaması kullanarak Iş Ortağı Merkezi API 'sine erişirken Multi-Factor Authentication 'ı kullanın. Bu değişiklik hakkında daha fazla bilgi için bkz. [güvenli uygulama modelini etkinleştirme](enable-secure-app-model.md).

- Tüm işlemler Iş Ortağı Merkezi API 'Sı yalnızca uygulama kimlik doğrulamasını desteklemez. Uygulama + kullanıcı kimlik doğrulamasını kullanmanız gereken bazı senaryolar vardır. Her makaledeki *Önkoşul* başlığı altında, [](scenarios.md)uygulama yalnızca kimlik doğrulaması, uygulama + kullanıcı kimlik doğrulaması veya her ikisinin de desteklenip desteklenmediğini belirten belgeleri bulacaksınız.

## <a name="initial-setup"></a>İlk kurulum

1. Başlamak için hem birincil Iş Ortağı Merkezi hesabına hem de bir tümleştirme korumalı alanı Iş Ortağı Merkezi hesabına sahip olduğunuzdan emin olmanız gerekir. Daha fazla bilgi için bkz. [API erişimi Için Iş Ortağı Merkezi hesapları ayarlama](set-up-api-access-in-partner-center.md). Hem birincil hesabınız hem de tümleştirme Sandbox hesabınız için Azure AAD uygulama kayıt KIMLIĞI ve gizli dizi (yalnızca uygulama kimliği için istemci parolası gereklidir) ' i unutmayın.

2. Azure portal Azure AD 'de oturum açın. **diğer uygulamalara yönelik izinler**' de, **Windows Azure Active Directory** için izinleri **temsilci** olarak ayarlayın ve her ikisini de oturum **açan kullanıcı olarak** ve **oturum açın ve kullanıcı profilini okuyun**.

3. Azure portal, **uygulama ekleyin**. Microsoft Iş Ortağı Merkezi uygulaması olan "Microsoft Iş Ortağı Merkezi" ni arayın. **Temsilci izinleri** , **Iş Ortağı Merkezi API 'sine erişim** için ayarlayın. Microsoft Cloud for US Government için Microsoft Bulut almanya veya iş ortağı merkezi için iş ortağı merkezi kullanıyorsanız, bu adım zorunludur. Iş ortağı merkezi genel örneği kullanıyorsanız, bu adım isteğe bağlıdır. CSP iş ortakları, iş ortağı merkezi genel örneği için bu adımı atlamak üzere Iş Ortağı Merkezi portalındaki uygulama yönetimi özelliğini kullanabilir.

## <a name="app-only-authentication"></a>Yalnızca uygulama kimlik doğrulaması

Iş Ortağı Merkezi REST API, .NET API, Java API 'SI veya PowerShell modülüne erişmek için yalnızca uygulama kimlik doğrulamasını kullanmak istiyorsanız, aşağıdaki yönergeleri kullanarak bunu yapabilirsiniz.

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

## <a name="app--user-authentication"></a>Uygulama + kullanıcı kimlik doğrulaması

Geçmişte, [kaynak sahibi parolası kimlik bilgileri verme](https://tools.ietf.org/html/rfc6749#section-4.3) , Iş ortağı merkezi REST API, .NET API, Java API 'Si veya PowerShell modülü ile kullanım için bir erişim belirteci istemek üzere kullanılmıştır. bu yöntem, istemci tanımlayıcısı ve kullanıcı kimlik bilgileri kullanarak Azure Active Directory bir erişim belirteci istemek için kullanılmıştır. Ancak, uygulama + kullanıcı kimlik doğrulaması kullanılırken iş ortağı merkezi Multi-Factor Authentication gerektirdiğinden bu yaklaşım artık çalışmayacaktır. Microsoft bu gereksinimle uyum sağlamak için multi-factor authentication kullanarak Bulut Çözümü Sağlayıcısı (CSP) iş ortakları ve denetim masası satıcıları (cpv) kimlik doğrulaması için güvenli ve ölçeklenebilir bir çerçeve sunmuştur. Bu çerçeve güvenli uygulama modeli olarak bilinir ve bir onay işleminden ve bir erişim belirteci için yenileme belirteci kullanılarak bir istekten oluşur.

### <a name="partner-consent"></a>İş ortağı onayı

İş ortağı onay süreci, iş ortağının Multi-Factor Authentication kullanarak kimlik doğrulaması yaptığı, uygulamaya yönelik onayları ve yenileme belirtecinin Azure Key Vault gibi güvenli bir depoda depolandığı etkileşimli bir işlemdir. Bu işlem için bir tümleştirme amaçlarıyla adanmış bir hesap kullanılmasını öneririz.

> [!IMPORTANT]
> İş ortağı onay sürecinde kullanılan hizmet hesabı için uygun Multi-Factor Authentication çözümü etkinleştirilmelidir. Değilse, sonuçta elde edilen yenileme belirteci güvenlik gereksinimleriyle uyumlu olmayacaktır.

### <a name="samples-for-app--user-authentication"></a>Uygulama + kullanıcı kimlik doğrulaması örnekleri

İş ortağı onay işlemi çeşitli yollarla gerçekleştirilebilir. İş ortaklarının her bir gerekli işlemin nasıl gerçekleştirileceğini anlamalarına yardımcı olmak için aşağıdaki örnekleri geliştirdik. Ortamınıza uygun çözümü uyguladığınızda, kodlama standartlarınız ve güvenlik ilkeleriniz ile uyumlu bir çözüm geliştirmeniz önemlidir.

## <a name="net-appuser-authentication"></a>.NET (uygulama + kullanıcı kimlik doğrulaması)

[iş ortağı onayı](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) örnek projesi, onayı yakalamak, yenileme belirteci istemek ve Azure Key Vault güvenli bir şekilde depolamak için ASP.NET kullanılarak geliştirilen bir web sitesini nasıl kullanacağınızı gösterir. Bu örnek için gerekli önkoşulları oluşturmak için aşağıdaki adımları gerçekleştirin.

1. Azure portal veya aşağıdaki PowerShell komutlarını kullanarak bir Azure Key Vault örneği oluşturun. Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirdiğinizden emin olun. Kasa adı benzersiz olmalıdır.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [hızlı başlangıç: Azure Key Vault Azure Portal veya hızlı başlangıç kullanarak gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-portal) [: PowerShell kullanarak Azure Key Vault bir gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-powershell). Sonra bir gizli dizi ayarlayın ve alın.

2. Azure portal veya aşağıdaki komutları kullanarak bir Azure AD uygulaması ve anahtarı oluşturun.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Aşağıdaki adımlarda kullanılabilecekleri için uygulama tanımlayıcısı ve gizli değerleri de göz önünde olduğunuzdan emin olun.

3. Yeni Create Azure AD uygulamasına Azure portal veya aşağıdaki komutları kullanarak gizli dizi okuma izinleri verin.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Iş Ortağı Merkezi için yapılandırılmış bir Azure AD uygulaması oluşturun. Bu adımı tamamlamak için aşağıdaki eylemleri gerçekleştirin.

    - Iş Ortağı Merkezi panosunun [uygulama yönetimi](https://partner.microsoft.com/pcv/apiintegration/appmanagement) özelliğine gidin
    - Yeni bir Azure AD uygulaması oluşturmak için *Yeni Web uygulaması Ekle* ' yi seçin.

    Aşağıdaki adımlarda kullanıldıkları için *uygulama kimliği*, * hesap kimliği * * ve *anahtar* değerlerini belgelediğinizden emin olun.

5. Visual Studio veya aşağıdaki komutu kullanarak [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) deposunu kopyalayın.

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. Dizinde bulunan *Partneronay* projesini açın `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .

7. [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) bulunan uygulama ayarlarını doldurun

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
    > Uygulama gizli dizileri gibi hassas bilgiler yapılandırma dosyalarında depolanmamalıdır. Bu örnek bir uygulama olduğu için burada gerçekleştirildi. Üretim uygulamanız sayesinde sertifika tabanlı kimlik doğrulaması kullanmanızı kesinlikle öneririz. Daha fazla bilgi için bkz. [uygulama kimlik doğrulaması Için sertifika kimlik bilgileri]( /azure/active-directory/develop/active-directory-certificate-credentials).

8. Bu örnek projeyi çalıştırdığınızda sizden kimlik doğrulaması istenir. Kimlik doğrulaması başarılı olduktan sonra Azure AD 'den bir erişim belirteci istenir. Azure AD 'den döndürülen bilgiler, yapılandırılmış Azure Key Vault örneğinde depolanan yenileme belirtecini içerir.

## <a name="java-appuser-authentication"></a>Java (uygulama + kullanıcı kimlik doğrulaması)

[İş ortağı onayı](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) örnek projesi, izin yakalamak, yenileme belirteci istemek ve Azure Key Vault 'da güvenli depo sağlamak için JSP kullanılarak geliştirilen bir Web sitesini nasıl kullanacağınızı gösterir. Bu örnek için gerekli önkoşulları oluşturmak için aşağıdakileri yapın.

1. Azure portal veya aşağıdaki PowerShell komutlarını kullanarak bir Azure Key Vault örneği oluşturun. Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirdiğinizden emin olun. Kasa adı benzersiz olmalıdır.

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [hızlı başlangıç: Azure Key Vault Azure Portal veya hızlı başlangıç kullanarak gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-portal) [: PowerShell kullanarak Azure Key Vault bir gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-powershell).

2. Azure portal veya aşağıdaki komutları kullanarak bir Azure AD uygulaması ve anahtarı oluşturun.

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    Aşağıdaki adımlarda kullanılabilecekleri için uygulama tanımlayıcısı ve gizli değerleri belgelediğinizden emin olun.

3. Yeni oluşturulan Azure AD uygulamasına Azure portal veya aşağıdaki komutları kullanarak okuma gizli dizileri izinleri verin.

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. Iş Ortağı Merkezi için yapılandırılmış bir Azure AD uygulaması oluşturun. Bu adımı tamamlamak için aşağıdakileri gerçekleştirin.

    - Iş Ortağı Merkezi panosunun [uygulama yönetimi](https://partner.microsoft.com/pcv/apiintegration/appmanagement) özelliğine gidin
    - Yeni bir Azure AD uygulaması oluşturmak için *Yeni Web uygulaması Ekle* ' yi seçin.

    Aşağıdaki adımlarda kullanıldıkları için *uygulama kimliği*, * hesap kimliği * * ve *anahtar* değerlerini belgelediğinizden emin olun.

5. Aşağıdaki komutu kullanarak [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalayın

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. Dizinde bulunan *Partneronay* projesini açın `Partner-Center-Java-Samples\secure-app-model\keyvault` .

7. [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) dosyasında bulunan uygulama ayarlarını doldur

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
    > Uygulama gizli dizileri gibi hassas bilgiler, yapılandırma dosyalarında depolanmamalıdır. Bu örnek bir uygulama olduğu için burada gerçekleştirildi. Üretim uygulamanız sayesinde sertifika tabanlı kimlik doğrulaması kullanmanızı kesinlikle öneririz. Daha fazla bilgi için bkz. [Key Vault sertifikası kimlik doğrulaması](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).

8. Bu örnek projeyi çalıştırdığınızda sizden kimlik doğrulaması istenir. Kimlik doğrulaması başarılı olduktan sonra Azure AD 'den bir erişim belirteci istenir. Azure AD 'den döndürülen bilgiler, yapılandırılmış Azure Key Vault örneğinde depolanan yenileme belirtecini içerir.

## <a name="cloud-solution-provider-authentication"></a>Bulut Çözümü Sağlayıcısı kimlik doğrulaması

Bulut Çözümü Sağlayıcısı iş ortakları, [iş ortağı onay](#partner-consent) süreci aracılığıyla elde edilen yenileme belirtecini kullanabilir.

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
