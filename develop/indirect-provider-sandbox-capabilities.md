---
title: Sanal alanda CSP dolaylı sağlayıcı özellikleri
description: Dolaylı sağlayıcılar, test amaçları için korumalı alanda dolaylı satıcılar oluşturabilir.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: bd0f38103e6b6f93ab5da386042b00801b683ccd
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2021
ms.locfileid: "110244610"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="7e931-103">Dolaylı satıcı hesapları oluşturmak için CSP dolaylı sağlayıcısı korumalı alanı özellikleri</span><span class="sxs-lookup"><span data-stu-id="7e931-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="7e931-104">**Şunlara uygulanır**</span><span class="sxs-lookup"><span data-stu-id="7e931-104">**Applies to**</span></span>

- <span data-ttu-id="7e931-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7e931-105">Partner Center</span></span>

<span data-ttu-id="7e931-106">**Uygun roller**</span><span class="sxs-lookup"><span data-stu-id="7e931-106">**Appropriate roles**</span></span>

- <span data-ttu-id="7e931-107">Dolaylı sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="7e931-107">Indirect provider</span></span>

<span data-ttu-id="7e931-108">CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı Bayi Sandbox hesabı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-108">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7e931-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7e931-109">Prerequisites</span></span> 

<span data-ttu-id="7e931-110">Partner Center dolaylı sağlayıcısı (katman 2) korumalı alan kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7e931-110">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="7e931-111">Sandbox senaryosu hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7e931-111">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="7e931-112">Korumalı alan dolaylı sağlayıcısı – Iş Ortağı Merkezi Kullanıcı arabirimini kullanarak korumalı alan dolaylı satıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e931-112">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="7e931-113">Bu, korumalı alan dolaylı sağlayıcılarına, Iş Ortağı Merkezi portalından korumalı alan dolaylı satıcı hesabı oluşturma yeteneği sağlayan yalnızca korumalı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="7e931-113">This is a Sandbox- only feature that allows Sandbox Indirect Providers the ability to create Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="7e931-114">Aşağıdaki senaryolar, Iş Ortağı Merkezi kullanıcı arabirimi aracılığıyla korumalı satıcıların dolaylı satıcılarına yönelik olarak ne yapabilecekleri, dolaylı sağlayıcılardır:</span><span class="sxs-lookup"><span data-stu-id="7e931-114">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="7e931-115">CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı Bayi Sandbox hesabı oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-115">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="7e931-116">CSP dolaylı satıcıları, müşteriyi dolaylı sağlayıcılara göre görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-116">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="7e931-117">CSP dolaylı satıcıları, yönetici temsilcisi izinlerini kullanarak müşteri hesabını yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-117">CSP Indirect Resellers  can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="7e931-118">CSP dolaylı sağlayıcıları, CSP dolaylı satıcılarını davet edebilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-118">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="7e931-119">CSP dolaylı sağlayıcıları, Iş Ortağı Merkezi portalındaki kendi katman 2 Sandbox hesabı aracılığıyla bir CSP dolaylı satıcı Sandbox hesabını silebilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-119">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="7e931-120">a.</span><span class="sxs-lookup"><span data-stu-id="7e931-120">a.</span></span>  <span data-ttu-id="7e931-121">Korumalı alan dolaylı sağlayıcısı, korumalı alan dolaylı satıcılarından ilişkiyi siler.</span><span class="sxs-lookup"><span data-stu-id="7e931-121">When Sandbox Indirect Provider deletes relationship with Sandbox Indirect Reseller.</span></span>

    <span data-ttu-id="7e931-122">b.</span><span class="sxs-lookup"><span data-stu-id="7e931-122">b.</span></span>  <span data-ttu-id="7e931-123">Dolaylı satıcının diğer sağlayıcılarla başka bir ilişkiye sahip olup olmadığını denetleyin.</span><span class="sxs-lookup"><span data-stu-id="7e931-123">Check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="7e931-124">Bu durumda, yalnızca söz konusu dolaylı sağlayıcıyla ilişki kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="7e931-124">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="7e931-125">c.</span><span class="sxs-lookup"><span data-stu-id="7e931-125">c.</span></span> <span data-ttu-id="7e931-126">Bu, IR için tek ilişkisidir, IR silinir.</span><span class="sxs-lookup"><span data-stu-id="7e931-126">If that is the only relationship for the IR, then the IR will be deleted.</span></span>

1. <span data-ttu-id="7e931-127">CSP Indirect Provider bir dosyayı CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="7e931-127">CSP Indirect Provider can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="7e931-128">a.</span><span class="sxs-lookup"><span data-stu-id="7e931-128">a.</span></span> <span data-ttu-id="7e931-129">Bu, Korumalı Alan Dolaylı Sağlayıcılarının Korumalı Alan Dolaylı Kurumsal Bayilerini silmesini sağlayan yalnızca korumalı alan özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="7e931-129">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="7e931-130">Korumalı Alan Dolaylı Kurumsal Bayiyi silmek için önkullar:</span><span class="sxs-lookup"><span data-stu-id="7e931-130">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="7e931-131">Korumalı Alan Dolaylı Kurumsal Bayi'nin her müşterisi için abonelikleri askıya alın.</span><span class="sxs-lookup"><span data-stu-id="7e931-131">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="7e931-132">Dolaylı Kurumsal Bayi'nin tüm müşterilerini silin.</span><span class="sxs-lookup"><span data-stu-id="7e931-132">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="7e931-133">Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen 5 Korumalı Alan Dolaylı Kurumsal Bayi sınırı.</span><span class="sxs-lookup"><span data-stu-id="7e931-133">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="7e931-134">Korumalı Alan Dolaylı kurumsal bayisi silindikten sonra kota sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="7e931-134">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="7e931-135">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="7e931-135">Pre-requisites</span></span>

- <span data-ttu-id="7e931-136">Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen 5 Korumalı Alan Dolaylı Kurumsal Bayi sınırı.</span><span class="sxs-lookup"><span data-stu-id="7e931-136">Limit of 5 Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="7e931-137">MPN ID ülke ve Dolaylı Kurumsal Bayi Korumalı Alanı ülke aynı ise birden çok Dolaylı Kurumsal Bayi Korumalı Alanı hesabı oluşturmak için aynı MPN Kimliği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-137">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="7e931-138">Kullanılabilir bir test MPN Kimliğiniz varsa, bunu kullanabilir veya Yammer kanalımız üzerinden MPN kimliklerinin bir [listesini eldeabilirsiniz.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 )</span><span class="sxs-lookup"><span data-stu-id="7e931-138">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="7e931-139">Yammer'a erişiminiz yoksa Yammer sizden erişim istemeyi sorar.</span><span class="sxs-lookup"><span data-stu-id="7e931-139">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="7e931-140">Korumalı Alan Dolaylı Sağlayıcısı başına yalnızca 75 müşteriye izin verilir</span><span class="sxs-lookup"><span data-stu-id="7e931-140">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="7e931-141">Korumalı CSP Indirect Reseller hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="7e931-141">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="7e931-142">Katman 2 İş Ortağı Merkezi hesabı aracılığıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7e931-142">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="7e931-143">Sol menüden Dolaylı Kurumsal Bayiler'e gidin.</span><span class="sxs-lookup"><span data-stu-id="7e931-143">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="7e931-144">"Kurumsal Bayi Korumalı Alanı Ekle" düğmesine tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e931-144">Click on “Add Reseller Sandbox” button.</span></span> 

4. <span data-ttu-id="7e931-145">Hesap kayıt formunu doldurun.</span><span class="sxs-lookup"><span data-stu-id="7e931-145">Fill the account enrollment form.</span></span> <span data-ttu-id="7e931-146">Bu kendi kendine açık bir ifadedir ancak Dolaylı Kurumsal Bayi için korumalı alan hesabı oluşturmakta olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="7e931-146">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="7e931-147">Bu hesap için bir yok etme işlemi olmayacaktır ve siz hesap kaydı tamamlana kadar hemen etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="7e931-147">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="7e931-148">Hesap oluşturulduktan sonra portalda Dolaylı Kurumsal Bayi korumalı alan hesabı için Genel Yönetici kimlik bilgilerini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="7e931-148">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="7e931-149">Bunu hemen kaydetmeyi unutmayın, aksi takdirde dolaylı satıcı korumalı alanı olarak oturum açamazsınız.</span><span class="sxs-lookup"><span data-stu-id="7e931-149">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="7e931-150">Oturumu kapatın ve dolaylı satıcı korumalı alanının yeni kimlik bilgilerini kullanarak Iş Ortağı Merkezi 'nde yeniden oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7e931-150">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="7e931-151">Dolaylı bir satıcı olarak yapabileceğiniz özellikleri keşfedebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7e931-151">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="7e931-152">Bazı şeyler:</span><span class="sxs-lookup"><span data-stu-id="7e931-152">Some things are :</span></span>  

    - <span data-ttu-id="7e931-153">Profilleri yönetme</span><span class="sxs-lookup"><span data-stu-id="7e931-153">Manage profiles</span></span>  

    - <span data-ttu-id="7e931-154">Kullanıcıları ve rolleri yönetme</span><span class="sxs-lookup"><span data-stu-id="7e931-154">Manage users and roles</span></span> 

    - <span data-ttu-id="7e931-155">Dolaylı sağlayıcıları yönetme</span><span class="sxs-lookup"><span data-stu-id="7e931-155">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="7e931-156">CSP korumalı alan müşterilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="7e931-156">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="7e931-157">İlişkileri yönetme</span><span class="sxs-lookup"><span data-stu-id="7e931-157">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="7e931-158">Korumalı alan dolaylı sağlayıcısı – Iş Ortağı Merkezi Kullanıcı arabirimini kullanarak korumalı alan dolaylı satıcısı silme</span><span class="sxs-lookup"><span data-stu-id="7e931-158">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="7e931-159">Bu, korumalı alan dolaylı sağlayıcılarının, Iş Ortağı Merkezi portalı aracılığıyla mevcut bir korumalı alan dolaylı satıcı hesabını silmesine izin veren yalnızca korumalı bir özelliktir.</span><span class="sxs-lookup"><span data-stu-id="7e931-159">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="7e931-160">Korumalı alan dolaylı satıcılarını silmenin önkoşulları:</span><span class="sxs-lookup"><span data-stu-id="7e931-160">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="7e931-161">Kendi CSP dolaylı sağlayıcısı katman 2 Sandbox hesabınızla ilişkili mevcut CSP dolaylı satıcı korumalı alan hesabı.</span><span class="sxs-lookup"><span data-stu-id="7e931-161">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="7e931-162">CSP dolaylı Bayi Sandbox hesabını Sil</span><span class="sxs-lookup"><span data-stu-id="7e931-162">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="7e931-163">Katman 2 Sandbox hesabınızı kullanarak Iş Ortağı Merkezi ' nde oturum açın.</span><span class="sxs-lookup"><span data-stu-id="7e931-163">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="7e931-164">Sol menüden dolaylı satıcılara gidin.</span><span class="sxs-lookup"><span data-stu-id="7e931-164">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="7e931-165">Silmek istediğiniz dolaylı satıcı korumalı alan hesabının yanındaki **satıcı korumalı** alanı bağlantısını Sil ' e tıklayın.</span><span class="sxs-lookup"><span data-stu-id="7e931-165">Click on **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="7e931-166">Dolaylı satıcı korumalı alan hesabı kalıcı olarak silinir ve kurtarılamaz.</span><span class="sxs-lookup"><span data-stu-id="7e931-166">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="7e931-167">API başvuruları</span><span class="sxs-lookup"><span data-stu-id="7e931-167">API references</span></span>

- <span data-ttu-id="7e931-168">Dolaylı satıcı oluştur</span><span class="sxs-lookup"><span data-stu-id="7e931-168">Create Indirect Reseller</span></span> 
- <span data-ttu-id="7e931-169">Dolaylı Bayi Sil</span><span class="sxs-lookup"><span data-stu-id="7e931-169">Delete Indirect Reseller</span></span> 

 

 