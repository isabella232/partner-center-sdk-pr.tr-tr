---
title: Güvenli uygulama modelini etkinleştirme
description: Uygulamalarınızı İş Ortağı Merkezi denetim masası uygulamalarının güvenliğini sağlama.
ms.date: 01/20/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-csp
author: aarzh-AaronZhang
ms.author: v-aarzh
ms.openlocfilehash: 19a1c39576a4f897df2d1205e3501839f6580831
ms.sourcegitcommit: e0077b2724d128ab20cb05696e5e5b1cde8e5214
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/07/2021
ms.locfileid: "113481676"
---
# <a name="enabling-the-secure-application-model-framework"></a><span data-ttu-id="7b7ae-103">Güvenlik Uygulama Modeli çerçevesini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="7b7ae-103">Enabling the Secure Application Model framework</span></span>

<span data-ttu-id="7b7ae-104">Microsoft, Microsoft Azure Active Directory Multi-Factor Authentication (MFA) mimarisi aracılığıyla bulut çözümü sağlayıcısı (CSP) iş ortaklarının ve denetim masası satıcılarının (CPV) kimliklerini doğrulamaya Microsoft Azure Active Directory güvenli ve ölçeklenebilir bir çerçeve sunmaktadır.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-104">Microsoft is introducing a secure, scalable framework for authenticating cloud solution provider (CSP) partners and control panel vendors (CPV) through the Microsoft Azure Active Directory Multi-Factor Authentication (MFA) architecture.</span></span>

<span data-ttu-id="7b7ae-105">Yeni modeli kullanarak API tümleştirme çağrılarına İş Ortağı Merkezi yükseltebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-105">You can use the new model to elevate security for Partner Center API integration calls.</span></span> <span data-ttu-id="7b7ae-106">Bu, tüm tarafların (Microsoft, CSP iş ortakları ve CPV'ler dahil) altyapılarını ve müşteri verilerini güvenlik risklerinden korumalarına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-106">This will help all parties (including Microsoft, CSP partners, and CPVs) to protect their infrastructure and customer data from security risks.</span></span>

## <a name="scope"></a><span data-ttu-id="7b7ae-107">Kapsam</span><span class="sxs-lookup"><span data-stu-id="7b7ae-107">Scope</span></span>

<span data-ttu-id="7b7ae-108">Bu makale aşağıdaki aktörlerle ilgilidir:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-108">This article concerns the following actors:</span></span>

- <span data-ttu-id="7b7ae-109">CPV’ler</span><span class="sxs-lookup"><span data-stu-id="7b7ae-109">CPVs</span></span>
  - <span data-ttu-id="7b7ae-110">CPV, CSP iş ortakları tarafından İş Ortağı Merkezi API’leriyle tümleştirilmek üzere kullanılacak uygulamalar geliştiren bağımsız yazılım satıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-110">A CPV is an independent software vendor that develops apps for use by CSP partners to integrate with Partner Center APIs.</span></span>
  - <span data-ttu-id="7b7ae-111">CPV, İş Ortağı Merkezi panosuna veya API’lerine doğrudan erişimi olan bir CSP iş ortağı değildir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-111">A CPV isn't a CSP partner with direct access to the Partner Center dashboard or APIs.</span></span>

- <span data-ttu-id="7b7ae-112">Uygulama kimliği + kullanıcı kimlik doğrulaması kullanan ve doğrudan uygulama API'leriyle tümleştiren CSP dolaylı sağlayıcıları ve CSP İş Ortağı Merkezi iş ortakları.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-112">CSP indirect providers and CSP direct partners who are using app ID + user authentication and directly integrate with Partner Center APIs.</span></span>

## <a name="security-requirements"></a><span data-ttu-id="7b7ae-113">Güvenlik gereksinimleri</span><span class="sxs-lookup"><span data-stu-id="7b7ae-113">Security requirements</span></span>

<span data-ttu-id="7b7ae-114">Güvenlik gereksinimleri hakkında ayrıntılı bilgi için bkz. [İş Ortağı Güvenlik Gereksinimleri.](/partner-center/partner-security-requirements)</span><span class="sxs-lookup"><span data-stu-id="7b7ae-114">For details on security requirements, see [Partner Security Requirements](/partner-center/partner-security-requirements).</span></span>

## <a name="secure-application-model"></a><span data-ttu-id="7b7ae-115">Güvenli Uygulama Modeli</span><span class="sxs-lookup"><span data-stu-id="7b7ae-115">Secure Application Model</span></span>

<span data-ttu-id="7b7ae-116">Market uygulamalarının Microsoft API'lerini çağıran CSP iş ortağı ayrıcalıklarının kimliğine bürünmeleri gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-116">Marketplace applications need to impersonate CSP partner privileges to call Microsoft APIs.</span></span> <span data-ttu-id="7b7ae-117">Bu hassas uygulamalara yönelik güvenlik saldırıları müşteri verilerini tehlikeye atarak yol açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-117">Security attacks on these sensitive applications can lead to the compromise of customer data.</span></span>

<span data-ttu-id="7b7ae-118">Yeni kimlik doğrulama çerçevesine genel bakış ve ayrıntılar için Güvenli Uygulama Modeli [belgesini](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) indirin.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-118">For an overview and details of the new authentication framework, download the [Secure Application Model framework](https://assetsprod.microsoft.com/secure-application-model-guide.pdf) document.</span></span> <span data-ttu-id="7b7ae-119">Bu belge, market uygulamalarını güvenlik tehlikeye atlarına karşı sürdürülebilir ve sağlam hale etmek için ilkeler ve en iyi yöntemleri kapsar.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-119">This document covers principles and best practices to make marketplace applications sustainable and robust from security compromises.</span></span>

## <a name="samples"></a><span data-ttu-id="7b7ae-120">Örnekler</span><span class="sxs-lookup"><span data-stu-id="7b7ae-120">Samples</span></span>

<span data-ttu-id="7b7ae-121">Aşağıdaki genel bakış belgeleri ve örnek kod, iş ortaklarının Güvenli Uygulama Modeli açıklar:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-121">The following overview documents and sample code describe how partners can implement the Secure Application Model framework:</span></span>

- [<span data-ttu-id="7b7ae-122">CPV genel bakış belgesi</span><span class="sxs-lookup"><span data-stu-id="7b7ae-122">CPV overview document</span></span>](https://assetsprod.microsoft.com/cpv-partner-application-overview.pdf)
- [<span data-ttu-id="7b7ae-123">CSP'ye genel bakış belgesi</span><span class="sxs-lookup"><span data-stu-id="7b7ae-123">CSP overview document</span></span>](https://assetsprod.microsoft.com/csp-partner-application-overview.pdf)
- [<span data-ttu-id="7b7ae-124">.NET Örnekleri</span><span class="sxs-lookup"><span data-stu-id="7b7ae-124">.NET Samples</span></span>](https://github.com/microsoft/Partner-Center-DotNet-Samples/tree/master/secure-app-model)
- [<span data-ttu-id="7b7ae-125">Java Örnekleri</span><span class="sxs-lookup"><span data-stu-id="7b7ae-125">Java Samples</span></span>](https://github.com/microsoft/Partner-Center-Java-Samples/tree/master/secure-app-model)

    [!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

- [<span data-ttu-id="7b7ae-126">REST yönergeleri ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="7b7ae-126">REST instructions and samples</span></span>](#rest)
- [<span data-ttu-id="7b7ae-127">PowerShell yönergeleri ve örnekleri</span><span class="sxs-lookup"><span data-stu-id="7b7ae-127">PowerShell instructions and samples</span></span>](#powershell)

## <a name="rest"></a><span data-ttu-id="7b7ae-128">REST</span><span class="sxs-lookup"><span data-stu-id="7b7ae-128">REST</span></span>

<span data-ttu-id="7b7ae-129">Güvenli Uygulama Modeli çerçevesini örnek kodla rest çağrısı yapmak için şu adımları izleyin:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-129">To to make REST calls with the Secure Application Model framework with sample code, follow these steps:</span></span>

1. [<span data-ttu-id="7b7ae-130">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b7ae-130">Create a web app</span></span>](#create-a-web-app)

2. [<span data-ttu-id="7b7ae-131">Yetkilendirme kodu al</span><span class="sxs-lookup"><span data-stu-id="7b7ae-131">Get an authorization code</span></span>](#get-authorization-code)

3. [<span data-ttu-id="7b7ae-132">Yenileme belirteci alın</span><span class="sxs-lookup"><span data-stu-id="7b7ae-132">Get a refresh token</span></span>](#get-refresh-token)

4. [<span data-ttu-id="7b7ae-133">Bir erişim belirteci alma</span><span class="sxs-lookup"><span data-stu-id="7b7ae-133">Get an access token</span></span>](#get-access-token)

5. [<span data-ttu-id="7b7ae-134">İş Ortağı Merkezi API çağrısı yapma</span><span class="sxs-lookup"><span data-stu-id="7b7ae-134">Make a Partner Center API call</span></span>](#make-partner-center-api-calls)

> [!TIP]
> <span data-ttu-id="7b7ae-135">Yetkilendirme kodu ve İş Ortağı Merkezi almak için PowerShell modülünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-135">You can use the Partner Center PowerShell module to get an authorization code and a refresh token.</span></span> <span data-ttu-id="7b7ae-136">2. ve 3. adımlar yerine bu seçeneği seçebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-136">You can choose this option in place of steps 2 and 3.</span></span> <span data-ttu-id="7b7ae-137">Daha fazla bilgi için [PowerShell bölümüne ve örneklerine bakın.](#powershell)</span><span class="sxs-lookup"><span data-stu-id="7b7ae-137">For more information, see the [PowerShell section and examples](#powershell).</span></span>

### <a name="create-a-web-app"></a><span data-ttu-id="7b7ae-138">Web uygulaması oluşturma</span><span class="sxs-lookup"><span data-stu-id="7b7ae-138">Create a web app</span></span>

<span data-ttu-id="7b7ae-139">REST çağrıları yapmadan önce bir web uygulamasını İş Ortağı Merkezi web uygulaması oluşturmanız ve kaydetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-139">You must create and register a web app in Partner Center before making REST calls.</span></span>

1. <span data-ttu-id="7b7ae-140">[Azure portalında](https://portal.azure.com) oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-140">Sign in to the [Azure portal](https://portal.azure.com).</span></span>

2. <span data-ttu-id="7b7ae-141">Bir Azure Active Directory (Azure AD) uygulaması oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-141">Create an Azure Active Directory (Azure AD) app.</span></span>

3. <span data-ttu-id="7b7ae-142">Uygulama gereksinimlerine bağlı olarak aşağıdaki *kaynaklara temsilcili uygulama izinleri verin.*</span><span class="sxs-lookup"><span data-stu-id="7b7ae-142">Give delegated application permissions to the following resources, *depending on your application's requirements*.</span></span> <span data-ttu-id="7b7ae-143">Gerekirse, uygulama kaynakları için daha fazla temsilcili izin ebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-143">If necessary, you can add more delegated permissions for application resources.</span></span>

   1. <span data-ttu-id="7b7ae-144">**Microsoft İş Ortağı Merkezi** (bazı kiracılar bunu **SampleBECApp olarak gösterir)**</span><span class="sxs-lookup"><span data-stu-id="7b7ae-144">**Microsoft Partner Center** (some tenants show this as **SampleBECApp**)</span></span>

   2. <span data-ttu-id="7b7ae-145">**Azure Yönetim API'leri** (Azure API'lerini çağırmayı planlıyorsanız)</span><span class="sxs-lookup"><span data-stu-id="7b7ae-145">**Azure Management APIs** (if you are planning to call Azure APIs)</span></span>

   3. <span data-ttu-id="7b7ae-146">**Windows Azure Active Directory**</span><span class="sxs-lookup"><span data-stu-id="7b7ae-146">**Windows Azure Active Directory**</span></span>

4. <span data-ttu-id="7b7ae-147">Uygulamanın giriş URL'sinin canlı bir web uygulamasının çalıştır bulunduğu uç nokta olarak ayarlanmış olduğundan emin olun.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-147">Make sure that the home URL of your app is set to an endpoint where a live web app is running.</span></span> <span data-ttu-id="7b7ae-148">Bu uygulamanın Azure AD oturum [açma çağrısından](#get-authorization-code) yetkilendirme kodunu kabul etmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-148">This app will need to accept the [authorization code](#get-authorization-code) from the Azure AD login call.</span></span> <span data-ttu-id="7b7ae-149">Örneğin, aşağıdaki bölümdeki örnek [kodda](#get-authorization-code)web uygulaması üzerinde `https://localhost:44395/` çalışıyor.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-149">For example, in the example code in [the following section](#get-authorization-code), the web app is running at `https://localhost:44395/`.</span></span>

5. <span data-ttu-id="7b7ae-150">Azure AD'de web uygulamasının ayarlarından aşağıdaki bilgileri not edin:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-150">Note the following information from your web app's settings in Azure AD:</span></span>

   - <span data-ttu-id="7b7ae-151">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="7b7ae-151">Application ID</span></span>
   - <span data-ttu-id="7b7ae-152">Uygulama gizli dizisi</span><span class="sxs-lookup"><span data-stu-id="7b7ae-152">Application secret</span></span>

> [!NOTE]
> <span data-ttu-id="7b7ae-153">Uygulama gizli anahtar [olarak bir sertifika kullanılması önerilir.](/azure/active-directory/develop/active-directory-certificate-credentials)</span><span class="sxs-lookup"><span data-stu-id="7b7ae-153">It is recommended to [use a certificate as your application secret](/azure/active-directory/develop/active-directory-certificate-credentials).</span></span> <span data-ttu-id="7b7ae-154">Ancak, uygulama anahtarı da uygulama anahtarı Azure portal.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-154">However, you can also create an application key in the Azure portal.</span></span> <span data-ttu-id="7b7ae-155">Aşağıdaki bölümdeki [örnek kod bir](#get-authorization-code) uygulama anahtarı kullanır.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-155">The sample code in [the following section](#get-authorization-code) uses an application key.</span></span>

### <a name="get-authorization-code"></a><span data-ttu-id="7b7ae-156">Yetkilendirme kodunu alma</span><span class="sxs-lookup"><span data-stu-id="7b7ae-156">Get authorization code</span></span>

<span data-ttu-id="7b7ae-157">Web uygulamanıza Azure AD oturum açma çağrısından kabul etmek için bir yetkilendirme kodu alalız:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-157">You must get an authorization code for your web app to accept from the Azure AD login call:</span></span>

1. <span data-ttu-id="7b7ae-158">Azure AD'de şu URL'de oturum açma: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1) .</span><span class="sxs-lookup"><span data-stu-id="7b7ae-158">Log in to Azure AD at the following URL: [https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1](https://login.microsoftonline.com/common/oauth2/authorize?client_id=Application-Id&response_mode=form_post&response_type=code%20id_token&scope=openid%20profile&nonce=1).</span></span> <span data-ttu-id="7b7ae-159">Api çağrılarını (yönetici aracısı veya satış aracısı hesabı gibi) İş Ortağı Merkezi kullanıcı hesabıyla oturum açabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-159">Be sure to log in with the user account from which you will make Partner Center API calls (such as an admin agent or sales agent account).</span></span>

2. <span data-ttu-id="7b7ae-160">**Application-Id yerine** Azure AD uygulama kimliğinizi (GUID) girin.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-160">Replace **Application-Id** with your Azure AD app ID (GUID).</span></span>

3. <span data-ttu-id="7b7ae-161">İstendiğinde, MFA yapılandırılmış şekilde kullanıcı hesabınızla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-161">When prompted, log in with your user account with MFA configured.</span></span>

4. <span data-ttu-id="7b7ae-162">İstendiğinde oturum açma bilgilerinizi doğrulamak için ek MFA bilgileri (telefon numarası veya e-posta adresi) girin.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-162">When prompted, enter additional MFA information (phone number or email address) to verify your login.</span></span>

5. <span data-ttu-id="7b7ae-163">Oturum açtıktan sonra tarayıcı, yetkilendirme kodunuzla çağrıyı web uygulaması uç noktanıza yeniden yönlendirecek.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-163">After you are logged in, the browser will redirect the call to your web app endpoint with your authorization code.</span></span> <span data-ttu-id="7b7ae-164">Örneğin, aşağıdaki örnek kod olarak yeniden `https://localhost:44395/` yönlendirildi.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-164">For example, the following sample code redirects to `https://localhost:44395/`.</span></span>

#### <a name="authorization-code-call-trace"></a><span data-ttu-id="7b7ae-165">Yetkilendirme kodu çağrı izlemesi</span><span class="sxs-lookup"><span data-stu-id="7b7ae-165">Authorization code call trace</span></span>

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

### <a name="get-refresh-token"></a><span data-ttu-id="7b7ae-166">Yenileme belirteci alın</span><span class="sxs-lookup"><span data-stu-id="7b7ae-166">Get refresh token</span></span>

<span data-ttu-id="7b7ae-167">Ardından yenileme belirteci almak için yetkilendirme kodunuzu kullansanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-167">You must then use your authorization code to get a refresh token:</span></span>

1. <span data-ttu-id="7b7ae-168">Yetkilendirme koduyla Azure AD oturum açma uç noktasına post `https://login.microsoftonline.com/CSPTenantID/oauth2/token` çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-168">Make a POST call to the Azure AD login endpoint `https://login.microsoftonline.com/CSPTenantID/oauth2/token` with the authorization code.</span></span> <span data-ttu-id="7b7ae-169">Bir örnek için aşağıdaki örnek [çağrısına bakın.](#sample-refresh-call)</span><span class="sxs-lookup"><span data-stu-id="7b7ae-169">For an example, see the following [sample call](#sample-refresh-call).</span></span>

2. <span data-ttu-id="7b7ae-170">Döndürülen yenileme belirteci not alın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-170">Note the refresh token that is returned.</span></span>

3. <span data-ttu-id="7b7ae-171">Yenileme belirteci Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-171">Store the refresh token in Azure Key Vault.</span></span> <span data-ttu-id="7b7ae-172">Daha fazla bilgi için api [Key Vault bakın.](/rest/api/keyvault/)</span><span class="sxs-lookup"><span data-stu-id="7b7ae-172">For more information, see the [Key Vault API documentation](/rest/api/keyvault/).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7b7ae-173">Yenileme belirteci Key Vault’ta [gizli dizi olarak depolanmalıdır](/rest/api/keyvault/setsecret/setsecret).</span><span class="sxs-lookup"><span data-stu-id="7b7ae-173">The refresh token must be [stored as a secret](/rest/api/keyvault/setsecret/setsecret) in Key Vault.</span></span>

#### <a name="sample-refresh-call"></a><span data-ttu-id="7b7ae-174">Örnek yenileme çağrısı</span><span class="sxs-lookup"><span data-stu-id="7b7ae-174">Sample refresh call</span></span>

<span data-ttu-id="7b7ae-175">Yer tutucu isteği:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-175">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 966
Expect: 100-continue
```

<span data-ttu-id="7b7ae-176">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-176">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id&client_secret=Application-Secret&grant_type=authorization_code&code=AuthorizationCodeValue
```

<span data-ttu-id="7b7ae-177">Yer tutucu yanıtı:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-177">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="7b7ae-178">Yanıt gövdesi:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-178">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","ext_expires_in":"3599","expires_on":"1547579127","not_before":"1547575227","resource":"https://api.partnercenter.microsoft.com","access_token":"Access
```

### <a name="get-access-token"></a><span data-ttu-id="7b7ae-179">Erişim belirteci al</span><span class="sxs-lookup"><span data-stu-id="7b7ae-179">Get access token</span></span>

<span data-ttu-id="7b7ae-180">Uygulama API'lerine çağrılar yapmak için önce bir erişim İş Ortağı Merkezi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-180">You must obtain an access token before you can make calls to the Partner Center APIs.</span></span> <span data-ttu-id="7b7ae-181">Erişim belirteçleri genellikle çok sınırlı bir yaşam süresine sahip olduğundan (örneğin, bir saatten az) erişim belirteci almak için yenileme belirteci kullanasınız.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-181">You must use a refresh token to obtain an access token because access tokens generally have a very limited lifetime (for example, less than an hour).</span></span>

<span data-ttu-id="7b7ae-182">Yer tutucu isteği:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-182">Placeholder request:</span></span>

```http
POST https://login.microsoftonline.com/CSPTenantID/oauth2/token HTTP/1.1
Content-Type: application/x-www-form-urlencoded
Host: login.microsoftonline.com
Content-Length: 1212
Expect: 100-continue
```

<span data-ttu-id="7b7ae-183">İstek gövdesi:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-183">Request body:</span></span>

```http
resource=https%3a%2f%2fapi.partnercenter.microsoft.com&client_id=Application-Id &client_secret= Application-Secret&grant_type=refresh_token&refresh_token=RefreshTokenVlaue&scope=openid
```

<span data-ttu-id="7b7ae-184">Yer tutucu yanıtı:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-184">Placeholder response:</span></span>

```http
HTTP/1.1 200 OK
Cache-Control: no-cache, no-store
Content-Type: application/json; charset=utf-8
```

<span data-ttu-id="7b7ae-185">Yanıt gövdesi:</span><span class="sxs-lookup"><span data-stu-id="7b7ae-185">Response body:</span></span>

```http
{"token_type":"Bearer","scope":"user_impersonation","expires_in":"3600","ext_expires_in":"3600","expires_on":"1547581389","not_before":"1547577489","resource":"https://api.partnercenter.microsoft.com","access_token":"AccessTokenValue","id_token":"IDTokenValue"}
```

### <a name="make-partner-center-api-calls"></a><span data-ttu-id="7b7ae-186">Api İş Ortağı Merkezi çağrıları yapma</span><span class="sxs-lookup"><span data-stu-id="7b7ae-186">Make Partner Center API calls</span></span>

<span data-ttu-id="7b7ae-187">İş Ortağı Merkezi API'lerini çağıran erişim belirtec İş Ortağı Merkezi gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-187">You must use your access token to call the Partner Center APIs.</span></span> <span data-ttu-id="7b7ae-188">Aşağıdaki örnek çağrıya bakın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-188">See the following example call.</span></span>

#### <a name="example-partner-center-api-call"></a><span data-ttu-id="7b7ae-189">Örnek İş Ortağı Merkezi API çağrısı</span><span class="sxs-lookup"><span data-stu-id="7b7ae-189">Example Partner Center API call</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/CustomerTenantId/users HTTP/1.1
Authorization: Bearer AccessTokenValue
Accept: application/json
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="powershell"></a><span data-ttu-id="7b7ae-190">PowerShell</span><span class="sxs-lookup"><span data-stu-id="7b7ae-190">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="7b7ae-191">Erişim belirteci İş Ortağı Merkezi yetkilendirme kodunu değiştirmesi için gerekli altyapıyı azaltmak üzere [powershell](https://www.powershellgallery.com/packages/PartnerCenter) modülünü kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-191">You can use the [Partner Center PowerShell module](https://www.powershellgallery.com/packages/PartnerCenter) to reduce the required infrastructure to exchange an authorization code for an access token.</span></span> <span data-ttu-id="7b7ae-192">Bu yöntem, rest çağrılarını [İş Ortağı Merkezi için isteğe bağlıdır.](#rest)</span><span class="sxs-lookup"><span data-stu-id="7b7ae-192">This method is optional for making [Partner Center REST calls](#rest).</span></span>

<span data-ttu-id="7b7ae-193">Bu işlem hakkında daha fazla bilgi için PowerShell [ile Uygulama Modeli](/powershell/partnercenter/secure-app-model) belgelerine bakın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-193">For more information on this process, see [Secure App Model](/powershell/partnercenter/secure-app-model) PowerShell documentation.</span></span>

1. <span data-ttu-id="7b7ae-194">Azure AD'ye ve İş Ortağı Merkezi PowerShell modüllerini yükleyin.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-194">Install the Azure AD and Partner Center PowerShell modules.</span></span>

    ```powershell
    Install-Module AzureAD
    ```

    ```powershell
    Install-Module PartnerCenter
    ```

2. <span data-ttu-id="7b7ae-195">Onay işlemini gerçekleştirmek ve gerekli yenileme belirteci yakalamak için **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** komutunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-195">Use the **[New-PartnerAccessToken](/powershell/module/partnercenter/new-partneraccesstoken)** command to perform the consent process and capture the required refresh token.</span></span>

    ```powershell
    $credential = Get-Credential

    $token = New-PartnerAccessToken -ApplicationId 'xxxx-xxxx-xxxx-xxxx' -Scopes 'https://api.partnercenter.microsoft.com/user_impersonation' -ServicePrincipal -Credential $credential -Tenant 'yyyy-yyyy-yyyy-yyyy' -UseAuthorizationCode
    ```

    > [!NOTE]
    > <span data-ttu-id="7b7ae-196">**Web/API** türüne sahip bir Azure AD uygulaması kullanıldığından **ServicePrincipal** parametresi **New-PartnerAccessToken** komutuyla birlikte kullanılır.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-196">The **ServicePrincipal** parameter is used with the **New-PartnerAccessToken** command because an Azure AD app with a type of **Web/API** is being used.</span></span> <span data-ttu-id="7b7ae-197">Bu tür bir uygulama, erişim belirteci isteğine bir istemci tanımlayıcısı ve gizli kodun dahilsini gerektirir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-197">This type of app requires that a client identifier and secret be included in the access token request.</span></span> <span data-ttu-id="7b7ae-198">**Get-Credential komutu** çağrıldığında kullanıcı adı ve parola girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-198">When the **Get-Credential** command is invoked, you will be prompted to enter a username and password.</span></span> <span data-ttu-id="7b7ae-199">Kullanıcı adı olarak uygulama tanımlayıcısını girin.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-199">Enter the application identifier as the username.</span></span> <span data-ttu-id="7b7ae-200">Parola olarak uygulama gizli parolasını girin.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-200">Enter the application secret as the password.</span></span> <span data-ttu-id="7b7ae-201">**New-PartnerAccessToken** komutu çağrıldığında, kimlik bilgilerini yeniden girmeniz istenir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-201">When the **New-PartnerAccessToken** command is invoked, you will be prompted to enter credentials again.</span></span> <span data-ttu-id="7b7ae-202">Kullanmakta olan hizmet hesabının kimlik bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-202">Enter the credentials for the service account that you are using.</span></span> <span data-ttu-id="7b7ae-203">Bu hizmet hesabı, uygun izinlere sahip bir iş ortağı hesabı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-203">This service account should be a partner account with appropriate permissions.</span></span>

3. <span data-ttu-id="7b7ae-204">Yenileme belirteci değerini kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-204">Copy the refresh token value.</span></span>

    ```powershell
    $token.RefreshToken | clip
    ```

<span data-ttu-id="7b7ae-205">Yenileme belirteci değerini, yenileme belirteci gibi güvenli bir Azure Key Vault.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-205">You should store the refresh token value in a secure repository, such as Azure Key Vault.</span></span> <span data-ttu-id="7b7ae-206">PowerShell ile güvenli uygulama modülü hakkında daha fazla bilgi için çok faktörlü [kimlik doğrulaması makalesine](/powershell/partnercenter/multi-factor-auth) bakın.</span><span class="sxs-lookup"><span data-stu-id="7b7ae-206">For more information on how to leverage the secure application module with PowerShell, see the [multi-factor authentication](/powershell/partnercenter/multi-factor-auth) article.</span></span>
