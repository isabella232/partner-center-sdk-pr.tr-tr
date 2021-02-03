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
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="ceba5-103">Güvenlik Uygulama Modeli çerçevesini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ceba5-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="ceba5-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="ceba5-104">**Applies to:**</span></span>

- <span data-ttu-id="ceba5-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ceba5-105">Partner Center</span></span>

<span data-ttu-id="ceba5-106">Microsoft, Microsoft Azure Multi-Factor Authentication (MFA) mimarisi aracılığıyla bulut çözümü sağlayıcısı (CSP) iş ortaklarının ve Denetim Masası satıcılarının (CPV) kimlik doğrulaması için güvenli ve ölçeklenebilir bir çerçeve sunuyor.</span><span class="sxs-lookup"><span data-stu-id="ceba5-106">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure multi-factor authentication (MFA) architecture.</span></span>

<span data-ttu-id="ceba5-107">Iş Ortağı Merkezi API Tümleştirmesi çağrıları için güvenliği yükseltmek üzere yeni modeli kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ceba5-107">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="ceba5-108">Bu, tüm taraflara (Microsoft, CSP iş ortakları ve CPVs 'ler dahil), altyapı ve müşteri verilerini güvenlik risklerinden korumalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="ceba5-108">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="ceba5-109">Kapsam</span><span class="sxs-lookup"><span data-stu-id="ceba5-109">Scope</span></span>

<span data-ttu-id="ceba5-110">Bu makalede aşağıdaki aktörlerin kaygıları vardır:</span><span class="sxs-lookup"><span data-stu-id="ceba5-110">This article concerns the following actors:</span></span>

- <span data-ttu-id="ceba5-111">CPV’ler</span><span class="sxs-lookup"><span data-stu-id="ceba5-111">CPVs</span></span>
  - <span data-ttu-id="ceba5-112">CPV, CSP iş ortakları tarafından İş Ortağı Merkezi API’leriyle tümleştirilmek üzere kullanılacak uygulamalar geliştiren bağımsız yazılım satıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="ceba5-112">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="ceba5-113">CPV, İş Ortağı Merkezi panosuna veya API’lerine doğrudan erişimi olan bir CSP iş ortağı değildir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-113">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="ceba5-114">CSP dolaylı sağlayıcıları ve uygulama KIMLIĞI + Kullanıcı kimlik doğrulaması kullanan CSP Direct iş ortakları ve doğrudan Iş Ortağı Merkezi API 'Leri ile tümleştirin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-114">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="ceba5-115">Güvenlik gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="ceba5-115">Security requirements</span></span>

<span data-ttu-id="ceba5-116">Güvenlik gereksinimleriyle ilgili ayrıntılar için bkz. [Iş ortağı güvenlik gereksinimleri](/partner-center/partner-security-requirements).</span><span class="sxs-lookup"><span data-stu-id="ceba5-116">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="ceba5-117">Güvenli uygulama modeli</span><span class="sxs-lookup"><span data-stu-id="ceba5-117">Secure Application Model</span></span>

<span data-ttu-id="ceba5-118">Market uygulamalarının Microsoft API 'Leri çağırmak için CSP iş ortağı ayrıcalıklarının kimliğine bürünmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-118">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="ceba5-119">Bu hassas uygulamalardaki güvenlik saldırıları müşteri verilerinin tehlikeye çıkmasına neden olabilir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-119">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="ceba5-120">Yeni kimlik doğrulama çerçevesiyle ilgili genel bilgiler ve Ayrıntılar için [güvenli uygulama modeli çerçevesi](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) belgesini indirin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-120">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="ceba5-121">Bu belgede, Market uygulamalarının güvenliği tehlikeye atmayı ve güçlü hale getirmek için ilkeler ve en iyi uygulamalar ele alınmaktadır.</span><span class="sxs-lookup"><span data-stu-id="ceba5-121">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="ceba5-122">Örnekler</span><span class="sxs-lookup"><span data-stu-id="ceba5-122">Samples</span></span>

<span data-ttu-id="ceba5-123">Aşağıdaki genel bakış belgeleri ve örnek kod, iş ortaklarının güvenli uygulama modeli çerçevesini nasıl uygulayabileceğini açıklamaktadır:</span><span class="sxs-lookup"><span data-stu-id="ceba5-123">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="ceba5-124">CPV genel bakış belgesi</span><span class="sxs-lookup"><span data-stu-id="ceba5-124">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="ceba5-125">CSP genel bakış belgesi</span><span class="sxs-lookup"><span data-stu-id="ceba5-125">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="ceba5-126">.NET örnekleri</span><span class="sxs-lookup"><span data-stu-id="ceba5-126">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="ceba5-127">Java örnekleri</span><span class="sxs-lookup"><span data-stu-id="ceba5-127">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="ceba5-128">REST yönergeleri ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="ceba5-128">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="ceba5-129">PowerShell yönergeleri ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="ceba5-129">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="ceba5-130">REST</span><span class="sxs-lookup"><span data-stu-id="ceba5-130">REST</span></span>

<span data-ttu-id="ceba5-131">Örnek kodla güvenli uygulama modeli çerçevesiyle REST çağrıları yapmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="ceba5-131">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="ceba5-132">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ceba5-132">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="ceba5-133">Yetkilendirme kodu al</span><span class="sxs-lookup"><span data-stu-id="ceba5-133">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="ceba5-134">Yenileme belirteci al</span><span class="sxs-lookup"><span data-stu-id="ceba5-134">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="ceba5-135">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="ceba5-135">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="ceba5-136">İş Ortağı Merkezi API çağrısı yapma</span><span class="sxs-lookup"><span data-stu-id="ceba5-136">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="ceba5-137">Bir yetkilendirme kodu ve yenileme belirteci almak için Iş Ortağı Merkezi PowerShell modülünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ceba5-137">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="ceba5-138">Adım 2 ve 3 ' ün yerine bu seçeneği belirleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ceba5-138">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="ceba5-139">Daha fazla bilgi için [PowerShell bölümüne ve örneklerine](#powershell)bakın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-139">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="ceba5-140">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="ceba5-140">Create a web app</span></span>

<span data-ttu-id="ceba5-141">REST çağrıları yapmadan önce Iş Ortağı Merkezi 'nde bir Web uygulaması oluşturmanız ve kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-141">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="ceba5-142">[Azure portalında](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-142">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="ceba5-143">Azure Active Directory (Azure AD) uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="ceba5-143">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="ceba5-144">*Uygulamanızın gereksinimlerine bağlı olarak* aşağıdaki kaynaklara atanmış uygulama izinleri verin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-144">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="ceba5-145">Gerekirse, uygulama kaynakları için daha fazla temsilci izinleri ekleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ceba5-145">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="ceba5-146">**Microsoft Iş Ortağı Merkezi** (Bazı kiracılar bunu **samplebecapp** olarak gösterir)</span><span class="sxs-lookup"><span data-stu-id="ceba5-146">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="ceba5-147">**Azure Yönetim API 'leri** (Azure API 'lerini çağırmayı planlıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="ceba5-147">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="ceba5-148">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="ceba5-148">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="ceba5-149">Uygulamanızın giriş URL 'sinin canlı bir Web uygulamasının çalıştığı bir uç noktaya ayarlandığından emin olun.</span><span class="sxs-lookup"><span data-stu-id="ceba5-149">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="ceba5-150">Bu uygulamanın Azure AD oturum açma çağrısından [Yetkilendirme kodunu](#get-authorization-code) kabul etmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-150">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="ceba5-151">Örneğin, [aşağıdaki bölümdeki](#get-authorization-code)örnek kodda, Web uygulaması ' de çalışır `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="ceba5-151">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="ceba5-152">Web uygulamanızın Azure AD 'deki ayarlarından aşağıdaki bilgilere göz atalım:</span><span class="sxs-lookup"><span data-stu-id="ceba5-152">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="ceba5-153">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="ceba5-153">Application ID</span></span>
   - <span data-ttu-id="ceba5-154">Uygulama gizli dizisi</span><span class="sxs-lookup"><span data-stu-id="ceba5-154">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="ceba5-155">[Uygulama gizli anahtarı olarak bir sertifika kullanmanız](/azure/active-directory/develop/active-directory-certificate-credentials)önerilir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-155">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="ceba5-156">Ancak, Azure portal bir uygulama anahtarı da oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ceba5-156">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="ceba5-157">[Aşağıdaki bölümdeki](#get-authorization-code) örnek kod bir uygulama anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="ceba5-157">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="ceba5-158">Yetkilendirme kodunu alma</span><span class="sxs-lookup"><span data-stu-id="ceba5-158">Get authorization code</span></span>

<span data-ttu-id="ceba5-159">Web uygulamanızın Azure AD oturum açma çağrısından kabul etmesi için bir yetkilendirme kodu almanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ceba5-159">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="ceba5-160">Şu URL 'de Azure AD 'de oturum açın: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="ceba5-160">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="ceba5-161">Iş Ortağı Merkezi API çağrılarını (bir Yönetim Aracısı veya satış aracısı hesabı gibi) yapacağınız kullanıcı hesabıyla oturum açmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-161">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="ceba5-162">**Uygulama kimliğini** Azure AD uygulama KIMLIĞINIZ (GUID) ile değiştirin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-162">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="ceba5-163">İstendiğinde, MFA yapılandırılmış kullanıcı hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-163">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="ceba5-164">İstendiğinde, oturum açma bilgilerinizi doğrulamak için ek MFA bilgilerini (telefon numarası veya e-posta adresi) girin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-164">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="ceba5-165">Oturum açtıktan sonra tarayıcı, yetkilendirme kodunuzla Web uygulaması uç noktanıza yapılan çağrıyı yeniden yönlendirir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-165">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="ceba5-166">Örneğin, aşağıdaki örnek kod öğesine yeniden yönlendirir `https://localhost:44395/` .</span><span class="sxs-lookup"><span data-stu-id="ceba5-166">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="ceba5-167">Yetkilendirme kodu çağrısı izleme</span><span class="sxs-lookup"><span data-stu-id="ceba5-167">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="ceba5-168">Yenileme belirtecini al</span><span class="sxs-lookup"><span data-stu-id="ceba5-168">Get refresh token</span></span>

<span data-ttu-id="ceba5-169">Daha sonra bir yenileme belirteci almak için yetkilendirme kodunuzu kullanmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="ceba5-169">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="ceba5-170">Azure AD oturum açma uç noktasına yetkilendirme kodu ile bir POST çağrısı yapın `https://login.microsoftonline.com/CSPTenantID/oauth2/token` .</span><span class="sxs-lookup"><span data-stu-id="ceba5-170">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="ceba5-171">Bir örnek için, aşağıdaki [örnek çağrıya](#sample-refresh-call)bakın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-171">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="ceba5-172">Döndürülen yenileme belirtecini unutmayın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-172">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="ceba5-173">Yenileme belirtecini Azure Key Vault olarak depolayın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-173">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="ceba5-174">Daha fazla bilgi için [Key Vault API belgelerine](/rest/api/keyvault/)bakın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-174">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ceba5-175">Yenileme belirteci Key Vault’ta [gizli dizi olarak depolanmalıdır](/rest/api/keyvault/setsecret/setsecret).</span><span class="sxs-lookup"><span data-stu-id="ceba5-175">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="ceba5-176">Örnek yenileme çağrısı</span><span class="sxs-lookup"><span data-stu-id="ceba5-176">Sample refresh call</span></span>

<span data-ttu-id="ceba5-177">Yer tutucu isteği:</span><span class="sxs-lookup"><span data-stu-id="ceba5-177">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="ceba5-178">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="ceba5-178">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="ceba5-179">Yer tutucu yanıtı:</span><span class="sxs-lookup"><span data-stu-id="ceba5-179">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="ceba5-180">Yanıt gövdesi:</span><span class="sxs-lookup"><span data-stu-id="ceba5-180">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="ceba5-181">Erişim belirteci al</span><span class="sxs-lookup"><span data-stu-id="ceba5-181">Get access token</span></span>

<span data-ttu-id="ceba5-182">Iş Ortağı Merkezi API 'Lerine çağrı yapmadan önce bir erişim belirteci almalısınız.</span><span class="sxs-lookup"><span data-stu-id="ceba5-182">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="ceba5-183">Erişim belirtecinin genellikle çok sınırlı bir yaşam süresi (örneğin, bir saatten kısa) olması nedeniyle, bir erişim belirteci almak için bir yenileme belirteci kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-183">You must use a refresh token to obtain an access token because access token generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="ceba5-184">Yer tutucu isteği:</span><span class="sxs-lookup"><span data-stu-id="ceba5-184">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="ceba5-185">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="ceba5-185">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="ceba5-186">Yer tutucu yanıtı:</span><span class="sxs-lookup"><span data-stu-id="ceba5-186">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="ceba5-187">Yanıt gövdesi:</span><span class="sxs-lookup"><span data-stu-id="ceba5-187">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="ceba5-188">Iş Ortağı Merkezi API çağrıları yapma</span><span class="sxs-lookup"><span data-stu-id="ceba5-188">Make Partner Center API calls</span></span>

<span data-ttu-id="ceba5-189">Iş Ortağı Merkezi API 'Lerini çağırmak için erişim belirtecinizi kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-189">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="ceba5-190">Aşağıdaki örnek çağrıya bakın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-190">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="ceba5-191">Örnek Iş Ortağı Merkezi API çağrısı</span><span class="sxs-lookup"><span data-stu-id="ceba5-191">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="ceba5-192">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ceba5-192">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="ceba5-193">[Iş Ortağı Merkezi PowerShell modülünü](https://www.powershellgallery.com/packages/PartnerCenter) , bir erişim belirteci için bir yetkilendirme kodu alışverişi yapmak üzere gerekli altyapıyı azaltmak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="ceba5-193">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="ceba5-194">Bu yöntem, [Iş ortağı MERKEZI Rest çağrıları](#rest)yapmak için isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="ceba5-194">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="ceba5-195">Bu işlem hakkında daha fazla bilgi için bkz. [App model PowerShell Için güvenli uygulama](/powershell/partnercenter/secure-app-model) .</span><span class="sxs-lookup"><span data-stu-id="ceba5-195">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="ceba5-196">Azure AD ve Iş Ortağı Merkezi PowerShell modüllerini yükler.</span><span class="sxs-lookup"><span data-stu-id="ceba5-196">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="ceba5-197">Onay işlemini gerçekleştirmek ve gerekli yenileme belirtecini yakalamak için **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-197">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="ceba5-198">**Web/API** türünde BIR Azure AD uygulaması kullanıldığından, **ServicePrincipal** parametresi **New-partneraccesstoken** komutuyla birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="ceba5-198">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="ceba5-199">Bu tür bir uygulama, erişim belirteci isteğine bir istemci tanımlayıcısı ve gizli anahtar eklenmesini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-199">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="ceba5-200">**Get-Credential** komutu çağrıldığında, bir Kullanıcı adı ve parola girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-200">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="ceba5-201">Uygulama tanımlayıcısını Kullanıcı adı olarak girin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-201">Enter the application identifier as the username.</span></span> <span data-ttu-id="ceba5-202">Parola olarak uygulama gizli anahtarını girin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-202">Enter the application secret as the password.</span></span> <span data-ttu-id="ceba5-203">**New-PartnerAccessToken** komutu çağrıldığında, kimlik bilgilerini yeniden girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-203">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="ceba5-204">Kullanmakta olduğunuz hizmet hesabının kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="ceba5-204">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="ceba5-205">Bu hizmet hesabı, uygun izinlere sahip bir iş ortağı hesabı olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="ceba5-205">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="ceba5-206">Yenileme belirteci değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="ceba5-206">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="ceba5-207">Yenileme belirteci değerini, Azure Key Vault gibi güvenli bir depoda depolamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="ceba5-207">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="ceba5-208">PowerShell ile güvenli uygulama modülünü kullanma hakkında daha fazla bilgi için bkz. [Multi-Factor Authentication](/powershell/partnercenter/multi-factor-auth) makalesi.</span><span class="sxs-lookup"><span data-stu-id="ceba5-208">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
