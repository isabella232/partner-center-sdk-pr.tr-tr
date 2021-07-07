---
title: Müşterinin kullanım harcama bütçesini güncelleştirme
description: Müşterinin kullanımı için ayrılan harcama bütçesini güncelleştirin.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 043bd442266d081105e5e8767b6d597e89fc9e8b
ms.sourcegitcommit: 4275f9f67f9479ce27af6a9fda96fe86d0bc0b44
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/05/2021
ms.locfileid: "111529724"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="04da2-103">Müşterinin kullanım harcama bütçesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="04da2-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="04da2-104">**Uygulama hedefi**: Iş Ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="04da2-104">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="04da2-105">Müşterinin kullanımı için ayrılan [harcama bütçesini](customer-usage-resources.md#customerusagesummary) güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="04da2-105">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="04da2-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="04da2-106">Prerequisites</span></span>

- <span data-ttu-id="04da2-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="04da2-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="04da2-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="04da2-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="04da2-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="04da2-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="04da2-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="04da2-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="04da2-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="04da2-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="04da2-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="04da2-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="04da2-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="04da2-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="04da2-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="04da2-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="04da2-115">C\#</span><span class="sxs-lookup"><span data-stu-id="04da2-115">C\#</span></span>

<span data-ttu-id="04da2-116">Müşterinin kullanım harcama bütçesini güncelleştirmek için, önce güncelleştirilmiş tutara sahip yeni bir [**Spendingbütçe**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="04da2-116">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="04da2-117">Ardından, [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) koleksiyonunu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini belirtilen müşterinin kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="04da2-117">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="04da2-118">Ardından [**usagebütçe**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) özelliğine erişin ve güncelleştirilmiş kullanım bütçesini [**Patch ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) veya [**patchasync ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="04da2-118">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;

// Create a new spending budget with the udpated amount.
var newUsageBudget = new SpendingBudget()
{
    Amount = 100
};

// Update the customer's usage budget.
var usageBudget = partnerOperations.Customers.ById(selectedCustomerId).UsageBudget.Patch(newUsageBudget);
```

## <a name="rest-request"></a><span data-ttu-id="04da2-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="04da2-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="04da2-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="04da2-120">Request syntax</span></span>

| <span data-ttu-id="04da2-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="04da2-121">Method</span></span>    | <span data-ttu-id="04da2-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="04da2-122">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="04da2-123">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="04da2-123">**PATCH**</span></span> | <span data-ttu-id="04da2-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagebütçe http/1.1</span><span class="sxs-lookup"><span data-stu-id="04da2-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="04da2-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="04da2-125">URI parameter</span></span>

<span data-ttu-id="04da2-126">Faturalandırma profilini güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="04da2-126">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="04da2-127">Ad</span><span class="sxs-lookup"><span data-stu-id="04da2-127">Name</span></span>                   | <span data-ttu-id="04da2-128">Tür</span><span class="sxs-lookup"><span data-stu-id="04da2-128">Type</span></span>     | <span data-ttu-id="04da2-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="04da2-129">Required</span></span> | <span data-ttu-id="04da2-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="04da2-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="04da2-131">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="04da2-131">**customer-tenant-id**</span></span> | <span data-ttu-id="04da2-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="04da2-132">**guid**</span></span> | <span data-ttu-id="04da2-133">Y</span><span class="sxs-lookup"><span data-stu-id="04da2-133">Y</span></span>        | <span data-ttu-id="04da2-134">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="04da2-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="04da2-135">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="04da2-135">Request headers</span></span>

<span data-ttu-id="04da2-136">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="04da2-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="04da2-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="04da2-137">Request body</span></span>

<span data-ttu-id="04da2-138">Tam kaynak.</span><span class="sxs-lookup"><span data-stu-id="04da2-138">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="04da2-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="04da2-139">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/usagebudget HTTP/1.1
Authorization: Bearer <token>
Accept: application/json, text/plain, */*
MS-RequestId: 312b044d-dc41-4b37-c2d5-7d27322d9654
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
Content-Type: application/json;charset=utf-8
X-Locale: "en-US"

{
     "Amount": 100,
     "Attributes": {
          "ObjectType": "SpendingBudget"
     }
}
```

## <a name="rest-response"></a><span data-ttu-id="04da2-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="04da2-140">REST response</span></span>

<span data-ttu-id="04da2-141">Başarılı olursa, bu yöntem bir kullanıcının harcama bütçesini güncelleştirilmiş tutara döndürür.</span><span class="sxs-lookup"><span data-stu-id="04da2-141">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="04da2-142">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="04da2-142">Response success and error codes</span></span>

<span data-ttu-id="04da2-143">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="04da2-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="04da2-144">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="04da2-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="04da2-145">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="04da2-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="04da2-146">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="04da2-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 12014
Content-Type: application/json
MS-CorrelationId: 7cb67bb7-4750-403d-cc2e-6bc44c52d52c
MS-RequestId: be82a8ba-4a53-49f7-8313-b033c058687e
Date: Tue, 10 Nov 2015 19:09:59 GMT

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
            "method":"PATCH",
            "headers":[]
        }
    }
}
```
