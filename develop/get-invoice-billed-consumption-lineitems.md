---
title: Faturalandırmış ticari tüketim satırı öğelerini alın
description: Belirli bir fatura için ticari tüketim fatura satırı öğesi (kapalı günlük olarak derecelendirilmiş kullanım satırı öğesi) ayrıntılarının bir koleksiyonunu almak için İş Ortağı Merkezi edinebilirsiniz.
ms.date: 01/13/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 285b6fbda774c9396dee8947550ed774d52bf901
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446233"
---
# <a name="get-invoice-billed-commercial-consumption-line-items"></a><span data-ttu-id="a19b2-103">Faturalandırmış ticari tüketim satırı öğelerini alın</span><span class="sxs-lookup"><span data-stu-id="a19b2-103">Get invoice billed commercial consumption line items</span></span>

<span data-ttu-id="a19b2-104">Belirtilen bir fatura için ticari tüketim fatura satırı öğelerine (kapalı günlük olarak anılan kullanım satırı öğeleri olarak da bilinir) ilişkin ayrıntıların bir koleksiyonunu almak için aşağıdaki yöntemleri kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a19b2-104">You can use the following methods to get a collection of details for commercial consumption invoice line items (also known as closed daily rated usage line items) for a specified invoice.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="a19b2-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a19b2-105">Prerequisites</span></span>

- <span data-ttu-id="a19b2-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="a19b2-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a19b2-107">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="a19b2-107">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="a19b2-108">Fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="a19b2-108">An invoice identifier.</span></span> <span data-ttu-id="a19b2-109">Bu, satır öğelerinin alın satırı için faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="a19b2-109">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="a19b2-110">C\#</span><span class="sxs-lookup"><span data-stu-id="a19b2-110">C\#</span></span>

<span data-ttu-id="a19b2-111">Belirtilen faturaya yönelik ticari satır öğelerini almak için fatura nesnesini alasiniz:</span><span class="sxs-lookup"><span data-stu-id="a19b2-111">To get the commercial line items for the specified invoice, you must retrieve the invoice object:</span></span>

1. <span data-ttu-id="a19b2-112">Belirtilen [**faturaya yönelik**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) fatura işlemlerine arabirim almak için ById yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="a19b2-112">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="a19b2-113">Fatura nesnesini [**almak**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) için [**Get veya GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="a19b2-113">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span> <span data-ttu-id="a19b2-114">Invoice nesnesi, belirtilen faturayla ilgili tüm bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="a19b2-114">The invoice object contains all of the information for the specified invoice.</span></span>

<span data-ttu-id="a19b2-115">Sağlayıcı, faturalandırilen ayrıntı bilgisinin kaynağını tanımlar (örneğin, **bir saat).** </span><span class="sxs-lookup"><span data-stu-id="a19b2-115">The **Provider** identifies the source of the billed detail information (for example, **onetime**).</span></span> <span data-ttu-id="a19b2-116">**InvoiceLineItemType** türü belirtir (örneğin, **UsageLineItem).**</span><span class="sxs-lookup"><span data-stu-id="a19b2-116">The **InvoiceLineItemType** specifies the type (for example, **UsageLineItem**).</span></span>

<span data-ttu-id="a19b2-117">Aşağıdaki örnek kod, satır öğeleri koleksiyonunu işlemeye bir **foreach** döngüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="a19b2-117">The following example code uses a **foreach** loop to process the line items collection.</span></span> <span data-ttu-id="a19b2-118">Her **InvoiceLineItemType** için ayrı bir satır öğeleri koleksiyonu alınır.</span><span class="sxs-lookup"><span data-stu-id="a19b2-118">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

<span data-ttu-id="a19b2-119">**InvoiceDetail** örneğine karşılık gelen satır öğeleri koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="a19b2-119">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="a19b2-120">Örneğin **BillingProvider ve** **InvoiceLineItemType** örneklerini [**By yöntemine**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) geçin.</span><span class="sxs-lookup"><span data-stu-id="a19b2-120">Pass the instance's **BillingProvider** and **InvoiceLineItemType** to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="a19b2-121">İlişkili [**satır öğelerini**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) almak için Get veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="a19b2-121">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>
3. <span data-ttu-id="a19b2-122">Aşağıdaki örnekte gösterildiği gibi koleksiyonda geçiş yapmak için bir numaralayıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a19b2-122">Create an enumerator to traverse the collection as shown in the following example.</span></span>

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

<span data-ttu-id="a19b2-123">Benzer bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="a19b2-123">For a similar example, see the following:</span></span>

- <span data-ttu-id="a19b2-124">Örnek: [Konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a19b2-124">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a19b2-125">Project: **İş Ortağı Merkezi SDK'sı Örnekleri**</span><span class="sxs-lookup"><span data-stu-id="a19b2-125">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="a19b2-126">Sınıf: **GetBilledConsumptionReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="a19b2-126">Class: **GetBilledConsumptionReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="a19b2-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a19b2-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a19b2-128">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="a19b2-128">Request syntax</span></span>

<span data-ttu-id="a19b2-129">Verilen faturanın her satır öğesinin tam listesini dönmek için ilk söz dizimlerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a19b2-129">Use the first syntax to return a full list of every line item for the given invoice.</span></span> <span data-ttu-id="a19b2-130">Büyük faturalar için, satır öğelerinin sayfalanmış listesini geri dönmek için belirtilen boyuta ve 0 tabanlı kaydırmaya sahip ikinci söz dizimi kullanın.</span><span class="sxs-lookup"><span data-stu-id="a19b2-130">For large invoices, use the second syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> <span data-ttu-id="a19b2-131">kullanarak mutabakat satırı öğelerinin sonraki sayfasını almak için üçüncü söz dizimlerini `seekOperation = "Next"` kullanın.</span><span class="sxs-lookup"><span data-stu-id="a19b2-131">Use the third syntax to get the next page of recon line items using `seekOperation = "Next"`.</span></span>

| <span data-ttu-id="a19b2-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a19b2-132">Method</span></span>  | <span data-ttu-id="a19b2-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a19b2-133">Request URI</span></span>                                                                                                                                                     |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="a19b2-134">**Al**</span><span class="sxs-lookup"><span data-stu-id="a19b2-134">**GET**</span></span> | <span data-ttu-id="a19b2-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a19b2-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode} HTTP/1.1</span></span>                              |
| <span data-ttu-id="a19b2-136">**Al**</span><span class="sxs-lookup"><span data-stu-id="a19b2-136">**GET**</span></span> | <span data-ttu-id="a19b2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="a19b2-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size} HTTP/1.1</span></span>  |
| <span data-ttu-id="a19b2-138">**Al**</span><span class="sxs-lookup"><span data-stu-id="a19b2-138">**GET**</span></span> | <span data-ttu-id="a19b2-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span><span class="sxs-lookup"><span data-stu-id="a19b2-139">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=usagelineitems&currencycode={currencycode}&size={size}&seekOperation=Next</span></span>                               |

#### <a name="uri-parameters"></a><span data-ttu-id="a19b2-140">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="a19b2-140">URI parameters</span></span>

<span data-ttu-id="a19b2-141">İsteği oluştururken aşağıdaki URI'yi ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a19b2-141">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="a19b2-142">Ad</span><span class="sxs-lookup"><span data-stu-id="a19b2-142">Name</span></span>                   | <span data-ttu-id="a19b2-143">Tür</span><span class="sxs-lookup"><span data-stu-id="a19b2-143">Type</span></span>   | <span data-ttu-id="a19b2-144">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a19b2-144">Required</span></span> | <span data-ttu-id="a19b2-145">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a19b2-145">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="a19b2-146">invoice-id</span><span class="sxs-lookup"><span data-stu-id="a19b2-146">invoice-id</span></span>             | <span data-ttu-id="a19b2-147">string</span><span class="sxs-lookup"><span data-stu-id="a19b2-147">string</span></span> | <span data-ttu-id="a19b2-148">Yes</span><span class="sxs-lookup"><span data-stu-id="a19b2-148">Yes</span></span>      | <span data-ttu-id="a19b2-149">Faturayı tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="a19b2-149">A string that identifies the invoice.</span></span>                             |
| <span data-ttu-id="a19b2-150">Sağlayıcı</span><span class="sxs-lookup"><span data-stu-id="a19b2-150">provider</span></span>               | <span data-ttu-id="a19b2-151">string</span><span class="sxs-lookup"><span data-stu-id="a19b2-151">string</span></span> | <span data-ttu-id="a19b2-152">Yes</span><span class="sxs-lookup"><span data-stu-id="a19b2-152">Yes</span></span>      | <span data-ttu-id="a19b2-153">Sağlayıcı: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="a19b2-153">The provider: "OneTime".</span></span>                                  |
| <span data-ttu-id="a19b2-154">invoice-line-item-type</span><span class="sxs-lookup"><span data-stu-id="a19b2-154">invoice-line-item-type</span></span> | <span data-ttu-id="a19b2-155">string</span><span class="sxs-lookup"><span data-stu-id="a19b2-155">string</span></span> | <span data-ttu-id="a19b2-156">Yes</span><span class="sxs-lookup"><span data-stu-id="a19b2-156">Yes</span></span>      | <span data-ttu-id="a19b2-157">Fatura ayrıntısı türü: "UsageLineItems".</span><span class="sxs-lookup"><span data-stu-id="a19b2-157">The type of invoice detail: "UsageLineItems".</span></span> |
| <span data-ttu-id="a19b2-158">currencyCode</span><span class="sxs-lookup"><span data-stu-id="a19b2-158">currencyCode</span></span>           | <span data-ttu-id="a19b2-159">string</span><span class="sxs-lookup"><span data-stu-id="a19b2-159">string</span></span> | <span data-ttu-id="a19b2-160">Yes</span><span class="sxs-lookup"><span data-stu-id="a19b2-160">Yes</span></span>      | <span data-ttu-id="a19b2-161">Faturalandırmış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="a19b2-161">The currency code for the billed line items.</span></span>                    |
| <span data-ttu-id="a19b2-162">dönem</span><span class="sxs-lookup"><span data-stu-id="a19b2-162">period</span></span>                 | <span data-ttu-id="a19b2-163">string</span><span class="sxs-lookup"><span data-stu-id="a19b2-163">string</span></span> | <span data-ttu-id="a19b2-164">Yes</span><span class="sxs-lookup"><span data-stu-id="a19b2-164">Yes</span></span>      | <span data-ttu-id="a19b2-165">Faturalandırmış mutabakat için dönem.</span><span class="sxs-lookup"><span data-stu-id="a19b2-165">The period for billed recon.</span></span> <span data-ttu-id="a19b2-166">örnek: geçerli, önceki.</span><span class="sxs-lookup"><span data-stu-id="a19b2-166">example: current, previous.</span></span>        |
| <span data-ttu-id="a19b2-167">boyut</span><span class="sxs-lookup"><span data-stu-id="a19b2-167">size</span></span>                   | <span data-ttu-id="a19b2-168">sayı</span><span class="sxs-lookup"><span data-stu-id="a19b2-168">number</span></span> | <span data-ttu-id="a19b2-169">Hayır</span><span class="sxs-lookup"><span data-stu-id="a19b2-169">No</span></span>       | <span data-ttu-id="a19b2-170">İade etmek istediğiniz en fazla öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="a19b2-170">The maximum number of items to return.</span></span> <span data-ttu-id="a19b2-171">Varsayılan boyut 2000'tir</span><span class="sxs-lookup"><span data-stu-id="a19b2-171">Default size is 2000</span></span>       |
| <span data-ttu-id="a19b2-172">seekOperation</span><span class="sxs-lookup"><span data-stu-id="a19b2-172">seekOperation</span></span>          | <span data-ttu-id="a19b2-173">dize</span><span class="sxs-lookup"><span data-stu-id="a19b2-173">string</span></span> | <span data-ttu-id="a19b2-174">No</span><span class="sxs-lookup"><span data-stu-id="a19b2-174">No</span></span>       | <span data-ttu-id="a19b2-175">Keşif satırı öğelerinin sonraki sayfasını almak için seekOperation=Next'i ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="a19b2-175">Set seekOperation=Next to get the next page of recon line items.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a19b2-176">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a19b2-176">Request headers</span></span>

<span data-ttu-id="a19b2-177">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="a19b2-177">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a19b2-178">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a19b2-178">Request body</span></span>

<span data-ttu-id="a19b2-179">Yok.</span><span class="sxs-lookup"><span data-stu-id="a19b2-179">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="a19b2-180">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a19b2-180">REST response</span></span>

<span data-ttu-id="a19b2-181">Başarılı olursa yanıt, satır öğesi ayrıntıları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="a19b2-181">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="a19b2-182">**ChargeType** satır öğesi için Satın Alma değeri **Yeni** ile **eşlenmiş.**</span><span class="sxs-lookup"><span data-stu-id="a19b2-182">For the line item **ChargeType**, the value **Purchase** is mapped to **New**.</span></span> <span data-ttu-id="a19b2-183">Para İadesi **değeri** İptal ile **eşlenmiş.**</span><span class="sxs-lookup"><span data-stu-id="a19b2-183">The value **Refund** is mapped to **Cancel**.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a19b2-184">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a19b2-184">Response success and error codes</span></span>

<span data-ttu-id="a19b2-185">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="a19b2-185">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a19b2-186">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a19b2-186">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a19b2-187">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="a19b2-187">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

## <a name="rest-examples"></a><span data-ttu-id="a19b2-188">REST örnekleri</span><span class="sxs-lookup"><span data-stu-id="a19b2-188">REST examples</span></span>

### <a name="request-response-example-1"></a><span data-ttu-id="a19b2-189">İstek-yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="a19b2-189">Request-response example 1</span></span>

<span data-ttu-id="a19b2-190">Bu örnek REST isteği ve yanıtının ayrıntıları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a19b2-190">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="a19b2-191">**Sağlayıcı:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="a19b2-191">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="a19b2-192">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="a19b2-192">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="a19b2-193">**Dönem:** **Önceki**</span><span class="sxs-lookup"><span data-stu-id="a19b2-193">**Period**: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="a19b2-194">İstek örneği 1</span><span class="sxs-lookup"><span data-stu-id="a19b2-194">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="a19b2-195">Yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="a19b2-195">Response example 1</span></span>

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

### <a name="request-response-example-2"></a><span data-ttu-id="a19b2-196">İstek-yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="a19b2-196">Request-response example 2</span></span>

<span data-ttu-id="a19b2-197">Bu örnek REST isteği ve yanıtının ayrıntıları aşağıdaki gibidir:</span><span class="sxs-lookup"><span data-stu-id="a19b2-197">The details for this example REST request and response are as follows:</span></span>

- <span data-ttu-id="a19b2-198">**Sağlayıcı:** **OneTime**</span><span class="sxs-lookup"><span data-stu-id="a19b2-198">**Provider**: **OneTime**</span></span>
- <span data-ttu-id="a19b2-199">**InvoiceLineItemType:** **UsageLineItems**</span><span class="sxs-lookup"><span data-stu-id="a19b2-199">**InvoiceLineItemType**: **UsageLineItems**</span></span>
- <span data-ttu-id="a19b2-200">**Dönem:** **Önceki**</span><span class="sxs-lookup"><span data-stu-id="a19b2-200">**Period**: **Previous**</span></span>
- <span data-ttu-id="a19b2-201">**SeekOperation:** **Next**</span><span class="sxs-lookup"><span data-stu-id="a19b2-201">**SeekOperation**: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="a19b2-202">İstek örneği 2</span><span class="sxs-lookup"><span data-stu-id="a19b2-202">Request example 2</span></span>

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

## <a name="response-example-2"></a><span data-ttu-id="a19b2-203">Yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="a19b2-203">Response example 2</span></span>

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
