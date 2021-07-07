---
title: Korumalı Alanda CSP Dolaylı sağlayıcı özellikleri
description: Dolaylı sağlayıcılar, test amacıyla Korumalı Alanda dolaylı kurumsal bayiler oluşturabilir.
ms.date: 05/20/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vinayks-ms
ms.author: vinayks
ms.openlocfilehash: da35dadd4e13247e923259a1cf3a67852f4b9e00
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445910"
---
# <a name="csp-indirect-provider-sandbox-capabilities-for-creating-indirect-reseller-accounts"></a><span data-ttu-id="fb3c7-103">Dolaylı kurumsal bayi hesapları oluşturmak için CSP Dolaylı sağlayıcı korumalı alan özellikleri</span><span class="sxs-lookup"><span data-stu-id="fb3c7-103">CSP Indirect provider sandbox capabilities for creating Indirect reseller accounts</span></span> 

<span data-ttu-id="fb3c7-104">**Uygun roller:** Dolaylı sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="fb3c7-104">**Appropriate roles**: Indirect provider</span></span>

<span data-ttu-id="fb3c7-105">CSP Indirect Providers, CSP Indirect Reseller portalında kendi Katman 2 Korumalı Alan hesabı aracılığıyla İş Ortağı Merkezi oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-105">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account via through their own Tier 2 Sandbox account in Partner Center portal.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="fb3c7-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="fb3c7-106">Prerequisites</span></span> 

<span data-ttu-id="fb3c7-107">İş Ortağı Merkezi Dolaylı Sağlayıcı (Katman 2) korumalı alan kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-107">Partner Center Indirect Provider (Tier 2) sandbox credentials.</span></span> <span data-ttu-id="fb3c7-108">Korumalı alan senaryosu hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span> 
 

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="fb3c7-109">Korumalı Alan Dolaylı Sağlayıcısı – Sanal ağ kullanıcı arabirimini kullanarak İş Ortağı Merkezi Dolaylı Kurumsal Bayi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb3c7-109">Sandbox Indirect Provider – Create Sandbox Indirect Reseller using the Partner Center user interface</span></span> 

 <span data-ttu-id="fb3c7-110">Bu, Korumalı Alan Dolaylı Sağlayıcılarının İş Ortağı Merkezi portal aracılığıyla Korumalı Alan Dolaylı Kurumsal Bayi hesabı oluşturmasını sağlayan yalnızca korumalı İş Ortağı Merkezi özelliktir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-110">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to create a Sandbox Indirect Reseller account through the Partner Center portal.</span></span>

<span data-ttu-id="fb3c7-111">Aşağıdaki senaryolar, Dolaylı sağlayıcıların Korumalı Alan'daki dolaylı kurumsal bayiler için İş Ortağı Merkezi arabirimidir:</span><span class="sxs-lookup"><span data-stu-id="fb3c7-111">The following scenarios are what Indirect providers can do for indirect resellers in Sandbox through the Partner Center user interface:</span></span> 

1. <span data-ttu-id="fb3c7-112">CSP Indirect Providers, CSP Indirect Reseller portalında kendi Katman 2 Korumalı Alan hesabı aracılığıyla İş Ortağı Merkezi oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-112">CSP Indirect Providers can create a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>
2. <span data-ttu-id="fb3c7-113">CSP Indirect Resellers, Dolaylı Sağlayıcılar tarafından müşteriyi görüntülemeyi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-113">CSP Indirect Resellers can view customer by Indirect Providers.</span></span> 

1. <span data-ttu-id="fb3c7-114">CSP Indirect Resellers, temsilcili yönetici izinlerini kullanarak müşteri hesabını yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-114">CSP Indirect Resellers can manage the customer account using delegated admin permissions.</span></span>

1. <span data-ttu-id="fb3c7-115">CSP Dolaylı Sağlayıcıları CSP Dolaylı Kurumsal Bayileri davet ediyor olabilir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-115">CSP Indirect Providers can invite CSP Indirect Resellers.</span></span>
 
1. <span data-ttu-id="fb3c7-116">CSP Dolaylı Sağlayıcıları, CSP Indirect Reseller portalında kendi Katman 2 Korumalı Alan hesabı aracılığıyla İş Ortağı Merkezi silebilir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-116">CSP Indirect Providers can delete a CSP Indirect Reseller Sandbox account through their own Tier 2 Sandbox account in Partner Center portal.</span></span>

    <span data-ttu-id="fb3c7-117">a.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-117">a.</span></span>  <span data-ttu-id="fb3c7-118">Korumalı Alan Dolaylı Sağlayıcısı Korumalı Alan Dolaylı Kurumsal Bayi ile ilişkiyi silse de Dolaylı Kurumsal Bayinin diğer sağlayıcılarla başka bir ilişkisi olup ola bir ilişkisi olup değildir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-118">When Sandbox Indirect Provider deletes the relationship with Sandbox Indirect Reseller, check if the Indirect Reseller has any other relationship with other providers.</span></span> <span data-ttu-id="fb3c7-119">Öyleyse, yalnızca ilgili Dolaylı sağlayıcıyla ilişki kaldırılır.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-119">If so, only the relationship with that specific Indirect provider will be removed.</span></span>

    <span data-ttu-id="fb3c7-120">c.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-120">c.</span></span> <span data-ttu-id="fb3c7-121">Dolaylı Kurumsal Bayi için tek ilişki bu ise Dolaylı Kurumsal Bayi silinir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-121">If that is the only relationship for the Indirect Reseller, then the Indirect Reseller will be deleted.</span></span>

1. <span data-ttu-id="fb3c7-122">CSP Dolaylı Sağlayıcıları bir hesabı CSP Indirect Reseller.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-122">CSP Indirect Providers can delete a CSP Indirect Reseller.</span></span>

    <span data-ttu-id="fb3c7-123">a.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-123">a.</span></span> <span data-ttu-id="fb3c7-124">Bu, Korumalı Alan Dolaylı Sağlayıcılarının Korumalı Alan Dolaylı Kurumsal Bayilerini silmesini sağlayan yalnızca korumalı alan özelliğidir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-124">This is a Sandbox-only feature that allows Sandbox Indirect Providers the ability to delete Sandbox Indirect Resellers.</span></span>
     
1. <span data-ttu-id="fb3c7-125">Korumalı Alan Dolaylı Kurumsal Bayiyi silmek için önkullar:</span><span class="sxs-lookup"><span data-stu-id="fb3c7-125">Pre-requisites for deleting a Sandbox Indirect Reseller:</span></span>

    1. <span data-ttu-id="fb3c7-126">Korumalı Alan Dolaylı Kurumsal Bayi'nin her müşterisi için abonelikleri askıya alın.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-126">Suspend the subscriptions for each customer of Sandbox Indirect Reseller.</span></span>

    1. <span data-ttu-id="fb3c7-127">Dolaylı Kurumsal Bayi'nin tüm müşterilerini silin.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-127">Delete all customers of Indirect Reseller.</span></span>

1. <span data-ttu-id="fb3c7-128">Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen beş Korumalı Alan Dolaylı Kurumsal Bayi sınırı.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-128">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> <span data-ttu-id="fb3c7-129">Korumalı Alan Dolaylı kurumsal bayisi silindikten sonra kota sıfırlanır.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-129">Once the Sandbox Indirect reseller is deleted, the quota will be reset.</span></span>

### <a name="pre-requisites"></a><span data-ttu-id="fb3c7-130">Ön koşullar</span><span class="sxs-lookup"><span data-stu-id="fb3c7-130">Pre-requisites</span></span>

- <span data-ttu-id="fb3c7-131">Korumalı Alan Dolaylı Sağlayıcısı başına izin verilen beş Korumalı Alan Dolaylı Kurumsal Bayi sınırı.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-131">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider.</span></span> 

- <span data-ttu-id="fb3c7-132">MPN ID ülke ve Dolaylı Kurumsal Bayi Korumalı Alanı ülke aynı ise birden çok Dolaylı Kurumsal Bayi Korumalı Alanı hesabı oluşturmak için aynı MPN Kimliği kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-132">Same MPN ID can be used to create multiple Indirect Reseller Sandbox accounts if MPN ID country and Indirect Reseller Sandbox country are same.</span></span> <span data-ttu-id="fb3c7-133">Kullanılabilir bir test MPN Kimliğiniz varsa, bunu kullanabilir veya mpN kimliklerinin listesini Yammer [kanalımız aracılığıyla eldeebilirsiniz.]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 )</span><span class="sxs-lookup"><span data-stu-id="fb3c7-133">If you have a test MPN ID available, you can use it, or you can get a list of MPN IDs through our [Yammer channel]( https://www.yammer.com/cloudpartnercommunity/#/files/929991598080 ).</span></span> <span data-ttu-id="fb3c7-134">Erişim iznine sahip değil Yammer Yammer erişim istemeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-134">If you don’t have access to Yammer, Yammer will ask you to request access.</span></span>
 
- <span data-ttu-id="fb3c7-135">Korumalı Alan Dolaylı Sağlayıcısı başına yalnızca 75 müşteriye izin verilir</span><span class="sxs-lookup"><span data-stu-id="fb3c7-135">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="create-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="fb3c7-136">Korumalı CSP Indirect Reseller hesabı oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb3c7-136">Create CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="fb3c7-137">Katman 2 İş Ortağı Merkezi hesabı aracılığıyla oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-137">Sign into Partner Center via your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="fb3c7-138">Sol menüden Dolaylı Kurumsal Bayiler'e gidin.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-138">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="fb3c7-139">Kurumsal Bayi **Korumalı Alanı Ekle düğmesini** seçin.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-139">Select the **Add Reseller Sandbox** button.</span></span> 

4. <span data-ttu-id="fb3c7-140">Hesap kayıt formunu doldurun.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-140">Fill the account enrollment form.</span></span> <span data-ttu-id="fb3c7-141">Bu kendi kendine açık bir ifadedir ancak Dolaylı Kurumsal Bayi için korumalı alan hesabı oluşturmakta olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-141">It's self-explanatory but remember you are creating a Sandbox account for an Indirect Reseller.</span></span> <span data-ttu-id="fb3c7-142">Bu hesap için bir yok etme işlemi olmayacaktır ve siz hesap kaydı tamamlana kadar hemen etkinleştirilir.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-142">This account won't undergo vetting and will be activated as soon as you finish the account enrollment.</span></span>  

5. <span data-ttu-id="fb3c7-143">Hesap oluşturulduktan sonra portalda Dolaylı Kurumsal Bayi korumalı alan hesabı için Genel Yönetici kimlik bilgilerini alırsınız.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-143">Once the account is created, you will get the Global Admin credentials for the Indirect Reseller sandbox account on the portal.</span></span> <span data-ttu-id="fb3c7-144">Hemen kaydetmeyi unutmayın; aksi takdirde Dolaylı Kurumsal Bayi Korumalı Alanı olarak oturum açamayacaksınız.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-144">Remember to save it immediately,  otherwise, you won't be able to sign in as an Indirect Reseller Sandbox.</span></span> 

6. <span data-ttu-id="fb3c7-145">Dolaylı Kurumsal Bayi Korumalı Alanı'nın İş Ortağı Merkezi kimlik bilgilerini kullanarak oturum açma ve yeniden oturum açma.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-145">Sign out and sign in again to Partner Center using the new credentials for Indirect Reseller Sandbox.</span></span> <span data-ttu-id="fb3c7-146">Dolaylı Kurumsal Bayi olarak sahip olduğunuz özellikleri keşfedin.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-146">Explore the capabilities you can do as an Indirect Reseller.</span></span> <span data-ttu-id="fb3c7-147">Bazı şeyler:</span><span class="sxs-lookup"><span data-stu-id="fb3c7-147">Some things are:</span></span>  

    - <span data-ttu-id="fb3c7-148">Profilleri yönetme</span><span class="sxs-lookup"><span data-stu-id="fb3c7-148">Manage profiles</span></span>  

    - <span data-ttu-id="fb3c7-149">Kullanıcıları ve rolleri yönetme</span><span class="sxs-lookup"><span data-stu-id="fb3c7-149">Manage users and roles</span></span> 

    - <span data-ttu-id="fb3c7-150">Dolaylı Sağlayıcıları Yönetme</span><span class="sxs-lookup"><span data-stu-id="fb3c7-150">Manage Indirect Providers</span></span> 

    - <span data-ttu-id="fb3c7-151">CSP Korumalı Alan müşterilerini yönetme</span><span class="sxs-lookup"><span data-stu-id="fb3c7-151">Manage CSP Sandbox customers</span></span> 

    - <span data-ttu-id="fb3c7-152">İlişkileri yönetme</span><span class="sxs-lookup"><span data-stu-id="fb3c7-152">Manage relationships</span></span>
    
     
## <a name="sandbox-indirect-provider--delete-sandbox-indirect-reseller-using-the-partner-center-user-interface"></a><span data-ttu-id="fb3c7-153">Sandbox Indirect Provider – İş Ortağı Merkezi kullanıcı arabirimini kullanarak Sandbox Indirect Reseller'ı silin</span><span class="sxs-lookup"><span data-stu-id="fb3c7-153">Sandbox Indirect Provider – Delete Sandbox Indirect Reseller using the Partner Center user interface</span></span>

 <span data-ttu-id="fb3c7-154">Bu yalnızca Korumalı Alan özelliğidir ve Korumalı Alan Dolaylı Sağlayıcılarının mevcut Korumalı Alan Dolaylı Kurumsal Bayi hesabını portal üzerinden İş Ortağı Merkezi sağlar.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-154">This is a Sandbox only feature that allows Sandbox Indirect Providers an ability to delete an existing Sandbox Indirect Reseller account via Partner Center portal.</span></span> 

### <a name="pre-requisites-to-delete-sandbox-indirect-reseller"></a><span data-ttu-id="fb3c7-155">Korumalı alan Dolaylı kurumsal bayiyi silmek için önkullar:</span><span class="sxs-lookup"><span data-stu-id="fb3c7-155">Pre-requisites to delete sandbox Indirect reseller:</span></span>

<span data-ttu-id="fb3c7-156">Kendi CSP Indirect Reseller Katman 2 Korumalı Alan hesabınızla CSP Indirect Provider bir korumalı alan hesabı.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-156">An existing CSP Indirect Reseller Sandbox account associated with your own CSP Indirect Provider Tier-2 Sandbox account.</span></span>  
 

## <a name="delete-csp-indirect-reseller-sandbox-account"></a><span data-ttu-id="fb3c7-157">Korumalı CSP Indirect Reseller hesabını silme</span><span class="sxs-lookup"><span data-stu-id="fb3c7-157">Delete CSP Indirect Reseller Sandbox account</span></span>

1. <span data-ttu-id="fb3c7-158">Katman 2 İş Ortağı Merkezi kullanarak oturum açın.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-158">Sign into Partner Center using your Tier 2 Sandbox account.</span></span> 

2. <span data-ttu-id="fb3c7-159">Sol menüden Dolaylı Kurumsal Bayiler'e gidin.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-159">Navigate to Indirect Resellers from the left menu.</span></span> 

3. <span data-ttu-id="fb3c7-160">Silmek **istediğiniz Dolaylı Kurumsal Bayi** Korumalı Alanı hesabının yanındaki Kurumsal Bayi Korumalı Alanı Sil bağlantısını seçin.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-160">Select the **Delete Reseller Sandbox** link next to the Indirect Reseller Sandbox account you want to delete.</span></span> <span data-ttu-id="fb3c7-161">Dolaylı Kurumsal Bayi Korumalı Alanı hesabı kalıcı olarak silinir ve kurtarılamaz.</span><span class="sxs-lookup"><span data-stu-id="fb3c7-161">The Indirect Reseller Sandbox account will be permanently deleted and cannot be recovered.</span></span> 

## <a name="api-references"></a><span data-ttu-id="fb3c7-162">API başvuruları</span><span class="sxs-lookup"><span data-stu-id="fb3c7-162">API references</span></span>

- <span data-ttu-id="fb3c7-163">Dolaylı Kurumsal Bayi oluşturma</span><span class="sxs-lookup"><span data-stu-id="fb3c7-163">Create Indirect Reseller</span></span> 
- <span data-ttu-id="fb3c7-164">Dolaylı Kurumsal Bayiyi silme</span><span class="sxs-lookup"><span data-stu-id="fb3c7-164">Delete Indirect Reseller</span></span> 

 

 