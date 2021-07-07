---
title: İş Ortağı Merkezi’nde API erişimini ayarlama
description: Sanal İş Ortağı Merkezi SDK'sı için geliştirme hesapları ayarlayın ve tümleştirme korumalı alanı içinde test olun.
ms.date: 05/29/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 2c564baa9b626ff6ce21f9bcc517902d7cf99244
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547436"
---
# <a name="set-up-api-access-in-partner-center"></a><span data-ttu-id="65665-103">İş Ortağı Merkezi’nde API erişimini ayarlama</span><span class="sxs-lookup"><span data-stu-id="65665-103">Set up API access in Partner Center</span></span>

<span data-ttu-id="65665-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government | İş Ortağı Merkezi Microsoft Bulut Almanya için destek</span><span class="sxs-lookup"><span data-stu-id="65665-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="65665-105">Bu makalede, bu hesaplara karşı geliştirmesi gereken hesaplar İş Ortağı Merkezi SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="65665-105">This article describes the accounts you need to develop against the Partner Center SDK.</span></span> <span data-ttu-id="65665-106">Bu makalede tümleştirme korumalı alanı hesabı oluşturma [ve tümleştirme korumalı alanda](#integration-sandbox-account) test oluşturma da açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="65665-106">This article also explains how to create an [integration sandbox account](#integration-sandbox-account) and test in the integration sandbox.</span></span>

>[!NOTE]
><span data-ttu-id="65665-107">API'lere erişim elde etmek için kiracınız CSP kiracısı olmalı ve dolaylı sağlayıcı veya Doğrudan fatura iş ortağınız olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="65665-107">To get access to APIs, your tenant must be a CSP tenant and you must be either an indirect provider or a Direct bill partner.</span></span>

## <a name="account-definitions"></a><span data-ttu-id="65665-108">Hesap tanımları</span><span class="sxs-lookup"><span data-stu-id="65665-108">Account definitions</span></span>

<span data-ttu-id="65665-109">API tümleştirmenizi tümleştirmenize ve test etmeye yardımcı olmak İş Ortağı Merkezi iki tür hesabı destekler:</span><span class="sxs-lookup"><span data-stu-id="65665-109">To help you integrate and test your API integration, Partner Center supports two kinds of accounts:</span></span>

### <a name="primary-partner-account"></a><span data-ttu-id="65665-110">Birincil İş Ortağı hesabı</span><span class="sxs-lookup"><span data-stu-id="65665-110">Primary Partner account</span></span>

<span data-ttu-id="65665-111">Bu hesap, gerçek müşteriler için gerçek siparişler oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65665-111">This account is where you create real orders for real customers.</span></span> <span data-ttu-id="65665-112">Birincil hesapta oturum asanız, İş Ortağı Merkezi SDK'sı veya İş Ortağı Panosu kullanıcı arabirimini kullanarak herhangi bir değişiklik veya işlem yaptısanız, bunlar gerçek müşteriler için resmi siparişler olarak kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="65665-112">If you make any changes or transactions when you are signed in to the primary account, by using either the Partner Center SDK or the Partner Dashboard UI, they will be treated as official orders for real customers.</span></span> <span data-ttu-id="65665-113">Bunlar faturanıza yansır ve bunlar için ödeme sizin şirketiniz tarafından sorumludur.</span><span class="sxs-lookup"><span data-stu-id="65665-113">They will be reflected in your invoice, and your company is responsible for paying for them.</span></span>

### <a name="integration-sandbox-account"></a><span data-ttu-id="65665-114">Tümleştirme korumalı alanı hesabı</span><span class="sxs-lookup"><span data-stu-id="65665-114">Integration sandbox account</span></span>

<span data-ttu-id="65665-115">Bu hesap, genel olarak dağıtmadan önce kodunuzu ve İş Ortağı Merkezi api'leriyle tümleştirmesini test etmek için.</span><span class="sxs-lookup"><span data-stu-id="65665-115">This account is for testing your code and its integration with the Partner Center APIs before you deploy it broadly.</span></span> <span data-ttu-id="65665-116">Tümleştirme korumalı alanı hesabında oturum asanız yaptığınız değişiklikler ve işlemler faturada görünür, ancak fatura tutarını ödemeniz gerek değildir.</span><span class="sxs-lookup"><span data-stu-id="65665-116">Changes and transactions you make when you are signed into the integration sandbox account will appear in your invoice, however, you do not have to pay the invoice amount.</span></span> <span data-ttu-id="65665-117">Fatura pdf dosyası şu şekilde bir sorumluluk reddine sahip olur: "ÖDEMEYİN.</span><span class="sxs-lookup"><span data-stu-id="65665-117">Invoice pdf will have a disclaimer as "DO NOT PAY.</span></span> <span data-ttu-id="65665-118">BU BIR KORUMALı ALAN FATURASıDıR VE HERHANGI BIR IŞLEM GEREKMEZ."</span><span class="sxs-lookup"><span data-stu-id="65665-118">THIS IS A SANDBOX INVOICE AND NO ACTION IS REQUIRED."</span></span>

<span data-ttu-id="65665-119">Tümleştirme korumalı alanı hesabı ve birincil hesap birbirinden bağımsız olarak hareket eder ve yönetici hesaplarını, kullanıcı hesaplarını, müşterileri, siparişleri, abonelikleri veya diğer verileri paylaşmaz.</span><span class="sxs-lookup"><span data-stu-id="65665-119">The integration sandbox account and the primary account act independently, and do not share admin accounts, user accounts, customers, orders, subscriptions, or other data.</span></span>

<span data-ttu-id="65665-120">Tümleştirme korumalı alanı sınırlı sayıda müşteri, sipariş, abonelik, lisans vb. ile işlemleri destekler.</span><span class="sxs-lookup"><span data-stu-id="65665-120">The integration sandbox supports transactions with a limited number of customers, orders, subscriptions, licenses, etc.</span></span>

<span data-ttu-id="65665-121">İlkeyle, tümleştirme korumalı alanı hesapları yalnızca tümleştirme testi amaçlarına yöneliktir.</span><span class="sxs-lookup"><span data-stu-id="65665-121">By policy, integration sandbox accounts are for integration testing purposes only.</span></span>

<span data-ttu-id="65665-122">Varsayılan olarak tümleştirme korumalı alan hesabı yoktur.</span><span class="sxs-lookup"><span data-stu-id="65665-122">By default, there is no integration sandbox account.</span></span> <span data-ttu-id="65665-123">Bu hesabı kullanmayı planlıyorsanız kendiniz bir tane İş Ortağı Merkezi SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="65665-123">You must create one yourself if you plan to use the Partner Center SDK.</span></span>

## <a name="set-up-your-accounts"></a><span data-ttu-id="65665-124">Hesaplarınızı ayarlama</span><span class="sxs-lookup"><span data-stu-id="65665-124">Set up your accounts</span></span>

<span data-ttu-id="65665-125">Bu bölümde, iş ortağı hesabı için birincil İş Ortağı hesabının ve tümleştirme korumalı alanı hesabının nasıl ayar İş Ortağı Merkezi SDK'sı.</span><span class="sxs-lookup"><span data-stu-id="65665-125">This section describes how to set up a primary Partner account and an integration sandbox account for the Partner Center SDK.</span></span>

### <a name="create-an-integration-sandbox"></a><span data-ttu-id="65665-126">Tümleştirme korumalı alanı oluşturma</span><span class="sxs-lookup"><span data-stu-id="65665-126">Create an integration sandbox</span></span>

1. <span data-ttu-id="65665-127">Genel yönetici hesabıyla (birincil İş ortağı hesabınız) İş Ortağı Panosu'nda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65665-127">Sign in to Partner Dashboard with a global admin account (your primary Partner account.)</span></span>

2. <span data-ttu-id="65665-128">İş ortağı **Ayarlar** (dişli simgesi) İş ortağı **ayarları'ı seçin.**</span><span class="sxs-lookup"><span data-stu-id="65665-128">From the **Settings** menu (gear icon), choose **Partner settings**.</span></span>

3. <span data-ttu-id="65665-129">Tümleştirme **korumalı alanı sekmesini** seçin.</span><span class="sxs-lookup"><span data-stu-id="65665-129">Choose **Integration sandbox** tab.</span></span>

    >[!NOTE]
    ><span data-ttu-id="65665-130">Tümleştirme korumalı alanı seçeneğini görmüyorsanız genel yönetici hesabınız yok olabilir.</span><span class="sxs-lookup"><span data-stu-id="65665-130">If you don't see an Integration sandbox option, you might not have a global admin account.</span></span> <span data-ttu-id="65665-131">Ayrıca bir tümleştirme korumalı alanı hesabı kullanıyor ve tümleştirme korumalı alanı zaten ayarlanmış olabilir.</span><span class="sxs-lookup"><span data-stu-id="65665-131">You also might be using an integration sandbox account and an integration sandbox has already been set up.</span></span>

4. <span data-ttu-id="65665-132">Tümleştirme korumalı alan yönetici hesabının iletişim bilgilerini girin.</span><span class="sxs-lookup"><span data-stu-id="65665-132">Enter the contact information for the integration sandbox admin account.</span></span> <span data-ttu-id="65665-133">Ardından Hesap **oluştur'a seçin.**</span><span class="sxs-lookup"><span data-stu-id="65665-133">Then, choose **Create account**.</span></span> <span data-ttu-id="65665-134">Hesabın oluşturularak ilgili onay iletisi için birkaç dakika bekleyin.</span><span class="sxs-lookup"><span data-stu-id="65665-134">Wait a few minutes for a confirmation message that the account has been created.</span></span>

5. <span data-ttu-id="65665-135">Onay mesajını gördüğünüzde İş Ortağı Panosu'nın oturumlarını açın.</span><span class="sxs-lookup"><span data-stu-id="65665-135">After you see the confirmation message, sign out of Partner Dashboard.</span></span>

6. <span data-ttu-id="65665-136">Yeni tümleştirme korumalı alan yönetici hesabınızla yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65665-136">Sign back in with your new integration sandbox admin account.</span></span> <span data-ttu-id="65665-137">Kimlik bilgileriniz için biçimi **username@domain** ve belirttiğiniz parolayı kullanmayı mutlaka kullanın.</span><span class="sxs-lookup"><span data-stu-id="65665-137">Be sure to use the format **username@domain** for your credentials along with the password that you specified.</span></span>

7. <span data-ttu-id="65665-138">Korumalı **alan hesabı kurulumunu tamamlamak** için Geçerli **Görevler'in** üzerinde Hesabı Ayarla'ya seçin.</span><span class="sxs-lookup"><span data-stu-id="65665-138">Choose **Set Up Account** above **Current Tasks** to complete the sandbox account setup.</span></span>

### <a name="enable-api-access"></a><span data-ttu-id="65665-139">API erişimini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="65665-139">Enable API access</span></span>

<span data-ttu-id="65665-140">Hesabınız ayarlandıktan sonra, İş Ortağı Merkezi SDK'sını tümleştirme korumalı alanıyla kullanabilmek için öncelikle API erişimini etkinleştirmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="65665-140">After your account is set up, you must enable API access before you can use the Partner Center SDK with the integration sandbox.</span></span> <span data-ttu-id="65665-141">Hem birincil İş Ortağı hesabınız hem de tümleştirme korumalı alanı hesabınız için API erişimini ayrı ayrı etkinleştirmelisiniz.</span><span class="sxs-lookup"><span data-stu-id="65665-141">You need to enable access to the API separately for both your primary Partner account and your integration sandbox account.</span></span>

1. <span data-ttu-id="65665-142">Genel yönetici hesabı kullanarak İş Ortağı Panosunda oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65665-142">Sign into Partner Dashboard using a global admin account.</span></span>

2. <span data-ttu-id="65665-143">İş ortağı **Ayarlar** (dişli simgesi) İş ortağı **ayarları'ı seçin.**</span><span class="sxs-lookup"><span data-stu-id="65665-143">From the **Settings** menu (gear icon), select **Partner settings**.</span></span>

3. <span data-ttu-id="65665-144">Hesap ayarları **sayfasında Uygulama** yönetimi'ne **tıklayın.**</span><span class="sxs-lookup"><span data-stu-id="65665-144">On the **Account settings** page, choose **App management**.</span></span>

4. <span data-ttu-id="65665-145">Henüz bir uygulamanız yoksa yeni bir web uygulaması ekleyin.</span><span class="sxs-lookup"><span data-stu-id="65665-145">If you do not already have an existing app, add a new web app.</span></span> <span data-ttu-id="65665-146">Mevcut bir web uygulamanız varsa Anahtar ekle **düğmesini** seçin.</span><span class="sxs-lookup"><span data-stu-id="65665-146">If you have an existing web app, choose the **Add key** button.</span></span>

5. <span data-ttu-id="65665-147">Uygulama kayıt bilgilerini, özellikle  de bir web uygulaması oluşturuyorsanız Anahtar'a kopyalayın ve güvenli bir yerde depolar.</span><span class="sxs-lookup"><span data-stu-id="65665-147">Copy the app registration information, especially the **Key** if you're creating a web app, and store it in a safe place.</span></span>

6. <span data-ttu-id="65665-148">İş Ortağı Panosu'da oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65665-148">Sign out of Partner Dashboard.</span></span>

7. <span data-ttu-id="65665-149">Tümleştirme korumalı alanı hesabınızla yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="65665-149">Sign back in with your integration sandbox account.</span></span> <span data-ttu-id="65665-150">Tümleştirme korumalı alanda API erişimini etkinleştirmek için 2-5. adımları tekrarlayın.</span><span class="sxs-lookup"><span data-stu-id="65665-150">Repeat steps 2-5 to enable API access in the integration sandbox.</span></span>

## <a name="write-and-test-code"></a><span data-ttu-id="65665-151">Kod yazma ve test</span><span class="sxs-lookup"><span data-stu-id="65665-151">Write and test code</span></span>

<span data-ttu-id="65665-152">Tümleştirme korumalı alanı içinde kod yazabilir ve kodu testebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="65665-152">You can write code and test code in the integration sandbox.</span></span> <span data-ttu-id="65665-153">Azure AD ile kimlik doğrulamasını ayarlamak [için İş Ortağı Merkezi](partner-center-authentication.md) bilgilere ihtiyacınız vardır.</span><span class="sxs-lookup"><span data-stu-id="65665-153">You'll need the following information to [set up Partner Center authentication](partner-center-authentication.md) with Azure AD.</span></span>

| <span data-ttu-id="65665-154">Öğe adı</span><span class="sxs-lookup"><span data-stu-id="65665-154">Item name</span></span> | <span data-ttu-id="65665-155">Öğe konumu</span><span class="sxs-lookup"><span data-stu-id="65665-155">Item location</span></span> |
| --------- | ------------- |
| <span data-ttu-id="65665-156">Uygulama Kimliği / İstemci Kimliği</span><span class="sxs-lookup"><span data-stu-id="65665-156">App ID / Client ID</span></span> | <span data-ttu-id="65665-157">İş ortağı **Ayarlar** (dişli simgesi) İş ortağı **ayarları'ı seçin.**</span><span class="sxs-lookup"><span data-stu-id="65665-157">From the **Settings** menu (gear icon), select **Partner settings**.</span></span> <span data-ttu-id="65665-158">Hesap ayarları **sayfasında Uygulama** Yönetimi'ne **tıklayın.**</span><span class="sxs-lookup"><span data-stu-id="65665-158">On the **Account settings** page, select **App Management**.</span></span> <span data-ttu-id="65665-159">Uygulama Kimliği/İstemci Kimliği, Kayıtlı uygulama Uygulama **Kimliği olarak listelenir.**</span><span class="sxs-lookup"><span data-stu-id="65665-159">The App ID/Client ID is listed as the **Registered application App ID**.</span></span> |
| <span data-ttu-id="65665-160">Anahtar</span><span class="sxs-lookup"><span data-stu-id="65665-160">Key</span></span> | <span data-ttu-id="65665-161">API erişimini etkinleştirme bölümünde bir web uygulaması [oluşturduysanız,](#enable-api-access)bu, 5. adımda kaydedilen anahtardır.</span><span class="sxs-lookup"><span data-stu-id="65665-161">If you created a web app in the section [Enable API access](#enable-api-access), this is the key that you saved in step 5.</span></span> |
| <span data-ttu-id="65665-162">Etki alanı</span><span class="sxs-lookup"><span data-stu-id="65665-162">Domain</span></span> | <span data-ttu-id="65665-163">Tümleştirme korumalı alanının etki alanı.</span><span class="sxs-lookup"><span data-stu-id="65665-163">The domain for the integration sandbox.</span></span> |

## <a name="run-tested-code"></a><span data-ttu-id="65665-164">Test edilen kodu çalıştırma</span><span class="sxs-lookup"><span data-stu-id="65665-164">Run tested code</span></span>

<span data-ttu-id="65665-165">Çözümlerinizi gerçek müşteri verileriyle kullanmak için tümleştirme korumalı alan kimlik bilgilerinizle birincil İş Ortağı hesabı kimlik bilgilerinize değişmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="65665-165">To use your solution with real customer data, you must change from your integration sandbox credentials to your primary Partner account credentials.</span></span>

<span data-ttu-id="65665-166">Test edilen kodunuzu birincil İş Ortağı hesabında kullanmaya hazırsanız bir Azure AD güvenlik belirteci alasınız.</span><span class="sxs-lookup"><span data-stu-id="65665-166">When you're ready to use your tested code in your primary Partner account, you must get an Azure AD security token.</span></span> <span data-ttu-id="65665-167">Bu güvenlik belirteci, İş Ortağı Merkezi, anahtar ve etki alanınıza (tümleştirme korumalı alan uygulamanız, anahtarınız ve etki alanınız yerine) dayalıdır.</span><span class="sxs-lookup"><span data-stu-id="65665-167">This security token is based on your Partner Center app, key, and domain (instead of your integration sandbox app, key, and domain).</span></span>

1. <span data-ttu-id="65665-168">Birincil kimlik bilgilerinizi [İş Ortağı Merkezi Azure](partner-center-authentication.md) AD güvenlik belirteci almak için kimlik doğrulaması İş Ortağı Merkezi izleyin.</span><span class="sxs-lookup"><span data-stu-id="65665-168">Follow the steps in [Partner Center authentication](partner-center-authentication.md) to get an Azure AD security token using your primary Partner Center credentials.</span></span> <span data-ttu-id="65665-169">(Tümleştirme korumalı alanınız için Azure AD güvenlik belirteci almak üzere daha önce bu adımları izlediniz.)</span><span class="sxs-lookup"><span data-stu-id="65665-169">(You previously followed these steps to get an Azure AD security token for your integration sandbox.)</span></span>

2. <span data-ttu-id="65665-170">Kodundaki tümleştirme güvenlik belirteci yerine birincil İş Ortağı hesabınız için yeni güvenlik belirteci girin.</span><span class="sxs-lookup"><span data-stu-id="65665-170">Replace the integration security token in your code with the new security token for your primary Partner account.</span></span>
