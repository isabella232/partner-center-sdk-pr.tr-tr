---
title: Müşteri siparişi oluşturma
description: Müşteri için sipariş oluşturmak üzere Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: ce176909a1f9c350f1c16615171de57a7beb888d
ms.sourcegitcommit: 4c253abb24140a6e00b0aea8e79a08823ea5a623
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/07/2020
ms.locfileid: "97770126"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="2e23f-104">Iş Ortağı Merkezi API 'Lerini kullanarak bir müşteri için sipariş oluşturma</span><span class="sxs-lookup"><span data-stu-id="2e23f-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="2e23f-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="2e23f-105">**Applies to:**</span></span>

- <span data-ttu-id="2e23f-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2e23f-106">Partner Center</span></span>
- <span data-ttu-id="2e23f-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2e23f-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2e23f-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2e23f-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2e23f-109">**Azure ayrılmış VM örneği ürünlerinin bir sırası** oluşturmak için *yalnızca* şu şekilde geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="2e23f-109">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="2e23f-110">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2e23f-110">Partner Center</span></span>

<span data-ttu-id="2e23f-111">Şu anda satmaya sunulan bilgiler hakkında daha fazla bilgi için bkz. [bulut çözümü sağlayıcısı programındaki Iş ortağı teklifleri](/partner-center/csp-offers).</span><span class="sxs-lookup"><span data-stu-id="2e23f-111">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e23f-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2e23f-112">Prerequisites</span></span>

- <span data-ttu-id="2e23f-113">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2e23f-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2e23f-114">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2e23f-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="2e23f-115">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="2e23f-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="2e23f-116">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="2e23f-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="2e23f-117">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="2e23f-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="2e23f-118">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="2e23f-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="2e23f-119">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="2e23f-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="2e23f-120">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="2e23f-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="2e23f-121">Bir teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-121">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="2e23f-122">C\#</span><span class="sxs-lookup"><span data-stu-id="2e23f-122">C\#</span></span>

<span data-ttu-id="2e23f-123">Bir müşteri için sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="2e23f-123">To create an order for a customer:</span></span>

1. <span data-ttu-id="2e23f-124">Bir [**Order**](order-resources.md) nesnesi örneği oluşturun ve müşteriyi kaydetmek Için **Referencecustomerıd** özelliğini müşteri kimliği olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="2e23f-124">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="2e23f-125">[**Orderlineıtem**](order-resources.md#orderlineitem) nesnelerinin bir listesini oluşturun ve listeyi Order 's **LineItems** özelliğine atayın.</span><span class="sxs-lookup"><span data-stu-id="2e23f-125">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="2e23f-126">Her sipariş satırı öğesi, bir teklifin satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="2e23f-126">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="2e23f-127">En az bir sipariş satırı öğesine sahip olmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="2e23f-127">You must have at least one order line item.</span></span>

3. <span data-ttu-id="2e23f-128">Sipariş işlemlerine yönelik bir arabirim edinin.</span><span class="sxs-lookup"><span data-stu-id="2e23f-128">Obtain an interface to order operations.</span></span> <span data-ttu-id="2e23f-129">İlk olarak, müşteriyi tanımlamak için [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) YÖNTEMINI Müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="2e23f-129">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="2e23f-130">Sonra, [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğinden arabirimi alın.</span><span class="sxs-lookup"><span data-stu-id="2e23f-130">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="2e23f-131">[**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) veya [**createasync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) metodunu çağırın ve [**Order**](order-resources.md) nesnesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="2e23f-131">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string customerId;
string offerId;

var order = new Order()
{
    ReferenceCustomerId = customerId,
    LineItems = new List<OrderLineItem>()
    {
        new OrderLineItem()
        {
            OfferId = offerId,
            FriendlyName = "new offer purchase",
            Quantity = 1,
            ProvisioningContext = new Dictionary<string, string>
            {
                { "subscriptionId", "5198C069-3DAA-403A-8660-5BE11BFD12EE" },
                { "scope", "shared" },
                { "duration", "3Years" }
            }
        }
    }
};

var createdOrder = partnerOperations.Customers.ById(customerId).Orders.Create(order);
```

<span data-ttu-id="2e23f-132">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2e23f-132">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2e23f-133">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="2e23f-133">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2e23f-134">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2e23f-134">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2e23f-135">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2e23f-135">Request syntax</span></span>

| <span data-ttu-id="2e23f-136">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2e23f-136">Method</span></span>   | <span data-ttu-id="2e23f-137">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2e23f-137">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="2e23f-138">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="2e23f-138">**POST**</span></span> | <span data-ttu-id="2e23f-139">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Orders http/1.1</span><span class="sxs-lookup"><span data-stu-id="2e23f-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="2e23f-140">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="2e23f-140">URI parameters</span></span>

<span data-ttu-id="2e23f-141">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e23f-141">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="2e23f-142">Ad</span><span class="sxs-lookup"><span data-stu-id="2e23f-142">Name</span></span>        | <span data-ttu-id="2e23f-143">Tür</span><span class="sxs-lookup"><span data-stu-id="2e23f-143">Type</span></span>   | <span data-ttu-id="2e23f-144">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2e23f-144">Required</span></span> | <span data-ttu-id="2e23f-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e23f-145">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="2e23f-146">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="2e23f-146">customer-id</span></span> | <span data-ttu-id="2e23f-147">string</span><span class="sxs-lookup"><span data-stu-id="2e23f-147">string</span></span> | <span data-ttu-id="2e23f-148">Yes</span><span class="sxs-lookup"><span data-stu-id="2e23f-148">Yes</span></span>      | <span data-ttu-id="2e23f-149">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="2e23f-149">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="2e23f-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2e23f-150">Request headers</span></span>

<span data-ttu-id="2e23f-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2e23f-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2e23f-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2e23f-152">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="2e23f-153">Sipariş</span><span class="sxs-lookup"><span data-stu-id="2e23f-153">Order</span></span>

<span data-ttu-id="2e23f-154">Bu tablo, istek gövdesindeki [sıra](order-resources.md) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2e23f-154">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="2e23f-155">Özellik</span><span class="sxs-lookup"><span data-stu-id="2e23f-155">Property</span></span>             | <span data-ttu-id="2e23f-156">Tür</span><span class="sxs-lookup"><span data-stu-id="2e23f-156">Type</span></span>                        | <span data-ttu-id="2e23f-157">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2e23f-157">Required</span></span>                        | <span data-ttu-id="2e23f-158">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e23f-158">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="2e23f-159">kimlik</span><span class="sxs-lookup"><span data-stu-id="2e23f-159">id</span></span>                   | <span data-ttu-id="2e23f-160">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-160">string</span></span>                      | <span data-ttu-id="2e23f-161">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-161">No</span></span>                              | <span data-ttu-id="2e23f-162">Siparişin başarıyla oluşturulması sırasında sağlanan bir sipariş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-162">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="2e23f-163">Referencecustomerıd</span><span class="sxs-lookup"><span data-stu-id="2e23f-163">referenceCustomerId</span></span>  | <span data-ttu-id="2e23f-164">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-164">string</span></span>                      | <span data-ttu-id="2e23f-165">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-165">No</span></span>                              | <span data-ttu-id="2e23f-166">Müşteri tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-166">The customer identifier.</span></span> |
| <span data-ttu-id="2e23f-167">Bilimlingcycle</span><span class="sxs-lookup"><span data-stu-id="2e23f-167">billingCycle</span></span>         | <span data-ttu-id="2e23f-168">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-168">string</span></span>                      | <span data-ttu-id="2e23f-169">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-169">No</span></span>                              | <span data-ttu-id="2e23f-170">Ortağın bu sipariş için faturalandırılabileceği sıklığı belirtir.</span><span class="sxs-lookup"><span data-stu-id="2e23f-170">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="2e23f-171">Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="2e23f-171">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="2e23f-172">"Aylık" veya "OneTime" varsayılan olarak sıralı oluşturma.</span><span class="sxs-lookup"><span data-stu-id="2e23f-172">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="2e23f-173">Bu alan, siparişin başarıyla oluşturulmasından sonra uygulanır.</span><span class="sxs-lookup"><span data-stu-id="2e23f-173">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="2e23f-174">LineItems</span><span class="sxs-lookup"><span data-stu-id="2e23f-174">lineItems</span></span>            | <span data-ttu-id="2e23f-175">[Orderlineıtem](order-resources.md#orderlineitem) kaynakları dizisi</span><span class="sxs-lookup"><span data-stu-id="2e23f-175">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="2e23f-176">Yes</span><span class="sxs-lookup"><span data-stu-id="2e23f-176">Yes</span></span>      | <span data-ttu-id="2e23f-177">Müşterinin miktarı dahil satın aldığı tekliflerinin listesi.</span><span class="sxs-lookup"><span data-stu-id="2e23f-177">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="2e23f-178">currencyCode</span><span class="sxs-lookup"><span data-stu-id="2e23f-178">currencyCode</span></span>         | <span data-ttu-id="2e23f-179">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-179">string</span></span>                      | <span data-ttu-id="2e23f-180">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-180">No</span></span>                              | <span data-ttu-id="2e23f-181">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="2e23f-181">Read-only.</span></span> <span data-ttu-id="2e23f-182">Sipariş yerleştirilirken kullanılan para birimi.</span><span class="sxs-lookup"><span data-stu-id="2e23f-182">The currency used when placing the order.</span></span> <span data-ttu-id="2e23f-183">Siparişin başarıyla oluşturulmasından sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-183">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="2e23f-184">creationDate</span><span class="sxs-lookup"><span data-stu-id="2e23f-184">creationDate</span></span>         | <span data-ttu-id="2e23f-185">datetime</span><span class="sxs-lookup"><span data-stu-id="2e23f-185">datetime</span></span>                    | <span data-ttu-id="2e23f-186">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-186">No</span></span>                              | <span data-ttu-id="2e23f-187">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="2e23f-187">Read-only.</span></span> <span data-ttu-id="2e23f-188">Siparişin oluşturulduğu tarih ve saat biçimi.</span><span class="sxs-lookup"><span data-stu-id="2e23f-188">The date the order was created, in date-time format.</span></span> <span data-ttu-id="2e23f-189">Siparişin başarıyla oluşturulmasından sonra uygulandı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-189">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="2e23f-190">durum</span><span class="sxs-lookup"><span data-stu-id="2e23f-190">status</span></span>               | <span data-ttu-id="2e23f-191">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-191">string</span></span>                      | <span data-ttu-id="2e23f-192">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-192">No</span></span>                              | <span data-ttu-id="2e23f-193">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="2e23f-193">Read-only.</span></span> <span data-ttu-id="2e23f-194">Siparişin durumu.</span><span class="sxs-lookup"><span data-stu-id="2e23f-194">The status of the order.</span></span>  <span data-ttu-id="2e23f-195">Desteklenen değerler [Orderstatus](order-resources.md#orderstatus)içinde bulunan üye adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="2e23f-195">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="2e23f-196">Köprü</span><span class="sxs-lookup"><span data-stu-id="2e23f-196">links</span></span>                | [<span data-ttu-id="2e23f-197">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="2e23f-197">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="2e23f-198">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-198">No</span></span>                              | <span data-ttu-id="2e23f-199">Sıraya karşılık gelen kaynak bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="2e23f-199">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="2e23f-200">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="2e23f-200">attributes</span></span>           | [<span data-ttu-id="2e23f-201">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="2e23f-201">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="2e23f-202">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-202">No</span></span>                              | <span data-ttu-id="2e23f-203">Sıraya karşılık gelen meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="2e23f-203">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="2e23f-204">Orderlineıtem</span><span class="sxs-lookup"><span data-stu-id="2e23f-204">OrderLineItem</span></span>

<span data-ttu-id="2e23f-205">Bu tablo, istek gövdesinde [Orderlineıtem](order-resources.md#orderlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2e23f-205">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="2e23f-206">PartnerIdOnRecord yalnızca dolaylı bir sağlayıcı dolaylı bir satıcı adına sipariş yerleştirirse sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="2e23f-206">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="2e23f-207">Yalnızca dolaylı satıcının Microsoft İş Ortağı Ağı KIMLIĞINI depolamak için kullanılır (dolaylı sağlayıcının KIMLIĞI değildir).</span><span class="sxs-lookup"><span data-stu-id="2e23f-207">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="2e23f-208">Ad</span><span class="sxs-lookup"><span data-stu-id="2e23f-208">Name</span></span>                 | <span data-ttu-id="2e23f-209">Tür</span><span class="sxs-lookup"><span data-stu-id="2e23f-209">Type</span></span>   | <span data-ttu-id="2e23f-210">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2e23f-210">Required</span></span> | <span data-ttu-id="2e23f-211">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e23f-211">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e23f-212">Lineıtemnumber</span><span class="sxs-lookup"><span data-stu-id="2e23f-212">lineItemNumber</span></span>       | <span data-ttu-id="2e23f-213">int</span><span class="sxs-lookup"><span data-stu-id="2e23f-213">int</span></span>    | <span data-ttu-id="2e23f-214">Yes</span><span class="sxs-lookup"><span data-stu-id="2e23f-214">Yes</span></span>      | <span data-ttu-id="2e23f-215">Koleksiyondaki her bir satır öğesi, 0 ' dan say-1 ' e kadar sayarak benzersiz bir satır numarası alır.</span><span class="sxs-lookup"><span data-stu-id="2e23f-215">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="2e23f-216">OfferId</span><span class="sxs-lookup"><span data-stu-id="2e23f-216">offerId</span></span>              | <span data-ttu-id="2e23f-217">string</span><span class="sxs-lookup"><span data-stu-id="2e23f-217">string</span></span> | <span data-ttu-id="2e23f-218">Yes</span><span class="sxs-lookup"><span data-stu-id="2e23f-218">Yes</span></span>      | <span data-ttu-id="2e23f-219">Teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-219">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="2e23f-220">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="2e23f-220">subscriptionId</span></span>       | <span data-ttu-id="2e23f-221">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-221">string</span></span> | <span data-ttu-id="2e23f-222">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-222">No</span></span>       | <span data-ttu-id="2e23f-223">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-223">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="2e23f-224">Parentsubscriptionıd</span><span class="sxs-lookup"><span data-stu-id="2e23f-224">parentSubscriptionId</span></span> | <span data-ttu-id="2e23f-225">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-225">string</span></span> | <span data-ttu-id="2e23f-226">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-226">No</span></span>       | <span data-ttu-id="2e23f-227">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-227">Optional.</span></span> <span data-ttu-id="2e23f-228">Bir eklenti teklifinde üst aboneliğin KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="2e23f-228">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="2e23f-229">Yalnızca düzeltme eki için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="2e23f-229">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="2e23f-230">friendlyName</span><span class="sxs-lookup"><span data-stu-id="2e23f-230">friendlyName</span></span>         | <span data-ttu-id="2e23f-231">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-231">string</span></span> | <span data-ttu-id="2e23f-232">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-232">No</span></span>       | <span data-ttu-id="2e23f-233">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-233">Optional.</span></span> <span data-ttu-id="2e23f-234">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-234">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="2e23f-235">miktar</span><span class="sxs-lookup"><span data-stu-id="2e23f-235">quantity</span></span>             | <span data-ttu-id="2e23f-236">int</span><span class="sxs-lookup"><span data-stu-id="2e23f-236">int</span></span>    | <span data-ttu-id="2e23f-237">Yes</span><span class="sxs-lookup"><span data-stu-id="2e23f-237">Yes</span></span>      | <span data-ttu-id="2e23f-238">Lisans tabanlı abonelik için lisans sayısı.</span><span class="sxs-lookup"><span data-stu-id="2e23f-238">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="2e23f-239">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="2e23f-239">partnerIdOnRecord</span></span>    | <span data-ttu-id="2e23f-240">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-240">string</span></span> | <span data-ttu-id="2e23f-241">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-241">No</span></span>       | <span data-ttu-id="2e23f-242">Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir).</span><span class="sxs-lookup"><span data-stu-id="2e23f-242">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="2e23f-243">Bu, teşvikleri için doğru hesaplamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="2e23f-243">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="2e23f-244">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="2e23f-244">provisioningContext</span></span>  | <span data-ttu-id="2e23f-245">Sözlük<dize, dize></span><span class="sxs-lookup"><span data-stu-id="2e23f-245">Dictionary<string, string></span></span>                | <span data-ttu-id="2e23f-246">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-246">No</span></span>       |  <span data-ttu-id="2e23f-247">Katalogdaki bazı öğelerin sağlanması için gereken bilgiler.</span><span class="sxs-lookup"><span data-stu-id="2e23f-247">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="2e23f-248">SKU 'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="2e23f-248">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="2e23f-249">Köprü</span><span class="sxs-lookup"><span data-stu-id="2e23f-249">links</span></span>                | [<span data-ttu-id="2e23f-250">Orderlineıtemlinks</span><span class="sxs-lookup"><span data-stu-id="2e23f-250">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="2e23f-251">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-251">No</span></span>       |  <span data-ttu-id="2e23f-252">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="2e23f-252">Read-only.</span></span> <span data-ttu-id="2e23f-253">Sipariş satırı öğesine karşılık gelen kaynak bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="2e23f-253">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="2e23f-254">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="2e23f-254">attributes</span></span>           | [<span data-ttu-id="2e23f-255">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="2e23f-255">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="2e23f-256">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-256">No</span></span>       | <span data-ttu-id="2e23f-257">Orderlineıtem öğesine karşılık gelen meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="2e23f-257">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="2e23f-258">renewsTo</span><span class="sxs-lookup"><span data-stu-id="2e23f-258">renewsTo</span></span>             | <span data-ttu-id="2e23f-259">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="2e23f-259">Array of objects</span></span>                          | <span data-ttu-id="2e23f-260">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-260">No</span></span>    |<span data-ttu-id="2e23f-261">[RenewsTo](order-resources.md#renewsto) kaynaklarından oluşan bir dizi.</span><span class="sxs-lookup"><span data-stu-id="2e23f-261">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="2e23f-262">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="2e23f-262">RenewsTo</span></span>

<span data-ttu-id="2e23f-263">Bu tablo, istek gövdesinde [RenewsTo](order-resources.md#renewsto) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="2e23f-263">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="2e23f-264">Özellik</span><span class="sxs-lookup"><span data-stu-id="2e23f-264">Property</span></span>              | <span data-ttu-id="2e23f-265">Tür</span><span class="sxs-lookup"><span data-stu-id="2e23f-265">Type</span></span>             | <span data-ttu-id="2e23f-266">Gerekli</span><span class="sxs-lookup"><span data-stu-id="2e23f-266">Required</span></span>        | <span data-ttu-id="2e23f-267">Açıklama</span><span class="sxs-lookup"><span data-stu-id="2e23f-267">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="2e23f-268">termDuration</span><span class="sxs-lookup"><span data-stu-id="2e23f-268">termDuration</span></span>          | <span data-ttu-id="2e23f-269">dize</span><span class="sxs-lookup"><span data-stu-id="2e23f-269">string</span></span>           | <span data-ttu-id="2e23f-270">No</span><span class="sxs-lookup"><span data-stu-id="2e23f-270">No</span></span>              | <span data-ttu-id="2e23f-271">Yenileme teriminin süresinin ISO 8601 temsili.</span><span class="sxs-lookup"><span data-stu-id="2e23f-271">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="2e23f-272">Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl).</span><span class="sxs-lookup"><span data-stu-id="2e23f-272">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="2e23f-273">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2e23f-273">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders HTTP/1.1
Authorization: Bearer <token>
Host: api.partnercenter.microsoft.com
Content-Length: 691
Content-Type: application/json

{
  "BillingCycle": "one_time",
  "CurrencyCode": "USD",
  "LineItems": [
    {
      "LineItemNumber": 0,
      "ProvisioningContext": {
        "subscriptionId": "3D5ECED6-1151-44C7-AEE6-70A4BB725666",
        "scope": "shared",
        "duration": "1Year"
      },
      "OfferId": "DZH318Z0BQ4B:0047:DZH318Z0DSM8",
      "FriendlyName": "A_sample_Azure_RI",
      "Quantity": 1
    }
  ]
}
```

## <a name="rest-response"></a><span data-ttu-id="2e23f-274">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2e23f-274">REST response</span></span>

<span data-ttu-id="2e23f-275">Başarılı olursa, yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="2e23f-275">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2e23f-276">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2e23f-276">Response success and error codes</span></span>

<span data-ttu-id="2e23f-277">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2e23f-277">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2e23f-278">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2e23f-278">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2e23f-279">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2e23f-279">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2e23f-280">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2e23f-280">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 788
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b593cbb7-b358-4b31-81fc-e60b9c277a7f
MS-RequestId: 025f4c19-217f-49d6-a056-391902c62fb3
Date: Thu, 15 Mar 2018 22:30:02 GMT

{
  "id": "Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
  "referenceCustomerId": "b0d70a69-4c42-4b27-b17b-91a835d8686a",
  "billingCycle": "one_time",
  "currencyCode": "USD",
  "lineItems": [
    {
        "lineItemNumber": 0,
        "offerId": "84A03D81-6B37-4D66-8D4A-FAEA24541538",
        "friendlyName": "A_sample_Azure_RI",
        "quantity": 1,
        "links": {
            "sku": {
                "uri": "/products/DZH318Z0BQ4B/skus/0047?country=US",
                "method": "GET",
                "headers": []
            }
        }
    } ],
    "creationDate": "2018-03-15T22:30:02.085152Z",
    "status": "pending",
    "links": {
        "provisioningStatus": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "self": {
            "uri": "/customers/b0d70a69-4c42-4b27-b17b-91a835d8686a/orders/Cs_jyTxubLpvdJXdo8xcQZN6I2RsLrgZ1",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
