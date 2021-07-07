---
title: API azaltma yönergeleri
description: Api'leri İş Ortağı Merkezi iş ortakları için, hangi API'lerin Microsoft API azaltmadan etkilene olduğunu ve azaltmayı önlemeye veya daha iyi işlemeye yönelik en iyi yöntemleri öğrenin.
ms.date: 04/14/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: f18518e88b9bb08d4fd248922f4ce2fefdde004f
ms.sourcegitcommit: c7dd3f92cade7f127f88cf6d4d6df5e9a05eca41
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/11/2021
ms.locfileid: "112025658"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="51f44-103">Api'leri çağıran iş ortakları için API İş Ortağı Merkezi azaltma kılavuzu</span><span class="sxs-lookup"><span data-stu-id="51f44-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="51f44-104">Microsoft, API'leri çağıran iş ortaklarının belirli bir zaman aralığı içinde daha tutarlı bir performans elde İş Ortağı Merkezi gerçekleştirmektedir.</span><span class="sxs-lookup"><span data-stu-id="51f44-104">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="51f44-105">Azaltma, kaynakların aşırı kullanımına engel olmak için bir zaman aralığı içinde hizmete yapılan istek sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="51f44-105">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="51f44-106">Bu İş Ortağı Merkezi, yüksek hacimli istekleri işlemek için tasarlansa da, az sayıda iş ortağı tarafından çok fazla istek oluşursa kısıtlama tüm iş ortakları için en iyi performansın ve güvenilirliğin korunmasına yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="51f44-106">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="51f44-107">Azaltma sınırları senaryoya göre değişiklik gösterir.</span><span class="sxs-lookup"><span data-stu-id="51f44-107">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="51f44-108">Örneğin, büyük hacimli yazmalar yapıyorsanız azaltma olasılığı yalnızca okumalar yapıyorsanız daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="51f44-108">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="51f44-109">Azaltma oluştuğunda ne olur?</span><span class="sxs-lookup"><span data-stu-id="51f44-109">What happens when throttling occurs?</span></span> 

<span data-ttu-id="51f44-110">Bir azaltma eşiği aşılırsa, İş Ortağı Merkezi istemciden gelen diğer tüm istekleri bir süre için sınırlar.</span><span class="sxs-lookup"><span data-stu-id="51f44-110">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="51f44-111">Azaltma davranışı istek türüne ve sayısına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="51f44-111">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="51f44-112">Yaygın azaltma senaryoları</span><span class="sxs-lookup"><span data-stu-id="51f44-112">Common throttling scenarios</span></span> 

<span data-ttu-id="51f44-113">İstemcilerin azaltmanın en yaygın nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="51f44-113">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="51f44-114">**İş Ortağı** Kiracı Kimliği başına çok sayıda API isteği: Bazı İş Ortağı Merkezi API'leri için azaltma İş Ortağı Kiracı Kimliği tarafından belirlenir; aynı İş Ortağı Kiracı Kimliğinde bu API'lere yapılan çok fazla çağrı azaltma eşiğinin aşılır.</span><span class="sxs-lookup"><span data-stu-id="51f44-114">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="51f44-115">**Müşteri Kiracı Kimliği** başına İş Ortağı Kiracı Kimliği başına çok sayıda API isteği: Diğer API'ler için azaltma, İş Ortağı Kiracı Kimliği/Müşteri Kiracı Kimliği birleşimine göre belirlenir; Bu durumlarda, aynı müşteri kiracı kimliğine karşı çok fazla çağrı yapmak azaltmaya neden olurken diğer müşterilere yapılan çağrılar başarılı olabilir.</span><span class="sxs-lookup"><span data-stu-id="51f44-115">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="51f44-116">Azaltmayı önlemeye yönelik en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="51f44-116">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="51f44-117">Güncelleştirmeleri kontrol etmek için bir kaynağı sürekli yoklama ve yeni veya silinmiş kaynakları kontrol etmek için kaynak koleksiyonlarını düzenli olarak tarama gibi programlama uygulamaları, azaltmaya neden olabilir ve genel performansı düşürecektir.</span><span class="sxs-lookup"><span data-stu-id="51f44-117">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="51f44-118">Eşzamanlı API çağrıları, birim zamanı başına çok sayıda istekle karşılanabilecek ve isteklerin kısıtlanabilecek şekilde kısıtlanabilecek.</span><span class="sxs-lookup"><span data-stu-id="51f44-118">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="51f44-119">Bunun yerine değişiklik izleme ve değişiklik bildirimlerini kullan gerekir.</span><span class="sxs-lookup"><span data-stu-id="51f44-119">You should instead use change tracking and change notifications.</span></span> <span data-ttu-id="51f44-120">Ayrıca, değişiklikleri algılamak için etkinlik günlüklerini de kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="51f44-120">Additionally, you should be able to use activity logs for detecting changes.</span></span> <span data-ttu-id="51f44-121">Daha fazla bilgi için [bkz. İş Ortağı Merkezi günlüklerini görüntüleme.](get-a-record-of-partner-center-activity-by-user.md)</span><span class="sxs-lookup"><span data-stu-id="51f44-121">For more information, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md).</span></span>  <span data-ttu-id="51f44-122">İş ortaklarının daha fazla verimlilik ve azaltmayı önlemek için etkinlik günlüğü API'sini kullanmayı göz önünde bulundurmalarını kesinlikle öneririz.</span><span class="sxs-lookup"><span data-stu-id="51f44-122">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="51f44-123">Ayrıca aşağıdaki etkinlik günlüklerini kullanma örneğine de bakın.</span><span class="sxs-lookup"><span data-stu-id="51f44-123">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="51f44-124">Azaltmayı işlemek için en iyi yöntemler</span><span class="sxs-lookup"><span data-stu-id="51f44-124">Best practices to handle throttling</span></span>

<span data-ttu-id="51f44-125">Aşağıda, azaltmayı işlemeye yönelik en iyi yöntemler ve daha iyi yöntemler ve ardından yer alan uygulamalar ve daha fazla bilgi yer amaktadır:</span><span class="sxs-lookup"><span data-stu-id="51f44-125">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="51f44-126">Paralellik derecesini azaltma.</span><span class="sxs-lookup"><span data-stu-id="51f44-126">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="51f44-127">Çağrı sıklığını azaltma.</span><span class="sxs-lookup"><span data-stu-id="51f44-127">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="51f44-128">Tüm istekler kullanım sınırlarınıza göre tahakkuk etti olarak hemen yeniden denemelerden kaçının.</span><span class="sxs-lookup"><span data-stu-id="51f44-128">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="51f44-129">Hata işleme uyguladığınızda, azaltmayı algılamak için HTTP hata kodu 429’u kullanın.</span><span class="sxs-lookup"><span data-stu-id="51f44-129">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="51f44-130">Başarısız yanıt, yanıt üst Retry-After içerir.</span><span class="sxs-lookup"><span data-stu-id="51f44-130">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="51f44-131">Yeniden deneme sonrası gecikmeyi kullanarak istekleri geri almanın en hızlı yolu azaltmadan kurtarmaktır.</span><span class="sxs-lookup"><span data-stu-id="51f44-131">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="51f44-132">Yeniden deneme sonrası gecikmeyi kullanmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="51f44-132">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="51f44-133">Üst bilgisinde belirtilen saniye Retry-After bekleyin.</span><span class="sxs-lookup"><span data-stu-id="51f44-133">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="51f44-134">İsteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="51f44-134">Retry the request.</span></span>  

3. <span data-ttu-id="51f44-135">İstek 429 hata koduyla yeniden başarısız olursa, yine de kısıtlamaya devam edersiniz.</span><span class="sxs-lookup"><span data-stu-id="51f44-135">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="51f44-136">Üstel geri ödeme ile yeniden deneyin, önerilen gecikmeyi Retry-After ve başarılı olana kadar isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="51f44-136">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="51f44-137">SDK'yı kullanıyorsanız isteğiniz kısıtlanacaksa durum kodu 429 olan bir özel durum alırsınız.</span><span class="sxs-lookup"><span data-stu-id="51f44-137">If you are using the SDK, you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="51f44-138">Özel durum içinde RetryAfter özelliğini kullanın ve süre sonra isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="51f44-138">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="51f44-139">Şu anda azaltmadan etkilene API'ler</span><span class="sxs-lookup"><span data-stu-id="51f44-139">APIs currently impacted by throttling</span></span>

<span data-ttu-id="51f44-140">Sonunda, "İş Ortağı Merkezi" uç noktasını çağıran her api api.partnercenter.microsoft.com/ kısıtlar.</span><span class="sxs-lookup"><span data-stu-id="51f44-140">In the end, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="51f44-141">Şu anda azaltma sınırları yalnızca aşağıda listelenen API'lere uygulanır.</span><span class="sxs-lookup"><span data-stu-id="51f44-141">Currently, the throttling limits are only enforced on the APIs listed below.</span></span> <span data-ttu-id="51f44-142">İş Ortağı Merkezi API'lerden her biri için telemetri toplayarak azaltma sınırlarını dinamik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="51f44-142">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="51f44-143">Aşağıdaki tabloda azaltmanın şu anda zorlanan API'leri listele.</span><span class="sxs-lookup"><span data-stu-id="51f44-143">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="51f44-144">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="51f44-144">**Operation**</span></span>| <span data-ttu-id="51f44-145">**İş Ortağı Merkezi belgeleri**</span><span class="sxs-lookup"><span data-stu-id="51f44-145">**Partner Center documentation**</span></span>|
|------------------------|----------------------------|
|<span data-ttu-id="51f44-146">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="51f44-146">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="51f44-147">sipariş oluşturma</span><span class="sxs-lookup"><span data-stu-id="51f44-147">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="51f44-148">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span><span class="sxs-lookup"><span data-stu-id="51f44-148">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="51f44-149">aboneliği geçiş</span><span class="sxs-lookup"><span data-stu-id="51f44-149">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="51f44-150">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span><span class="sxs-lookup"><span data-stu-id="51f44-150">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="51f44-151">abonelik için eklenti satın alma</span><span class="sxs-lookup"><span data-stu-id="51f44-151">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="51f44-152">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="51f44-152">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="51f44-153">sepet oluşturma</span><span class="sxs-lookup"><span data-stu-id="51f44-153">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="51f44-154">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span><span class="sxs-lookup"><span data-stu-id="51f44-154">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="51f44-155">sepete göz at</span><span class="sxs-lookup"><span data-stu-id="51f44-155">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="51f44-156">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="51f44-156">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="51f44-157">sepeti güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="51f44-157">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="51f44-158">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span><span class="sxs-lookup"><span data-stu-id="51f44-158">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="51f44-159">aboneliği kaydetme</span><span class="sxs-lookup"><span data-stu-id="51f44-159">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="51f44-160">{baseURL}/v1/productupgrades</span><span class="sxs-lookup"><span data-stu-id="51f44-160">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="51f44-161">ürün yükseltme varlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="51f44-161">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="51f44-162">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="51f44-162">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="51f44-163">deneme aboneliğini ücretli aboneliğe dönüştürme</span><span class="sxs-lookup"><span data-stu-id="51f44-163">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="51f44-164">{baseURL}/v1/customers/{customer-tenant-id}</span><span class="sxs-lookup"><span data-stu-id="51f44-164">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="51f44-165">Kimliğine göre müşteri al</span><span class="sxs-lookup"><span data-stu-id="51f44-165">get a customer by ID</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="51f44-166">{baseURL}/v1/productUpgrades/uygunluk</span><span class="sxs-lookup"><span data-stu-id="51f44-166">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="51f44-167">ürün yükseltmesi için uygunluk elde etmek</span><span class="sxs-lookup"><span data-stu-id="51f44-167">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="51f44-168">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span><span class="sxs-lookup"><span data-stu-id="51f44-168">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="51f44-169">aboneliği yönetme</span><span class="sxs-lookup"><span data-stu-id="51f44-169">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="51f44-170">{baseURL}/v1/customers/{customer_id}/subscriptions</span><span class="sxs-lookup"><span data-stu-id="51f44-170">{baseURL}/v1/customers/{customer_id}/subscriptions</span></span> |[<span data-ttu-id="51f44-171">get-all-of-a-customer-s-subscriptions</span><span class="sxs-lookup"><span data-stu-id="51f44-171">get-all-of-a-customer-s-subscriptions</span></span>](get-all-of-a-customer-s-subscriptions.md)|
|<span data-ttu-id="51f44-172">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="51f44-172">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="51f44-173">Kimliğe göre bir abonelik alma</span><span class="sxs-lookup"><span data-stu-id="51f44-173">Get a subscription by ID</span></span>](get-a-subscription-by-id.md)|
|<span data-ttu-id="51f44-174">{baseURL}/v1/customers/{customer_id}/orders</span><span class="sxs-lookup"><span data-stu-id="51f44-174">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="51f44-175">Tüm müşteri siparişlerini alma</span><span class="sxs-lookup"><span data-stu-id="51f44-175">Get all customer orders</span></span>](get-all-of-a-customer-s-orders.md)|
|<span data-ttu-id="51f44-176">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span><span class="sxs-lookup"><span data-stu-id="51f44-176">{baseURL}/v1/customers/{customer_id}/orders/{order_id}</span></span>|[<span data-ttu-id="51f44-177">Kimliğe göre bir sipariş alma</span><span class="sxs-lookup"><span data-stu-id="51f44-177">Get an order by ID</span></span>](get-an-order-by-id.md)|
|<span data-ttu-id="51f44-178">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span><span class="sxs-lookup"><span data-stu-id="51f44-178">{baseURL}/v1/customers/{customer_id}/orders/{order_id}/provisioningstatus</span></span>|[<span data-ttu-id="51f44-179">Abonelik sağlama durumunu alma</span><span class="sxs-lookup"><span data-stu-id="51f44-179">Get subscription provisioning status</span></span>](get-subscription-provisioning-status.md)|
|<span data-ttu-id="51f44-180">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span><span class="sxs-lookup"><span data-stu-id="51f44-180">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}</span></span>|[<span data-ttu-id="51f44-181">Siparişleri yönetme ve aboneliği yönetme</span><span class="sxs-lookup"><span data-stu-id="51f44-181">Manage orders and manage a subscription</span></span>](manage-orders.md#manage-a-subscription)|
|<span data-ttu-id="51f44-182">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span><span class="sxs-lookup"><span data-stu-id="51f44-182">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/addons</span></span>|[<span data-ttu-id="51f44-183">Bir abonelik için eklentilerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="51f44-183">Get a list of add-ons for a subscription</span></span>](get-a-list-of-add-ons-for-a-subscription.md)|
|<span data-ttu-id="51f44-184">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span><span class="sxs-lookup"><span data-stu-id="51f44-184">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/azureEntitlements</span></span>|[<span data-ttu-id="51f44-185">Bir abonelik için Azure yetkilendirmelerinin listesini alma</span><span class="sxs-lookup"><span data-stu-id="51f44-185">Get a list of Azure entitlements for a subscription</span></span>](get-a-list-of-azure-entitlements-for-subscription.md)|
|<span data-ttu-id="51f44-186">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span><span class="sxs-lookup"><span data-stu-id="51f44-186">{baseURL}/v1/customers/{customer_id}/subscriptions/{subscription_id}/registrationstatus</span></span>|[<span data-ttu-id="51f44-187">Abonelik kayıt durumunu alma</span><span class="sxs-lookup"><span data-stu-id="51f44-187">Get subscription registration status</span></span>](get-subscription-registration-status.md)|
|<span data-ttu-id="51f44-188">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span><span class="sxs-lookup"><span data-stu-id="51f44-188">{baseURL}/v1/customers/{customer-tenant-id}/transfers</span></span>|[<span data-ttu-id="51f44-189">Müşterinin tüm aktarımlarını al</span><span class="sxs-lookup"><span data-stu-id="51f44-189">Get all of a customer's transfers</span></span>](get-all-of-a-customer-s-transfers.md)|
|<span data-ttu-id="51f44-190">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span><span class="sxs-lookup"><span data-stu-id="51f44-190">{baseURL}/v1/productUpgrades/{upgrade-id}/status</span></span>|[<span data-ttu-id="51f44-191">Ürün yükseltme durumunu alma</span><span class="sxs-lookup"><span data-stu-id="51f44-191">Get product upgrade status</span></span>](get-product-upgrade-status.md)|
|<span data-ttu-id="51f44-192">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span><span class="sxs-lookup"><span data-stu-id="51f44-192">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span>|[<span data-ttu-id="51f44-193">Deneme dönüştürme tekliflerinin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="51f44-193">Get a list of trial conversion offers</span></span>](get-a-list-of-trial-conversion-offers.md)|


### <a name="error-code-response"></a><span data-ttu-id="51f44-194">Hata kodu yanıtı:</span><span class="sxs-lookup"><span data-stu-id="51f44-194">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="51f44-195">Etkinlik günlüğü örneği</span><span class="sxs-lookup"><span data-stu-id="51f44-195">Example of activity log</span></span>

<span data-ttu-id="51f44-196">Günlük değişiklikleri analiz etmede en iyi yöntem olarak, denetim kaydını belirli bir gün için sorgulamayı öneririz.</span><span class="sxs-lookup"><span data-stu-id="51f44-196">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="51f44-197">Yanıtta, belirli bir işlem türüne yapılan değişikliklerle bir sonuç elde olur.</span><span class="sxs-lookup"><span data-stu-id="51f44-197">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="51f44-198">Filtreyi önemsersiniz işlemi temel alarak filtreleysiniz.</span><span class="sxs-lookup"><span data-stu-id="51f44-198">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="51f44-199">Örneğin, yeni oluşturulan bir müşteriyle ilgileniyorsanız operationType = "add_customer".</span><span class="sxs-lookup"><span data-stu-id="51f44-199"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="51f44-200">operationtype/resources listesi aşağıdaki API belgelerinden bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="51f44-200">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="51f44-201">Kaynakları denetleme</span><span class="sxs-lookup"><span data-stu-id="51f44-201">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="51f44-202">Kullanıcıya göre Iş Ortağı Merkezi etkinliğinin kaydını al</span><span class="sxs-lookup"><span data-stu-id="51f44-202">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="51f44-203">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="51f44-203">Response example</span></span>

<span data-ttu-id="51f44-204">**İstek**:</span><span class="sxs-lookup"><span data-stu-id="51f44-204">**Request**:</span></span>  
```http
Http Get call:  https://api.partnercenter.microsoft.com/v1/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50 

Authorization: Bearer <token> 

Accept: application/json 

MS-RequestId: 127facaa-e389-41f8-8bb7-1d1af99db893 

MS-CorrelationId: de9c2ccc-40dd-4186-9660-65b9b64c3d14 

X-Locale: en-US 

Host: api.partnercenter.microsoft.com 

Connection: Keep-Alive 
```

<span data-ttu-id="51f44-205">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="51f44-205">**Response**:</span></span>    
```http
{ 

    "totalCount": 17, 

    "items": [ 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_e905b566-4779-4e57-944c-7b1b5312705b_updatecustomeruserlicenses_637346859797753934", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "e905b566-4779-4e57-944c-7b1b5312705b", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "FulfillmentService", 

            "resourceType": "license", 

            "operationType": "update_customer_user_licenses", 

            "operationDate": "2020-09-02T23:26:19.7753934Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "CustomerUserId", 

                    "value": "933808c7-b165-496c-a24e-1a4b7846fab4" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

        { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_ia80zlkxp6ewoqpp35pbqjlhqv9iigvz1_createorder_637346662909268372", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "order", 

            "resourceNewValue": "{\"Id\":\"Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"AlternateId\":\"64144d300bde\",\"ReferenceCustomerId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"BillingCycle\":\"monthly\",\"CurrencyCode\":\"USD\",\"CurrencySymbol\":\"$\",\"LineItems\":[{\"LineItemNumber\":0,\"ProvisioningContext\":null,\"OfferId\":\"DZH318Z0C964:0001:DZH318Z0BZDG\",\"SubscriptionId\":\"f428d44a-d08b-348b-579e-ce92a6362c7b\",\"ParentSubscriptionId\":null,\"TermDuration\":\"P1M\",\"TransactionType\":\"New\",\"FriendlyName\":\"SaaS custom meter offer - Bronze\",\"Quantity\":1,\"Pricing\":null,\"PartnerIdOnRecord\":null,\"RenewsTo\":null,\"Links\":{\"Product\":{\"Uri\":\"/products/DZH318Z0C964?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Sku\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"Availability\":{\"Uri\":\"/products/DZH318Z0C964/skus/0001/availabilities/DZH318Z0BZDG?country=US\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ActivationLinks\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/lineitems/0/activationlinks\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}}}],\"CreationDate\":\"2020-09-02T17:58:01.7755853Z\",\"Status\":\"pending\",\"TransactionType\":\"UserPurchase\",\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"ProvisioningStatus\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1/provisioningstatus\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]},\"PatchOperation\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/orders/Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1\",\"Method\":\"PATCH\",\"Body\":null,\"Headers\":[]}},\"Client\":{\"marketplaceCountry\":\"US\",\"deviceFamily\":\"UniversalStore-PartnerCenter\",\"name\":\"Partner Center Web\"},\"Attributes\":{\"ObjectType\":\"Order\"}}", 

            "operationType": "create_order", 

            "originalCorrelationId": "96514ebe-c1b2-4865-cb46-2c2d20a2e911", 

            "operationDate": "2020-09-02T17:58:10.9268372Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "OrderId", 

                    "value": "Ia80ZLkXp6eWOqpp35pBQJLhqv9IiGVZ1" 

                }, 

                { 

                    "key": "AlternateId", 

                    "value": "64144d300bde" 

                }, 

                { 

                    "key": "BillingCycle", 

                    "value": "Monthly" 

                }, 

                { 

                    "key": "OfferId-0", 

                    "value": "DZH318Z0C964:0001:DZH318Z0BZDG" 

                }, 

                { 

                    "key": "SubscriptionId-0", 

                    "value": "f428d44a-d08b-348b-579e-ce92a6362c7b" 

                }, 

                { 

                    "key": "SubscriptionName-0", 

                    "value": "SaaS custom meter offer - Bronze" 

                }, 

                { 

                   "key": "Quantity-0", 

                    "value": "1" 

                }, 

                { 

                    "key": "PartnerOnRecord-0", 

                    "value": null 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                           { 

            "id": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d_86bddccf-9a53-40c6-907c-08067a3f8da7_86bddccf-9a53-40c6-907c-08067a3f8da7_addcustomer_637346648528069005", 

            "partnerId": "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d", 

            "participants": [ 

                "9daaeb1c-4195-4db5-9f1d-509eb70c8c2d" 

            ], 

            "customerId": "86bddccf-9a53-40c6-907c-08067a3f8da7", 

            "customerName": "CustomMetersStagingTest", 

            "userPrincipalName": "admin@testsw09.onmicrosoft.com", 

            "applicationId": "4990cffe-04e8-4e8b-808a-1175604b879f", 

            "resourceType": "customer", 

            "resourceNewValue": "{\"Id\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"CommerceId\":\"9dd78b4f-f98a-44b4-a2fa-2b82ac58d24c\",\"CompanyProfile\":{\"TenantId\":\"86bddccf-9a53-40c6-907c-08067a3f8da7\",\"Domain\":\"CustomMetersStagingTest.onmicrosoft.com\",\"CompanyName\":\"CustomMetersStagingTest\",\"Address\":null,\"Email\":null,\"OrganizationRegistrationNumber\":null,\"Links\":{\"Self\":{\"Uri\":\"/customers/86bddccf-9a53-40c6-907c-08067a3f8da7/profiles/company\",\"Method\":\"GET\",\"Body\":null,\"Headers\":[]}},\"Attributes\":{\"ObjectType\":\"CustomerCompanyProfile\"}},\"BillingProfile\":{\"Id\":\"4beafd7b-cdab-5bdc-52ed-02e16edf2e7a\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"Email\":\"CustomMetersStagingTest@CustomMetersStagingTest.com\",\"Culture\":\"en-US\",\"Language\":\"en\",\"CompanyName\":\"CustomMetersStagingTest\",\"DefaultAddress\":{\"Id\":null,\"Country\":\"US\",\"Region\":null,\"City\":\"Seattle\",\"State\":\"WA\",\"District\":null,\"AddressLine1\":\"CustomMetersStagingTest\",\"AddressLine2\":null,\"AddressLine3\":null,\"PostalCode\":\"98122\",\"FirstName\":\"CustomMetersStagingTest\",\"LastName\":\"CustomMetersStagingTest\",\"EmailAddress\":null,\"PhoneNumber\":null,\"MiddleName\":null},\"Attributes\":{\"Etag\":\"-2279334701316321663\",\"ObjectType\":\"CustomerBillingProfile\"}},\"RelationshipToPartner\":\"reseller\",\"AllowDelegatedAccess\":true,\"UserCredentials\":{\"userName\":\"admin\",\"password\":\"\"},\"AssociatedPartnerId\":null,\"CustomDomains\":null,\"Attributes\":{\"ObjectType\":\"Customer\"}}", 

            "operationType": "add_customer", 

            "originalCorrelationId": "7550d9ea-e64a-416f-e49b-3670c516cf69", 

            "operationDate": "2020-09-02T17:34:12.8069005Z", 

            "operationStatus": "succeeded", 

            "customizedData": [ 

                { 

                    "key": "PrimaryDomainName", 

                    "value": "CustomMetersStagingTest.onmicrosoft.com" 

                }, 

                { 

                    "key": "Relationship", 

                    "value": "Reseller" 

                } 

            ], 

            "attributes": { 

                "objectType": "AuditRecord" 

            } 

        }, 

                            

        ... 

    ], 

    "links": { 

        "self": { 

            "uri": "/auditrecords?startDate=2020-09-02&endDate=2020-09-02&size=50", 

            "method": "GET", 

            "headers": [] 

        } 

    }, 

    "attributes": { 

        "objectType": "Collection" 

    } 

} 
```
 

