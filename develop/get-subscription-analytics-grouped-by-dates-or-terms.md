---
title: Tarih veya koşullara göre gruplandırılmış abonelik analizlerini al
description: Tarih veya koşullara göre gruplanmış abonelik Analizi bilgilerini alma.
ms.date: 06/27/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8192a9863d53ec8697a7341cd38c69200614bd4a
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548728"
---
# <a name="get-subscription-analytics-grouped-by-dates-or-terms"></a><span data-ttu-id="84e36-103">Tarih veya koşullara göre gruplandırılmış abonelik analizlerini al</span><span class="sxs-lookup"><span data-stu-id="84e36-103">Get subscription analytics grouped by dates or terms</span></span>

<span data-ttu-id="84e36-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="84e36-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="84e36-105">Müşterilerinizin tarihlere veya terimlere göre gruplanmış abonelik Analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="84e36-105">How to get subscription analytics information for your customers grouped by dates or terms.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="84e36-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="84e36-106">Prerequisites</span></span>

- <span data-ttu-id="84e36-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="84e36-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="84e36-108">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="84e36-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="84e36-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="84e36-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="84e36-110">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="84e36-110">Request syntax</span></span>

| <span data-ttu-id="84e36-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="84e36-111">Method</span></span> | <span data-ttu-id="84e36-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="84e36-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="84e36-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="84e36-113">**GET**</span></span> | <span data-ttu-id="84e36-114">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri? GroupBy = {groupby_queries}</span><span class="sxs-lookup"><span data-stu-id="84e36-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?groupby={groupby_queries}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="84e36-115">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="84e36-115">URI parameters</span></span>

<span data-ttu-id="84e36-116">Kuruluşunuzu tanımlamak ve sonuçları gruplandırmak için aşağıdaki gerekli yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="84e36-116">Use the following required path parameters to identify your organization and to group the results.</span></span>

| <span data-ttu-id="84e36-117">Ad</span><span class="sxs-lookup"><span data-stu-id="84e36-117">Name</span></span> | <span data-ttu-id="84e36-118">Tür</span><span class="sxs-lookup"><span data-stu-id="84e36-118">Type</span></span> | <span data-ttu-id="84e36-119">Gerekli</span><span class="sxs-lookup"><span data-stu-id="84e36-119">Required</span></span> | <span data-ttu-id="84e36-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84e36-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="84e36-121">groupby_queries</span><span class="sxs-lookup"><span data-stu-id="84e36-121">groupby_queries</span></span> | <span data-ttu-id="84e36-122">dizeler ve tarih saat çiftleri</span><span class="sxs-lookup"><span data-stu-id="84e36-122">pairs of strings and dateTime</span></span> | <span data-ttu-id="84e36-123">Yes</span><span class="sxs-lookup"><span data-stu-id="84e36-123">Yes</span></span> | <span data-ttu-id="84e36-124">Sonucu filtrelemek için hüküm ve tarihler.</span><span class="sxs-lookup"><span data-stu-id="84e36-124">The terms and dates to filter the result.</span></span> |

### <a name="groupby-syntax"></a><span data-ttu-id="84e36-125">GroupBy sözdizimi</span><span class="sxs-lookup"><span data-stu-id="84e36-125">GroupBy syntax</span></span>

<span data-ttu-id="84e36-126">Group By parametresi bir dizi virgülle ayrılmış, alan değeri olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="84e36-126">The group by parameter must be composed as a series of comma separated, field values.</span></span>

<span data-ttu-id="84e36-127">Kodlanamayan bir örnek şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="84e36-127">An unencoded example looks like this:</span></span>

```http
?groupby=termField1,dateField1,termField2
```

<span data-ttu-id="84e36-128">Aşağıdaki tabloda Group by için desteklenen alanların listesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="84e36-128">The following table shows a list of the supported fields for group by.</span></span>

| <span data-ttu-id="84e36-129">Alan</span><span class="sxs-lookup"><span data-stu-id="84e36-129">Field</span></span> | <span data-ttu-id="84e36-130">Tür</span><span class="sxs-lookup"><span data-stu-id="84e36-130">Type</span></span> | <span data-ttu-id="84e36-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84e36-131">Description</span></span> |
|-------|------|-------------|
| <span data-ttu-id="84e36-132">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="84e36-132">customerTenantId</span></span> | <span data-ttu-id="84e36-133">string</span><span class="sxs-lookup"><span data-stu-id="84e36-133">string</span></span> | <span data-ttu-id="84e36-134">Müşteri kiracısını tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="84e36-134">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="84e36-135">customerName</span><span class="sxs-lookup"><span data-stu-id="84e36-135">customerName</span></span> | <span data-ttu-id="84e36-136">string</span><span class="sxs-lookup"><span data-stu-id="84e36-136">string</span></span> | <span data-ttu-id="84e36-137">Müşterinin adı.</span><span class="sxs-lookup"><span data-stu-id="84e36-137">The name of the customer.</span></span> |
| <span data-ttu-id="84e36-138">customerMarket</span><span class="sxs-lookup"><span data-stu-id="84e36-138">customerMarket</span></span> | <span data-ttu-id="84e36-139">string</span><span class="sxs-lookup"><span data-stu-id="84e36-139">string</span></span> | <span data-ttu-id="84e36-140">Müşterinin iş üzerinde kullandığı ülke/bölge.</span><span class="sxs-lookup"><span data-stu-id="84e36-140">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="84e36-141">kimlik</span><span class="sxs-lookup"><span data-stu-id="84e36-141">id</span></span> | <span data-ttu-id="84e36-142">string</span><span class="sxs-lookup"><span data-stu-id="84e36-142">string</span></span> | <span data-ttu-id="84e36-143">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="84e36-143">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="84e36-144">durum</span><span class="sxs-lookup"><span data-stu-id="84e36-144">status</span></span> | <span data-ttu-id="84e36-145">string</span><span class="sxs-lookup"><span data-stu-id="84e36-145">string</span></span> | <span data-ttu-id="84e36-146">Abonelik durumu.</span><span class="sxs-lookup"><span data-stu-id="84e36-146">The subscription status.</span></span> <span data-ttu-id="84e36-147">Desteklenen değerler şunlardır: "ETKIN", "askıya ALıNDı" veya "SAĞLAMASı KALDıRıLDı".</span><span class="sxs-lookup"><span data-stu-id="84e36-147">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="84e36-148">productName</span><span class="sxs-lookup"><span data-stu-id="84e36-148">productName</span></span> | <span data-ttu-id="84e36-149">string</span><span class="sxs-lookup"><span data-stu-id="84e36-149">string</span></span> | <span data-ttu-id="84e36-150">Ürünün adı.</span><span class="sxs-lookup"><span data-stu-id="84e36-150">The name of the product.</span></span> |
| <span data-ttu-id="84e36-151">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="84e36-151">subscriptionType</span></span> | <span data-ttu-id="84e36-152">string</span><span class="sxs-lookup"><span data-stu-id="84e36-152">string</span></span> | <span data-ttu-id="84e36-153">Abonelik türü.</span><span class="sxs-lookup"><span data-stu-id="84e36-153">The subscription type.</span></span> <span data-ttu-id="84e36-154">Note: Bu alan, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="84e36-154">Note: This field is case-sensitive.</span></span> <span data-ttu-id="84e36-155">desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="84e36-155">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="84e36-156">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="84e36-156">autoRenewEnabled</span></span> | <span data-ttu-id="84e36-157">Boole</span><span class="sxs-lookup"><span data-stu-id="84e36-157">Boolean</span></span> | <span data-ttu-id="84e36-158">Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer.</span><span class="sxs-lookup"><span data-stu-id="84e36-158">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="84e36-159">iş ortağı kimliği</span><span class="sxs-lookup"><span data-stu-id="84e36-159">partnerId</span></span>  | <span data-ttu-id="84e36-160">string</span><span class="sxs-lookup"><span data-stu-id="84e36-160">string</span></span> | <span data-ttu-id="84e36-161">MPN KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="84e36-161">The MPN ID.</span></span> <span data-ttu-id="84e36-162">Doğrudan satıcı için, bu parametre ortağın MPN KIMLIĞI olur.</span><span class="sxs-lookup"><span data-stu-id="84e36-162">For a direct reseller, this parameter will be the MPN ID of the partner.</span></span> <span data-ttu-id="84e36-163">Dolaylı bir satıcı için, bu parametre dolaylı satıcıdan MPN KIMLIĞI olacaktır.</span><span class="sxs-lookup"><span data-stu-id="84e36-163">For an indirect reseller, this parameter will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="84e36-164">friendlyName</span><span class="sxs-lookup"><span data-stu-id="84e36-164">friendlyName</span></span> | <span data-ttu-id="84e36-165">string</span><span class="sxs-lookup"><span data-stu-id="84e36-165">string</span></span> | <span data-ttu-id="84e36-166">Aboneliğin adı.</span><span class="sxs-lookup"><span data-stu-id="84e36-166">The name of the subscription.</span></span> |
| <span data-ttu-id="84e36-167">partnerName</span><span class="sxs-lookup"><span data-stu-id="84e36-167">partnerName</span></span> | <span data-ttu-id="84e36-168">string</span><span class="sxs-lookup"><span data-stu-id="84e36-168">string</span></span> | <span data-ttu-id="84e36-169">Aboneliğin satın alındığı ortağın adı</span><span class="sxs-lookup"><span data-stu-id="84e36-169">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="84e36-170">Adı</span><span class="sxs-lookup"><span data-stu-id="84e36-170">providerName</span></span> | <span data-ttu-id="84e36-171">string</span><span class="sxs-lookup"><span data-stu-id="84e36-171">string</span></span> | <span data-ttu-id="84e36-172">Abonelik işlemi dolaylı satıcı için olduğunda, sağlayıcı adı aboneliği satın alan dolaylı sağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="84e36-172">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>
| <span data-ttu-id="84e36-173">creationDate</span><span class="sxs-lookup"><span data-stu-id="84e36-173">creationDate</span></span> | <span data-ttu-id="84e36-174">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-174">string in UTC date time format</span></span> | <span data-ttu-id="84e36-175">Aboneliğin oluşturulduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="84e36-175">The date the subscription was created.</span></span> |
| <span data-ttu-id="84e36-176">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="84e36-176">effectiveStartDate</span></span> | <span data-ttu-id="84e36-177">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-177">string in UTC date time format</span></span> | <span data-ttu-id="84e36-178">Aboneliğin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="84e36-178">The date the subscription starts.</span></span> |
| <span data-ttu-id="84e36-179">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="84e36-179">commitmentEndDate</span></span> | <span data-ttu-id="84e36-180">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-180">string in UTC date time format</span></span> | <span data-ttu-id="84e36-181">Aboneliğin bitiş tarihi.</span><span class="sxs-lookup"><span data-stu-id="84e36-181">The date the subscription ends.</span></span> |
| <span data-ttu-id="84e36-182">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="84e36-182">currentStateEndDate</span></span> | <span data-ttu-id="84e36-183">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-183">string in UTC date time format</span></span> | <span data-ttu-id="84e36-184">Aboneliğin geçerli durumunun değiştirileceği tarih.</span><span class="sxs-lookup"><span data-stu-id="84e36-184">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="84e36-185">Trialtopaıdconversiondate</span><span class="sxs-lookup"><span data-stu-id="84e36-185">trialToPaidConversionDate</span></span> | <span data-ttu-id="84e36-186">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-186">string in UTC date time format</span></span> | <span data-ttu-id="84e36-187">Aboneliğin deneme sürümünden ücretli olarak dönüştürdüğü tarih.</span><span class="sxs-lookup"><span data-stu-id="84e36-187">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="84e36-188">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="84e36-188">The default value is null.</span></span> |
| <span data-ttu-id="84e36-189">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="84e36-189">trialStartDate</span></span> | <span data-ttu-id="84e36-190">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-190">string in UTC date time format</span></span> | <span data-ttu-id="84e36-191">Abonelik için deneme süresinin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="84e36-191">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="84e36-192">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="84e36-192">The default value is null.</span></span> |
| <span data-ttu-id="84e36-193">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="84e36-193">lastUsageDate</span></span> | <span data-ttu-id="84e36-194">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-194">string in UTC date time format</span></span> | <span data-ttu-id="84e36-195">Aboneliğin son kullanıldığı tarih.</span><span class="sxs-lookup"><span data-stu-id="84e36-195">The date that the subscription was last used.</span></span> <span data-ttu-id="84e36-196">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="84e36-196">The default value is null.</span></span> |
| <span data-ttu-id="84e36-197">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="84e36-197">deprovisionedDate</span></span> | <span data-ttu-id="84e36-198">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-198">string in UTC date time format</span></span> | <span data-ttu-id="84e36-199">Aboneliğin sağlaması kaldırılmış olan tarih.</span><span class="sxs-lookup"><span data-stu-id="84e36-199">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="84e36-200">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="84e36-200">The default value is null.</span></span> |
| <span data-ttu-id="84e36-201">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="84e36-201">lastRenewalDate</span></span> | <span data-ttu-id="84e36-202">UTC Tarih saat biçiminde dize</span><span class="sxs-lookup"><span data-stu-id="84e36-202">string in UTC date time format</span></span> | <span data-ttu-id="84e36-203">Aboneliğin son yenilenme tarihi.</span><span class="sxs-lookup"><span data-stu-id="84e36-203">The date that the subscription was last renewed.</span></span> <span data-ttu-id="84e36-204">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="84e36-204">The default value is null.</span></span> |

### <a name="filter-fields"></a><span data-ttu-id="84e36-205">Filtre alanları</span><span class="sxs-lookup"><span data-stu-id="84e36-205">Filter fields</span></span>

<span data-ttu-id="84e36-206">Aşağıdaki tablo, isteğe bağlı filtre alanlarını ve açıklamalarını listelemektedir:</span><span class="sxs-lookup"><span data-stu-id="84e36-206">The following table lists optional filter fields and their descriptions:</span></span>

| <span data-ttu-id="84e36-207">Alan</span><span class="sxs-lookup"><span data-stu-id="84e36-207">Field</span></span> | <span data-ttu-id="84e36-208">Tür</span><span class="sxs-lookup"><span data-stu-id="84e36-208">Type</span></span> |  <span data-ttu-id="84e36-209">Açıklama</span><span class="sxs-lookup"><span data-stu-id="84e36-209">Description</span></span> |
|-------|------|--------------|
| <span data-ttu-id="84e36-210">top</span><span class="sxs-lookup"><span data-stu-id="84e36-210">top</span></span> | <span data-ttu-id="84e36-211">int</span><span class="sxs-lookup"><span data-stu-id="84e36-211">int</span></span> | <span data-ttu-id="84e36-212">İstekte döndürülecek veri satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="84e36-212">The number of rows of data to return in the request.</span></span> <span data-ttu-id="84e36-213">Değer belirtilmezse, en büyük değer ve varsayılan değer 10000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="84e36-213">If the value isn't specified, the maximum value and the default value are 10000.</span></span> <span data-ttu-id="84e36-214">Sorguda daha fazla satır varsa, yanıt gövdesi sonraki veri sayfasını istemek için kullanabileceğiniz bir sonraki bağlantıyı içerir.</span><span class="sxs-lookup"><span data-stu-id="84e36-214">If there are more rows in the query, the response body includes a next link that you can use to request the next page of data.</span></span> |
| <span data-ttu-id="84e36-215">Atla</span><span class="sxs-lookup"><span data-stu-id="84e36-215">skip</span></span> | <span data-ttu-id="84e36-216">int</span><span class="sxs-lookup"><span data-stu-id="84e36-216">int</span></span> | <span data-ttu-id="84e36-217">Sorgudaki atlanacak satır sayısı.</span><span class="sxs-lookup"><span data-stu-id="84e36-217">The number of rows to skip in the query.</span></span> <span data-ttu-id="84e36-218">Büyük veri kümeleri üzerinden sayfa eklemek için bu parametreyi kullanın.</span><span class="sxs-lookup"><span data-stu-id="84e36-218">Use this parameter to page through large data sets.</span></span> <span data-ttu-id="84e36-219">Örneğin, top = 10000 ve Skip = 0 verilerin ilk 10000 satırını alır, top = 10000 ve Skip = 10000, sonraki 10000 satırlık verileri alır.</span><span class="sxs-lookup"><span data-stu-id="84e36-219">For example, top=10000 and skip=0 retrieves the first 10000 rows of data, top=10000 and skip=10000 retrieves the next 10000 rows of data.</span></span> |
| <span data-ttu-id="84e36-220">filtre</span><span class="sxs-lookup"><span data-stu-id="84e36-220">filter</span></span> | <span data-ttu-id="84e36-221">string</span><span class="sxs-lookup"><span data-stu-id="84e36-221">string</span></span> | <span data-ttu-id="84e36-222">Yanıttaki satırları filtreleyen bir veya daha fazla deyim.</span><span class="sxs-lookup"><span data-stu-id="84e36-222">One or more statements that filter the rows in the response.</span></span> <span data-ttu-id="84e36-223">Her filtre ekstresi, yanıt gövdesinden bir alan adı ve **`eq`** , **`ne`** veya belirli alanlar için, işleci ile ilişkili bir değer içerir **`contains`** .</span><span class="sxs-lookup"><span data-stu-id="84e36-223">Each filter statement contains a field name from the response body and a value that are associated with the **`eq`**, **`ne`**, or for certain fields, the **`contains`** operator.</span></span> <span data-ttu-id="84e36-224">Deyimler, veya kullanılarak birleştirilebilir **`and`** **`or`** .</span><span class="sxs-lookup"><span data-stu-id="84e36-224">Statements can be combined using **`and`** or **`or`**.</span></span> <span data-ttu-id="84e36-225">Dize değerleri, filtre parametresindeki tek tırnak işaretleriyle çevrelenmelidir.</span><span class="sxs-lookup"><span data-stu-id="84e36-225">String values must be surrounded by single quotes in the filter parameter.</span></span> <span data-ttu-id="84e36-226">Filtrelenebilir alanların listesi ve bu alanlarla Desteklenen işleçler için aşağıdaki bölüme bakın.</span><span class="sxs-lookup"><span data-stu-id="84e36-226">See the following section for a list of fields that can be filtered and the operators that are supported with those fields.</span></span> |
| <span data-ttu-id="84e36-227">aggregationLevel</span><span class="sxs-lookup"><span data-stu-id="84e36-227">aggregationLevel</span></span> | <span data-ttu-id="84e36-228">string</span><span class="sxs-lookup"><span data-stu-id="84e36-228">string</span></span> | <span data-ttu-id="84e36-229">Toplam verilerinin alınacağı zaman aralığını belirtir.</span><span class="sxs-lookup"><span data-stu-id="84e36-229">Specifies the time range for which to retrieve aggregate data.</span></span> <span data-ttu-id="84e36-230">Şu dizelerden biri olabilir: **gün**, **hafta** veya **ay**.</span><span class="sxs-lookup"><span data-stu-id="84e36-230">Can be one of the following strings: **day**, **week**, or **month**.</span></span> <span data-ttu-id="84e36-231">Değer belirtilmezse, varsayılan olarak **Dadterange** olur.</span><span class="sxs-lookup"><span data-stu-id="84e36-231">If the value isn't specified, the default is **dateRange**.</span></span> <span data-ttu-id="84e36-232">**Note**: Bu parametre yalnızca, GroupBy parametresinin bir parçası olarak bir tarih alanı geçirildiğinde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="84e36-232">**Note**: This parameter applies only when a date field is passed as part of the groupBy parameter.</span></span> |
| <span data-ttu-id="84e36-233">Ölçütü</span><span class="sxs-lookup"><span data-stu-id="84e36-233">groupBy</span></span> | <span data-ttu-id="84e36-234">string</span><span class="sxs-lookup"><span data-stu-id="84e36-234">string</span></span> | <span data-ttu-id="84e36-235">Yalnızca belirtilen alanlara veri toplamayı uygulayan bir ifade.</span><span class="sxs-lookup"><span data-stu-id="84e36-235">A statement that applies data aggregation only to the specified fields.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="84e36-236">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="84e36-236">Request headers</span></span>

<span data-ttu-id="84e36-237">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="84e36-237">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="84e36-238">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="84e36-238">Request body</span></span>

<span data-ttu-id="84e36-239">Yok.</span><span class="sxs-lookup"><span data-stu-id="84e36-239">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="84e36-240">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="84e36-240">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?groupBy=subscriptionType
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="84e36-241">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="84e36-241">REST response</span></span>

<span data-ttu-id="84e36-242">Başarılı olursa, yanıt gövdesi belirtilen hüküm ve tarihlere göre gruplanmış bir [abonelik](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="84e36-242">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources grouped by the specified terms and dates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="84e36-243">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="84e36-243">Response success and error codes</span></span>

<span data-ttu-id="84e36-244">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="84e36-244">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="84e36-245">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="84e36-245">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="84e36-246">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="84e36-246">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="84e36-247">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="84e36-247">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="84e36-248">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="84e36-248">See also</span></span>

[<span data-ttu-id="84e36-249">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="84e36-249">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
