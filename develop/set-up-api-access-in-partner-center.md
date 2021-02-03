---
title: İş Ortağı Merkezi’nde API erişimini ayarlama
description: Iş Ortağı Merkezi SDK 'sında geliştirme ve tümleştirme korumalı alanında test için hesapları ayarlayın.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 873ff2ff9cecbfa92429958d3bfe2aa79fc3ad9a
ms.sourcegitcommit: d5de47c08ba661ba5de4935caa6843d7c2c91710
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/28/2020
ms.locfileid: "97769418"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="b618d-103">İş Ortağı Merkezi’nde API erişimini ayarlama</span><span class="sxs-lookup"><span data-stu-id="b618d-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="b618d-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="b618d-104">**Applies to:**</span></span>

- <span data-ttu-id="b618d-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b618d-105">Partner Center</span></span>
- <span data-ttu-id="b618d-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b618d-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b618d-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b618d-107">Partner Center for Microsoft Cloud for US Government</span></span>
- <span data-ttu-id="b618d-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b618d-108">Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="b618d-109">Bu makalede, Iş Ortağı Merkezi SDK 'sına karşı geliştirme yapmanız gereken hesaplar açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b618d-109">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="b618d-110">Bu makalede ayrıca Integration Sandbox [hesabının](#integration-sandbox-account) nasıl oluşturulacağı ve tümleştirme korumalı alanında nasıl test kurulacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b618d-110">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="b618d-111">API 'lere erişim sağlamak için kiracınızın bir CSP kiracısı olması ve dolaylı bir sağlayıcı ya da doğrudan fatura ortağı olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b618d-111">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="b618d-112">Hesap tanımları</span><span class="sxs-lookup"><span data-stu-id="b618d-112">Account definitions</span></span>

<span data-ttu-id="b618d-113">Iş Ortağı Merkezi, API tümleştirmenizi tümleştirmenize ve test etmenize yardımcı olmak için iki hesap türünü destekler:</span><span class="sxs-lookup"><span data-stu-id="b618d-113">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="b618d-114">Birincil Iş ortağı hesabı</span><span class="sxs-lookup"><span data-stu-id="b618d-114">Primary Partner account</span></span>

<span data-ttu-id="b618d-115">Bu hesap, gerçek müşteriler için gerçek siparişler oluşturduğunuz yerdir.</span><span class="sxs-lookup"><span data-stu-id="b618d-115">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="b618d-116">Birincil hesapta oturum açtığınızda, Iş Ortağı Merkezi SDK 'sını veya Iş ortağı panosu Kullanıcı arabirimini kullanarak herhangi bir değişiklik veya işlem yaparsanız, bunlar gerçek müşteriler için resmi siparişler olarak değerlendirilir.</span><span class="sxs-lookup"><span data-stu-id="b618d-116">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="b618d-117">Bunlar faturanızda yansıtılır ve şirketiniz bu ücret ödemekten sorumludur.</span><span class="sxs-lookup"><span data-stu-id="b618d-117">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="b618d-118">Tümleştirme korumalı alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="b618d-118">Integration sandbox account</span></span>

<span data-ttu-id="b618d-119">Bu hesap, büyük çapta dağıtmadan önce kodunuzun test edilmesine ve Iş Ortağı Merkezi API 'Leriyle tümleştirilmesine yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="b618d-119">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="b618d-120">Tümleştirme korumalı alanı hesabında oturum açtığınızda yaptığınız değişiklikler ve işlemler faturanızda görünür, ancak fatura tutarını ödemek zorunda değilsiniz.</span><span class="sxs-lookup"><span data-stu-id="b618d-120">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="b618d-121">Fatura PDF 'sine "ödeme yapmayın" olarak bir vazgeçme belgesi sunulacaktır.</span><span class="sxs-lookup"><span data-stu-id="b618d-121">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="b618d-122">BU BIR KORUMALı ALAN FATURADıR VE HERHANGI BIR EYLEM GEREKMEZ. "</span><span class="sxs-lookup"><span data-stu-id="b618d-122">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="b618d-123">Tümleştirme korumalı alanı hesabı ve birincil hesap bağımsız olarak davranır ve yönetici hesaplarını, Kullanıcı hesaplarını, müşterileri, siparişleri, abonelikleri veya diğer verileri paylaşmazlar.</span><span class="sxs-lookup"><span data-stu-id="b618d-123">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="b618d-124">Tümleştirme korumalı alanı, sınırlı sayıda müşteri, sipariş, abonelik, lisans vb. ile işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="b618d-124">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="b618d-125">İlkeye göre, tümleştirme korumalı alanı hesapları yalnızca tümleştirme testi amaçlıdır.</span><span class="sxs-lookup"><span data-stu-id="b618d-125">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="b618d-126">Varsayılan olarak tümleştirme korumalı alan hesabı yoktur.</span><span class="sxs-lookup"><span data-stu-id="b618d-126">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="b618d-127">Iş Ortağı Merkezi SDK 'sını kullanmayı planlıyorsanız bir tane oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b618d-127">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="b618d-128">Hesaplarınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="b618d-128">Set up your accounts</span></span>

<span data-ttu-id="b618d-129">Bu bölümde, Iş Ortağı Merkezi SDK 'Sı için bir birincil Iş ortağı hesabının ve bir tümleştirme korumalı alanı hesabının nasıl ayarlanacağı açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="b618d-129">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="b618d-130">Tümleştirme korumalı alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="b618d-130">Create an integration sandbox</span></span>

1. <span data-ttu-id="b618d-131">Genel yönetici hesabıyla (birincil Iş ortağı hesabınız) Iş ortağı panosunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b618d-131">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="b618d-132">**Ayarlar** menüsünde (dişli simgesi), **iş ortağı ayarları**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-132">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="b618d-133">**Tümleştirme korumalı alanı** sekmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-133">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="b618d-134">Tümleştirme korumalı alanı seçeneğini görmüyorsanız, genel yönetici hesabınız olmayabilir.</span><span class="sxs-lookup"><span data-stu-id="b618d-134">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="b618d-135">Aynı zamanda bir tümleştirme korumalı alanı hesabı kullanıyor olabilirsiniz ve bir tümleştirme korumalı alanı zaten ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="b618d-135">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="b618d-136">Integration Sandbox yönetici hesabı için iletişim bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="b618d-136">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="b618d-137">Ardından **Hesap oluştur**' u seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-137">Then, choose **Create account**.</span></span> <span data-ttu-id="b618d-138">Hesabın oluşturulduğunu belirten bir onay iletisi için birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="b618d-138">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="b618d-139">Onay iletisini görbaşladıktan sonra Iş ortağı panosunun oturumunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="b618d-139">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="b618d-140">Yeni tümleştirme korumalı alanı Yönetici hesabınızla yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b618d-140">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="b618d-141">**username@domain** Kimlik bilgilerinizin biçimini, yeni belirttiğiniz parolayla birlikte kullandığınızdan emin olun.</span><span class="sxs-lookup"><span data-stu-id="b618d-141">Be sure to use the format **username@domain** for your credentials along with the password that you just specified.</span></span>

7. <span data-ttu-id="b618d-142">Korumalı alan hesabı kurulumunu gerçekleştirmek için **geçerli görevlerin** yukarısında **hesabı ayarla** ' yı seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-142">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="b618d-143">API erişimini etkinleştir</span><span class="sxs-lookup"><span data-stu-id="b618d-143">Enable API access</span></span>

<span data-ttu-id="b618d-144">Hesabınız ayarlandıktan sonra, İş Ortağı Merkezi SDK'sını tümleştirme korumalı alanıyla kullanabilmek için öncelikle API erişimini etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="b618d-144">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="b618d-145">Hem birincil İş Ortağı hesabınız hem de tümleştirme korumalı alanı hesabınız için API erişimini ayrı ayrı etkinleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="b618d-145">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="b618d-146">Genel yönetici hesabı kullanarak Iş ortağı panosunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b618d-146">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="b618d-147">**Ayarlar** menüsünde (dişli simgesi), **iş ortağı ayarları**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-147">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="b618d-148">**Hesap ayarları** sayfasında, **uygulama yönetimi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-148">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="b618d-149">Zaten mevcut bir uygulamanız yoksa, yeni bir Web uygulaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="b618d-149">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="b618d-150">Mevcut bir Web uygulamanız varsa **anahtar Ekle** düğmesini seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-150">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="b618d-151">Uygulama kayıt bilgilerini, özellikle de bir Web uygulaması oluşturuyorsanız ve güvenli bir yerde depoluyorsanız bu **anahtarı** kopyalayın.</span><span class="sxs-lookup"><span data-stu-id="b618d-151">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="b618d-152">Iş ortağı panosunun oturumunu kapatın.</span><span class="sxs-lookup"><span data-stu-id="b618d-152">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="b618d-153">Tümleştirme korumalı alanı hesabınızla yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="b618d-153">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="b618d-154">Tümleştirme korumalı alanında API erişimini etkinleştirmek için 2-5 arasındaki adımları yineleyin.</span><span class="sxs-lookup"><span data-stu-id="b618d-154">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="b618d-155">Kod yazın ve test edin</span><span class="sxs-lookup"><span data-stu-id="b618d-155">Write and test code</span></span>

<span data-ttu-id="b618d-156">Tümleştirme korumalı alanında kod ve test kodu yazabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b618d-156">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="b618d-157">Azure AD ile [Iş ortağı merkezi kimlik doğrulamasını ayarlamak](partner-center-authentication.md) için aşağıdaki bilgilere ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="b618d-157">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="b618d-158">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="b618d-158">Item name</span></span> | <span data-ttu-id="b618d-159">Öğe konumu</span><span class="sxs-lookup"><span data-stu-id="b618d-159">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="b618d-160">Uygulama KIMLIĞI/Istemci KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="b618d-160">App ID / Client ID</span></span> | <span data-ttu-id="b618d-161">**Ayarlar** menüsünde (dişli simgesi), **iş ortağı ayarları**' nı seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-161">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="b618d-162">**Hesap ayarları** sayfasında, **uygulama yönetimi**' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="b618d-162">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="b618d-163">Uygulama KIMLIĞI/Istemci KIMLIĞI **kayıtlı uygulama uygulama kimliği** olarak listelenir.</span><span class="sxs-lookup"><span data-stu-id="b618d-163">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="b618d-164">Anahtar</span><span class="sxs-lookup"><span data-stu-id="b618d-164">Key</span></span> | <span data-ttu-id="b618d-165">[API erişimini etkinleştir](#enable-api-access)bölümünde bir Web uygulaması oluşturduysanız, bu, 5. adımda kaydettiğiniz anahtardır.</span><span class="sxs-lookup"><span data-stu-id="b618d-165">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="b618d-166">Etki alanı</span><span class="sxs-lookup"><span data-stu-id="b618d-166">Domain</span></span> | <span data-ttu-id="b618d-167">Tümleştirme korumalı alanı için etki alanı.</span><span class="sxs-lookup"><span data-stu-id="b618d-167">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="b618d-168">Sınanan kodu Çalıştır</span><span class="sxs-lookup"><span data-stu-id="b618d-168">Run tested code</span></span>

<span data-ttu-id="b618d-169">Çözümünüzü gerçek müşteri verileriyle birlikte kullanmak için, tümleştirme korumalı alanı kimlik bilgilerinizle birincil Iş ortağı hesabı kimlik bilgilerinizle değişiklik yapmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="b618d-169">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="b618d-170">Birincil Iş ortağı hesabınızda test ettiğiniz kodu kullanmaya hazırsanız, bir Azure AD güvenlik belirteci almalısınız.</span><span class="sxs-lookup"><span data-stu-id="b618d-170">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="b618d-171">Bu güvenlik belirteci, Iş Ortağı Merkezi uygulamanızı, anahtarınızı ve etki alanınızı temel alır (Tümleştirme korumalı alanı uygulamanız, anahtar ve etki alanınız yerine).</span><span class="sxs-lookup"><span data-stu-id="b618d-171">This security token is based on your Partner Center app, key and domain (instead of your integration sandbox app, key and domain).</span></span>

1. <span data-ttu-id="b618d-172">Birincil Iş ortağı merkezi kimlik bilgilerinizi kullanarak bir Azure AD güvenlik belirteci almak için [Iş ortağı merkezi kimlik doğrulaması](partner-center-authentication.md) içindeki adımları izleyin.</span><span class="sxs-lookup"><span data-stu-id="b618d-172">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="b618d-173">(Daha önce tümleştirme korumalı alanınız için bir Azure AD güvenlik belirteci almak üzere bu adımları izlediyseniz.)</span><span class="sxs-lookup"><span data-stu-id="b618d-173">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="b618d-174">Kodunuzda tümleştirme güvenlik belirtecini, birincil Iş ortağı hesabınızın yeni güvenlik belirteciyle değiştirin.</span><span class="sxs-lookup"><span data-stu-id="b618d-174">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
