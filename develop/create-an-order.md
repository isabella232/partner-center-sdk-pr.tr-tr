---
title: Müşteri siparişi oluşturma
description: Müşteri için sipariş İş Ortağı Merkezi API'leri kullanmayı öğrenin. Makale önkoşulları, adımları ve örnekleri içerir.
ms.date: 07/12/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3a86a99f43bdeec5e4c560ab59e1924b76c0636
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973562"
---
# <a name="create-an-order-for-a-customer-using-partner-center-apis"></a><span data-ttu-id="995cc-104">İş Ortağı Merkezi API'lerini kullanarak müşteri İş Ortağı Merkezi oluşturma</span><span class="sxs-lookup"><span data-stu-id="995cc-104">Create an order for a customer using Partner Center APIs</span></span>

<span data-ttu-id="995cc-105">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="995cc-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="995cc-106">Azure ayrılmış **VM örneği ürünleri için sipariş oluşturma yalnızca** *aşağıdakiler için* geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="995cc-106">Creating an **order for Azure reserved VM instance products** applies *only* to:</span></span>

- <span data-ttu-id="995cc-107">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="995cc-107">Partner Center</span></span>

<span data-ttu-id="995cc-108">Şu anda satış için nelerin kullanılabilir olduğu hakkında daha fazla bilgi için, Bulut Çözümü Sağlayıcısı [bakın.](/partner-center/csp-offers)</span><span class="sxs-lookup"><span data-stu-id="995cc-108">For information about what is currently available to sell, see [Partner offers in the Cloud Solution Provider program](/partner-center/csp-offers).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="995cc-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="995cc-109">Prerequisites</span></span>

- <span data-ttu-id="995cc-110">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="995cc-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="995cc-111">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="995cc-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="995cc-112">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="995cc-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="995cc-113">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="995cc-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="995cc-114">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="995cc-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="995cc-115">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="995cc-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="995cc-116">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="995cc-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="995cc-117">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="995cc-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="995cc-118">Teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="995cc-118">An offer identifier.</span></span>

## <a name="c"></a><span data-ttu-id="995cc-119">C\#</span><span class="sxs-lookup"><span data-stu-id="995cc-119">C\#</span></span>

<span data-ttu-id="995cc-120">Bir müşteriye sipariş oluşturmak için:</span><span class="sxs-lookup"><span data-stu-id="995cc-120">To create an order for a customer:</span></span>

1. <span data-ttu-id="995cc-121">Bir Order nesnesi [**örneği**](order-resources.md) oluşturma ve müşteriyi kaydetmek **için ReferenceCustomerID** özelliğini müşteri kimliğine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="995cc-121">Instantiate an [**Order**](order-resources.md) object and set the **ReferenceCustomerID** property to the customer ID to record the customer.</span></span>

2. <span data-ttu-id="995cc-122">[**OrderLineItem nesnelerinin**](order-resources.md#orderlineitem) listesini oluşturun ve listeyi siparişin **LineItems özelliğine** attayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="995cc-122">Create a list of [**OrderLineItem**](order-resources.md#orderlineitem) objects, and assign the list to the order's **LineItems** property.</span></span> <span data-ttu-id="995cc-123">Her sipariş satırı öğesi, bir teklif için satın alma bilgilerini içerir.</span><span class="sxs-lookup"><span data-stu-id="995cc-123">Each order line item contains the purchase information for one offer.</span></span> <span data-ttu-id="995cc-124">En az bir sipariş satırı öğeniz olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="995cc-124">You must have at least one order line item.</span></span>

3. <span data-ttu-id="995cc-125">İşlemleri sıralamak için bir arabirim elde edin.</span><span class="sxs-lookup"><span data-stu-id="995cc-125">Obtain an interface to order operations.</span></span> <span data-ttu-id="995cc-126">İlk olarak, [**müşteri kimliğini kullanarak IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırarak müşteriyi tanıyın.</span><span class="sxs-lookup"><span data-stu-id="995cc-126">First, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="995cc-127">Ardından Orders özelliğinden [**arabirimini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) alın.</span><span class="sxs-lookup"><span data-stu-id="995cc-127">Next, retrieve the interface from the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property.</span></span>

4. <span data-ttu-id="995cc-128">[**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) veya [**CreateAsync yöntemini**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) çağırma ve [**Order nesnesine**](order-resources.md) geçme.</span><span class="sxs-lookup"><span data-stu-id="995cc-128">Call the [**Create**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.create) or [**CreateAsync**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.createasync) method and pass in the [**Order**](order-resources.md) object.</span></span>

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

<span data-ttu-id="995cc-129">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="995cc-129">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="995cc-130">**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** CreateOrder.cs</span><span class="sxs-lookup"><span data-stu-id="995cc-130">**Project**: Partner Center SDK Samples **Class**: CreateOrder.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="995cc-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="995cc-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="995cc-132">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="995cc-132">Request syntax</span></span>

| <span data-ttu-id="995cc-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="995cc-133">Method</span></span>   | <span data-ttu-id="995cc-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="995cc-134">Request URI</span></span>                                                                            |
|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="995cc-135">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="995cc-135">**POST**</span></span> | <span data-ttu-id="995cc-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="995cc-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/orders HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="995cc-137">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="995cc-137">URI parameters</span></span>

<span data-ttu-id="995cc-138">Müşteriyi tanımlamak için aşağıdaki yol parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="995cc-138">Use the following path parameter to identify the customer.</span></span>

| <span data-ttu-id="995cc-139">Ad</span><span class="sxs-lookup"><span data-stu-id="995cc-139">Name</span></span>        | <span data-ttu-id="995cc-140">Tür</span><span class="sxs-lookup"><span data-stu-id="995cc-140">Type</span></span>   | <span data-ttu-id="995cc-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="995cc-141">Required</span></span> | <span data-ttu-id="995cc-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="995cc-142">Description</span></span>                                                |
|-------------|--------|----------|------------------------------------------------------------|
| <span data-ttu-id="995cc-143">customer-id</span><span class="sxs-lookup"><span data-stu-id="995cc-143">customer-id</span></span> | <span data-ttu-id="995cc-144">string</span><span class="sxs-lookup"><span data-stu-id="995cc-144">string</span></span> | <span data-ttu-id="995cc-145">Yes</span><span class="sxs-lookup"><span data-stu-id="995cc-145">Yes</span></span>      | <span data-ttu-id="995cc-146">Müşteriyi tanımlayan GUID biçimlendirilmiş customer-id.</span><span class="sxs-lookup"><span data-stu-id="995cc-146">A GUID formatted customer-id that identifies the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="995cc-147">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="995cc-147">Request headers</span></span>

<span data-ttu-id="995cc-148">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="995cc-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="995cc-149">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="995cc-149">Request body</span></span>

#### <a name="order"></a><span data-ttu-id="995cc-150">Sipariş</span><span class="sxs-lookup"><span data-stu-id="995cc-150">Order</span></span>

<span data-ttu-id="995cc-151">Bu tablo, istek [gövdesinin](order-resources.md) Sipariş özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="995cc-151">This table describes the [Order](order-resources.md) properties in the request body.</span></span>

| <span data-ttu-id="995cc-152">Özellik</span><span class="sxs-lookup"><span data-stu-id="995cc-152">Property</span></span>             | <span data-ttu-id="995cc-153">Tür</span><span class="sxs-lookup"><span data-stu-id="995cc-153">Type</span></span>                        | <span data-ttu-id="995cc-154">Gerekli</span><span class="sxs-lookup"><span data-stu-id="995cc-154">Required</span></span>                        | <span data-ttu-id="995cc-155">Açıklama</span><span class="sxs-lookup"><span data-stu-id="995cc-155">Description</span></span>                                                                   |
|----------------------|-----------------------------|---------------------------------|-------------------------------------------------------------------------------|
| <span data-ttu-id="995cc-156">kimlik</span><span class="sxs-lookup"><span data-stu-id="995cc-156">id</span></span>                   | <span data-ttu-id="995cc-157">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-157">string</span></span>                      | <span data-ttu-id="995cc-158">No</span><span class="sxs-lookup"><span data-stu-id="995cc-158">No</span></span>                              | <span data-ttu-id="995cc-159">Siparişin başarıyla oluşturulmasının ardından sağlanan bir sipariş tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="995cc-159">An order identifier that is supplied upon successful creation of the order.</span></span>   |
| <span data-ttu-id="995cc-160">referenceCustomerId</span><span class="sxs-lookup"><span data-stu-id="995cc-160">referenceCustomerId</span></span>  | <span data-ttu-id="995cc-161">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-161">string</span></span>                      | <span data-ttu-id="995cc-162">No</span><span class="sxs-lookup"><span data-stu-id="995cc-162">No</span></span>                              | <span data-ttu-id="995cc-163">Müşteri tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="995cc-163">The customer identifier.</span></span> |
| <span data-ttu-id="995cc-164">billingCycle</span><span class="sxs-lookup"><span data-stu-id="995cc-164">billingCycle</span></span>         | <span data-ttu-id="995cc-165">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-165">string</span></span>                      | <span data-ttu-id="995cc-166">No</span><span class="sxs-lookup"><span data-stu-id="995cc-166">No</span></span>                              | <span data-ttu-id="995cc-167">İş ortağının bu sipariş için faturalandırılama sıklığını gösterir.</span><span class="sxs-lookup"><span data-stu-id="995cc-167">Indicates the frequency with which the partner is billed for this order.</span></span> <span data-ttu-id="995cc-168">Desteklenen değerler, [BillingCycleType](product-resources.md#billingcycletype)içinde bulunan üye adlarıdır.</span><span class="sxs-lookup"><span data-stu-id="995cc-168">Supported values are the member names found in [BillingCycleType](product-resources.md#billingcycletype).</span></span> <span data-ttu-id="995cc-169">Varsayılan değer, sipariş oluşturma sırasında "Monthly" veya "OneTime" şeklindedir.</span><span class="sxs-lookup"><span data-stu-id="995cc-169">The default is "Monthly" or "OneTime" at order creation.</span></span> <span data-ttu-id="995cc-170">Bu alan, siparişin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="995cc-170">This field is applied upon successful creation of the order.</span></span> |
| <span data-ttu-id="995cc-171">lineItems</span><span class="sxs-lookup"><span data-stu-id="995cc-171">lineItems</span></span>            | <span data-ttu-id="995cc-172">[OrderLineItem kaynakları](order-resources.md#orderlineitem) dizisi</span><span class="sxs-lookup"><span data-stu-id="995cc-172">array of [OrderLineItem](order-resources.md#orderlineitem) resources</span></span> | <span data-ttu-id="995cc-173">Yes</span><span class="sxs-lookup"><span data-stu-id="995cc-173">Yes</span></span>      | <span data-ttu-id="995cc-174">Miktarı da dahil olmak üzere müşterinin satın alma tekliflerinin maddeli listesi.</span><span class="sxs-lookup"><span data-stu-id="995cc-174">An itemized list of the offers the customer is purchasing including the quantity.</span></span>        |
| <span data-ttu-id="995cc-175">currencyCode</span><span class="sxs-lookup"><span data-stu-id="995cc-175">currencyCode</span></span>         | <span data-ttu-id="995cc-176">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-176">string</span></span>                      | <span data-ttu-id="995cc-177">No</span><span class="sxs-lookup"><span data-stu-id="995cc-177">No</span></span>                              | <span data-ttu-id="995cc-178">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="995cc-178">Read-only.</span></span> <span data-ttu-id="995cc-179">Siparişin yerleştirilmesi için kullanılan para birimi.</span><span class="sxs-lookup"><span data-stu-id="995cc-179">The currency used when placing the order.</span></span> <span data-ttu-id="995cc-180">Siparişin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="995cc-180">Applied upon successful creation of the order.</span></span>           |
| <span data-ttu-id="995cc-181">Creationdate</span><span class="sxs-lookup"><span data-stu-id="995cc-181">creationDate</span></span>         | <span data-ttu-id="995cc-182">datetime</span><span class="sxs-lookup"><span data-stu-id="995cc-182">datetime</span></span>                    | <span data-ttu-id="995cc-183">Hayır</span><span class="sxs-lookup"><span data-stu-id="995cc-183">No</span></span>                              | <span data-ttu-id="995cc-184">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="995cc-184">Read-only.</span></span> <span data-ttu-id="995cc-185">Siparişin tarih-saat biçiminde oluşturulma tarihi.</span><span class="sxs-lookup"><span data-stu-id="995cc-185">The date the order was created, in date-time format.</span></span> <span data-ttu-id="995cc-186">Siparişin başarıyla oluşturulmasının ardından uygulanır.</span><span class="sxs-lookup"><span data-stu-id="995cc-186">Applied upon successful creation of the order.</span></span>                                   |
| <span data-ttu-id="995cc-187">durum</span><span class="sxs-lookup"><span data-stu-id="995cc-187">status</span></span>               | <span data-ttu-id="995cc-188">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-188">string</span></span>                      | <span data-ttu-id="995cc-189">No</span><span class="sxs-lookup"><span data-stu-id="995cc-189">No</span></span>                              | <span data-ttu-id="995cc-190">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="995cc-190">Read-only.</span></span> <span data-ttu-id="995cc-191">Siparişin durumu.</span><span class="sxs-lookup"><span data-stu-id="995cc-191">The status of the order.</span></span>  <span data-ttu-id="995cc-192">Desteklenen değerler OrderStatus içinde bulunan üye [adlarıdır.](order-resources.md#orderstatus)</span><span class="sxs-lookup"><span data-stu-id="995cc-192">Supported values are the member names found in [OrderStatus](order-resources.md#orderstatus).</span></span>        |
| <span data-ttu-id="995cc-193">Bağlantı</span><span class="sxs-lookup"><span data-stu-id="995cc-193">links</span></span>                | [<span data-ttu-id="995cc-194">OrderLinks</span><span class="sxs-lookup"><span data-stu-id="995cc-194">OrderLinks</span></span>](utility-resources.md#resourcelinks)              | <span data-ttu-id="995cc-195">Hayır</span><span class="sxs-lookup"><span data-stu-id="995cc-195">No</span></span>                              | <span data-ttu-id="995cc-196">Siparişe karşılık gelen kaynak bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="995cc-196">The resource links corresponding to the Order.</span></span> |
| <span data-ttu-id="995cc-197">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="995cc-197">attributes</span></span>           | [<span data-ttu-id="995cc-198">Resourceattributes</span><span class="sxs-lookup"><span data-stu-id="995cc-198">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="995cc-199">Hayır</span><span class="sxs-lookup"><span data-stu-id="995cc-199">No</span></span>                              | <span data-ttu-id="995cc-200">Order'a karşılık gelen meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="995cc-200">The metadata attributes corresponding to the Order.</span></span> |

#### <a name="orderlineitem"></a><span data-ttu-id="995cc-201">Orderlineıtem</span><span class="sxs-lookup"><span data-stu-id="995cc-201">OrderLineItem</span></span>

<span data-ttu-id="995cc-202">Bu tablo, istek gövdesinde [Orderlineıtem](order-resources.md#orderlineitem) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="995cc-202">This table describes the [OrderLineItem](order-resources.md#orderlineitem) properties in the request body.</span></span>

>[!NOTE]
><span data-ttu-id="995cc-203">PartnerIdOnRecord yalnızca dolaylı bir sağlayıcı dolaylı bir satıcı adına sipariş yerleştirirse sağlanmalıdır.</span><span class="sxs-lookup"><span data-stu-id="995cc-203">The partnerIdOnRecord should only be provided when an indirect provider places an order on behalf of an indirect reseller.</span></span> <span data-ttu-id="995cc-204">Yalnızca dolaylı satıcının Microsoft İş Ortağı Ağı KIMLIĞINI depolamak için kullanılır (dolaylı sağlayıcının KIMLIĞI değildir).</span><span class="sxs-lookup"><span data-stu-id="995cc-204">It's used to store the Microsoft Partner Network ID of the indirect reseller only (never the ID of the indirect provider).</span></span>

| <span data-ttu-id="995cc-205">Ad</span><span class="sxs-lookup"><span data-stu-id="995cc-205">Name</span></span>                 | <span data-ttu-id="995cc-206">Tür</span><span class="sxs-lookup"><span data-stu-id="995cc-206">Type</span></span>   | <span data-ttu-id="995cc-207">Gerekli</span><span class="sxs-lookup"><span data-stu-id="995cc-207">Required</span></span> | <span data-ttu-id="995cc-208">Açıklama</span><span class="sxs-lookup"><span data-stu-id="995cc-208">Description</span></span>                                                                                                                                                                                                                                |
|----------------------|--------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="995cc-209">Lineıtemnumber</span><span class="sxs-lookup"><span data-stu-id="995cc-209">lineItemNumber</span></span>       | <span data-ttu-id="995cc-210">int</span><span class="sxs-lookup"><span data-stu-id="995cc-210">int</span></span>    | <span data-ttu-id="995cc-211">Yes</span><span class="sxs-lookup"><span data-stu-id="995cc-211">Yes</span></span>      | <span data-ttu-id="995cc-212">Koleksiyondaki her bir satır öğesi, 0 ' dan say-1 ' e kadar sayarak benzersiz bir satır numarası alır.</span><span class="sxs-lookup"><span data-stu-id="995cc-212">Each line item in the collection gets a unique line number, counting up from 0 to count-1.</span></span>                                                                                                                                                 |
| <span data-ttu-id="995cc-213">OfferId</span><span class="sxs-lookup"><span data-stu-id="995cc-213">offerId</span></span>              | <span data-ttu-id="995cc-214">string</span><span class="sxs-lookup"><span data-stu-id="995cc-214">string</span></span> | <span data-ttu-id="995cc-215">Yes</span><span class="sxs-lookup"><span data-stu-id="995cc-215">Yes</span></span>      | <span data-ttu-id="995cc-216">Teklif tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="995cc-216">The offer identifier.</span></span>                                                                                                                                                                                                                      |
| <span data-ttu-id="995cc-217">subscriptionId</span><span class="sxs-lookup"><span data-stu-id="995cc-217">subscriptionId</span></span>       | <span data-ttu-id="995cc-218">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-218">string</span></span> | <span data-ttu-id="995cc-219">No</span><span class="sxs-lookup"><span data-stu-id="995cc-219">No</span></span>       | <span data-ttu-id="995cc-220">Abonelik tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="995cc-220">The subscription identifier.</span></span>                                                                                                                                                                                                               |
| <span data-ttu-id="995cc-221">Parentsubscriptionıd</span><span class="sxs-lookup"><span data-stu-id="995cc-221">parentSubscriptionId</span></span> | <span data-ttu-id="995cc-222">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-222">string</span></span> | <span data-ttu-id="995cc-223">No</span><span class="sxs-lookup"><span data-stu-id="995cc-223">No</span></span>       | <span data-ttu-id="995cc-224">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="995cc-224">Optional.</span></span> <span data-ttu-id="995cc-225">Bir eklenti teklifinde üst aboneliğin KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="995cc-225">The ID of the parent subscription in an add-on offer.</span></span> <span data-ttu-id="995cc-226">Yalnızca düzeltme eki için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="995cc-226">Applies to PATCH only.</span></span>                                                                                                                                                     |
| <span data-ttu-id="995cc-227">friendlyName</span><span class="sxs-lookup"><span data-stu-id="995cc-227">friendlyName</span></span>         | <span data-ttu-id="995cc-228">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-228">string</span></span> | <span data-ttu-id="995cc-229">No</span><span class="sxs-lookup"><span data-stu-id="995cc-229">No</span></span>       | <span data-ttu-id="995cc-230">İsteğe bağlı.</span><span class="sxs-lookup"><span data-stu-id="995cc-230">Optional.</span></span> <span data-ttu-id="995cc-231">Belirsizliği ortadan kaldırmaya yardımcı olmak için iş ortağı tarafından tanımlanan aboneliğin kolay adı.</span><span class="sxs-lookup"><span data-stu-id="995cc-231">The friendly name for the subscription defined by the partner to help disambiguate.</span></span>                                                                                                                                              |
| <span data-ttu-id="995cc-232">miktar</span><span class="sxs-lookup"><span data-stu-id="995cc-232">quantity</span></span>             | <span data-ttu-id="995cc-233">int</span><span class="sxs-lookup"><span data-stu-id="995cc-233">int</span></span>    | <span data-ttu-id="995cc-234">Yes</span><span class="sxs-lookup"><span data-stu-id="995cc-234">Yes</span></span>      | <span data-ttu-id="995cc-235">Lisans tabanlı abonelik için lisans sayısı.</span><span class="sxs-lookup"><span data-stu-id="995cc-235">The number of licenses for a license-based subscription.</span></span>                                                                                                                                                                                   |
| <span data-ttu-id="995cc-236">partnerIdOnRecord</span><span class="sxs-lookup"><span data-stu-id="995cc-236">partnerIdOnRecord</span></span>    | <span data-ttu-id="995cc-237">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-237">string</span></span> | <span data-ttu-id="995cc-238">No</span><span class="sxs-lookup"><span data-stu-id="995cc-238">No</span></span>       | <span data-ttu-id="995cc-239">Dolaylı bir sağlayıcı dolaylı bir satıcı adına bir sipariş yerleştirirse, bu alanı **yalnızca dolaylı** satıcının MPN kimliğiyle doldurun (hiçbir zaman dolaylı sağlayıcının kimliği değildir).</span><span class="sxs-lookup"><span data-stu-id="995cc-239">When an indirect provider places an order on behalf of an indirect reseller, populate this field with the MPN ID of the **indirect reseller only** (never the ID of the indirect provider).</span></span> <span data-ttu-id="995cc-240">Bu, teşvikleri için doğru hesaplamayı sağlar.</span><span class="sxs-lookup"><span data-stu-id="995cc-240">This ensures proper accounting for incentives.</span></span> |
| <span data-ttu-id="995cc-241">provisioningContext</span><span class="sxs-lookup"><span data-stu-id="995cc-241">provisioningContext</span></span>  | <span data-ttu-id="995cc-242">Sözlük<dize, dize></span><span class="sxs-lookup"><span data-stu-id="995cc-242">Dictionary<string, string></span></span>                | <span data-ttu-id="995cc-243">Hayır</span><span class="sxs-lookup"><span data-stu-id="995cc-243">No</span></span>       |  <span data-ttu-id="995cc-244">Katalogdaki bazı öğelerin sağlanması için gereken bilgiler.</span><span class="sxs-lookup"><span data-stu-id="995cc-244">Information required for provisioning for some items in the catalog.</span></span> <span data-ttu-id="995cc-245">SKU 'daki provisioningVariables özelliği, katalogdaki belirli öğeler için hangi özelliklerin gerekli olduğunu gösterir.</span><span class="sxs-lookup"><span data-stu-id="995cc-245">The provisioningVariables property in a SKU indicates which properties are required for specific items in the catalog.</span></span>                  |
| <span data-ttu-id="995cc-246">Köprü</span><span class="sxs-lookup"><span data-stu-id="995cc-246">links</span></span>                | [<span data-ttu-id="995cc-247">Orderlineıtemlinks</span><span class="sxs-lookup"><span data-stu-id="995cc-247">OrderLineItemLinks</span></span>](order-resources.md#orderlineitemlinks) | <span data-ttu-id="995cc-248">Hayır</span><span class="sxs-lookup"><span data-stu-id="995cc-248">No</span></span>       |  <span data-ttu-id="995cc-249">Salt okunur.</span><span class="sxs-lookup"><span data-stu-id="995cc-249">Read-only.</span></span> <span data-ttu-id="995cc-250">Sipariş satırı öğesine karşılık gelen kaynak bağlantıları.</span><span class="sxs-lookup"><span data-stu-id="995cc-250">The resource links corresponding to the Order line item.</span></span>  |
| <span data-ttu-id="995cc-251">öznitelikler</span><span class="sxs-lookup"><span data-stu-id="995cc-251">attributes</span></span>           | [<span data-ttu-id="995cc-252">ResourceAttributes</span><span class="sxs-lookup"><span data-stu-id="995cc-252">ResourceAttributes</span></span>](utility-resources.md#resourceattributes) | <span data-ttu-id="995cc-253">Hayır</span><span class="sxs-lookup"><span data-stu-id="995cc-253">No</span></span>       | <span data-ttu-id="995cc-254">Orderlineıtem öğesine karşılık gelen meta veri öznitelikleri.</span><span class="sxs-lookup"><span data-stu-id="995cc-254">The metadata attributes corresponding to the OrderLineItem.</span></span> |
| <span data-ttu-id="995cc-255">renewsTo</span><span class="sxs-lookup"><span data-stu-id="995cc-255">renewsTo</span></span>             | <span data-ttu-id="995cc-256">Nesne dizisi</span><span class="sxs-lookup"><span data-stu-id="995cc-256">Array of objects</span></span>                          | <span data-ttu-id="995cc-257">Hayır</span><span class="sxs-lookup"><span data-stu-id="995cc-257">No</span></span>    |<span data-ttu-id="995cc-258">[RenewsTo](order-resources.md#renewsto) kaynaklarından oluşan bir dizi.</span><span class="sxs-lookup"><span data-stu-id="995cc-258">An array of [RenewsTo](order-resources.md#renewsto) resources.</span></span>                                                                            |

##### <a name="renewsto"></a><span data-ttu-id="995cc-259">RenewsTo</span><span class="sxs-lookup"><span data-stu-id="995cc-259">RenewsTo</span></span>

<span data-ttu-id="995cc-260">Bu tablo, istek gövdesinde [RenewsTo](order-resources.md#renewsto) özelliklerini açıklar.</span><span class="sxs-lookup"><span data-stu-id="995cc-260">This table describes the [RenewsTo](order-resources.md#renewsto) properties in the request body.</span></span>

| <span data-ttu-id="995cc-261">Özellik</span><span class="sxs-lookup"><span data-stu-id="995cc-261">Property</span></span>              | <span data-ttu-id="995cc-262">Tür</span><span class="sxs-lookup"><span data-stu-id="995cc-262">Type</span></span>             | <span data-ttu-id="995cc-263">Gerekli</span><span class="sxs-lookup"><span data-stu-id="995cc-263">Required</span></span>        | <span data-ttu-id="995cc-264">Açıklama</span><span class="sxs-lookup"><span data-stu-id="995cc-264">Description</span></span> |
|-----------------------|------------------|-----------------|-------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="995cc-265">termDuration</span><span class="sxs-lookup"><span data-stu-id="995cc-265">termDuration</span></span>          | <span data-ttu-id="995cc-266">dize</span><span class="sxs-lookup"><span data-stu-id="995cc-266">string</span></span>           | <span data-ttu-id="995cc-267">No</span><span class="sxs-lookup"><span data-stu-id="995cc-267">No</span></span>              | <span data-ttu-id="995cc-268">Yenileme teriminin süresinin ISO 8601 temsili.</span><span class="sxs-lookup"><span data-stu-id="995cc-268">An ISO 8601 representation of the renewal term's duration.</span></span> <span data-ttu-id="995cc-269">Desteklenen geçerli değerler **P1M** (1 ay) ve **P1Y** (1 yıl).</span><span class="sxs-lookup"><span data-stu-id="995cc-269">The current supported values are **P1M** (1 month) and **P1Y** (1 year).</span></span> |

### <a name="request-example"></a><span data-ttu-id="995cc-270">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="995cc-270">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="995cc-271">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="995cc-271">REST response</span></span>

<span data-ttu-id="995cc-272">Başarılı olursa, yöntem yanıt gövdesinde bir [sipariş](order-resources.md) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="995cc-272">If successful, the method returns an [Order](order-resources.md) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="995cc-273">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="995cc-273">Response success and error codes</span></span>

<span data-ttu-id="995cc-274">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="995cc-274">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="995cc-275">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="995cc-275">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="995cc-276">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="995cc-276">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="995cc-277">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="995cc-277">Response example</span></span>

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
