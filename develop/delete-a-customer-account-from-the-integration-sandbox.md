---
title: Tümleştirme korumalı alandan bir müşteri hesabını silme
description: Bir müşteri hesabını Üretimde Test (İpucu) tümleştirme korumalı alandan silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b9d9e44ac9c40bd4e3c7e1a9e04253f853dfd96c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973137"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="0dd37-103">Tümleştirme korumalı alandan bir müşteri hesabını silme</span><span class="sxs-lookup"><span data-stu-id="0dd37-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="0dd37-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="0dd37-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0dd37-105">Bu makalede iş ortağı ile müşteri hesabı arasındaki ilişkiyi kesme ve Üretimde Test (İpucu) tümleştirme korumalı alanı kotasını geri kazanma açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="0dd37-105">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0dd37-106">Bir müşteri hesabını silebilirsiniz. Bu müşteri kiracısı ile ilişkili tüm kaynaklar temiz olur.</span><span class="sxs-lookup"><span data-stu-id="0dd37-106">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0dd37-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0dd37-107">Prerequisites</span></span>

- <span data-ttu-id="0dd37-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0dd37-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0dd37-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="0dd37-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0dd37-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0dd37-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0dd37-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0dd37-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0dd37-112">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="0dd37-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0dd37-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="0dd37-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0dd37-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="0dd37-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0dd37-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="0dd37-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0dd37-116">İpucu Azure Ayrılmış Sanal Makine Örnekleri alanından müşteri silmeden önce tüm yazılım satın alma siparişlerini ve yazılım satın alma siparişlerini iptal etmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="0dd37-116">All Azure Reserved Virtual Machine Instances and software purchase orders must be canceled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="0dd37-117">C\#</span><span class="sxs-lookup"><span data-stu-id="0dd37-117">C\#</span></span>

<span data-ttu-id="0dd37-118">İpucu tümleştirme korumalı alandan bir müşteri silmek için:</span><span class="sxs-lookup"><span data-stu-id="0dd37-118">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="0dd37-119">İş ortağı işlemlerine bir [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) arabirimi almak için İpucu hesabı kimlik bilgilerinizi [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) yöntemine girin.</span><span class="sxs-lookup"><span data-stu-id="0dd37-119">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="0dd37-120">Yetkilendirme koleksiyonunu almak için iş ortağı işlemleri arabirimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0dd37-120">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="0dd37-121">Müşteriyi [**belirtmek için müşteri tanımlayıcısıyla Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="0dd37-121">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="0dd37-122">**Yetkilendirmeler özelliğini** çağırma.</span><span class="sxs-lookup"><span data-stu-id="0dd37-122">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="0dd37-123">Yetkilendirme koleksiyonunu almak için **Get** **veya GetAsync** [**yöntemini**](entitlement-resources.md) çağırma.</span><span class="sxs-lookup"><span data-stu-id="0dd37-123">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="0dd37-124">Bu müşteriye Azure Ayrılmış Sanal Makine Örnekleri satın alma siparişlerini iptal etmelerini sağlar.</span><span class="sxs-lookup"><span data-stu-id="0dd37-124">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are canceled.</span></span> <span data-ttu-id="0dd37-125">Koleksiyonda [**her Yetkilendirme**](entitlement-resources.md) için:</span><span class="sxs-lookup"><span data-stu-id="0dd37-125">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="0dd37-126">Yetkilendirmeyi [**kullanın. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) sipariş koleksiyonundan ilgili [Siparişin](order-resources.md#order) yerel bir kopyasını almak için kullanın.</span><span class="sxs-lookup"><span data-stu-id="0dd37-126">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="0dd37-127">[**Order.Status özelliğini**](order-resources.md#order) "Cancelled" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0dd37-127">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="0dd37-128">Siparişi **güncelleştirmek için Patch()** yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0dd37-128">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="0dd37-129">Tüm siparişleri iptal edin.</span><span class="sxs-lookup"><span data-stu-id="0dd37-129">Cancel all orders.</span></span> <span data-ttu-id="0dd37-130">Örneğin, aşağıdaki kod örneği durumu "İptal Edildi" olana kadar her siparişi yoklama amacıyla bir döngü kullanır.</span><span class="sxs-lookup"><span data-stu-id="0dd37-130">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be canceled.
    ResourceCollection<Entitlement> entitlements = tipAccountPartnerOperations.Customers.ById(customerTenantId).Entitlements.Get();

    // Cancel all orders
    foreach (var entitlement in entitlements)
    {
        var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
        order.Status = "Cancelled";
        order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(order.Id).Patch(order);
    }

    // Keep polling until the status of all orders is "Cancelled".
    bool proceed = true;
    do
    {
        // Check if all the orders were canceled.
        foreach (var entitlement in entitlements)
        {
            var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(entitlement.ReferenceOrder.Id).Get();
            if (!order.Status.Equals("Cancelled", StringComparison.OrdinalIgnoreCase))
            {
                proceed = false;
            }
        }

        // Wait for a few seconds.
        Thread.Sleep(5000);
    }
    while (proceed == false);

    tipAccountPartnerOperations.Customers.ById(customerTenantId).Delete();
    ```

5. <span data-ttu-id="0dd37-131">Müşteri için Delete yöntemi çağrılarak tüm siparişlerin **iptal** edildiğine emin olun.</span><span class="sxs-lookup"><span data-stu-id="0dd37-131">Make sure all orders are canceled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="0dd37-132">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0dd37-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0dd37-133">**Project:** İş Ortağı Merkezi PartnerCenterSDK.FeaturesSamples **Sınıfı:** DeleteCustomerFromTipAccount.cs</span><span class="sxs-lookup"><span data-stu-id="0dd37-133">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0dd37-134">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0dd37-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0dd37-135">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="0dd37-135">Request syntax</span></span>

| <span data-ttu-id="0dd37-136">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0dd37-136">Method</span></span>     | <span data-ttu-id="0dd37-137">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0dd37-137">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="0dd37-138">DELETE</span><span class="sxs-lookup"><span data-stu-id="0dd37-138">DELETE</span></span>     | <span data-ttu-id="0dd37-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0dd37-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="0dd37-140">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="0dd37-140">URI parameter</span></span>

<span data-ttu-id="0dd37-141">Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0dd37-141">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="0dd37-142">Ad</span><span class="sxs-lookup"><span data-stu-id="0dd37-142">Name</span></span>                   | <span data-ttu-id="0dd37-143">Tür</span><span class="sxs-lookup"><span data-stu-id="0dd37-143">Type</span></span>     | <span data-ttu-id="0dd37-144">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0dd37-144">Required</span></span> | <span data-ttu-id="0dd37-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0dd37-145">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="0dd37-146">customer-tenant-id</span><span class="sxs-lookup"><span data-stu-id="0dd37-146">customer-tenant-id</span></span>     | <span data-ttu-id="0dd37-147">GUID</span><span class="sxs-lookup"><span data-stu-id="0dd37-147">GUID</span></span>     | <span data-ttu-id="0dd37-148">Y</span><span class="sxs-lookup"><span data-stu-id="0dd37-148">Y</span></span>        | <span data-ttu-id="0dd37-149">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="0dd37-149">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0dd37-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0dd37-150">Request headers</span></span>

<span data-ttu-id="0dd37-151">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0dd37-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0dd37-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0dd37-152">Request body</span></span>

<span data-ttu-id="0dd37-153">Yok.</span><span class="sxs-lookup"><span data-stu-id="0dd37-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0dd37-154">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0dd37-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="0dd37-155">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0dd37-155">REST response</span></span>

<span data-ttu-id="0dd37-156">Başarılı olursa, bu yöntem boş bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="0dd37-156">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0dd37-157">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0dd37-157">Response success and error codes</span></span>

<span data-ttu-id="0dd37-158">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="0dd37-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0dd37-159">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0dd37-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0dd37-160">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0dd37-160">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0dd37-161">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0dd37-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
