---
title: Sepeti güncelleştirme
description: Sepette müşteri için sipariş güncelleştirme.
ms.date: 10/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8954d4dad39f9b1a1b9a2f213e0231f01856fcd2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446692"
---
# <a name="update-a-cart"></a><span data-ttu-id="89da3-103">Sepeti güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="89da3-103">Update a cart</span></span>

<span data-ttu-id="89da3-104">Sepette müşteri için sipariş güncelleştirme.</span><span class="sxs-lookup"><span data-stu-id="89da3-104">How to update an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="89da3-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="89da3-105">Prerequisites</span></span>

- <span data-ttu-id="89da3-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="89da3-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="89da3-107">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="89da3-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="89da3-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="89da3-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="89da3-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="89da3-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="89da3-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="89da3-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="89da3-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="89da3-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="89da3-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="89da3-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="89da3-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="89da3-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="89da3-114">Mevcut sepet için sepet kimliği.</span><span class="sxs-lookup"><span data-stu-id="89da3-114">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="89da3-115">C\#</span><span class="sxs-lookup"><span data-stu-id="89da3-115">C\#</span></span>

<span data-ttu-id="89da3-116">Müşterinin siparişlerini güncelleştirmek **için, ById()** işlevini kullanarak müşteri ve sepet kimliklerini ileterek Get() yöntemini kullanarak **sepete** sahip olun.</span><span class="sxs-lookup"><span data-stu-id="89da3-116">To update an order for a customer, get the cart using the **Get()** method by passing the customer and cart IDs using the **ById()** function.</span></span> <span data-ttu-id="89da3-117">Sepette gerekli değişiklikleri yapın.</span><span class="sxs-lookup"><span data-stu-id="89da3-117">Make the necessary changes to the cart.</span></span> <span data-ttu-id="89da3-118">Şimdi **ById()** yöntemini kullanarak müşteri ve sepet kimliklerini kullanarak **Put** yöntemini çağır.</span><span class="sxs-lookup"><span data-stu-id="89da3-118">Now call the **Put** method by using customer and cart IDs using the **ById()** method.</span></span>

<span data-ttu-id="89da3-119">Son olarak, **siparişi oluşturmak için Put()** veya **PutAsync()** yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="89da3-119">Finally, call the **Put()** or **PutAsync()** method to create the order.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Get();

cart.LineItems.ToArray()[0].Quantity++;

var updatedCart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Put(cart);
```

## <a name="rest-request"></a><span data-ttu-id="89da3-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="89da3-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="89da3-121">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="89da3-121">Request syntax</span></span>

| <span data-ttu-id="89da3-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="89da3-122">Method</span></span>  | <span data-ttu-id="89da3-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="89da3-123">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89da3-124">**PUT**</span><span class="sxs-lookup"><span data-stu-id="89da3-124">**PUT**</span></span> | <span data-ttu-id="89da3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="89da3-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id} HTTP/1.1</span></span>              |

### <a name="uri-parameters"></a><span data-ttu-id="89da3-126">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="89da3-126">URI parameters</span></span>

<span data-ttu-id="89da3-127">Müşteriyi tanımlamak ve güncelleştirilacak sepeti belirtmek için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="89da3-127">Use the following path parameters to identify the customer, and specify the cart to be updated.</span></span>

| <span data-ttu-id="89da3-128">Ad</span><span class="sxs-lookup"><span data-stu-id="89da3-128">Name</span></span>            | <span data-ttu-id="89da3-129">Tür</span><span class="sxs-lookup"><span data-stu-id="89da3-129">Type</span></span>     | <span data-ttu-id="89da3-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="89da3-130">Required</span></span> | <span data-ttu-id="89da3-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89da3-131">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="89da3-132">**customer-id**</span><span class="sxs-lookup"><span data-stu-id="89da3-132">**customer-id**</span></span> | <span data-ttu-id="89da3-133">string</span><span class="sxs-lookup"><span data-stu-id="89da3-133">string</span></span>   | <span data-ttu-id="89da3-134">Yes</span><span class="sxs-lookup"><span data-stu-id="89da3-134">Yes</span></span>      | <span data-ttu-id="89da3-135">Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id.</span><span class="sxs-lookup"><span data-stu-id="89da3-135">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="89da3-136">**cart-id**</span><span class="sxs-lookup"><span data-stu-id="89da3-136">**cart-id**</span></span>     | <span data-ttu-id="89da3-137">string</span><span class="sxs-lookup"><span data-stu-id="89da3-137">string</span></span>   | <span data-ttu-id="89da3-138">Yes</span><span class="sxs-lookup"><span data-stu-id="89da3-138">Yes</span></span>      | <span data-ttu-id="89da3-139">Sepeti tanımlayan GUID biçimli sepet kimliği.</span><span class="sxs-lookup"><span data-stu-id="89da3-139">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="89da3-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="89da3-140">Request headers</span></span>

<span data-ttu-id="89da3-141">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="89da3-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="89da3-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="89da3-142">Request body</span></span>

<span data-ttu-id="89da3-143">Bu tablo, istek [gövdesinin](cart-resources.md) Sepet özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="89da3-143">This table describes the [Cart](cart-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="89da3-144">Özellik</span><span class="sxs-lookup"><span data-stu-id="89da3-144">Property</span></span>              | <span data-ttu-id="89da3-145">Tür</span><span class="sxs-lookup"><span data-stu-id="89da3-145">Type</span></span>             | <span data-ttu-id="89da3-146">Gerekli</span><span class="sxs-lookup"><span data-stu-id="89da3-146">Required</span></span>        | <span data-ttu-id="89da3-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89da3-147">Description</span></span>                                                                                               |
|-----------------------|------------------|-----------------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89da3-148">kimlik</span><span class="sxs-lookup"><span data-stu-id="89da3-148">id</span></span>                    | <span data-ttu-id="89da3-149">dize</span><span class="sxs-lookup"><span data-stu-id="89da3-149">string</span></span>           | <span data-ttu-id="89da3-150">No</span><span class="sxs-lookup"><span data-stu-id="89da3-150">No</span></span>              | <span data-ttu-id="89da3-151">Sepetin başarıyla oluşturulmasının ardından sağlanan bir sepet tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="89da3-151">A cart identifier that is supplied upon successful creation of the cart.</span></span>                                  |
| <span data-ttu-id="89da3-152">creationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="89da3-152">creationTimeStamp</span></span>     | <span data-ttu-id="89da3-153">DateTime</span><span class="sxs-lookup"><span data-stu-id="89da3-153">DateTime</span></span>         | <span data-ttu-id="89da3-154">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da3-154">No</span></span>              | <span data-ttu-id="89da3-155">Sepetin tarih-saat biçiminde oluşturulma tarihi.</span><span class="sxs-lookup"><span data-stu-id="89da3-155">The date the cart was created, in date-time format.</span></span> <span data-ttu-id="89da3-156">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="89da3-156">Applied upon successful creation of the cart.</span></span>        |
| <span data-ttu-id="89da3-157">lastModifiedTimeStamp</span><span class="sxs-lookup"><span data-stu-id="89da3-157">lastModifiedTimeStamp</span></span> | <span data-ttu-id="89da3-158">DateTime</span><span class="sxs-lookup"><span data-stu-id="89da3-158">DateTime</span></span>         | <span data-ttu-id="89da3-159">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da3-159">No</span></span>              | <span data-ttu-id="89da3-160">Sepetin en son güncelleştirilen tarih-saat biçiminde olduğu tarih.</span><span class="sxs-lookup"><span data-stu-id="89da3-160">The date the cart was last updated, in date-time format.</span></span> <span data-ttu-id="89da3-161">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="89da3-161">Applied upon successful creation of the cart.</span></span>    |
| <span data-ttu-id="89da3-162">expirationTimeStamp</span><span class="sxs-lookup"><span data-stu-id="89da3-162">expirationTimeStamp</span></span>   | <span data-ttu-id="89da3-163">DateTime</span><span class="sxs-lookup"><span data-stu-id="89da3-163">DateTime</span></span>         | <span data-ttu-id="89da3-164">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da3-164">No</span></span>              | <span data-ttu-id="89da3-165">Sepet tarih-saat biçiminde sona erer.</span><span class="sxs-lookup"><span data-stu-id="89da3-165">The date the cart will expire, in date-time format.</span></span>  <span data-ttu-id="89da3-166">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="89da3-166">Applied upon successful creation of cart.</span></span>            |
| <span data-ttu-id="89da3-167">lastModifiedUser</span><span class="sxs-lookup"><span data-stu-id="89da3-167">lastModifiedUser</span></span>      | <span data-ttu-id="89da3-168">dize</span><span class="sxs-lookup"><span data-stu-id="89da3-168">string</span></span>           | <span data-ttu-id="89da3-169">No</span><span class="sxs-lookup"><span data-stu-id="89da3-169">No</span></span>              | <span data-ttu-id="89da3-170">Sepeti en son güncelleştirilen kullanıcı.</span><span class="sxs-lookup"><span data-stu-id="89da3-170">The user who last updated the cart.</span></span> <span data-ttu-id="89da3-171">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="89da3-171">Applied upon successful creation of cart.</span></span>                             |
| <span data-ttu-id="89da3-172">lineItems</span><span class="sxs-lookup"><span data-stu-id="89da3-172">lineItems</span></span>             | <span data-ttu-id="89da3-173">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="89da3-173">Array of objects</span></span> | <span data-ttu-id="89da3-174">Yes</span><span class="sxs-lookup"><span data-stu-id="89da3-174">Yes</span></span>             | <span data-ttu-id="89da3-175">[Bir CartLineItem kaynakları](cart-resources.md#cartlineitem) dizisi.</span><span class="sxs-lookup"><span data-stu-id="89da3-175">An Array of [CartLineItem](cart-resources.md#cartlineitem) resources.</span></span>                                               |

<span data-ttu-id="89da3-176">Bu tablo, istek [gövdesinin CartLineItem](cart-resources.md#cartlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="89da3-176">This table describes the [CartLineItem](cart-resources.md#cartlineitem) properties in the request body.</span></span>

| <span data-ttu-id="89da3-177">Özellik</span><span class="sxs-lookup"><span data-stu-id="89da3-177">Property</span></span>             | <span data-ttu-id="89da3-178">Tür</span><span class="sxs-lookup"><span data-stu-id="89da3-178">Type</span></span>                        | <span data-ttu-id="89da3-179">Gerekli</span><span class="sxs-lookup"><span data-stu-id="89da3-179">Required</span></span>     | <span data-ttu-id="89da3-180">Açıklama</span><span class="sxs-lookup"><span data-stu-id="89da3-180">Description</span></span>                                                                                        |
|----------------------|-----------------------------|--------------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="89da3-181">kimlik</span><span class="sxs-lookup"><span data-stu-id="89da3-181">id</span></span>                   | <span data-ttu-id="89da3-182">dize</span><span class="sxs-lookup"><span data-stu-id="89da3-182">string</span></span>                      | <span data-ttu-id="89da3-183">No</span><span class="sxs-lookup"><span data-stu-id="89da3-183">No</span></span>           | <span data-ttu-id="89da3-184">Sepet satır öğesi için benzersiz tanımlayıcı.</span><span class="sxs-lookup"><span data-stu-id="89da3-184">A Unique identifier for a cart line item.</span></span> <span data-ttu-id="89da3-185">Sepetin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="89da3-185">Applied upon successful creation of cart.</span></span>                |
| <span data-ttu-id="89da3-186">catalogId</span><span class="sxs-lookup"><span data-stu-id="89da3-186">catalogId</span></span>            | <span data-ttu-id="89da3-187">string</span><span class="sxs-lookup"><span data-stu-id="89da3-187">string</span></span>                      | <span data-ttu-id="89da3-188">Yes</span><span class="sxs-lookup"><span data-stu-id="89da3-188">Yes</span></span>          | <span data-ttu-id="89da3-189">Katalog öğesi tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="89da3-189">The catalog item identifier.</span></span>                                                                       |
| <span data-ttu-id="89da3-190">Friendlyname</span><span class="sxs-lookup"><span data-stu-id="89da3-190">friendlyName</span></span>         | <span data-ttu-id="89da3-191">dize</span><span class="sxs-lookup"><span data-stu-id="89da3-191">string</span></span>                      | <span data-ttu-id="89da3-192">No</span><span class="sxs-lookup"><span data-stu-id="89da3-192">No</span></span>           | <span data-ttu-id="89da3-193">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="89da3-193">Optional.</span></span> <span data-ttu-id="89da3-194">Karartmanıza yardımcı olmak için iş ortağı tarafından tanımlanan öğenin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="89da3-194">The friendly name for the item defined by the partner to help disambiguate.</span></span>              |
| <span data-ttu-id="89da3-195">miktar</span><span class="sxs-lookup"><span data-stu-id="89da3-195">quantity</span></span>             | <span data-ttu-id="89da3-196">int</span><span class="sxs-lookup"><span data-stu-id="89da3-196">int</span></span>                         | <span data-ttu-id="89da3-197">Yes</span><span class="sxs-lookup"><span data-stu-id="89da3-197">Yes</span></span>          | <span data-ttu-id="89da3-198">Lisans veya örnek sayısı.</span><span class="sxs-lookup"><span data-stu-id="89da3-198">The number of licenses or instances.</span></span>     |
| <span data-ttu-id="89da3-199">currencyCode</span><span class="sxs-lookup"><span data-stu-id="89da3-199">currencyCode</span></span>         | <span data-ttu-id="89da3-200">dize</span><span class="sxs-lookup"><span data-stu-id="89da3-200">string</span></span>                      | <span data-ttu-id="89da3-201">No</span><span class="sxs-lookup"><span data-stu-id="89da3-201">No</span></span>           | <span data-ttu-id="89da3-202">Para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="89da3-202">The currency code.</span></span>                                                                                 |
| <span data-ttu-id="89da3-203">billingCycle</span><span class="sxs-lookup"><span data-stu-id="89da3-203">billingCycle</span></span>         | <span data-ttu-id="89da3-204">Nesne</span><span class="sxs-lookup"><span data-stu-id="89da3-204">Object</span></span>                      | <span data-ttu-id="89da3-205">Yes</span><span class="sxs-lookup"><span data-stu-id="89da3-205">Yes</span></span>          | <span data-ttu-id="89da3-206">Geçerli dönem için ayarlanmış faturalama dönemi türü.</span><span class="sxs-lookup"><span data-stu-id="89da3-206">The type of billing cycle set for the current period.</span></span>                                              |
| <span data-ttu-id="89da3-207">Katılımcılar</span><span class="sxs-lookup"><span data-stu-id="89da3-207">participants</span></span>         | <span data-ttu-id="89da3-208">Nesne Dizesi çiftlerinin listesi</span><span class="sxs-lookup"><span data-stu-id="89da3-208">List of Object String pairs</span></span> | <span data-ttu-id="89da3-209">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da3-209">No</span></span>           | <span data-ttu-id="89da3-210">Satın alma ile ilgili katılımcılardan bir koleksiyon.</span><span class="sxs-lookup"><span data-stu-id="89da3-210">A collection of participants on the purchase.</span></span>                                                      |
| <span data-ttu-id="89da3-211">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="89da3-211">provisioningContext</span></span>  | <span data-ttu-id="89da3-212">Sözlük<dizesi, dize></span><span class="sxs-lookup"><span data-stu-id="89da3-212">Dictionary<string, string></span></span>  | <span data-ttu-id="89da3-213">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da3-213">No</span></span>           | <span data-ttu-id="89da3-214">Teklifin sağlanması için kullanılan bağlam.</span><span class="sxs-lookup"><span data-stu-id="89da3-214">A context used for provisioning of offer.</span></span>                                                          |
| <span data-ttu-id="89da3-215">orderGroup</span><span class="sxs-lookup"><span data-stu-id="89da3-215">orderGroup</span></span>           | <span data-ttu-id="89da3-216">dize</span><span class="sxs-lookup"><span data-stu-id="89da3-216">string</span></span>                      | <span data-ttu-id="89da3-217">No</span><span class="sxs-lookup"><span data-stu-id="89da3-217">No</span></span>           | <span data-ttu-id="89da3-218">Hangi öğelerin bir araya yerleştiril olduğunu belirten bir grup.</span><span class="sxs-lookup"><span data-stu-id="89da3-218">A group to indicate which items can be placed together.</span></span>                                            |
| <span data-ttu-id="89da3-219">error</span><span class="sxs-lookup"><span data-stu-id="89da3-219">error</span></span>                | <span data-ttu-id="89da3-220">Nesne</span><span class="sxs-lookup"><span data-stu-id="89da3-220">Object</span></span>                      | <span data-ttu-id="89da3-221">Hayır</span><span class="sxs-lookup"><span data-stu-id="89da3-221">No</span></span>           | <span data-ttu-id="89da3-222">Bir hata durumunda sepet oluşturulduktan sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="89da3-222">Applied after cart is created in case of an error.</span></span>                                                 |

### <a name="request-example"></a><span data-ttu-id="89da3-223">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="89da3-223">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="89da3-224">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="89da3-224">REST response</span></span>

<span data-ttu-id="89da3-225">Başarılı olursa, bu yöntem yanıt [gövdesinde](cart-resources.md) doldurulmuş Sepet kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="89da3-225">If successful, this method returns the populated [Cart](cart-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="89da3-226">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="89da3-226">Response success and error codes</span></span>

<span data-ttu-id="89da3-227">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="89da3-227">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="89da3-228">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="89da3-228">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="89da3-229">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="89da3-229">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="89da3-230">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="89da3-230">Response example</span></span>

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
