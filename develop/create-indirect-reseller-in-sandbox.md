---
title: Sandbox 'de dolaylı satıcı oluşturma
description: API 'Leri kullanarak uçtan uca teste olanak sağlayan korumalı alan dolaylı sağlayıcıları için bilgi sağlar.
ms.date: 5/24/2021
ms.author: vijvala
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 93e26792b66e447a0047bd550f4302c7fca4e87b
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973443"
---
# <a name="create-indirect-reseller-in-sandbox"></a><span data-ttu-id="251d2-103">Sandbox 'de dolaylı satıcı oluşturma</span><span class="sxs-lookup"><span data-stu-id="251d2-103">Create Indirect Reseller in Sandbox</span></span>

<span data-ttu-id="251d2-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="251d2-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany</span></span>

<span data-ttu-id="251d2-105">Bu belgede, korumalı alan dolaylı sağlayıcılarının nasıl oluşturulacağı ve API 'Ler kullanılarak uçtan uca testlerin nasıl etkinleştirileceği gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="251d2-105">This document shows how to create Sandbox Indirect Providers and enable end-to-end testing using APIs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="251d2-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="251d2-106">Prerequisites</span></span>

- <span data-ttu-id="251d2-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="251d2-107">Credentials as described in [Partner Center Authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="251d2-108">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="251d2-108">This scenario supports authentication with App+User credentials.</span></span>

## <a name="csp-indirect-provider"></a><span data-ttu-id="251d2-109">CSP Indirect Provider</span><span class="sxs-lookup"><span data-stu-id="251d2-109">CSP Indirect Provider</span></span>

| <span data-ttu-id="251d2-110">Üretim özellikleri</span><span class="sxs-lookup"><span data-stu-id="251d2-110">Production capabilities</span></span>             | <span data-ttu-id="251d2-111">Korumalı alan özellikleri</span><span class="sxs-lookup"><span data-stu-id="251d2-111">Sandbox capabilities</span></span>                            |
|-------------------------------------|-------------------------------------------------|
| <span data-ttu-id="251d2-112">Son müşteriye dolaylı satıcı üzerinden satış yapın</span><span class="sxs-lookup"><span data-stu-id="251d2-112">Sells through the indirect reseller to the end customer</span></span> | <span data-ttu-id="251d2-113">Desteklenir</span><span class="sxs-lookup"><span data-stu-id="251d2-113">Supported</span></span> |
| <span data-ttu-id="251d2-114">Tüm satış, faturalandırma, sağlama ve yönetim/destek sahibi</span><span class="sxs-lookup"><span data-stu-id="251d2-114">Owns all sales, billing, provisioning, and management/support</span></span> | <span data-ttu-id="251d2-115">Desteklenir</span><span class="sxs-lookup"><span data-stu-id="251d2-115">Supported</span></span> |
| <span data-ttu-id="251d2-116">Satıcılarla iş ortaklığı isteme</span><span class="sxs-lookup"><span data-stu-id="251d2-116">Request a partnership with the resellers</span></span> | <span data-ttu-id="251d2-117">Desteklenir</span><span class="sxs-lookup"><span data-stu-id="251d2-117">Supported</span></span> |
| <span data-ttu-id="251d2-118">Müşterileri satıcıya göre görüntüleme</span><span class="sxs-lookup"><span data-stu-id="251d2-118">View customers by Reseller</span></span> | <span data-ttu-id="251d2-119">Desteklenir</span><span class="sxs-lookup"><span data-stu-id="251d2-119">Supported</span></span> |
| <span data-ttu-id="251d2-120">Satıcılara göre yeni müşteriler ekleyin</span><span class="sxs-lookup"><span data-stu-id="251d2-120">Add new customers by resellers</span></span> | <span data-ttu-id="251d2-121">Desteklenir</span><span class="sxs-lookup"><span data-stu-id="251d2-121">Supported</span></span> |
| <span data-ttu-id="251d2-122">Müşterileri davet et</span><span class="sxs-lookup"><span data-stu-id="251d2-122">Invite customers</span></span> | <span data-ttu-id="251d2-123">Korumalı alanda müşteri ilişkisi isteği desteklenmiyor</span><span class="sxs-lookup"><span data-stu-id="251d2-123">Customer relationship request not supported in Sandbox</span></span> |
| <span data-ttu-id="251d2-124">Korumalı alan dolaylı sağlayıcısı, işlem sırasında g veya s olarak korumalı alan IR (MPN ID) seçebilir</span><span class="sxs-lookup"><span data-stu-id="251d2-124">Sandbox Indirect Provider can select Sandbox IR (MPN ID) as the POR while placing the transaction</span></span> | <span data-ttu-id="251d2-125">Desteklenir</span><span class="sxs-lookup"><span data-stu-id="251d2-125">Supported</span></span> |
| <span data-ttu-id="251d2-126">Üretimde desteklenmez</span><span class="sxs-lookup"><span data-stu-id="251d2-126">Not supported in production</span></span> | <span data-ttu-id="251d2-127">Korumalı alan dolaylı sağlayıcısı, korumalı alan dolaylı satıcısı oluşturabilir</span><span class="sxs-lookup"><span data-stu-id="251d2-127">Sandbox Indirect Provider can create Sandbox Indirect Reseller</span></span> |
| <span data-ttu-id="251d2-128">Korumalı alan MPN KIMLIĞI girilmelidir, ürün MPN KIMLIĞI çalışmayacak</span><span class="sxs-lookup"><span data-stu-id="251d2-128">Sandbox MPN ID should be entered, the product MPN ID will not work</span></span> | <span data-ttu-id="251d2-129">Üretimde desteklenmez</span><span class="sxs-lookup"><span data-stu-id="251d2-129">Not supported in production</span></span> |
| <span data-ttu-id="251d2-130">Üretimde desteklenmez</span><span class="sxs-lookup"><span data-stu-id="251d2-130">Not supported in production</span></span> | <span data-ttu-id="251d2-131">Korumalı alan dolaylı sağlayıcısı, korumalı alan dolaylı Bayi silebilir</span><span class="sxs-lookup"><span data-stu-id="251d2-131">Sandbox Indirect Provider can delete Sandbox Indirect Reseller</span></span> |

## <a name="sandbox-indirect-provider--create-sandbox-indirect-reseller"></a><span data-ttu-id="251d2-132">Korumalı alan dolaylı sağlayıcısı – korumalı alan dolaylı satıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="251d2-132">Sandbox Indirect Provider – Create Sandbox Indirect Reseller</span></span>

<span data-ttu-id="251d2-133">Bu özellik yalnızca korumalı alanda kullanılabilir ve Sandbox dolaylı sağlayıcılarına korumalı alan dolaylı satıcıları oluşturma olanağı sağlar.</span><span class="sxs-lookup"><span data-stu-id="251d2-133">This feature is only available in the Sandbox and gives Sandbox Indirect Providers an ability to create Sandbox Indirect Resellers.</span></span>

1. <span data-ttu-id="251d2-134">Sandbox dolaylı sağlayıcısı başına beş korumalı alan dolaylı satıcıların izin verdiği sınır</span><span class="sxs-lookup"><span data-stu-id="251d2-134">Limit of five Sandbox Indirect Resellers allowed per Sandbox Indirect Provider</span></span>
2. <span data-ttu-id="251d2-135">Korumalı alan dolaylı sağlayıcıları, `associatedPartnerId` korumalı alan dolaylı satıcısı olan müşteriler oluşturabilir</span><span class="sxs-lookup"><span data-stu-id="251d2-135">Sandbox Indirect Providers can create customers with `associatedPartnerId` of Sandbox Indirect Reseller</span></span>
3. <span data-ttu-id="251d2-136">Korumalı alan dolaylı satıcısı oluştururken belirli bir bölgenin [MPN](/partner-center/mpn-create-a-partner-center-account) kimliğini girin.</span><span class="sxs-lookup"><span data-stu-id="251d2-136">Enter the [MPN](/partner-center/mpn-create-a-partner-center-account) ID of a specific region while creating a Sandbox Indirect Reseller.</span></span> <span data-ttu-id="251d2-137">Aynı korumalı alan MPN KIMLIĞIYLE birden çok korumalı alan dolaylı satıcıları oluşturulabilir.</span><span class="sxs-lookup"><span data-stu-id="251d2-137">Multiple Sandbox Indirect Resellers can be created with the same Sandbox MPN ID.</span></span>
4. <span data-ttu-id="251d2-138">Sandbox dolaylı sağlayıcısı başına yalnızca 75 müşteriye izin verilir</span><span class="sxs-lookup"><span data-stu-id="251d2-138">Only 75 customers are allowed per Sandbox Indirect Provider</span></span>

## <a name="sandbox-indirect-resellers--view-customers"></a><span data-ttu-id="251d2-139">Korumalı alan dolaylı satıcıları – müşterileri görüntüleyin</span><span class="sxs-lookup"><span data-stu-id="251d2-139">Sandbox Indirect Resellers – View customers</span></span>

1. <span data-ttu-id="251d2-140">Korumalı alan dolaylı satıcıları, korumalı alan müşterilerinin listesini Sandbox dolaylı sağlayıcılarına göre görüntüleyebilir.</span><span class="sxs-lookup"><span data-stu-id="251d2-140">Sandbox Indirect Resellers can view the list of sandbox customers by Sandbox Indirect providers.</span></span>
2. <span data-ttu-id="251d2-141">Korumalı alan dolaylı satıcıları, yönetici temsilcisi izinlerini kullanarak müşteri hesabını yönetebilir.</span><span class="sxs-lookup"><span data-stu-id="251d2-141">Sandbox Indirect Resellers can manage the customer account by using delegated administrator permissions.</span></span>

## <a name="create-sandbox-indirect-reseller-through-api"></a><span data-ttu-id="251d2-142">API aracılığıyla korumalı alan dolaylı satıcısı oluşturma</span><span class="sxs-lookup"><span data-stu-id="251d2-142">Create Sandbox Indirect Reseller through API</span></span>

### <a name="rest-request"></a><span data-ttu-id="251d2-143">REST isteği</span><span class="sxs-lookup"><span data-stu-id="251d2-143">REST request</span></span>

#### <a name="request-syntax"></a><span data-ttu-id="251d2-144">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="251d2-144">Request syntax</span></span>

| <span data-ttu-id="251d2-145">**Yöntem**</span><span class="sxs-lookup"><span data-stu-id="251d2-145">**Method**</span></span> | <span data-ttu-id="251d2-146">**İstek URI'si**</span><span class="sxs-lookup"><span data-stu-id="251d2-146">**Request URI**</span></span>                                                        |
|------------|------------------------------------------------------------------------|
| <span data-ttu-id="251d2-147">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="251d2-147">**POST**</span></span>   | <span data-ttu-id="251d2-148">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/sandboxındirectbayi</span><span class="sxs-lookup"><span data-stu-id="251d2-148">[*{baseURL}*](partner-center-rest-urls.md)/v1//sandboxIndirectReseller</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="251d2-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="251d2-149">Request headers</span></span>

- <span data-ttu-id="251d2-150">Bu API, ıdempotent (birden çok kez çağırırsanız farklı bir sonuç vermez).</span><span class="sxs-lookup"><span data-stu-id="251d2-150">This API is idempotent (it will not yield a different result if you call it multiple times).</span></span>
- <span data-ttu-id="251d2-151">İstek KIMLIĞI ve bağıntı KIMLIĞI gereklidir.</span><span class="sxs-lookup"><span data-stu-id="251d2-151">A request ID and correlation ID are required.</span></span>
- <span data-ttu-id="251d2-152">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="251d2-152">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="251d2-153">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="251d2-153">Request body</span></span>

<span data-ttu-id="251d2-154">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="251d2-154">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="251d2-155">Özellik</span><span class="sxs-lookup"><span data-stu-id="251d2-155">Property</span></span>             | <span data-ttu-id="251d2-156">Tür</span><span class="sxs-lookup"><span data-stu-id="251d2-156">Type</span></span>           | <span data-ttu-id="251d2-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="251d2-157">Description</span></span>                                      |
|----------------------|----------------|--------------------------------------------------|
| <span data-ttu-id="251d2-158">Mpnıd</span><span class="sxs-lookup"><span data-stu-id="251d2-158">mpnId</span></span>                | <span data-ttu-id="251d2-159">string</span><span class="sxs-lookup"><span data-stu-id="251d2-159">string</span></span>         | <span data-ttu-id="251d2-160">Belirli bir bölgedeki IR için MPN KIMLIĞI</span><span class="sxs-lookup"><span data-stu-id="251d2-160">The MPN ID for the IR in specific region</span></span>         |
| <span data-ttu-id="251d2-161">Kiracı</span><span class="sxs-lookup"><span data-stu-id="251d2-161">tenant</span></span>               | <span data-ttu-id="251d2-162">Sözlük &lt; dizesi, dize&gt;</span><span class="sxs-lookup"><span data-stu-id="251d2-162">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="251d2-163">Oluşturulacak bir hesabı tanımlayan temel bilgilerin toplanması</span><span class="sxs-lookup"><span data-stu-id="251d2-163">Collection of basic information that defines an account to be created</span></span> |
| <span data-ttu-id="251d2-164">legalBusinessProfile</span><span class="sxs-lookup"><span data-stu-id="251d2-164">legalBusinessProfile</span></span> | <span data-ttu-id="251d2-165">Sözlük &lt; dizesi, dize&gt;</span><span class="sxs-lookup"><span data-stu-id="251d2-165">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="251d2-166">Kişi, adres ve ad gibi yasal iş varlığını temsil eden bilgilerin toplanması</span><span class="sxs-lookup"><span data-stu-id="251d2-166">Collection of information that represents the legal business entity such as contact, address, and name</span></span> |
| <span data-ttu-id="251d2-167">organizationProfileLanguage</span><span class="sxs-lookup"><span data-stu-id="251d2-167">organizationProfileLanguage</span></span> | <span data-ttu-id="251d2-168">Sözlük &lt; dizesi, dize&gt;</span><span class="sxs-lookup"><span data-stu-id="251d2-168">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="251d2-169">Kuruluş dil tanımlayıcısı</span><span class="sxs-lookup"><span data-stu-id="251d2-169">The organization language identifier</span></span> |

<span data-ttu-id="251d2-170">Bu tabloda, **kiracı** özniteliğinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="251d2-170">This table describes the required properties in the **tenant** attribute.</span></span>

| <span data-ttu-id="251d2-171">Özellik</span><span class="sxs-lookup"><span data-stu-id="251d2-171">Property</span></span>           | <span data-ttu-id="251d2-172">Tür</span><span class="sxs-lookup"><span data-stu-id="251d2-172">Type</span></span>           | <span data-ttu-id="251d2-173">Açıklama</span><span class="sxs-lookup"><span data-stu-id="251d2-173">Description</span></span>                         |
|--------------------|----------------|-------------------------------------|
| <span data-ttu-id="251d2-174">domainPrefix</span><span class="sxs-lookup"><span data-stu-id="251d2-174">domainPrefix</span></span>       | <span data-ttu-id="251d2-175">Dizisinde eşi</span><span class="sxs-lookup"><span data-stu-id="251d2-175">String; unique</span></span> | <span data-ttu-id="251d2-176">Kiracı hesabı için etki alanı</span><span class="sxs-lookup"><span data-stu-id="251d2-176">Domain for the tenant account</span></span>       |
| <span data-ttu-id="251d2-177">name</span><span class="sxs-lookup"><span data-stu-id="251d2-177">name</span></span>               | <span data-ttu-id="251d2-178">string</span><span class="sxs-lookup"><span data-stu-id="251d2-178">string</span></span>         | <span data-ttu-id="251d2-179">Kiracının kolay adı</span><span class="sxs-lookup"><span data-stu-id="251d2-179">Friendly name of the tenant</span></span>         |
| <span data-ttu-id="251d2-180">displayName</span><span class="sxs-lookup"><span data-stu-id="251d2-180">displayName</span></span>        | <span data-ttu-id="251d2-181">string</span><span class="sxs-lookup"><span data-stu-id="251d2-181">string</span></span>         | <span data-ttu-id="251d2-182">Hesabın görünen adı</span><span class="sxs-lookup"><span data-stu-id="251d2-182">Display name for the account</span></span>        |
| <span data-ttu-id="251d2-183">adminUserName</span><span class="sxs-lookup"><span data-stu-id="251d2-183">adminUserName</span></span>      | <span data-ttu-id="251d2-184">string</span><span class="sxs-lookup"><span data-stu-id="251d2-184">string</span></span>         | <span data-ttu-id="251d2-185">Oturum açma hesabının Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="251d2-185">User name for the account for login</span></span> |
| <span data-ttu-id="251d2-186">adminfirstname</span><span class="sxs-lookup"><span data-stu-id="251d2-186">adminfirstname</span></span>     | <span data-ttu-id="251d2-187">string</span><span class="sxs-lookup"><span data-stu-id="251d2-187">string</span></span>         | <span data-ttu-id="251d2-188">Yönetici Kullanıcı adı</span><span class="sxs-lookup"><span data-stu-id="251d2-188">First Name for the admin user</span></span>       |
| <span data-ttu-id="251d2-189">adminlastname</span><span class="sxs-lookup"><span data-stu-id="251d2-189">adminlastname</span></span>      | <span data-ttu-id="251d2-190">string</span><span class="sxs-lookup"><span data-stu-id="251d2-190">string</span></span>         | <span data-ttu-id="251d2-191">Yönetici Kullanıcı için Soyadı</span><span class="sxs-lookup"><span data-stu-id="251d2-191">Last Name for the admin user</span></span>        |
| <span data-ttu-id="251d2-192">adminAlernateEmail</span><span class="sxs-lookup"><span data-stu-id="251d2-192">adminAlernateEmail</span></span> | <span data-ttu-id="251d2-193">string</span><span class="sxs-lookup"><span data-stu-id="251d2-193">string</span></span>         | <span data-ttu-id="251d2-194">Yönetici Kullanıcı için e-posta</span><span class="sxs-lookup"><span data-stu-id="251d2-194">email for the admin user</span></span>            |
| <span data-ttu-id="251d2-195">ülke</span><span class="sxs-lookup"><span data-stu-id="251d2-195">country</span></span>            | <span data-ttu-id="251d2-196">string</span><span class="sxs-lookup"><span data-stu-id="251d2-196">string</span></span>         | <span data-ttu-id="251d2-197">Hesabın ülkesi</span><span class="sxs-lookup"><span data-stu-id="251d2-197">Country of the account</span></span>              |
| <span data-ttu-id="251d2-198">kültür</span><span class="sxs-lookup"><span data-stu-id="251d2-198">culture</span></span>            | <span data-ttu-id="251d2-199">string</span><span class="sxs-lookup"><span data-stu-id="251d2-199">string</span></span>         | <span data-ttu-id="251d2-200">Hesap için dil tercihi</span><span class="sxs-lookup"><span data-stu-id="251d2-200">Language preference for account</span></span>     |

<span data-ttu-id="251d2-201">Bu tabloda, **legalBusinessProfile** özniteliğinde gerekli özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="251d2-201">This table describes the required properties in the **legalBusinessProfile** attribute.</span></span>

| <span data-ttu-id="251d2-202">Özellik</span><span class="sxs-lookup"><span data-stu-id="251d2-202">Property</span></span>       | <span data-ttu-id="251d2-203">Tür</span><span class="sxs-lookup"><span data-stu-id="251d2-203">Type</span></span>                             | <span data-ttu-id="251d2-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="251d2-204">Description</span></span>                          |
|----------------|----------------------------------|--------------------------------------|
| <span data-ttu-id="251d2-205">Tadı</span><span class="sxs-lookup"><span data-stu-id="251d2-205">companyName</span></span>    | <span data-ttu-id="251d2-206">string</span><span class="sxs-lookup"><span data-stu-id="251d2-206">string</span></span>                           | <span data-ttu-id="251d2-207">Yasal varlık için şirket adı</span><span class="sxs-lookup"><span data-stu-id="251d2-207">Company name for legal entity</span></span>        |
| <span data-ttu-id="251d2-208">adres</span><span class="sxs-lookup"><span data-stu-id="251d2-208">address</span></span>        | <span data-ttu-id="251d2-209">Sözlük &lt; dizesi, dize&gt;</span><span class="sxs-lookup"><span data-stu-id="251d2-209">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="251d2-210">Yasal varlık konumunun adresi</span><span class="sxs-lookup"><span data-stu-id="251d2-210">Address of the legal entity location</span></span> |
| <span data-ttu-id="251d2-211">primaryContact</span><span class="sxs-lookup"><span data-stu-id="251d2-211">primaryContact</span></span> | <span data-ttu-id="251d2-212">Sözlük &lt; dizesi, dize&gt;</span><span class="sxs-lookup"><span data-stu-id="251d2-212">Dictionary&lt;string, string&gt;</span></span> | <span data-ttu-id="251d2-213">Şirketin iletişim ayrıntıları</span><span class="sxs-lookup"><span data-stu-id="251d2-213">Contact details of the company</span></span>       |
| <span data-ttu-id="251d2-214">kültür</span><span class="sxs-lookup"><span data-stu-id="251d2-214">culture</span></span>        | <span data-ttu-id="251d2-215">string</span><span class="sxs-lookup"><span data-stu-id="251d2-215">string</span></span>                           | <span data-ttu-id="251d2-216">Şirket tarafından tercih edilen dil</span><span class="sxs-lookup"><span data-stu-id="251d2-216">Language preferred by the company</span></span>    |

### <a name="request-example"></a><span data-ttu-id="251d2-217">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="251d2-217">Request Example</span></span>

```http
{
    "mpnId": "6363276",
    "tenant": {
        "domainPrefix": "TipIRIntTest705",
        "name": "TipIRIntTest705",
        "displayName": "TipIRIntTest705",
        "adminUserName": "admin",
        "adminFirstName": "TipIRIntTest705",
        "adminLastName": "TipIRIntTest705",
        "adminAlternateEmail": "TipIRIntTest705@test.com",
        "country": "US",
        "culture": "en-us"
    },
    "legalBusinessProfile": {
        "companyName": "TipIRIntTest705",
        "address": {
            "country": "FR",
            "city": "Issy-les-Moulineaux",
            "state": "",
            "addressLine1": "39-41 quai du Président Roosevelt",
            "addressLine2": "",
            "postalCode": "92130"
        },
        "primaryContact": {
            "firstName": "Sandbox",
            "lastName": "Scenario",
            "email": "Sandbox.Scenario@test.com",
            "phoneNumber": "1234567890"
        },
        "culture": "en-US"
    },
    "organizationProfileLanguage": "en"
}
```

### <a name="rest-response"></a><span data-ttu-id="251d2-218">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="251d2-218">REST response</span></span>

<span data-ttu-id="251d2-219">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş korumalı alan IR kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="251d2-219">If successful, this method returns the populated Sandbox IR resource in the response body.</span></span>

```http
{

    "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
    "mpnId": "6363276",
    "tenant": {
        "id": "6f94b119-793c-44c7-862b-c327c9057eab",
        "adminUserAccount": "admin@TipIRIntTest705.onmicrosoft.com",
        "password": "\*\*\*\*\*\*”
    },
    "agreementSignature": {
        "id": "30ac23e7-e200-42cf-a5bc-dd9148cdc632",
        "accountId": "6f94b119-793c-44c7-862b-c327c9057eab",
        "agreementId": "1e18c5b2-e42a-4b84-82c8-d0155aa94c6e",
        "agreementType": "ValueAddedReseller",
        "dateSigned": "2021-02-23T18:10:14.8461137Z",
        "signedByFirstName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserPrincipalName": "Test123@PLAMUATT2NetNewTip.onmicrosoft.com",
        "signedByUserObjectId": "e6e0c29d-acda-4ef2-b370-d37a4e06fb98",
        "signedByUserTenantId": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "attributes": {
            "objectType": "AgreementSignatureResponse"
        }
    },
    "partnerRelationship": {
        "id": "0e195b37-4574-4539-bc42-0e539b9684c0",
        "name": "PLAMUATT2NetNew",
        "relationshipType": "is\_indirect\_reseller\_of",
        "state": "Active",
        "mpnId": "6363276",
        "attributes": {
            "objectType": "PartnerRelationshipResponse"
        }
    }
}
```
