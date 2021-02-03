---
title: Arama sorgusuna abonelik Analizi al
description: Bir arama sorgusuyla filtrelenmiş abonelik Analizi bilgilerini alma.
ms.date: 05/10/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c1046ea3c7e813eedae4890eebf6356337c80ede
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769053"
---
# <a name="get-subscription-analytics-information-filtered-by-a-search-query"></a><span data-ttu-id="a05c5-103">Bir arama sorgusuyla filtrelenmiş abonelik analizi bilgilerini alma</span><span class="sxs-lookup"><span data-stu-id="a05c5-103">Get subscription analytics information filtered by a search query</span></span>

<span data-ttu-id="a05c5-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="a05c5-104">**Applies To**</span></span>

- <span data-ttu-id="a05c5-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a05c5-105">Partner Center</span></span>
- <span data-ttu-id="a05c5-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a05c5-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a05c5-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a05c5-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a05c5-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a05c5-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a05c5-109">Bir arama sorgusuyla filtrelenmiş müşterileriniz için abonelik Analizi bilgilerini alma.</span><span class="sxs-lookup"><span data-stu-id="a05c5-109">How to get subscription analytics information for your customers filtered by a search query.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a05c5-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a05c5-110">Prerequisites</span></span>

- <span data-ttu-id="a05c5-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a05c5-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a05c5-112">Bu senaryo yalnızca Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a05c5-112">This scenario supports authentication with User credentials only.</span></span>

## <a name="rest-request"></a><span data-ttu-id="a05c5-113">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a05c5-113">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a05c5-114">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a05c5-114">Request syntax</span></span>

| <span data-ttu-id="a05c5-115">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a05c5-115">Method</span></span> | <span data-ttu-id="a05c5-116">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a05c5-116">Request URI</span></span> |
|--------|-------------|
| <span data-ttu-id="a05c5-117">**Al**</span><span class="sxs-lookup"><span data-stu-id="a05c5-117">**GET**</span></span> | <span data-ttu-id="a05c5-118">[*\{ BaseUrl \}*](partner-center-rest-urls.md)/partner/v1/analiz Tics/abonelikleri? Filter = {filter_string}</span><span class="sxs-lookup"><span data-stu-id="a05c5-118">[*\{baseURL\}*](partner-center-rest-urls.md)/partner/v1/analytics/subscriptions?filter={filter_string}</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="a05c5-119">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a05c5-119">URI parameters</span></span>

<span data-ttu-id="a05c5-120">Kuruluşunuzu tanımlamak ve aramayı filtrelemek için aşağıdaki gerekli yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a05c5-120">Use the following required path parameter to identify your organization and filter the search.</span></span>

| <span data-ttu-id="a05c5-121">Ad</span><span class="sxs-lookup"><span data-stu-id="a05c5-121">Name</span></span> | <span data-ttu-id="a05c5-122">Tür</span><span class="sxs-lookup"><span data-stu-id="a05c5-122">Type</span></span> | <span data-ttu-id="a05c5-123">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a05c5-123">Required</span></span> | <span data-ttu-id="a05c5-124">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a05c5-124">Description</span></span> |
|------|------|----------|-------------|
| <span data-ttu-id="a05c5-125">filter_string</span><span class="sxs-lookup"><span data-stu-id="a05c5-125">filter_string</span></span> | <span data-ttu-id="a05c5-126">string</span><span class="sxs-lookup"><span data-stu-id="a05c5-126">string</span></span> | <span data-ttu-id="a05c5-127">Yes</span><span class="sxs-lookup"><span data-stu-id="a05c5-127">Yes</span></span> | <span data-ttu-id="a05c5-128">Abonelik analizinden uygulanacak filtre.</span><span class="sxs-lookup"><span data-stu-id="a05c5-128">The filter to apply to the subscription analytics.</span></span> <span data-ttu-id="a05c5-129">Bu parametrede kullanılacak söz dizimi, alanlar ve işleçler için filtre söz dizimini ve filtre alanları bölümlerine bakın.</span><span class="sxs-lookup"><span data-stu-id="a05c5-129">See the Filter syntax and Filter fields sections for the syntax, fields, and operators to use in this parameter.</span></span> |

### <a name="filter-syntax"></a><span data-ttu-id="a05c5-130">Filtre sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a05c5-130">Filter syntax</span></span>

<span data-ttu-id="a05c5-131">Filter parametresi bir dizi alan, değer ve işleç birleşimi olarak oluşturulmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a05c5-131">The filter parameter must be composed as a series of field, value, and operator combinations.</span></span> <span data-ttu-id="a05c5-132">Birden çok bileşim, **`and`** veya işleçleri kullanılarak birleştirilebilir **`or`** .</span><span class="sxs-lookup"><span data-stu-id="a05c5-132">Multiple combinations can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="a05c5-133">Kodlanamayan bir örnek şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="a05c5-133">An unencoded example looks like this:</span></span>

- <span data-ttu-id="a05c5-134">Dizisinde `?filter=Field operator 'Value'`</span><span class="sxs-lookup"><span data-stu-id="a05c5-134">String: `?filter=Field operator 'Value'`</span></span>
- <span data-ttu-id="a05c5-135">Boolean `?filter=Field operator Value`</span><span class="sxs-lookup"><span data-stu-id="a05c5-135">Boolean: `?filter=Field operator Value`</span></span>
- <span data-ttu-id="a05c5-136">Vardır `?filter=contains(field,'value')`</span><span class="sxs-lookup"><span data-stu-id="a05c5-136">Contains `?filter=contains(field,'value')`</span></span>

### <a name="filter-fields"></a><span data-ttu-id="a05c5-137">Filtre alanları</span><span class="sxs-lookup"><span data-stu-id="a05c5-137">Filter fields</span></span>

<span data-ttu-id="a05c5-138">İsteğin filtre parametresi, yanıttaki satırları filtreleyen bir veya daha fazla deyim içeriyor.</span><span class="sxs-lookup"><span data-stu-id="a05c5-138">The filter parameter of the request contains one or more statements that filter the rows in the response.</span></span> <span data-ttu-id="a05c5-139">Her bir ifade, **`eq`** veya işleçleriyle ilişkili bir alan ve değer içerir **`ne`** .</span><span class="sxs-lookup"><span data-stu-id="a05c5-139">Each statement contains a field and value that are associated with the **`eq`** or **`ne`** operators.</span></span> <span data-ttu-id="a05c5-140">Bazı alanlar,,, **`contains`** , **`gt`** **`lt`** **`ge`** ve **`le`** işleçlerini da destekler.</span><span class="sxs-lookup"><span data-stu-id="a05c5-140">Some fields also support the **`contains`**, **`gt`**, **`lt`**, **`ge`**, and **`le`** operators.</span></span> <span data-ttu-id="a05c5-141">Deyimler, **`and`** veya işleçleri kullanılarak birleştirilebilir **`or`** .</span><span class="sxs-lookup"><span data-stu-id="a05c5-141">Statements can be combined using **`and`** or **`or`** operators.</span></span>

<span data-ttu-id="a05c5-142">Filtre dizelerinin örnekleri aşağıda verilmiştir:</span><span class="sxs-lookup"><span data-stu-id="a05c5-142">The following are examples of filter strings:</span></span>

```http
autoRenewEnabled eq true

autoRenewEnabled eq true and customerMarket eq 'US'
```

<span data-ttu-id="a05c5-143">Aşağıdaki tabloda, filtre parametresi için desteklenen alanların ve destek işleçlerinin listesi gösterilmektedir.</span><span class="sxs-lookup"><span data-stu-id="a05c5-143">The following table shows a list of the supported fields and support operators for the filter parameter.</span></span> <span data-ttu-id="a05c5-144">Dize değerleri tek tırnak işareti içine alınmalıdır.</span><span class="sxs-lookup"><span data-stu-id="a05c5-144">String values must be surrounded by single quotes.</span></span>

| <span data-ttu-id="a05c5-145">Parametre</span><span class="sxs-lookup"><span data-stu-id="a05c5-145">Parameter</span></span> | <span data-ttu-id="a05c5-146">Desteklenen işleçler</span><span class="sxs-lookup"><span data-stu-id="a05c5-146">Supported operators</span></span> | <span data-ttu-id="a05c5-147">Description</span><span class="sxs-lookup"><span data-stu-id="a05c5-147">Description</span></span> |
|-----------|---------------------|-------------|
| <span data-ttu-id="a05c5-148">autoRenewEnabled</span><span class="sxs-lookup"><span data-stu-id="a05c5-148">autoRenewEnabled</span></span> | <span data-ttu-id="a05c5-149">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-149">`eq`, `ne`</span></span> | <span data-ttu-id="a05c5-150">Aboneliğin otomatik olarak yenilenip yenilenmediğini gösteren bir değer.</span><span class="sxs-lookup"><span data-stu-id="a05c5-150">A value indicating whether the subscription is renewed automatically.</span></span> |
| <span data-ttu-id="a05c5-151">commitmentEndDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-151">commitmentEndDate</span></span> | <span data-ttu-id="a05c5-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-152">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="a05c5-153">Aboneliğin bitiş tarihi.</span><span class="sxs-lookup"><span data-stu-id="a05c5-153">The date the subscription ends.</span></span> |
| <span data-ttu-id="a05c5-154">creationDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-154">creationDate</span></span> | <span data-ttu-id="a05c5-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-155">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="a05c5-156">Aboneliğin oluşturulduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="a05c5-156">The date the subscription was created.</span></span> |
| <span data-ttu-id="a05c5-157">currentStateEndDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-157">currentStateEndDate</span></span> | <span data-ttu-id="a05c5-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-158">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="a05c5-159">Aboneliğin geçerli durumunun değiştirileceği tarih.</span><span class="sxs-lookup"><span data-stu-id="a05c5-159">The date that the current status of the subscription will change.</span></span> |
| <span data-ttu-id="a05c5-160">customerMarket</span><span class="sxs-lookup"><span data-stu-id="a05c5-160">customerMarket</span></span> | <span data-ttu-id="a05c5-161">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-161">`eq`, `ne`</span></span> | <span data-ttu-id="a05c5-162">Müşterinin iş üzerinde kullandığı ülke/bölge.</span><span class="sxs-lookup"><span data-stu-id="a05c5-162">The country/region that the customer does business in.</span></span> |
| <span data-ttu-id="a05c5-163">customerName</span><span class="sxs-lookup"><span data-stu-id="a05c5-163">customerName</span></span> | `contains` | <span data-ttu-id="a05c5-164">Müşterinin adı.</span><span class="sxs-lookup"><span data-stu-id="a05c5-164">The name of the customer.</span></span> |
| <span data-ttu-id="a05c5-165">Customertenantıd</span><span class="sxs-lookup"><span data-stu-id="a05c5-165">customerTenantId</span></span> | <span data-ttu-id="a05c5-166">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-166">`eq`, `ne`</span></span> | <span data-ttu-id="a05c5-167">Müşteri kiracısını tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="a05c5-167">A GUID-formatted string that identifies the customer tenant.</span></span> |
| <span data-ttu-id="a05c5-168">deprovisionedDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-168">deprovisionedDate</span></span> | <span data-ttu-id="a05c5-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-169">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="a05c5-170">Aboneliğin sağlaması kaldırılmış olan tarih.</span><span class="sxs-lookup"><span data-stu-id="a05c5-170">The date that the subscription was deprovisioned.</span></span> <span data-ttu-id="a05c5-171">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="a05c5-171">The default value is null.</span></span> |
| <span data-ttu-id="a05c5-172">effectiveStartDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-172">effectiveStartDate</span></span> | <span data-ttu-id="a05c5-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-173">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="a05c5-174">Aboneliğin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="a05c5-174">The date the subscription starts.</span></span> |
| <span data-ttu-id="a05c5-175">friendlyName</span><span class="sxs-lookup"><span data-stu-id="a05c5-175">friendlyName</span></span> | `contains` | <span data-ttu-id="a05c5-176">Aboneliğin adı.</span><span class="sxs-lookup"><span data-stu-id="a05c5-176">The name of the subscription.</span></span> |
| <span data-ttu-id="a05c5-177">kimlik</span><span class="sxs-lookup"><span data-stu-id="a05c5-177">id</span></span> | <span data-ttu-id="a05c5-178">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-178">`eq`, `ne`</span></span> | <span data-ttu-id="a05c5-179">Aboneliği tanımlayan GUID biçimli bir dize.</span><span class="sxs-lookup"><span data-stu-id="a05c5-179">A GUID-formatted string that identifies the subscription.</span></span> |
| <span data-ttu-id="a05c5-180">lastRenewalDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-180">lastRenewalDate</span></span> | <span data-ttu-id="a05c5-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-181">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="a05c5-182">Aboneliğin son yenilenme tarihi.</span><span class="sxs-lookup"><span data-stu-id="a05c5-182">The date that the subscription was last renewed.</span></span> <span data-ttu-id="a05c5-183">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="a05c5-183">The default value is null.</span></span> |
| <span data-ttu-id="a05c5-184">lastUsageDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-184">lastUsageDate</span></span> | <span data-ttu-id="a05c5-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-185">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="a05c5-186">Aboneliğin son kullanıldığı tarih.</span><span class="sxs-lookup"><span data-stu-id="a05c5-186">The date that the subscription was last used.</span></span> <span data-ttu-id="a05c5-187">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="a05c5-187">The default value is null.</span></span> |
| <span data-ttu-id="a05c5-188">iş ortağı kimliği</span><span class="sxs-lookup"><span data-stu-id="a05c5-188">partnerId</span></span> | <span data-ttu-id="a05c5-189">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-189">`eq`, `ne`</span></span> | <span data-ttu-id="a05c5-190">MPN KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="a05c5-190">The MPN ID.</span></span> <span data-ttu-id="a05c5-191">Doğrudan satıcı için bu değer ortağın MPN KIMLIĞI olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a05c5-191">For a direct reseller, this value will be the MPN ID of the partner.</span></span> <span data-ttu-id="a05c5-192">Dolaylı bir satıcı için, bu değer dolaylı satıcının MPN KIMLIĞI olacaktır.</span><span class="sxs-lookup"><span data-stu-id="a05c5-192">For an indirect reseller, this value will be the MPN ID of the indirect reseller.</span></span> |
| <span data-ttu-id="a05c5-193">partnerName</span><span class="sxs-lookup"><span data-stu-id="a05c5-193">partnerName</span></span> | <span data-ttu-id="a05c5-194">string</span><span class="sxs-lookup"><span data-stu-id="a05c5-194">string</span></span> | <span data-ttu-id="a05c5-195">Aboneliğin satın alındığı ortağın adı</span><span class="sxs-lookup"><span data-stu-id="a05c5-195">Name of the partner for whom the subscription was purchased</span></span> |
| <span data-ttu-id="a05c5-196">productName</span><span class="sxs-lookup"><span data-stu-id="a05c5-196">productName</span></span> | <span data-ttu-id="a05c5-197">`contains`, `eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-197">`contains`, `eq`, `ne`</span></span> | <span data-ttu-id="a05c5-198">Ürünün adı.</span><span class="sxs-lookup"><span data-stu-id="a05c5-198">The name of the product.</span></span> |
| <span data-ttu-id="a05c5-199">Adı</span><span class="sxs-lookup"><span data-stu-id="a05c5-199">providerName</span></span> | <span data-ttu-id="a05c5-200">string</span><span class="sxs-lookup"><span data-stu-id="a05c5-200">string</span></span> | <span data-ttu-id="a05c5-201">Abonelik işlemi dolaylı satıcı için olduğunda, sağlayıcı adı aboneliği satın alan dolaylı sağlayıcıdır.</span><span class="sxs-lookup"><span data-stu-id="a05c5-201">When subscription transaction is for the indirect reseller, provider name is the indirect provider who bought the subscription.</span></span>|
| <span data-ttu-id="a05c5-202">durum</span><span class="sxs-lookup"><span data-stu-id="a05c5-202">status</span></span> | <span data-ttu-id="a05c5-203">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-203">`eq`, `ne`</span></span> | <span data-ttu-id="a05c5-204">Abonelik durumu.</span><span class="sxs-lookup"><span data-stu-id="a05c5-204">The subscription status.</span></span> <span data-ttu-id="a05c5-205">Desteklenen değerler şunlardır: "ETKIN", "askıya ALıNDı" veya "SAĞLAMASı KALDıRıLDı".</span><span class="sxs-lookup"><span data-stu-id="a05c5-205">Supported values are: "ACTIVE", "SUSPENDED", or "DEPROVISIONED".</span></span> |
| <span data-ttu-id="a05c5-206">subscriptionType</span><span class="sxs-lookup"><span data-stu-id="a05c5-206">subscriptionType</span></span> | <span data-ttu-id="a05c5-207">`eq`, `ne`</span><span class="sxs-lookup"><span data-stu-id="a05c5-207">`eq`, `ne`</span></span> | <span data-ttu-id="a05c5-208">Abonelik türü.</span><span class="sxs-lookup"><span data-stu-id="a05c5-208">The subscription type.</span></span> <span data-ttu-id="a05c5-209">**Note**: Bu alan, büyük/küçük harfe duyarlıdır.</span><span class="sxs-lookup"><span data-stu-id="a05c5-209">**Note**: This field is case-sensitive.</span></span> <span data-ttu-id="a05c5-210">Desteklenen değerler şunlardır: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span><span class="sxs-lookup"><span data-stu-id="a05c5-210">Supported values are: "Office", "Azure", "Microsoft365", "Dynamics", "EMS".</span></span> |
| <span data-ttu-id="a05c5-211">trialStartDate</span><span class="sxs-lookup"><span data-stu-id="a05c5-211">trialStartDate</span></span> | <span data-ttu-id="a05c5-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-212">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span> | <span data-ttu-id="a05c5-213">Abonelik için deneme süresinin başladığı tarih.</span><span class="sxs-lookup"><span data-stu-id="a05c5-213">The date that the trial period for the subscription started.</span></span> <span data-ttu-id="a05c5-214">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="a05c5-214">The default value is null.</span></span> |
| <span data-ttu-id="a05c5-215">Trialtopaıdconversiondate</span><span class="sxs-lookup"><span data-stu-id="a05c5-215">trialToPaidConversionDate</span></span> | <span data-ttu-id="a05c5-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span><span class="sxs-lookup"><span data-stu-id="a05c5-216">`eq`, `ne`, `gt`, `lt`, `ge`, `le`</span></span>  | <span data-ttu-id="a05c5-217">Aboneliğin deneme sürümünden ücretli olarak dönüştürdüğü tarih.</span><span class="sxs-lookup"><span data-stu-id="a05c5-217">The date that the subscription converts from trial to paid.</span></span> <span data-ttu-id="a05c5-218">Varsayılan değer boştur.</span><span class="sxs-lookup"><span data-stu-id="a05c5-218">The default value is null.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a05c5-219">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a05c5-219">Request headers</span></span>

<span data-ttu-id="a05c5-220">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a05c5-220">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a05c5-221">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a05c5-221">Request body</span></span>

<span data-ttu-id="a05c5-222">Yok.</span><span class="sxs-lookup"><span data-stu-id="a05c5-222">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a05c5-223">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a05c5-223">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/partner/v1/analytics/subscriptions?filter=autoRenewEnabled eq true
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: ca7c39f7-1a80-43bc-90d8-ee7d1cad3123
MS-CorrelationId: ec8f62e5-1d92-47e9-8d5d-1924af105123
Content-Type: application/json
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="a05c5-224">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a05c5-224">REST response</span></span>

<span data-ttu-id="a05c5-225">Başarılı olursa, yanıt gövdesi, filtre ölçütlerini karşılayan bir [abonelik](partner-center-analytics-resources.md#subscription-resource) kaynakları koleksiyonu içerir.</span><span class="sxs-lookup"><span data-stu-id="a05c5-225">If successful, the response body contains a collection of [Subscription](partner-center-analytics-resources.md#subscription-resource) resources that meet the filter criteria.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a05c5-226">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a05c5-226">Response success and error codes</span></span>

<span data-ttu-id="a05c5-227">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a05c5-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a05c5-228">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a05c5-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a05c5-229">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a05c5-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a05c5-230">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a05c5-230">Response example</span></span>

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

## <a name="see-also"></a><span data-ttu-id="a05c5-231">Ayrıca bkz.</span><span class="sxs-lookup"><span data-stu-id="a05c5-231">See also</span></span>

- [<span data-ttu-id="a05c5-232">İş Ortağı Merkezi Analizi - Kaynaklar</span><span class="sxs-lookup"><span data-stu-id="a05c5-232">Partner Center Analytics - Resources</span></span>](partner-center-analytics-resources.md)
