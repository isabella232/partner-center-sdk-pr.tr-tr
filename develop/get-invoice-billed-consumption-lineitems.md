---
title: Faturalandırmış ticari tüketim satırı öğelerini alın
description: Belirli bir fatura için ticari tüketim fatura satırı öğesi (kapalı günlük olarak derecelendirilmiş kullanım satırı öğesi) ayrıntılarının bir koleksiyonunu almak için İş Ortağı Merkezi edinebilirsiniz.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 1406938b16e5a363a73c36ef0338eb5fc4305279
ms.sourcegitcommit: 89aefbff6dbe740b6f27a888492ffc2e5f98b1e9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 05/24/2021
ms.locfileid: "110325454"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="7a638-103">Faturalandırmış ticari tüketim satırı öğelerini alın</span><span class="sxs-lookup"><span data-stu-id="7a638-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="7a638-104">**Aşağıdakiler için geçerlidir:**</span><span class="sxs-lookup"><span data-stu-id="7a638-104">**Applies to:**</span></span>

- <span data-ttu-id="7a638-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7a638-105">Partner Center</span></span>

<span data-ttu-id="7a638-106">Belirtilen fatura için ticari tüketim fatura satırı öğelerine (kapalı günlük olarak anılan kullanım satırı öğeleri olarak da bilinir) ilişkin ayrıntıların bir koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7a638-106">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7a638-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7a638-107">Prerequisites</span></span>

- <span data-ttu-id="7a638-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="7a638-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7a638-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="7a638-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7a638-110">Fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7a638-110">An invoice identifier.</span></span> <span data-ttu-id="7a638-111">Bu, satır öğelerinin alın satırı için faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7a638-111">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="7a638-112">C\#</span><span class="sxs-lookup"><span data-stu-id="7a638-112">C\#</span></span>

<span data-ttu-id="7a638-113">Belirtilen faturaya yönelik ticari satır öğelerini almak için fatura nesnesini alasiniz:</span><span class="sxs-lookup"><span data-stu-id="7a638-113">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="7a638-114">Belirtilen [**faturaya yönelik**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) fatura işlemlerine arabirim almak için ById yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="7a638-114">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="7a638-115">Fatura nesnesini [**almak**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) için [**Get veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="7a638-115">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="7a638-116">Invoice nesnesi, belirtilen faturayla ilgili tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="7a638-116">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="7a638-117">Sağlayıcı, faturalandırilen ayrıntı bilgisinin kaynağını tanımlar (örneğin, **bir saat).** </span><span class="sxs-lookup"><span data-stu-id="7a638-117">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="7a638-118">**InvoiceLineItemType** türü belirtir (örneğin, **UsageLineItem).**</span><span class="sxs-lookup"><span data-stu-id="7a638-118">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="7a638-119">Aşağıdaki örnek kod, satır öğeleri koleksiyonunu işlemeye bir **foreach** döngüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="7a638-119">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="7a638-120">Her **InvoiceLineItemType** için ayrı bir satır öğeleri koleksiyonu alınır.</span><span class="sxs-lookup"><span data-stu-id="7a638-120">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="7a638-121">**InvoiceDetail** örneğine karşılık gelen satır öğeleri koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="7a638-121">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="7a638-122">Örneğin **BillingProvider ve** **InvoiceLineItemType** bilgilerini [**By yöntemine**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) geçin.</span><span class="sxs-lookup"><span data-stu-id="7a638-122">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="7a638-123">İlişkili [**satır öğelerini**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) almak için Get veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="7a638-123">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="7a638-124">Aşağıdaki örnekte gösterildiği gibi koleksiyonun çapraz geçişini yapmak için bir Numaralandırıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7a638-124">Create an enumerator to traverse the collection as shown in the following example.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string invoiceId;
// string curencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById(invoiceId).By("onetime", "usagelineitems", curencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="7a638-125">Benzer bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="7a638-125">For a similar example, see the following:</span></span>

- <span data-ttu-id="7a638-126">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7a638-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7a638-127">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="7a638-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="7a638-128">Sınıf: **GetBilledConsumptionReconLineItemsPaging. cs**</span><span class="sxs-lookup"><span data-stu-id="7a638-128">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7a638-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7a638-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7a638-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7a638-130">Request syntax</span></span>

<span data-ttu-id="7a638-131">Verilen faturaya ait her satır öğesinin tam listesini döndürmek için ilk sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a638-131">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="7a638-132">Büyük faturalar için, satır öğelerinin disk belleğine alınmış bir listesini döndürmek üzere belirtilen boyut ve 0 tabanlı uzaklığa sahip ikinci söz dizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a638-132">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="7a638-133">Kullanarak keşfi satır öğelerinin sonraki sayfasını almak için üçüncü sözdizimini kullanın `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="7a638-133">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="7a638-134">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7a638-134">Method</span></span>  | <span data-ttu-id="7a638-135">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7a638-135">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7a638-136">**Al**</span><span class="sxs-lookup"><span data-stu-id="7a638-136">**GET**</span></span> | <span data-ttu-id="7a638-137">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvoyıtemtype = usagelineıtems&CurrencyCode = {CURRENCYCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7a638-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="7a638-138">**Al**</span><span class="sxs-lookup"><span data-stu-id="7a638-138">**GET**</span></span> | <span data-ttu-id="7a638-139">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvoyıtemtype = usagelineıtems&CurrencyCode = {currencycode} &boyut = {SIZE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7a638-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="7a638-140">**Al**</span><span class="sxs-lookup"><span data-stu-id="7a638-140">**GET**</span></span> | <span data-ttu-id="7a638-141">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvoyıtemtype = usagelineıtems&CurrencyCode = {currencycode} &size = {size} &seekoperation = ileri</span><span class="sxs-lookup"><span data-stu-id="7a638-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="7a638-142">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="7a638-142">URI parameters</span></span>

<span data-ttu-id="7a638-143">İsteği oluştururken aşağıdaki URI ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a638-143">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="7a638-144">Ad</span><span class="sxs-lookup"><span data-stu-id="7a638-144">Name</span></span>                   | <span data-ttu-id="7a638-145">Tür</span><span class="sxs-lookup"><span data-stu-id="7a638-145">Type</span></span>   | <span data-ttu-id="7a638-146">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7a638-146">Required</span></span> | <span data-ttu-id="7a638-147">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7a638-147">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="7a638-148">Fatura kimliği</span><span class="sxs-lookup"><span data-stu-id="7a638-148">invoice-id</span></span>             | <span data-ttu-id="7a638-149">string</span><span class="sxs-lookup"><span data-stu-id="7a638-149">string</span></span> | <span data-ttu-id="7a638-150">Yes</span><span class="sxs-lookup"><span data-stu-id="7a638-150">Yes</span></span>      | <span data-ttu-id="7a638-151">Faturayı tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="7a638-151">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="7a638-152">Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="7a638-152">provider</span></span>               | <span data-ttu-id="7a638-153">string</span><span class="sxs-lookup"><span data-stu-id="7a638-153">string</span></span> | <span data-ttu-id="7a638-154">Yes</span><span class="sxs-lookup"><span data-stu-id="7a638-154">Yes</span></span>      | <span data-ttu-id="7a638-155">Sağlayıcı: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="7a638-155">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="7a638-156">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="7a638-156">invoice-line-item-type</span></span> | <span data-ttu-id="7a638-157">string</span><span class="sxs-lookup"><span data-stu-id="7a638-157">string</span></span> | <span data-ttu-id="7a638-158">Yes</span><span class="sxs-lookup"><span data-stu-id="7a638-158">Yes</span></span>      | <span data-ttu-id="7a638-159">Fatura ayrıntısı türü: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="7a638-159">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="7a638-160">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7a638-160">currencyCode</span></span>           | <span data-ttu-id="7a638-161">string</span><span class="sxs-lookup"><span data-stu-id="7a638-161">string</span></span> | <span data-ttu-id="7a638-162">Yes</span><span class="sxs-lookup"><span data-stu-id="7a638-162">Yes</span></span>      | <span data-ttu-id="7a638-163">Faturalandırmış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="7a638-163">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="7a638-164">dönem</span><span class="sxs-lookup"><span data-stu-id="7a638-164">period</span></span>                 | <span data-ttu-id="7a638-165">string</span><span class="sxs-lookup"><span data-stu-id="7a638-165">string</span></span> | <span data-ttu-id="7a638-166">Yes</span><span class="sxs-lookup"><span data-stu-id="7a638-166">Yes</span></span>      | <span data-ttu-id="7a638-167">Faturalandırmış mutabakat için dönem.</span><span class="sxs-lookup"><span data-stu-id="7a638-167">The period for billed recon.</span></span> <span data-ttu-id="7a638-168">örnek: geçerli, önceki.</span><span class="sxs-lookup"><span data-stu-id="7a638-168">example: current, previous.</span></span>        |
| <span data-ttu-id="7a638-169">boyut</span><span class="sxs-lookup"><span data-stu-id="7a638-169">size</span></span>                   | <span data-ttu-id="7a638-170">sayı</span><span class="sxs-lookup"><span data-stu-id="7a638-170">number</span></span> | <span data-ttu-id="7a638-171">No</span><span class="sxs-lookup"><span data-stu-id="7a638-171">No</span></span>       | <span data-ttu-id="7a638-172">İade etmek istediğiniz en fazla öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a638-172">The maximum number of items to return.</span></span> <span data-ttu-id="7a638-173">Varsayılan boyut 2000'tir</span><span class="sxs-lookup"><span data-stu-id="7a638-173">Default size is 2000</span></span>       |
| <span data-ttu-id="7a638-174">seekOperation</span><span class="sxs-lookup"><span data-stu-id="7a638-174">seekOperation</span></span>          | <span data-ttu-id="7a638-175">dize</span><span class="sxs-lookup"><span data-stu-id="7a638-175">string</span></span> | <span data-ttu-id="7a638-176">No</span><span class="sxs-lookup"><span data-stu-id="7a638-176">No</span></span>       | <span data-ttu-id="7a638-177">Keşif satırı öğelerinin sonraki sayfasını almak için seekOperation=Next'i ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7a638-177">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7a638-178">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7a638-178">Request headers</span></span>

<span data-ttu-id="7a638-179">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="7a638-179">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7a638-180">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7a638-180">Request body</span></span>

<span data-ttu-id="7a638-181">Yok.</span><span class="sxs-lookup"><span data-stu-id="7a638-181">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="7a638-182">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7a638-182">REST response</span></span>

<span data-ttu-id="7a638-183">Başarılı olursa yanıt, satır öğesi ayrıntıları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="7a638-183">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="7a638-184">**ChargeType** satır öğesi için Satın Alma değeri **Yeni** ile **eşlenmiş.**</span><span class="sxs-lookup"><span data-stu-id="7a638-184">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="7a638-185">Para İadesi **değeri** İptal ile **eşlenmiş.**</span><span class="sxs-lookup"><span data-stu-id="7a638-185">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7a638-186">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7a638-186">Response success and error codes</span></span>

<span data-ttu-id="7a638-187">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="7a638-187">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7a638-188">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a638-188">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7a638-189">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="7a638-189">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="7a638-190">REST örnekleri</span><span class="sxs-lookup"><span data-stu-id="7a638-190">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="7a638-191">İstek-yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="7a638-191">Request-response example 1</span></span>

<span data-ttu-id="7a638-192">Bu örnek REST isteği ve yanıtının ayrıntıları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7a638-192">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="7a638-193">**Sağlayıcı**: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="7a638-193">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="7a638-194">**Faturaışgıtemtype**: **usagelineıtems**</span><span class="sxs-lookup"><span data-stu-id="7a638-194">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="7a638-195">**Dönem**: **önceki**</span><span class="sxs-lookup"><span data-stu-id="7a638-195">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="7a638-196">İstek örneği 1</span><span class="sxs-lookup"><span data-stu-id="7a638-196">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="7a638-197">Yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="7a638-197">Response example 1</span></span>

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
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "creditType": "Credit Not Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        },
        {
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Ubuntu 16.04 (WebHost)",
            "productName": "Test Test on Linux",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Linux",
            "meterName": "Test Test on Linux - Test Test on Ubuntu 16.04 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TESTRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestRG/providers/Microsoft.Compute/virtualMachines/testUbuntuTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209951014286867,
            "quantity": 23.350007,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.490235765325545,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.490235765325545,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1999968000511991808131,
            "rateOfPartnerEarnedCredit": 0,
            "rateOfCredit": 1,
            "creditType": "Azure Credit Applied",
            "invoiceLineItemType": "usage_line_items",
            "billingProvider": "marketplace",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="7a638-198">İstek-yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="7a638-198">Request-response example 2</span></span>

<span data-ttu-id="7a638-199">Bu örnek REST isteği ve yanıtının ayrıntıları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="7a638-199">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="7a638-200">**Sağlayıcı**: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="7a638-200">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="7a638-201">**Faturaışgıtemtype**: **usagelineıtems**</span><span class="sxs-lookup"><span data-stu-id="7a638-201">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="7a638-202">**Dönem**: **önceki**</span><span class="sxs-lookup"><span data-stu-id="7a638-202">**Period**: **Previous**</span></span>
- <span data-ttu-id="7a638-203">**Seekoperation**: **İleri**</span><span class="sxs-lookup"><span data-stu-id="7a638-203">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="7a638-204">İstek örneği 2</span><span class="sxs-lookup"><span data-stu-id="7a638-204">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/T000001234/lineitems?provider=onetime&invoiceLineItemType=usagelineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="response-example-2"></a><span data-ttu-id="7a638-205">Yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="7a638-205">Response example 2</span></span>

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
            "partnerId": "2b8940db-5089-539c-e757-520ed1d1bc88",
            "partnerName": "",
            "customerId": "",
            "customerName": "",
            "customerDomainName": "",
            "invoiceNumber": "T000001234",
            "productId": "",
            "skuId": "",
            "availabilityId": "",
            "skuName": "Test Test on Windows 2012 R2 (WebHost)",
            "productName": "Test Test on Windows",
            "publisherName": "Test",
            "publisherId": "28503520",
            "subscriptionId": "12345678-9d62-4a85-8fd0-91a87c261bc4",
            "subscriptionDescription": "Subscription 10",
            "chargeStartDate": "2018-11-01T00:00:00Z",
            "chargeEndDate": "2018-12-01T00:00:00Z",
            "usageDate": "2018-11-13T00:00:00Z",
            "meterType": "1 Compute Hour - 1core",
            "meterCategory": "Virtual Machine Licenses",
            "meterId": "1core",
            "meterSubCategory": "Test Test on Windows",
            "meterName": "Test Test on Windows - Test Test on Windows 2012 R2 (WebHost) - 1 Core Hours",
            "meterRegion": "",
            "unitOfMeasure": "1 Hour",
            "resourceLocation": "EASTUS2",
            "consumedService": "Microsoft.Compute",
            "resourceGroup": "TestWINRG",
            "resourceUri": "/subscriptions/12345678-9d62-4a85-8fd0-91a87c261bc4/resourceGroups/TestWINRG/providers/Microsoft.Compute/virtualMachines/testWinTest",
            "tags": "",
            "additionalInfo": "{  \"ImageType\": null,  \"ServiceType\": \"Standard_B1s\",  \"VMName\": null,  \"VMProperties\": null,  \"UsageType\": \"ComputeHR_SW\"}",
            "serviceInfo1": "",
            "serviceInfo2": "",
            "customerCountry": "",
            "mpnId": "1234567",
            "resellerMpnId": "",
            "chargeType": "new",
            "unitPrice": 0.0209496384791679,
            "quantity": 23.200004,
            "unitType": "1 Hour",
            "billingPreTaxTotal": 0.486031696515249,
            "billingCurrency": "USD",
            "pricingPreTaxTotal": 0.486031696515249,
            "pricingCurrency": "USD",
            "entitlementId": "66bada28-271e-4b7a-aaf5-c0ead6312345",
            "entitlementDescription": "Partner Subscription",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "effectiveUnitPrice": 0.1835431430074643112595,
            "rateOfPartnerEarnedCredit": 0.15,
            "rateOfCredit": 0.15,
            "creditType": "Partner Earned Credit Applied",
            "attributes": {
                "objectType": "DailyRatedUsageLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/T000001234/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
