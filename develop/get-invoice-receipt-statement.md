---
title: Fatura makbuz ekstresi alma
description: Fatura KIMLIĞI ve giriş KIMLIĞI ' ni kullanarak bir fatura alındısı ekstresi alır.
ms.date: 02/11/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 96cef11d6778de2d9bf28e466d88a39f9415727d
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768711"
---
# <a name="get-invoice-receipt-statement"></a><span data-ttu-id="1a23a-103">Fatura makbuz ekstresi alma</span><span class="sxs-lookup"><span data-stu-id="1a23a-103">Get invoice receipt statement</span></span>

<span data-ttu-id="1a23a-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="1a23a-104">**Applies To**</span></span>

- <span data-ttu-id="1a23a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1a23a-105">Partner Center</span></span>

<span data-ttu-id="1a23a-106">Fatura KIMLIĞI ve giriş KIMLIĞI ' ni kullanarak bir fatura alındısı ekstresi alır.</span><span class="sxs-lookup"><span data-stu-id="1a23a-106">Retrieves an invoice receipt statement using invoice ID and the receipt ID.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1a23a-107">Bu özellik yalnızca Tayvan vergi alındıları için geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="1a23a-107">This feature is only applicable to Taiwan tax receipts.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1a23a-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1a23a-108">Prerequisites</span></span>

- <span data-ttu-id="1a23a-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1a23a-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1a23a-110">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="1a23a-110">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1a23a-111">Geçerli bir fatura KIMLIĞI ve buna karşılık gelen bir giriş KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="1a23a-111">A valid Invoice ID and a corresponding receipt ID.</span></span>

## <a name="c"></a><span data-ttu-id="1a23a-112">C\#</span><span class="sxs-lookup"><span data-stu-id="1a23a-112">C\#</span></span>

<span data-ttu-id="1a23a-113">Iş Ortağı Merkezi SDK v 1.12.0 'den başlayarak, KIMLIĞE göre fatura alındı bilgisi almak için, **ıpartner.** Invoice koleksiyonunuzu kullanın ve fatura kimliğini kullanarak **byıd ()** yöntemini çağırın, ardından **alındılar** koleksiyonunu çağırın ve **Byıd (** ) çağrısı yapın ve ardından **Belgeler ()** ve **Ekstre ()** yöntemlerini çağırarak fatura alındısı bildirimine erişin.</span><span class="sxs-lookup"><span data-stu-id="1a23a-113">To get an invoice receipt statement by ID, starting with Partner Center SDK v1.12.0, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Receipts** collection and call **ById()** then call the **Documents()** and **Statement()** methods to access the invoice receipt statement.</span></span> <span data-ttu-id="1a23a-114">Son olarak **Get ()** veya **GetAsync ()** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1a23a-114">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Receipts.ById(selectedReceipt).Documents.Statement.Get();
```

<span data-ttu-id="1a23a-115">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1a23a-115">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1a23a-116">**Proje**: Partnersdk. Featuresample **sınıfı**: GetInvoiceReceiptStatement.cs</span><span class="sxs-lookup"><span data-stu-id="1a23a-116">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceReceiptStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1a23a-117">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1a23a-117">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1a23a-118">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1a23a-118">Request syntax</span></span>

| <span data-ttu-id="1a23a-119">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1a23a-119">Method</span></span>  | <span data-ttu-id="1a23a-120">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1a23a-120">Request URI</span></span>                                                                                                            |
|---------|------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1a23a-121">**Al**</span><span class="sxs-lookup"><span data-stu-id="1a23a-121">**GET**</span></span> | <span data-ttu-id="1a23a-122">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{INVOICE-ID}/POTS/{pot-id}/Documents/deyimin http/1.1</span><span class="sxs-lookup"><span data-stu-id="1a23a-122">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/receipts/{receipt-id}/documents/statement HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1a23a-123">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1a23a-123">URI parameter</span></span>

<span data-ttu-id="1a23a-124">Fatura alındısı ekstresini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1a23a-124">Use the following query parameter to get the invoice receipt statement.</span></span>

| <span data-ttu-id="1a23a-125">Ad</span><span class="sxs-lookup"><span data-stu-id="1a23a-125">Name</span></span>       | <span data-ttu-id="1a23a-126">Tür</span><span class="sxs-lookup"><span data-stu-id="1a23a-126">Type</span></span>   | <span data-ttu-id="1a23a-127">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1a23a-127">Required</span></span> | <span data-ttu-id="1a23a-128">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1a23a-128">Description</span></span>                                                                                    |
|------------|--------|-----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1a23a-129">Fatura kimliği</span><span class="sxs-lookup"><span data-stu-id="1a23a-129">invoice-id</span></span> | <span data-ttu-id="1a23a-130">string</span><span class="sxs-lookup"><span data-stu-id="1a23a-130">string</span></span> | <span data-ttu-id="1a23a-131">Yes</span><span class="sxs-lookup"><span data-stu-id="1a23a-131">Yes</span></span>      | <span data-ttu-id="1a23a-132">Değer, satıcının belirli bir faturaya ait sonuçları filtrelemesine olanak tanıyan bir fatura kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="1a23a-132">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |
| <span data-ttu-id="1a23a-133">makbuz kimliği</span><span class="sxs-lookup"><span data-stu-id="1a23a-133">receipt-id</span></span> | <span data-ttu-id="1a23a-134">string</span><span class="sxs-lookup"><span data-stu-id="1a23a-134">string</span></span> | <span data-ttu-id="1a23a-135">Yes</span><span class="sxs-lookup"><span data-stu-id="1a23a-135">Yes</span></span>      | <span data-ttu-id="1a23a-136">Değer, satıcının belirli bir faturaya ait alındıları filtrelemesine olanak tanıyan bir makbuz kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="1a23a-136">The value is a receipt-id that allows the reseller to filter the receipts for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1a23a-137">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1a23a-137">Request headers</span></span>

<span data-ttu-id="1a23a-138">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1a23a-138">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1a23a-139">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1a23a-139">Request body</span></span>

<span data-ttu-id="1a23a-140">Yok</span><span class="sxs-lookup"><span data-stu-id="1a23a-140">None</span></span>

### <a name="request-example"></a><span data-ttu-id="1a23a-141">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1a23a-141">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/receipts/<receipt-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="1a23a-142">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1a23a-142">REST response</span></span>

<span data-ttu-id="1a23a-143">Başarılı olursa, bu yöntem yanıt gövdesinde bir PDF akışı döndürür.</span><span class="sxs-lookup"><span data-stu-id="1a23a-143">If successful, this method returns a pdf stream in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1a23a-144">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1a23a-144">Response success and error codes</span></span>

<span data-ttu-id="1a23a-145">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1a23a-145">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1a23a-146">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1a23a-146">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1a23a-147">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1a23a-147">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1a23a-148">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1a23a-148">Response example</span></span>

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
