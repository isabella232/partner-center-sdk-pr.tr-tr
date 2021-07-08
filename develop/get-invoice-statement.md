---
title: Fatura ekstresini alma
description: Fatura KIMLIĞINI kullanarak bir fatura ekstresi alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: f0324916eb2efd9244530a53b1d7bb4abc0c8e6e
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549136"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="34087-103">Fatura ekstresini alma</span><span class="sxs-lookup"><span data-stu-id="34087-103">Get invoice statement</span></span>

<span data-ttu-id="34087-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="34087-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34087-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="34087-105">Prerequisites</span></span>

- <span data-ttu-id="34087-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="34087-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="34087-107">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="34087-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="34087-108">Geçerli bir fatura KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="34087-108">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="34087-109">C\#</span><span class="sxs-lookup"><span data-stu-id="34087-109">C\#</span></span>

<span data-ttu-id="34087-110">Bir fatura ekstresini KIMLIĞE göre almak için, **ıpartner.** Invoice koleksiyonunuzu kullanın ve fatura kimliğini kullanarak **byıd (** ) yöntemini çağırın, sonra fatura ekstresini erişmek için **Belgeler ()** ve **Ekstre ()** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="34087-110">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="34087-111">Son olarak **Get ()** veya **GetAsync ()** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="34087-111">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="34087-112">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="34087-112">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="34087-113">**Project**: partnersdk. featuresample **sınıfı**: getfaturalarestatement. cs</span><span class="sxs-lookup"><span data-stu-id="34087-113">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="34087-114">REST isteği</span><span class="sxs-lookup"><span data-stu-id="34087-114">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="34087-115">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="34087-115">Request syntax</span></span>

| <span data-ttu-id="34087-116">Yöntem</span><span class="sxs-lookup"><span data-stu-id="34087-116">Method</span></span>  | <span data-ttu-id="34087-117">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="34087-117">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="34087-118">**Al**</span><span class="sxs-lookup"><span data-stu-id="34087-118">**GET**</span></span> | <span data-ttu-id="34087-119">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{INVOICE-ID}/Documents/deyimin http/1.1</span><span class="sxs-lookup"><span data-stu-id="34087-119">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="34087-120">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="34087-120">URI parameter</span></span>

<span data-ttu-id="34087-121">Fatura ekstresini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="34087-121">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="34087-122">Ad</span><span class="sxs-lookup"><span data-stu-id="34087-122">Name</span></span>       | <span data-ttu-id="34087-123">Tür</span><span class="sxs-lookup"><span data-stu-id="34087-123">Type</span></span>       | <span data-ttu-id="34087-124">Gerekli</span><span class="sxs-lookup"><span data-stu-id="34087-124">Required</span></span> | <span data-ttu-id="34087-125">Açıklama</span><span class="sxs-lookup"><span data-stu-id="34087-125">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="34087-126">Fatura kimliği</span><span class="sxs-lookup"><span data-stu-id="34087-126">invoice-id</span></span> | <span data-ttu-id="34087-127">string</span><span class="sxs-lookup"><span data-stu-id="34087-127">string</span></span>     | <span data-ttu-id="34087-128">Yes</span><span class="sxs-lookup"><span data-stu-id="34087-128">Yes</span></span>      | <span data-ttu-id="34087-129">Değer, satıcının belirli bir faturaya ait sonuçları filtrelemesine olanak tanıyan bir fatura kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="34087-129">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="34087-130">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="34087-130">Request headers</span></span>

<span data-ttu-id="34087-131">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="34087-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="34087-132">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="34087-132">Request body</span></span>

<span data-ttu-id="34087-133">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="34087-133">None</span></span>

### <a name="request-example"></a><span data-ttu-id="34087-134">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="34087-134">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="34087-135">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="34087-135">REST response</span></span>

<span data-ttu-id="34087-136">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Faturalarestatement](invoice-resources.md#invoicestatement) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="34087-136">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="34087-137">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="34087-137">Response success and error codes</span></span>

<span data-ttu-id="34087-138">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="34087-138">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="34087-139">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="34087-139">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="34087-140">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="34087-140">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="34087-141">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="34087-141">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 219753
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    _content    {System.Net.Http.ByteArrayContent}    System.Net.Http.HttpContent {System.Net.Http.ByteArrayContent}
    _content    {byte[219753]}    byte[]
    _headers    {Content-Type: application/pdf Content-Disposition: attachment; filename=Invoice_G000024132.pdf}
}
```
