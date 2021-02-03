---
title: Konsol test uygulaması
description: Bu konsol test uygulaması, Iş Ortağı Merkezi API 'Leri tarafından desteklenen tüm senaryolar için örnek kod sağlar. Test etmek için de kullanabilirsiniz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e82bac3ccc22d0e7cf898e5b2d2e002c622584ae
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769179"
---
# <a name="console-test-app"></a><span data-ttu-id="f2d01-104">Konsol test uygulaması</span><span class="sxs-lookup"><span data-stu-id="f2d01-104">Console test app</span></span>

<span data-ttu-id="f2d01-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="f2d01-105">**Applies to:**</span></span>

- <span data-ttu-id="f2d01-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2d01-106">Partner Center</span></span>
- <span data-ttu-id="f2d01-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2d01-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f2d01-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2d01-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f2d01-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f2d01-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f2d01-110">Konsol test uygulaması C# ve Java 'da sağlanır, Iş Ortağı Merkezi API 'Leri tarafından desteklenen tüm senaryolar için örnek kodlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="f2d01-110">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="f2d01-111">Test etmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2d01-111">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="f2d01-112">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="f2d01-112">Get the code</span></span>

<span data-ttu-id="f2d01-113">Konsol test uygulaması için örnek kodu indirin.</span><span class="sxs-lookup"><span data-stu-id="f2d01-113">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="f2d01-114">.NET</span><span class="sxs-lookup"><span data-stu-id="f2d01-114">.NET</span></span>

<span data-ttu-id="f2d01-115">[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=746682) ve gereken şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f2d01-115">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2d01-116">Uygulamayı oluşturmadan önce, *App.config* dosyadaki değerleri, [iş ortağı merkezi kimlik doğrulaması](partner-center-authentication.md)' nda oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f2d01-116">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f2d01-117">Özellikle, tümleştirme korumalı alanı hesap ayarlarınızı erken geliştirme sırasında veya üretimde test etmek için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2d01-117">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="f2d01-118">*App.config* dosyasında **ScenarioSettings** altında, çalıştırdığınız senaryolara otomatik olarak geçirilecek parametreleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2d01-118">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="f2d01-119">Çalıştırılan senaryoların listesini değiştirmek için, **ıpartnerscenario \[ \] mainsenaryolarında** ya da *program.cs* dosyasında bulunan tek bir **Get senaryolar** yönteminde bulunan satırları açıklama satırı yapın.</span><span class="sxs-lookup"><span data-stu-id="f2d01-119">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="f2d01-120">Java</span><span class="sxs-lookup"><span data-stu-id="f2d01-120">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="f2d01-121">[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=2026887) ve gereken şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="f2d01-121">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="f2d01-122">Uygulamayı oluşturmadan önce, dosyadaki *SamplesConfigurations.js* , [iş ortağı merkezi kimlik DOĞRULAMASıNDA](partner-center-authentication.md)oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="f2d01-122">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f2d01-123">Özellikle, tümleştirme korumalı alanı hesap ayarlarınızı erken geliştirme sırasında veya üretimde test etmek için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="f2d01-123">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="f2d01-124">*SamplesConfiguration.js* dosyadaki **ScenarioSettings** altında, çalıştırdığınız senaryolara otomatik olarak geçirilecek parametreleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f2d01-124">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="f2d01-125">Çalıştırılan senaryoların listesini değiştirmek için, **ıpartnerscenario \[ \] Mainsenaryolarında** ya da *program. Java* dosyasında bulunan tek bir **Get senaryolar** yönteminde bulunan satırları açıklama satırı yapın.</span><span class="sxs-lookup"><span data-stu-id="f2d01-125">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="f2d01-126">Ne değiştirilebilir</span><span class="sxs-lookup"><span data-stu-id="f2d01-126">What to change</span></span>

<span data-ttu-id="f2d01-127">Örnek kodda nelerin değişiklik yapılacağını veya değişdiklerinizi belirlemek için aşağıdaki listeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="f2d01-127">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="f2d01-128">Partnerservice ayarları</span><span class="sxs-lookup"><span data-stu-id="f2d01-128">PartnerServiceSettings</span></span>

<span data-ttu-id="f2d01-129">**Partnerservicesettings** için şu değişikliği yapmayın:</span><span class="sxs-lookup"><span data-stu-id="f2d01-129">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="f2d01-130">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="f2d01-130">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="f2d01-131">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="f2d01-131">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="f2d01-132">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="f2d01-132">**GraphEndpoint**</span></span>
- <span data-ttu-id="f2d01-133">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="f2d01-133">**CommonDomain**</span></span>

<span data-ttu-id="f2d01-134">Bu ayarların tümü, örnek API çağrılarının düzgün çalışması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="f2d01-134">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="f2d01-135">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="f2d01-135">UserAuthentication</span></span>

<span data-ttu-id="f2d01-136">**Userauthentication** için şunları değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f2d01-136">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="f2d01-137">**ApplicationId** (Azure Active Directory oturum açma için kullanılan uygulama kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-137">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="f2d01-138">**Kullanıcı adı** (Active Directory Kullanıcı adınız)</span><span class="sxs-lookup"><span data-stu-id="f2d01-138">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="f2d01-139">**Parola** (Active Directory parolanız).</span><span class="sxs-lookup"><span data-stu-id="f2d01-139">**Password** (your active directory password).</span></span>

<span data-ttu-id="f2d01-140">Değiştirme:</span><span class="sxs-lookup"><span data-stu-id="f2d01-140">Don't change:</span></span>

- <span data-ttu-id="f2d01-141">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="f2d01-141">**ResourceUrl**</span></span>
- <span data-ttu-id="f2d01-142">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="f2d01-142">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="f2d01-143">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="f2d01-143">AppAuthentication</span></span>

<span data-ttu-id="f2d01-144">**Appauthentication** için şunları değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="f2d01-144">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="f2d01-145">**ApplicationId** (uygulama oturum açması için kullanılan Active DIRECTORY uygulama kimliğiniz)</span><span class="sxs-lookup"><span data-stu-id="f2d01-145">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="f2d01-146">**Applicationsecret** (uygulama oturum açması için kullanılan Active Directory uygulama gizli anahtarı)</span><span class="sxs-lookup"><span data-stu-id="f2d01-146">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="f2d01-147">**Etki alanı** (uygulamanın barındırıldığı Active Directory etki alanı)</span><span class="sxs-lookup"><span data-stu-id="f2d01-147">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="f2d01-148">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="f2d01-148">ScenarioSettings</span></span>

<span data-ttu-id="f2d01-149">**ScenarioSettings** için şunu değiştirmeyin:</span><span class="sxs-lookup"><span data-stu-id="f2d01-149">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="f2d01-150">**Customerdomainsuffix** (yeni müşteri oluşturulurken kullanılan etki alanı soneki)</span><span class="sxs-lookup"><span data-stu-id="f2d01-150">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="f2d01-151">İsteğe bağlı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="f2d01-151">Optional settings.</span></span> <span data-ttu-id="f2d01-152">Boş bırakılırsa, gereken yerde bir senaryo çalıştırılırken bu bilgilerin oluşturulması gerekir):</span><span class="sxs-lookup"><span data-stu-id="f2d01-152">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="f2d01-153">**Customerıdtodelete** (silinmek üzere kullanılan müşterinin kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-153">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="f2d01-154">**Defaultcustomerıd** (müşteriyle ilgili senaryolarda kullanılacak müşteri kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-154">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="f2d01-155">**Defaultınvoiceıd** (fatura senaryolarında kullanılacak fatura kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-155">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="f2d01-156">**Partnermpnıd** (dolaylı iş ortağı senaryolarında kullanılacak iş ortağı MPN kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-156">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="f2d01-157">**DefaultServiceRequestId** (hizmet isteği senaryolarında kullanılacak HIZMET isteği kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-157">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="f2d01-158">**Defaultsupporttopicıd** (hizmet isteği senaryolarında kullanılacak destek konusu kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-158">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="f2d01-159">**Defaultofferıd** (teklif senaryolarında kullanılacak teklif kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-159">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="f2d01-160">**DefaultOrderID** (sipariş senaryolarında kullanılacak sıra kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-160">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="f2d01-161">**Defaultsubscriptionıd** (abonelik senaryolarında kullanılacak abonelik kimliği)</span><span class="sxs-lookup"><span data-stu-id="f2d01-161">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="f2d01-162">Değişiklik için isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="f2d01-162">Optional to change.</span></span> <span data-ttu-id="f2d01-163">Bu ayarların tümü, disk belleği içeriğini alırken sayfa başına giriş miktarını belirtir:</span><span class="sxs-lookup"><span data-stu-id="f2d01-163">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="f2d01-164">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="f2d01-164">**CustomerPageSize**</span></span>
- <span data-ttu-id="f2d01-165">**Invoicepagesize**</span><span class="sxs-lookup"><span data-stu-id="f2d01-165">**InvoicePageSize**</span></span>
- <span data-ttu-id="f2d01-166">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="f2d01-166">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="f2d01-167">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="f2d01-167">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="f2d01-168">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="f2d01-168">**SubscriptionPageSize**</span></span>
