---
title: Fatura ekstresini alma
description: Fatura KIMLIĞINI kullanarak bir fatura ekstresi alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 42e5201919eea5644da463dfe2584c8d55002083
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769016"
---
# <a name="get-invoice-statement"></a><span data-ttu-id="42b37-103">Fatura ekstresini alma</span><span class="sxs-lookup"><span data-stu-id="42b37-103">Get invoice statement</span></span>

<span data-ttu-id="42b37-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="42b37-104">**Applies To**</span></span>

- <span data-ttu-id="42b37-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="42b37-105">Partner Center</span></span>
- <span data-ttu-id="42b37-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="42b37-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="42b37-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="42b37-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="42b37-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="42b37-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="42b37-109">Fatura KIMLIĞINI kullanarak bir fatura ekstresi alır.</span><span class="sxs-lookup"><span data-stu-id="42b37-109">Retrieves an invoice statement using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="42b37-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="42b37-110">Prerequisites</span></span>

- <span data-ttu-id="42b37-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="42b37-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="42b37-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="42b37-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="42b37-113">Geçerli bir fatura KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="42b37-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="42b37-114">C\#</span><span class="sxs-lookup"><span data-stu-id="42b37-114">C\#</span></span>

<span data-ttu-id="42b37-115">Bir fatura ekstresini KIMLIĞE göre almak için, **ıpartner.** Invoice koleksiyonunuzu kullanın ve fatura kimliğini kullanarak **byıd (** ) yöntemini çağırın, sonra fatura ekstresini erişmek için **Belgeler ()** ve **Ekstre ()** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="42b37-115">To get an invoice statement by ID, use your **IPartner.Invoices** collection and call the **ById()** method using the invoice ID, then call the **Documents()** and **Statement()** methods to access the invoice statement.</span></span> <span data-ttu-id="42b37-116">Son olarak **Get ()** veya **GetAsync ()** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="42b37-116">Finally, call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoiceStatement = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Documents.Statement.Get();
```

<span data-ttu-id="42b37-117">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="42b37-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="42b37-118">**Proje**: Partnersdk. Featuresample **sınıfı**: GetInvoiceStatement.cs</span><span class="sxs-lookup"><span data-stu-id="42b37-118">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceStatement.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="42b37-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="42b37-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="42b37-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="42b37-120">Request syntax</span></span>

| <span data-ttu-id="42b37-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="42b37-121">Method</span></span>  | <span data-ttu-id="42b37-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="42b37-122">Request URI</span></span>                                                                                       |
|---------|---------------------------------------------------------------------------------------------------|
| <span data-ttu-id="42b37-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="42b37-123">**GET**</span></span> | <span data-ttu-id="42b37-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{INVOICE-ID}/Documents/deyimin http/1.1</span><span class="sxs-lookup"><span data-stu-id="42b37-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id}/documents/statement HTTP/1.1</span></span>  |

### <a name="uri-parameter"></a><span data-ttu-id="42b37-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="42b37-125">URI parameter</span></span>

<span data-ttu-id="42b37-126">Fatura ekstresini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="42b37-126">Use the following query parameter to get the invoice statement.</span></span>

| <span data-ttu-id="42b37-127">Ad</span><span class="sxs-lookup"><span data-stu-id="42b37-127">Name</span></span>       | <span data-ttu-id="42b37-128">Tür</span><span class="sxs-lookup"><span data-stu-id="42b37-128">Type</span></span>       | <span data-ttu-id="42b37-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="42b37-129">Required</span></span> | <span data-ttu-id="42b37-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="42b37-130">Description</span></span>                                                                                        |
|------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="42b37-131">Fatura kimliği</span><span class="sxs-lookup"><span data-stu-id="42b37-131">invoice-id</span></span> | <span data-ttu-id="42b37-132">string</span><span class="sxs-lookup"><span data-stu-id="42b37-132">string</span></span>     | <span data-ttu-id="42b37-133">Yes</span><span class="sxs-lookup"><span data-stu-id="42b37-133">Yes</span></span>      | <span data-ttu-id="42b37-134">Değer, satıcının belirli bir faturaya ait sonuçları filtrelemesine olanak tanıyan bir fatura kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="42b37-134">The value is an invoice-id that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="42b37-135">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="42b37-135">Request headers</span></span>

<span data-ttu-id="42b37-136">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="42b37-136">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="42b37-137">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="42b37-137">Request body</span></span>

<span data-ttu-id="42b37-138">Yok</span><span class="sxs-lookup"><span data-stu-id="42b37-138">None</span></span>

### <a name="request-example"></a><span data-ttu-id="42b37-139">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="42b37-139">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id>/documents/statement HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="42b37-140">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="42b37-140">REST response</span></span>

<span data-ttu-id="42b37-141">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Faturalarestatement](invoice-resources.md#invoicestatement) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="42b37-141">If successful, this method returns an [InvoiceStatement](invoice-resources.md#invoicestatement) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="42b37-142">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="42b37-142">Response success and error codes</span></span>

<span data-ttu-id="42b37-143">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="42b37-143">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="42b37-144">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="42b37-144">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="42b37-145">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="42b37-145">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="42b37-146">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="42b37-146">Response example</span></span>

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
