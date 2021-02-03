---
title: Satıcı ilişkisini destekleyen iş ortağı korumalı özellikleri
description: İş ortağı korumalı alanı, iş ortağı ve müşteri arasındaki ilişkileri destekleyebilir
ms.date: 11/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e01dd1a83ca459cbdf12b8e564b43a2d18f5595b
ms.sourcegitcommit: f69ceae441bbb2ddba96e878a1ec8c1a499a4879
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 01/13/2021
ms.locfileid: "98180740"
---
# <a name="partner-sandbox-capabilities-that-support-reseller-relationship"></a><span data-ttu-id="34d27-103">Satıcı ilişkisini destekleyen iş ortağı korumalı özellikleri</span><span class="sxs-lookup"><span data-stu-id="34d27-103">Partner sandbox capabilities that support reseller relationship</span></span>

<span data-ttu-id="34d27-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="34d27-104">**Applies to:**</span></span>

- <span data-ttu-id="34d27-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="34d27-105">Partner Center</span></span>
- <span data-ttu-id="34d27-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="34d27-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="34d27-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="34d27-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="34d27-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="34d27-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="34d27-109">Bu makalede, iş ortağı ve müşteri arasındaki satıcı ilişkileri için korumalı alanda nelerin desteklendiği açıklanır.</span><span class="sxs-lookup"><span data-stu-id="34d27-109">This article explains what is supported in the Sandbox for reseller relationships between the partner and the customer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="34d27-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="34d27-110">Prerequisites</span></span>

- <span data-ttu-id="34d27-111">İş Ortağı Merkezi hesabı kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="34d27-111">Partner Center account credentials.</span></span> <span data-ttu-id="34d27-112">Sandbox senaryosu hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="34d27-112">The sandbox scenario supports authentication with both the standalone App and App+User credentials.</span></span>
- <span data-ttu-id="34d27-113">Bir müşteri KIMLIĞI (müşteri-Kiracı kimliği).</span><span class="sxs-lookup"><span data-stu-id="34d27-113">A customer ID (customer-tenant-id).</span></span> <span data-ttu-id="34d27-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard/home)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34d27-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard/home).</span></span> <span data-ttu-id="34d27-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="34d27-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="34d27-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="34d27-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="34d27-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="34d27-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="34d27-118">Microsoft KIMLIĞI, müşteri KIMLIĞI (müşteri-Kiracı kimliği) ile aynıdır.</span><span class="sxs-lookup"><span data-stu-id="34d27-118">The Microsoft ID is the same as the customer ID (customer-tenant-id).</span></span>
- <span data-ttu-id="34d27-119">Bir müşteri, tıp tümleştirme korumalı alanından silinmeden önce tüm Azure ayrılmış sanal makine örneklerinin ve yazılım satın alma siparişlerinin iptal edilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="34d27-119">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="scenarios-supporting-reseller-relationship"></a><span data-ttu-id="34d27-120">Satıcı Ilişkisini destekleyen senaryolar</span><span class="sxs-lookup"><span data-stu-id="34d27-120">Scenarios Supporting Reseller Relationship</span></span>

1.  <span data-ttu-id="34d27-121">Korumalı alan doğrudan fatura ortakları ve dolaylı sağlayıcılar, Sandbox müşterisi ile ilişkiler oluşturabilir.</span><span class="sxs-lookup"><span data-stu-id="34d27-121">Sandbox Direct Bill Partners and Indirect Providers can create relationships with the Sandbox customer.</span></span> 
2.  <span data-ttu-id="34d27-122">Korumalı alan doğrudan fatura ortakları ve dolaylı sağlayıcılar, korumalı alan müşterilerini davet edemez.</span><span class="sxs-lookup"><span data-stu-id="34d27-122">Sandbox Direct Bill Partners and Indirect Providers cannot invite Sandbox customers.</span></span>



### <a name="in-the-sandbox"></a><span data-ttu-id="34d27-123">Korumalı alanda</span><span class="sxs-lookup"><span data-stu-id="34d27-123">In the Sandbox</span></span>

<span data-ttu-id="34d27-124">**Doğrudan fatura ortakları**:</span><span class="sxs-lookup"><span data-stu-id="34d27-124">**Direct bill partners**:</span></span>

<span data-ttu-id="34d27-125">• Mevcut müşteriler eklenebilir</span><span class="sxs-lookup"><span data-stu-id="34d27-125">•   Can add existing customers</span></span>

<span data-ttu-id="34d27-126">• Yeni müşterilerle ilişkiler isteyemezsiniz</span><span class="sxs-lookup"><span data-stu-id="34d27-126">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="34d27-127">**Dolaylı sağlayıcılar**:</span><span class="sxs-lookup"><span data-stu-id="34d27-127">**Indirect providers**:</span></span>

<span data-ttu-id="34d27-128">• Mevcut müşteriler eklenebilir</span><span class="sxs-lookup"><span data-stu-id="34d27-128">•   Can add existing customers</span></span>

<span data-ttu-id="34d27-129">• Yeni müşterilerle ilişkiler isteyemezsiniz</span><span class="sxs-lookup"><span data-stu-id="34d27-129">•   Cannot request relationships with new customers</span></span>

<span data-ttu-id="34d27-130">• Dolaylı bir satıcı ile bir ilişkiye sahip olamaz</span><span class="sxs-lookup"><span data-stu-id="34d27-130">•   Cannot have a relationship with an Indirect reseller</span></span>

<span data-ttu-id="34d27-131">**Dolaylı satıcı**: (çok yakında)</span><span class="sxs-lookup"><span data-stu-id="34d27-131">**Indirect reseller**: (coming soon)</span></span>

<span data-ttu-id="34d27-132">• Mevcut müşterilerle ilişkilerine sahip olabilir</span><span class="sxs-lookup"><span data-stu-id="34d27-132">•   Can have a relationships with existing customers</span></span>

<span data-ttu-id="34d27-133">• Yeni ilişkiler isteyemezsiniz veya yeni müşteriler ekleyemez</span><span class="sxs-lookup"><span data-stu-id="34d27-133">•   Cannot request new relationships or add new customers</span></span>

### <a name="in-partner-center"></a><span data-ttu-id="34d27-134">Iş Ortağı Merkezi 'nde</span><span class="sxs-lookup"><span data-stu-id="34d27-134">In Partner Center</span></span>

<span data-ttu-id="34d27-135">**Doğrudan fatura ortakları**:</span><span class="sxs-lookup"><span data-stu-id="34d27-135">**Direct bill partners**:</span></span>

<span data-ttu-id="34d27-136">• Yeni müşteriler ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="34d27-136">•   Can add new customers</span></span>

<span data-ttu-id="34d27-137">• Yeni müşterilerle ilişkiler talep edebilir</span><span class="sxs-lookup"><span data-stu-id="34d27-137">•   Can request relationships with new customers</span></span>

<span data-ttu-id="34d27-138">**Dolaylı sağlayıcılar**:</span><span class="sxs-lookup"><span data-stu-id="34d27-138">**Indirect providers**:</span></span>

<span data-ttu-id="34d27-139">• Yeni müşteriler ekleyebilir</span><span class="sxs-lookup"><span data-stu-id="34d27-139">•   Can add new customers</span></span>

<span data-ttu-id="34d27-140">• Yeni müşterilerle ilişkiler talep edebilir</span><span class="sxs-lookup"><span data-stu-id="34d27-140">•   Can request relationships with new customers</span></span>

<span data-ttu-id="34d27-141">• Dolaylı satıcılarla ilişkiler alabilir</span><span class="sxs-lookup"><span data-stu-id="34d27-141">•   Can have relationships with indirect resellers</span></span>

<span data-ttu-id="34d27-142">**Dolaylı satıcılar**:</span><span class="sxs-lookup"><span data-stu-id="34d27-142">**Indirect resellers**:</span></span>

<span data-ttu-id="34d27-143">• Yeni müşteriler eklenemiyor</span><span class="sxs-lookup"><span data-stu-id="34d27-143">•   Can’t add new customers</span></span>

<span data-ttu-id="34d27-144">• Yeni müşterilerle ilişkiler talep edebilir</span><span class="sxs-lookup"><span data-stu-id="34d27-144">•   Can request relationships with new customers</span></span>

3. <span data-ttu-id="34d27-145">Korumalı alan doğrudan fatura ortağı ve dolaylı sağlayıcılar, Iş Ortağı Merkezi kullanıcı arabiriminden ve API 'den satıcı ilişkisini kaldırabilir.</span><span class="sxs-lookup"><span data-stu-id="34d27-145">Sandbox Direct Bill Partner and Indirect Providers are able to remove reseller relationship from Partner Center UI and API.</span></span>

4. <span data-ttu-id="34d27-146">Korumalı alan satıcı Ilişkisini kaldır müşteri AP 'sini Sil ' i çağırır.</span><span class="sxs-lookup"><span data-stu-id="34d27-146">Sandbox Remove Reseller Relationship will call Delete customer AP.</span></span> <span data-ttu-id="34d27-147">Bu işlem ilişkiyi kaldırır ve müşteri kiracısını siler.</span><span class="sxs-lookup"><span data-stu-id="34d27-147">This will remove the relationship as well as delete the customer tenant.</span></span> <span data-ttu-id="34d27-148">{baseURL}/v1/Customers/{Customer-Tenant-ID}</span><span class="sxs-lookup"><span data-stu-id="34d27-148">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span>

<span data-ttu-id="34d27-149">Ayrıntılar için müşterinin [satıcı Ilişkilerini kaldır ilişkisini](remove-a-reseller-relationship-with-a-customer.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="34d27-149">Follow the [Remove Reseller Relationship](remove-a-reseller-relationship-with-a-customer.md) for the customer for details.</span></span> <span data-ttu-id="34d27-150">Ancak, ürün ve Sandbox özellikleri arasında bazı farklılıklar vardır.</span><span class="sxs-lookup"><span data-stu-id="34d27-150">However, there are some differences between the Product and Sandbox capabilities.</span></span>

### <a name="request-syntax"></a><span data-ttu-id="34d27-151">ISTEK SÖZDIZIMI</span><span class="sxs-lookup"><span data-stu-id="34d27-151">REQUEST SYNTAX</span></span>

|<span data-ttu-id="34d27-152">**Yöntem**</span><span class="sxs-lookup"><span data-stu-id="34d27-152">**Method**</span></span>|<span data-ttu-id="34d27-153">**Silme**</span><span class="sxs-lookup"><span data-stu-id="34d27-153">**Delete**</span></span>|
|-------------|------------|
|<span data-ttu-id="34d27-154">Sil</span><span class="sxs-lookup"><span data-stu-id="34d27-154">Delete</span></span>|<span data-ttu-id="34d27-155">{baseURL}/v1/Customers/{Customer-Tenant-ID}</span><span class="sxs-lookup"><span data-stu-id="34d27-155">{baseURL}/v1/Customers/{customer-Tenant-id}</span></span> |

<span data-ttu-id="34d27-156">İstek gövdesi yok</span><span class="sxs-lookup"><span data-stu-id="34d27-156">Request body None</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="34d27-157">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="34d27-157">Response success and error codes</span></span>

<span data-ttu-id="34d27-158">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="34d27-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="34d27-159">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="34d27-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="34d27-160">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](https://docs.microsoft.com/partner-center/develop/error-codes).</span><span class="sxs-lookup"><span data-stu-id="34d27-160">For the full list, see [Partner Center REST error codes](https://docs.microsoft.com/partner-center/develop/error-codes).</span></span>

## <a name="next-steps"></a><span data-ttu-id="34d27-161">Sonraki adımlar</span><span class="sxs-lookup"><span data-stu-id="34d27-161">Next steps</span></span>

- [<span data-ttu-id="34d27-162">Azure Market ürünleri için korumalı alan aboneliklerini etkinleştirin</span><span class="sxs-lookup"><span data-stu-id="34d27-162">Activate Sandbox subscriptions for Azure Marketplace products</span></span>](activate-sandbox-subscription-azure-marketplace-products.md)

- [<span data-ttu-id="34d27-163">Korumalı alan 'dan bir siparişi iptal etme</span><span class="sxs-lookup"><span data-stu-id="34d27-163">Cancel an order from Sandbox</span></span>](cancel-an-order-from-the-integration-sandbox.md)

- [<span data-ttu-id="34d27-164">Test etme ve hata ayıklama</span><span class="sxs-lookup"><span data-stu-id="34d27-164">Test and debug</span></span>](test-and-debug.md) 
