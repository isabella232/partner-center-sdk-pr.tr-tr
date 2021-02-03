---
title: Müşterinin kullanım harcama bütçesini güncelleştirme
description: Müşterinin kullanımı için ayrılan harcama bütçesini güncelleştirin.
ms.date: 02/05/2018
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 839305fb8fad3ce2442ab93e1d8a4a170b4d41c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769760"
---
# <a name="update-a-customers-usage-spending-budget"></a><span data-ttu-id="0d32e-103">Müşterinin kullanım harcama bütçesini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="0d32e-103">Update a customer's usage spending budget</span></span>

<span data-ttu-id="0d32e-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="0d32e-104">**Applies To**</span></span>

- <span data-ttu-id="0d32e-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0d32e-105">Partner Center</span></span>
- <span data-ttu-id="0d32e-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0d32e-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0d32e-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0d32e-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0d32e-108">Müşterinin kullanımı için ayrılan [harcama bütçesini](customer-usage-resources.md#customerusagesummary) güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="0d32e-108">Update the [spending budget](customer-usage-resources.md#customerusagesummary) allocated for a customer's usage.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0d32e-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0d32e-109">Prerequisites</span></span>

- <span data-ttu-id="0d32e-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0d32e-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0d32e-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="0d32e-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0d32e-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0d32e-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0d32e-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0d32e-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0d32e-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="0d32e-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0d32e-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0d32e-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0d32e-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="0d32e-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0d32e-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="0d32e-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0d32e-118">C\#</span><span class="sxs-lookup"><span data-stu-id="0d32e-118">C\#</span></span>

<span data-ttu-id="0d32e-119">Müşterinin kullanım harcama bütçesini güncelleştirmek için, önce güncelleştirilmiş tutara sahip yeni bir [**Spendingbütçe**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="0d32e-119">To update a customer's usage spending budget, first create a new [**SpendingBudget**](/dotnet/api/microsoft.store.partnercenter.models.usage.spendingbudget) object with the updated amount.</span></span> <span data-ttu-id="0d32e-120">Ardından, [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) koleksiyonunu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini belirtilen müşterinin kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="0d32e-120">Then use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer's ID.</span></span> <span data-ttu-id="0d32e-121">Ardından [**usagebütçe**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) özelliğine erişin ve güncelleştirilmiş kullanım bütçesini [**Patch ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) veya [**patchasync ()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="0d32e-121">Then access the [**UsageBudget**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.usagebudget) property and pass the updated usage budget to the [**Patch()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patch) or [**PatchAsync()**](/dotnet/api/microsoft.store.partnercenter.usage.icustomerusagespendingbudget.patchasync) method.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="0d32e-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0d32e-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0d32e-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0d32e-123">Request syntax</span></span>

| <span data-ttu-id="0d32e-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0d32e-124">Method</span></span>    | <span data-ttu-id="0d32e-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0d32e-125">Request URI</span></span>                                                                                             |
|-----------|---------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0d32e-126">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="0d32e-126">**PATCH**</span></span> | <span data-ttu-id="0d32e-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/usagebütçe http/1.1</span><span class="sxs-lookup"><span data-stu-id="0d32e-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/usagebudget  HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="0d32e-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="0d32e-128">URI parameter</span></span>

<span data-ttu-id="0d32e-129">Faturalandırma profilini güncelleştirmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d32e-129">Use the following query parameter to update the billing profile.</span></span>

| <span data-ttu-id="0d32e-130">Ad</span><span class="sxs-lookup"><span data-stu-id="0d32e-130">Name</span></span>                   | <span data-ttu-id="0d32e-131">Tür</span><span class="sxs-lookup"><span data-stu-id="0d32e-131">Type</span></span>     | <span data-ttu-id="0d32e-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0d32e-132">Required</span></span> | <span data-ttu-id="0d32e-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0d32e-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0d32e-134">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="0d32e-134">**customer-tenant-id**</span></span> | <span data-ttu-id="0d32e-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="0d32e-135">**guid**</span></span> | <span data-ttu-id="0d32e-136">Y</span><span class="sxs-lookup"><span data-stu-id="0d32e-136">Y</span></span>        | <span data-ttu-id="0d32e-137">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="0d32e-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0d32e-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0d32e-138">Request headers</span></span>

<span data-ttu-id="0d32e-139">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0d32e-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0d32e-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0d32e-140">Request body</span></span>

<span data-ttu-id="0d32e-141">Tam kaynak.</span><span class="sxs-lookup"><span data-stu-id="0d32e-141">The full resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="0d32e-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0d32e-142">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0d32e-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0d32e-143">REST response</span></span>

<span data-ttu-id="0d32e-144">Başarılı olursa, bu yöntem bir kullanıcının harcama bütçesini güncelleştirilmiş tutara döndürür.</span><span class="sxs-lookup"><span data-stu-id="0d32e-144">If successful, this method returns a user's spending budget with the updated amount.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0d32e-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0d32e-145">Response success and error codes</span></span>

<span data-ttu-id="0d32e-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="0d32e-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0d32e-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0d32e-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0d32e-148">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0d32e-148">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0d32e-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0d32e-149">Response example</span></span>

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
