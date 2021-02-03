---
title: Faturaların koleksiyonunu alma
description: Ortağın faturalarının bir koleksiyonunu alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: sourishdeb
ms.author: sodeb
ms.openlocfilehash: f56c3de8dd227f573921e5b969c2217c2f743a21
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769287"
---
# <a name="get-a-collection-of-invoices"></a><span data-ttu-id="f310e-103">Faturaların koleksiyonunu alma</span><span class="sxs-lookup"><span data-stu-id="f310e-103">Get a collection of invoices</span></span>

<span data-ttu-id="f310e-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="f310e-104">**Applies To**</span></span>

- <span data-ttu-id="f310e-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f310e-105">Partner Center</span></span>
- <span data-ttu-id="f310e-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f310e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="f310e-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f310e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="f310e-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f310e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="f310e-109">Ortağın faturalarının bir koleksiyonunu alma.</span><span class="sxs-lookup"><span data-stu-id="f310e-109">How to retrieve a collection of the partner's invoices.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f310e-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f310e-110">Prerequisites</span></span>

- <span data-ttu-id="f310e-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f310e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f310e-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="f310e-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="f310e-113">C\#</span><span class="sxs-lookup"><span data-stu-id="f310e-113">C\#</span></span>

<span data-ttu-id="f310e-114">Tüm kullanılabilir faturaların bir koleksiyonunu almak için, fatura işlemleri için bir arabirim almak üzere [**faturalar**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) özelliğini kullanın ve ardından koleksiyonu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f310e-114">To get a collection of all available invoices, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then call the [**Get**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.get) or [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.getasync) method to retrieve the collection.</span></span>

<span data-ttu-id="f310e-115">Sayfalanmış faturaların toplanmasını sağlamak için, önce [**Buildındexedquery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) yöntemini çağırın ve bir [**ıquery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesi oluşturmak için bunu sayfa boyutuna geçirin.</span><span class="sxs-lookup"><span data-stu-id="f310e-115">To get a paged collection of invoices, first call the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method and pass it the page size to create an [**IQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object.</span></span> <span data-ttu-id="f310e-116">Ardından, Faturalanacak işlemleri için bir arabirim almak üzere [**faturalar**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) özelliğini kullanın ve ardından isteği göndermek ve ilk sayfayı almak Için ıquery nesnesini [**sorguya**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) veya [**queryasync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) yöntemine geçirin.</span><span class="sxs-lookup"><span data-stu-id="f310e-116">Next, use the [**Invoices**](/dotnet/api/microsoft.store.partnercenter.ipartner.invoices) property to get an interface to invoice operations, and then pass the IQuery object to the [**Query**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.invoices.iinvoicecollection.queryasync) method to send the request and get the first page.</span></span>

<span data-ttu-id="f310e-117">Daha sonra, desteklenen kaynak koleksiyonu numaralandırıcıları koleksiyonuna bir arabirim almak için [**Numaralandırıcılar**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) özelliğini kullanın ve ardından faturalar koleksiyonuna geçiş için bir Numaralandırıcı oluşturmak üzere [**faturalar. Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) öğesini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f310e-117">Next, use the [**Enumerators**](/dotnet/api/microsoft.store.partnercenter.ipartner.enumerators) property to get an interface to the collection of supported resource collection enumerators, and then call [**Invoices.Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create) to create an enumerator for traversing the collection of invoices.</span></span> <span data-ttu-id="f310e-118">Son olarak, aşağıdaki kod örneğinde gösterildiği gibi her bir fatura sayfasını almak ve bunlarla çalışmak için numaralandırıcıyı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f310e-118">Finally, use the enumerator to retrieve and work with each page of invoices as shown in the following code example.</span></span> <span data-ttu-id="f310e-119">[**Sonraki**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) yönteme yapılan her çağrı, sayfa boyutuna bağlı olarak bir sonraki fatura sayfası için bir istek gönderir.</span><span class="sxs-lookup"><span data-stu-id="f310e-119">Each call to the [**Next**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumerator-1.next) method sends a request for the next page of invoices based on the page size.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int invoicePageSize;

// Is this an unpaged or paged request?
bool isUnpaged = (this.invoicePageSize <= 0);

// If the scenario is unpaged, get all the invoices, otherwise get the first page.
var invoicesPage = (isUnpaged)
                 ? partnerOperations.Invoices.Get()
                 : partnerOperations.Invoices.Query(QueryFactory.Instance.BuildIndexedQuery(this.invoicePageSize));

// Create an invoice enumerator for traversing the invoice pages.
var invoicesEnumerator = partnerOperations.Enumerators.Invoices.Create(invoicesPage);
int lineCounter = 1;

while (invoicesEnumerator.HasValue)
{
    // Print the current invoice results page.
    var invoices = invoicesEnumerator.Current.Items;

    foreach (var i in invoices)
    {
        Console.WriteLine(String.Format("{0,3}. {1}  {2}  {3,16:C2}",
            lineCounter++,
            i.Id,
            i.InvoiceDate.ToString("yyyy&#39;-&#39;MM&#39;-&#39;dd&#39;T&#39;HH&#39;:&#39;mm&#39;:&#39;ss&#39;Z&#39;"),
            i.TotalCharges));
    }

    Console.WriteLine();
    Console.Write("Press any key to retrieve the next invoices page");
    Console.ReadKey();

    // Get the next page of invoices.
    invoicesEnumerator.Next();
}
```

<span data-ttu-id="f310e-120">Biraz farklı bir örnek için bkz. **örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f310e-120">For a slightly different example, see **Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f310e-121">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetPagedInvoices.cs</span><span class="sxs-lookup"><span data-stu-id="f310e-121">**Project**: Partner Center SDK Samples **Class**: GetPagedInvoices.cs</span></span>

> [!NOTE] 
> <span data-ttu-id="f310e-122">Aynı API, tüm modern ticari satın alımlar ve 145p ve Office lisansları için de kullanılır.</span><span class="sxs-lookup"><span data-stu-id="f310e-122">The same API is used for all modern commercial purchases as well as 145p and Office licenses.</span></span> <span data-ttu-id="f310e-123">Boyut ve konum yalnızca eski faturalar için kabul edilir.</span><span class="sxs-lookup"><span data-stu-id="f310e-123">Size and offset are only considered for legacy invoices.</span></span> <span data-ttu-id="f310e-124">Tüm modern ticari satın alımlarda, PageSize & boşluğu yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="f310e-124">For all modern commercial purchases, pagesize & offset will be ignored.</span></span>

## <a name="rest-request"></a><span data-ttu-id="f310e-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f310e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f310e-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f310e-126">Request syntax</span></span>

| <span data-ttu-id="f310e-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f310e-127">Method</span></span>  | <span data-ttu-id="f310e-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f310e-128">Request URI</span></span>                                                                                  |
|---------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f310e-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="f310e-129">**GET**</span></span> | <span data-ttu-id="f310e-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar? size = {size} &kayması = {KAYMASı} http/1.1</span><span class="sxs-lookup"><span data-stu-id="f310e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices?size={size}&offset={offset} HTTP/1.1</span></span>  |

### <a name="uri-parameters"></a><span data-ttu-id="f310e-131">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="f310e-131">URI parameters</span></span>

<span data-ttu-id="f310e-132">İsteği oluştururken aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f310e-132">Use the following query parameters when creating the request.</span></span>

| <span data-ttu-id="f310e-133">Ad</span><span class="sxs-lookup"><span data-stu-id="f310e-133">Name</span></span>   | <span data-ttu-id="f310e-134">Tür</span><span class="sxs-lookup"><span data-stu-id="f310e-134">Type</span></span> | <span data-ttu-id="f310e-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f310e-135">Required</span></span> | <span data-ttu-id="f310e-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f310e-136">Description</span></span>                                                                            |
|--------|------|----------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="f310e-137">boyut</span><span class="sxs-lookup"><span data-stu-id="f310e-137">size</span></span>   | <span data-ttu-id="f310e-138">int</span><span class="sxs-lookup"><span data-stu-id="f310e-138">int</span></span>  | <span data-ttu-id="f310e-139">No</span><span class="sxs-lookup"><span data-stu-id="f310e-139">No</span></span>       | <span data-ttu-id="f310e-140">Yanıtta döndürülecek fatura kaynağı sayısı.</span><span class="sxs-lookup"><span data-stu-id="f310e-140">The number of invoice resources to return in the response.</span></span> <span data-ttu-id="f310e-141">Bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="f310e-141">This parameter is optional.</span></span> |
| <span data-ttu-id="f310e-142">uzaklık</span><span class="sxs-lookup"><span data-stu-id="f310e-142">offset</span></span> | <span data-ttu-id="f310e-143">int</span><span class="sxs-lookup"><span data-stu-id="f310e-143">int</span></span>  | <span data-ttu-id="f310e-144">No</span><span class="sxs-lookup"><span data-stu-id="f310e-144">No</span></span>       | <span data-ttu-id="f310e-145">Döndürülecek ilk faturanın sıfır tabanlı dizini.</span><span class="sxs-lookup"><span data-stu-id="f310e-145">The zero-based index of the first invoice to return.</span></span>                                   |

### <a name="request-headers"></a><span data-ttu-id="f310e-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f310e-146">Request headers</span></span>

<span data-ttu-id="f310e-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f310e-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f310e-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f310e-148">Request body</span></span>

<span data-ttu-id="f310e-149">Yok</span><span class="sxs-lookup"><span data-stu-id="f310e-149">None</span></span>

### <a name="request-example"></a><span data-ttu-id="f310e-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f310e-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices?size=200&offset=0 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: e88d014d-ab70-41de-90a0-f7fd1797267d
MS-CorrelationId: de894e18-f027-4ac0-8b5a-34f0c222af0c
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="f310e-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f310e-151">REST response</span></span>

<span data-ttu-id="f310e-152">Başarılı olursa, yanıt gövdesi [Fatura](invoice-resources.md#invoice) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="f310e-152">If successful, the response body contains the collection of [Invoice](invoice-resources.md#invoice) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f310e-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f310e-153">Response success and error codes</span></span>

<span data-ttu-id="f310e-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="f310e-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f310e-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f310e-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f310e-156">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f310e-156">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f310e-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f310e-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT
{
    "totalCount": 2,
    "items": [
        {
            "id": "D02005YFHI",
            "invoiceDate": "2017-01-21T00:00:00Z",
            "totalCharges": 24606.35,
            "paidAmount": 1000,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "pdfDownloadLink": "/invoices/D02005YFHI/documents/statement",
            "taxReceipts": [
                {
                    "id": "123456",
                    "taxReceiptPdfDownloadLink": "/invoices/D02005YFHI/receipts/123456/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "office",
                    "links": {
                        "self": {
                            "uri": "/invoices/Recurring-D02005YFHI/lineitems/Office/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "documentType": "invoice",
            "invoiceType": "Recurring",
            "links": {
                "self": {
                    "uri": "/invoices/Recurring-D02005YFHI",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        },
        {
            "id": "G000024130",
            "invoiceDate": "2018-02-08T01:22:47.603895Z",
            "totalCharges": 586366,
            "paidAmount": 0,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "pdfDownloadLink": "/invoices/G000024130/documents/statement",
            "taxReceipts": [
                {
                    "id": "234567",
                    "taxReceiptPdfDownloadLink": "/invoices/G000024130/receipts/234567/documents/statement"
                }
            ],
            "invoiceDetails": [
                {
                    "invoiceLineItemType": "billing_line_items",
                    "billingProvider": "one_time",
                    "links": {
                        "self": {
                            "uri": "/invoices/OneTime-G000024130/lineitems/OneTime/BillingLineItems",
                            "method": "GET",
                            "headers": []
                        }
                    },
                    "attributes": {
                        "objectType": "InvoiceDetail"
                    }
                }
            ],
            "amendments": [
                {
                    "id": "G000024131",
                    "invoiceDate": "2018-02-08T18:44:37.5381456Z",
                    "totalCharges": 107661.12,
                    "paidAmount": 0,
                    "currencyCode": "CHF",
                    "currencySymbol": "CHF",
                    "invoiceDetails": [
                        {
                            "invoiceLineItemType": "billing_line_items",
                            "billingProvider": "one_time",
                            "attributes": {
                                "objectType": "InvoiceDetail"
                            }
                        }
                    ],
                    "documentType": "adjustment_note",
                    "amendsOf": "G000024130",
                    "invoiceType": "OneTime",
                    "attributes": {
                        "objectType": "Invoice"
                    }
                }
            ],
            "documentType": "void_note",
            "invoiceType": "OneTime",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024130",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Invoice"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices?size=2&offset=0",
            "method": "GET",
            "headers": []
        },
        "next": {
            "uri": "/invoices?size=2&offset=2",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
