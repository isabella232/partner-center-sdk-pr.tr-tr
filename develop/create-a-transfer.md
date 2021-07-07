---
title: Aktarım oluştur
description: Bir müşteri için aboneliklerin aktarımını oluşturma.
ms.date: 04/10/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: d459a0a96912ab27f312bc73af16af2d4fdb518c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973715"
---
# <a name="create-a-transfer"></a><span data-ttu-id="77dc2-103">Aktarım oluştur</span><span class="sxs-lookup"><span data-stu-id="77dc2-103">Create a transfer</span></span>

## <a name="prerequisites"></a><span data-ttu-id="77dc2-104">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="77dc2-104">Prerequisites</span></span>

- <span data-ttu-id="77dc2-105">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="77dc2-105">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="77dc2-106">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="77dc2-106">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="77dc2-107">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="77dc2-107">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="77dc2-108">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="77dc2-108">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="77dc2-109">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="77dc2-109">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="77dc2-110">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="77dc2-110">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="77dc2-111">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="77dc2-111">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="77dc2-112">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="77dc2-112">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="rest-request"></a><span data-ttu-id="77dc2-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="77dc2-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="77dc2-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="77dc2-114">Request syntax</span></span>

| <span data-ttu-id="77dc2-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="77dc2-115">Method</span></span>   | <span data-ttu-id="77dc2-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="77dc2-116">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="77dc2-117">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="77dc2-117">**POST**</span></span> | <span data-ttu-id="77dc2-118">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/aktarımlar http/1.1</span><span class="sxs-lookup"><span data-stu-id="77dc2-118">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/transfers HTTP/1.1</span></span>                    |

### <a name="uri-parameter"></a><span data-ttu-id="77dc2-119">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="77dc2-119">URI parameter</span></span>

<span data-ttu-id="77dc2-120">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="77dc2-120">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="77dc2-121">Ad</span><span class="sxs-lookup"><span data-stu-id="77dc2-121">Name</span></span>            | <span data-ttu-id="77dc2-122">Tür</span><span class="sxs-lookup"><span data-stu-id="77dc2-122">Type</span></span>     | <span data-ttu-id="77dc2-123">Gerekli</span><span class="sxs-lookup"><span data-stu-id="77dc2-123">Required</span></span> | <span data-ttu-id="77dc2-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="77dc2-124">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="77dc2-125">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="77dc2-125">**customer-id**</span></span> | <span data-ttu-id="77dc2-126">string</span><span class="sxs-lookup"><span data-stu-id="77dc2-126">string</span></span>   | <span data-ttu-id="77dc2-127">Yes</span><span class="sxs-lookup"><span data-stu-id="77dc2-127">Yes</span></span>      | <span data-ttu-id="77dc2-128">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="77dc2-128">A GUID formatted customer-id that identifies the customer.</span></span>             |

### <a name="request-headers"></a><span data-ttu-id="77dc2-129">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="77dc2-129">Request headers</span></span>

<span data-ttu-id="77dc2-130">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="77dc2-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="77dc2-131">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="77dc2-131">Request body</span></span>

<span data-ttu-id="77dc2-132">Bu tablo, istek gövdesinde [Transferentity](transfer-entity-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="77dc2-132">This table describes the [TransferEntity](transfer-entity-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="77dc2-133">Özellik</span><span class="sxs-lookup"><span data-stu-id="77dc2-133">Property</span></span>              | <span data-ttu-id="77dc2-134">Tür</span><span class="sxs-lookup"><span data-stu-id="77dc2-134">Type</span></span>          | <span data-ttu-id="77dc2-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="77dc2-135">Required</span></span>  | <span data-ttu-id="77dc2-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="77dc2-136">Description</span></span>                                                                                |
|-----------------------|---------------|-----------|--------------------------------------------------------------------------------------------|
| <span data-ttu-id="77dc2-137">kimlik</span><span class="sxs-lookup"><span data-stu-id="77dc2-137">id</span></span>                    | <span data-ttu-id="77dc2-138">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-138">string</span></span>        | <span data-ttu-id="77dc2-139">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-139">No</span></span>    | <span data-ttu-id="77dc2-140">TransferEntity başarıyla oluşturulduktan sonra sağlanan bir transferEntity tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-140">A transferEntity identifier that is supplied upon successful creation of the transferEntity.</span></span>                               |
| <span data-ttu-id="77dc2-141">createdTime</span><span class="sxs-lookup"><span data-stu-id="77dc2-141">createdTime</span></span>           | <span data-ttu-id="77dc2-142">DateTime</span><span class="sxs-lookup"><span data-stu-id="77dc2-142">DateTime</span></span>      | <span data-ttu-id="77dc2-143">Hayır</span><span class="sxs-lookup"><span data-stu-id="77dc2-143">No</span></span>    | <span data-ttu-id="77dc2-144">TransferEntity oluşturulduğu tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="77dc2-144">The date the transferEntity was created, in date-time format.</span></span> <span data-ttu-id="77dc2-145">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-145">Applied upon successful creation of the transferEntity.</span></span>      |
| <span data-ttu-id="77dc2-146">Zamanı</span><span class="sxs-lookup"><span data-stu-id="77dc2-146">lastModifiedTime</span></span>      | <span data-ttu-id="77dc2-147">DateTime</span><span class="sxs-lookup"><span data-stu-id="77dc2-147">DateTime</span></span>      | <span data-ttu-id="77dc2-148">Hayır</span><span class="sxs-lookup"><span data-stu-id="77dc2-148">No</span></span>    | <span data-ttu-id="77dc2-149">TransferEntity 'ın son güncelleştirilme tarihi, tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="77dc2-149">The date the transferEntity was last updated, in date-time format.</span></span> <span data-ttu-id="77dc2-150">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-150">Applied upon successful creation of the transferEntity.</span></span> |
| <span data-ttu-id="77dc2-151">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="77dc2-151">lastModifiedUser</span></span>      | <span data-ttu-id="77dc2-152">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-152">string</span></span>        | <span data-ttu-id="77dc2-153">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-153">No</span></span>    | <span data-ttu-id="77dc2-154">Transfer varlığını son güncelleştiren Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-154">The user who last updated the transferEntity.</span></span> <span data-ttu-id="77dc2-155">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-155">Applied upon successful creation of transferEntity.</span></span>                          |
| <span data-ttu-id="77dc2-156">customerName</span><span class="sxs-lookup"><span data-stu-id="77dc2-156">customerName</span></span>          | <span data-ttu-id="77dc2-157">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-157">string</span></span>        | <span data-ttu-id="77dc2-158">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-158">No</span></span>    | <span data-ttu-id="77dc2-159">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-159">Optional.</span></span> <span data-ttu-id="77dc2-160">Abonelikleri aktarılmakta olan müşterinin adı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-160">The name of the customer whose subscriptions are being transferred.</span></span>                                              |
| <span data-ttu-id="77dc2-161">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="77dc2-161">customerTenantId</span></span>      | <span data-ttu-id="77dc2-162">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-162">string</span></span>        | <span data-ttu-id="77dc2-163">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-163">No</span></span>    | <span data-ttu-id="77dc2-164">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="77dc2-164">A GUID formatted customer-id that identifies the customer.</span></span> <span data-ttu-id="77dc2-165">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-165">Applied upon successful creation of the transferEntity.</span></span>         |
| <span data-ttu-id="77dc2-166">partnertenantıd</span><span class="sxs-lookup"><span data-stu-id="77dc2-166">partnertenantid</span></span>       | <span data-ttu-id="77dc2-167">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-167">string</span></span>        | <span data-ttu-id="77dc2-168">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-168">No</span></span>    | <span data-ttu-id="77dc2-169">Ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.</span><span class="sxs-lookup"><span data-stu-id="77dc2-169">A GUID formatted partner-id that identifies the partner.</span></span>                                                                   |
| <span data-ttu-id="77dc2-170">sourcePartnerName</span><span class="sxs-lookup"><span data-stu-id="77dc2-170">sourcePartnerName</span></span>     | <span data-ttu-id="77dc2-171">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-171">string</span></span>        | <span data-ttu-id="77dc2-172">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-172">No</span></span>    | <span data-ttu-id="77dc2-173">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-173">Optional.</span></span> <span data-ttu-id="77dc2-174">Aktarımı başlatan iş ortağının kuruluşun adı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-174">The name of the partner's organization who is initiating the transfer.</span></span>                                           |
| <span data-ttu-id="77dc2-175">Sourcepartnertenantıd</span><span class="sxs-lookup"><span data-stu-id="77dc2-175">sourcePartnerTenantId</span></span> | <span data-ttu-id="77dc2-176">string</span><span class="sxs-lookup"><span data-stu-id="77dc2-176">string</span></span>        | <span data-ttu-id="77dc2-177">Yes</span><span class="sxs-lookup"><span data-stu-id="77dc2-177">Yes</span></span>   | <span data-ttu-id="77dc2-178">Aktarımı başlatan ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.</span><span class="sxs-lookup"><span data-stu-id="77dc2-178">A GUID formatted partner-id that identifies the partner initiating the transfer.</span></span>                                           |
| <span data-ttu-id="77dc2-179">targetPartnerName</span><span class="sxs-lookup"><span data-stu-id="77dc2-179">targetPartnerName</span></span>     | <span data-ttu-id="77dc2-180">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-180">string</span></span>        | <span data-ttu-id="77dc2-181">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-181">No</span></span>    | <span data-ttu-id="77dc2-182">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-182">Optional.</span></span> <span data-ttu-id="77dc2-183">Aktarımın hedeflediği iş ortağının kuruluşun adı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-183">The name of the partner's organization to whom the transfer is targeted.</span></span>                                         |
| <span data-ttu-id="77dc2-184">Targetpartnertenantıd</span><span class="sxs-lookup"><span data-stu-id="77dc2-184">targetPartnerTenantId</span></span> | <span data-ttu-id="77dc2-185">string</span><span class="sxs-lookup"><span data-stu-id="77dc2-185">string</span></span>        | <span data-ttu-id="77dc2-186">Yes</span><span class="sxs-lookup"><span data-stu-id="77dc2-186">Yes</span></span>   | <span data-ttu-id="77dc2-187">Aktarımın hedeflediği ortağı tanımlayan bir GUID biçimli iş ortağı kimliği.</span><span class="sxs-lookup"><span data-stu-id="77dc2-187">A GUID formatted partner-id that identifies the partner to whom the transfer is targeted.</span></span>                                  |
| <span data-ttu-id="77dc2-188">LineItems</span><span class="sxs-lookup"><span data-stu-id="77dc2-188">lineItems</span></span>             | <span data-ttu-id="77dc2-189">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="77dc2-189">Array of objects</span></span> | <span data-ttu-id="77dc2-190">Yes</span><span class="sxs-lookup"><span data-stu-id="77dc2-190">Yes</span></span>| <span data-ttu-id="77dc2-191">Bir [Transferlineıtem](transfer-entity-resources.md#transferlineitem) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="77dc2-191">An Array of [TransferLineItem](transfer-entity-resources.md#transferlineitem) resources.</span></span>                                   |
| <span data-ttu-id="77dc2-192">durum</span><span class="sxs-lookup"><span data-stu-id="77dc2-192">status</span></span>                | <span data-ttu-id="77dc2-193">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-193">string</span></span>        | <span data-ttu-id="77dc2-194">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-194">No</span></span>    | <span data-ttu-id="77dc2-195">TransferEntity durumu.</span><span class="sxs-lookup"><span data-stu-id="77dc2-195">The status of the transferEntity.</span></span> <span data-ttu-id="77dc2-196">Olası değerler şunlardır. "etkin" (silinebilir/gönderilebilir) ve "tamamlandı" (daha önce tamamlanmış).</span><span class="sxs-lookup"><span data-stu-id="77dc2-196">Possible values are "Active" (can be deleted/submitted) and "Completed" (has already been completed).</span></span> <span data-ttu-id="77dc2-197">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-197">Applied upon successful creation of the transferEntity.</span></span>|

<span data-ttu-id="77dc2-198">Bu tablo, istek gövdesinde [Transferlineıtem](transfer-entity-resources.md#transferlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="77dc2-198">This table describes the [TransferLineItem](transfer-entity-resources.md#transferlineitem) properties in the request body.</span></span>

|      <span data-ttu-id="77dc2-199">Özellik</span><span class="sxs-lookup"><span data-stu-id="77dc2-199">Property</span></span>       |            <span data-ttu-id="77dc2-200">Tür</span><span class="sxs-lookup"><span data-stu-id="77dc2-200">Type</span></span>             | <span data-ttu-id="77dc2-201">Gerekli</span><span class="sxs-lookup"><span data-stu-id="77dc2-201">Required</span></span> | <span data-ttu-id="77dc2-202">Açıklama</span><span class="sxs-lookup"><span data-stu-id="77dc2-202">Description</span></span>                                                                                     |
|---------------------|-----------------------------|----------|-------------------------------------------------------------------------------------------------|
| <span data-ttu-id="77dc2-203">kimlik</span><span class="sxs-lookup"><span data-stu-id="77dc2-203">id</span></span>                   | <span data-ttu-id="77dc2-204">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-204">string</span></span>                     | <span data-ttu-id="77dc2-205">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-205">No</span></span>       | <span data-ttu-id="77dc2-206">Aktarım satırı öğesi için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-206">A unique identifier for a transfer line item.</span></span> <span data-ttu-id="77dc2-207">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-207">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="77dc2-208">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="77dc2-208">subscriptionId</span></span>       | <span data-ttu-id="77dc2-209">string</span><span class="sxs-lookup"><span data-stu-id="77dc2-209">string</span></span>                     | <span data-ttu-id="77dc2-210">Yes</span><span class="sxs-lookup"><span data-stu-id="77dc2-210">Yes</span></span>      | <span data-ttu-id="77dc2-211">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-211">The subscription identifier.</span></span>                                                                         |
| <span data-ttu-id="77dc2-212">miktar</span><span class="sxs-lookup"><span data-stu-id="77dc2-212">quantity</span></span>             | <span data-ttu-id="77dc2-213">int</span><span class="sxs-lookup"><span data-stu-id="77dc2-213">int</span></span>                        | <span data-ttu-id="77dc2-214">Hayır</span><span class="sxs-lookup"><span data-stu-id="77dc2-214">No</span></span>       | <span data-ttu-id="77dc2-215">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-215">The number of licenses or instances.</span></span>                                                                 |
| <span data-ttu-id="77dc2-216">Bilimlingcycle</span><span class="sxs-lookup"><span data-stu-id="77dc2-216">billingCycle</span></span>         | <span data-ttu-id="77dc2-217">Nesne</span><span class="sxs-lookup"><span data-stu-id="77dc2-217">Object</span></span>                     | <span data-ttu-id="77dc2-218">Hayır</span><span class="sxs-lookup"><span data-stu-id="77dc2-218">No</span></span>       | <span data-ttu-id="77dc2-219">Geçerli dönem için ayarlanan faturalandırma dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="77dc2-219">The type of billing cycle set for the current period.</span></span>                                                |
| <span data-ttu-id="77dc2-220">friendlyName</span><span class="sxs-lookup"><span data-stu-id="77dc2-220">friendlyName</span></span>         | <span data-ttu-id="77dc2-221">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-221">string</span></span>                     | <span data-ttu-id="77dc2-222">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-222">No</span></span>       | <span data-ttu-id="77dc2-223">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-223">Optional.</span></span> <span data-ttu-id="77dc2-224">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-224">The friendly name for the item defined by the partner to help disambiguate.</span></span>                |
| <span data-ttu-id="77dc2-225">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="77dc2-225">partnerIdOnRecord</span></span>    | <span data-ttu-id="77dc2-226">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-226">string</span></span>                     | <span data-ttu-id="77dc2-227">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-227">No</span></span>       | <span data-ttu-id="77dc2-228">Aktarım kabul edildiğinde gerçekleşen Satınalmadaki iş ortağı kimliği (MPN KIMLIĞI).</span><span class="sxs-lookup"><span data-stu-id="77dc2-228">PartnerId on Record (MPN ID) on the purchase that happens when the transfer is accepted.</span></span>              |
| <span data-ttu-id="77dc2-229">OfferId</span><span class="sxs-lookup"><span data-stu-id="77dc2-229">offerId</span></span>              | <span data-ttu-id="77dc2-230">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-230">string</span></span>                     | <span data-ttu-id="77dc2-231">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-231">No</span></span>       | <span data-ttu-id="77dc2-232">Teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-232">The offer identifier.</span></span>                                                                                |
| <span data-ttu-id="77dc2-233">Addonıtems</span><span class="sxs-lookup"><span data-stu-id="77dc2-233">addonItems</span></span>           | <span data-ttu-id="77dc2-234">**Transferlineıtem** nesnelerinin listesi</span><span class="sxs-lookup"><span data-stu-id="77dc2-234">List of **TransferLineItem** objects</span></span> | <span data-ttu-id="77dc2-235">Hayır</span><span class="sxs-lookup"><span data-stu-id="77dc2-235">No</span></span> | <span data-ttu-id="77dc2-236">Aktarılmakta olan, aktarılan temel abonelikle birlikte aktarılacak olan bir transferEntity satır öğeleri koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="77dc2-236">A collection of transferEntity line items for addons that will be transferred along with the base subscription that is being transferred.</span></span> <span data-ttu-id="77dc2-237">TransferEntity başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="77dc2-237">Applied upon successful creation of the transferEntity.</span></span>|
| <span data-ttu-id="77dc2-238">Transferhatası</span><span class="sxs-lookup"><span data-stu-id="77dc2-238">transferError</span></span>        | <span data-ttu-id="77dc2-239">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-239">string</span></span>                     | <span data-ttu-id="77dc2-240">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-240">No</span></span>       | <span data-ttu-id="77dc2-241">Bir hata varsa transferEntity kabul edildikten sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="77dc2-241">Applied after transferEntity is accepted if there is an error.</span></span>                                        |
| <span data-ttu-id="77dc2-242">durum</span><span class="sxs-lookup"><span data-stu-id="77dc2-242">status</span></span>               | <span data-ttu-id="77dc2-243">dize</span><span class="sxs-lookup"><span data-stu-id="77dc2-243">string</span></span>                     | <span data-ttu-id="77dc2-244">No</span><span class="sxs-lookup"><span data-stu-id="77dc2-244">No</span></span>       | <span data-ttu-id="77dc2-245">TransferEntity içindeki LineItem 'ın durumu.</span><span class="sxs-lookup"><span data-stu-id="77dc2-245">The status of the lineitem in the transferEntity.</span></span>                                                    |

### <a name="request-example"></a><span data-ttu-id="77dc2-246">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="77dc2-246">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="77dc2-247">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="77dc2-247">REST response</span></span>

<span data-ttu-id="77dc2-248">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [Transferenity](transfer-entity-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="77dc2-248">If successful, this method returns the populated [TransferEnity](transfer-entity-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="77dc2-249">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="77dc2-249">Response success and error codes</span></span>

<span data-ttu-id="77dc2-250">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="77dc2-250">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="77dc2-251">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="77dc2-251">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="77dc2-252">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="77dc2-252">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="77dc2-253">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="77dc2-253">Response example</span></span>

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
