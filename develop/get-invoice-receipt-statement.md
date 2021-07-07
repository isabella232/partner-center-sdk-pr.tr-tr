---
title: Fatura makbuz ekstresi alma
description: Fatura kimliğini ve makbuz kimliğini kullanarak bir fatura makbuzu deyimini alınır.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: dcac4c8f0b881409dcad3560eefb82d4bb5e877a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446138"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="be0f3-103">Fatura makbuz ekstresi alma</span><span class="sxs-lookup"><span data-stu-id="be0f3-103">Get invoice receipt statement</span></span>

<span data-ttu-id="be0f3-104">Fatura kimliğini ve makbuz kimliğini kullanarak bir fatura makbuzu deyimini alınır.</span><span class="sxs-lookup"><span data-stu-id="be0f3-104">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="be0f3-105">Bu özellik yalnızca Tayvan vergi makbuzları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="be0f3-105">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="be0f3-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="be0f3-106">Prerequisites</span></span>

- <span data-ttu-id="be0f3-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="be0f3-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="be0f3-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="be0f3-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="be0f3-109">Geçerli bir Fatura Kimliği ve karşılık gelen makbuz kimliği.</span><span class="sxs-lookup"><span data-stu-id="be0f3-109">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="be0f3-110">C\#</span><span class="sxs-lookup"><span data-stu-id="be0f3-110">C\#</span></span>

<span data-ttu-id="be0f3-111">İş Ortağı Merkezi SDK'sı v1.12.0 ile başlayarak, id ile bir fatura makbuzu deyimi almak için **IPartner.Invoices** koleksiyonu kullanın ve fatura kimliğini kullanarak **ById()** yöntemini arayın, ardından **Makbuzlar** koleksiyonunu çağırarak **ById()** çağrısında bulundurarak **Documents()** ve **Statement()** yöntemlerini fatura makbuzu deyimine erişin.</span><span class="sxs-lookup"><span data-stu-id="be0f3-111">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="be0f3-112">Son olarak **Get() veya** **GetAsync() yöntemlerini** arayın.</span><span class="sxs-lookup"><span data-stu-id="be0f3-112">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="be0f3-113">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="be0f3-113">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="be0f3-114">**Project:** PartnerSDK.FeatureSample **Sınıfı:** GetInvoiceReceiptStatement.cs</span><span class="sxs-lookup"><span data-stu-id="be0f3-114">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="be0f3-115">REST isteği</span><span class="sxs-lookup"><span data-stu-id="be0f3-115">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="be0f3-116">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="be0f3-116">Request syntax</span></span>

| <span data-ttu-id="be0f3-117">Yöntem</span><span class="sxs-lookup"><span data-stu-id="be0f3-117">Method</span></span>  | <span data-ttu-id="be0f3-118">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="be0f3-118">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="be0f3-119">**Al**</span><span class="sxs-lookup"><span data-stu-id="be0f3-119">**GET**</span></span> | <span data-ttu-id="be0f3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="be0f3-120">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="be0f3-121">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="be0f3-121">URI parameter</span></span>

<span data-ttu-id="be0f3-122">Fatura makbuzu deyimini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="be0f3-122">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="be0f3-123">Ad</span><span class="sxs-lookup"><span data-stu-id="be0f3-123">Name</span></span>       | <span data-ttu-id="be0f3-124">Tür</span><span class="sxs-lookup"><span data-stu-id="be0f3-124">Type</span></span>   | <span data-ttu-id="be0f3-125">Gerekli</span><span class="sxs-lookup"><span data-stu-id="be0f3-125">Required</span></span> | <span data-ttu-id="be0f3-126">Açıklama</span><span class="sxs-lookup"><span data-stu-id="be0f3-126">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="be0f3-127">invoice-id</span><span class="sxs-lookup"><span data-stu-id="be0f3-127">invoice-id</span></span> | <span data-ttu-id="be0f3-128">string</span><span class="sxs-lookup"><span data-stu-id="be0f3-128">string</span></span> | <span data-ttu-id="be0f3-129">Yes</span><span class="sxs-lookup"><span data-stu-id="be0f3-129">Yes</span></span>      | <span data-ttu-id="be0f3-130">Değer, kurumsal bayinin belirli bir faturanın sonuçlarını filtrelemesini sağlayan bir invoice-id değeridir.</span><span class="sxs-lookup"><span data-stu-id="be0f3-130">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="be0f3-131">receipt-id</span><span class="sxs-lookup"><span data-stu-id="be0f3-131">receipt-id</span></span> | <span data-ttu-id="be0f3-132">string</span><span class="sxs-lookup"><span data-stu-id="be0f3-132">string</span></span> | <span data-ttu-id="be0f3-133">Yes</span><span class="sxs-lookup"><span data-stu-id="be0f3-133">Yes</span></span>      | <span data-ttu-id="be0f3-134">Değer, kurumsal bayinin belirli bir fatura için makbuzları filtrelemesini sağlayan bir makbuz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="be0f3-134">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="be0f3-135">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="be0f3-135">Request headers</span></span>

<span data-ttu-id="be0f3-136">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="be0f3-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="be0f3-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="be0f3-137">Request body</span></span>

<span data-ttu-id="be0f3-138">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="be0f3-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="be0f3-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="be0f3-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="be0f3-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="be0f3-140">REST response</span></span>

<span data-ttu-id="be0f3-141">Başarılı olursa, bu yöntem yanıt gövdesinde bir pdf akışı döndürür.</span><span class="sxs-lookup"><span data-stu-id="be0f3-141">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="be0f3-142">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="be0f3-142">Response success and error codes</span></span>

<span data-ttu-id="be0f3-143">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="be0f3-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="be0f3-144">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="be0f3-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="be0f3-145">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="be0f3-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="be0f3-146">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="be0f3-146">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 195556
Content-Type: application/pdf
MS-CorrelationId: a1d6ab41-5a30-4643-898b-b30d65d3a0a1
MS-RequestId: cc1ba6db-ab26-404a-9196-712b6395f518
Date: Tue, 05 Feb 2019 04:08:23 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[195556]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=E-Tax-8602768.pdf}
}
```
