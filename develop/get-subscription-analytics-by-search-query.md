---
title: Arama sorgusuna abonelik Analizi al
description: Bir arama sorgusuyla filtrelenmiş abonelik Analizi bilgilerini alma.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8df777b9a88206f8b22579f0f445c54d80f7cd64
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548745"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="4e3a1-103">Bir arama sorgusuyla filtrelenmiş abonelik analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="4e3a1-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="4e3a1-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4e3a1-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4e3a1-105">Bir arama sorgusuyla filtrelenmiş müşterileriniz için abonelik Analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-105">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e3a1-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4e3a1-106">Prerequisites</span></span>

- <span data-ttu-id="4e3a1-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4e3a1-108">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-108">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="4e3a1-109">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4e3a1-109">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4e3a1-110">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4e3a1-110">Request syntax</span></span>

| <span data-ttu-id="4e3a1-111">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4e3a1-111">Method</span></span> | <span data-ttu-id="4e3a1-112">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4e3a1-112">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="4e3a1-113">**Al**</span><span class="sxs-lookup"><span data-stu-id="4e3a1-113">**GET**</span></span> | <span data-ttu-id="4e3a1-114">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri? Filter = {filter_string}</span><span class="sxs-lookup"><span data-stu-id="4e3a1-114">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="4e3a1-115">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="4e3a1-115">URI parameters</span></span>

<span data-ttu-id="4e3a1-116">Kuruluşunuzu tanımlamak ve aramayı filtrelemek için aşağıdaki gerekli yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-116">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="4e3a1-117">Ad</span><span class="sxs-lookup"><span data-stu-id="4e3a1-117">Name</span></span> | <span data-ttu-id="4e3a1-118">Tür</span><span class="sxs-lookup"><span data-stu-id="4e3a1-118">Type</span></span> | <span data-ttu-id="4e3a1-119">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4e3a1-119">Required</span></span> | <span data-ttu-id="4e3a1-120">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e3a1-120">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="4e3a1-121">filter_string</span><span class="sxs-lookup"><span data-stu-id="4e3a1-121">filter_string</span></span> | <span data-ttu-id="4e3a1-122">string</span><span class="sxs-lookup"><span data-stu-id="4e3a1-122">string</span></span> | <span data-ttu-id="4e3a1-123">Yes</span><span class="sxs-lookup"><span data-stu-id="4e3a1-123">Yes</span></span> | <span data-ttu-id="4e3a1-124">Abonelik analizinden uygulanacak filtre.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-124">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="4e3a1-125">Bu parametrede kullanılacak söz dizimi, alanlar ve işleçler için filtre söz dizimini ve filtre alanları bölümlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-125">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="4e3a1-126">Filtre sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4e3a1-126">Filter syntax</span></span>

<span data-ttu-id="4e3a1-127">Filter parametresi bir dizi alan, değer ve işleç birleşimi olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-127">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="4e3a1-128">Birden çok bileşim, **`and`** veya işleçleri kullanılarak birleştirilebilir **`or`** .</span><span class="sxs-lookup"><span data-stu-id="4e3a1-128">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="4e3a1-129">Kodlanamayan bir örnek şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="4e3a1-129">An unencoded example looks like this:</span></span>

- <span data-ttu-id="4e3a1-130">Dizisinde `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-130">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="4e3a1-131">Boolean `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-131">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="4e3a1-132">Vardır `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-132">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="4e3a1-133">Filtre alanları</span><span class="sxs-lookup"><span data-stu-id="4e3a1-133">Filter fields</span></span>

<span data-ttu-id="4e3a1-134">İsteğin filtre parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-134">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="4e3a1-135">Her bir ifade, **`eq`** veya işleçleriyle ilişkili bir alan ve değer içerir **`ne`** .</span><span class="sxs-lookup"><span data-stu-id="4e3a1-135">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="4e3a1-136">Bazı alanlar,,, **`contains`** , **`gt`** **`lt`** **`ge`** ve **`le`** işleçlerini da destekler.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-136">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="4e3a1-137">Deyimler, **`and`** veya işleçleri kullanılarak birleştirilebilir **`or`** .</span><span class="sxs-lookup"><span data-stu-id="4e3a1-137">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="4e3a1-138">Filtre dizelerinin örnekleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="4e3a1-138">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="4e3a1-139">Aşağıdaki tabloda, filtre parametresi için desteklenen alanların ve destek işleçlerinin listesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-139">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="4e3a1-140">Dize değerleri tek tırnak işareti içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-140">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="4e3a1-141">Parametre</span><span class="sxs-lookup"><span data-stu-id="4e3a1-141">Parameter</span></span> | <span data-ttu-id="4e3a1-142">Desteklenen işleçler</span><span class="sxs-lookup"><span data-stu-id="4e3a1-142">Supported operators</span></span> | <span data-ttu-id="4e3a1-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4e3a1-143">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="4e3a1-144">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="4e3a1-144">autoRenewEnabled</span></span> | <span data-ttu-id="4e3a1-145">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-145">`eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-146">Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-146">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="4e3a1-147">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-147">commitmentEndDate</span></span> | <span data-ttu-id="4e3a1-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-148">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="4e3a1-149">Aboneliğin bitiş tarihi.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-149">The date the subscription ends.</span></span> |
| <span data-ttu-id="4e3a1-150">creationDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-150">creationDate</span></span> | <span data-ttu-id="4e3a1-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-151">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="4e3a1-152">Aboneliğin oluşturulduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-152">The date the subscription was created.</span></span> |
| <span data-ttu-id="4e3a1-153">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-153">currentStateEndDate</span></span> | <span data-ttu-id="4e3a1-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-154">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="4e3a1-155">Aboneliğin geçerli durumunun değiştirileceği tarih.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-155">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="4e3a1-156">customerMarket</span><span class="sxs-lookup"><span data-stu-id="4e3a1-156">customerMarket</span></span> | <span data-ttu-id="4e3a1-157">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-157">`eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-158">Müşterinin iş üzerinde kullandığı ülke/bölge.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-158">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="4e3a1-159">customerName</span><span class="sxs-lookup"><span data-stu-id="4e3a1-159">customerName</span></span> | `contains` | <span data-ttu-id="4e3a1-160">Müşterinin adı.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-160">The name of the customer.</span></span> |
| <span data-ttu-id="4e3a1-161">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="4e3a1-161">customerTenantId</span></span> | <span data-ttu-id="4e3a1-162">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-162">`eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-163">Müşteri kiracısını tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-163">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="4e3a1-164">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-164">deprovisionedDate</span></span> | <span data-ttu-id="4e3a1-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-165">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="4e3a1-166">Aboneliğin sağlaması kaldırılmış olan tarih.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-166">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="4e3a1-167">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-167">The default value is null.</span></span> |
| <span data-ttu-id="4e3a1-168">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-168">effectiveStartDate</span></span> | <span data-ttu-id="4e3a1-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="4e3a1-170">Aboneliğin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-170">The date the subscription starts.</span></span> |
| <span data-ttu-id="4e3a1-171">friendlyName</span><span class="sxs-lookup"><span data-stu-id="4e3a1-171">friendlyName</span></span> | `contains` | <span data-ttu-id="4e3a1-172">Aboneliğin adı.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-172">The name of the subscription.</span></span> |
| <span data-ttu-id="4e3a1-173">kimlik</span><span class="sxs-lookup"><span data-stu-id="4e3a1-173">id</span></span> | <span data-ttu-id="4e3a1-174">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-174">`eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-175">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-175">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="4e3a1-176">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-176">lastRenewalDate</span></span> | <span data-ttu-id="4e3a1-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-177">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="4e3a1-178">Aboneliğin son yenilenme tarihi.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-178">The date that the subscription was last renewed.</span></span> <span data-ttu-id="4e3a1-179">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-179">The default value is null.</span></span> |
| <span data-ttu-id="4e3a1-180">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-180">lastUsageDate</span></span> | <span data-ttu-id="4e3a1-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="4e3a1-182">Aboneliğin son kullanıldığı tarih.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-182">The date that the subscription was last used.</span></span> <span data-ttu-id="4e3a1-183">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-183">The default value is null.</span></span> |
| <span data-ttu-id="4e3a1-184">iş ortağı kimliği</span><span class="sxs-lookup"><span data-stu-id="4e3a1-184">partnerId</span></span> | <span data-ttu-id="4e3a1-185">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-185">`eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-186">MPN KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-186">The MPN ID.</span></span> <span data-ttu-id="4e3a1-187">Doğrudan satıcı için bu değer ortağın MPN KIMLIĞI olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-187">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="4e3a1-188">Dolaylı bir satıcı için, bu değer dolaylı satıcının MPN KIMLIĞI olacaktır.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-188">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="4e3a1-189">partnerName</span><span class="sxs-lookup"><span data-stu-id="4e3a1-189">partnerName</span></span> | <span data-ttu-id="4e3a1-190">string</span><span class="sxs-lookup"><span data-stu-id="4e3a1-190">string</span></span> | <span data-ttu-id="4e3a1-191">Aboneliğin satın alındığı ortağın adı</span><span class="sxs-lookup"><span data-stu-id="4e3a1-191">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="4e3a1-192">productName</span><span class="sxs-lookup"><span data-stu-id="4e3a1-192">productName</span></span> | <span data-ttu-id="4e3a1-193">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-193">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-194">Ürünün adı.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-194">The name of the product.</span></span> |
| <span data-ttu-id="4e3a1-195">Adı</span><span class="sxs-lookup"><span data-stu-id="4e3a1-195">providerName</span></span> | <span data-ttu-id="4e3a1-196">string</span><span class="sxs-lookup"><span data-stu-id="4e3a1-196">string</span></span> | <span data-ttu-id="4e3a1-197">Abonelik işlemi dolaylı satıcı için olduğunda, sağlayıcı adı aboneliği satın alan dolaylı sağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-197">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="4e3a1-198">durum</span><span class="sxs-lookup"><span data-stu-id="4e3a1-198">status</span></span> | <span data-ttu-id="4e3a1-199">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-199">`eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-200">Abonelik durumu.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-200">The subscription status.</span></span> <span data-ttu-id="4e3a1-201">Desteklenen değerler şunlardır: "ETKIN", "askıya ALıNDı" veya "SAĞLAMASı KALDıRıLDı".</span><span class="sxs-lookup"><span data-stu-id="4e3a1-201">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="4e3a1-202">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="4e3a1-202">subscriptionType</span></span> | <span data-ttu-id="4e3a1-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-203">`eq`, `ne`</span></span> | <span data-ttu-id="4e3a1-204">Abonelik türü.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-204">The subscription type.</span></span> <span data-ttu-id="4e3a1-205">**Note**: Bu alan, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-205">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="4e3a1-206">desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="4e3a1-206">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="4e3a1-207">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-207">trialStartDate</span></span> | <span data-ttu-id="4e3a1-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-208">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="4e3a1-209">Abonelik için deneme süresinin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-209">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="4e3a1-210">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-210">The default value is null.</span></span> |
| <span data-ttu-id="4e3a1-211">Trialtopaıdconversiondate</span><span class="sxs-lookup"><span data-stu-id="4e3a1-211">trialToPaidConversionDate</span></span> | <span data-ttu-id="4e3a1-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="4e3a1-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="4e3a1-213">Aboneliğin deneme sürümünden ücretli olarak dönüştürdüğü tarih.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-213">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="4e3a1-214">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-214">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="4e3a1-215">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4e3a1-215">Request headers</span></span>

<span data-ttu-id="4e3a1-216">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4e3a1-216">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4e3a1-217">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4e3a1-217">Request body</span></span>

<span data-ttu-id="4e3a1-218">Yok.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-218">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4e3a1-219">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4e3a1-219">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="4e3a1-220">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4e3a1-220">REST response</span></span>

<span data-ttu-id="4e3a1-221">Başarılı olursa, yanıt gövdesi, filtre ölçütlerini karşılayan bir [abonelik](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-221">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4e3a1-222">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4e3a1-222">Response success and error codes</span></span>

<span data-ttu-id="4e3a1-223">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-223">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4e3a1-224">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-224">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4e3a1-225">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4e3a1-225">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4e3a1-226">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4e3a1-226">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 177
Content-Type: application/json; charset=utf-8
MS-CorrelationId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-RequestId: ec8f62e5-1d92-47e9-8d5d-1924af105123

{
    "customerTenantId": "735920EB-A564-4C72-9FE5-52632562712C",
    "customerName": "SURFACE TEST2",
    "customerMarket": "US",
    "id": "B76412DA-D382-4688-A6A4-711A207C1C2E",
    "status": "ACTIVE",
    "productName": "UNKNOWN",
    "subscriptionType": "Azure",
    "autoRenewEnabled": true,
    "partnerId": "3B33E682-00C3-41EE-9DD2-A548ADF56438",
    "friendlyName": "MICROSOFT AZURE",
    "creationDate": "2017-06-02T23:11:58.747",
    "effectiveStartDate": "2017-06-02T00:00:00",
    "commitmentEndDate": null,
    "currentStateEndDate": null,
    "trialToPaidConversionDate": null,
    "trialStartDate": null,
    "trialEndDate": null,
    "lastUsageDate": null,
    "deprovisionedDate": null,
    "lastRenewalDate": null,
    "licenseCount": 0
}
```

## <a name="see-also"></a><span data-ttu-id="4e3a1-227">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="4e3a1-227">See also</span></span>

- [<span data-ttu-id="4e3a1-228">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="4e3a1-228">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
