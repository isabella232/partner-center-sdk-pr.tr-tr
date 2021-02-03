---
title: Kodu kimliğe göre al
description: Fatura KIMLIĞINI kullanarak belirli bir faturayı alır.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 17880265d06e8e5eaacc5470d83c49defd10ad51
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768717"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="b6a5e-103">Kodu kimliğe göre al</span><span class="sxs-lookup"><span data-stu-id="b6a5e-103">Get invoice by ID</span></span>

<span data-ttu-id="b6a5e-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="b6a5e-104">**Applies to:**</span></span>

- <span data-ttu-id="b6a5e-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b6a5e-105">Partner Center</span></span>
- <span data-ttu-id="b6a5e-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b6a5e-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="b6a5e-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b6a5e-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="b6a5e-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="b6a5e-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b6a5e-109">Fatura KIMLIĞINI kullanarak belirli bir faturayı alır.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-109">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b6a5e-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b6a5e-110">Prerequisites</span></span>

- <span data-ttu-id="b6a5e-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b6a5e-112">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="b6a5e-113">Geçerli bir fatura KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-113">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="b6a5e-114">C\#</span><span class="sxs-lookup"><span data-stu-id="b6a5e-114">C\#</span></span>

<span data-ttu-id="b6a5e-115">Bir faturayı KIMLIĞE göre almak için:</span><span class="sxs-lookup"><span data-stu-id="b6a5e-115">To get an invoice by ID:</span></span>

1. <span data-ttu-id="b6a5e-116">**Ipartner. Invoices** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-116">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="b6a5e-117">**Get ()** veya **GetAsync ()** yöntemlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-117">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="b6a5e-118">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="b6a5e-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="b6a5e-119">**Proje**: Partnersdk. Featuresample **sınıfı**: GetInvoice.cs</span><span class="sxs-lookup"><span data-stu-id="b6a5e-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="b6a5e-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="b6a5e-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b6a5e-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="b6a5e-121">Request syntax</span></span>

| <span data-ttu-id="b6a5e-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="b6a5e-122">Method</span></span>  | <span data-ttu-id="b6a5e-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="b6a5e-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="b6a5e-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="b6a5e-124">**GET**</span></span> | <span data-ttu-id="b6a5e-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/{INVOICE-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="b6a5e-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="b6a5e-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="b6a5e-126">URI parameter</span></span>

<span data-ttu-id="b6a5e-127">Faturayı almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-127">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="b6a5e-128">Ad</span><span class="sxs-lookup"><span data-stu-id="b6a5e-128">Name</span></span>           | <span data-ttu-id="b6a5e-129">Tür</span><span class="sxs-lookup"><span data-stu-id="b6a5e-129">Type</span></span>       | <span data-ttu-id="b6a5e-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="b6a5e-130">Required</span></span> | <span data-ttu-id="b6a5e-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="b6a5e-131">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b6a5e-132">**Fatura kimliği**</span><span class="sxs-lookup"><span data-stu-id="b6a5e-132">**invoice-id**</span></span> | <span data-ttu-id="b6a5e-133">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="b6a5e-133">**string**</span></span> | <span data-ttu-id="b6a5e-134">Yes</span><span class="sxs-lookup"><span data-stu-id="b6a5e-134">Yes</span></span>      | <span data-ttu-id="b6a5e-135">Değer, satıcının belirli bir faturaya ait sonuçları filtrelemesine olanak tanıyan bir **Fatura kimliğidir** .</span><span class="sxs-lookup"><span data-stu-id="b6a5e-135">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b6a5e-136">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="b6a5e-136">Request headers</span></span>

<span data-ttu-id="b6a5e-137">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="b6a5e-137">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b6a5e-138">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="b6a5e-138">Request body</span></span>

<span data-ttu-id="b6a5e-139">Yok</span><span class="sxs-lookup"><span data-stu-id="b6a5e-139">None</span></span>

### <a name="request-example"></a><span data-ttu-id="b6a5e-140">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="b6a5e-140">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="b6a5e-141">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="b6a5e-141">REST response</span></span>

<span data-ttu-id="b6a5e-142">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Fatura](invoice-resources.md#invoice) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-142">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b6a5e-143">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="b6a5e-143">Response success and error codes</span></span>

<span data-ttu-id="b6a5e-144">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-144">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b6a5e-145">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b6a5e-145">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b6a5e-146">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="b6a5e-146">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b6a5e-147">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="b6a5e-147">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 676
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
Date: Thu, 24 Mar 2016 05:22:14 GMT

{
    "id": "G000024135",
    "invoiceDate": "2018-02-08T22:40:37.5897767Z",
    "billingPeriodStartDate": "2018-02-01T22:40:37.5897767Z",
    "billingPeriodEndDate": "2018-02-28T22:40:37.5897767Z",
    "totalCharges": 2076.63,
    "paidAmount": 0,
    "currencyCode": "USD",
    "currencySymbol": "$",
    "pdfDownloadLink": "/invoices/G000024135/documents/statement",
    "taxReceipts": [
        {
            "id": "123456",
            "taxReceiptPdfDownloadLink": "/invoices/G000024135/receipts/123456/documents/statement"
        }
    ],
    "invoiceDetails": [
        {
            "invoiceLineItemType": "billing_line_items",
            "billingProvider": "one_time",
            "links": {
                "self": {
                    "uri": "/invoices/OneTime-G000024135/lineitems/OneTime/BillingLineItems",
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
    "invoiceType": "OneTime",
    "links": {
        "self": {
            "uri": "/invoices/OneTime-G000024135",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Invoice"
    }
}
```
