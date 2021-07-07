---
title: Konsol test uygulaması
description: Bu konsol test uygulaması, Iş Ortağı Merkezi API 'Leri tarafından desteklenen tüm senaryolar için örnek kod sağlar. Test etmek için de kullanabilirsiniz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b35167104deeede50107d59fca6112c10dc7b4bf
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111974038"
---
# <a name="console-test-app"></a><span data-ttu-id="06279-104">Konsol test uygulaması</span><span class="sxs-lookup"><span data-stu-id="06279-104">Console test app</span></span>

<span data-ttu-id="06279-105">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="06279-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="06279-106">Konsol test uygulaması C# ve Java 'da sağlanır, Iş Ortağı Merkezi API 'Leri tarafından desteklenen tüm senaryolar için örnek kodlar sağlar.</span><span class="sxs-lookup"><span data-stu-id="06279-106">The console test app is provided in C# and Java, it provides sample codes for all of the scenarios supported by the Partner Center APIs.</span></span> <span data-ttu-id="06279-107">Test etmek için de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06279-107">You can also use it for testing.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="06279-108">Kodu alma</span><span class="sxs-lookup"><span data-stu-id="06279-108">Get the code</span></span>

<span data-ttu-id="06279-109">Konsol test uygulaması için örnek kodu indirin.</span><span class="sxs-lookup"><span data-stu-id="06279-109">Download the sample code for the console test app.</span></span>

## <a name="net"></a><span data-ttu-id="06279-110">.NET</span><span class="sxs-lookup"><span data-stu-id="06279-110">.NET</span></span>

<span data-ttu-id="06279-111">[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=746682) ve gereken şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06279-111">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=746682) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06279-112">Uygulamayı oluşturmadan önce, *App.config* dosyadaki değerleri, [iş ortağı merkezi kimlik doğrulaması](partner-center-authentication.md)' nda oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="06279-112">Before you build the application, update the values in the *App.config* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="06279-113">Özellikle, tümleştirme korumalı alanı hesap ayarlarınızı erken geliştirme sırasında veya üretimde test etmek için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06279-113">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="06279-114">*App.config* dosyasında **ScenarioSettings** altında, çalıştırdığınız senaryolara otomatik olarak geçirilecek parametreleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06279-114">Under **ScenarioSettings** in the *App.config* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="06279-115">Çalıştırılan senaryoların listesini değiştirmek için, **ıpartnerscenario \[ \] Mainsenaryolarında** ya da *program. cs* dosyasında bulunan tek bir **Get senaryo** yönteminde bulunan satırları açıklama satırı yapın.</span><span class="sxs-lookup"><span data-stu-id="06279-115">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.cs* file.</span></span>

## <a name="java"></a><span data-ttu-id="06279-116">Java</span><span class="sxs-lookup"><span data-stu-id="06279-116">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="06279-117">[Örnek kodu indirin](https://go.microsoft.com/fwlink/p/?LinkId=2026887) ve gereken şekilde değiştirin.</span><span class="sxs-lookup"><span data-stu-id="06279-117">[Download the sample code](https://go.microsoft.com/fwlink/p/?LinkId=2026887) and modify it as necessary.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="06279-118">Uygulamayı oluşturmadan önce, dosyadaki *SamplesConfigurations.js* , [iş ortağı merkezi kimlik DOĞRULAMASıNDA](partner-center-authentication.md)oluşturduğunuz Azure AD kimlik doğrulaması bilgilerini yansıtacak şekilde güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="06279-118">Before you build the application, update the values in the *SamplesConfigurations.json* file to reflect the Azure AD authentication information you created in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="06279-119">Özellikle, tümleştirme korumalı alanı hesap ayarlarınızı erken geliştirme sırasında veya üretimde test etmek için kullanmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="06279-119">Specifically, you should use your integration sandbox account settings during early development or for testing in production.</span></span>

<span data-ttu-id="06279-120">*SamplesConfiguration.js* dosyadaki **ScenarioSettings** altında, çalıştırdığınız senaryolara otomatik olarak geçirilecek parametreleri ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="06279-120">Under **ScenarioSettings** in the *SamplesConfiguration.json* file, you can set parameters that will be automatically passed into the scenarios that you run.</span></span>

<span data-ttu-id="06279-121">Çalıştırılan senaryoların listesini değiştirmek için, **ıpartnerscenario \[ \] Mainsenaryolarında** ya da *program. Java* dosyasında bulunan tek bir **Get senaryolar** yönteminde bulunan satırları açıklama satırı yapın.</span><span class="sxs-lookup"><span data-stu-id="06279-121">To modify the list of scenarios that are run, comment out lines in **IPartnerScenario\[\] mainScenarios** or in an individual **Get Scenarios** method found in the *Program.java* file.</span></span>

## <a name="what-to-change"></a><span data-ttu-id="06279-122">Ne değiştirilebilir</span><span class="sxs-lookup"><span data-stu-id="06279-122">What to change</span></span>

<span data-ttu-id="06279-123">Örnek kodda nelerin değişiklik yapılacağını veya değişdiklerinizi belirlemek için aşağıdaki listeleri kullanın.</span><span class="sxs-lookup"><span data-stu-id="06279-123">Use the following lists to determine what to change or not change in the sample code.</span></span>

### <a name="partnerservicesettings"></a><span data-ttu-id="06279-124">Partnerservice ayarları</span><span class="sxs-lookup"><span data-stu-id="06279-124">PartnerServiceSettings</span></span>

<span data-ttu-id="06279-125">**Partnerservicesettings** için şu değişikliği yapmayın:</span><span class="sxs-lookup"><span data-stu-id="06279-125">For **PartnerServiceSettings**, don't change:</span></span>

- <span data-ttu-id="06279-126">**PartnerServiceApiEndpoint**</span><span class="sxs-lookup"><span data-stu-id="06279-126">**PartnerServiceApiEndpoint**</span></span>
- <span data-ttu-id="06279-127">**AuthenticationAuthorityEndpoint**</span><span class="sxs-lookup"><span data-stu-id="06279-127">**AuthenticationAuthorityEndpoint**</span></span>
- <span data-ttu-id="06279-128">**GraphEndpoint**</span><span class="sxs-lookup"><span data-stu-id="06279-128">**GraphEndpoint**</span></span>
- <span data-ttu-id="06279-129">**CommonDomain**</span><span class="sxs-lookup"><span data-stu-id="06279-129">**CommonDomain**</span></span>

<span data-ttu-id="06279-130">Bu ayarların tümü, örnek API çağrılarının düzgün çalışması için gereklidir.</span><span class="sxs-lookup"><span data-stu-id="06279-130">All of these settings are necessary for the sample API calls to properly function.</span></span>

### <a name="userauthentication"></a><span data-ttu-id="06279-131">UserAuthentication</span><span class="sxs-lookup"><span data-stu-id="06279-131">UserAuthentication</span></span>

<span data-ttu-id="06279-132">**Userauthentication** için şunları değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="06279-132">For **UserAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="06279-133">**applicationıd** (Azure Active Directory oturum açma için kullanılan uygulama kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-133">**ApplicationId** (your Azure Active Directory application ID used for login)</span></span>
- <span data-ttu-id="06279-134">**Kullanıcı adı** (Active Directory Kullanıcı adınız)</span><span class="sxs-lookup"><span data-stu-id="06279-134">**UserName** (your active directory username)</span></span>
- <span data-ttu-id="06279-135">**Parola** (Active Directory parolanız).</span><span class="sxs-lookup"><span data-stu-id="06279-135">**Password** (your active directory password).</span></span>

<span data-ttu-id="06279-136">Değiştirme:</span><span class="sxs-lookup"><span data-stu-id="06279-136">Don't change:</span></span>

- <span data-ttu-id="06279-137">**ResourceUrl**</span><span class="sxs-lookup"><span data-stu-id="06279-137">**ResourceUrl**</span></span>
- <span data-ttu-id="06279-138">**RedirectUrl**</span><span class="sxs-lookup"><span data-stu-id="06279-138">**RedirectUrl**</span></span>

### <a name="appauthentication"></a><span data-ttu-id="06279-139">AppAuthentication</span><span class="sxs-lookup"><span data-stu-id="06279-139">AppAuthentication</span></span>

<span data-ttu-id="06279-140">**Appauthentication** için şunları değiştirmeniz gerekir:</span><span class="sxs-lookup"><span data-stu-id="06279-140">For **AppAuthentication**, you're required to change:</span></span>

- <span data-ttu-id="06279-141">**ApplicationId** (uygulama oturum açması için kullanılan Active DIRECTORY uygulama kimliğiniz)</span><span class="sxs-lookup"><span data-stu-id="06279-141">**ApplicationId** (your active directory application ID used for application login)</span></span>
- <span data-ttu-id="06279-142">**Applicationsecret** (uygulama oturum açması için kullanılan Active Directory uygulama gizli anahtarı)</span><span class="sxs-lookup"><span data-stu-id="06279-142">**ApplicationSecret** (your active directory application secret used for application login)</span></span>
- <span data-ttu-id="06279-143">**Etki alanı** (uygulamanın barındırıldığı Active Directory etki alanı)</span><span class="sxs-lookup"><span data-stu-id="06279-143">**Domain** (your active directory domain on which the application is hosted)</span></span>

### <a name="scenariosettings"></a><span data-ttu-id="06279-144">ScenarioSettings</span><span class="sxs-lookup"><span data-stu-id="06279-144">ScenarioSettings</span></span>

<span data-ttu-id="06279-145">**ScenarioSettings** için şunu değiştirmeyin:</span><span class="sxs-lookup"><span data-stu-id="06279-145">For **ScenarioSettings**, don't change:</span></span>

- <span data-ttu-id="06279-146">**Customerdomainsuffix** (yeni müşteri oluşturulurken kullanılan etki alanı soneki)</span><span class="sxs-lookup"><span data-stu-id="06279-146">**CustomerDomainSuffix** (the domain suffix used when creating a new customer)</span></span>

<span data-ttu-id="06279-147">İsteğe bağlı ayarlar.</span><span class="sxs-lookup"><span data-stu-id="06279-147">Optional settings.</span></span> <span data-ttu-id="06279-148">Boş bırakılırsa, gereken yerde bir senaryo çalıştırılırken bu bilgilerin oluşturulması gerekir):</span><span class="sxs-lookup"><span data-stu-id="06279-148">If left blank, this information will need to be inputted when running a scenario where necessary):</span></span>

- <span data-ttu-id="06279-149">**Customerıdtodelete** (silinmek üzere kullanılan müşterinin kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-149">**CustomerIdToDelete** (the ID of the customer used for deletion)</span></span>
- <span data-ttu-id="06279-150">**Defaultcustomerıd** (müşteriyle ilgili senaryolarda kullanılacak müşteri kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-150">**DefaultCustomerId** (the customer ID to use in customer-related scenarios)</span></span>
- <span data-ttu-id="06279-151">**Defaultınvoiceıd** (fatura senaryolarında kullanılacak fatura kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-151">**DefaultInvoiceID** (the invoice ID to use in invoice scenarios)</span></span>
- <span data-ttu-id="06279-152">**Partnermpnıd** (dolaylı iş ortağı senaryolarında kullanılacak iş ortağı MPN kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-152">**PartnerMpnId** (the partner MPN ID to use in indirect partner scenarios)</span></span>
- <span data-ttu-id="06279-153">**DefaultServiceRequestId** (hizmet isteği senaryolarında kullanılacak HIZMET isteği kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-153">**DefaultServiceRequestId** (the service request ID to use in service request scenarios)</span></span>
- <span data-ttu-id="06279-154">**Defaultsupporttopicıd** (hizmet isteği senaryolarında kullanılacak destek konusu kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-154">**DefaultSupportTopicID** (the support topic ID to use in service request scenarios)</span></span>
- <span data-ttu-id="06279-155">**Defaultofferıd** (teklif senaryolarında kullanılacak teklif kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-155">**DefaultOfferID** (the offer ID to use in offer scenarios)</span></span>
- <span data-ttu-id="06279-156">**DefaultOrderID** (sipariş senaryolarında kullanılacak sıra kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-156">**DefaultOrderID** (the order ID to use in order scenarios)</span></span>
- <span data-ttu-id="06279-157">**Defaultsubscriptionıd** (abonelik senaryolarında kullanılacak abonelik kimliği)</span><span class="sxs-lookup"><span data-stu-id="06279-157">**DefaultSubscriptionID** (the subscription ID to use in subscription scenarios)</span></span>

<span data-ttu-id="06279-158">Değişiklik için isteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="06279-158">Optional to change.</span></span> <span data-ttu-id="06279-159">Bu ayarların tümü, disk belleği içeriğini alırken sayfa başına giriş miktarını belirtir:</span><span class="sxs-lookup"><span data-stu-id="06279-159">All of these settings specify the amount of entries per page when retrieving paged content:</span></span>

- <span data-ttu-id="06279-160">**CustomerPageSize**</span><span class="sxs-lookup"><span data-stu-id="06279-160">**CustomerPageSize**</span></span>
- <span data-ttu-id="06279-161">**Invoicepagesize**</span><span class="sxs-lookup"><span data-stu-id="06279-161">**InvoicePageSize**</span></span>
- <span data-ttu-id="06279-162">**ServiceRequestPageSize**</span><span class="sxs-lookup"><span data-stu-id="06279-162">**ServiceRequestPageSize**</span></span>
- <span data-ttu-id="06279-163">**DefaultOfferPageSize**</span><span class="sxs-lookup"><span data-stu-id="06279-163">**DefaultOfferPageSize**</span></span>
- <span data-ttu-id="06279-164">**SubscriptionPageSize**</span><span class="sxs-lookup"><span data-stu-id="06279-164">**SubscriptionPageSize**</span></span>
