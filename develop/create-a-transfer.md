---
title: Aktarım oluştur
description: Bir müşteri için aboneliklerin aktarımını oluşturma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d5e70cc5b7ce4fcfa715f581a2151f0b8d1922b0
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768830"
---
# <a name="create-a-transfer"></a><span data-ttu-id="99eef-103">Aktarım oluştur</span><span class="sxs-lookup"><span data-stu-id="99eef-103">Create a transfer</span></span>

<span data-ttu-id="99eef-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="99eef-104">**Applies to:**</span></span>

- <span data-ttu-id="99eef-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="99eef-105">Partner Center</span></span>

## <a name="prerequisites"></a><span data-ttu-id="99eef-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="99eef-106">Prerequisites</span></span>

- <span data-ttu-id="99eef-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="99eef-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="99eef-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="99eef-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="99eef-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="99eef-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="99eef-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="99eef-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="99eef-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="99eef-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="99eef-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="99eef-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="99eef-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="99eef-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="99eef-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="99eef-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="99eef-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="99eef-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="99eef-116">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="99eef-116">Request syntax</span></span>

| <span data-ttu-id="99eef-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="99eef-117">Method</span></span>   | <span data-ttu-id="99eef-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="99eef-118">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="99eef-119">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="99eef-119">**POST**</span></span> | <span data-ttu-id="99eef-120">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/aktarımlar http/1.1</span><span class="sxs-lookup"><span data-stu-id="99eef-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="99eef-121">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="99eef-121">URI parameter</span></span>

<span data-ttu-id="99eef-122">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="99eef-122">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="99eef-123">Ad</span><span class="sxs-lookup"><span data-stu-id="99eef-123">Name</span></span>            | <span data-ttu-id="99eef-124">Tür</span><span class="sxs-lookup"><span data-stu-id="99eef-124">Type</span></span>     | <span data-ttu-id="99eef-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="99eef-125">Required</span></span> | <span data-ttu-id="99eef-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="99eef-126">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="99eef-127">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="99eef-127">**customer-id**</span></span> | <span data-ttu-id="99eef-128">string</span><span class="sxs-lookup"><span data-stu-id="99eef-128">string</span></span>   | <span data-ttu-id="99eef-129">Yes</span><span class="sxs-lookup"><span data-stu-id="99eef-129">Yes</span></span>      | <span data-ttu-id="99eef-130">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="99eef-130">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="99eef-131">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="99eef-131">Request headers</span></span>

<span data-ttu-id="99eef-132">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="99eef-132">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="99eef-133">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="99eef-133">Request body</span></span>

<span data-ttu-id="99eef-134">Bu tablo, istek gövdesinde [Transferentity](transfer-entity-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="99eef-134">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="99eef-135">Özellik</span><span class="sxs-lookup"><span data-stu-id="99eef-135">Property</span></span>              | <span data-ttu-id="99eef-136">Tür</span><span class="sxs-lookup"><span data-stu-id="99eef-136">Type</span></span>          | <span data-ttu-id="99eef-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="99eef-137">Required</span></span>  | <span data-ttu-id="99eef-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="99eef-138">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="99eef-139">kimlik</span><span class="sxs-lookup"><span data-stu-id="99eef-139">id</span></span>                    | <span data-ttu-id="99eef-140">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-140">string</span></span>        | <span data-ttu-id="99eef-141">No</span><span class="sxs-lookup"><span data-stu-id="99eef-141">No</span></span>    | <span data-ttu-id="99eef-142">TransferEntity başarıyla oluşturulduktan sonra sağlanan bir transferEntity tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="99eef-142">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="99eef-143">createdTime</span><span class="sxs-lookup"><span data-stu-id="99eef-143">createdTime</span></span>           | <span data-ttu-id="99eef-144">DateTime</span><span class="sxs-lookup"><span data-stu-id="99eef-144">DateTime</span></span>      | <span data-ttu-id="99eef-145">No</span><span class="sxs-lookup"><span data-stu-id="99eef-145">No</span></span>    | <span data-ttu-id="99eef-146">TransferEntity oluşturulduğu tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="99eef-146">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="99eef-147">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-147">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="99eef-148">Zamanı</span><span class="sxs-lookup"><span data-stu-id="99eef-148">lastModifiedTime</span></span>      | <span data-ttu-id="99eef-149">DateTime</span><span class="sxs-lookup"><span data-stu-id="99eef-149">DateTime</span></span>      | <span data-ttu-id="99eef-150">No</span><span class="sxs-lookup"><span data-stu-id="99eef-150">No</span></span>    | <span data-ttu-id="99eef-151">TransferEntity 'ın son güncelleştirilme tarihi, tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="99eef-151">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="99eef-152">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-152">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="99eef-153">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="99eef-153">lastModifiedUser</span></span>      | <span data-ttu-id="99eef-154">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-154">string</span></span>        | <span data-ttu-id="99eef-155">No</span><span class="sxs-lookup"><span data-stu-id="99eef-155">No</span></span>    | <span data-ttu-id="99eef-156">Transfer varlığını son güncelleştiren Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="99eef-156">The user who last updated the transferEntity.</span></span> <span data-ttu-id="99eef-157">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-157">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="99eef-158">customerName</span><span class="sxs-lookup"><span data-stu-id="99eef-158">customerName</span></span>          | <span data-ttu-id="99eef-159">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-159">string</span></span>        | <span data-ttu-id="99eef-160">No</span><span class="sxs-lookup"><span data-stu-id="99eef-160">No</span></span>    | <span data-ttu-id="99eef-161">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="99eef-161">Optional.</span></span> <span data-ttu-id="99eef-162">Abonelikleri aktarılmakta olan müşterinin adı.</span><span class="sxs-lookup"><span data-stu-id="99eef-162">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="99eef-163">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="99eef-163">customerTenantId</span></span>      | <span data-ttu-id="99eef-164">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-164">string</span></span>        | <span data-ttu-id="99eef-165">No</span><span class="sxs-lookup"><span data-stu-id="99eef-165">No</span></span>    | <span data-ttu-id="99eef-166">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="99eef-166">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="99eef-167">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-167">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="99eef-168">partnertenantıd</span><span class="sxs-lookup"><span data-stu-id="99eef-168">partnertenantid</span></span>       | <span data-ttu-id="99eef-169">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-169">string</span></span>        | <span data-ttu-id="99eef-170">No</span><span class="sxs-lookup"><span data-stu-id="99eef-170">No</span></span>    | <span data-ttu-id="99eef-171">Ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.</span><span class="sxs-lookup"><span data-stu-id="99eef-171">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="99eef-172">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="99eef-172">sourcePartnerName</span></span>     | <span data-ttu-id="99eef-173">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-173">string</span></span>        | <span data-ttu-id="99eef-174">No</span><span class="sxs-lookup"><span data-stu-id="99eef-174">No</span></span>    | <span data-ttu-id="99eef-175">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="99eef-175">Optional.</span></span> <span data-ttu-id="99eef-176">Aktarımı başlatan iş ortağının kuruluşun adı.</span><span class="sxs-lookup"><span data-stu-id="99eef-176">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="99eef-177">Sourcepartnertenantıd</span><span class="sxs-lookup"><span data-stu-id="99eef-177">sourcePartnerTenantId</span></span> | <span data-ttu-id="99eef-178">string</span><span class="sxs-lookup"><span data-stu-id="99eef-178">string</span></span>        | <span data-ttu-id="99eef-179">Yes</span><span class="sxs-lookup"><span data-stu-id="99eef-179">Yes</span></span>   | <span data-ttu-id="99eef-180">Aktarımı başlatan ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.</span><span class="sxs-lookup"><span data-stu-id="99eef-180">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="99eef-181">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="99eef-181">targetPartnerName</span></span>     | <span data-ttu-id="99eef-182">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-182">string</span></span>        | <span data-ttu-id="99eef-183">No</span><span class="sxs-lookup"><span data-stu-id="99eef-183">No</span></span>    | <span data-ttu-id="99eef-184">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="99eef-184">Optional.</span></span> <span data-ttu-id="99eef-185">Aktarımın hedeflediği iş ortağının kuruluşun adı.</span><span class="sxs-lookup"><span data-stu-id="99eef-185">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="99eef-186">Targetpartnertenantıd</span><span class="sxs-lookup"><span data-stu-id="99eef-186">targetPartnerTenantId</span></span> | <span data-ttu-id="99eef-187">string</span><span class="sxs-lookup"><span data-stu-id="99eef-187">string</span></span>        | <span data-ttu-id="99eef-188">Yes</span><span class="sxs-lookup"><span data-stu-id="99eef-188">Yes</span></span>   | <span data-ttu-id="99eef-189">Aktarımın hedeflediği ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.</span><span class="sxs-lookup"><span data-stu-id="99eef-189">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="99eef-190">LineItems</span><span class="sxs-lookup"><span data-stu-id="99eef-190">lineItems</span></span>             | <span data-ttu-id="99eef-191">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="99eef-191">Array of objects</span></span> | <span data-ttu-id="99eef-192">Yes</span><span class="sxs-lookup"><span data-stu-id="99eef-192">Yes</span></span>| <span data-ttu-id="99eef-193">Bir [Transferlineıtem](transfer-entity-resources.md#transferlineitem) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="99eef-193">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="99eef-194">durum</span><span class="sxs-lookup"><span data-stu-id="99eef-194">status</span></span>                | <span data-ttu-id="99eef-195">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-195">string</span></span>        | <span data-ttu-id="99eef-196">No</span><span class="sxs-lookup"><span data-stu-id="99eef-196">No</span></span>    | <span data-ttu-id="99eef-197">TransferEntity durumu.</span><span class="sxs-lookup"><span data-stu-id="99eef-197">The status of the transferEntity.</span></span> <span data-ttu-id="99eef-198">Olası değerler şunlardır. "etkin" (silinebilir/gönderilebilir) ve "tamamlandı" (daha önce tamamlanmış).</span><span class="sxs-lookup"><span data-stu-id="99eef-198">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="99eef-199">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-199">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="99eef-200">Bu tablo, istek gövdesinde [Transferlineıtem](transfer-entity-resources.md#transferlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="99eef-200">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="99eef-201">Özellik</span><span class="sxs-lookup"><span data-stu-id="99eef-201">Property</span></span>       |            <span data-ttu-id="99eef-202">Tür</span><span class="sxs-lookup"><span data-stu-id="99eef-202">Type</span></span>             | <span data-ttu-id="99eef-203">Gerekli</span><span class="sxs-lookup"><span data-stu-id="99eef-203">Required</span></span> | <span data-ttu-id="99eef-204">Açıklama</span><span class="sxs-lookup"><span data-stu-id="99eef-204">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="99eef-205">kimlik</span><span class="sxs-lookup"><span data-stu-id="99eef-205">id</span></span>                   | <span data-ttu-id="99eef-206">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-206">string</span></span>                     | <span data-ttu-id="99eef-207">No</span><span class="sxs-lookup"><span data-stu-id="99eef-207">No</span></span>       | <span data-ttu-id="99eef-208">Aktarım satırı öğesi için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="99eef-208">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="99eef-209">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-209">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="99eef-210">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="99eef-210">subscriptionId</span></span>       | <span data-ttu-id="99eef-211">string</span><span class="sxs-lookup"><span data-stu-id="99eef-211">string</span></span>                     | <span data-ttu-id="99eef-212">Yes</span><span class="sxs-lookup"><span data-stu-id="99eef-212">Yes</span></span>      | <span data-ttu-id="99eef-213">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="99eef-213">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="99eef-214">miktar</span><span class="sxs-lookup"><span data-stu-id="99eef-214">quantity</span></span>             | <span data-ttu-id="99eef-215">int</span><span class="sxs-lookup"><span data-stu-id="99eef-215">int</span></span>                        | <span data-ttu-id="99eef-216">No</span><span class="sxs-lookup"><span data-stu-id="99eef-216">No</span></span>       | <span data-ttu-id="99eef-217">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="99eef-217">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="99eef-218">Bilimlingcycle</span><span class="sxs-lookup"><span data-stu-id="99eef-218">billingCycle</span></span>         | <span data-ttu-id="99eef-219">Nesne</span><span class="sxs-lookup"><span data-stu-id="99eef-219">Object</span></span>                     | <span data-ttu-id="99eef-220">No</span><span class="sxs-lookup"><span data-stu-id="99eef-220">No</span></span>       | <span data-ttu-id="99eef-221">Geçerli dönem için ayarlanan faturalandırma dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="99eef-221">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="99eef-222">friendlyName</span><span class="sxs-lookup"><span data-stu-id="99eef-222">friendlyName</span></span>         | <span data-ttu-id="99eef-223">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-223">string</span></span>                     | <span data-ttu-id="99eef-224">No</span><span class="sxs-lookup"><span data-stu-id="99eef-224">No</span></span>       | <span data-ttu-id="99eef-225">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="99eef-225">Optional.</span></span> <span data-ttu-id="99eef-226">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="99eef-226">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="99eef-227">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="99eef-227">partnerIdOnRecord</span></span>    | <span data-ttu-id="99eef-228">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-228">string</span></span>                     | <span data-ttu-id="99eef-229">No</span><span class="sxs-lookup"><span data-stu-id="99eef-229">No</span></span>       | <span data-ttu-id="99eef-230">Aktarım kabul edildiğinde gerçekleşen Satınalmadaki iş ortağı kimliği (MPNıD).</span><span class="sxs-lookup"><span data-stu-id="99eef-230">PartnerId on Record (MPNID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="99eef-231">OfferId</span><span class="sxs-lookup"><span data-stu-id="99eef-231">offerId</span></span>              | <span data-ttu-id="99eef-232">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-232">string</span></span>                     | <span data-ttu-id="99eef-233">No</span><span class="sxs-lookup"><span data-stu-id="99eef-233">No</span></span>       | <span data-ttu-id="99eef-234">Teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="99eef-234">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="99eef-235">Addonıtems</span><span class="sxs-lookup"><span data-stu-id="99eef-235">addonItems</span></span>           | <span data-ttu-id="99eef-236">**Transferlineıtem** nesnelerinin listesi</span><span class="sxs-lookup"><span data-stu-id="99eef-236">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="99eef-237">No</span><span class="sxs-lookup"><span data-stu-id="99eef-237">No</span></span> | <span data-ttu-id="99eef-238">Aktarılmakta olan, aktarılan temel abonelikle birlikte aktarılacak olan bir transferEntity satır öğeleri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="99eef-238">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="99eef-239">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-239">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="99eef-240">Transferhatası</span><span class="sxs-lookup"><span data-stu-id="99eef-240">transferError</span></span>        | <span data-ttu-id="99eef-241">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-241">string</span></span>                     | <span data-ttu-id="99eef-242">No</span><span class="sxs-lookup"><span data-stu-id="99eef-242">No</span></span>       | <span data-ttu-id="99eef-243">Bir hata durumunda transferEntity kabul edildikten sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="99eef-243">Applied after transferEntity is accepted in case of an error.</span></span>                                        |
| <span data-ttu-id="99eef-244">durum</span><span class="sxs-lookup"><span data-stu-id="99eef-244">status</span></span>               | <span data-ttu-id="99eef-245">dize</span><span class="sxs-lookup"><span data-stu-id="99eef-245">string</span></span>                     | <span data-ttu-id="99eef-246">No</span><span class="sxs-lookup"><span data-stu-id="99eef-246">No</span></span>       | <span data-ttu-id="99eef-247">TransferEntity içindeki LineItem 'ın durumu.</span><span class="sxs-lookup"><span data-stu-id="99eef-247">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="99eef-248">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="99eef-248">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/transfers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Expect: 100-continue

{
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lineItems": [
        {
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "partnerIdOnRecord": "517285"
        },
        {
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "partnerIdOnRecord": "517285"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="99eef-249">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="99eef-249">REST response</span></span>

<span data-ttu-id="99eef-250">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [Transferenity](transfer-entity-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="99eef-250">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="99eef-251">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="99eef-251">Response success and error codes</span></span>

<span data-ttu-id="99eef-252">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="99eef-252">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="99eef-253">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="99eef-253">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="99eef-254">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="99eef-254">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="99eef-255">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="99eef-255">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 138
Content-Type: application/json; charset=utf-8
MS-RequestId: 4fa6dad6-a89f-4875-8247-7294a10ae1cf
MS-CorrelationId: 0e93c70c-977c-4a88-9580-7cf084c73286
X-Locale: en-US,en-US
{
    "id": "67c5b05b-09b5-47ba-9047-5056fe2afa4f",
    "status": "Active",
    "createdTime": "2020-03-24T20:44:14.9602781Z",
    "lastModifiedTime": "2020-03-24T20:44:15Z",
    "customerTenantId": "823c6c3f-9259-4d51-bae2-5dd06743177f",
    "partnertenantid": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "sourcePartnerTenantId": "da6c51b5-1246-4a42-b4ab-cbf38df54537",
    "targetPartnerTenantId": "656218b1-80c9-40b2-83ae-3a2703b55271",
    "lastModifiedUser": "d0648481-b615-45c9-8cd1-ff87940dbdc4",
    "lineItems": [
        {
            "id": 0,
            "subscriptionId": "7291BFBF-1772-4C5B-A624-18B6152CD8CB",
            "offerId": "50E9A47A-7B4D-4970-9D90-CAE927F53753",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 for Sales Enterprise Attach to Qualifying Dynamics 365 Base Offer",
            "quantity": 1,
            "addonItems": [
                {
                    "id": 0,
                    "subscriptionId": "D738C6C9-DDBD-46E9-B316-65F9D9B3ECB4",
                    "offerId": "2BCF9FE8-8B65-4FCF-9240-419203FB8CF4",
                    "billingCycle": "annual",
                    "friendlyName": "Dynamics 365 - Additional Production Instance (Qualified Offer)",
                    "quantity": 4
                }
            ]
        },
        {
            "id": 0,
            "subscriptionId": "6C0B221B-8DF9-4F4A-A5BB-4C9CBB7B27B0",
            "offerId": "455DDD41-32ED-4E2D-B3A2-BBCB22CAA467",
            "billingCycle": "annual",
            "friendlyName": "Dynamics 365 Customer Engagement Plan Patch",
            "quantity": 8,
            "addonItems": []
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/823c6c3f-9259-4d51-bae2-5dd06743177f/transfers/67c5b05b-09b5-47ba-9047-5056fe2afa4f",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "TransferEntity"
    }
}
```
