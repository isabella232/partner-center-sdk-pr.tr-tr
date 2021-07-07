---
title: Faturanın faturalandırılmamış mutabakat satırı öğelerini Al
description: Iş Ortağı Merkezi API 'Lerini kullanarak, belirtilen dönem için faturalandırılmamış mutabakat satır öğesi ayrıntılarının koleksiyonunu alabilirsiniz.
ms.date: 01/27/2020
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: 5ab7dde0d78e8ff15bb1a960b16c8c925b0478ce
ms.sourcegitcommit: c5acfb373aa012eb3b6c17182f7ca56883502c6b
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/19/2021
ms.locfileid: "112391300"
---
# <a name="get-invoices-unbilled-reconciliation-line-items"></a><span data-ttu-id="924da-103">Faturanın faturalandırılmamış mutabakat satırı öğelerini Al</span><span class="sxs-lookup"><span data-stu-id="924da-103">Get invoice's unbilled reconciliation line items</span></span>

<span data-ttu-id="924da-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="924da-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="924da-105">Aşağıdaki yöntemleri kullanarak, faturalandırılmamış fatura satırı öğeleri (açık faturalandırma satırı öğeleri olarak da bilinir) için bir ayrıntılar koleksiyonu alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="924da-105">You can use the following methods get a collection of details for unbilled invoice line items (also known as open billing line items).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="924da-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="924da-106">Prerequisites</span></span>

- <span data-ttu-id="924da-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="924da-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="924da-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="924da-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="924da-109">Bir fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="924da-109">An invoice identifier.</span></span> <span data-ttu-id="924da-110">Bu, satır öğelerinin alınacağı faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="924da-110">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="924da-111">C\#</span><span class="sxs-lookup"><span data-stu-id="924da-111">C\#</span></span>

<span data-ttu-id="924da-112">Belirtilen faturaya ait satır öğelerini almak için fatura nesnesini alın:</span><span class="sxs-lookup"><span data-stu-id="924da-112">To get the line items for the specified invoice, retrieve the invoice object:</span></span>

1. <span data-ttu-id="924da-113">Belirtilen faturaya yönelik işlemleri faturalamak için bir arabirim almak üzere [**Byıd**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="924da-113">Call the [**ById**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.byid) method to get an interface to invoice operations for the specified invoice.</span></span>

2. <span data-ttu-id="924da-114">Fatura nesnesini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="924da-114">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the invoice object.</span></span>

<span data-ttu-id="924da-115">Fatura nesnesi belirtilen faturaya ait tüm bilgileri içerir:</span><span class="sxs-lookup"><span data-stu-id="924da-115">The invoice object contains all of the information for the specified invoice:</span></span>

- <span data-ttu-id="924da-116">**Sağlayıcı** , faturalandırılmamış ayrıntı bilgisinin kaynağını tanımlar (örneğin, **Onetime**).</span><span class="sxs-lookup"><span data-stu-id="924da-116">**Provider** identifies the source of the unbilled detail information (for example, **OneTime**).</span></span>

- <span data-ttu-id="924da-117">**Fatura Elineıtemtype** türü belirtir (örneğin, **Billinglineıtem**).</span><span class="sxs-lookup"><span data-stu-id="924da-117">**InvoiceLineItemType** specifies the type (for example, **BillingLineItem**).</span></span>

<span data-ttu-id="924da-118">Bir **InvoiceDetail** örneğine karşılık gelen satır öğelerinin bir koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="924da-118">To get a collection of line items that correspond to an **InvoiceDetail** instance:</span></span>

1. <span data-ttu-id="924da-119">Örneğe ait BillingProvider ve ınvoineıtemtype 'ı [**by**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="924da-119">Pass the instance's BillingProvider and InvoiceLineItemType to the [**By**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.by) method.</span></span>

2. <span data-ttu-id="924da-120">İlişkili satır öğelerini almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="924da-120">Call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoice.getasync) method to retrieve the associated line items.</span></span>

3. <span data-ttu-id="924da-121">Koleksiyonda çapraz geçiş yapmak için bir Numaralandırıcı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="924da-121">Create an enumerator to traverse the collection.</span></span> <span data-ttu-id="924da-122">Örnek için aşağıdaki örnek koda bakın.</span><span class="sxs-lookup"><span data-stu-id="924da-122">For an example, see the following sample code.</span></span>

<span data-ttu-id="924da-123">Aşağıdaki örnek kod, **ınvogıtems** koleksiyonunu işlemek için bir **foreach** döngüsü kullanır.</span><span class="sxs-lookup"><span data-stu-id="924da-123">The following sample code uses a **foreach** loop to process the **InvoiceLineItems** collection.</span></span> <span data-ttu-id="924da-124">Her bir **Faturaöğeside** her bir faturaya ait ayrı bir satır öğesi koleksiyonu alınır.</span><span class="sxs-lookup"><span data-stu-id="924da-124">A separate collection of line items is retrieved for each **InvoiceLineItemType**.</span></span>

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

<span data-ttu-id="924da-125">Benzer bir örnek için bkz.:</span><span class="sxs-lookup"><span data-stu-id="924da-125">For a similar example, see:</span></span>

- <span data-ttu-id="924da-126">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="924da-126">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="924da-127">Project: **iş ortağı merkezi SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="924da-127">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="924da-128">Sınıf: **GetUnBilledReconLineItemsPaging. cs**</span><span class="sxs-lookup"><span data-stu-id="924da-128">Class: **GetUnBilledReconLineItemsPaging.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="924da-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="924da-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="924da-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="924da-130">Request syntax</span></span>

<span data-ttu-id="924da-131">Kullanım durumunuza bağlı olarak REST isteğiniz için aşağıdaki sözdizimleri kullanılabilir.</span><span class="sxs-lookup"><span data-stu-id="924da-131">You can use the following syntaxes for your REST request, depending on your use case.</span></span> <span data-ttu-id="924da-132">Daha fazla bilgi için her bir sözdizimi için açıklamalara bakın.</span><span class="sxs-lookup"><span data-stu-id="924da-132">For more information, see the descriptions for each syntax.</span></span>

 | <span data-ttu-id="924da-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="924da-133">Method</span></span>  | <span data-ttu-id="924da-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="924da-134">Request URI</span></span>            | <span data-ttu-id="924da-135">Sözdizimi kullanım durumunun açıklaması</span><span class="sxs-lookup"><span data-stu-id="924da-135">Description of syntax use case</span></span>                                                                                |
|---------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="924da-136">**Al**</span><span class="sxs-lookup"><span data-stu-id="924da-136">**GET**</span></span> | <span data-ttu-id="924da-137">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvogıtemtype = billinglineıtems&CurrencyCode = {currencycode} &period = {PERIOD} http/1.1</span><span class="sxs-lookup"><span data-stu-id="924da-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period} HTTP/1.1</span></span>                              | <span data-ttu-id="924da-138">Verilen faturaya ait her satır öğesinin tam listesini döndürmek için bu sözdizimini kullanın.</span><span class="sxs-lookup"><span data-stu-id="924da-138">Use this syntax to return a full list of every line item for the given invoice.</span></span> |
| <span data-ttu-id="924da-139">**Al**</span><span class="sxs-lookup"><span data-stu-id="924da-139">**GET**</span></span> | <span data-ttu-id="924da-140">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvoyıtemtype = billinglineıtems&CurrencyCode = {currencycode} &period = {period} &boyut = {SIZE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="924da-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size} HTTP/1.1</span></span>  | <span data-ttu-id="924da-141">Büyük faturalar için bu sözdizimini belirtilen boyut ve 0 tabanlı uzaklığa göre kullanarak satır öğelerinin sayfalandırılmış bir listesini döndürün.</span><span class="sxs-lookup"><span data-stu-id="924da-141">For large invoices, use this syntax with a specified size and 0-based offset to return a paged list of line items.</span></span> |
| <span data-ttu-id="924da-142">**Al**</span><span class="sxs-lookup"><span data-stu-id="924da-142">**GET**</span></span> | <span data-ttu-id="924da-143">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{Invoice-ID}/LineItems? Provider = onetime&ınvogıtemtype = billinglineıtems&CurrencyCode = {currencycode} &period = {period} &boyut = {size} &Seekoperation = ileri</span><span class="sxs-lookup"><span data-stu-id="924da-143">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/lineitems?provider=onetime&invoicelineitemtype=billinglineitems&currencycode={currencycode}&period={period}&size={size}&seekOperation=Next</span></span>                               | <span data-ttu-id="924da-144">Kullanılarak mutabakat satır öğelerinin sonraki sayfasını almak için bu sözdizimini kullanın `seekOperation = "Next"` .</span><span class="sxs-lookup"><span data-stu-id="924da-144">Use this syntax to get the next page of reconciliation line items using `seekOperation = "Next"`.</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="924da-145">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="924da-145">URI parameters</span></span>

<span data-ttu-id="924da-146">İsteği oluştururken aşağıdaki URI ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="924da-146">Use the following URI and query parameters when creating the request.</span></span>

| <span data-ttu-id="924da-147">Ad</span><span class="sxs-lookup"><span data-stu-id="924da-147">Name</span></span>                   | <span data-ttu-id="924da-148">Tür</span><span class="sxs-lookup"><span data-stu-id="924da-148">Type</span></span>   | <span data-ttu-id="924da-149">Gerekli</span><span class="sxs-lookup"><span data-stu-id="924da-149">Required</span></span> | <span data-ttu-id="924da-150">Açıklama</span><span class="sxs-lookup"><span data-stu-id="924da-150">Description</span></span>                                                                     |
|------------------------|--------|----------|---------------------------------------------------------------------------------|
| <span data-ttu-id="924da-151">Fatura kimliği</span><span class="sxs-lookup"><span data-stu-id="924da-151">invoice-id</span></span>             | <span data-ttu-id="924da-152">string</span><span class="sxs-lookup"><span data-stu-id="924da-152">string</span></span> | <span data-ttu-id="924da-153">Yes</span><span class="sxs-lookup"><span data-stu-id="924da-153">Yes</span></span>      | <span data-ttu-id="924da-154">Faturayı tanımlayan bir dize.</span><span class="sxs-lookup"><span data-stu-id="924da-154">A string that identifies the invoice.</span></span> <span data-ttu-id="924da-155">Faturalandırılmamış tahminleri almak için ' faturalandırılmamış ' kullanın.</span><span class="sxs-lookup"><span data-stu-id="924da-155">Use 'unbilled' to get unbilled estimates.</span></span> |
| <span data-ttu-id="924da-156">sağlayıcısını</span><span class="sxs-lookup"><span data-stu-id="924da-156">provider</span></span>               | <span data-ttu-id="924da-157">string</span><span class="sxs-lookup"><span data-stu-id="924da-157">string</span></span> | <span data-ttu-id="924da-158">Yes</span><span class="sxs-lookup"><span data-stu-id="924da-158">Yes</span></span>      | <span data-ttu-id="924da-159">Sağlayıcı: "OneTime".</span><span class="sxs-lookup"><span data-stu-id="924da-159">The provider: "OneTime".</span></span>                                                |
| <span data-ttu-id="924da-160">fatura-satır-öğe türü</span><span class="sxs-lookup"><span data-stu-id="924da-160">invoice-line-item-type</span></span> | <span data-ttu-id="924da-161">string</span><span class="sxs-lookup"><span data-stu-id="924da-161">string</span></span> | <span data-ttu-id="924da-162">Yes</span><span class="sxs-lookup"><span data-stu-id="924da-162">Yes</span></span>      | <span data-ttu-id="924da-163">Fatura ayrıntısı türü: "Billinglineıtems".</span><span class="sxs-lookup"><span data-stu-id="924da-163">The type of invoice detail: "BillingLineItems".</span></span>               |
| <span data-ttu-id="924da-164">Haspartnerearnedkrediyi</span><span class="sxs-lookup"><span data-stu-id="924da-164">hasPartnerEarnedCredit</span></span> | <span data-ttu-id="924da-165">bool</span><span class="sxs-lookup"><span data-stu-id="924da-165">bool</span></span>   | <span data-ttu-id="924da-166">Hayır</span><span class="sxs-lookup"><span data-stu-id="924da-166">No</span></span>       | <span data-ttu-id="924da-167">Ortak kazanılan kredi uygulanmış olan satır öğelerinin döndürülmeyeceğini belirten değer.</span><span class="sxs-lookup"><span data-stu-id="924da-167">The value indicating if to return the line items with partner earned credit applied.</span></span> <span data-ttu-id="924da-168">Note: Bu parametre yalnızca sağlayıcı türü OneTime olduğunda ve Faturaınıneıtemtype 'ın Usagelineıtems olması durumunda uygulanır.</span><span class="sxs-lookup"><span data-stu-id="924da-168">Note: this parameter will be only applied when provider type is OneTime and InvoiceLineItemType is UsageLineItems.</span></span>
| <span data-ttu-id="924da-169">currencyCode</span><span class="sxs-lookup"><span data-stu-id="924da-169">currencyCode</span></span>           | <span data-ttu-id="924da-170">string</span><span class="sxs-lookup"><span data-stu-id="924da-170">string</span></span> | <span data-ttu-id="924da-171">Yes</span><span class="sxs-lookup"><span data-stu-id="924da-171">Yes</span></span>      | <span data-ttu-id="924da-172">Faturalandırılmamış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="924da-172">The currency code for the unbilled line items.</span></span>                                  |
| <span data-ttu-id="924da-173">dönem</span><span class="sxs-lookup"><span data-stu-id="924da-173">period</span></span>                 | <span data-ttu-id="924da-174">string</span><span class="sxs-lookup"><span data-stu-id="924da-174">string</span></span> | <span data-ttu-id="924da-175">Yes</span><span class="sxs-lookup"><span data-stu-id="924da-175">Yes</span></span>      | <span data-ttu-id="924da-176">Faturalandırılmamış keşfi için dönem.</span><span class="sxs-lookup"><span data-stu-id="924da-176">The period for unbilled recon.</span></span> <span data-ttu-id="924da-177">Örnek: geçerli, önceki.</span><span class="sxs-lookup"><span data-stu-id="924da-177">example: current, previous.</span></span>                      |
| <span data-ttu-id="924da-178">boyut</span><span class="sxs-lookup"><span data-stu-id="924da-178">size</span></span>                   | <span data-ttu-id="924da-179">sayı</span><span class="sxs-lookup"><span data-stu-id="924da-179">number</span></span> | <span data-ttu-id="924da-180">Hayır</span><span class="sxs-lookup"><span data-stu-id="924da-180">No</span></span>       | <span data-ttu-id="924da-181">Döndürülecek en fazla öğe sayısı.</span><span class="sxs-lookup"><span data-stu-id="924da-181">The maximum number of items to return.</span></span> <span data-ttu-id="924da-182">Varsayılan boyut 2000 ' dir</span><span class="sxs-lookup"><span data-stu-id="924da-182">Default size is 2000</span></span>                     |
| <span data-ttu-id="924da-183">seekOperation</span><span class="sxs-lookup"><span data-stu-id="924da-183">seekOperation</span></span>          | <span data-ttu-id="924da-184">dize</span><span class="sxs-lookup"><span data-stu-id="924da-184">string</span></span> | <span data-ttu-id="924da-185">No</span><span class="sxs-lookup"><span data-stu-id="924da-185">No</span></span>       | <span data-ttu-id="924da-186">Keşfi satır öğelerinin sonraki sayfasını almak için seekOperation = Next öğesini ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="924da-186">Set seekOperation=Next to get the next page of recon line items.</span></span>                |

### <a name="request-headers"></a><span data-ttu-id="924da-187">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="924da-187">Request headers</span></span>

<span data-ttu-id="924da-188">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="924da-188">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="924da-189">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="924da-189">Request body</span></span>

<span data-ttu-id="924da-190">Yok.</span><span class="sxs-lookup"><span data-stu-id="924da-190">None.</span></span>

## <a name="rest-response"></a><span data-ttu-id="924da-191">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="924da-191">REST response</span></span>

<span data-ttu-id="924da-192">Başarılı olursa, yanıt satır öğesi ayrıntıları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="924da-192">If successful, the response contains the collection of line item details.</span></span>

<span data-ttu-id="924da-193">*Satır **öğesi için**, **satın alma** değeri **Yeni** ile eşlenir ve değer **iadesi** **iptal** edilecek şekilde eşlenir.*</span><span class="sxs-lookup"><span data-stu-id="924da-193">*For the line item **ChargeType**, the value **Purchase** is mapped to **New** and the value **Refund** is mapped to **Cancel**.*</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="924da-194">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="924da-194">Response success and error codes</span></span>

<span data-ttu-id="924da-195">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="924da-195">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="924da-196">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="924da-196">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="924da-197">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="924da-197">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="request-response-examples"></a><span data-ttu-id="924da-198">İstek-yanıt örnekleri</span><span class="sxs-lookup"><span data-stu-id="924da-198">Request-response examples</span></span>

#### <a name="request-response-example-1"></a><span data-ttu-id="924da-199">İstek-yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="924da-199">Request-response example 1</span></span>

<span data-ttu-id="924da-200">Aşağıdaki ayrıntılar Bu örnek için geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="924da-200">The following details apply to this example:</span></span>

- <span data-ttu-id="924da-201">Sağlayıcı: **OneTime**</span><span class="sxs-lookup"><span data-stu-id="924da-201">Provider: **OneTime**</span></span>
- <span data-ttu-id="924da-202">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="924da-202">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="924da-203">Dönem: **Önceki**</span><span class="sxs-lookup"><span data-stu-id="924da-203">Period: **Previous**</span></span>

#### <a name="request-example-1"></a><span data-ttu-id="924da-204">İstek örneği 1</span><span class="sxs-lookup"><span data-stu-id="924da-204">Request example 1</span></span>

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

#### <a name="response-example-1"></a><span data-ttu-id="924da-205">Yanıt örneği 1</span><span class="sxs-lookup"><span data-stu-id="924da-205">Response example 1</span></span>

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
   "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "4649221",
            "orderId": "94e858b6d855",
            "orderDate": "2021-05-20T18:30:06.6045692Z",
            "productId": "CFQ7TTC0LH0R",
            "skuId": "0002",
            "availabilityId": "CFQ7TTC0K5RQ",
            "productName": "Microsoft 365 Phone System - Virtual User",
            "skuName": "Microsoft 365 Phone System - Virtual User",
            "productQualifiers": [
                "AddOn",
                "Trial"
            ],
            "chargeType": "new",
            "unitPrice": "0",
            "effectiveUnitPrice": "0",
            "unitType": "",
            "quantity": "25",
            "subtotal": "0",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "86646af9-e80a-4aa0-da80-3fd2b792c2cc",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2021-06-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Month commitment for trial",
            "alternateId": "94e858b6d855",
            "referenceId": "0cf1202a-5b7d-4219-966e-93c637113708",
            "priceAdjustmentDescription": "",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "25",
            "meterDescription": "",
            "billingFrequency": "",
            "reservationOrderId": "99f246cf-ed96-41b4-b0cd-0aa43eb1fe91",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
            
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "835a59a7-3172-47b5-bdef-d9cc65f4d0e4",
            "customerName": "TEST_TEST Test Promotions 01",
            "customerDomainName": "kyletestpromos01.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "0",
            "orderId": "5f9d52bb1408",
            "orderDate": "2021-05-20T18:48:30.6168285Z",
            "productId": "CFQ7TTC0HL8W",
            "skuId": "0001",
            "availabilityId": "CFQ7TTC0K59S",
            "productName": "Power BI Premium Per User",
            "skuName": "Power BI Premium Per User",
            "productQualifiers": [],
            "chargeType": "new",
            "unitPrice": "16",
            "effectiveUnitPrice": "14.4",
            "unitType": "",
            "quantity": "50",
            "subtotal": "720",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "9d7d1f3d-c8de-461c-db6d-91debd5129f0",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2022-05-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Year commitment for monthly/yearly billing",
            "alternateId": "5f9d52bb1408",
            "referenceId": "28b535e0-68f4-40b5-84f7-8ed9241eb149",
            "priceAdjustmentDescription": "[\"Price for given billing period\",\"You are getting a discount due to a pre-determined override.\",\"You are getting a discount for being a partner.\",\"You are getting a price guarantee for your price.\",\"Price for given term\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "50",
            "meterDescription": "",
            "billingFrequency": "Monthly",
            "reservationOrderId": "8fdebb4a-7110-496e-9570-623e4c992797",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "78bcf906-b945-4210-8818-cfb93caf12a1",
            "attributes/objectType": "OneTimeInvoiceLineItem",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
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
            "subscriptionStartDate": "2019-02-01T00:00:00Z",
            "subscriptionEndDate": "2020-01-31T00:00:00Z",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Year Subscription",
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
        }
    ]
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

### <a name="request-response-example-2"></a><span data-ttu-id="924da-206">İstek-yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="924da-206">Request-response example 2</span></span>

<span data-ttu-id="924da-207">Bu örnek için aşağıdaki ayrıntılar geçerlidir:</span><span class="sxs-lookup"><span data-stu-id="924da-207">The following details apply to this example:</span></span>

- <span data-ttu-id="924da-208">Sağlayıcı: **OneTime**</span><span class="sxs-lookup"><span data-stu-id="924da-208">Provider: **OneTime**</span></span>
- <span data-ttu-id="924da-209">InvoiceLineItemType: **BillingLineItems**</span><span class="sxs-lookup"><span data-stu-id="924da-209">InvoiceLineItemType: **BillingLineItems**</span></span>
- <span data-ttu-id="924da-210">Dönem: **Önceki**</span><span class="sxs-lookup"><span data-stu-id="924da-210">Period: **Previous**</span></span>
- <span data-ttu-id="924da-211">SeekOperation: **Sonraki**</span><span class="sxs-lookup"><span data-stu-id="924da-211">SeekOperation: **Next**</span></span>

#### <a name="request-example-2"></a><span data-ttu-id="924da-212">İstek örneği 2</span><span class="sxs-lookup"><span data-stu-id="924da-212">Request example 2</span></span>

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

#### <a name="response-example-2"></a><span data-ttu-id="924da-213">Yanıt örneği 2</span><span class="sxs-lookup"><span data-stu-id="924da-213">Response example 2</span></span>

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
   "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "4649221",
            "orderId": "94e858b6d855",
            "orderDate": "2021-05-20T18:30:06.6045692Z",
            "productId": "CFQ7TTC0LH0R",
            "skuId": "0002",
            "availabilityId": "CFQ7TTC0K5RQ",
            "productName": "Microsoft 365 Phone System - Virtual User",
            "skuName": "Microsoft 365 Phone System - Virtual User",
            "productQualifiers": [
                "AddOn",
                "Trial"
            ],
            "chargeType": "new",
            "unitPrice": "0",
            "effectiveUnitPrice": "0",
            "unitType": "",
            "quantity": "25",
            "subtotal": "0",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "86646af9-e80a-4aa0-da80-3fd2b792c2cc",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2021-06-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Month commitment for trial",
            "alternateId": "94e858b6d855",
            "referenceId": "0cf1202a-5b7d-4219-966e-93c637113708",
            "priceAdjustmentDescription": "",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "25",
            "meterDescription": "",
            "billingFrequency": "",
            "reservationOrderId": "99f246cf-ed96-41b4-b0cd-0aa43eb1fe91",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
            
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "835a59a7-3172-47b5-bdef-d9cc65f4d0e4",
            "customerName": "TEST_TEST Test Promotions 01",
            "customerDomainName": "kyletestpromos01.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "0",
            "orderId": "5f9d52bb1408",
            "orderDate": "2021-05-20T18:48:30.6168285Z",
            "productId": "CFQ7TTC0HL8W",
            "skuId": "0001",
            "availabilityId": "CFQ7TTC0K59S",
            "productName": "Power BI Premium Per User",
            "skuName": "Power BI Premium Per User",
            "productQualifiers": [],
            "chargeType": "new",
            "unitPrice": "16",
            "effectiveUnitPrice": "14.4",
            "unitType": "",
            "quantity": "50",
            "subtotal": "720",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "9d7d1f3d-c8de-461c-db6d-91debd5129f0",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2022-05-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Year commitment for monthly/yearly billing",
            "alternateId": "5f9d52bb1408",
            "referenceId": "28b535e0-68f4-40b5-84f7-8ed9241eb149",
            "priceAdjustmentDescription": "[\"Price for given billing period\",\"You are getting a discount due to a pre-determined override.\",\"You are getting a discount for being a partner.\",\"You are getting a price guarantee for your price.\",\"Price for given term\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "50",
            "meterDescription": "",
            "billingFrequency": "Monthly",
            "reservationOrderId": "8fdebb4a-7110-496e-9570-623e4c992797",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "78bcf906-b945-4210-8818-cfb93caf12a1",
            "attributes/objectType": "OneTimeInvoiceLineItem",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
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
            "subscriptionStartDate": "2019-02-01T00:00:00Z",
            "subscriptionEndDate": "2020-01-31T00:00:00Z",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Year Subscription",
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
        }
    ]
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

#### <a name="request-example-3"></a><span data-ttu-id="924da-214">İstek örneği 3</span><span class="sxs-lookup"><span data-stu-id="924da-214">Request example 3</span></span>

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

#### <a name="response-example-3"></a><span data-ttu-id="924da-215">Yanıt örneği 3</span><span class="sxs-lookup"><span data-stu-id="924da-215">Response example 3</span></span>

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
    "totalCount": 3,
    "items": [
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "4649221",
            "orderId": "94e858b6d855",
            "orderDate": "2021-05-20T18:30:06.6045692Z",
            "productId": "CFQ7TTC0LH0R",
            "skuId": "0002",
            "availabilityId": "CFQ7TTC0K5RQ",
            "productName": "Microsoft 365 Phone System - Virtual User",
            "skuName": "Microsoft 365 Phone System - Virtual User",
            "productQualifiers": [
                "AddOn",
                "Trial"
            ],
            "chargeType": "new",
            "unitPrice": "0",
            "effectiveUnitPrice": "0",
            "unitType": "",
            "quantity": "25",
            "subtotal": "0",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "86646af9-e80a-4aa0-da80-3fd2b792c2cc",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2021-06-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Month commitment for trial",
            "alternateId": "94e858b6d855",
            "referenceId": "0cf1202a-5b7d-4219-966e-93c637113708",
            "priceAdjustmentDescription": "",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "25",
            "meterDescription": "",
            "billingFrequency": "",
            "reservationOrderId": "99f246cf-ed96-41b4-b0cd-0aa43eb1fe91",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
            
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "835a59a7-3172-47b5-bdef-d9cc65f4d0e4",
            "customerName": "TEST_TEST Test Promotions 01",
            "customerDomainName": "kyletestpromos01.onmicrosoft.com",
            "customerCountry": "US",
            "invoiceNumber": "",
            "mpnId": "5357564",
            "resellerMpnId": "0",
            "orderId": "5f9d52bb1408",
            "orderDate": "2021-05-20T18:48:30.6168285Z",
            "productId": "CFQ7TTC0HL8W",
            "skuId": "0001",
            "availabilityId": "CFQ7TTC0K59S",
            "productName": "Power BI Premium Per User",
            "skuName": "Power BI Premium Per User",
            "productQualifiers": [],
            "chargeType": "new",
            "unitPrice": "16",
            "effectiveUnitPrice": "14.4",
            "unitType": "",
            "quantity": "50",
            "subtotal": "720",
            "taxTotal": "0",
            "totalForCustomer": "0",
            "currency": "USD",
            "publisherName": "Microsoft Corporation",
            "publisherId": "",
            "subscriptionDescription": "",
            "subscriptionId": "9d7d1f3d-c8de-461c-db6d-91debd5129f0",
            "subscriptionStartDate": "2021-05-20T00:00:00Z",
            "subscriptionEndDate": "2022-05-19T00:00:00Z",
            "chargeStartDate": "2021-05-20T00:00:00Z",
            "chargeEndDate": "2021-06-19T00:00:00Z",
            "termAndBillingCycle": "One-Year commitment for monthly/yearly billing",
            "alternateId": "5f9d52bb1408",
            "referenceId": "28b535e0-68f4-40b5-84f7-8ed9241eb149",
            "priceAdjustmentDescription": "[\"Price for given billing period\",\"You are getting a discount due to a pre-determined override.\",\"You are getting a discount for being a partner.\",\"You are getting a price guarantee for your price.\",\"Price for given term\"]",
            "discountDetails": "",
            "pricingCurrency": "USD",
            "pcToBCExchangeRate": "1",
            "pcToBCExchangeRateDate": "2021-05-01T00:00:00",
            "billableQuantity": "50",
            "meterDescription": "",
            "billingFrequency": "Monthly",
            "reservationOrderId": "8fdebb4a-7110-496e-9570-623e4c992797",
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "promotionId": "78bcf906-b945-4210-8818-cfb93caf12a1",
            "attributes/objectType": "OneTimeInvoiceLineItem",
            "attributes": {
                "objectType": "OneTimeInvoiceLineItem"
            }
        },
        {
            "partnerId": "934f3416-bc2f-47f3-b492-77e517d4e572",
            "customerId": "c139c4bf-2e8b-4ab5-8bed-d9f50dcca7a2",
            "customerName": "Test_Test_Office R2 Reduce Seats Validation",
            "customerDomainName": "testcustomerr2t2reduce.onmicrosoft.com",
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
            "subscriptionStartDate": "2019-02-01T00:00:00Z",
            "subscriptionEndDate": "2020-01-31T00:00:00Z",
            "chargeStartDate": "2019-02-04T09:22:40.1767993-08:00",
            "chargeEndDate": "2019-03-03T09:22:40.1767993-08:00",
            "termAndBillingCycle": "1 Year Subscription",
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
        }
    ]
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
