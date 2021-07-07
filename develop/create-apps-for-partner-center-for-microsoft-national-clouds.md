---
title: Microsoft Ulusal bulut için Iş Ortağı Merkezi için uygulama ayrıntılarını kaydetme
description: Microsoft National Cloud için Iş Ortağı Merkezi 'nin uygulama geliştiricilerinin, Azure portal aracılığıyla Azure AD ile uygulamaları hakkındaki ayrıntıları nasıl ve neden kaydetmesi gerektiğini öğrenin.
MS-HAID:
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_cloud\_germany
- pc\_apiv2.create\_apps\_for\_partner\_center\_for\_microsoft\_national\_clouds
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93d46a17bc26e9586e5e773bdf934653a571367f
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973460"
---
# <a name="register-app-details-for-partner-center-for-microsoft-national-cloud-through-the-azure-portal"></a><span data-ttu-id="eaf07-103">Microsoft National Cloud için Iş Ortağı Merkezi 'nin Azure portal aracılığıyla uygulama ayrıntılarını kaydedin</span><span class="sxs-lookup"><span data-stu-id="eaf07-103">Register app details for Partner Center for Microsoft National Cloud through the Azure portal</span></span>

<span data-ttu-id="eaf07-104">**Uygulama hedefi**: Microsoft bulut Almanya için Iş Ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="eaf07-104">**Applies to**: Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="eaf07-105">Geliştiricilerin, Azure portal aracılığıyla Azure AD ile uygulamaları hakkındaki ayrıntıları kaydetmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaf07-105">Developers must register details about their app with Azure AD through the Azure portal.</span></span> <span data-ttu-id="eaf07-106">Bu, yalnızca belirtilen uygulamaların iş ortağı ve müşteri verilerine bağlanabildiğinden emin olmanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="eaf07-106">This helps ensure that only specified apps are able to connect to partner and customer data.</span></span>

<span data-ttu-id="eaf07-107">Microsoft Cloud for US Government için iş ortağı merkezi 'nde, şu anda uygulamaları PowerShell aracılığıyla yönetmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaf07-107">For Partner Center for Microsoft Cloud for US Government, you currently must manage apps through PowerShell.</span></span> <span data-ttu-id="eaf07-108">daha fazla bilgi için [Azure PowerShell başvuru belgelerine](/powershell/module/Azuread/#applications)bakın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-108">For more information, see the [Azure PowerShell reference documentation](/powershell/module/Azuread/#applications).</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="eaf07-109">Microsoft Cloud for US Government için Microsoft Bulut Almanya veya Iş Ortağı Merkezi için bir Iş Ortağı Merkezi uygulaması oluşturduğunuzda aşağıdaki ek gereksinimleri göz önünde bulundurun.</span><span class="sxs-lookup"><span data-stu-id="eaf07-109">Be aware of the following additional requirements when you create an app for Partner Center for Microsoft Cloud Germany or Partner Center for Microsoft Cloud for US Government.</span></span>

## <a name="web-apps"></a><span data-ttu-id="eaf07-110">Web uygulamaları</span><span class="sxs-lookup"><span data-stu-id="eaf07-110">Web apps</span></span>

<span data-ttu-id="eaf07-111">Web Apps için, uygulama KIMLIĞINIZI kaydetmek üzere aşağıdaki yordamları kullanın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-111">For web apps, use the following procedures to register your application ID.</span></span>

### <a name="create-or-update-web-app"></a><span data-ttu-id="eaf07-112">Web uygulaması oluştur veya güncelleştir</span><span class="sxs-lookup"><span data-stu-id="eaf07-112">Create or update web app</span></span>

1. <span data-ttu-id="eaf07-113">Uygulamanızı kaydetmek için [Azure portal uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-113">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="eaf07-114">Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-114">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="eaf07-115">**Yeni kayıt** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-115">Select **New registration**.</span></span> <span data-ttu-id="eaf07-116">daha fazla bilgi için bkz. [hızlı başlangıç: Microsoft kimlik platformu bir uygulamayı kaydetme](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="eaf07-116">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-web-app"></a><span data-ttu-id="eaf07-117">Web uygulaması için API erişim izinlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eaf07-117">Configure API access permissions for web app</span></span>

1. <span data-ttu-id="eaf07-118">Uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-118">Choose your app.</span></span> <span data-ttu-id="eaf07-119">Web uygulamasının **Ayarlar** gidin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-119">Go to **Settings** of the Web app.</span></span>

2. <span data-ttu-id="eaf07-120">**API erişimi** bölümünde **gerekli izinleri** seçin</span><span class="sxs-lookup"><span data-stu-id="eaf07-120">In **API Access** section, choose **Required permissions**</span></span>

3. <span data-ttu-id="eaf07-121">Azure Active directory izinleri Windows için:</span><span class="sxs-lookup"><span data-stu-id="eaf07-121">For Windows Azure Active directory permissions:</span></span>

    1. <span data-ttu-id="eaf07-122">**Windows Azure Active Directory izinlerini** seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-122">Choose **Windows Azure Active Directory permissions**.</span></span>

    2. <span data-ttu-id="eaf07-123">**Uygulamalar izinler**' de, dizin verilerini oku ' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-123">In **Applications permissions**, select Read directory data.</span></span>

    3. <span data-ttu-id="eaf07-124">İzinleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-124">Save the permissions.</span></span>

4. <span data-ttu-id="eaf07-125">Web uygulamanızın **Özellikler** BÖLÜMÜNDEKI uygulama kimliği ' ni aklınızda yapın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-125">Note the application ID in the **Properties** section of your web app.</span></span>

### <a name="add-a-secret-key-to-your-app"></a><span data-ttu-id="eaf07-126">Uygulamanıza gizli anahtar ekleme</span><span class="sxs-lookup"><span data-stu-id="eaf07-126">Add a secret key to your app</span></span>

1. <span data-ttu-id="eaf07-127">Web uygulamanızın **anahtarlar** bölümüne gidin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-127">Go to the **Keys** section of your web app.</span></span>

2. <span data-ttu-id="eaf07-128">Anahtar açıklaması girin ve gereken süreyi 1 veya 2 yıl olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-128">Enter key description and select duration as 1 or 2 years, as you need.</span></span>

3. <span data-ttu-id="eaf07-129">Gizli anahtar değerini kaydedin ve kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-129">Save and copy the secret key value.</span></span> <span data-ttu-id="eaf07-130">**Bu sayfadan ayrıldığınızda bu değer tekrar gösterilmeyecektir.**</span><span class="sxs-lookup"><span data-stu-id="eaf07-130">**This value will not be shown again once you leave this page.**</span></span>

<span data-ttu-id="eaf07-131">Web uygulaması yapılandırmasından aşağıdaki ayrıntılara sahip olmanız gerekir:</span><span class="sxs-lookup"><span data-stu-id="eaf07-131">You should have the following details from the web app configuration:</span></span>

- <span data-ttu-id="eaf07-132">Uygulama Kimliği</span><span class="sxs-lookup"><span data-stu-id="eaf07-132">Application ID</span></span>
- <span data-ttu-id="eaf07-133">Uygulama gizli dizisi</span><span class="sxs-lookup"><span data-stu-id="eaf07-133">Application secret</span></span>

### <a name="register-the-web-app-in-partner-center"></a><span data-ttu-id="eaf07-134">Web uygulamasını Iş Ortağı Merkezi 'ne kaydetme</span><span class="sxs-lookup"><span data-stu-id="eaf07-134">Register the Web app in Partner Center</span></span>

1. <span data-ttu-id="eaf07-135">[https://partnercenter.microsoft.com](https://partnercenter.microsoft.com) adresinde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-135">Sign in to [https://partnercenter.microsoft.com](https://partnercenter.microsoft.com).</span></span>

2. <span data-ttu-id="eaf07-136">**pano**' yı seçin, ardından **hesap Ayarlar** öğesini ve ardından **uygulama yönetimi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-136">Choose **Dashboard**, then choose **Account Settings**, then choose **App Management**.</span></span>

3. <span data-ttu-id="eaf07-137">**Web uygulaması** bölümünde **var olan uygulamayı kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-137">In the **Web App** section, choose **Register existing app**.</span></span>

4. <span data-ttu-id="eaf07-138">Azure portal içinde oluşturduğunuz Web uygulamasını seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-138">Select the web app you created in Azure portal.</span></span>

5. <span data-ttu-id="eaf07-139">**Uygulamanızı kaydet**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-139">Choose **register your app**.</span></span>

## <a name="native-apps"></a><span data-ttu-id="eaf07-140">Yerel uygulamalar</span><span class="sxs-lookup"><span data-stu-id="eaf07-140">Native apps</span></span>

<span data-ttu-id="eaf07-141">Yerel uygulamaların Iş Ortağı Merkezi 'ne kayıtlı olması gerekmez.</span><span class="sxs-lookup"><span data-stu-id="eaf07-141">Native apps do not need to be registered to Partner Center.</span></span> <span data-ttu-id="eaf07-142">Ancak bu uygulamaların Iş Ortağı Merkezi API 'Lerine erişim sağlayacak şekilde yapılandırılması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaf07-142">But these apps need to be configured to provide access to Partner Center APIs.</span></span>

>[!NOTE]
><span data-ttu-id="eaf07-143">Azure portal yerel bir uygulama oluşturmadan önce, iş ortağı kiracısındaki Yönetici Kullanıcı kimlik bilgilerini kullanarak Iş Ortağı Merkezi ' nde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-143">Before creating a native app in the Azure portal, log in into Partner Center using the admin user credentials from the partner tenant.</span></span> <span data-ttu-id="eaf07-144">Bu, uygulama izinlerini etkinleştirmek için Kiracıdaki ayarları oluşturur.</span><span class="sxs-lookup"><span data-stu-id="eaf07-144">This creates the settings on the tenant to enable app permissions.</span></span>

### <a name="create-native-app"></a><span data-ttu-id="eaf07-145">Yerel uygulama oluştur</span><span class="sxs-lookup"><span data-stu-id="eaf07-145">Create native app</span></span>

1. <span data-ttu-id="eaf07-146">Uygulamanızı kaydetmek için [Azure portal uygulama kayıtları](https://go.microsoft.com/fwlink/?linkid=2083908) sayfasına gidin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-146">Navigate to the [Azure portal - App registrations](https://go.microsoft.com/fwlink/?linkid=2083908) page to register your app.</span></span> <span data-ttu-id="eaf07-147">Bir iş veya okul hesabını ya da kişisel bir Microsoft hesabını kullanarak Azure portalında oturum açın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-147">Sign in to the Azure portal using either a work or school account or a personal Microsoft account.</span></span>

2. <span data-ttu-id="eaf07-148">**Yeni kayıt** seçeneğini belirleyin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-148">Select **New registration**.</span></span> <span data-ttu-id="eaf07-149">daha fazla bilgi için bkz. [hızlı başlangıç: Microsoft kimlik platformu bir uygulamayı kaydetme](/azure/active-directory/develop/quickstart-register-app).</span><span class="sxs-lookup"><span data-stu-id="eaf07-149">For more information, see [Quickstart: Register an application with the Microsoft identity platform](/azure/active-directory/develop/quickstart-register-app).</span></span>

### <a name="configure-api-access-permissions-for-native-app"></a><span data-ttu-id="eaf07-150">Yerel uygulama için API erişim izinlerini yapılandırma</span><span class="sxs-lookup"><span data-stu-id="eaf07-150">Configure API access permissions for native app</span></span>

1. <span data-ttu-id="eaf07-151">Uygulamanızı seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-151">Choose your app.</span></span> <span data-ttu-id="eaf07-152">**Ayarlar** gidin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-152">Go to **Settings**.</span></span>

2. <span data-ttu-id="eaf07-153">API erişimi ' nde **gerekli izinler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-153">In API Access, choose **Required permissions**.</span></span>

3. <span data-ttu-id="eaf07-154">**Windows Azure Active Directory izinlerini** seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-154">Choose **Windows Azure Active Directory permissions**.</span></span> <span data-ttu-id="eaf07-155">**Temsilci izinleri**' nde şu izinleri seçin:</span><span class="sxs-lookup"><span data-stu-id="eaf07-155">In **Delegated permissions**, select these permissions:</span></span>

    - <span data-ttu-id="eaf07-156">**Oturum açma ve kullanıcı profilini okuma**</span><span class="sxs-lookup"><span data-stu-id="eaf07-156">**Sign in and read user profile**</span></span>
    - <span data-ttu-id="eaf07-157">**Dizin verilerini oku**</span><span class="sxs-lookup"><span data-stu-id="eaf07-157">**Read directory data**</span></span>
    - <span data-ttu-id="eaf07-158">**Dizine oturum açmış kullanıcı olarak erişin**</span><span class="sxs-lookup"><span data-stu-id="eaf07-158">**Access the directory as the signed-in user**</span></span>
    - <span data-ttu-id="eaf07-159">**Tüm grupları oku**</span><span class="sxs-lookup"><span data-stu-id="eaf07-159">**Read all groups**</span></span>

4. <span data-ttu-id="eaf07-160">İzinleri kaydedin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-160">Save the permissions.</span></span>

5. <span data-ttu-id="eaf07-161">**Gerekli Izinlere** **Ekle** ' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-161">Choose **Add** in **Required permissions**.</span></span>

6. <span data-ttu-id="eaf07-162">**API seçin** öğesini seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-162">Choose **Select an API**.</span></span>

    1. <span data-ttu-id="eaf07-163">Arama kutusuna **Microsoft Iş Ortağı Merkezi** ' ni girin ve sonuçlar listesinden seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-163">In the search box, enter **Microsoft Partner Center** and select it from the results list.</span></span>

    2. <span data-ttu-id="eaf07-164">**Seç**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-164">Choose **Select**.</span></span>

7. <span data-ttu-id="eaf07-165">**Izinleri Seç ' i** seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-165">Choose **Select permissions**.</span></span>

    1. <span data-ttu-id="eaf07-166">**Erişim Iş Ortağı Merkezi PPE**'yi seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-166">Select **Access Partner Center PPE**.</span></span>
    
    2. <span data-ttu-id="eaf07-167">**Seç**’i seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-167">Choose **Select**.</span></span>

8. <span data-ttu-id="eaf07-168">**Bitti**’yi seçin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-168">Choose **Done**.</span></span>

>[!IMPORTANT]
> <span data-ttu-id="eaf07-169">Uygulamanızın özelliklerindeki uygulama KIMLIĞI ' ni aklınızda yapın.</span><span class="sxs-lookup"><span data-stu-id="eaf07-169">Note the application ID in the Properties of your app.</span></span>

<span data-ttu-id="eaf07-170">Yerel uygulamaları Iş Ortağı Merkezi 'ne kaydetmeniz gerekmez, ancak yerel uygulamanın yönetici onaylı olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="eaf07-170">You do not need to register native apps in Partner Center, however the native app must be admin consented.</span></span> <span data-ttu-id="eaf07-171">Yerel uygulamanızın uygulama KIMLIĞI ' ni aklınızda edin.</span><span class="sxs-lookup"><span data-stu-id="eaf07-171">Note the application ID of your native app.</span></span>
