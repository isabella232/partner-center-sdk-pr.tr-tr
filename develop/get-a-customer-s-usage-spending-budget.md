---
title: Müşterinin kullanım harcama bütçesini alın
description: Bir müşteri kullanım özetini (Müşterusagesummary kaynağı) güncelleştirmek için bir harcama bütçesi (Spendingbütçe nesnesi) kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8be9ceaab6b7546de8eacba1e52e8766719e5125
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769346"
---
# <a name="get-a-customers-usage-spending-budget"></a><span data-ttu-id="664e4-103">Müşterinin kullanım harcama bütçesini alın</span><span class="sxs-lookup"><span data-stu-id="664e4-103">Get a customer's usage spending budget</span></span>

<span data-ttu-id="664e4-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="664e4-104">**Applies to:**</span></span>

- <span data-ttu-id="664e4-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="664e4-105">Partner Center</span></span>
- <span data-ttu-id="664e4-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="664e4-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="664e4-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="664e4-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="664e4-108">Harcama bütçesini ( **Spendingbütçe** nesnesi) [Müşteri kullanım özetinde ( **Müşterusagesummary** kaynağı)](customer-usage-resources.md#customerusagesummary)güncelleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="664e4-108">You can update the spending budget (the **SpendingBudget** object) in the [customer usage summary (the **CustomerUsageSummary** resource)](customer-usage-resources.md#customerusagesummary).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="664e4-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="664e4-109">Prerequisites</span></span>

- <span data-ttu-id="664e4-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="664e4-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="664e4-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="664e4-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="664e4-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="664e4-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="664e4-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="664e4-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="664e4-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="664e4-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="664e4-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="664e4-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="664e4-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="664e4-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="664e4-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="664e4-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="664e4-118">C\#</span><span class="sxs-lookup"><span data-stu-id="664e4-118">C\#</span></span>

<span data-ttu-id="664e4-119">Müşterinin kullanım harcama bütçesini güncelleştirmek için:</span><span class="sxs-lookup"><span data-stu-id="664e4-119">To update a customer's usage spending budget:</span></span>

1. <span data-ttu-id="664e4-120">Güncelleştirilmiş tutarla yeni bir [**Spendingbütçe**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="664e4-120">Create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span>

2. <span data-ttu-id="664e4-121">Belirtilen müşterinin tanımlayıcısına sahip [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırmak Için [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) koleksiyonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="664e4-121">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection to call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's identifier.</span></span>

3. <span data-ttu-id="664e4-122">Müşterinin kullanım bütçesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="664e4-122">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.subscribedskus.icustomersubscribedskucollection.getasync) method to get the customer's usage budget.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="664e4-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="664e4-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="664e4-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="664e4-124">Request syntax</span></span>

| <span data-ttu-id="664e4-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="664e4-125">Method</span></span>    | <span data-ttu-id="664e4-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="664e4-126">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="664e4-127">**Al**</span><span class="sxs-lookup"><span data-stu-id="664e4-127">**GET**</span></span> | <span data-ttu-id="664e4-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagebütçe http/1.1</span><span class="sxs-lookup"><span data-stu-id="664e4-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="664e4-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="664e4-129">URI parameter</span></span>

<span data-ttu-id="664e4-130">Faturalandırma profilini güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="664e4-130">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="664e4-131">Ad</span><span class="sxs-lookup"><span data-stu-id="664e4-131">Name</span></span>                   | <span data-ttu-id="664e4-132">Tür</span><span class="sxs-lookup"><span data-stu-id="664e4-132">Type</span></span>     | <span data-ttu-id="664e4-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="664e4-133">Required</span></span> | <span data-ttu-id="664e4-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="664e4-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="664e4-135">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="664e4-135">**customer-tenant-id**</span></span> | <span data-ttu-id="664e4-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="664e4-136">**guid**</span></span> | <span data-ttu-id="664e4-137">Y</span><span class="sxs-lookup"><span data-stu-id="664e4-137">Y</span></span>        | <span data-ttu-id="664e4-138">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="664e4-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="664e4-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="664e4-139">Request headers</span></span>

<span data-ttu-id="664e4-140">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="664e4-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="664e4-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="664e4-141">Request body</span></span>

<span data-ttu-id="664e4-142">Tam kaynak.</span><span class="sxs-lookup"><span data-stu-id="664e4-142">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="664e4-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="664e4-143">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"
```

## <a name="rest-response"></a><span data-ttu-id="664e4-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="664e4-144">REST response</span></span>

<span data-ttu-id="664e4-145">Başarılı olursa, bu yöntem bir kullanıcının harcama bütçesini güncelleştirilmiş tutara döndürür.</span><span class="sxs-lookup"><span data-stu-id="664e4-145">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="664e4-146">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="664e4-146">Response success and error codes</span></span>

<span data-ttu-id="664e4-147">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="664e4-147">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="664e4-148">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="664e4-148">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="664e4-149">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="664e4-149">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="664e4-150">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="664e4-150">Response example</span></span>

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
