---
title: Sepeti güncelleştirme
description: Bir sepetteki müşteri için bir siparişi güncelleştirme.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 7c0806ccc87281b9b34005f22cd8d6ad57fb5de5
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768939"
---
# <a name="update-a-cart"></a><span data-ttu-id="9b2ba-103">Sepeti güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="9b2ba-103">Update a cart</span></span>

<span data-ttu-id="9b2ba-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="9b2ba-104">**Applies To**</span></span>

- <span data-ttu-id="9b2ba-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9b2ba-105">Partner Center</span></span>

<span data-ttu-id="9b2ba-106">Bir sepetteki müşteri için bir siparişi güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-106">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9b2ba-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9b2ba-107">Prerequisites</span></span>

- <span data-ttu-id="9b2ba-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9b2ba-109">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="9b2ba-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9b2ba-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9b2ba-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9b2ba-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9b2ba-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9b2ba-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9b2ba-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="9b2ba-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="9b2ba-116">Mevcut bir sepet için sepet KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-116">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="9b2ba-117">C\#</span><span class="sxs-lookup"><span data-stu-id="9b2ba-117">C\#</span></span>

<span data-ttu-id="9b2ba-118">Müşterinin bir siparişini güncelleştirmek için, **Byıd ()** işlevini kullanarak müşteriyi ve sepet kimliğini geçirerek **Get ()** yöntemini kullanarak sepetini alın.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-118">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart ID's using the **ById()** function.</span></span> <span data-ttu-id="9b2ba-119">Sepette gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-119">Make the necessary changes to the cart.</span></span> <span data-ttu-id="9b2ba-120">Şimdi, **Byıd ()** yöntemini kullanarak Customer ve sepet kimliği ' ni kullanarak **PUT** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-120">Now call the **Put** method by using customer and cart ID's using the **ById()** method.</span></span>

<span data-ttu-id="9b2ba-121">Son olarak, siparişi oluşturmak için **PUT ()** veya **PutAsync ()** metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-121">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="9b2ba-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9b2ba-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9b2ba-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9b2ba-123">Request syntax</span></span>

| <span data-ttu-id="9b2ba-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9b2ba-124">Method</span></span>  | <span data-ttu-id="9b2ba-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9b2ba-125">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9b2ba-126">**PUT**</span><span class="sxs-lookup"><span data-stu-id="9b2ba-126">**PUT**</span></span> | <span data-ttu-id="9b2ba-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts/{cart-id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="9b2ba-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="9b2ba-128">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="9b2ba-128">URI parameters</span></span>

<span data-ttu-id="9b2ba-129">Müşteriyi tanımlamak için aşağıdaki yol parametrelerini kullanın ve güncelleştirileceğini seçin.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-129">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="9b2ba-130">Ad</span><span class="sxs-lookup"><span data-stu-id="9b2ba-130">Name</span></span>            | <span data-ttu-id="9b2ba-131">Tür</span><span class="sxs-lookup"><span data-stu-id="9b2ba-131">Type</span></span>     | <span data-ttu-id="9b2ba-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9b2ba-132">Required</span></span> | <span data-ttu-id="9b2ba-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9b2ba-133">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="9b2ba-134">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="9b2ba-134">**customer-id**</span></span> | <span data-ttu-id="9b2ba-135">string</span><span class="sxs-lookup"><span data-stu-id="9b2ba-135">string</span></span>   | <span data-ttu-id="9b2ba-136">Yes</span><span class="sxs-lookup"><span data-stu-id="9b2ba-136">Yes</span></span>      | <span data-ttu-id="9b2ba-137">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-137">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="9b2ba-138">**sepet kimliği**</span><span class="sxs-lookup"><span data-stu-id="9b2ba-138">**cart-id**</span></span>     | <span data-ttu-id="9b2ba-139">string</span><span class="sxs-lookup"><span data-stu-id="9b2ba-139">string</span></span>   | <span data-ttu-id="9b2ba-140">Yes</span><span class="sxs-lookup"><span data-stu-id="9b2ba-140">Yes</span></span>      | <span data-ttu-id="9b2ba-141">Sepeti tanımlayan bir GUID biçimli sepet kimliği.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-141">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="9b2ba-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9b2ba-142">Request headers</span></span>

<span data-ttu-id="9b2ba-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9b2ba-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9b2ba-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9b2ba-144">Request body</span></span>

<span data-ttu-id="9b2ba-145">Bu tablo, istek gövdesinde [sepet](cart-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-145">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="9b2ba-146">Özellik</span><span class="sxs-lookup"><span data-stu-id="9b2ba-146">Property</span></span>              | <span data-ttu-id="9b2ba-147">Tür</span><span class="sxs-lookup"><span data-stu-id="9b2ba-147">Type</span></span>             | <span data-ttu-id="9b2ba-148">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9b2ba-148">Required</span></span>        | <span data-ttu-id="9b2ba-149">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9b2ba-149">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9b2ba-150">kimlik</span><span class="sxs-lookup"><span data-stu-id="9b2ba-150">id</span></span>                    | <span data-ttu-id="9b2ba-151">dize</span><span class="sxs-lookup"><span data-stu-id="9b2ba-151">string</span></span>           | <span data-ttu-id="9b2ba-152">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-152">No</span></span>              | <span data-ttu-id="9b2ba-153">Sepet başarıyla oluşturulduktan sonra sağlanan bir sepet tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-153">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="9b2ba-154">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="9b2ba-154">creationTimeStamp</span></span>     | <span data-ttu-id="9b2ba-155">DateTime</span><span class="sxs-lookup"><span data-stu-id="9b2ba-155">DateTime</span></span>         | <span data-ttu-id="9b2ba-156">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-156">No</span></span>              | <span data-ttu-id="9b2ba-157">Sepetin oluşturulduğu tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-157">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="9b2ba-158">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-158">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="9b2ba-159">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="9b2ba-159">lastModifiedTimeStamp</span></span> | <span data-ttu-id="9b2ba-160">DateTime</span><span class="sxs-lookup"><span data-stu-id="9b2ba-160">DateTime</span></span>         | <span data-ttu-id="9b2ba-161">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-161">No</span></span>              | <span data-ttu-id="9b2ba-162">Sepetin son güncelleştirildiği tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-162">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="9b2ba-163">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-163">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="9b2ba-164">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="9b2ba-164">expirationTimeStamp</span></span>   | <span data-ttu-id="9b2ba-165">DateTime</span><span class="sxs-lookup"><span data-stu-id="9b2ba-165">DateTime</span></span>         | <span data-ttu-id="9b2ba-166">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-166">No</span></span>              | <span data-ttu-id="9b2ba-167">Sepetin süresinin dolacağı tarih-saat biçiminde.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-167">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="9b2ba-168">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-168">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="9b2ba-169">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="9b2ba-169">lastModifiedUser</span></span>      | <span data-ttu-id="9b2ba-170">dize</span><span class="sxs-lookup"><span data-stu-id="9b2ba-170">string</span></span>           | <span data-ttu-id="9b2ba-171">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-171">No</span></span>              | <span data-ttu-id="9b2ba-172">Sepetini son güncelleştiren Kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-172">The user who last updated the cart.</span></span> <span data-ttu-id="9b2ba-173">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-173">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="9b2ba-174">LineItems</span><span class="sxs-lookup"><span data-stu-id="9b2ba-174">lineItems</span></span>             | <span data-ttu-id="9b2ba-175">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="9b2ba-175">Array of objects</span></span> | <span data-ttu-id="9b2ba-176">Yes</span><span class="sxs-lookup"><span data-stu-id="9b2ba-176">Yes</span></span>             | <span data-ttu-id="9b2ba-177">Bir [Cartlineıtem](cart-resources.md#cartlineitem) kaynakları dizisi.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-177">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="9b2ba-178">Bu tablo, istek gövdesinde [Cartlineıtem](cart-resources.md#cartlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-178">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="9b2ba-179">Özellik</span><span class="sxs-lookup"><span data-stu-id="9b2ba-179">Property</span></span>             | <span data-ttu-id="9b2ba-180">Tür</span><span class="sxs-lookup"><span data-stu-id="9b2ba-180">Type</span></span>                        | <span data-ttu-id="9b2ba-181">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9b2ba-181">Required</span></span>     | <span data-ttu-id="9b2ba-182">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9b2ba-182">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="9b2ba-183">kimlik</span><span class="sxs-lookup"><span data-stu-id="9b2ba-183">id</span></span>                   | <span data-ttu-id="9b2ba-184">dize</span><span class="sxs-lookup"><span data-stu-id="9b2ba-184">string</span></span>                      | <span data-ttu-id="9b2ba-185">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-185">No</span></span>           | <span data-ttu-id="9b2ba-186">Sepet çizgisi öğesi için benzersiz bir tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-186">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="9b2ba-187">Sepet başarıyla oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-187">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="9b2ba-188">catalogId</span><span class="sxs-lookup"><span data-stu-id="9b2ba-188">catalogId</span></span>            | <span data-ttu-id="9b2ba-189">string</span><span class="sxs-lookup"><span data-stu-id="9b2ba-189">string</span></span>                      | <span data-ttu-id="9b2ba-190">Yes</span><span class="sxs-lookup"><span data-stu-id="9b2ba-190">Yes</span></span>          | <span data-ttu-id="9b2ba-191">Katalog öğesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-191">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="9b2ba-192">friendlyName</span><span class="sxs-lookup"><span data-stu-id="9b2ba-192">friendlyName</span></span>         | <span data-ttu-id="9b2ba-193">dize</span><span class="sxs-lookup"><span data-stu-id="9b2ba-193">string</span></span>                      | <span data-ttu-id="9b2ba-194">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-194">No</span></span>           | <span data-ttu-id="9b2ba-195">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-195">Optional.</span></span> <span data-ttu-id="9b2ba-196">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-196">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="9b2ba-197">miktar</span><span class="sxs-lookup"><span data-stu-id="9b2ba-197">quantity</span></span>             | <span data-ttu-id="9b2ba-198">int</span><span class="sxs-lookup"><span data-stu-id="9b2ba-198">int</span></span>                         | <span data-ttu-id="9b2ba-199">Yes</span><span class="sxs-lookup"><span data-stu-id="9b2ba-199">Yes</span></span>          | <span data-ttu-id="9b2ba-200">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-200">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="9b2ba-201">currencyCode</span><span class="sxs-lookup"><span data-stu-id="9b2ba-201">currencyCode</span></span>         | <span data-ttu-id="9b2ba-202">dize</span><span class="sxs-lookup"><span data-stu-id="9b2ba-202">string</span></span>                      | <span data-ttu-id="9b2ba-203">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-203">No</span></span>           | <span data-ttu-id="9b2ba-204">Para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-204">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="9b2ba-205">Bilimlingcycle</span><span class="sxs-lookup"><span data-stu-id="9b2ba-205">billingCycle</span></span>         | <span data-ttu-id="9b2ba-206">Nesne</span><span class="sxs-lookup"><span data-stu-id="9b2ba-206">Object</span></span>                      | <span data-ttu-id="9b2ba-207">Yes</span><span class="sxs-lookup"><span data-stu-id="9b2ba-207">Yes</span></span>          | <span data-ttu-id="9b2ba-208">Geçerli dönem için ayarlanan faturalandırma dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-208">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="9b2ba-209">Katılımcılar</span><span class="sxs-lookup"><span data-stu-id="9b2ba-209">participants</span></span>         | <span data-ttu-id="9b2ba-210">Nesne dizesi çiftlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="9b2ba-210">List of Object String pairs</span></span> | <span data-ttu-id="9b2ba-211">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-211">No</span></span>           | <span data-ttu-id="9b2ba-212">Satın alımdaki katılımcılar koleksiyonu.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-212">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="9b2ba-213">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="9b2ba-213">provisioningContext</span></span>  | <span data-ttu-id="9b2ba-214">Sözlük<dize, dize></span><span class="sxs-lookup"><span data-stu-id="9b2ba-214">Dictionary<string, string></span></span>  | <span data-ttu-id="9b2ba-215">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-215">No</span></span>           | <span data-ttu-id="9b2ba-216">Teklifin sağlanması için kullanılan bir bağlam.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-216">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="9b2ba-217">orderGroup</span><span class="sxs-lookup"><span data-stu-id="9b2ba-217">orderGroup</span></span>           | <span data-ttu-id="9b2ba-218">dize</span><span class="sxs-lookup"><span data-stu-id="9b2ba-218">string</span></span>                      | <span data-ttu-id="9b2ba-219">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-219">No</span></span>           | <span data-ttu-id="9b2ba-220">Hangi öğelerin birlikte yerleştirilebileceğini belirten bir grup.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-220">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="9b2ba-221">error</span><span class="sxs-lookup"><span data-stu-id="9b2ba-221">error</span></span>                | <span data-ttu-id="9b2ba-222">Nesne</span><span class="sxs-lookup"><span data-stu-id="9b2ba-222">Object</span></span>                      | <span data-ttu-id="9b2ba-223">No</span><span class="sxs-lookup"><span data-stu-id="9b2ba-223">No</span></span>           | <span data-ttu-id="9b2ba-224">Bir hata durumunda sepet oluşturulduktan sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-224">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="9b2ba-225">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9b2ba-225">Request example</span></span>

```http
PUT /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/65faf57b-0205-47ee-92b3-08dcf233ea73/ HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 496
Expect: 100-continue

{
    {
        "Id":"b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
        "CreationTimestamp":"2018-03-15T17:15:02.3840528Z",
        "LastModifiedTimestamp":"2018-03-15T17:15:02.3840528Z",
        "ExpirationTimestamp":"0001-01-01T00:00:00",
        "LastModifiedUser":"2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
        "LineItems":[
            {
                "Id":0,
                "CatalogItemId":"DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
                "FriendlyName":"A_sample_Azure_RI",
                "Quantity":2,
                "BillingCycle":"one_time",
                "ProvisioningContext": {
                    "SubscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                    "Scope": "shared",
                    "Duration": "1Year"
                }
            }
        ],
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="9b2ba-226">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9b2ba-226">REST response</span></span>

<span data-ttu-id="9b2ba-227">Başarılı olursa, bu yöntem yanıt gövdesinde doldurulmuş [sepet](cart-resources.md) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-227">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9b2ba-228">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9b2ba-228">Response success and error codes</span></span>

<span data-ttu-id="9b2ba-229">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-229">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9b2ba-230">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9b2ba-230">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9b2ba-231">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9b2ba-231">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9b2ba-232">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9b2ba-232">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
{
    "id": "b4c8fdea-cbe4-4d17-9576-13fcacbf9605",
    "creationTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedTimestamp": "2018-03-15T17:15:02.3840528Z",
    "lastModifiedUser": "2713ccd7-ea3b-470a-9cfb-451d5d0482cc",
    "lineItems": [
        {
            "id": 0,
            "catalogItemId": "DG7GMGF0DWTL:0001:DG7GMGF0DSJB",
            "friendlyName": "A_sample_Azure_RI",
            "quantity": 2,
            "currencyCode": "USD",
            "billingCycle": "one_time",
            "ProvisioningContext": {
                "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
                "scope": "shared",
                "duration": "1Year"
            }
            "orderGroup": "0"
        }
    ],
    "links": {
        "self": {
            "uri": "/v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Cart"
    }
}
```
