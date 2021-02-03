---
title: Tarih veya koşullara göre gruplandırılmış abonelik analizlerini al
description: Tarih veya koşullara göre gruplanmış abonelik Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4a9946027fa89f5a93fff5eede86e36a6be5b721
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769052"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="7043d-103">Tarih veya koşullara göre gruplandırılmış abonelik analizlerini al</span><span class="sxs-lookup"><span data-stu-id="7043d-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="7043d-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="7043d-104">**Applies To**</span></span>

- <span data-ttu-id="7043d-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7043d-105">Partner Center</span></span>
- <span data-ttu-id="7043d-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7043d-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7043d-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7043d-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7043d-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7043d-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7043d-109">Müşterilerinizin tarihlere veya terimlere göre gruplanmış abonelik Analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="7043d-109">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7043d-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7043d-110">Prerequisites</span></span>

- <span data-ttu-id="7043d-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7043d-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7043d-112">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7043d-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="7043d-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7043d-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7043d-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7043d-114">Request syntax</span></span>

| <span data-ttu-id="7043d-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7043d-115">Method</span></span> | <span data-ttu-id="7043d-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7043d-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="7043d-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="7043d-117">**GET**</span></span> | <span data-ttu-id="7043d-118">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri? GroupBy = {groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="7043d-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="7043d-119">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="7043d-119">URI parameters</span></span>

<span data-ttu-id="7043d-120">Kuruluşunuzu tanımlamak ve sonuçları gruplandırmak için aşağıdaki gerekli yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7043d-120">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="7043d-121">Ad</span><span class="sxs-lookup"><span data-stu-id="7043d-121">Name</span></span> | <span data-ttu-id="7043d-122">Tür</span><span class="sxs-lookup"><span data-stu-id="7043d-122">Type</span></span> | <span data-ttu-id="7043d-123">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7043d-123">Required</span></span> | <span data-ttu-id="7043d-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7043d-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="7043d-125">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="7043d-125">groupby_queries</span></span> | <span data-ttu-id="7043d-126">dizeler ve tarih saat çiftleri</span><span class="sxs-lookup"><span data-stu-id="7043d-126">pairs of strings and dateTime</span></span> | <span data-ttu-id="7043d-127">Yes</span><span class="sxs-lookup"><span data-stu-id="7043d-127">Yes</span></span> | <span data-ttu-id="7043d-128">Sonucu filtrelemek için hüküm ve tarihler.</span><span class="sxs-lookup"><span data-stu-id="7043d-128">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="7043d-129">GroupBy sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7043d-129">GroupBy syntax</span></span>

<span data-ttu-id="7043d-130">Group By parametresi bir dizi virgülle ayrılmış, alan değeri olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="7043d-130">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="7043d-131">Kodlanamayan bir örnek şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="7043d-131">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="7043d-132">Aşağıdaki tabloda Group by için desteklenen alanların listesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="7043d-132">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="7043d-133">Alan</span><span class="sxs-lookup"><span data-stu-id="7043d-133">Field</span></span> | <span data-ttu-id="7043d-134">Tür</span><span class="sxs-lookup"><span data-stu-id="7043d-134">Type</span></span> | <span data-ttu-id="7043d-135">Description</span><span class="sxs-lookup"><span data-stu-id="7043d-135">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="7043d-136">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="7043d-136">customerTenantId</span></span> | <span data-ttu-id="7043d-137">string</span><span class="sxs-lookup"><span data-stu-id="7043d-137">string</span></span> | <span data-ttu-id="7043d-138">Müşteri kiracısını tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="7043d-138">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="7043d-139">customerName</span><span class="sxs-lookup"><span data-stu-id="7043d-139">customerName</span></span> | <span data-ttu-id="7043d-140">string</span><span class="sxs-lookup"><span data-stu-id="7043d-140">string</span></span> | <span data-ttu-id="7043d-141">Müşterinin adı.</span><span class="sxs-lookup"><span data-stu-id="7043d-141">The name of the customer.</span></span> |
| <span data-ttu-id="7043d-142">customerMarket</span><span class="sxs-lookup"><span data-stu-id="7043d-142">customerMarket</span></span> | <span data-ttu-id="7043d-143">string</span><span class="sxs-lookup"><span data-stu-id="7043d-143">string</span></span> | <span data-ttu-id="7043d-144">Müşterinin iş üzerinde kullandığı ülke/bölge.</span><span class="sxs-lookup"><span data-stu-id="7043d-144">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="7043d-145">kimlik</span><span class="sxs-lookup"><span data-stu-id="7043d-145">id</span></span> | <span data-ttu-id="7043d-146">string</span><span class="sxs-lookup"><span data-stu-id="7043d-146">string</span></span> | <span data-ttu-id="7043d-147">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="7043d-147">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="7043d-148">durum</span><span class="sxs-lookup"><span data-stu-id="7043d-148">status</span></span> | <span data-ttu-id="7043d-149">string</span><span class="sxs-lookup"><span data-stu-id="7043d-149">string</span></span> | <span data-ttu-id="7043d-150">Abonelik durumu.</span><span class="sxs-lookup"><span data-stu-id="7043d-150">The subscription status.</span></span> <span data-ttu-id="7043d-151">Desteklenen değerler şunlardır: "ETKIN", "askıya ALıNDı" veya "SAĞLAMASı KALDıRıLDı".</span><span class="sxs-lookup"><span data-stu-id="7043d-151">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="7043d-152">productName</span><span class="sxs-lookup"><span data-stu-id="7043d-152">productName</span></span> | <span data-ttu-id="7043d-153">string</span><span class="sxs-lookup"><span data-stu-id="7043d-153">string</span></span> | <span data-ttu-id="7043d-154">Ürünün adı.</span><span class="sxs-lookup"><span data-stu-id="7043d-154">The name of the product.</span></span> |
| <span data-ttu-id="7043d-155">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="7043d-155">subscriptionType</span></span> | <span data-ttu-id="7043d-156">string</span><span class="sxs-lookup"><span data-stu-id="7043d-156">string</span></span> | <span data-ttu-id="7043d-157">Abonelik türü.</span><span class="sxs-lookup"><span data-stu-id="7043d-157">The subscription type.</span></span> <span data-ttu-id="7043d-158">Note: Bu alan, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="7043d-158">Note: This field is case sensitive.</span></span> <span data-ttu-id="7043d-159">Desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="7043d-159">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="7043d-160">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="7043d-160">autoRenewEnabled</span></span> | <span data-ttu-id="7043d-161">Boole</span><span class="sxs-lookup"><span data-stu-id="7043d-161">Boolean</span></span> | <span data-ttu-id="7043d-162">Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer.</span><span class="sxs-lookup"><span data-stu-id="7043d-162">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="7043d-163">iş ortağı kimliği</span><span class="sxs-lookup"><span data-stu-id="7043d-163">partnerId</span></span>  | <span data-ttu-id="7043d-164">string</span><span class="sxs-lookup"><span data-stu-id="7043d-164">string</span></span> | <span data-ttu-id="7043d-165">MPN KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="7043d-165">The MPN ID.</span></span> <span data-ttu-id="7043d-166">Doğrudan satıcı için, bu parametre ortağın MPN KIMLIĞI olur.</span><span class="sxs-lookup"><span data-stu-id="7043d-166">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="7043d-167">Dolaylı bir satıcı için, bu parametre dolaylı satıcıdan MPN KIMLIĞI olacaktır.</span><span class="sxs-lookup"><span data-stu-id="7043d-167">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="7043d-168">friendlyName</span><span class="sxs-lookup"><span data-stu-id="7043d-168">friendlyName</span></span> | <span data-ttu-id="7043d-169">string</span><span class="sxs-lookup"><span data-stu-id="7043d-169">string</span></span> | <span data-ttu-id="7043d-170">Aboneliğin adı.</span><span class="sxs-lookup"><span data-stu-id="7043d-170">The name of the subscription.</span></span> |
| <span data-ttu-id="7043d-171">partnerName</span><span class="sxs-lookup"><span data-stu-id="7043d-171">partnerName</span></span> | <span data-ttu-id="7043d-172">string</span><span class="sxs-lookup"><span data-stu-id="7043d-172">string</span></span> | <span data-ttu-id="7043d-173">Aboneliğin satın alındığı ortağın adı</span><span class="sxs-lookup"><span data-stu-id="7043d-173">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="7043d-174">Adı</span><span class="sxs-lookup"><span data-stu-id="7043d-174">providerName</span></span> | <span data-ttu-id="7043d-175">string</span><span class="sxs-lookup"><span data-stu-id="7043d-175">string</span></span> | <span data-ttu-id="7043d-176">Abonelik işlemi dolaylı satıcı için olduğunda, sağlayıcı adı aboneliği satın alan dolaylı sağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="7043d-176">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="7043d-177">creationDate</span><span class="sxs-lookup"><span data-stu-id="7043d-177">creationDate</span></span> | <span data-ttu-id="7043d-178">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-178">string in UTC date time format</span></span> | <span data-ttu-id="7043d-179">Aboneliğin oluşturulduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="7043d-179">The date the subscription was created.</span></span> |
| <span data-ttu-id="7043d-180">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="7043d-180">effectiveStartDate</span></span> | <span data-ttu-id="7043d-181">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-181">string in UTC date time format</span></span> | <span data-ttu-id="7043d-182">Aboneliğin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="7043d-182">The date the subscription starts.</span></span> |
| <span data-ttu-id="7043d-183">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="7043d-183">commitmentEndDate</span></span> | <span data-ttu-id="7043d-184">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-184">string in UTC date time format</span></span> | <span data-ttu-id="7043d-185">Aboneliğin bitiş tarihi.</span><span class="sxs-lookup"><span data-stu-id="7043d-185">The date the subscription ends.</span></span> |
| <span data-ttu-id="7043d-186">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="7043d-186">currentStateEndDate</span></span> | <span data-ttu-id="7043d-187">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-187">string in UTC date time format</span></span> | <span data-ttu-id="7043d-188">Aboneliğin geçerli durumunun değiştirileceği tarih.</span><span class="sxs-lookup"><span data-stu-id="7043d-188">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="7043d-189">Trialtopaıdconversiondate</span><span class="sxs-lookup"><span data-stu-id="7043d-189">trialToPaidConversionDate</span></span> | <span data-ttu-id="7043d-190">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-190">string in UTC date time format</span></span> | <span data-ttu-id="7043d-191">Aboneliğin deneme sürümünden ücretli olarak dönüştürdüğü tarih.</span><span class="sxs-lookup"><span data-stu-id="7043d-191">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="7043d-192">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="7043d-192">The default value is null.</span></span> |
| <span data-ttu-id="7043d-193">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="7043d-193">trialStartDate</span></span> | <span data-ttu-id="7043d-194">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-194">string in UTC date time format</span></span> | <span data-ttu-id="7043d-195">Abonelik için deneme süresinin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="7043d-195">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="7043d-196">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="7043d-196">The default value is null.</span></span> |
| <span data-ttu-id="7043d-197">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="7043d-197">lastUsageDate</span></span> | <span data-ttu-id="7043d-198">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-198">string in UTC date time format</span></span> | <span data-ttu-id="7043d-199">Aboneliğin son kullanıldığı tarih.</span><span class="sxs-lookup"><span data-stu-id="7043d-199">The date that the subscription was last used.</span></span> <span data-ttu-id="7043d-200">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="7043d-200">The default value is null.</span></span> |
| <span data-ttu-id="7043d-201">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="7043d-201">deprovisionedDate</span></span> | <span data-ttu-id="7043d-202">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-202">string in UTC date time format</span></span> | <span data-ttu-id="7043d-203">Aboneliğin sağlaması kaldırılmış olan tarih.</span><span class="sxs-lookup"><span data-stu-id="7043d-203">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="7043d-204">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="7043d-204">The default value is null.</span></span> |
| <span data-ttu-id="7043d-205">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="7043d-205">lastRenewalDate</span></span> | <span data-ttu-id="7043d-206">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="7043d-206">string in UTC date time format</span></span> | <span data-ttu-id="7043d-207">Aboneliğin son yenilenme tarihi.</span><span class="sxs-lookup"><span data-stu-id="7043d-207">The date that the subscription was last renewed.</span></span> <span data-ttu-id="7043d-208">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="7043d-208">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="7043d-209">Filtre alanları</span><span class="sxs-lookup"><span data-stu-id="7043d-209">Filter fields</span></span>

<span data-ttu-id="7043d-210">Aşağıdaki tablo, isteğe bağlı filtre alanlarını ve açıklamalarını listelemektedir:</span><span class="sxs-lookup"><span data-stu-id="7043d-210">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="7043d-211">Alan</span><span class="sxs-lookup"><span data-stu-id="7043d-211">Field</span></span> | <span data-ttu-id="7043d-212">Tür</span><span class="sxs-lookup"><span data-stu-id="7043d-212">Type</span></span> |  <span data-ttu-id="7043d-213">Description</span><span class="sxs-lookup"><span data-stu-id="7043d-213">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="7043d-214">top</span><span class="sxs-lookup"><span data-stu-id="7043d-214">top</span></span> | <span data-ttu-id="7043d-215">int</span><span class="sxs-lookup"><span data-stu-id="7043d-215">int</span></span> | <span data-ttu-id="7043d-216">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="7043d-216">The number of rows of data to return in the request.</span></span> <span data-ttu-id="7043d-217">Değer belirtilmezse, en büyük değer ve varsayılan değer 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="7043d-217">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="7043d-218">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="7043d-218">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="7043d-219">Atla</span><span class="sxs-lookup"><span data-stu-id="7043d-219">skip</span></span> | <span data-ttu-id="7043d-220">int</span><span class="sxs-lookup"><span data-stu-id="7043d-220">int</span></span> | <span data-ttu-id="7043d-221">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="7043d-221">The number of rows to skip in the query.</span></span> <span data-ttu-id="7043d-222">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="7043d-222">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="7043d-223">Örneğin, top = 10000 ve Skip = 0 verilerin ilk 10000 satırını alır, top = 10000 ve Skip = 10000, sonraki 10000 satırlık verileri alır.</span><span class="sxs-lookup"><span data-stu-id="7043d-223">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="7043d-224">filtre</span><span class="sxs-lookup"><span data-stu-id="7043d-224">filter</span></span> | <span data-ttu-id="7043d-225">string</span><span class="sxs-lookup"><span data-stu-id="7043d-225">string</span></span> | <span data-ttu-id="7043d-226">Yanıttaki satırları filtreleyen bir veya daha fazla deyim.</span><span class="sxs-lookup"><span data-stu-id="7043d-226">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="7043d-227">Her filtre ekstresi, yanıt gövdesinden bir alan adı ve **`eq`** , **`ne`** veya belirli alanlar için, işleci ile ilişkili bir değer içerir **`contains`** .</span><span class="sxs-lookup"><span data-stu-id="7043d-227">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="7043d-228">Deyimler, veya kullanılarak birleştirilebilir **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="7043d-228">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="7043d-229">Dize değerleri, filtre parametresindeki tek tırnak işaretleriyle çevrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="7043d-229">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="7043d-230">Filtrelenebilir alanların listesi ve bu alanlarla Desteklenen işleçler için aşağıdaki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="7043d-230">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="7043d-231">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="7043d-231">aggregationLevel</span></span> | <span data-ttu-id="7043d-232">string</span><span class="sxs-lookup"><span data-stu-id="7043d-232">string</span></span> | <span data-ttu-id="7043d-233">Toplam verilerinin alınacağı zaman aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="7043d-233">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="7043d-234">Şu dizelerden biri olabilir: **gün**, **hafta** veya **ay**.</span><span class="sxs-lookup"><span data-stu-id="7043d-234">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="7043d-235">Değer belirtilmezse, varsayılan olarak **Dadterange** olur.</span><span class="sxs-lookup"><span data-stu-id="7043d-235">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="7043d-236">**Note**: Bu parametre yalnızca, GroupBy parametresinin bir parçası olarak bir tarih alanı geçirildiğinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="7043d-236">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="7043d-237">Ölçütü</span><span class="sxs-lookup"><span data-stu-id="7043d-237">groupBy</span></span> | <span data-ttu-id="7043d-238">string</span><span class="sxs-lookup"><span data-stu-id="7043d-238">string</span></span> | <span data-ttu-id="7043d-239">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="7043d-239">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7043d-240">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7043d-240">Request headers</span></span>

<span data-ttu-id="7043d-241">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7043d-241">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7043d-242">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7043d-242">Request body</span></span>

<span data-ttu-id="7043d-243">Yok.</span><span class="sxs-lookup"><span data-stu-id="7043d-243">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7043d-244">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7043d-244">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="7043d-245">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7043d-245">REST response</span></span>

<span data-ttu-id="7043d-246">Başarılı olursa, yanıt gövdesi belirtilen hüküm ve tarihlere göre gruplanmış bir [abonelik](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="7043d-246">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7043d-247">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7043d-247">Response success and error codes</span></span>

<span data-ttu-id="7043d-248">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7043d-248">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7043d-249">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7043d-249">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7043d-250">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7043d-250">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7043d-251">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7043d-251">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123
{
  "Value": [
    {
      "subscriptionType": "Azure",
      "subscriptionCount": "63",
      "licenseCount": "0"
    },
    {
      "subscriptionType": "Dynamics",
      "subscriptionCount": "62",
      "licenseCount": "405"
    },
    {
      "subscriptionType": "EMS",
      "subscriptionCount": "39",
      "licenseCount": "193"
    },
    {
      "subscriptionType": "M365",
      "subscriptionCount": "2",
      "licenseCount": "5"
    },
    {
      "subscriptionType": "Office",
      "subscriptionCount": "906",
      "licenseCount": "7485"
    },
    {
      "subscriptionType": "UNKNOWN",
      "subscriptionCount": "104",
      "licenseCount": "439"
    },
    {
      "subscriptionType": "Windows",
      "subscriptionCount": "2",
      "licenseCount": "2"
    }
  ],
  "@nextLink": null,
  "TotalCount": 7
}
```

## <a name="see-also"></a><span data-ttu-id="7043d-252">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="7043d-252">See also</span></span>

[<span data-ttu-id="7043d-253">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="7043d-253">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
