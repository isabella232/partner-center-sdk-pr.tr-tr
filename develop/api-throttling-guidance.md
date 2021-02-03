---
title: API azaltma yönergeleri
description: Iş Ortağı Merkezi API 'Lerini çağıran iş ortakları için, hangi API 'Lerin Microsoft API daraltma ve en iyi uygulamalardan etkilendiğinin ve daha iyi bir şekilde azaltılmasını önlemek için
ms.date: 09/09/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: vijvala
ms.author: vijvala
ms.openlocfilehash: a52751a97e699050075c1aac910cc51e94514f26
ms.sourcegitcommit: 01e75175077611da92175c777a440a594fb05797
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/08/2020
ms.locfileid: "97770234"
---
# <a name="api-throttling-guidance-for-partners-calling-partner-center-apis"></a><span data-ttu-id="27136-103">Iş Ortağı Merkezi API 'Lerini çağıran iş ortakları için API azaltma Kılavuzu</span><span class="sxs-lookup"><span data-stu-id="27136-103">API throttling guidance for partners calling Partner Center APIs</span></span> 

<span data-ttu-id="27136-104">**Şunlara uygulanır**</span><span class="sxs-lookup"><span data-stu-id="27136-104">**Applies to**</span></span>

- <span data-ttu-id="27136-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="27136-105">Partner Center</span></span>

<span data-ttu-id="27136-106">Microsoft, Iş Ortağı Merkezi API 'Lerini çağıran iş ortakları için zaman dilimi içinde daha tutarlı performans sağlamak üzere API daraltma işlemi yapıyor.</span><span class="sxs-lookup"><span data-stu-id="27136-106">Microsoft is implementing API throttling to allow more consistent performance within a time span for partners calling the Partner Center APIs.</span></span> <span data-ttu-id="27136-107">Azaltma, kaynakların aşırı kullanımını engellemek için bir zaman dilimi içindeki bir hizmete yönelik isteklerin sayısını sınırlar.</span><span class="sxs-lookup"><span data-stu-id="27136-107">Throttling limits the number of requests to a service in a time span to prevent overuse of resources.</span></span> <span data-ttu-id="27136-108">Iş ortağı merkezi yüksek bir istek hacmi işleyecek şekilde tasarlandığından, birkaç iş ortağı tarafından çok sayıda istek oluşursa, azaltma işlemi tüm iş ortakları için en iyi performansı ve güvenilirliği korumanıza yardımcı olur.</span><span class="sxs-lookup"><span data-stu-id="27136-108">While Partner Center is designed to handle a high volume of requests, if an overwhelming number of requests occur by few partners, throttling helps maintain optimal performance and reliability for all partners.</span></span>  

<span data-ttu-id="27136-109">Azaltma limitleri senaryoya göre farklılık gösterir.</span><span class="sxs-lookup"><span data-stu-id="27136-109">Throttling limits vary based on the scenario.</span></span> <span data-ttu-id="27136-110">Örneğin, büyük bir yazma hacmi gerçekleştiriyorsanız, yalnızca okuma işlemi gerçekleştirmekten daha yüksektir.</span><span class="sxs-lookup"><span data-stu-id="27136-110">For example, if you are performing a large volume of writes, the possibility for throttling is higher than if you are only performing reads.</span></span>

## <a name="what-happens-when-throttling-occurs"></a><span data-ttu-id="27136-111">Kısıtlama gerçekleştiğinde ne olur?</span><span class="sxs-lookup"><span data-stu-id="27136-111">What happens when throttling occurs?</span></span> 

<span data-ttu-id="27136-112">Bir azaltma eşiği aşıldığında, Iş ortağı merkezi bir süre için o istemciden gelen diğer istekleri sınırlandırır.</span><span class="sxs-lookup"><span data-stu-id="27136-112">When a throttling threshold is exceeded, Partner Center limits any further requests from that client for a period of time.</span></span> <span data-ttu-id="27136-113">Kısıtlama davranışı, istek türüne ve sayısına bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="27136-113">Throttling behavior depends on the type and number of requests.</span></span>   

### <a name="common-throttling-scenarios"></a><span data-ttu-id="27136-114">Yaygın kısıtlama senaryoları</span><span class="sxs-lookup"><span data-stu-id="27136-114">Common throttling scenarios</span></span> 

<span data-ttu-id="27136-115">İstemcilerin azaltmasının en yaygın nedenleri şunlardır:</span><span class="sxs-lookup"><span data-stu-id="27136-115">The most common causes of throttling of clients include:</span></span> 

- <span data-ttu-id="27136-116">**BIR API Için Iş ortağı KIRACı kimliği başına çok sayıda istek** vardır: bazı Iş Ortağı Merkezi API 'leri Için azaltma Iş ortağı kiracı kimliğine göre belirlenir, aynı Iş ortağı kiracı kimliğinde bu API 'lere çok fazla çağrı azaltma eşiğini aşarak sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="27136-116">**A large number of requests for an API per Partner Tenant ID**: for some Partner Center APIs, throttling is determined by Partner Tenant ID, too many calls to those APIs on the same Partner Tenant ID will result in exceeding the throttling threshold.</span></span>  

- <span data-ttu-id="27136-117">Her **Müşteri KIRACı kimliği Için Iş ortağı KIRACı kimliği başına BIR API için çok sayıda istek** vardır: diğer API 'ler için, azaltma Iş ortağı Kiracı kimliği/MÜŞTERI Kiracı kimliği birleşimine göre belirlenir; Bu durumlarda, aynı müşteri kiracı KIMLIĞINE karşı çok fazla çağrı yapmak, diğer müşterilerle yapılan çağrıların başarılı olabileceği azaltma ile sonuçlanır.</span><span class="sxs-lookup"><span data-stu-id="27136-117">**A large number of requests for an API per Partner Tenant ID per Customer Tenant ID**: for other APIs, throttling is determined by Partner Tenant ID/Customer Tenant ID combination; in those cases, making too many calls against the same customer tenant ID will result in throttling - while calls against other customers may succeed.</span></span>

## <a name="best-practices-to-avoid-throttling"></a><span data-ttu-id="27136-118">Azaltmayı önlemek için en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="27136-118">Best practices to avoid throttling</span></span> 
 
<span data-ttu-id="27136-119">Güncelleştirmeleri denetlemek için bir kaynağı sürekli yoklamak ve yeni veya silinmiş kaynakları denetlemek için düzenli olarak kaynak koleksiyonlarını taramak, azaltmaya neden olabilir ve genel performansı düşürür.</span><span class="sxs-lookup"><span data-stu-id="27136-119">Programming practices such as continuously polling a resource to check for updates and regularly scanning resource collections to check for new or deleted resources are more likely to lead to throttling and will degrade overall performance.</span></span> <span data-ttu-id="27136-120">Eşzamanlı API çağrıları, birim zamanı başına yüksek sayıda isteğe yol açabilir, bu da isteklerin kısıtlanmasına neden olur.</span><span class="sxs-lookup"><span data-stu-id="27136-120">Concurrent API calls may lead to high number of requests per unit time, which will also cause requests to be throttled.</span></span> <span data-ttu-id="27136-121">Bunun yerine değişiklik izleme ve değişiklik bildirimleri özelliğinden yararlanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27136-121">You should instead leverage change tracking and change notifications.</span></span> <span data-ttu-id="27136-122">Ayrıca, değişiklikleri algılamak için etkinlik günlüklerinden yararlanabilirsiniz, daha fazla bilgi için bkz. [Iş ortağı merkezi etkinlik günlükleri](get-a-record-of-partner-center-activity-by-user.md) .</span><span class="sxs-lookup"><span data-stu-id="27136-122">Additionally, you should be able to leverage activity logs for detecting changes, see [Partner Center activity logs](get-a-record-of-partner-center-activity-by-user.md) for more information.</span></span>  <span data-ttu-id="27136-123">İş ortaklarının, daha fazla verimlilik için etkinlik günlüğü API 'sini kullanmayı ve azaltmasını önlemek için kullanılması önerilir.</span><span class="sxs-lookup"><span data-stu-id="27136-123">We highly recommend partners to consider using the activity log API for more efficiency and to avoid throttling.</span></span> <span data-ttu-id="27136-124">Ayrıca aşağıdaki etkinlik günlüklerini kullanma örneğine bakın.</span><span class="sxs-lookup"><span data-stu-id="27136-124">See also the example of using activity logs, below.</span></span>

## <a name="best-practices-to-handle-throttling"></a><span data-ttu-id="27136-125">Azaltmayı işlemek için en iyi uygulamalar</span><span class="sxs-lookup"><span data-stu-id="27136-125">Best practices to handle throttling</span></span>

<span data-ttu-id="27136-126">Azaltma işlemi için en iyi uygulamalar şunlardır:</span><span class="sxs-lookup"><span data-stu-id="27136-126">The following are best practices for handling throttling:</span></span> 

- <span data-ttu-id="27136-127">Paralellik derecesini azaltın.</span><span class="sxs-lookup"><span data-stu-id="27136-127">Reduce the degree of parallelism.</span></span> 
- <span data-ttu-id="27136-128">Çağrıların sıklığını azaltın.</span><span class="sxs-lookup"><span data-stu-id="27136-128">Reduce the frequency of calls.</span></span> 
- <span data-ttu-id="27136-129">Tüm istekler kullanım sınırlarınıza göre tahakkuk ettiğinden anında denemeler yapmaktan kaçının.</span><span class="sxs-lookup"><span data-stu-id="27136-129">Avoid immediate retries because all requests accrue against your usage limits.</span></span> 

<span data-ttu-id="27136-130">Hata işleme uyguladığınızda, azaltmayı algılamak için HTTP hata kodu 429’u kullanın.</span><span class="sxs-lookup"><span data-stu-id="27136-130">When you implement error handling, use the HTTP error code 429 to detect throttling.</span></span> <span data-ttu-id="27136-131">Başarısız yanıt Retry-After yanıt üst bilgisini içerir.</span><span class="sxs-lookup"><span data-stu-id="27136-131">The failed response includes the Retry-After response header.</span></span> <span data-ttu-id="27136-132">Yeniden deneme-sonrası gecikmesini kullanarak istekleri kapatmak, azaltmayı kurtarmanın en hızlı yoludur.</span><span class="sxs-lookup"><span data-stu-id="27136-132">Backing off requests using the Retry-after delay is the fastest way to recover from throttling.</span></span> 

<span data-ttu-id="27136-133">Retry-After gecikmesini kullanmak için şunları yapın:</span><span class="sxs-lookup"><span data-stu-id="27136-133">To use the Retry-after delay, do the following:</span></span> 

1. <span data-ttu-id="27136-134">Retry-After üstbilgisinde belirtilen saniye sayısını bekleyin.</span><span class="sxs-lookup"><span data-stu-id="27136-134">Wait the number of seconds specified in the Retry-After header.</span></span> 

2. <span data-ttu-id="27136-135">İsteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="27136-135">Retry the request.</span></span>  

3. <span data-ttu-id="27136-136">İstek bir 429 hata koduyla yeniden başarısız olursa, hala kısıtlanıyor olursunuz.</span><span class="sxs-lookup"><span data-stu-id="27136-136">If the request fails again with a 429 error code, you are still being throttled.</span></span> <span data-ttu-id="27136-137">Üstel geri alma ile yeniden deneyin, önerilen Retry-After gecikmesini kullanın ve başarılı olana kadar isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="27136-137">Retry with Exponential backoff, use the recommended Retry-After delay and retry the request until it succeeds.</span></span>

4. <span data-ttu-id="27136-138">SDK kullanıyorsanız, isteğiniz kısıtlandığınızda 429 durum koduyla bir özel durum alırsınız.</span><span class="sxs-lookup"><span data-stu-id="27136-138">If you are using SDK you'll receive an exception with status code 429 when your request is being throttled.</span></span> <span data-ttu-id="27136-139">Özel durumda RetryAfter özelliğini kullanın ve zaman geçtikten sonra isteği yeniden deneyin.</span><span class="sxs-lookup"><span data-stu-id="27136-139">Use the RetryAfter property in the exception and retry the request after the time is elapsed.</span></span>


## <a name="apis-currently-impacted-by-throttling"></a><span data-ttu-id="27136-140">Daraltma tarafından şu anda etkilenen API 'Ler</span><span class="sxs-lookup"><span data-stu-id="27136-140">APIs currently impacted by throttling</span></span>

<span data-ttu-id="27136-141">Uzun çalıştırmada, "api.partnercenter.microsoft.com/" uç noktasını çağıran her tek Iş Ortağı Merkezi API 'SI kısıtlanacak.</span><span class="sxs-lookup"><span data-stu-id="27136-141">In the long run, every single Partner Center API that calls the endpoint “api.partnercenter.microsoft.com/” will be throttled.</span></span> <span data-ttu-id="27136-142">Şu anda azaltma sınırları yalnızca aşağıda listelenen birkaç API üzerinde zorlanır.</span><span class="sxs-lookup"><span data-stu-id="27136-142">Currently, the throttling limits are only enforced on the few APIs listed below.</span></span> <span data-ttu-id="27136-143">İş Ortağı Merkezi, her API için telemetri toplar ve azaltma sınırlarını dinamik olarak ayarlar.</span><span class="sxs-lookup"><span data-stu-id="27136-143">Partner Center will be collecting the telemetry on each of the APIs and will dynamically adjust the throttling limits.</span></span> <span data-ttu-id="27136-144">Aşağıdaki tabloda, azaltma 'nın Şu anda zorlandığı API 'Ler listelenmektedir.</span><span class="sxs-lookup"><span data-stu-id="27136-144">The following table lists the APIs where throttling is currently enforced.</span></span>  


|<span data-ttu-id="27136-145">**İşlem**</span><span class="sxs-lookup"><span data-stu-id="27136-145">**Operation**</span></span>| <span data-ttu-id="27136-146">**İş Ortağı Merkezi belgeleri**</span><span class="sxs-lookup"><span data-stu-id="27136-146">**Partner Center documentation**</span></span>|       
|------------------------|----------------------------|
|<span data-ttu-id="27136-147">{baseURL}/v1/Customers/{customer_id}/Orders</span><span class="sxs-lookup"><span data-stu-id="27136-147">{baseURL}/v1/customers/{customer_id}/orders</span></span>|[<span data-ttu-id="27136-148">sipariş oluşturma</span><span class="sxs-lookup"><span data-stu-id="27136-148">create an order</span></span>](create-an-order.md)|
|<span data-ttu-id="27136-149">{baseURL}/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}/yükseltmeler</span><span class="sxs-lookup"><span data-stu-id="27136-149">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}/upgrades</span></span>|[<span data-ttu-id="27136-150">abonelik geçişi</span><span class="sxs-lookup"><span data-stu-id="27136-150">transition a subscription</span></span>](transition-a-subscription.md)|
|<span data-ttu-id="27136-151">{baseURL}/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID}</span><span class="sxs-lookup"><span data-stu-id="27136-151">{baseURL}/v1/customers/{customer-tenant-id}/orders/{order-id}</span></span>|[<span data-ttu-id="27136-152">bir aboneliğe eklenti satın alma</span><span class="sxs-lookup"><span data-stu-id="27136-152">purchase an addon to a subscription</span></span>](purchase-an-add-on-to-a-subscription.md)|
|<span data-ttu-id="27136-153">{baseURL}/v1/Customers/{Customer-id}/Carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="27136-153">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="27136-154">sepet oluşturma</span><span class="sxs-lookup"><span data-stu-id="27136-154">create a cart</span></span>](create-a-cart.md)|
|<span data-ttu-id="27136-155">{baseURL}/v1/Customers/{Customer-id}/Carts/{cart-id}/Checkout</span><span class="sxs-lookup"><span data-stu-id="27136-155">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}/checkout</span></span>|[<span data-ttu-id="27136-156">sepet kullanıma alma</span><span class="sxs-lookup"><span data-stu-id="27136-156">checkout a cart</span></span>](checkout-a-cart.md)|
|<span data-ttu-id="27136-157">{baseURL}/v1/Customers/{Customer-id}/Carts/{cart-id}</span><span class="sxs-lookup"><span data-stu-id="27136-157">{baseURL}/v1/customers/{customer-id}/carts/{cart-id}</span></span>|[<span data-ttu-id="27136-158">sepetini güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="27136-158">update a cart</span></span>](update-a-cart.md)|
|<span data-ttu-id="27136-159">{baseURL}/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/kayıtları</span><span class="sxs-lookup"><span data-stu-id="27136-159">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/registrations</span></span>|[<span data-ttu-id="27136-160">abonelik kaydetme</span><span class="sxs-lookup"><span data-stu-id="27136-160">register a subscription</span></span>](register-a-subscription.md)|
|<span data-ttu-id="27136-161">{baseURL}/v1/productyükseltmeleri</span><span class="sxs-lookup"><span data-stu-id="27136-161">{baseURL}/v1/productupgrades</span></span>|[<span data-ttu-id="27136-162">ürün yükseltme varlığı oluştur</span><span class="sxs-lookup"><span data-stu-id="27136-162">create product upgrade entity</span></span>](create-product-upgrade-entity.md)|
|<span data-ttu-id="27136-163">{baseURL}/v1/Customers/{Customer-id}/Subscriptions/{Subscription-ID}/dönüşümler</span><span class="sxs-lookup"><span data-stu-id="27136-163">{baseURL}/v1/customers/{customer-id}/subscriptions/{subscription-id}/conversions</span></span> |[<span data-ttu-id="27136-164">deneme aboneliğini ücretli olarak dönüştürme</span><span class="sxs-lookup"><span data-stu-id="27136-164">convert a trial subscription to paid</span></span>](convert-a-trial-subscription-to-paid.md)|
|<span data-ttu-id="27136-165">{baseURL}/v1/Customers/{Customer-Tenant-ID}</span><span class="sxs-lookup"><span data-stu-id="27136-165">{baseURL}/v1/customers/{customer-tenant-id}</span></span>|[<span data-ttu-id="27136-166">kimliğe göre müşteri al</span><span class="sxs-lookup"><span data-stu-id="27136-166">get a customer by id</span></span>](get-a-customer-by-id.md)|
|<span data-ttu-id="27136-167">{baseURL}/v1/productupgrades/uygunluk</span><span class="sxs-lookup"><span data-stu-id="27136-167">{baseURL}/v1/productUpgrades/eligibility</span></span>|[<span data-ttu-id="27136-168">ürün yükseltmesine uygunluk sağlayın</span><span class="sxs-lookup"><span data-stu-id="27136-168">get eligibility for product upgrade</span></span>](get-eligibility-for-product-upgrade.md)|
|<span data-ttu-id="27136-169">{baseURL}/v1/Customers/{Customer-Tenant-ID}/Subscriptions/{ID-for-Subscription}</span><span class="sxs-lookup"><span data-stu-id="27136-169">{baseURL}/v1/customers/{customer-tenant-id}/subscriptions/{id-for-subscription}</span></span> |[<span data-ttu-id="27136-170">aboneliği Yönet</span><span class="sxs-lookup"><span data-stu-id="27136-170">manage subscription</span></span>](manage-orders.md#manage-a-subscription)|


### <a name="error-code-response"></a><span data-ttu-id="27136-171">Hata kodu yanıtı:</span><span class="sxs-lookup"><span data-stu-id="27136-171">Error code response:</span></span>
```http
HTTP/1.1 429 Too Many Requests 

Content-Length: 84 

Content-Type: application/json 

Retry-After: 57 

Date: Tue, 21 Jul 2020 04:10:58 GMT 

{ "statusCode": 429, "message": "Rate limit is exceeded. Try again in 57 seconds." } 
```

## <a name="example-of-activity-log"></a><span data-ttu-id="27136-172">Etkinlik günlüğü örneği</span><span class="sxs-lookup"><span data-stu-id="27136-172">Example of activity log</span></span>

<span data-ttu-id="27136-173">Günlük değişiklikleri çözümlemede en iyi yöntem için, belirli bir gün için denetim kaydını sorgulamanızı öneririz.</span><span class="sxs-lookup"><span data-stu-id="27136-173">For best practice in analyzing daily changes, we recommend that you query audit record for a specific day.</span></span> 

<span data-ttu-id="27136-174">Yanıtta, belirli işlem türünde değişikliklerle bir sonuç alacaksınız.</span><span class="sxs-lookup"><span data-stu-id="27136-174">In the response, you will get a result with changes to specific operation type.</span></span><span data-ttu-id="27136-175">İlgilendiğiniz işleme göre filtreleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27136-175">  You can filter based on the operation you care about.</span></span> <span data-ttu-id="27136-176">Örneğin, yeni oluşturulan bir müşteriyle ilgileniyorsanız, operationType = "add_customer" adresinden bakabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="27136-176"> For example, if you are interested in a newly created customer, you can look at operationType = “add_customer”.</span></span>  

<span data-ttu-id="27136-177">OperationType/Resources listesi aşağıdaki API belgeleri altında bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="27136-177">List of operationtype/resources can be found in below API docs.</span></span>  

- [<span data-ttu-id="27136-178">Kaynakları denetleme</span><span class="sxs-lookup"><span data-stu-id="27136-178">Auditing resources</span></span>](auditing-resources.md)  

- [<span data-ttu-id="27136-179">Kullanıcıya göre Iş Ortağı Merkezi etkinliğinin kaydını al</span><span class="sxs-lookup"><span data-stu-id="27136-179">Get a record of a Partner Center activity by user</span></span>](get-a-record-of-partner-center-activity-by-user.md)  



### <a name="response-example"></a><span data-ttu-id="27136-180">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="27136-180">Response example</span></span>

<span data-ttu-id="27136-181">**İstek**:</span><span class="sxs-lookup"><span data-stu-id="27136-181">**Request**:</span></span>  
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

<span data-ttu-id="27136-182">**Yanıt**:</span><span class="sxs-lookup"><span data-stu-id="27136-182">**Response**:</span></span>    
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
 

