---
title: İş Ortağı Merkezi kimlik doğrulaması
description: İş ortağı merkezi kimlik doğrulaması için Azure AD 'yi kullanır ve Iş Ortağı Merkezi API 'Lerini kullanmak için kimlik doğrulama ayarlarınızı doğru şekilde yapılandırmanız gerekir.
ms.date: 11/13/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
ms.openlocfilehash: 46ef9c6bc151c368281e943b7d24ebc07e34b66d
ms.sourcegitcommit: 64c498d3571f2287305968890578bc7396779621
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/19/2020
ms.locfileid: "97770290"
---
# <a name="partner-center-authentication"></a><span data-ttu-id="5fa30-103">İş Ortağı Merkezi kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5fa30-103">Partner Center authentication</span></span>

<span data-ttu-id="5fa30-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="5fa30-104">**Applies to:**</span></span>

- <span data-ttu-id="5fa30-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5fa30-105">Partner Center</span></span>
- <span data-ttu-id="5fa30-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5fa30-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5fa30-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5fa30-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5fa30-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5fa30-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5fa30-109">İş Ortağı Merkezi kimlik doğrulaması için Azure Active Directory’yi kullanır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-109">Partner Center uses Azure Active Directory for authentication.</span></span> <span data-ttu-id="5fa30-110">İş Ortağı Merkezi API’si, SDK veya PowerShell modülüyle etkileşim kurarken Azure AD uygulamasını doğru yapılandırmalı ve ardından erişim belirteci istemelisiniz.</span><span class="sxs-lookup"><span data-stu-id="5fa30-110">When interacting with the Partner Center API, SDK, or PowerShell module you must correctly configure an Azure AD application and then request an access token.</span></span> <span data-ttu-id="5fa30-111">Yalnızca uygulama kullanılarak alınan erişim belirteçleri veya uygulama + kullanıcı kimlik doğrulaması Iş Ortağı Merkezi ile kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-111">Access tokens obtained using app only or app + user authentication can be used with the Partner Center.</span></span> <span data-ttu-id="5fa30-112">Ancak, dikkate alınmaması gereken iki önemli öğe vardır</span><span class="sxs-lookup"><span data-stu-id="5fa30-112">However, there are two important items that need to be considered</span></span>

- <span data-ttu-id="5fa30-113">Uygulama + kullanıcı kimlik doğrulaması kullanarak Iş Ortağı Merkezi API 'sine erişirken Multi-Factor Authentication 'ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-113">Use multi-factor authentication when accessing the Partner Center API using app + user authentication.</span></span> <span data-ttu-id="5fa30-114">Bu değişiklik hakkında daha fazla bilgi için bkz. [güvenli uygulama modelini etkinleştirme](enable-secure-app-model.md).</span><span class="sxs-lookup"><span data-stu-id="5fa30-114">For more information regarding this change, see [Enable secure application model](enable-secure-app-model.md).</span></span>

- <span data-ttu-id="5fa30-115">Tüm işlemler Iş Ortağı Merkezi API 'Sı yalnızca uygulama kimlik doğrulamasını desteklemez.</span><span class="sxs-lookup"><span data-stu-id="5fa30-115">Not all of the operations the Partner Center API support app only authentication.</span></span> <span data-ttu-id="5fa30-116">Uygulama + kullanıcı kimlik doğrulamasını kullanmanız gereken bazı senaryolar vardır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-116">There are certain scenarios where you'll be required to use app + user authentication.</span></span> <span data-ttu-id="5fa30-117">Her makaledeki *Önkoşul* başlığı altında, [](scenarios.md)uygulama yalnızca kimlik doğrulaması, uygulama + kullanıcı kimlik doğrulaması veya her ikisinin de desteklenip desteklenmediğini belirten belgeleri bulacaksınız.</span><span class="sxs-lookup"><span data-stu-id="5fa30-117">Under the *Prerequisites* heading on each [article](scenarios.md), you'll find documentation that states whether app only authentication, app + user authentication, or both are supported.</span></span>

## <a name="initial-setup"></a><span data-ttu-id="5fa30-118">İlk kurulum</span><span class="sxs-lookup"><span data-stu-id="5fa30-118">Initial setup</span></span>

1. <span data-ttu-id="5fa30-119">Başlamak için hem birincil Iş Ortağı Merkezi hesabına hem de bir tümleştirme korumalı alanı Iş Ortağı Merkezi hesabına sahip olduğunuzdan emin olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-119">To begin, you need to make sure that you have both a primary Partner Center account, and an integration sandbox Partner Center account.</span></span> <span data-ttu-id="5fa30-120">Daha fazla bilgi için bkz. [API erişimi Için Iş Ortağı Merkezi hesapları ayarlama](set-up-api-access-in-partner-center.md).</span><span class="sxs-lookup"><span data-stu-id="5fa30-120">For more information, see [Set up Partner Center accounts for API access](set-up-api-access-in-partner-center.md).</span></span> <span data-ttu-id="5fa30-121">Hem birincil hesabınız hem de tümleştirme Sandbox hesabınız için Azure AAD uygulama kayıt KIMLIĞI ve gizli dizi (yalnızca uygulama kimliği için istemci parolası gereklidir) ' i unutmayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-121">Make note of the Azure AAD App registration ID and Secret (client secret is required for App only identification) for both your primary account and your integration sandbox account.</span></span>

2. <span data-ttu-id="5fa30-122">Azure portal Azure AD 'de oturum açın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-122">Sign in to Azure AD from the Azure portal.</span></span> <span data-ttu-id="5fa30-123">**Diğer uygulamalara yönelik izinler**' de, **Windows Azure Active Directory** izinleri **temsilci izinleri** olarak ayarlayın ve her iki dizine da oturum **açmış kullanıcı olarak erişin** ve **oturum açın ve kullanıcı profilini okuyun**.</span><span class="sxs-lookup"><span data-stu-id="5fa30-123">In **permissions to other applications**, set permissions for **Windows Azure Active Directory** to **Delegated Permissions**, and select both **Access the directory as the signed-in user** and **Sign in and read user profile**.</span></span>

3. <span data-ttu-id="5fa30-124">Azure portal, **uygulama ekleyin**.</span><span class="sxs-lookup"><span data-stu-id="5fa30-124">In the Azure portal, **Add application**.</span></span> <span data-ttu-id="5fa30-125">Microsoft Iş Ortağı Merkezi uygulaması olan "Microsoft Iş Ortağı Merkezi" ni arayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-125">Search for "Microsoft Partner Center", which is the Microsoft Partner Center application.</span></span> <span data-ttu-id="5fa30-126">**Temsilci izinleri** , **Iş Ortağı Merkezi API 'sine erişim** için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-126">Set the **Delegated Permissions** to **Access Partner Center API**.</span></span> <span data-ttu-id="5fa30-127">ABD hükümeti için Microsoft Bulut için Microsoft Bulut Almanya veya Iş Ortağı Merkezi için Iş Ortağı Merkezi kullanıyorsanız, bu adım zorunludur.</span><span class="sxs-lookup"><span data-stu-id="5fa30-127">If you are using Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government, this step is mandatory.</span></span> <span data-ttu-id="5fa30-128">Iş ortağı merkezi genel örneği kullanıyorsanız, bu adım isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-128">If you are using Partner Center global instance, this step is optional.</span></span> <span data-ttu-id="5fa30-129">CSP iş ortakları, iş ortağı merkezi genel örneği için bu adımı atlamak üzere Iş Ortağı Merkezi portalındaki uygulama yönetimi özelliğini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-129">CSP Partners can use the App Management feature in the Partner Center portal to bypass this step for Partner Center global instance.</span></span>

## <a name="app-only-authentication"></a><span data-ttu-id="5fa30-130">Yalnızca uygulama kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5fa30-130">App-only authentication</span></span>

<span data-ttu-id="5fa30-131">Iş Ortağı Merkezi REST API, .NET API, Java API 'SI veya PowerShell modülüne erişmek için yalnızca uygulama kimlik doğrulamasını kullanmak istiyorsanız, aşağıdaki yönergelerden yararlanarak bunu yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5fa30-131">If you would like to use app-only authentication to access the Partner Center REST API, .NET API, Java API, or PowerShell module then you can do so by leveraging the following instructions.</span></span>

## <a name="net-app-only-authentication"></a><span data-ttu-id="5fa30-132">.NET (yalnızca uygulama kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-132">.NET (app-only authentication)</span></span>

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

## <a name="java-app-only-authentication"></a><span data-ttu-id="5fa30-133">Java (yalnızca uygulama kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-133">Java (app-only authentication)</span></span>

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

## <a name="rest-app-only-authentication"></a><span data-ttu-id="5fa30-134">REST (yalnızca uygulama kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-134">REST (app-only authentication)</span></span>

### <a name="rest-request"></a><span data-ttu-id="5fa30-135">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5fa30-135">REST request</span></span>

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

### <a name="rest-response"></a><span data-ttu-id="5fa30-136">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5fa30-136">REST response</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Pragma: no-cache
Content-Type: application/json; charset=utf-8
Expires: -1
Content-Length: 1406

{"token_type":"Bearer","expires_in":"3600","ext_expires_in":"3600","expires_on":"1546469802","not_before":"1546465902","resource":"https://graph.windows.net","access_token":"value-has-been-removed"}
```

## <a name="app--user-authentication"></a><span data-ttu-id="5fa30-137">Uygulama + kullanıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5fa30-137">App + User authentication</span></span>

<span data-ttu-id="5fa30-138">Geçmişte, [kaynak sahibi parolası kimlik bilgileri verme](https://tools.ietf.org/html/rfc6749#section-4.3) , Iş ortağı merkezi REST API, .NET API, Java API 'Si veya PowerShell modülü ile kullanmak üzere bir erişim belirteci istemek için kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-138">Historically the [resource owner password credentials grant](https://tools.ietf.org/html/rfc6749#section-4.3) has been used to request an access token for use with the Partner Center REST API, .NET API, Java API, or PowerShell module.</span></span> <span data-ttu-id="5fa30-139">Bu yöntem, istemci tanımlayıcısı ve Kullanıcı kimlik bilgileri kullanarak Azure Active Directory bir erişim belirteci istemek için kullanılmıştır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-139">That method was used to request an access token from Azure Active Directory using a client identifier and user credentials.</span></span> <span data-ttu-id="5fa30-140">Ancak, uygulama + kullanıcı kimlik doğrulaması kullanılırken iş ortağı merkezi Multi-Factor Authentication gerektirdiğinden bu yaklaşım artık çalışmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-140">However, this approach will no longer work because Partner Center requires multi-factor authentication, when using app + user authentication.</span></span> <span data-ttu-id="5fa30-141">Microsoft bu gereksinimle uyum sağlamak için, Multi-Factor Authentication kullanarak bulut çözümü sağlayıcısı (CSP) iş ortakları ve Denetim Masası satıcıları (CPV) kimlik doğrulaması için güvenli, ölçeklenebilir bir çerçeve sunmuştur.</span><span class="sxs-lookup"><span data-stu-id="5fa30-141">To comply with this requirement Microsoft has introduced a secure, scalable framework for authenticating Cloud Solution Provider (CSP) partners and control panel vendors (CPV) using multi-factor authentication.</span></span> <span data-ttu-id="5fa30-142">Bu çerçeve güvenli uygulama modeli olarak bilinir ve bir onay işleminden ve bir erişim belirteci için yenileme belirteci kullanılarak bir istekten oluşur.</span><span class="sxs-lookup"><span data-stu-id="5fa30-142">This framework is known as the Secure Application Model, and it is composed of a consent process and a request for an access token using a refresh token.</span></span>

### <a name="partner-consent"></a><span data-ttu-id="5fa30-143">İş ortağı onayı</span><span class="sxs-lookup"><span data-stu-id="5fa30-143">Partner consent</span></span>

<span data-ttu-id="5fa30-144">İş ortağı onay süreci, iş ortağının Multi-Factor Authentication kullanarak kimlik doğrulaması yaptığı, uygulamaya yönelik onayları ve yenileme belirtecinin Azure Key Vault gibi güvenli bir depoda depolandığı etkileşimli bir işlemdir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-144">The partner consent process is an interactive process where the partner authenticates using multi-factor authentication, consents to the application, and a refresh token is stored in a secure repository such as Azure Key Vault.</span></span> <span data-ttu-id="5fa30-145">Bu işlem için bir tümleştirme amaçlarıyla adanmış bir hesap kullanılmasını öneririz.</span><span class="sxs-lookup"><span data-stu-id="5fa30-145">We recommend that a dedicated account for integration purposes be used for this process.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5fa30-146">İş ortağı onay sürecinde kullanılan hizmet hesabı için uygun Multi-Factor Authentication çözümü etkinleştirilmelidir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-146">The appropriate multi-factor authentication solution should be enabled for the service account used in the partner consent process.</span></span> <span data-ttu-id="5fa30-147">Değilse, sonuçta elde edilen yenileme belirteci güvenlik gereksinimleriyle uyumlu olmayacaktır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-147">If it isn't then the resulting refresh token will not be compliant with security requirements.</span></span>

### <a name="samples-for-app--user-authentication"></a><span data-ttu-id="5fa30-148">Uygulama + kullanıcı kimlik doğrulaması örnekleri</span><span class="sxs-lookup"><span data-stu-id="5fa30-148">Samples for App + User authentication</span></span>

<span data-ttu-id="5fa30-149">İş ortağı onay işlemi çeşitli yollarla gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-149">The partner consent process can be performed in a number of ways.</span></span> <span data-ttu-id="5fa30-150">İş ortaklarının her bir gerekli işlemin nasıl gerçekleştirileceğini anlamalarına yardımcı olmak için aşağıdaki örnekleri geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="5fa30-150">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="5fa30-151">Ortamınıza uygun çözümü uyguladığınızda, kodlama standartlarınız ve güvenlik ilkeleriniz ile uyumlu bir çözüm geliştirmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-151">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-appuser-authentication"></a><span data-ttu-id="5fa30-152">.NET (uygulama + kullanıcı kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-152">.NET (app+user authentication)</span></span>

<span data-ttu-id="5fa30-153">[İş ortağı onayı](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) örnek projesi, onayı yakalamak, yenileme belirteci istemek ve Azure Key Vault güvenli bir şekilde depolamak için ASP.NET kullanılarak geliştirilen bir Web sitesini nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-153">The [partner consent](https://github.com/Microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using ASP.NET to capture consent, request a refresh token, and securely store it in Azure Key Vault.</span></span> <span data-ttu-id="5fa30-154">Bu örnek için gerekli önkoşulları oluşturmak için aşağıdaki adımları gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-154">Perform the following steps to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="5fa30-155">Azure portal veya aşağıdaki PowerShell komutlarını kullanarak bir Azure Key Vault örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-155">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="5fa30-156">Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-156">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="5fa30-157">Kasa adı benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-157">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="5fa30-158">Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [hızlı başlangıç: Azure Key Vault Azure Portal veya hızlı başlangıç kullanarak gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-portal) [: PowerShell kullanarak Azure Key Vault bir gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="5fa30-158">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span> <span data-ttu-id="5fa30-159">Sonra bir gizli dizi ayarlayın ve alın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-159">Then set and retrieve a secret.</span></span>

2. <span data-ttu-id="5fa30-160">Azure portal veya aşağıdaki komutları kullanarak bir Azure AD uygulaması ve anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-160">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="5fa30-161">Aşağıdaki adımlarda kullanılabilecekleri için uygulama tanımlayıcısı ve gizli değerleri de göz önünde olduğunuzdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-161">Be sure to make note of the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="5fa30-162">Yeni Create Azure AD uygulamasına Azure portal veya aşağıdaki komutları kullanarak gizli dizi okuma izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-162">Grant the newly create Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="5fa30-163">Iş Ortağı Merkezi için yapılandırılmış bir Azure AD uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-163">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="5fa30-164">Bu adımı tamamlamak için aşağıdaki eylemleri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-164">Perform the following actions to complete this step.</span></span>

    - <span data-ttu-id="5fa30-165">Iş Ortağı Merkezi panosunun [uygulama yönetimi](https://partner.microsoft.com/pcv/apiintegration/appmanagement) özelliğine gidin</span><span class="sxs-lookup"><span data-stu-id="5fa30-165">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="5fa30-166">Yeni bir Azure AD uygulaması oluşturmak için *Yeni Web uygulaması Ekle* ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-166">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="5fa30-167">Aşağıdaki adımlarda kullanıldıkları için *uygulama kimliği*, \* hesap kimliği \* \* ve *anahtar* değerlerini belgelediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-167">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="5fa30-168">Visual Studio 'Yu veya aşağıdaki komutu kullanarak [Iş ortağı-orta DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) deposunu kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-168">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command.</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

6. <span data-ttu-id="5fa30-169">Dizinde bulunan *Partneronay* projesini açın `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="5fa30-169">Open the *PartnerConsent* project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="5fa30-170">[web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config) bulunan uygulama ayarlarını doldurun</span><span class="sxs-lookup"><span data-stu-id="5fa30-170">Populate the application settings found in the [web.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/PartnerConsent/Web.config)</span></span>

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
    > <span data-ttu-id="5fa30-171">Uygulama gizli dizileri gibi hassas bilgiler yapılandırma dosyalarında depolanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-171">Sensitive information such as application secrets should not be stored in configuration files.</span></span> <span data-ttu-id="5fa30-172">Bu örnek bir uygulama olduğu için burada gerçekleştirildi.</span><span class="sxs-lookup"><span data-stu-id="5fa30-172">It was done here because this is a sample application.</span></span> <span data-ttu-id="5fa30-173">Üretim uygulamanız sayesinde sertifika tabanlı kimlik doğrulaması kullanmanızı kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="5fa30-173">With your production application we strongly recommend that you use certificate-based authentication.</span></span> <span data-ttu-id="5fa30-174">Daha fazla bilgi için bkz. [uygulama kimlik doğrulaması Için sertifika kimlik bilgileri]( /azure/active-directory/develop/active-directory-certificate-credentials).</span><span class="sxs-lookup"><span data-stu-id="5fa30-174">For more information, see [Certificate credentials for application authentication]( /azure/active-directory/develop/active-directory-certificate-credentials).</span></span>

8. <span data-ttu-id="5fa30-175">Bu örnek projeyi çalıştırdığınızda sizden kimlik doğrulaması istenir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-175">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="5fa30-176">Kimlik doğrulaması başarılı olduktan sonra Azure AD 'den bir erişim belirteci istenir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-176">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="5fa30-177">Azure AD 'den döndürülen bilgiler, yapılandırılmış Azure Key Vault örneğinde depolanan yenileme belirtecini içerir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-177">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="java-appuser-authentication"></a><span data-ttu-id="5fa30-178">Java (uygulama + kullanıcı kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-178">Java (app+user authentication)</span></span>

<span data-ttu-id="5fa30-179">[İş ortağı onayı](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) örnek projesi, izin yakalamak, yenileme belirteci istemek ve Azure Key Vault 'da güvenli depo sağlamak için JSP kullanılarak geliştirilen bir Web sitesini nasıl kullanacağınızı gösterir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-179">The [partner consent](https://github.com/Microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model/keyvault) sample project demonstrates how to utilize a website developed using JSP to capture consent, request a refresh token, and secure store in Azure Key Vault.</span></span> <span data-ttu-id="5fa30-180">Bu örnek için gerekli önkoşulları oluşturmak için aşağıdakileri yapın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-180">Perform the following to create the required prerequisites for this sample.</span></span>

1. <span data-ttu-id="5fa30-181">Azure portal veya aşağıdaki PowerShell komutlarını kullanarak bir Azure Key Vault örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-181">Create an instance of Azure Key Vault using the Azure portal or the following PowerShell commands.</span></span> <span data-ttu-id="5fa30-182">Komutu yürütmeden önce parametre değerlerini uygun şekilde değiştirdiğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-182">Before executing the command, be sure to modify the parameter values accordingly.</span></span> <span data-ttu-id="5fa30-183">Kasa adı benzersiz olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-183">The vault name must be unique.</span></span>

    ```azurepowershell-interactive
    Login-AzureRmAccount

    # Create a new resource group
    New-AzureRmResourceGroup -Name ContosoResourceGroup -Location EastUS

    New-AzureRmKeyVault -Name 'Contoso-Vault' -ResourceGroupName 'ContosoResourceGroup' -Location 'East US'
    ```

    <span data-ttu-id="5fa30-184">Azure Key Vault oluşturma hakkında daha fazla bilgi için bkz. [hızlı başlangıç: Azure Key Vault Azure Portal veya hızlı başlangıç kullanarak gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-portal) [: PowerShell kullanarak Azure Key Vault bir gizli dizi ayarlama ve alma](/azure/key-vault/quick-create-powershell).</span><span class="sxs-lookup"><span data-stu-id="5fa30-184">For more information about creating an Azure Key Vault, see [Quickstart: Set and retrieve a secret from Azure Key Vault using the Azure portal](/azure/key-vault/quick-create-portal) or [Quickstart: Set and retrieve a secret from Azure Key Vault using PowerShell](/azure/key-vault/quick-create-powershell).</span></span>

2. <span data-ttu-id="5fa30-185">Azure portal veya aşağıdaki komutları kullanarak bir Azure AD uygulaması ve anahtarı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-185">Create an Azure AD Application and a key using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    Connect-AzureAD

    $SessionInfo = Get-AzureADCurrentSessionInfo

    $app = New-AzureADApplication -DisplayName 'My Vault Access App' -IdentifierUris 'https://$($SessionInfo.TenantDomain)/$((New-Guid).ToString())'
    $password = New-AzureADApplicationPasswordCredential -ObjectId $app.ObjectId

    Write-Host "ApplicationId       = $($app.AppId)"
    Write-Host "ApplicationSecret   = $($password.Value)"
    ```

    <span data-ttu-id="5fa30-186">Aşağıdaki adımlarda kullanılabilecekleri için uygulama tanımlayıcısı ve gizli değerleri belgelediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-186">Be sure to document the application identifier and secret values because they'll be used in the steps below.</span></span>

3. <span data-ttu-id="5fa30-187">Yeni oluşturulan Azure AD uygulamasına Azure portal veya aşağıdaki komutları kullanarak okuma gizli dizileri izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-187">Grant the newly created Azure AD application the read secrets permissions using the Azure portal or the following commands.</span></span>

    ```azurepowershell-interactive
    $app = Get-AzureADApplication -Filter {AppId -eq 'ENTER-APP-ID-HERE'}

    Set-AzureRmKeyVaultAccessPolicy -VaultName ContosoVault -ObjectId $app.ObjectId -PermissionsToSecrets get
    ```

4. <span data-ttu-id="5fa30-188">Iş Ortağı Merkezi için yapılandırılmış bir Azure AD uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-188">Create an Azure AD application that is configured for Partner Center.</span></span> <span data-ttu-id="5fa30-189">Bu adımı tamamlamak için aşağıdakileri gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-189">Perform the following to complete this step.</span></span>

    - <span data-ttu-id="5fa30-190">Iş Ortağı Merkezi panosunun [uygulama yönetimi](https://partner.microsoft.com/pcv/apiintegration/appmanagement) özelliğine gidin</span><span class="sxs-lookup"><span data-stu-id="5fa30-190">Browse to the [App management](https://partner.microsoft.com/pcv/apiintegration/appmanagement) feature of the Partner Center Dashboard</span></span>
    - <span data-ttu-id="5fa30-191">Yeni bir Azure AD uygulaması oluşturmak için *Yeni Web uygulaması Ekle* ' ye tıklayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-191">Click *Add new web app* to create a new Azure AD application.</span></span>

    <span data-ttu-id="5fa30-192">Aşağıdaki adımlarda kullanıldıkları için *uygulama kimliği*, \* hesap kimliği \* \* ve *anahtar* değerlerini belgelediğinizden emin olun.</span><span class="sxs-lookup"><span data-stu-id="5fa30-192">Be sure to document the *App ID*, \*Account ID\*\*, and *Key* values because they'll be used in the steps below.</span></span>

5. <span data-ttu-id="5fa30-193">Aşağıdaki komutu kullanarak [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="5fa30-193">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

6. <span data-ttu-id="5fa30-194">Dizinde bulunan *Partneronay* projesini açın `Partner-Center-Java-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="5fa30-194">Open the *PartnerConsent* project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

7. <span data-ttu-id="5fa30-195">[web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) dosyasında bulunan uygulama ayarlarını doldur</span><span class="sxs-lookup"><span data-stu-id="5fa30-195">Populate the application settings found in the [web.xml](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/partnerconsent/src/main/webapp/WEB-INF/web.xml) file</span></span>

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
    > <span data-ttu-id="5fa30-196">Uygulama gizli dizileri gibi hassas bilgiler, yapılandırma dosyalarında depolanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-196">Sensitive information such as application secrets should not be stored in configurations files.</span></span> <span data-ttu-id="5fa30-197">Bu örnek bir uygulama olduğu için burada gerçekleştirildi.</span><span class="sxs-lookup"><span data-stu-id="5fa30-197">It was done here because this is a sample application.</span></span> <span data-ttu-id="5fa30-198">Üretim uygulamanız sayesinde sertifika tabanlı kimlik doğrulaması kullanmanızı kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="5fa30-198">With your production application, we strongly recommend that you use certificate based authenticate.</span></span> <span data-ttu-id="5fa30-199">Daha fazla bilgi için bkz. [Key Vault sertifikası kimlik doğrulaması](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span><span class="sxs-lookup"><span data-stu-id="5fa30-199">For more information, see [Key Vault Certificate authentication](https://github.com/Azure-Samples/key-vault-java-certificate-authentication).</span></span>

8. <span data-ttu-id="5fa30-200">Bu örnek projeyi çalıştırdığınızda sizden kimlik doğrulaması istenir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-200">When you run this sample project, it will prompt you for authentication.</span></span> <span data-ttu-id="5fa30-201">Kimlik doğrulaması başarılı olduktan sonra Azure AD 'den bir erişim belirteci istenir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-201">After successfully authenticating, an access token is requested from Azure AD.</span></span> <span data-ttu-id="5fa30-202">Azure AD 'den döndürülen bilgiler, yapılandırılmış Azure Key Vault örneğinde depolanan yenileme belirtecini içerir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-202">The information returned from Azure AD includes a refresh token that is stored in the configured instance of Azure Key Vault.</span></span>

## <a name="cloud-solution-provider-authentication"></a><span data-ttu-id="5fa30-203">Bulut çözümü sağlayıcısı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5fa30-203">Cloud Solution Provider authentication</span></span>

<span data-ttu-id="5fa30-204">Bulut çözümü sağlayıcısı iş ortakları, [iş ortağı onay](#partner-consent) süreci aracılığıyla elde edilen yenileme belirtecini kullanabilir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-204">Cloud Solution Provider partners can use the refresh token obtained through the [partner consent](#partner-consent) process.</span></span>

### <a name="samples-for-cloud-solution-provider-authentication"></a><span data-ttu-id="5fa30-205">Bulut çözümü sağlayıcısı kimlik doğrulaması örnekleri</span><span class="sxs-lookup"><span data-stu-id="5fa30-205">Samples for Cloud Solution Provider authentication</span></span>

<span data-ttu-id="5fa30-206">İş ortaklarının her bir gerekli işlemin nasıl gerçekleştirileceğini anlamalarına yardımcı olmak için aşağıdaki örnekleri geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="5fa30-206">To help partners understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="5fa30-207">Ortamınıza uygun çözümü uyguladığınızda, kodlama standartlarınız ve güvenlik ilkeleriniz ile uyumlu bir çözüm geliştirmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-207">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-csp-authentication"></a><span data-ttu-id="5fa30-208">.NET (CSP kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-208">.NET (CSP authentication)</span></span>

1. <span data-ttu-id="5fa30-209">Daha önce yapmadıysanız, [iş ortağı onay işlemini](#partner-consent)gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-209">If you have not already done so, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="5fa30-210">Visual Studio 'Yu veya aşağıdaki komutu kullanarak [Iş ortağı-orta DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) deposunu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="5fa30-210">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="5fa30-211">`CSPApplication`Dizinde bulunan projeyi açın `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="5fa30-211">Open the `CSPApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="5fa30-212">[App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) dosyasında bulunan uygulama ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-212">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="5fa30-213">[Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) dosyasında bulunan **PartnerId** ve **CustomerID** değişkenleri için uygun değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-213">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CSPApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="5fa30-214">Bu örnek projeyi çalıştırdığınızda, iş ortağı onay işlemi sırasında elde edilen yenileme belirtecini edinir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-214">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="5fa30-215">Daha sonra, iş ortağının adına Iş Ortağı Merkezi SDK 'Sı ile etkileşime geçmek için bir erişim belirteci ister.</span><span class="sxs-lookup"><span data-stu-id="5fa30-215">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span> <span data-ttu-id="5fa30-216">Son olarak, belirtilen müşteri adına Microsoft Graph etkileşimde bulunmak için bir erişim belirteci ister.</span><span class="sxs-lookup"><span data-stu-id="5fa30-216">Finally, it requests an access token to interact with Microsoft Graph on behalf of the specified customer.</span></span>

## <a name="java-csp-authentication"></a><span data-ttu-id="5fa30-217">Java (CSP kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-217">Java (CSP authentication)</span></span>

1. <span data-ttu-id="5fa30-218">Şimdiye kadar yapmadıysanız, [iş ortağı onay işlemini](#partner-consent)gerçekleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-218">If you have not done so already, perform the [partner consent process](#partner-consent).</span></span>

2. <span data-ttu-id="5fa30-219">Visual Studio 'Yu veya aşağıdaki komutu kullanarak [Iş ortağı-merkezi-Java-örnekleri](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="5fa30-219">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="5fa30-220">`cspsample`Dizinde bulunan projeyi açın `Partner-Center-Java-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="5fa30-220">Open the `cspsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="5fa30-221">[Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) dosyasında bulunan uygulama ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-221">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cspsample/src/main/resources/application.properties) file.</span></span>

     ```java
    azuread.authority=https://login.microsoftonline.com
    keyvault.baseurl=
    keyvault.clientId=
    keyvault.clientSecret=
    partnercenter.accountId=
    partnercenter.clientId=
    partnercenter.clientSecret=
    ```

5. <span data-ttu-id="5fa30-222">Bu örnek projeyi çalıştırdığınızda, iş ortağı onay işlemi sırasında elde edilen yenileme belirtecini edinir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-222">When you run this sample project, it obtains the refresh token obtained during the partner consent process.</span></span> <span data-ttu-id="5fa30-223">Daha sonra, iş ortağının adına Iş Ortağı Merkezi SDK 'Sı ile etkileşime geçmek için bir erişim belirteci ister.</span><span class="sxs-lookup"><span data-stu-id="5fa30-223">Then, it requests an access token to interact with the Partner Center SDK on the partner's behalf.</span></span>

6. <span data-ttu-id="5fa30-224">İsteğe bağlı-müşteri adına Azure Resource Manager ve Microsoft Graph nasıl etkileşim kuracağınızı görmek istiyorsanız *RunAzureTask* ve *rungraphtask* işlev çağrılarının açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-224">Optional - uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>

## <a name="control-panel-provider-authentication"></a><span data-ttu-id="5fa30-225">Denetim Masası sağlayıcı kimlik doğrulaması</span><span class="sxs-lookup"><span data-stu-id="5fa30-225">Control Panel Provider authentication</span></span>

<span data-ttu-id="5fa30-226">Denetim Masası satıcılarının, [iş ortağının izin](#partner-consent) sürecini gerçekleştirmesini destekleyen her bir iş ortağı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-226">Control panel vendors need to have each partner they support perform the [partner consent](#partner-consent) process.</span></span> <span data-ttu-id="5fa30-227">Bu işlem tamamlandıktan sonra, Iş Ortağı Merkezi REST API ve .NET API 'sine erişmek için bu işlem aracılığıyla elde edilen yenileme belirteci kullanılır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-227">Once that is completed the refresh token obtained through that process is used to access the Partner Center REST API and .NET API.</span></span>

### <a name="samples-for-cloud-panel-provider-authentication"></a><span data-ttu-id="5fa30-228">Bulut paneli sağlayıcı kimlik doğrulaması örnekleri</span><span class="sxs-lookup"><span data-stu-id="5fa30-228">Samples for Cloud Panel Provider authentication</span></span>

<span data-ttu-id="5fa30-229">Denetim Masası satıcılarının her bir gerekli işlemin nasıl gerçekleştirileceğini anlamalarına yardımcı olmak için aşağıdaki örnekleri geliştirdik.</span><span class="sxs-lookup"><span data-stu-id="5fa30-229">To help control panel vendors understand how to perform each required operation, we have developed the following samples.</span></span> <span data-ttu-id="5fa30-230">Ortamınıza uygun çözümü uyguladığınızda, kodlama standartlarınız ve güvenlik ilkeleriniz ile uyumlu bir çözüm geliştirmeniz önemlidir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-230">When you implement the appropriate solution in your environment, it is important that you develop a solution that is complaint with your coding standards and security policies.</span></span>

## <a name="net-cpv-authentication"></a><span data-ttu-id="5fa30-231">.NET (CPV kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-231">.NET (CPV authentication)</span></span>

1. <span data-ttu-id="5fa30-232">Uygun izin sağlamak için bulut çözümü sağlayıcısı iş ortakları için bir işlem geliştirin ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-232">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="5fa30-233">Daha fazla bilgi için bkz. [iş ortağı onayı](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="5fa30-233">For more information an example, see [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5fa30-234">Bir bulut çözümü sağlayıcısı ortağından Kullanıcı kimlik bilgileri depolanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-234">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="5fa30-235">İş ortağı onay süreci aracılığıyla elde edilen yenileme belirteci, herhangi bir Microsoft API 'siyle etkileşimde bulunmak üzere erişim belirteçleri istemek için depolanmalıdır ve kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-235">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="5fa30-236">Visual Studio 'Yu veya aşağıdaki komutu kullanarak [Iş ortağı-orta DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) deposunu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="5fa30-236">Clone the [Partner-Center-DotNet-Samples](https://github.com/Microsoft/Partner-Center-DotNet-Samples) repository using Visual Studio or the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-DotNet-Samples.git
    ```

3. <span data-ttu-id="5fa30-237">`CPVApplication`Dizinde bulunan projeyi açın `Partner-Center-DotNet-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="5fa30-237">Open the `CPVApplication` project found in the `Partner-Center-DotNet-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="5fa30-238">[App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) dosyasında bulunan uygulama ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-238">Update the application settings found in the [App.config](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/App.config) file.</span></span>

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

5. <span data-ttu-id="5fa30-239">[Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) dosyasında bulunan **PartnerId** ve **CustomerID** değişkenleri için uygun değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-239">Set the appropriate values for the **PartnerId** and **CustomerId** variables found in the [Program.cs](https://github.com/Microsoft/Partner-Center-DotNet-Samples/blob/master/secure-app-model/keyvault/CPVApplication/Program.cs) file.</span></span>

    ```csharp
    // The following properties indicate which partner and customer context the calls are going to be made.
    string PartnerId = "<Partner tenant id>";
    string CustomerId = "<Customer tenant id>";
    ```

6. <span data-ttu-id="5fa30-240">Bu örnek projeyi çalıştırdığınızda, belirtilen iş ortağı için yenileme belirtecini alır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-240">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="5fa30-241">Daha sonra, iş ortağı merkezi ve Azure AD grafiğine erişmek için bir erişim belirteci ister.</span><span class="sxs-lookup"><span data-stu-id="5fa30-241">Then, it requests an access token to access Partner Center and Azure AD Graph on behalf of the partner.</span></span> <span data-ttu-id="5fa30-242">Yaptığı sonraki görev, müşteri kiracısına izin verdiği silme ve iznin oluşturulma işlemidir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-242">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="5fa30-243">Denetim Masası satıcısı ve müşteri arasında ilişki olmadığından, bu izinlerin Iş Ortağı Merkezi API 'SI kullanılarak eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-243">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="5fa30-244">Aşağıdaki örnek bunun nasıl yapılacağını göstermektedir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-244">The following example shows how to accomplish that.</span></span>

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

<span data-ttu-id="5fa30-245">Bu izinler kurulduktan sonra örnek, müşteri adına Azure AD Graph kullanarak işlemleri gerçekleştirir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-245">After these permissions have been established, the sample performs operations using Azure AD Graph on behalf of the customer.</span></span>

## <a name="java-cpv-authentication"></a><span data-ttu-id="5fa30-246">Java (CPV kimlik doğrulaması)</span><span class="sxs-lookup"><span data-stu-id="5fa30-246">Java (CPV authentication)</span></span>

1. <span data-ttu-id="5fa30-247">Uygun izin sağlamak için bulut çözümü sağlayıcısı iş ortakları için bir işlem geliştirin ve dağıtın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-247">Develop and deploy a process for Cloud Solution Provider partners to provide the appropriate consent.</span></span> <span data-ttu-id="5fa30-248">Daha fazla bilgi ve bir örnek için bkz. [iş ortağı onayı](#partner-consent).</span><span class="sxs-lookup"><span data-stu-id="5fa30-248">For more information and an example, see the [partner consent](#partner-consent).</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="5fa30-249">Bir bulut çözümü sağlayıcısı ortağından Kullanıcı kimlik bilgileri depolanmamalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-249">User credentials from a Cloud Solution Provider partner should not be stored.</span></span> <span data-ttu-id="5fa30-250">İş ortağı onay süreci aracılığıyla elde edilen yenileme belirteci, herhangi bir Microsoft API 'siyle etkileşimde bulunmak üzere erişim belirteçleri istemek için depolanmalıdır ve kullanılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-250">The refresh token obtained through the partner consent process should be stored and used to request access tokens for interacting with any Microsoft API.</span></span>

2. <span data-ttu-id="5fa30-251">Aşağıdaki komutu kullanarak [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) deposunu kopyalayın</span><span class="sxs-lookup"><span data-stu-id="5fa30-251">Clone the [Partner-Center-Java-Samples](https://github.com/Microsoft/Partner-Center-Java-Samples) repository using the following command</span></span>

    ```bash
    git clone https://github.com/Microsoft/Partner-Center-Java-Samples.git
    ```

3. <span data-ttu-id="5fa30-252">`cpvsample`Dizinde bulunan projeyi açın `Partner-Center-Java-Samples\secure-app-model\keyvault` .</span><span class="sxs-lookup"><span data-stu-id="5fa30-252">Open the `cpvsample` project found in the `Partner-Center-Java-Samples\secure-app-model\keyvault` directory.</span></span>

4. <span data-ttu-id="5fa30-253">[Application. Properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) dosyasında bulunan uygulama ayarlarını güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="5fa30-253">Update the application settings found in the [application.properties](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/resources/application.properties) file.</span></span>

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

    <span data-ttu-id="5fa30-254">İçin değeri `partnercenter.displayName` Market uygulamanızın görünen adı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-254">The value for the `partnercenter.displayName` should be the display name of your marketplace application.</span></span>

5. <span data-ttu-id="5fa30-255">[Program. Java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) dosyasında bulunan **PartnerId** ve **CustomerID** değişkenleri için uygun değerleri ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-255">Set the appropriate values for the **partnerId** and **customerId** variables found in the [Program.java](https://github.com/Microsoft/Partner-Center-Java-Samples/blob/master/secure-app-model/keyvault/cpvsample/src/main/java/com/microsoft/store/samples/secureappmodel/cpvsample/Program.java) file.</span></span>

    ```java
    partnerId = "SPECIFY-THE-PARTNER-TENANT-ID-HERE";
    customerId = "SPECIFY-THE-CUSTOMER-TENANT-ID-HERE";
    ```

6. <span data-ttu-id="5fa30-256">Bu örnek projeyi çalıştırdığınızda, belirtilen iş ortağı için yenileme belirtecini alır.</span><span class="sxs-lookup"><span data-stu-id="5fa30-256">When you run this sample project, it obtains the refresh token for the specified partner.</span></span> <span data-ttu-id="5fa30-257">Sonra iş ortağı adına iş ortağı merkezi 'ne erişmek için bir erişim belirteci ister.</span><span class="sxs-lookup"><span data-stu-id="5fa30-257">Then, it requests an access token to access Partner Center on behalf of the partner.</span></span> <span data-ttu-id="5fa30-258">Yaptığı sonraki görev, müşteri kiracısına izin verdiği silme ve iznin oluşturulma işlemidir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-258">The next task it performs is the deletion and creation of permission grants into the customer tenant.</span></span> <span data-ttu-id="5fa30-259">Denetim Masası satıcısı ve müşteri arasında ilişki olmadığından, bu izinlerin Iş Ortağı Merkezi API 'SI kullanılarak eklenmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-259">Since there's no relationship between the control panel vendor and the customer, these permissions need to be added using the Partner Center API.</span></span> <span data-ttu-id="5fa30-260">Aşağıdaki örnek, izinlerin nasıl verildiğini gösterir.</span><span class="sxs-lookup"><span data-stu-id="5fa30-260">The following example shows how to grant the permissions.</span></span>

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

<span data-ttu-id="5fa30-261">Azure Resource Manager ve Microsoft Graph müşteri adına nasıl etkileşim kuracağınızı görmek istiyorsanız, *RunAzureTask* ve *rungraphtask* işlev çağrılarının açıklamasını kaldırın.</span><span class="sxs-lookup"><span data-stu-id="5fa30-261">Uncomment the *RunAzureTask* and *RunGraphTask* function calls if you want to see how to interact with Azure Resource Manager and Microsoft Graph on behalf of the customer.</span></span>
