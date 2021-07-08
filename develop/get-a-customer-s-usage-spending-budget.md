---
title: Müşterinin kullanım harcama bütçesini al
description: Müşteri kullanım özetini (CustomerUsageSummary kaynağı) güncelleştirmek için bir harcama bütçesi (SpendingBudget nesnesi) kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b55f59fff7e5d7865811ecab3e901848126d31f7
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874882"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="41c31-103">Müşterinin kullanım harcama bütçesini al</span><span class="sxs-lookup"><span data-stu-id="41c31-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="41c31-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="41c31-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="41c31-105">Harcama bütçesini **(SpendingBudget** nesnesi) müşteri kullanım özetini [ **(CustomerUsageSummary** kaynağı) güncelleştirebilirsiniz.](customer-usage-resources.md#customerusagesummary)</span><span class="sxs-lookup"><span data-stu-id="41c31-105">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="41c31-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="41c31-106">Prerequisites</span></span>

- <span data-ttu-id="41c31-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="41c31-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="41c31-108">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="41c31-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="41c31-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="41c31-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="41c31-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="41c31-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="41c31-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="41c31-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="41c31-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="41c31-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="41c31-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="41c31-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="41c31-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="41c31-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="41c31-115">C\#</span><span class="sxs-lookup"><span data-stu-id="41c31-115">C\#</span></span>

<span data-ttu-id="41c31-116">Müşterinin kullanım harcama bütçesini güncelleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="41c31-116">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="41c31-117">Güncelleştirilmiş [**tutara sahip yeni bir SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="41c31-117">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="41c31-118">Belirtilen müşterinin tanımlayıcısıyla [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağıran [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) koleksiyonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="41c31-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="41c31-119">Müşterinin kullanım [**bütçesini**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) almak için Get veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="41c31-119">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Get();
```

## <a name="rest-request"></a><span data-ttu-id="41c31-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="41c31-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="41c31-121">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="41c31-121">Request syntax</span></span>

| <span data-ttu-id="41c31-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="41c31-122">Method</span></span>    | <span data-ttu-id="41c31-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="41c31-123">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="41c31-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="41c31-124">**GET**</span></span> | <span data-ttu-id="41c31-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="41c31-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="41c31-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="41c31-126">URI parameter</span></span>

<span data-ttu-id="41c31-127">Faturalama profilini güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="41c31-127">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="41c31-128">Ad</span><span class="sxs-lookup"><span data-stu-id="41c31-128">Name</span></span>                   | <span data-ttu-id="41c31-129">Tür</span><span class="sxs-lookup"><span data-stu-id="41c31-129">Type</span></span>     | <span data-ttu-id="41c31-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="41c31-130">Required</span></span> | <span data-ttu-id="41c31-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="41c31-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="41c31-132">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="41c31-132">**customer-tenant-id**</span></span> | <span data-ttu-id="41c31-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="41c31-133">**guid**</span></span> | <span data-ttu-id="41c31-134">Y</span><span class="sxs-lookup"><span data-stu-id="41c31-134">Y</span></span>        | <span data-ttu-id="41c31-135">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="41c31-135">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="41c31-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="41c31-136">Request headers</span></span>

<span data-ttu-id="41c31-137">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="41c31-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="41c31-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="41c31-138">Request body</span></span>

<span data-ttu-id="41c31-139">Tam kaynak.</span><span class="sxs-lookup"><span data-stu-id="41c31-139">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="41c31-140">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="41c31-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="41c31-141">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="41c31-141">REST response</span></span>

<span data-ttu-id="41c31-142">Başarılı olursa bu yöntem, güncelleştirilmiş tutara sahip bir kullanıcının harcama bütçesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="41c31-142">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="41c31-143">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="41c31-143">Response success and error codes</span></span>

<span data-ttu-id="41c31-144">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="41c31-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="41c31-145">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="41c31-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="41c31-146">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="41c31-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="41c31-147">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="41c31-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 17 Sep 2019 20:31:45 GMT

{
    {
        "amount": 100,
        "usageSpendingBudget": 100,
        "attributes":{
            "objectType":"SpendingBudget"
        }
    },
    "links":{
        "self":{
            "uri":"/v1/customers/<customer-tenant-id>/usagebudget",
            "method":"GET",
            "headers":[]
        }
    }
}
```
