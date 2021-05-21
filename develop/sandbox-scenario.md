---
title: Satıcı ilişkisi için korumalı alan özellikleri
description: İş ortağı korumalı alanı, iş ortağı ve müşteri arasındaki ilişkileri destekleyebilir
ms.date: 05/01/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9bef4a15685ebbdc2212988f5ac5724b946cfd54
ms.sourcegitcommit: 1aeaa12705a5945b8aab6bca254fedebd9c8bc4e
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/21/2021
ms.locfileid: "110243393"
---
# <a name="sandbox-capabilities-for-reseller-relationship"></a><span data-ttu-id="45fe4-103">Satıcı ilişkisi için korumalı alan özellikleri</span><span class="sxs-lookup"><span data-stu-id="45fe4-103">Sandbox capabilities for Reseller relationship</span></span>

<span data-ttu-id="45fe4-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="45fe4-104">**Applies to:**</span></span>

- <span data-ttu-id="45fe4-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="45fe4-105">Partner Center</span></span>
- <span data-ttu-id="45fe4-106">21Vianet tarafından çalıştırılan İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="45fe4-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="45fe4-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="45fe4-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="45fe4-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="45fe4-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="45fe4-109">Bu makalede, iş ortağı ve müşteri arasındaki satıcı ilişkileri için korumalı alanda nelerin desteklendiği açıklanır.</span><span class="sxs-lookup"><span data-stu-id="45fe4-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="45fe4-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="45fe4-110">Prerequisites</span></span>

- <span data-ttu-id="45fe4-111">İş Ortağı Merkezi hesabı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="45fe4-111">Partner Center account credentials.</span></span> <span data-ttu-id="45fe4-112">Sandbox senaryosu hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="45fe4-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="45fe4-113">Bir müşteri KIMLIĞI (müşteri-Kiracı kimliği).</span><span class="sxs-lookup"><span data-stu-id="45fe4-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="45fe4-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard/home)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="45fe4-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="45fe4-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="45fe4-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="45fe4-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="45fe4-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="45fe4-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="45fe4-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="45fe4-118">Microsoft KIMLIĞI, müşteri KIMLIĞI (müşteri-Kiracı kimliği) ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="45fe4-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="45fe4-119">Bir müşteri, tıp tümleştirme korumalı alanından silinmeden önce tüm Azure ayrılmış sanal makine örneklerinin ve yazılım satın alma siparişlerinin iptal edilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="45fe4-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="45fe4-120">Satıcı Ilişkisini destekleyen senaryolar</span><span class="sxs-lookup"><span data-stu-id="45fe4-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="45fe4-121">Korumalı alan doğrudan fatura ortakları ve dolaylı sağlayıcılar, Sandbox müşterisi ile ilişkiler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="45fe4-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="45fe4-122">Korumalı alan doğrudan fatura ortakları ve dolaylı sağlayıcılar, korumalı alan müşterilerini davet edemez.</span><span class="sxs-lookup"><span data-stu-id="45fe4-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>

3. <span data-ttu-id="45fe4-123">Korumalı alan doğrudan fatura ortağı ve dolaylı sağlayıcılar, Iş Ortağı Merkezi kullanıcı arabiriminden ve API 'den satıcı ilişkisini kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="45fe4-123">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="45fe4-124">Korumalı alan satıcı Ilişkisini kaldır müşteri AP 'sini Sil ' i çağırır.</span><span class="sxs-lookup"><span data-stu-id="45fe4-124">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="45fe4-125">Bu işlem ilişkiyi kaldırır ve müşteri kiracısını siler.</span><span class="sxs-lookup"><span data-stu-id="45fe4-125">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="45fe4-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span><span class="sxs-lookup"><span data-stu-id="45fe4-126">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>


    ### <a name="in-the-sandbox"></a><span data-ttu-id="45fe4-127">Korumalı Alanda</span><span class="sxs-lookup"><span data-stu-id="45fe4-127">In the Sandbox</span></span>

    <span data-ttu-id="45fe4-128">**Doğrudan fatura iş ortakları:**</span><span class="sxs-lookup"><span data-stu-id="45fe4-128">**Direct bill partners**:</span></span>

    - <span data-ttu-id="45fe4-129">Mevcut müşterileri ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-129">Can add existing customers</span></span>

    - <span data-ttu-id="45fe4-130">Yeni müşterilerle ilişki isteği bulunamaz</span><span class="sxs-lookup"><span data-stu-id="45fe4-130">Cannot request relationships with new customers</span></span>

    <span data-ttu-id="45fe4-131">**Dolaylı sağlayıcılar:**</span><span class="sxs-lookup"><span data-stu-id="45fe4-131">**Indirect providers**:</span></span>

    - <span data-ttu-id="45fe4-132">Mevcut müşterileri ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-132">Can add existing customers</span></span>

    - <span data-ttu-id="45fe4-133">Yeni müşterilerle ilişki isteği bulunamaz</span><span class="sxs-lookup"><span data-stu-id="45fe4-133">Cannot request relationships with new customers</span></span>

    - <span data-ttu-id="45fe4-134">Dolaylı kurumsal bayi ile ilişki bulunamaz</span><span class="sxs-lookup"><span data-stu-id="45fe4-134">Cannot have a relationship with an Indirect reseller</span></span>

    <span data-ttu-id="45fe4-135">**Dolaylı kurumsal bayi:**</span><span class="sxs-lookup"><span data-stu-id="45fe4-135">**Indirect reseller**:</span></span> 

    -   <span data-ttu-id="45fe4-136">Mevcut müşterilerle ilişki olabilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-136">Can have a relationships with existing customers</span></span>

    -   <span data-ttu-id="45fe4-137">Yeni ilişkiler isteği veya yeni müşteri ekleme</span><span class="sxs-lookup"><span data-stu-id="45fe4-137">Cannot request new relationships or add new customers</span></span>

    ### <a name="in-partner-center"></a><span data-ttu-id="45fe4-138">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="45fe4-138">In Partner Center</span></span>

    <span data-ttu-id="45fe4-139">**Doğrudan fatura iş ortakları:**</span><span class="sxs-lookup"><span data-stu-id="45fe4-139">**Direct bill partners**:</span></span>

    -   <span data-ttu-id="45fe4-140">Yeni müşteriler ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-140">Can add new customers</span></span>

    -   <span data-ttu-id="45fe4-141">Yeni müşterilerle ilişki isteğide olabilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-141">Can request relationships with new customers</span></span>

    <span data-ttu-id="45fe4-142">**Dolaylı sağlayıcılar:**</span><span class="sxs-lookup"><span data-stu-id="45fe4-142">**Indirect providers**:</span></span>

    -   <span data-ttu-id="45fe4-143">Yeni müşteriler ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-143">Can add new customers</span></span>

    -   <span data-ttu-id="45fe4-144">Yeni müşterilerle ilişki isteğide olabilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-144">Can request relationships with new customers</span></span>

    -   <span data-ttu-id="45fe4-145">Dolaylı kurumsal bayilerle ilişki olabilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-145">Can have relationships with indirect resellers</span></span>

    <span data-ttu-id="45fe4-146">**Dolaylı satıcılar**:</span><span class="sxs-lookup"><span data-stu-id="45fe4-146">**Indirect resellers**:</span></span>

    -   <span data-ttu-id="45fe4-147">Yeni müşteriler eklenemiyor</span><span class="sxs-lookup"><span data-stu-id="45fe4-147">Can’t add new customers</span></span>

    -   <span data-ttu-id="45fe4-148">Yeni müşterilerle ilişkiler talep edebilir</span><span class="sxs-lookup"><span data-stu-id="45fe4-148">Can request relationships with new customers</span></span>


<span data-ttu-id="45fe4-149">Ayrıntılar için müşterinin [satıcı Ilişkilerini kaldır ilişkisini](remove-a-reseller-relationship-with-a-customer.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="45fe4-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="45fe4-150">Ancak, ürün ve Sandbox özellikleri arasında bazı farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="45fe4-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="45fe4-151">ISTEK SÖZDIZIMI</span><span class="sxs-lookup"><span data-stu-id="45fe4-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="45fe4-152">**Yöntem**</span><span class="sxs-lookup"><span data-stu-id="45fe4-152">**Method**</span></span>|<span data-ttu-id="45fe4-153">**Silme**</span><span class="sxs-lookup"><span data-stu-id="45fe4-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="45fe4-154">Sil</span><span class="sxs-lookup"><span data-stu-id="45fe4-154">Delete</span></span>|<span data-ttu-id="45fe4-155">{baseURL}/v1/Customers/{Customer-Tenant-ID}</span><span class="sxs-lookup"><span data-stu-id="45fe4-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="45fe4-156">İstek gövdesi yok</span><span class="sxs-lookup"><span data-stu-id="45fe4-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="45fe4-157">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="45fe4-157">Response success and error codes</span></span>

<span data-ttu-id="45fe4-158">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="45fe4-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="45fe4-159">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="45fe4-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="45fe4-160">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](./error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="45fe4-160">For the full list, see [Partner Center REST error codes](./error-codes.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="45fe4-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="45fe4-161">Next steps</span></span>

- [<span data-ttu-id="45fe4-162">Azure Market ürünleri için korumalı alan aboneliklerini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="45fe4-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="45fe4-163">Korumalı alan 'dan bir siparişi iptal etme</span><span class="sxs-lookup"><span data-stu-id="45fe4-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="45fe4-164">Test etme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="45fe4-164">Test and debug</span></span>](test-and-debug.md)