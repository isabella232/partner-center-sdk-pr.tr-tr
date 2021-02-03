---
title: Microsoft Ulusal bulut için Iş Ortağı Merkezi için uygulama ayrıntılarını kaydetme
description: Microsoft National Cloud için Iş Ortağı Merkezi 'nin uygulama geliştiricilerinin, Azure portal aracılığıyla Azure AD ile uygulamaları hakkındaki ayrıntıları nasıl ve neden kaydetmesi gerektiğini öğrenin.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 887cb71c752ac5d9c61398536711545c19cc7600
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770146"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="47749-103">Microsoft National Cloud için Iş Ortağı Merkezi 'nin Azure portal aracılığıyla uygulama ayrıntılarını kaydedin</span><span class="sxs-lookup"><span data-stu-id="47749-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="47749-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="47749-104">**Applies to:**</span></span>

- <span data-ttu-id="47749-105">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="47749-105">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="47749-106">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="47749-106">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="47749-107">Geliştiricilerin, Azure portal aracılığıyla Azure AD ile uygulamaları hakkındaki ayrıntıları kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="47749-107">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="47749-108">Bu, yalnızca belirtilen uygulamaların iş ortağı ve müşteri verilerine bağlanabildiğinden emin olmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="47749-108">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="47749-109">ABD hükümeti için Microsoft Bulut Iş Ortağı Merkezi için, şu anda uygulamaları PowerShell aracılığıyla yönetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="47749-109">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="47749-110">Daha fazla bilgi için [Azure PowerShell başvuru belgelerine](/powershell/module/Azuread/#applications)bakın.</span><span class="sxs-lookup"><span data-stu-id="47749-110">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="47749-111">ABD hükümeti için Microsoft Bulut için Microsoft Bulut Almanya veya Iş Ortağı Merkezi için Iş Ortağı Merkezi için bir uygulama oluşturduğunuzda aşağıdaki ek gereksinimleri unutmayın.</span><span class="sxs-lookup"><span data-stu-id="47749-111">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="47749-112">Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="47749-112">Web apps</span></span>

<span data-ttu-id="47749-113">Web Apps için, uygulama KIMLIĞINIZI kaydetmek üzere aşağıdaki yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="47749-113">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="47749-114">Web uygulaması oluştur veya güncelleştir</span><span class="sxs-lookup"><span data-stu-id="47749-114">Create or update web app</span></span>

1. <span data-ttu-id="47749-115">Uygulamanızı kaydetmek için [Azure portal uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="47749-115">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="47749-116">Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="47749-116">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="47749-117">**Yeni kayıt** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="47749-117">Select **New registration**.</span></span> <span data-ttu-id="47749-118">Daha fazla bilgi için bkz. [hızlı başlangıç: Microsoft Identity platformu ile uygulama kaydetme](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="47749-118">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="47749-119">Web uygulaması için API erişim izinlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="47749-119">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="47749-120">Uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-120">Choose your app.</span></span> <span data-ttu-id="47749-121">Web uygulamasının **Ayarlar** ' a gidin.</span><span class="sxs-lookup"><span data-stu-id="47749-121">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="47749-122">**API erişimi** bölümünde **gerekli izinleri** seçin</span><span class="sxs-lookup"><span data-stu-id="47749-122">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="47749-123">Windows Azure Active Directory izinleri için:</span><span class="sxs-lookup"><span data-stu-id="47749-123">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="47749-124">**Windows Azure Active Directory izinleri**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-124">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="47749-125">**Uygulamalar izinler**' de, dizin verilerini oku ' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-125">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="47749-126">İzinleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="47749-126">Save the permissions.</span></span>

4. <span data-ttu-id="47749-127">Web uygulamanızın **Özellikler** BÖLÜMÜNDEKI uygulama kimliği ' ni aklınızda yapın.</span><span class="sxs-lookup"><span data-stu-id="47749-127">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="47749-128">Uygulamanıza gizli anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="47749-128">Add a secret key to your app</span></span>

1. <span data-ttu-id="47749-129">Web uygulamanızın **anahtarlar** bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="47749-129">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="47749-130">Anahtar açıklaması girin ve gereken süreyi 1 veya 2 yıl olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-130">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="47749-131">Gizli anahtar değerini kaydedin ve kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="47749-131">Save and copy the secret key value.</span></span> <span data-ttu-id="47749-132">**Bu sayfadan ayrıldığınızda bu değer tekrar gösterilmeyecektir.**</span><span class="sxs-lookup"><span data-stu-id="47749-132">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="47749-133">Web uygulaması yapılandırmasından aşağıdaki ayrıntılara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="47749-133">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="47749-134">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="47749-134">Application ID</span></span>
- <span data-ttu-id="47749-135">Uygulama gizli dizisi</span><span class="sxs-lookup"><span data-stu-id="47749-135">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="47749-136">Web uygulamasını Iş Ortağı Merkezi 'ne kaydetme</span><span class="sxs-lookup"><span data-stu-id="47749-136">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="47749-137">' Da oturum açın [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) .</span><span class="sxs-lookup"><span data-stu-id="47749-137">Log in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="47749-138">**Pano**' yı ve ardından **Hesap ayarları**' nı ve ardından **uygulama yönetimi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-138">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="47749-139">**Web uygulaması** bölümünde **var olan uygulamayı kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-139">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="47749-140">Azure portal içinde oluşturduğunuz Web uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-140">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="47749-141">**Uygulamanızı kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-141">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="47749-142">Yerel uygulamalar</span><span class="sxs-lookup"><span data-stu-id="47749-142">Native apps</span></span>

<span data-ttu-id="47749-143">Yerel uygulamaların Iş Ortağı Merkezi 'ne kayıtlı olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="47749-143">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="47749-144">Ancak bu uygulamaların Iş Ortağı Merkezi API 'Lerine erişim sağlayacak şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="47749-144">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="47749-145">Azure portal yerel bir uygulama oluşturmadan önce, iş ortağı kiracısındaki Yönetici Kullanıcı kimlik bilgilerini kullanarak Iş Ortağı Merkezi ' nde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="47749-145">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="47749-146">Bu, uygulama izinlerini etkinleştirmek için Kiracıdaki ayarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="47749-146">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="47749-147">Yerel uygulama oluştur</span><span class="sxs-lookup"><span data-stu-id="47749-147">Create native app</span></span>

1. <span data-ttu-id="47749-148">Uygulamanızı kaydetmek için [Azure portal uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="47749-148">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="47749-149">Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="47749-149">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="47749-150">**Yeni kayıt** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="47749-150">Select **New registration**.</span></span> <span data-ttu-id="47749-151">Daha fazla bilgi için bkz. [hızlı başlangıç: Microsoft Identity platformu ile uygulama kaydetme](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="47749-151">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="47749-152">Yerel uygulama için API erişim izinlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="47749-152">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="47749-153">Uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-153">Choose your app.</span></span> <span data-ttu-id="47749-154">**Ayarlar**' a gidin.</span><span class="sxs-lookup"><span data-stu-id="47749-154">Go to **Settings**.</span></span>

2. <span data-ttu-id="47749-155">API erişimi ' nde **gerekli izinler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-155">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="47749-156">**Windows Azure Active Directory izinleri**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-156">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="47749-157">**Temsilci izinleri**' nde şu izinleri seçin:</span><span class="sxs-lookup"><span data-stu-id="47749-157">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="47749-158">**Oturum açma ve kullanıcı profilini okuma**</span><span class="sxs-lookup"><span data-stu-id="47749-158">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="47749-159">**Dizin verilerini oku**</span><span class="sxs-lookup"><span data-stu-id="47749-159">**Read directory data**</span></span>
    - <span data-ttu-id="47749-160">**Dizine oturum açmış kullanıcı olarak erişin**</span><span class="sxs-lookup"><span data-stu-id="47749-160">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="47749-161">**Tüm grupları oku**</span><span class="sxs-lookup"><span data-stu-id="47749-161">**Read all groups**</span></span>

4. <span data-ttu-id="47749-162">İzinleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="47749-162">Save the permissions.</span></span>

5. <span data-ttu-id="47749-163">**Gerekli Izinlere** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-163">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="47749-164">**API seçin** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-164">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="47749-165">Arama kutusuna **Microsoft Iş Ortağı Merkezi** ' ni girin ve sonuçlar listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-165">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="47749-166">**Seç**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-166">Choose **Select**.</span></span>

7. <span data-ttu-id="47749-167">**Izinleri Seç ' i** seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-167">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="47749-168">**Erişim Iş Ortağı Merkezi PPE**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-168">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="47749-169">**Seç**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-169">Choose **Select**.</span></span>

8. <span data-ttu-id="47749-170">**Bitti**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="47749-170">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="47749-171">Uygulamanızın özelliklerindeki uygulama KIMLIĞI ' ni aklınızda yapın.</span><span class="sxs-lookup"><span data-stu-id="47749-171">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="47749-172">Yerel uygulamaları Iş Ortağı Merkezi 'ne kaydetmeniz gerekmez, ancak yerel uygulamanın yönetici onaylı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="47749-172">You do not need to register native apps in Partner Center, however the native app must be admin consented .</span></span> <span data-ttu-id="47749-173">Yerel uygulamanızın uygulama KIMLIĞI ' ni aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="47749-173">Note the application ID of your native app.</span></span>
