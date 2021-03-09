---
title: Fatura faturalanmamış ticari tüketim satırı öğelerini Al
description: Iş Ortağı Merkezi API 'Lerini kullanarak belirli bir faturaya ait faturalandırılmamış ticari tüketim çizgisi öğe ayrıntılarının bir koleksiyonunu alabilirsiniz.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8d3bbe7921029dc6c40c65fb8d82baaa944089b6
ms.sourcegitcommit: 160296667833366fb3f4021d042094606e1032ec
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 03/09/2021
ms.locfileid: "102472691"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="cc395-103">Fatura faturalanmamış ticari tüketim satırı öğelerini Al</span><span class="sxs-lookup"><span data-stu-id="cc395-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="cc395-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="cc395-104">**Applies to:**</span></span>

- <span data-ttu-id="cc395-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="cc395-105">Partner Center</span></span>

<span data-ttu-id="cc395-106">Faturalandırılmamış ticari tüketim satırı öğe ayrıntılarının koleksiyonunu alma.</span><span class="sxs-lookup"><span data-stu-id="cc395-106">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="cc395-107">Ayrıca, faturalandırılmamış ticari tüketim çizgisi öğelerinin (açık kullanım satırı öğeleri olarak da bilinir) programlı bir şekilde ayrıntılarını almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="cc395-107">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="cc395-108">Günlük olarak derecelendirilen kullanımlar, Iş Ortağı Merkezi 'nde veya API aracılığıyla erişilecek 24 saat sürer.</span><span class="sxs-lookup"><span data-stu-id="cc395-108">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cc395-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="cc395-109">Prerequisites</span></span>

- <span data-ttu-id="cc395-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="cc395-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="cc395-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="cc395-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="cc395-112">Bir fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="cc395-112">An invoice identifier.</span></span> <span data-ttu-id="cc395-113">Bu, satır öğelerinin alınacağı faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="cc395-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="cc395-114">C\#</span><span class="sxs-lookup"><span data-stu-id="cc395-114">C\#</span></span>

<span data-ttu-id="cc395-115">Belirtilen faturaya ait satır öğelerini almak için:</span><span class="sxs-lookup"><span data-stu-id="cc395-115">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="cc395-116">Belirtilen faturaya yönelik işlemleri faturalamak için bir arabirim almak üzere [**Byıd**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="cc395-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="cc395-117">Fatura nesnesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="cc395-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="cc395-118">**Fatura nesnesi** belirtilen faturaya ait tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="cc395-118">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="cc395-119">**Sağlayıcı** , faturalandırılmamış ayrıntı bilgisinin kaynağını tanımlar (örneğin, **Onetime**).</span><span class="sxs-lookup"><span data-stu-id="cc395-119">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="cc395-120">**Invoineıtemtype** türü belirtir (örneğin, **Usagelineitem**).</span><span class="sxs-lookup"><span data-stu-id="cc395-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="cc395-121">Aşağıdaki örnek kod, **ınvogıtems** koleksiyonunu işlemek için bir **foreach** döngüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="cc395-121">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="cc395-122">Her bir **Faturaöğeside** her bir faturaya ait ayrı bir satır öğesi koleksiyonu alınır.</span><span class="sxs-lookup"><span data-stu-id="cc395-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="cc395-123">Bir **InvoiceDetail** örneğine karşılık gelen satır öğelerinin bir koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="cc395-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="cc395-124">Örneğe ait **Billingprovider** ve **ınvoineıtemtype** 'ı [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="cc395-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="cc395-125">İlişkili satır öğelerini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="cc395-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="cc395-126">Aşağıdaki örnekte gösterildiği gibi koleksiyonun çapraz geçişini yapmak için bir Numaralandırıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="cc395-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type DailyRatedUsageLineItem
        if (item is DailyRatedUsageLineItem)
        {
            Type t = typeof(DailyRatedUsageLineItem);
            PropertyInfo[] properties = t.GetProperties();

            foreach (PropertyInfo property in properties)
            {
                // Insert code here to work with the line item properties
            }
        }
        itemNumber++;
    });

    Console.Out.WriteLine("\tPress any key to fetch next data. Press the Escape (Esc) key to quit: \n");
    keyInfo = Console.ReadKey();

    if (keyInfo.Key == ConsoleKey.Escape)
    {
        break;
    }

    fetchNext = !string.IsNullOrWhiteSpace(seekBasedResourceCollection.ContinuationToken);

    if (fetchNext)
    {
        if (seekBasedResourceCollection.Links.Next.Headers != null && seekBasedResourceCollection.Links.Next.Headers.Any())
        {
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="cc395-127">Benzer bir örnek için bkz.:</span><span class="sxs-lookup"><span data-stu-id="cc395-127">For a similar example, see:</span></span>

- <span data-ttu-id="cc395-128">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="cc395-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="cc395-129">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="cc395-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="cc395-130">Sınıf: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="cc395-130">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="cc395-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="cc395-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="cc395-132">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="cc395-132">Request syntax</span></span>

<span data-ttu-id="cc395-133">Kullanım durumunuza bağlı olarak REST isteğiniz için aşağıdaki sözdizimleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="cc395-133">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="cc395-134">Daha fazla bilgi için her bir sözdizimi için açıklamalara bakın.</span><span class="sxs-lookup"><span data-stu-id="cc395-134">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="cc395-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="cc395-135">Method</span></span>  | <span data-ttu-id="cc395-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="cc395-136">Request URI</span></span>         | <span data-ttu-id="cc395-137">Sözdizimi kullanım durumunun açıklaması</span><span class="sxs-lookup"><span data-stu-id="cc395-137">Description of syntax use case</span></span> |                                                                                                                                            |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="cc395-138">**Al**</span><span class="sxs-lookup"><span data-stu-id="cc395-138">**GET**</span></span> | <span data-ttu-id="cc395-139">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturaın/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &period = {PERIOD} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cc395-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="cc395-140">Verilen faturaya ait her satır öğesinin tam listesini döndürmek için bu sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc395-140">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="cc395-141">**Al**</span><span class="sxs-lookup"><span data-stu-id="cc395-141">**GET**</span></span> | <span data-ttu-id="cc395-142">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &süre = {period} &boyut = {SIZE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="cc395-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="cc395-143">Büyük faturalar için bu sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc395-143">Use this syntax for large invoices.</span></span> <span data-ttu-id="cc395-144">Satır öğelerinin disk belleğine alınmış bir listesini döndürmek için bu söz dizimini belirtilen boyut ve 0 tabanlı bir uzaklığa göre kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc395-144">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="cc395-145">**Al**</span><span class="sxs-lookup"><span data-stu-id="cc395-145">**GET**</span></span> | <span data-ttu-id="cc395-146">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &period = {period} &boyut = {size} &Seekoperation = ileri</span><span class="sxs-lookup"><span data-stu-id="cc395-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="cc395-147">Kullanılarak mutabakat satır öğelerinin sonraki sayfasını almak için bu sözdizimini kullanın `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="cc395-147">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="cc395-148">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="cc395-148">URI parameters</span></span>

<span data-ttu-id="cc395-149">İsteği oluştururken aşağıdaki URI ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc395-149">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="cc395-150">Ad</span><span class="sxs-lookup"><span data-stu-id="cc395-150">Name</span></span>                   | <span data-ttu-id="cc395-151">Tür</span><span class="sxs-lookup"><span data-stu-id="cc395-151">Type</span></span>   | <span data-ttu-id="cc395-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="cc395-152">Required</span></span> | <span data-ttu-id="cc395-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="cc395-153">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="cc395-154">sağlayıcısını</span><span class="sxs-lookup"><span data-stu-id="cc395-154">provider</span></span>               | <span data-ttu-id="cc395-155">string</span><span class="sxs-lookup"><span data-stu-id="cc395-155">string</span></span> | <span data-ttu-id="cc395-156">Yes</span><span class="sxs-lookup"><span data-stu-id="cc395-156">Yes</span></span>      | <span data-ttu-id="cc395-157">Sağlayıcı: "**Onetime**".</span><span class="sxs-lookup"><span data-stu-id="cc395-157">The provider: "**OneTime**".</span></span>                                                |
| <span data-ttu-id="cc395-158">fatura-satır-öğe türü</span><span class="sxs-lookup"><span data-stu-id="cc395-158">invoice-line-item-type</span></span> | <span data-ttu-id="cc395-159">string</span><span class="sxs-lookup"><span data-stu-id="cc395-159">string</span></span> | <span data-ttu-id="cc395-160">Yes</span><span class="sxs-lookup"><span data-stu-id="cc395-160">Yes</span></span>      | <span data-ttu-id="cc395-161">Fatura ayrıntısı türü: "**Usagelineıtems**", "**usagelineıtems**".</span><span class="sxs-lookup"><span data-stu-id="cc395-161">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>               |
| <span data-ttu-id="cc395-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="cc395-162">currencyCode</span></span>           | <span data-ttu-id="cc395-163">string</span><span class="sxs-lookup"><span data-stu-id="cc395-163">string</span></span> | <span data-ttu-id="cc395-164">Yes</span><span class="sxs-lookup"><span data-stu-id="cc395-164">Yes</span></span>      | <span data-ttu-id="cc395-165">Faturalandırılmamış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="cc395-165">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="cc395-166">dönem</span><span class="sxs-lookup"><span data-stu-id="cc395-166">period</span></span>                 | <span data-ttu-id="cc395-167">string</span><span class="sxs-lookup"><span data-stu-id="cc395-167">string</span></span> | <span data-ttu-id="cc395-168">Yes</span><span class="sxs-lookup"><span data-stu-id="cc395-168">Yes</span></span>      | <span data-ttu-id="cc395-169">Faturalandırılmamış keşfi için süre (örneğin: **geçerli**, **önceki**).</span><span class="sxs-lookup"><span data-stu-id="cc395-169">The period for unbilled recon (for example: **current**, **previous**).</span></span> <span data-ttu-id="cc395-170">Fatura döngüsünün faturalandırılmamış kullanım verilerini (01/01/2020 – 01/31/2020), Ocak ayında **"geçerli,"** diğer **"önceki** " olarak seçin.</span><span class="sxs-lookup"><span data-stu-id="cc395-170">Suppose you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) in January, choose period as **“Current,”** else **“Previous.”**</span></span> |
| <span data-ttu-id="cc395-171">boyut</span><span class="sxs-lookup"><span data-stu-id="cc395-171">size</span></span>                   | <span data-ttu-id="cc395-172">sayı</span><span class="sxs-lookup"><span data-stu-id="cc395-172">number</span></span> | <span data-ttu-id="cc395-173">Hayır</span><span class="sxs-lookup"><span data-stu-id="cc395-173">No</span></span>       | <span data-ttu-id="cc395-174">Döndürülecek en fazla öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="cc395-174">The maximum number of items to return.</span></span> <span data-ttu-id="cc395-175">Varsayılan boyut 2000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="cc395-175">The default size is 2000.</span></span>                    |
| <span data-ttu-id="cc395-176">seekOperation</span><span class="sxs-lookup"><span data-stu-id="cc395-176">seekOperation</span></span>          | <span data-ttu-id="cc395-177">dize</span><span class="sxs-lookup"><span data-stu-id="cc395-177">string</span></span> | <span data-ttu-id="cc395-178">No</span><span class="sxs-lookup"><span data-stu-id="cc395-178">No</span></span>       | <span data-ttu-id="cc395-179">`seekOperation=Next`Mutabakat satır öğelerinin sonraki sayfasını almak için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="cc395-179">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="cc395-180">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="cc395-180">Request headers</span></span>

<span data-ttu-id="cc395-181">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="cc395-181">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="cc395-182">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="cc395-182">Request body</span></span>

<span data-ttu-id="cc395-183">Yok.</span><span class="sxs-lookup"><span data-stu-id="cc395-183">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="cc395-184">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="cc395-184">REST response</span></span>

<span data-ttu-id="cc395-185">Başarılı olursa, yanıt satır öğesi ayrıntıları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="cc395-185">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="cc395-186">*Satır **öğesi için**, **satın alma** değeri **Yeni** ile eşlenir ve değer **iadesi** **iptal** edilecek şekilde eşlenir.*</span><span class="sxs-lookup"><span data-stu-id="cc395-186">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="cc395-187">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="cc395-187">Response success and error codes</span></span>

<span data-ttu-id="cc395-188">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="cc395-188">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="cc395-189">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="cc395-189">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="cc395-190">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="cc395-190">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="cc395-191">İstek-yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="cc395-191">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="cc395-192">İstek-yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="cc395-192">Request-response example 1</span></span>

<span data-ttu-id="cc395-193">Aşağıdaki ayrıntılar Bu örnek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="cc395-193">The following details apply to this example:</span></span>

- <span data-ttu-id="cc395-194">**Sağlayıcı**: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="cc395-194">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="cc395-195">**Faturaışgıtemtype**: **usagelineıtems**</span><span class="sxs-lookup"><span data-stu-id="cc395-195">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="cc395-196">**Dönem**: **önceki**</span><span class="sxs-lookup"><span data-stu-id="cc395-196">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="cc395-197">İstek örneği 1</span><span class="sxs-lookup"><span data-stu-id="cc395-197">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

### <a name="response-example-1"></a><span data-ttu-id="cc395-198">Yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="cc395-198">Response example 1</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 2,
    "items": [
        {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-01T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "1234547f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
         },
         {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d12345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
            "method": "GET",
            "headers": [
                {
                    "key": "MS-ContinuationToken",
                    "value": "AQAAAA=="
                }
            ]
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

### <a name="request-response-example-2"></a><span data-ttu-id="cc395-199">İstek-yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="cc395-199">Request-response example 2</span></span>

<span data-ttu-id="cc395-200">Aşağıdaki ayrıntılar Bu örnek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="cc395-200">The following details apply to this example:</span></span>

- <span data-ttu-id="cc395-201">**Sağlayıcı**: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="cc395-201">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="cc395-202">**Faturaışgıtemtype**: **usagelineıtems**</span><span class="sxs-lookup"><span data-stu-id="cc395-202">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="cc395-203">**Dönem**: **önceki**</span><span class="sxs-lookup"><span data-stu-id="cc395-203">**Period**: **Previous**</span></span>
- <span data-ttu-id="cc395-204">**Seekoperation**: **İleri**</span><span class="sxs-lookup"><span data-stu-id="cc395-204">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="cc395-205">İstek örneği 2</span><span class="sxs-lookup"><span data-stu-id="cc395-205">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="cc395-206">Yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="cc395-206">Response example 2</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2484
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CV: bpqyomePDUqrSSYC.0
MS-ServerId: 202010406
Date: Wed, 20 Feb 2019 19:59:27 GMT

{
    "totalCount": 1,
    "items": [
        {
            "partnerId": "00083575-bbd0-54de-b2ad-0f5b0e927d71",
            "partnerName": "MTBC",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "VM-Series Next-Generation Firewall (Bundle 2 PAYG)",
            "productName": "VM-Series Next Generation Firewall",
            "publisherName": "Test Alto Networks, Inc.",
            "publisherId": "",
            "subscriptionId": "12345678-04d9-421c-baf8-e3b8dd62ddba",
            "subscriptionDescription": "Pay-As-You-Go",
            "chargeStartDate": "2019-01-01T00:00:00Z",
            "chargeEndDate": "2019-02-01T00:00:00Z",
            "usageDate": "2019-01-02T00:00:00Z",
            "meterType": "1 Compute Hour - 4core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "4core",
            "meterSubCategory": "VM-Series Next Generation Firewall",
            "meterName": "VM-Series Next Generation Firewall - VM-Series Next-Generation Firewall (Bundle 2 PAYG) - 4 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "ECH-PAN-RG",
            "resourceUri": "/subscriptions/12345678-04d9-421c-baf8-e3b8dd62ddba/resourceGroups/ECH-PAN-RG/providers/Microsoft.Compute/virtualMachines/echpanfw",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_D3_v2\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "",
            "unitPrice": 1.2799888920023,
            "quantity": 24.0,
            "unitType": "",
            "billingPreTaxTotal": 30.7197334080551,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 30.7197334080551,
            "pricingCurrency": "USD",
            "entitlementId": "31cdf47f-b249-4edd-9319-637862d8c0b4",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0,
            "rateOfPartnerEarnedCredit": 0,
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
