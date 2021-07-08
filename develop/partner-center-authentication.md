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
# <a name="partner-center-authentication"></a><span data-ttu-id="26e12-103">İş Ortağı Merkezi kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="26e12-103">Partner Center authentication</span></span>

<span data-ttu-id="26e12-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="26e12-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="26e12-105">İş Ortağı Merkezi kimlik doğrulaması için Azure Active Directory’yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="26e12-105">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="26e12-106">İş Ortağı Merkezi API’si, SDK veya PowerShell modülüyle etkileşim kurarken Azure AD uygulamasını doğru yapılandırmalı ve ardından erişim belirteci istemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="26e12-106">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="26e12-107">Yalnızca uygulama kullanılarak alınan erişim belirteçleri veya uygulama + kullanıcı kimlik doğrulaması Iş Ortağı Merkezi ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="26e12-107">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="26e12-108">Ancak, dikkate alınmaması gereken iki önemli öğe vardır</span><span class="sxs-lookup"><span data-stu-id="26e12-108">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="26e12-109">Uygulama + kullanıcı kimlik doğrulaması kullanarak Iş Ortağı Merkezi API 'sine erişirken Multi-Factor Authentication 'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="26e12-109">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="26e12-110">Bu değişiklik hakkında daha fazla bilgi için bkz. [güvenli uygulama modelini etkinleştirme](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="26e12-110">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="26e12-111">Tüm işlemler Iş Ortağı Merkezi API 'Sı yalnızca uygulama kimlik doğrulamasını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="26e12-111">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="26e12-112">Uygulama + kullanıcı kimlik doğrulamasını kullanmanız gereken bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="26e12-112">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="26e12-113">Her makaledeki *Önkoşul* başlığı altında, [](scenarios.md)uygulama yalnızca kimlik doğrulaması, uygulama + kullanıcı kimlik doğrulaması veya her ikisinin de desteklenip desteklenmediğini belirten belgeleri bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="26e12-113">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="26e12-114">İlk kurulum</span><span class="sxs-lookup"><span data-stu-id="26e12-114">Initial setup</span></span>

1. <span data-ttu-id="26e12-115">Başlamak için hem birincil Iş Ortağı Merkezi hesabına hem de bir tümleştirme korumalı alanı Iş Ortağı Merkezi hesabına sahip olduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e12-115">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="26e12-116">Daha fazla bilgi için bkz. [API erişimi Için Iş Ortağı Merkezi hesapları ayarlama](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="26e12-116">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="26e12-117">Hem birincil hesabınız hem de tümleştirme Sandbox hesabınız için Azure AAD uygulama kayıt KIMLIĞI ve gizli dizi (yalnızca uygulama kimliği için istemci parolası gereklidir) ' i unutmayın.</span><span class="sxs-lookup"><span data-stu-id="26e12-117">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="26e12-118">Azure portal Azure AD 'de oturum açın.</span><span class="sxs-lookup"><span data-stu-id="26e12-118">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="26e12-119">**diğer uygulamalara yönelik izinler**' de, **Windows Azure Active Directory** için izinleri **temsilci** olarak ayarlayın ve her ikisini de oturum **açan kullanıcı olarak** ve **oturum açın ve kullanıcı profilini okuyun**.</span><span class="sxs-lookup"><span data-stu-id="26e12-119">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="26e12-120">Azure portal, **uygulama ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="26e12-120">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="26e12-121">Microsoft Iş Ortağı Merkezi uygulaması olan "Microsoft Iş Ortağı Merkezi" ni arayın.</span><span class="sxs-lookup"><span data-stu-id="26e12-121">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="26e12-122">**Temsilci izinleri** , **Iş Ortağı Merkezi API 'sine erişim** için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="26e12-122">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="26e12-123">Microsoft Cloud for US Government için Microsoft Bulut almanya veya iş ortağı merkezi için iş ortağı merkezi kullanıyorsanız, bu adım zorunludur.</span><span class="sxs-lookup"><span data-stu-id="26e12-123">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="26e12-124">Iş ortağı merkezi genel örneği kullanıyorsanız, bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-124">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="26e12-125">CSP iş ortakları, iş ortağı merkezi genel örneği için bu adımı atlamak üzere Iş Ortağı Merkezi portalındaki uygulama yönetimi özelliğini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="26e12-125">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="26e12-126">Yalnızca uygulama kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="26e12-126">App-only authentication</span></span>

<span data-ttu-id="26e12-127">Iş Ortağı Merkezi REST API, .NET API, Java API 'SI veya PowerShell modülüne erişmek için yalnızca uygulama kimlik doğrulamasını kullanmak istiyorsanız, aşağıdaki yönergeleri kullanarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="26e12-127">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by using the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="26e12-128">.NET (yalnızca uygulama kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-128">.NET (app-only authentication)</span></span>

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

## <a name="java-app-only-authentication"></a><span data-ttu-id="26e12-129">Java (yalnızca uygulama kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-129">Java (app-only authentication)</span></span>

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

## <a name="rest-app-only-authentication"></a><span data-ttu-id="26e12-130">REST (yalnızca uygulama kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-130">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="26e12-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="26e12-131">REST request</span></span>

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

### <a name="rest-response"></a><span data-ttu-id="26e12-132">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="26e12-132">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="26e12-133">Uygulama + kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="26e12-133">App + User authentication</span></span>

<span data-ttu-id="26e12-134">Geçmişte, [kaynak sahibi parolası kimlik bilgileri verme](https://tools.ietf.org/html/rfc6749#section-4.3) , Iş ortağı merkezi REST API, .NET API, Java API 'Si veya PowerShell modülü ile kullanım için bir erişim belirteci istemek üzere kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="26e12-134">Historically, the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="26e12-135">bu yöntem, istemci tanımlayıcısı ve kullanıcı kimlik bilgileri kullanarak Azure Active Directory bir erişim belirteci istemek için kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="26e12-135">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="26e12-136">Ancak, uygulama + kullanıcı kimlik doğrulaması kullanılırken iş ortağı merkezi Multi-Factor Authentication gerektirdiğinden bu yaklaşım artık çalışmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="26e12-136">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="26e12-137">Microsoft bu gereksinimle uyum sağlamak için multi-factor authentication kullanarak Bulut Çözümü Sağlayıcısı (CSP) iş ortakları ve denetim masası satıcıları (cpv) kimlik doğrulaması için güvenli ve ölçeklenebilir bir çerçeve sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="26e12-137">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="26e12-138">Bu çerçeve güvenli uygulama modeli olarak bilinir ve bir onay işleminden ve bir erişim belirteci için yenileme belirteci kullanılarak bir istekten oluşur.</span><span class="sxs-lookup"><span data-stu-id="26e12-138">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="26e12-139">İş ortağı onayı</span><span class="sxs-lookup"><span data-stu-id="26e12-139">Partner consent</span></span>

<span data-ttu-id="26e12-140">İş ortağı onay süreci, iş ortağının Multi-Factor Authentication kullanarak kimlik doğrulaması yaptığı, uygulamaya yönelik onayları ve yenileme belirtecinin Azure Key Vault gibi güvenli bir depoda depolandığı etkileşimli bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="26e12-140">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="26e12-141">Bu işlem için bir tümleştirme amaçlarıyla adanmış bir hesap kullanılmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="26e12-141">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="26e12-142">İş ortağı onay sürecinde kullanılan hizmet hesabı için uygun Multi-Factor Authentication çözümü etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="26e12-142">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="26e12-143">Değilse, sonuçta elde edilen yenileme belirteci güvenlik gereksinimleriyle uyumlu olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="26e12-143">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="26e12-144">Uygulama + kullanıcı kimlik doğrulaması örnekleri</span><span class="sxs-lookup"><span data-stu-id="26e12-144">Samples for App + User authentication</span></span>

<span data-ttu-id="26e12-145">İş ortağı onay işlemi çeşitli yollarla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="26e12-145">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="26e12-146">İş ortaklarının her bir gerekli işlemin nasıl gerçekleştirileceğini anlamalarına yardımcı olmak için aşağıdaki örnekleri geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="26e12-146">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="26e12-147">Ortamınıza uygun çözümü uyguladığınızda, kodlama standartlarınız ve güvenlik ilkeleriniz ile uyumlu bir çözüm geliştirmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="26e12-147">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="26e12-148">.NET (uygulama + kullanıcı kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-148">.NET (app+user authentication)</span></span>

<span data-ttu-id="26e12-149">[iş ortağı onayı](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) örnek projesi, onayı yakalamak, yenileme belirteci istemek ve Azure Key Vault güvenli bir şekilde depolamak için ASP.NET kullanılarak geliştirilen bir web sitesini nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="26e12-149">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="26e12-150">Bu örnek için gerekli önkoşulları oluşturmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="26e12-150">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="26e12-151">Azure portal veya aşağıdaki PowerShell komutlarını kullanarak bir Azure Key Vault örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e12-151">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="26e12-152">Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e12-152">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="26e12-153">Kasa adı benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-153">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="26e12-154">Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [hızlı başlangıç: Azure Key Vault Azure Portal veya hızlı başlangıç kullanarak gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-portal) [: PowerShell kullanarak Azure Key Vault bir gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="26e12-154">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="26e12-155">Sonra bir gizli dizi ayarlayın ve alın.</span><span class="sxs-lookup"><span data-stu-id="26e12-155">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="26e12-156">Azure portal veya aşağıdaki komutları kullanarak bir Azure AD uygulaması ve anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e12-156">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="26e12-157">Aşağıdaki adımlarda kullanılabilecekleri için uygulama tanımlayıcısı ve gizli değerleri de göz önünde olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e12-157">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="26e12-158">Yeni Create Azure AD uygulamasına Azure portal veya aşağıdaki komutları kullanarak gizli dizi okuma izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="26e12-158">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="26e12-159">Iş Ortağı Merkezi için yapılandırılmış bir Azure AD uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e12-159">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="26e12-160">Bu adımı tamamlamak için aşağıdaki eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="26e12-160">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="26e12-161">Iş Ortağı Merkezi panosunun [uygulama yönetimi](https://partner.microsoft.com/pcv/apiintegration/appmanagement) özelliğine gidin</span><span class="sxs-lookup"><span data-stu-id="26e12-161">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="26e12-162">Yeni bir Azure AD uygulaması oluşturmak için *Yeni Web uygulaması Ekle* ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="26e12-162">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="26e12-163">Aşağıdaki adımlarda kullanıldıkları için *uygulama kimliği*, \* hesap kimliği \* \* ve *anahtar* değerlerini belgelediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e12-163">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="26e12-164">Visual Studio veya aşağıdaki komutu kullanarak [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) deposunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="26e12-164">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="26e12-165">Dizinde bulunan *Partneronay* projesini açın `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="26e12-165">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="26e12-166">[web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) bulunan uygulama ayarlarını doldurun</span><span class="sxs-lookup"><span data-stu-id="26e12-166">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

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
    > <span data-ttu-id="26e12-167">Uygulama gizli dizileri gibi hassas bilgiler yapılandırma dosyalarında depolanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-167">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="26e12-168">Bu örnek bir uygulama olduğu için burada gerçekleştirildi.</span><span class="sxs-lookup"><span data-stu-id="26e12-168">It was done here because this is a sample application.</span></span> <span data-ttu-id="26e12-169">Üretim uygulamanız sayesinde sertifika tabanlı kimlik doğrulaması kullanmanızı kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="26e12-169">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="26e12-170">Daha fazla bilgi için bkz. [uygulama kimlik doğrulaması Için sertifika kimlik bilgileri]( /azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="26e12-170">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="26e12-171">Bu örnek projeyi çalıştırdığınızda sizden kimlik doğrulaması istenir.</span><span class="sxs-lookup"><span data-stu-id="26e12-171">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="26e12-172">Kimlik doğrulaması başarılı olduktan sonra Azure AD 'den bir erişim belirteci istenir.</span><span class="sxs-lookup"><span data-stu-id="26e12-172">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="26e12-173">Azure AD 'den döndürülen bilgiler, yapılandırılmış Azure Key Vault örneğinde depolanan yenileme belirtecini içerir.</span><span class="sxs-lookup"><span data-stu-id="26e12-173">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="26e12-174">Java (uygulama + kullanıcı kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-174">Java (app+user authentication)</span></span>

<span data-ttu-id="26e12-175">[İş ortağı onayı](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) örnek projesi, izin yakalamak, yenileme belirteci istemek ve Azure Key Vault 'da güvenli depo sağlamak için JSP kullanılarak geliştirilen bir Web sitesini nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="26e12-175">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="26e12-176">Bu örnek için gerekli önkoşulları oluşturmak için aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="26e12-176">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="26e12-177">Azure portal veya aşağıdaki PowerShell komutlarını kullanarak bir Azure Key Vault örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e12-177">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="26e12-178">Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e12-178">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="26e12-179">Kasa adı benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-179">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="26e12-180">Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [hızlı başlangıç: Azure Key Vault Azure Portal veya hızlı başlangıç kullanarak gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-portal) [: PowerShell kullanarak Azure Key Vault bir gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="26e12-180">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="26e12-181">Azure portal veya aşağıdaki komutları kullanarak bir Azure AD uygulaması ve anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e12-181">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="26e12-182">Aşağıdaki adımlarda kullanılabilecekleri için uygulama tanımlayıcısı ve gizli değerleri belgelediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e12-182">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="26e12-183">Yeni oluşturulan Azure AD uygulamasına Azure portal veya aşağıdaki komutları kullanarak okuma gizli dizileri izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="26e12-183">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="26e12-184">Iş Ortağı Merkezi için yapılandırılmış bir Azure AD uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="26e12-184">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="26e12-185">Bu adımı tamamlamak için aşağıdakileri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="26e12-185">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="26e12-186">Iş Ortağı Merkezi panosunun [uygulama yönetimi](https://partner.microsoft.com/pcv/apiintegration/appmanagement) özelliğine gidin</span><span class="sxs-lookup"><span data-stu-id="26e12-186">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="26e12-187">Yeni bir Azure AD uygulaması oluşturmak için *Yeni Web uygulaması Ekle* ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="26e12-187">Select *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="26e12-188">Aşağıdaki adımlarda kullanıldıkları için *uygulama kimliği*, \* hesap kimliği \* \* ve *anahtar* değerlerini belgelediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="26e12-188">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="26e12-189">Aşağıdaki komutu kullanarak [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="26e12-189">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="26e12-190">Dizinde bulunan *Partneronay* projesini açın `Partner-Center-Java-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="26e12-190">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="26e12-191">[web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) dosyasında bulunan uygulama ayarlarını doldur</span><span class="sxs-lookup"><span data-stu-id="26e12-191">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

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
    > <span data-ttu-id="26e12-192">Uygulama gizli dizileri gibi hassas bilgiler, yapılandırma dosyalarında depolanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-192">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="26e12-193">Bu örnek bir uygulama olduğu için burada gerçekleştirildi.</span><span class="sxs-lookup"><span data-stu-id="26e12-193">It was done here because this is a sample application.</span></span> <span data-ttu-id="26e12-194">Üretim uygulamanız sayesinde sertifika tabanlı kimlik doğrulaması kullanmanızı kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="26e12-194">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="26e12-195">Daha fazla bilgi için bkz. [Key Vault sertifikası kimlik doğrulaması](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="26e12-195">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="26e12-196">Bu örnek projeyi çalıştırdığınızda sizden kimlik doğrulaması istenir.</span><span class="sxs-lookup"><span data-stu-id="26e12-196">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="26e12-197">Kimlik doğrulaması başarılı olduktan sonra Azure AD 'den bir erişim belirteci istenir.</span><span class="sxs-lookup"><span data-stu-id="26e12-197">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="26e12-198">Azure AD 'den döndürülen bilgiler, yapılandırılmış Azure Key Vault örneğinde depolanan yenileme belirtecini içerir.</span><span class="sxs-lookup"><span data-stu-id="26e12-198">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="26e12-199">Bulut Çözümü Sağlayıcısı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="26e12-199">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="26e12-200">Bulut Çözümü Sağlayıcısı iş ortakları, [iş ortağı onay](#partner-consent) süreci aracılığıyla elde edilen yenileme belirtecini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="26e12-200">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="26e12-201">Kimlik doğrulaması Bulut Çözümü Sağlayıcısı örnekleri</span><span class="sxs-lookup"><span data-stu-id="26e12-201">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="26e12-202">İş ortaklarının gerekli işlemleri nasıl gerçekleştireceklerini anlarına yardımcı olmak için aşağıdaki örnekleri geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="26e12-202">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="26e12-203">Ortamınıza uygun çözümü uygulayan, kodlama standartlarınız ve güvenlik ilkelerinize uygun bir çözüm geliştirmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="26e12-203">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="26e12-204">.NET (CSP kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-204">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="26e12-205">Henüz bunu yapmadıysanız, iş ortağı onay [işlemini gerçekleştirin.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="26e12-205">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="26e12-206">Aşağıdaki komutu [kullanarak Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) Visual Studio deposunu kopyalama</span><span class="sxs-lookup"><span data-stu-id="26e12-206">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="26e12-207">dizininde `CSPApplication` bulunan projeyi `Partner-Center-DotNet-Samples\secure-app-model\keyvault` açın.</span><span class="sxs-lookup"><span data-stu-id="26e12-207">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="26e12-208">App.configdosyasında [ bulunan uygulama ayarlarını ](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="26e12-208">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="26e12-209">[Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) dosyasında **bulunan PartnerId** ve **CustomerId** değişkenleri için uygun değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="26e12-209">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="26e12-210">Bu örnek projeyi çalıştırarak iş ortağı onay işlemi sırasında alınan yenileme belirteci elde eder.</span><span class="sxs-lookup"><span data-stu-id="26e12-210">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="26e12-211">Ardından, iş ortağı adına İş Ortağı Merkezi SDK'sı için bir erişim belirteci talep eder.</span><span class="sxs-lookup"><span data-stu-id="26e12-211">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="26e12-212">Son olarak, Belirtilen müşteri adına Microsoft Graph için bir erişim belirteci talep eder.</span><span class="sxs-lookup"><span data-stu-id="26e12-212">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="26e12-213">Java (CSP kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-213">Java (CSP authentication)</span></span>

1. <span data-ttu-id="26e12-214">Henüz bunu yapmadıysanız, iş ortağı onay [işlemini gerçekleştirin.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="26e12-214">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="26e12-215">aşağıdaki komutu [kullanarak Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) Visual Studio deposunu kopyalama</span><span class="sxs-lookup"><span data-stu-id="26e12-215">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="26e12-216">dizininde `cspsample` bulunan projeyi `Partner-Center-Java-Samples\secure-app-model\keyvault` açın.</span><span class="sxs-lookup"><span data-stu-id="26e12-216">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="26e12-217">[application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) dosyasında bulunan uygulama ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="26e12-217">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="26e12-218">Bu örnek projeyi çalıştırarak iş ortağı onay işlemi sırasında alınan yenileme belirteci elde eder.</span><span class="sxs-lookup"><span data-stu-id="26e12-218">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="26e12-219">Ardından, iş ortağı adına İş Ortağı Merkezi SDK'sı için bir erişim belirteci talep eder.</span><span class="sxs-lookup"><span data-stu-id="26e12-219">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="26e12-220">İsteğe bağlı - Azure Resource Manager ve Microsoft Graph müşteri adına nasıl etkileşim kuracaklarını görmek için *RunAzureTask* ve *RunGraphTask* işlev çağrılarının açıklamalarını geri almak.</span><span class="sxs-lookup"><span data-stu-id="26e12-220">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="26e12-221">Denetim Masası Sağlayıcısı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="26e12-221">Control Panel Provider authentication</span></span>

<span data-ttu-id="26e12-222">Denetim masası satıcılarının, desteklemektedir her iş ortağının iş ortağı onay [işlemini gerçekleştirmesi](#partner-consent) gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e12-222">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="26e12-223">Bu tamamlandıktan sonra, bu işlem aracılığıyla alınan yenileme belirteci, İş Ortağı Merkezi REST API .NET API'sini erişmek için kullanılır.</span><span class="sxs-lookup"><span data-stu-id="26e12-223">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="26e12-224">Bulut Paneli Sağlayıcısı kimlik doğrulaması örnekleri</span><span class="sxs-lookup"><span data-stu-id="26e12-224">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="26e12-225">Denetim masası satıcılarının her gerekli işlemi nasıl gerçekleştireceklerini anlarına yardımcı olmak için aşağıdaki örnekleri geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="26e12-225">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="26e12-226">Ortamınıza uygun çözümü uygulayan, kodlama standartlarınız ve güvenlik ilkelerinize uygun bir çözüm geliştirmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="26e12-226">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="26e12-227">.NET (CPV kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-227">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="26e12-228">İş ortaklarının uygun onayı Bulut Çözümü Sağlayıcısı bir süreç geliştirin ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="26e12-228">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="26e12-229">Bir örnek hakkında daha fazla bilgi için bkz. [iş ortağı onayı.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="26e12-229">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="26e12-230">Bir iş ortağından Bulut Çözümü Sağlayıcısı kimlik bilgileri depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="26e12-230">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="26e12-231">İş ortağı onay işlemi aracılığıyla alınan yenileme belirteci depolanmış ve herhangi bir Microsoft API'si ile etkileşim kurmak için erişim belirteçleri isteğinde bulunmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-231">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="26e12-232">Aşağıdaki komutu [kullanarak Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) Visual Studio deposunu kopyalama</span><span class="sxs-lookup"><span data-stu-id="26e12-232">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="26e12-233">dizininde `CPVApplication` bulunan projeyi `Partner-Center-DotNet-Samples\secure-app-model\keyvault` açın.</span><span class="sxs-lookup"><span data-stu-id="26e12-233">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="26e12-234">App.configdosyasında [ bulunan uygulama ayarlarını ](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="26e12-234">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="26e12-235">[Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) dosyasında **bulunan PartnerId** ve **CustomerId** değişkenleri için uygun değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="26e12-235">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="26e12-236">Bu örnek projeyi çalıştırarak belirtilen iş ortağı için yenileme belirteci alır.</span><span class="sxs-lookup"><span data-stu-id="26e12-236">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="26e12-237">Ardından, İş Ortağı Merkezi ve Azure AD Graph iş ortağı adına erişim belirteci talep eder.</span><span class="sxs-lookup"><span data-stu-id="26e12-237">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="26e12-238">Gerçekleştirdiği bir sonraki görev, müşteri kiracısına izin verilmesinin silinmesi ve oluşturulmasıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-238">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="26e12-239">Denetim masası satıcısı ile müşteri arasında ilişki yoktur, bu izinlerin İş Ortağı Merkezi API'si kullanılarak İş Ortağı Merkezi gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e12-239">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="26e12-240">Aşağıdaki örnekte bunu nasıl gerçekleştirin?</span><span class="sxs-lookup"><span data-stu-id="26e12-240">The following example shows how to accomplish that.</span></span>

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

<span data-ttu-id="26e12-241">Bu izinler belirlendikten sonra örnek, müşteri adına Azure AD Graph işlemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="26e12-241">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="26e12-242">Java (CPV kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="26e12-242">Java (CPV authentication)</span></span>

1. <span data-ttu-id="26e12-243">İş ortaklarının uygun onayı Bulut Çözümü Sağlayıcısı bir süreç geliştirin ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="26e12-243">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="26e12-244">Daha fazla bilgi ve örnek için bkz. iş [ortağı onayı.](#partner-consent)</span><span class="sxs-lookup"><span data-stu-id="26e12-244">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="26e12-245">Bir iş ortağından Bulut Çözümü Sağlayıcısı kimlik bilgileri depolanmaz.</span><span class="sxs-lookup"><span data-stu-id="26e12-245">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="26e12-246">İş ortağı onay işlemi aracılığıyla alınan yenileme belirteci depolanmış ve herhangi bir Microsoft API'si ile etkileşim kurmak için erişim belirteçleri isteğinde bulunmak için kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-246">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="26e12-247">Aşağıdaki komutu [kullanarak Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalama</span><span class="sxs-lookup"><span data-stu-id="26e12-247">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="26e12-248">dizininde `cpvsample` bulunan projeyi `Partner-Center-Java-Samples\secure-app-model\keyvault` açın.</span><span class="sxs-lookup"><span data-stu-id="26e12-248">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="26e12-249">[application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) dosyasında bulunan uygulama ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="26e12-249">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

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

    <span data-ttu-id="26e12-250">değerinin `partnercenter.displayName` market uygulamanıza görünen adı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e12-250">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="26e12-251">[Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) dosyasında **bulunan partnerId** ve **customerId** değişkenleri için uygun değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="26e12-251">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="26e12-252">Bu örnek projeyi çalıştırarak belirtilen iş ortağı için yenileme belirteci alır.</span><span class="sxs-lookup"><span data-stu-id="26e12-252">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="26e12-253">Ardından, iş ortağı adına İş Ortağı Merkezi erişim belirteci talep eder.</span><span class="sxs-lookup"><span data-stu-id="26e12-253">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="26e12-254">Gerçekleştirdiği bir sonraki görev, müşteri kiracısına izin verilmesinin silinmesi ve oluşturulmasıdır.</span><span class="sxs-lookup"><span data-stu-id="26e12-254">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="26e12-255">Denetim masası satıcısı ile müşteri arasında ilişki yoktur, bu izinlerin İş Ortağı Merkezi API'si kullanılarak İş Ortağı Merkezi gerekir.</span><span class="sxs-lookup"><span data-stu-id="26e12-255">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="26e12-256">Aşağıdaki örnekte, izinlerin nasıl ver naslı olduğu gösterir.</span><span class="sxs-lookup"><span data-stu-id="26e12-256">The following example shows how to grant the permissions.</span></span>

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

<span data-ttu-id="26e12-257">Azure Resource Manager ve Microsoft Graph müşteri adına etkileşim kurma hakkında bilgi almak için *RunAzureTask* ve *RunGraphTask* işlev çağrılarının açıklamalarını geri almak.</span><span class="sxs-lookup"><span data-stu-id="26e12-257">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
