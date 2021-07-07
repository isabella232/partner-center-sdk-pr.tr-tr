---
title: Kurumsal Bayi ilişkisi için korumalı alan özellikleri
description: İş ortağı korumalı alanı, iş ortağı ile müşteri arasındaki ilişkileri destekleyene sahip
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: aa6c4fb9ef71bacfad7e0f1510fec15f6af60a05
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111547402"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="ae087-103">Kurumsal Bayi ilişkisi için korumalı alan özellikleri</span><span class="sxs-lookup"><span data-stu-id="ae087-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="ae087-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="ae087-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="ae087-105">Bu makalede iş ortağı ile müşteri arasındaki kurumsal bayi ilişkileri için Korumalı Alan'da desteklenenler açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="ae087-105">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ae087-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="ae087-106">Prerequisites</span></span>

- <span data-ttu-id="ae087-107">İş Ortağı Merkezi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="ae087-107">Partner Center account credentials.</span></span> <span data-ttu-id="ae087-108">Korumalı alan senaryosu hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="ae087-108">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="ae087-109">Müşteri kimliği (customer-tenant-id).</span><span class="sxs-lookup"><span data-stu-id="ae087-109">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="ae087-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard/home)</span><span class="sxs-lookup"><span data-stu-id="ae087-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="ae087-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="ae087-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="ae087-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="ae087-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="ae087-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="ae087-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="ae087-114">Microsoft Kimliği, müşteri kimliği (customer-tenant-id) ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="ae087-114">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="ae087-115">İpucu Azure Ayrılmış Sanal Makine Örnekleri alanından müşteri silmeden önce tüm yazılım satın alma siparişlerini ve yazılım satın alma siparişlerini iptal etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="ae087-115">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="ae087-116">Kurumsal Bayi İlişkisi Destekleyen Senaryolar</span><span class="sxs-lookup"><span data-stu-id="ae087-116">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="ae087-117">Korumalı Alan Doğrudan Fatura İş Ortakları ve Dolaylı Sağlayıcılar, Korumalı Alan müşterisi ile ilişkiler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="ae087-117">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="ae087-118">Korumalı Alan Doğrudan Fatura İş Ortakları ve Dolaylı Sağlayıcılar Korumalı Alan müşterilerini davetamaz.</span><span class="sxs-lookup"><span data-stu-id="ae087-118">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="ae087-119">Korumalı Alan Doğrudan Fatura İş Ortağı ve Dolaylı Sağlayıcılar, kurumsal bayi ilişkisini kullanıcı arabiriminden İş Ortağı Merkezi API'den kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="ae087-119">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="ae087-120">Korumalı Alan Kurumsal Bayi İlişkisi Silme müşteri AP'lerini çağıracak.</span><span class="sxs-lookup"><span data-stu-id="ae087-120">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="ae087-121">Bu, ilişkiyi kaldırır ve müşteri kiracısı silinir.</span><span class="sxs-lookup"><span data-stu-id="ae087-121">This will remove the relationship and delete the customer tenant.</span></span> <span data-ttu-id="ae087-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="ae087-122">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="ae087-123">Korumalı Alanda</span><span class="sxs-lookup"><span data-stu-id="ae087-123">In the Sandbox</span></span>

    <span data-ttu-id="ae087-124">**Doğrudan fatura iş ortakları:**</span><span class="sxs-lookup"><span data-stu-id="ae087-124">**Direct bill partners**:</span></span>

    - <span data-ttu-id="ae087-125">Mevcut müşterileri ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="ae087-125">Can add existing customers</span></span>

    - <span data-ttu-id="ae087-126">Yeni müşterilerle ilişki isteği bulunamaz</span><span class="sxs-lookup"><span data-stu-id="ae087-126">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="ae087-127">**Dolaylı sağlayıcılar:**</span><span class="sxs-lookup"><span data-stu-id="ae087-127">**Indirect providers**:</span></span>

    - <span data-ttu-id="ae087-128">Mevcut müşterileri ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="ae087-128">Can add existing customers</span></span>

    - <span data-ttu-id="ae087-129">Yeni müşterilerle ilişki isteği bulunamaz</span><span class="sxs-lookup"><span data-stu-id="ae087-129">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="ae087-130">Dolaylı kurumsal bayi ile ilişki bulunamaz</span><span class="sxs-lookup"><span data-stu-id="ae087-130">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="ae087-131">**Dolaylı kurumsal bayi:**</span><span class="sxs-lookup"><span data-stu-id="ae087-131">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="ae087-132">Mevcut müşterilerle ilişkileri olabilir</span><span class="sxs-lookup"><span data-stu-id="ae087-132">Can have relationships with existing customers</span></span>

    -   <span data-ttu-id="ae087-133">Yeni ilişkiler isteği veya yeni müşteri ekleme</span><span class="sxs-lookup"><span data-stu-id="ae087-133">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="ae087-134">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="ae087-134">In Partner Center</span></span>

    <span data-ttu-id="ae087-135">**Doğrudan fatura iş ortakları:**</span><span class="sxs-lookup"><span data-stu-id="ae087-135">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="ae087-136">Yeni müşteriler ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="ae087-136">Can add new customers</span></span>

    -   <span data-ttu-id="ae087-137">Yeni müşterilerle ilişki isteğide olabilir</span><span class="sxs-lookup"><span data-stu-id="ae087-137">Can request relationships with new customers</span></span>

    <span data-ttu-id="ae087-138">**Dolaylı sağlayıcılar:**</span><span class="sxs-lookup"><span data-stu-id="ae087-138">**Indirect providers**:</span></span>

    -   <span data-ttu-id="ae087-139">Yeni müşteriler ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="ae087-139">Can add new customers</span></span>

    -   <span data-ttu-id="ae087-140">Yeni müşterilerle ilişki isteğide olabilir</span><span class="sxs-lookup"><span data-stu-id="ae087-140">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="ae087-141">Dolaylı kurumsal bayilerle ilişki olabilir</span><span class="sxs-lookup"><span data-stu-id="ae087-141">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="ae087-142">**Dolaylı kurumsal bayiler:**</span><span class="sxs-lookup"><span data-stu-id="ae087-142">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="ae087-143">Yeni müşteri ekley bilmiyorum</span><span class="sxs-lookup"><span data-stu-id="ae087-143">Can’t add new customers</span></span>

    -   <span data-ttu-id="ae087-144">Yeni müşterilerle ilişki isteğide olabilir</span><span class="sxs-lookup"><span data-stu-id="ae087-144">Can request relationships with new customers</span></span>


<span data-ttu-id="ae087-145">Ayrıntılar için [müşterinin Kurumsal Bayi](remove-a-reseller-relationship-with-a-customer.md) İlişkilerini Kaldır'ı izleyin.</span><span class="sxs-lookup"><span data-stu-id="ae087-145">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="ae087-146">Ancak Product ve Sandbox özellikleri arasında bazı farklar vardır.</span><span class="sxs-lookup"><span data-stu-id="ae087-146">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="ae087-147">İSTEK SÖZ DIZIMI</span><span class="sxs-lookup"><span data-stu-id="ae087-147">REQUEST SYNTAX</span></span>

|<span data-ttu-id="ae087-148">**Yöntem**</span><span class="sxs-lookup"><span data-stu-id="ae087-148">**Method**</span></span>|<span data-ttu-id="ae087-149">**Silme**</span><span class="sxs-lookup"><span data-stu-id="ae087-149">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="ae087-150">Sil</span><span class="sxs-lookup"><span data-stu-id="ae087-150">Delete</span></span>|<span data-ttu-id="ae087-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="ae087-151">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="ae087-152">İstek gövdesi Yok</span><span class="sxs-lookup"><span data-stu-id="ae087-152">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="ae087-153">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="ae087-153">Response success and error codes</span></span>

<span data-ttu-id="ae087-154">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="ae087-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="ae087-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="ae087-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="ae087-156">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](./error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="ae087-156">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae087-157">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="ae087-157">Next steps</span></span>

- [<span data-ttu-id="ae087-158">Azure Market ürünleri için Korumalı alan aboneliklerini etkinleştirme</span><span class="sxs-lookup"><span data-stu-id="ae087-158">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="ae087-159">Korumalı Alandan siparişi iptal etme</span><span class="sxs-lookup"><span data-stu-id="ae087-159">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="ae087-160">Test etme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="ae087-160">Test and debug</span></span>](test-and-debug.md)