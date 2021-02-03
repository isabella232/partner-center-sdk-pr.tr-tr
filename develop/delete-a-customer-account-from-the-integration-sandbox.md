---
title: Tümleştirme korumalı alandan bir müşteri hesabını silme
description: Üretim (tıp) tümleştirme korumalı alanındaki sınamadan bir müşteri hesabını silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: e3a1642c0202c174ddd4f65a6aeda2752def9176
ms.sourcegitcommit: b1ff781b67b1d322820bbcac2c583229201a8c07
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/29/2020
ms.locfileid: "97769424"
---
# <a name="delete-a-customer-account-from-the-integration-sandbox"></a><span data-ttu-id="0f5bb-103">Tümleştirme korumalı alandan bir müşteri hesabını silme</span><span class="sxs-lookup"><span data-stu-id="0f5bb-103">Delete a customer account from the integration sandbox</span></span>

<span data-ttu-id="0f5bb-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="0f5bb-104">**Applies to:**</span></span>

- <span data-ttu-id="0f5bb-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0f5bb-105">Partner Center</span></span>
- <span data-ttu-id="0f5bb-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0f5bb-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="0f5bb-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0f5bb-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="0f5bb-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0f5bb-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="0f5bb-109">Bu makalede, iş ortağı ile müşteri hesabı arasındaki ilişkiyi bölmek ve üretim (tıp) tümleştirme korumalı alanında test için kotayı geri kazanmak açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-109">This article explains, how to break the relationship between the partner and the customer account and regain the quota for Testing in Production (Tip) integration sandbox.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="0f5bb-110">Bir müşteri hesabını sildiğinizde, bu müşteri kiracısıyla ilişkili tüm kaynaklar temizlenir.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-110">When you delete a customer account, all resources associated with that customer tenant will be purged.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0f5bb-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0f5bb-111">Prerequisites</span></span>

- <span data-ttu-id="0f5bb-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0f5bb-113">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="0f5bb-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0f5bb-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0f5bb-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0f5bb-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0f5bb-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0f5bb-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0f5bb-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="0f5bb-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0f5bb-120">Bir müşteri, tıp tümleştirme korumalı alanından silinmeden önce tüm Azure ayrılmış sanal makine örneklerinin ve yazılım satın alma siparişlerinin iptal edilmesi gerekir.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-120">All Azure Reserved Virtual Machine Instances and software purchase orders must be cancelled before deleting a customer from the Tip integration sandbox.</span></span>

## <a name="c"></a><span data-ttu-id="0f5bb-121">C\#</span><span class="sxs-lookup"><span data-stu-id="0f5bb-121">C\#</span></span>

<span data-ttu-id="0f5bb-122">Bir müşteriyi tıp tümleştirme korumalı alanından silmek için:</span><span class="sxs-lookup"><span data-stu-id="0f5bb-122">To delete a customer from the Tip integration sandbox:</span></span>

1. <span data-ttu-id="0f5bb-123">İş ortağı işlemlerine bir [**ıpartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) arabirimi almak için tıp hesabı kimlik bilgilerinizi [**createpartneroperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-123">Pass your Tip account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to partner operations.</span></span>

2. <span data-ttu-id="0f5bb-124">Yetkilendirmeler koleksiyonunu almak için iş ortağı işlemler arabirimini kullanın:</span><span class="sxs-lookup"><span data-stu-id="0f5bb-124">Use the partner operations interface to retrieve the collection of entitlements:</span></span>

    1. <span data-ttu-id="0f5bb-125">Müşteriyi belirtmek için müşteri tanımlayıcısı ile [**Customers. byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-125">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer.</span></span>

    2. <span data-ttu-id="0f5bb-126">**Yetkilendirmeler** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-126">Call the **Entitlements** property.</span></span>

    3. <span data-ttu-id="0f5bb-127">[**Yetkilendirme**](entitlement-resources.md) koleksiyonunu almak için **Get** veya **GetAsync** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-127">Call the **Get** or **GetAsync** method to retrieve the [**Entitlement**](entitlement-resources.md) collection.</span></span>

3. <span data-ttu-id="0f5bb-128">Söz konusu müşteriye ait tüm Azure ayrılmış sanal makine örneklerinin ve yazılım satın alma siparişlerinin iptal edildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-128">Make sure that all Azure Reserved Virtual Machine Instances and software purchase orders for that customer are cancelled.</span></span> <span data-ttu-id="0f5bb-129">Koleksiyondaki her [**Yetkilendirme**](entitlement-resources.md) için:</span><span class="sxs-lookup"><span data-stu-id="0f5bb-129">For each [**Entitlement**](entitlement-resources.md) in the collection:</span></span>

    1. <span data-ttu-id="0f5bb-130">[**Yetkilendirme kullanın. ReferenceOrder.Id**](entitlement-resources.md#referenceorder) , müşterinin sipariş koleksiyonundan Ilgili [siparişin](order-resources.md#order) yerel bir kopyasını almak için.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-130">Use the [**entitlement.ReferenceOrder.Id**](entitlement-resources.md#referenceorder) to get a local copy of the corresponding [Order](order-resources.md#order) from the customer's collection of orders.</span></span>

    2. <span data-ttu-id="0f5bb-131">[**Order. Status**](order-resources.md#order) özelliğini "iptal edildi" olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-131">Set the [**Order.Status**](order-resources.md#order) property to "Cancelled".</span></span>

    3. <span data-ttu-id="0f5bb-132">Sıralamayı güncelleştirmek için **Patch ()** metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-132">Use the **Patch()** method to update the order.</span></span>

4. <span data-ttu-id="0f5bb-133">Tüm siparişleri iptal et.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-133">Cancel all orders.</span></span> <span data-ttu-id="0f5bb-134">Örneğin, aşağıdaki kod örneği, durumu "Iptal edildi" olana kadar her sırayı yoklamak için bir döngü kullanır.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-134">For example, the following code sample uses a loop to poll each order until its status is "Cancelled".</span></span>

    ``` csharp
    // IPartnerCredentials tipAccountCredentials;
    // Customer tenant Id to be deleted.
    // string customerTenantId;

    IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

    // Get all entitlements whose order must be cancelled.
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
        // Check if all the orders were cancelled.
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

5. <span data-ttu-id="0f5bb-135">Müşterinin **silme** yöntemini çağırarak tüm siparişlerin iptal edildiğinden emin olun.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-135">Make sure all orders are cancelled by calling the **Delete** method for the customer.</span></span>

<span data-ttu-id="0f5bb-136">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0f5bb-136">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0f5bb-137">**Proje**: Iş ortağı Center PartnerCenterSDK. FeaturesSamples **sınıfı**: DeleteCustomerFromTipAccount.cs</span><span class="sxs-lookup"><span data-stu-id="0f5bb-137">**Project**: Partner Center PartnerCenterSDK.FeaturesSamples **Class**: DeleteCustomerFromTipAccount.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0f5bb-138">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0f5bb-138">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0f5bb-139">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0f5bb-139">Request syntax</span></span>

| <span data-ttu-id="0f5bb-140">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0f5bb-140">Method</span></span>     | <span data-ttu-id="0f5bb-141">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0f5bb-141">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="0f5bb-142">DELETE</span><span class="sxs-lookup"><span data-stu-id="0f5bb-142">DELETE</span></span>     | <span data-ttu-id="0f5bb-143">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="0f5bb-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="0f5bb-144">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="0f5bb-144">URI parameter</span></span>

<span data-ttu-id="0f5bb-145">Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-145">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="0f5bb-146">Ad</span><span class="sxs-lookup"><span data-stu-id="0f5bb-146">Name</span></span>                   | <span data-ttu-id="0f5bb-147">Tür</span><span class="sxs-lookup"><span data-stu-id="0f5bb-147">Type</span></span>     | <span data-ttu-id="0f5bb-148">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0f5bb-148">Required</span></span> | <span data-ttu-id="0f5bb-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0f5bb-149">Description</span></span>                                                                         |
|------------------------|----------|----------|-------------------------------------------------------------------------------------|
| <span data-ttu-id="0f5bb-150">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="0f5bb-150">customer-tenant-id</span></span>     | <span data-ttu-id="0f5bb-151">GUID</span><span class="sxs-lookup"><span data-stu-id="0f5bb-151">GUID</span></span>     | <span data-ttu-id="0f5bb-152">Y</span><span class="sxs-lookup"><span data-stu-id="0f5bb-152">Y</span></span>        | <span data-ttu-id="0f5bb-153">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-153">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0f5bb-154">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0f5bb-154">Request headers</span></span>

<span data-ttu-id="0f5bb-155">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0f5bb-155">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0f5bb-156">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0f5bb-156">Request body</span></span>

<span data-ttu-id="0f5bb-157">Yok.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-157">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="0f5bb-158">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0f5bb-158">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="0f5bb-159">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0f5bb-159">REST response</span></span>

<span data-ttu-id="0f5bb-160">Başarılı olursa, bu yöntem boş bir yanıt döndürür.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-160">If successful, this method returns an empty response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0f5bb-161">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0f5bb-161">Response success and error codes</span></span>

<span data-ttu-id="0f5bb-162">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-162">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0f5bb-163">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0f5bb-163">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0f5bb-164">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0f5bb-164">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0f5bb-165">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0f5bb-165">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
Date: Wed, 16 Mar 2016 00:43:02 GMT
```
