---
title: Fatura faturalanmamış ticari tüketim satırı öğelerini Al
description: Iş Ortağı Merkezi API 'Lerini kullanarak belirli bir faturaya ait faturalandırılmamış ticari tüketim çizgisi öğe ayrıntılarının bir koleksiyonunu alabilirsiniz.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 594946db712c28983dd390207fb06c8d9f62f18b
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769677"
---
# <a name="get-invoice-unbilled-commercial-consumption-line-items"></a><span data-ttu-id="5de35-103">Fatura faturalanmamış ticari tüketim satırı öğelerini Al</span><span class="sxs-lookup"><span data-stu-id="5de35-103">Get invoice unbilled commercial consumption line items</span></span>

<span data-ttu-id="5de35-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="5de35-104">**Applies to:**</span></span>

- <span data-ttu-id="5de35-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5de35-105">Partner Center</span></span>

<span data-ttu-id="5de35-106">Faturalandırılmamış ticari tüketim satırı öğe ayrıntılarının koleksiyonunu alma.</span><span class="sxs-lookup"><span data-stu-id="5de35-106">How to get a collection of unbilled commercial consumption line item details.</span></span>

<span data-ttu-id="5de35-107">Ayrıca, faturalandırılmamış ticari tüketim çizgisi öğelerinin (açık kullanım satırı öğeleri olarak da bilinir) programlı bir şekilde ayrıntılarını almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5de35-107">You can use the following methods to get a collection of details unbilled commercial consumption line items (also known as open usage line items) programmatically.</span></span>

>[!NOTE]
><span data-ttu-id="5de35-108">Günlük olarak derecelendirilen kullanımlar, Iş Ortağı Merkezi 'nde veya API aracılığıyla erişilecek 24 saat sürer.</span><span class="sxs-lookup"><span data-stu-id="5de35-108">Daily-rated usage normally takes 24 hours to appear in Partner Center or to be accessed through the API.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5de35-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5de35-109">Prerequisites</span></span>

- <span data-ttu-id="5de35-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5de35-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5de35-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5de35-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5de35-112">Bir fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5de35-112">An invoice identifier.</span></span> <span data-ttu-id="5de35-113">Bu, satır öğelerinin alınacağı faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="5de35-113">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="5de35-114">C\#</span><span class="sxs-lookup"><span data-stu-id="5de35-114">C\#</span></span>

<span data-ttu-id="5de35-115">Belirtilen faturaya ait satır öğelerini almak için:</span><span class="sxs-lookup"><span data-stu-id="5de35-115">To get the line items for the specified invoice:</span></span>

1. <span data-ttu-id="5de35-116">Belirtilen faturaya yönelik işlemleri faturalamak için bir arabirim almak üzere [**Byıd**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5de35-116">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="5de35-117">Fatura nesnesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5de35-117">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="5de35-118">**Fatura nesnesi** belirtilen faturaya ait tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="5de35-118">The **invoice object** contains all of the information for the specified invoice.</span></span> <span data-ttu-id="5de35-119">**Sağlayıcı** , faturalandırılmamış ayrıntı bilgisinin kaynağını tanımlar (örneğin, **Onetime**).</span><span class="sxs-lookup"><span data-stu-id="5de35-119">The **Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span> <span data-ttu-id="5de35-120">**Invoineıtemtype** türü belirtir (örneğin, **Usagelineitem**).</span><span class="sxs-lookup"><span data-stu-id="5de35-120">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="5de35-121">Aşağıdaki örnek kod, **ınvogıtems** koleksiyonunu işlemek için bir **foreach** döngüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="5de35-121">The following example code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="5de35-122">Her bir **Faturaöğeside** her bir faturaya ait ayrı bir satır öğesi koleksiyonu alınır.</span><span class="sxs-lookup"><span data-stu-id="5de35-122">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="5de35-123">Bir **InvoiceDetail** örneğine karşılık gelen satır öğelerinin bir koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="5de35-123">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="5de35-124">Örneğe ait **Billingprovider** ve **ınvoineıtemtype** 'ı [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="5de35-124">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="5de35-125">İlişkili satır öğelerini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5de35-125">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="5de35-126">Aşağıdaki örnekte gösterildiği gibi koleksiyonun çapraz geçişini yapmak için bir Numaralandırıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5de35-126">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="5de35-127">Benzer bir örnek için bkz.:</span><span class="sxs-lookup"><span data-stu-id="5de35-127">For a similar example, see:</span></span>

- <span data-ttu-id="5de35-128">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="5de35-128">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="5de35-129">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="5de35-129">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="5de35-130">Sınıf: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="5de35-130">Class: **GetUnBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="5de35-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5de35-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5de35-132">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5de35-132">Request syntax</span></span>

<span data-ttu-id="5de35-133">Kullanım durumunuza bağlı olarak REST isteğiniz için aşağıdaki sözdizimleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="5de35-133">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="5de35-134">Daha fazla bilgi için her bir sözdizimi için açıklamalara bakın.</span><span class="sxs-lookup"><span data-stu-id="5de35-134">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="5de35-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5de35-135">Method</span></span>  | <span data-ttu-id="5de35-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5de35-136">Request URI</span></span>         | <span data-ttu-id="5de35-137">Sözdizimi kullanım durumunun açıklaması</span><span class="sxs-lookup"><span data-stu-id="5de35-137">Description of syntax use case</span></span> |                                                                                                                                            |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5de35-138">**Al**</span><span class="sxs-lookup"><span data-stu-id="5de35-138">**GET**</span></span> | <span data-ttu-id="5de35-139">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturaın/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &period = {PERIOD} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5de35-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="5de35-140">Verilen faturaya ait her satır öğesinin tam listesini döndürmek için bu sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5de35-140">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="5de35-141">**Al**</span><span class="sxs-lookup"><span data-stu-id="5de35-141">**GET**</span></span> | <span data-ttu-id="5de35-142">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &süre = {period} &boyut = {SIZE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5de35-142">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="5de35-143">Büyük faturalar için bu sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5de35-143">Use this syntax for large invoices.</span></span> <span data-ttu-id="5de35-144">Satır öğelerinin disk belleğine alınmış bir listesini döndürmek için bu söz dizimini belirtilen boyut ve 0 tabanlı bir uzaklığa göre kullanın.</span><span class="sxs-lookup"><span data-stu-id="5de35-144">Use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="5de35-145">**Al**</span><span class="sxs-lookup"><span data-stu-id="5de35-145">**GET**</span></span> | <span data-ttu-id="5de35-146">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/Unbilled/LineItems? sağlayıcı = onetime&fatura elineıtemtype = usagelineıtems&CurrencyCode = {currencycode} &period = {period} &boyut = {size} &Seekoperation = ileri</span><span class="sxs-lookup"><span data-stu-id="5de35-146">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="5de35-147">Kullanılarak mutabakat satır öğelerinin sonraki sayfasını almak için bu sözdizimini kullanın `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="5de35-147">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="5de35-148">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="5de35-148">URI parameters</span></span>

<span data-ttu-id="5de35-149">İsteği oluştururken aşağıdaki URI ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5de35-149">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="5de35-150">Ad</span><span class="sxs-lookup"><span data-stu-id="5de35-150">Name</span></span>                   | <span data-ttu-id="5de35-151">Tür</span><span class="sxs-lookup"><span data-stu-id="5de35-151">Type</span></span>   | <span data-ttu-id="5de35-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5de35-152">Required</span></span> | <span data-ttu-id="5de35-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5de35-153">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="5de35-154">sağlayıcısını</span><span class="sxs-lookup"><span data-stu-id="5de35-154">provider</span></span>               | <span data-ttu-id="5de35-155">string</span><span class="sxs-lookup"><span data-stu-id="5de35-155">string</span></span> | <span data-ttu-id="5de35-156">Yes</span><span class="sxs-lookup"><span data-stu-id="5de35-156">Yes</span></span>      | <span data-ttu-id="5de35-157">Sağlayıcı: "**Onetime**".</span><span class="sxs-lookup"><span data-stu-id="5de35-157">The provider: "**OneTime**".</span></span>                                                |
| <span data-ttu-id="5de35-158">fatura-satır-öğe türü</span><span class="sxs-lookup"><span data-stu-id="5de35-158">invoice-line-item-type</span></span> | <span data-ttu-id="5de35-159">string</span><span class="sxs-lookup"><span data-stu-id="5de35-159">string</span></span> | <span data-ttu-id="5de35-160">Yes</span><span class="sxs-lookup"><span data-stu-id="5de35-160">Yes</span></span>      | <span data-ttu-id="5de35-161">Fatura ayrıntısı türü: "**Usagelineıtems**", "**usagelineıtems**".</span><span class="sxs-lookup"><span data-stu-id="5de35-161">The type of invoice detail: "**UsageLineItems**", "**UsageLineItems**".</span></span>               |
| <span data-ttu-id="5de35-162">currencyCode</span><span class="sxs-lookup"><span data-stu-id="5de35-162">currencyCode</span></span>           | <span data-ttu-id="5de35-163">string</span><span class="sxs-lookup"><span data-stu-id="5de35-163">string</span></span> | <span data-ttu-id="5de35-164">Yes</span><span class="sxs-lookup"><span data-stu-id="5de35-164">Yes</span></span>      | <span data-ttu-id="5de35-165">Faturalandırılmamış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="5de35-165">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="5de35-166">dönem</span><span class="sxs-lookup"><span data-stu-id="5de35-166">period</span></span>                 | <span data-ttu-id="5de35-167">string</span><span class="sxs-lookup"><span data-stu-id="5de35-167">string</span></span> | <span data-ttu-id="5de35-168">Yes</span><span class="sxs-lookup"><span data-stu-id="5de35-168">Yes</span></span>      | <span data-ttu-id="5de35-169">Faturalandırılmamış keşfi için süre (örneğin: **geçerli**, **önceki**).</span><span class="sxs-lookup"><span data-stu-id="5de35-169">The period for unbilled recon (for example: **current**, **previous**).</span></span><br/><br/><span data-ttu-id="5de35-170">**Önceki** – faturalandırma döngüsünün 01/01/2020 – 01/31/2020 olması, büyük olasılıkla faturanızda 02/06/2020 ve 02/08/2020 UTC zamanı arasında oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5de35-170">**Previous** – if the billing cycle is 01/01/2020 – 01/31/2020 then, most likely that your invoice is generated between 02/06/2020 and 02/08/2020 UTC time.</span></span> <span data-ttu-id="5de35-171">Faturalandırma döngüsünün faturalandırılmamış kullanım verilerini (01/01/2020 – 01/31/2020) 02/01/2020 ve fatura tarafından üretilen tarih (02/06/2020 ve 02/08/2020 UTC saati arasında) arasında herhangi bir zamanda sorgulayıp, "önceki" olarak dönem ' i seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5de35-171">If you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) on any time between 02/01/2020 and the invoice-generated date (which is between 02/06/2020 and 02/08/2020 UTC time), then, you need to choose Period as "Previous".</span></span><br/><br/><span data-ttu-id="5de35-172">**Current** : faturalandırma döngüsünün 01/01/2020 – 01/31/2020 olması, büyük olasılıkla faturanızda 02/06/2020 ve 02/08/2020 UTC zamanı arasında oluşturulması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5de35-172">**Current** – if the billing cycle is 01/01/2020 – 01/31/2020 then, most likely that your invoice is generated between 02/06/2020 and 02/08/2020 UTC time.</span></span> <span data-ttu-id="5de35-173">Fatura döneminizin içinde olan 01/01/2020 ve 01/31/2020 arasında herhangi bir zamanda faturalandırma döngüsünün faturalandırılmamış kullanım verilerini (01/01/2020 – 01/31/2020) sorgulayabilmeniz gerekiyorsa, dönemi "geçerli" olarak seçmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5de35-173">If you need to query your unbilled usage data of the billing cycle (01/01/2020 – 01/31/2020) on any time between 01/01/2020 and 01/31/2020 which is within your billing cycle, then, you need to choose Period as "Current".</span></span> |
| <span data-ttu-id="5de35-174">boyut</span><span class="sxs-lookup"><span data-stu-id="5de35-174">size</span></span>                   | <span data-ttu-id="5de35-175">sayı</span><span class="sxs-lookup"><span data-stu-id="5de35-175">number</span></span> | <span data-ttu-id="5de35-176">No</span><span class="sxs-lookup"><span data-stu-id="5de35-176">No</span></span>       | <span data-ttu-id="5de35-177">Döndürülecek en fazla öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="5de35-177">The maximum number of items to return.</span></span> <span data-ttu-id="5de35-178">Varsayılan boyut 2000 ' dir.</span><span class="sxs-lookup"><span data-stu-id="5de35-178">The default size is 2000.</span></span>                    |
| <span data-ttu-id="5de35-179">seekOperation</span><span class="sxs-lookup"><span data-stu-id="5de35-179">seekOperation</span></span>          | <span data-ttu-id="5de35-180">dize</span><span class="sxs-lookup"><span data-stu-id="5de35-180">string</span></span> | <span data-ttu-id="5de35-181">No</span><span class="sxs-lookup"><span data-stu-id="5de35-181">No</span></span>       | <span data-ttu-id="5de35-182">`seekOperation=Next`Mutabakat satır öğelerinin sonraki sayfasını almak için ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="5de35-182">Set `seekOperation=Next` to get the next page of reconciliation line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="5de35-183">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5de35-183">Request headers</span></span>

<span data-ttu-id="5de35-184">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5de35-184">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5de35-185">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5de35-185">Request body</span></span>

<span data-ttu-id="5de35-186">Yok.</span><span class="sxs-lookup"><span data-stu-id="5de35-186">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="5de35-187">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5de35-187">REST response</span></span>

<span data-ttu-id="5de35-188">Başarılı olursa, yanıt satır öğesi ayrıntıları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="5de35-188">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="5de35-189">*Satır **öğesi için**, **satın alma** değeri **Yeni** ile eşlenir ve değer **iadesi** **iptal** edilecek şekilde eşlenir.*</span><span class="sxs-lookup"><span data-stu-id="5de35-189">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5de35-190">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5de35-190">Response success and error codes</span></span>

<span data-ttu-id="5de35-191">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5de35-191">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5de35-192">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5de35-192">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5de35-193">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5de35-193">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="request-response-examples"></a><span data-ttu-id="5de35-194">İstek-yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="5de35-194">Request-response examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="5de35-195">İstek-yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="5de35-195">Request-response example 1</span></span>

<span data-ttu-id="5de35-196">Aşağıdaki ayrıntılar Bu örnek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="5de35-196">The following details apply to this example:</span></span>

- <span data-ttu-id="5de35-197">**Sağlayıcı**: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="5de35-197">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="5de35-198">**Faturaışgıtemtype**: **usagelineıtems**</span><span class="sxs-lookup"><span data-stu-id="5de35-198">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="5de35-199">**Dönem**: **önceki**</span><span class="sxs-lookup"><span data-stu-id="5de35-199">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="5de35-200">İstek örneği 1</span><span class="sxs-lookup"><span data-stu-id="5de35-200">Request example 1</span></span>

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

### <a name="response-example-1"></a><span data-ttu-id="5de35-201">Yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="5de35-201">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="5de35-202">İstek-yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="5de35-202">Request-response example 2</span></span>

<span data-ttu-id="5de35-203">Aşağıdaki ayrıntılar Bu örnek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="5de35-203">The following details apply to this example:</span></span>

- <span data-ttu-id="5de35-204">**Sağlayıcı**: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="5de35-204">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="5de35-205">**Faturaışgıtemtype**: **usagelineıtems**</span><span class="sxs-lookup"><span data-stu-id="5de35-205">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="5de35-206">**Dönem**: **önceki**</span><span class="sxs-lookup"><span data-stu-id="5de35-206">**Period**: **Previous**</span></span>
- <span data-ttu-id="5de35-207">**Seekoperation**: **İleri**</span><span class="sxs-lookup"><span data-stu-id="5de35-207">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="5de35-208">İstek örneği 2</span><span class="sxs-lookup"><span data-stu-id="5de35-208">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="5de35-209">Yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="5de35-209">Response example 2</span></span>

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
