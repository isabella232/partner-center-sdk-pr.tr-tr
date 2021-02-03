---
title: Faturanın faturalandırılmamış mutabakat satırı öğelerini Al
description: Iş Ortağı Merkezi API 'Lerini kullanarak, belirtilen dönem için faturalandırılmamış mutabakat satır öğesi ayrıntılarının koleksiyonunu alabilirsiniz.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: ff69798ddfd91fca817ec0d047bf407f326066c2
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769851"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a><span data-ttu-id="7fabf-103">Faturanın faturalandırılmamış mutabakat satırı öğelerini Al</span><span class="sxs-lookup"><span data-stu-id="7fabf-103">Get invoice's unbilled reconciliation line items</span></span>

<span data-ttu-id="7fabf-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="7fabf-104">**Applies to:**</span></span>

- <span data-ttu-id="7fabf-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7fabf-105">Partner Center</span></span>
- <span data-ttu-id="7fabf-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7fabf-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="7fabf-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7fabf-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="7fabf-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7fabf-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7fabf-109">Aşağıdaki yöntemleri kullanarak, faturalandırılmamış fatura satırı öğeleri (açık faturalandırma satırı öğeleri olarak da bilinir) için bir ayrıntılar koleksiyonu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7fabf-109">You can use the following methods get a collection of details for unbilled invoice line items (also known as open billing line items).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7fabf-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7fabf-110">Prerequisites</span></span>

- <span data-ttu-id="7fabf-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7fabf-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7fabf-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7fabf-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7fabf-113">Bir fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7fabf-113">An invoice identifier.</span></span> <span data-ttu-id="7fabf-114">Bu, satır öğelerinin alınacağı faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7fabf-114">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="7fabf-115">C\#</span><span class="sxs-lookup"><span data-stu-id="7fabf-115">C\#</span></span>

<span data-ttu-id="7fabf-116">Belirtilen faturaya ait satır öğelerini almak için fatura nesnesini alın:</span><span class="sxs-lookup"><span data-stu-id="7fabf-116">To get the line items for the specified invoice, retrieve the invoice object:</span></span>

1. <span data-ttu-id="7fabf-117">Belirtilen faturaya yönelik işlemleri faturalamak için bir arabirim almak üzere [**Byıd**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-117">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="7fabf-118">Fatura nesnesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-118">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="7fabf-119">Fatura nesnesi belirtilen faturaya ait tüm bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="7fabf-119">The invoice object contains all of the information for the specified invoice:</span></span>

- <span data-ttu-id="7fabf-120">**Sağlayıcı** , faturalandırılmamış ayrıntı bilgisinin kaynağını tanımlar (örneğin, **Onetime**).</span><span class="sxs-lookup"><span data-stu-id="7fabf-120">**Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span>

- <span data-ttu-id="7fabf-121">**Fatura Elineıtemtype** türü belirtir (örneğin, **Billinglineıtem**).</span><span class="sxs-lookup"><span data-stu-id="7fabf-121">**InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="7fabf-122">Bir **InvoiceDetail** örneğine karşılık gelen satır öğelerinin bir koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="7fabf-122">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="7fabf-123">Örneğe ait BillingProvider ve ınvoineıtemtype 'ı [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="7fabf-123">Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="7fabf-124">İlişkili satır öğelerini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-124">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>

3. <span data-ttu-id="7fabf-125">Koleksiyonda çapraz geçiş yapmak için bir Numaralandırıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7fabf-125">Create an enumerator to traverse the collection.</span></span> <span data-ttu-id="7fabf-126">Örnek için aşağıdaki örnek koda bakın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-126">For an example, see the following sample code.</span></span>

<span data-ttu-id="7fabf-127">Aşağıdaki örnek kod, **ınvogıtems** koleksiyonunu işlemek için bir **foreach** döngüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="7fabf-127">The following sample code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="7fabf-128">Her bir **Faturaöğeside** her bir faturaya ait ayrı bir satır öğesi koleksiyonu alınır.</span><span class="sxs-lookup"><span data-stu-id="7fabf-128">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string currencyCode;
// string period;
// int pageMaxSizeReconLineItems = 2000;

// all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

var seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Get();

var fetchNext = true;

ConsoleKeyInfo keyInfo;

var itemNumber = 1;
while (fetchNext)
{
    Console.Out.WriteLine("\tLine line items count: " + seekBasedResourceCollection.Items.Count());

    seekBasedResourceCollection.Items.ToList().ForEach(item =>
    {
        // Instance of type OneTimeInvoiceLineItem
        if (item is OneTimeInvoiceLineItem)
        {
            Type t = typeof(OneTimeInvoiceLineItem);
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
            seekBasedResourceCollection = scopedPartnerOperations.Invoices.ById("unbilled").By("onetime", "billinglineitems", currencyCode, period, pageMaxSizeReconLineItems).Seek(seekBasedResourceCollection.ContinuationToken, SeekOperation.Next);
        }
    }
}
```

<span data-ttu-id="7fabf-129">Benzer bir örnek için bkz.:</span><span class="sxs-lookup"><span data-stu-id="7fabf-129">For a similar example, see:</span></span>

- <span data-ttu-id="7fabf-130">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7fabf-130">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7fabf-131">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="7fabf-131">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="7fabf-132">Sınıf: **GetUnBilledReconLineItemsPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="7fabf-132">Class: **GetUnBilledReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7fabf-133">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7fabf-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7fabf-134">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7fabf-134">Request syntax</span></span>

<span data-ttu-id="7fabf-135">Kullanım durumunuza bağlı olarak REST isteğiniz için aşağıdaki sözdizimleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="7fabf-135">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="7fabf-136">Daha fazla bilgi için her bir sözdizimi için açıklamalara bakın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-136">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="7fabf-137">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7fabf-137">Method</span></span>  | <span data-ttu-id="7fabf-138">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7fabf-138">Request URI</span></span>            | <span data-ttu-id="7fabf-139">Sözdizimi kullanım durumunun açıklaması</span><span class="sxs-lookup"><span data-stu-id="7fabf-139">Description of syntax use case</span></span>                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7fabf-140">**Al**</span><span class="sxs-lookup"><span data-stu-id="7fabf-140">**GET**</span></span> | <span data-ttu-id="7fabf-141">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvogıtemtype = billinglineıtems&CurrencyCode = {currencycode} &period = {PERIOD} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7fabf-141">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="7fabf-142">Verilen faturaya ait her satır öğesinin tam listesini döndürmek için bu sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-142">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="7fabf-143">**Al**</span><span class="sxs-lookup"><span data-stu-id="7fabf-143">**GET**</span></span> | <span data-ttu-id="7fabf-144">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvoyıtemtype = billinglineıtems&CurrencyCode = {currencycode} &period = {period} &boyut = {SIZE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7fabf-144">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="7fabf-145">Büyük faturalar için bu sözdizimini belirtilen boyut ve 0 tabanlı uzaklığa göre kullanarak satır öğelerinin sayfalandırılmış bir listesini döndürün.</span><span class="sxs-lookup"><span data-stu-id="7fabf-145">For large invoices, use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="7fabf-146">**Al**</span><span class="sxs-lookup"><span data-stu-id="7fabf-146">**GET**</span></span> | <span data-ttu-id="7fabf-147">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvogıtemtype = billinglineıtems&CurrencyCode = {currencycode} &period = {period} &boyut = {size} &Seekoperation = ileri</span><span class="sxs-lookup"><span data-stu-id="7fabf-147">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="7fabf-148">Kullanılarak mutabakat satır öğelerinin sonraki sayfasını almak için bu sözdizimini kullanın `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="7fabf-148">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="7fabf-149">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="7fabf-149">URI parameters</span></span>

<span data-ttu-id="7fabf-150">İsteği oluştururken aşağıdaki URI ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-150">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="7fabf-151">Ad</span><span class="sxs-lookup"><span data-stu-id="7fabf-151">Name</span></span>                   | <span data-ttu-id="7fabf-152">Tür</span><span class="sxs-lookup"><span data-stu-id="7fabf-152">Type</span></span>   | <span data-ttu-id="7fabf-153">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7fabf-153">Required</span></span> | <span data-ttu-id="7fabf-154">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7fabf-154">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="7fabf-155">Fatura kimliği</span><span class="sxs-lookup"><span data-stu-id="7fabf-155">invoice-id</span></span>             | <span data-ttu-id="7fabf-156">string</span><span class="sxs-lookup"><span data-stu-id="7fabf-156">string</span></span> | <span data-ttu-id="7fabf-157">Yes</span><span class="sxs-lookup"><span data-stu-id="7fabf-157">Yes</span></span>      | <span data-ttu-id="7fabf-158">Faturayı tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="7fabf-158">A string that identifies the invoice.</span></span> <span data-ttu-id="7fabf-159">Faturalandırılmamış tahminleri almak için ' faturalandırılmamış ' kullanın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-159">Use 'unbilled' to get unbilled estimates.</span></span> |
| <span data-ttu-id="7fabf-160">sağlayıcısını</span><span class="sxs-lookup"><span data-stu-id="7fabf-160">provider</span></span>               | <span data-ttu-id="7fabf-161">string</span><span class="sxs-lookup"><span data-stu-id="7fabf-161">string</span></span> | <span data-ttu-id="7fabf-162">Yes</span><span class="sxs-lookup"><span data-stu-id="7fabf-162">Yes</span></span>      | <span data-ttu-id="7fabf-163">Sağlayıcı: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="7fabf-163">The provider: "OneTime".</span></span>                                                |
| <span data-ttu-id="7fabf-164">fatura-satır-öğe türü</span><span class="sxs-lookup"><span data-stu-id="7fabf-164">invoice-line-item-type</span></span> | <span data-ttu-id="7fabf-165">string</span><span class="sxs-lookup"><span data-stu-id="7fabf-165">string</span></span> | <span data-ttu-id="7fabf-166">Yes</span><span class="sxs-lookup"><span data-stu-id="7fabf-166">Yes</span></span>      | <span data-ttu-id="7fabf-167">Fatura ayrıntısı türü: "Billinglineıtems".</span><span class="sxs-lookup"><span data-stu-id="7fabf-167">The type of invoice detail: "BillingLineItems".</span></span>               |
| <span data-ttu-id="7fabf-168">Haspartnerearnedkrediyi</span><span class="sxs-lookup"><span data-stu-id="7fabf-168">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="7fabf-169">bool</span><span class="sxs-lookup"><span data-stu-id="7fabf-169">bool</span></span>   | <span data-ttu-id="7fabf-170">No</span><span class="sxs-lookup"><span data-stu-id="7fabf-170">No</span></span>       | <span data-ttu-id="7fabf-171">Ortak kazanılan kredi uygulanmış olan satır öğelerinin döndürülmeyeceğini belirten değer.</span><span class="sxs-lookup"><span data-stu-id="7fabf-171">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="7fabf-172">Note: Bu parametre yalnızca sağlayıcı türü OneTime olduğunda ve Faturaınıneıtemtype 'ın Usagelineıtems olması durumunda uygulanır.</span><span class="sxs-lookup"><span data-stu-id="7fabf-172">Note: this parameter will be only applied when provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span>
| <span data-ttu-id="7fabf-173">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7fabf-173">currencyCode</span></span>           | <span data-ttu-id="7fabf-174">string</span><span class="sxs-lookup"><span data-stu-id="7fabf-174">string</span></span> | <span data-ttu-id="7fabf-175">Yes</span><span class="sxs-lookup"><span data-stu-id="7fabf-175">Yes</span></span>      | <span data-ttu-id="7fabf-176">Faturalandırılmamış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="7fabf-176">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="7fabf-177">dönem</span><span class="sxs-lookup"><span data-stu-id="7fabf-177">period</span></span>                 | <span data-ttu-id="7fabf-178">string</span><span class="sxs-lookup"><span data-stu-id="7fabf-178">string</span></span> | <span data-ttu-id="7fabf-179">Yes</span><span class="sxs-lookup"><span data-stu-id="7fabf-179">Yes</span></span>      | <span data-ttu-id="7fabf-180">Faturalandırılmamış keşfi için dönem.</span><span class="sxs-lookup"><span data-stu-id="7fabf-180">The period for unbilled recon.</span></span> <span data-ttu-id="7fabf-181">Örnek: geçerli, önceki.</span><span class="sxs-lookup"><span data-stu-id="7fabf-181">example: current, previous.</span></span>                      |
| <span data-ttu-id="7fabf-182">boyut</span><span class="sxs-lookup"><span data-stu-id="7fabf-182">size</span></span>                   | <span data-ttu-id="7fabf-183">sayı</span><span class="sxs-lookup"><span data-stu-id="7fabf-183">number</span></span> | <span data-ttu-id="7fabf-184">No</span><span class="sxs-lookup"><span data-stu-id="7fabf-184">No</span></span>       | <span data-ttu-id="7fabf-185">Döndürülecek en fazla öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="7fabf-185">The maximum number of items to return.</span></span> <span data-ttu-id="7fabf-186">Varsayılan boyut 2000 ' dir</span><span class="sxs-lookup"><span data-stu-id="7fabf-186">Default size is 2000</span></span>                     |
| <span data-ttu-id="7fabf-187">seekOperation</span><span class="sxs-lookup"><span data-stu-id="7fabf-187">seekOperation</span></span>          | <span data-ttu-id="7fabf-188">dize</span><span class="sxs-lookup"><span data-stu-id="7fabf-188">string</span></span> | <span data-ttu-id="7fabf-189">No</span><span class="sxs-lookup"><span data-stu-id="7fabf-189">No</span></span>       | <span data-ttu-id="7fabf-190">Keşfi satır öğelerinin sonraki sayfasını almak için seekOperation = Next öğesini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-190">Set seekOperation=Next to get the next page of recon line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="7fabf-191">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7fabf-191">Request headers</span></span>

<span data-ttu-id="7fabf-192">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7fabf-192">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7fabf-193">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7fabf-193">Request body</span></span>

<span data-ttu-id="7fabf-194">Yok.</span><span class="sxs-lookup"><span data-stu-id="7fabf-194">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="7fabf-195">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7fabf-195">REST response</span></span>

<span data-ttu-id="7fabf-196">Başarılı olursa, yanıt satır öğesi ayrıntıları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="7fabf-196">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="7fabf-197">*Satır **öğesi için**, **satın alma** değeri **Yeni** ile eşlenir ve değer **iadesi** **iptal** edilecek şekilde eşlenir.*</span><span class="sxs-lookup"><span data-stu-id="7fabf-197">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7fabf-198">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7fabf-198">Response success and error codes</span></span>

<span data-ttu-id="7fabf-199">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7fabf-199">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7fabf-200">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7fabf-200">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7fabf-201">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7fabf-201">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="request-response-examples"></a><span data-ttu-id="7fabf-202">İstek-yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="7fabf-202">Request-response examples</span></span>

#### <a name="request-response-example-1"></a><span data-ttu-id="7fabf-203">İstek-yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="7fabf-203">Request-response example 1</span></span>

<span data-ttu-id="7fabf-204">Aşağıdaki ayrıntılar Bu örnek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="7fabf-204">The following details apply to this example:</span></span>

- <span data-ttu-id="7fabf-205">Sağlayıcı: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="7fabf-205">Provider: **OneTime**</span></span>
- <span data-ttu-id="7fabf-206">Fatura Elineıtemtype: **Billinglineıtems**</span><span class="sxs-lookup"><span data-stu-id="7fabf-206">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="7fabf-207">Dönem: **önceki**</span><span class="sxs-lookup"><span data-stu-id="7fabf-207">Period: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="7fabf-208">İstek örneği 1</span><span class="sxs-lookup"><span data-stu-id="7fabf-208">Request example 1</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1//invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-1"></a><span data-ttu-id="7fabf-209">Yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="7fabf-209">Response example 1</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "HJVtMZMkgQ2miuCiNv0RSr51zQDans0m1",
            "orderDate": "2019-02-04T17:59:52.9460102Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0002",
            "availabilityId": "DZH318Z0BP8B",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Medium Plan",
            "chargeType": "New",
            "unitPrice": 820,
            "effectiveUnitPrice": 820,
            "unitType": "",
            "quantity": 1,
            "subtotal": 820,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-9cf0-4a1f-9514-7fcc7fe9d1fe",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 3.1618,
            "meterDescription": "Bandwidth - Data Transfer In (GB) - Zone 2",
            "reservationOrderId": "883d475b-0000-1234-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": "883d475b-0000-2222-0000-8818752f1234",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000&seekOperation=Next",
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

### <a name="request-response-example-2"></a><span data-ttu-id="7fabf-210">İstek-yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="7fabf-210">Request-response example 2</span></span>

<span data-ttu-id="7fabf-211">Aşağıdaki ayrıntılar Bu örnek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="7fabf-211">The following details apply to this example:</span></span>

- <span data-ttu-id="7fabf-212">Sağlayıcı: **Onetime**</span><span class="sxs-lookup"><span data-stu-id="7fabf-212">Provider: **OneTime**</span></span>
- <span data-ttu-id="7fabf-213">Fatura Elineıtemtype: **Billinglineıtems**</span><span class="sxs-lookup"><span data-stu-id="7fabf-213">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="7fabf-214">Dönem: **önceki**</span><span class="sxs-lookup"><span data-stu-id="7fabf-214">Period: **Previous**</span></span>
- <span data-ttu-id="7fabf-215">SeekOperation: **İleri**</span><span class="sxs-lookup"><span data-stu-id="7fabf-215">SeekOperation: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="7fabf-216">İstek örneği 2</span><span class="sxs-lookup"><span data-stu-id="7fabf-216">Request example 2</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=onetime&invoiceLineItemType=billinglineitems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-2"></a><span data-ttu-id="7fabf-217">Yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="7fabf-217">Response example 2</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "1234567",
            "resellerMpnId": 0,
            "orderId": "Oi2kwDPEOyGEFUkESk3QR4XSxcpvwp1x1",
            "orderDate": "2019-02-04T17:59:53.1628078Z",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "skuName": "Test WaaS - Large Plan",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "publisherName": "Test Networks, Inc.",
            "publisherId": "21223810",
            "subscriptionDescription": "",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "priceAdjustmentDescription": "[\"15.0% Partner earned credit for services managed\",\"100.0% Tier 1 Discount\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": 1,
            "pcToBCExchangeRateDate": "2019-08-01T00:00:00Z",
            "billableQuantity": 0.737083,
            "meterDescription": "",
            "reservationOrderId": ""
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```

#### <a name="request-example-3"></a><span data-ttu-id="7fabf-218">İstek örneği 3</span><span class="sxs-lookup"><span data-stu-id="7fabf-218">Request example 3</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/unbilled/lineitems?provider=OneTime&invoiceLineItemType=UsageLineItems&currencyCode=usd&period=previous&size=2000&seekoperation=next HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-ContinuationToken: d19617b8-fbe5-4684-a5d8-0230972fb0cf,0705c4a9-39f7-4261-ba6d-53e24a9ce47d_a4ayc/80/OGda4BO/1o/V0etpOqiLx1JwB5S3beHW0s=,0d81c700-98b4-4b13-9129-ffd5620f72e7
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

#### <a name="response-example-3"></a><span data-ttu-id="7fabf-219">Yanıt örneği 3</span><span class="sxs-lookup"><span data-stu-id="7fabf-219">Response example 3</span></span>

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
            "partnerId": "0c924e8d-4852-4692-a4d7-7dd0dc09ad80",
            "PartnerName": "testPartner",
            "customerId": "org:d7f565f5-5367-492f-a465-9e2057c5e3c3",
            "customerName": "TEST_TEST_GTM1",
            "customerDomainName": "TESTTESTGTM1.ccsctp.net",
            "invoiceNumber": "T11ETHHDDD",
            "productId": "DZH318Z0BXWC",
            "skuId": "0005",
            "availabilityId": "DZH318Z0BH9R",
            "productName": "Test WAF-as-a-Service",
            "publisherId": "21223810",
            "subscriptionId": "12345678-28db-48c2-8c30-04d7c9455746",
            "subscriptionDescription": "sub description",
            "chargeStartDate": "2019-02-04T09:22:34.6455294-08:00",
            "chargeEndDate": "2019-03-03T09:22:34.6455294-08:00",
            "UsageDate": "2019-02-07T09:22:34.6455294-08:00",
            "MeterType": "type",
            "MeterCategory": "category",
            "MeterId": "21312312312-fdsfsd",
            "MeterSubCategory": "subcategory",
            "MeterName": "meter name",
            "MeterRegion": "meter region",
            "UnitOfMeasure": "11",
            "skuName": "Test WaaS - Large Plan",
            "publisherName": "Test Networks, Inc.",
            "chargeType": "New",
            "unitPrice": 2598,
            "effectiveUnitPrice": 2598,
            "unitType": "",
            "quantity": 1,
            "subtotal": 2598,
            "taxTotal": 0,
            "totalForCustomer": 0,
            "currency": "USD",
            "termAndBillingCycle": "1 Month Subscription",
            "alternateId": "123456ad566",
            "discountDetails": "",
            "providerSource": "All",
            "RateOfPartnerEarnedCredit": 0.15,
            "IsPartnerEarnedCreditApplied": true,
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        }
    ],
    "links": {
        "self": {
             "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=usd&period=previous&size=2000",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
