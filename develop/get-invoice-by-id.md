---
title: Kimliğine göre fatura al
description: Fatura kimliğini kullanarak verilen bir faturayı alan.
ms.date: 06/10/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: c888786a6b6ca941629bb7aac95227021c37a7fc
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549170"
---
# <a name="get-invoice-by-id"></a><span data-ttu-id="25388-103">Kimliğine göre fatura al</span><span class="sxs-lookup"><span data-stu-id="25388-103">Get invoice by ID</span></span>

<span data-ttu-id="25388-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="25388-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="25388-105">Fatura kimliğini kullanarak verilen bir faturayı alan.</span><span class="sxs-lookup"><span data-stu-id="25388-105">Retrieves a given invoice using the invoice ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="25388-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="25388-106">Prerequisites</span></span>

- <span data-ttu-id="25388-107">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="25388-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="25388-108">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="25388-108">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="25388-109">Geçerli bir Fatura Kimliği.</span><span class="sxs-lookup"><span data-stu-id="25388-109">A valid Invoice ID.</span></span>

## <a name="c"></a><span data-ttu-id="25388-110">C\#</span><span class="sxs-lookup"><span data-stu-id="25388-110">C\#</span></span>

<span data-ttu-id="25388-111">Kimliğine göre fatura almak için:</span><span class="sxs-lookup"><span data-stu-id="25388-111">To get an invoice by ID:</span></span>

1. <span data-ttu-id="25388-112">**IPartner.Invoices koleksiyonu kullanın** ve **ById() yöntemini** çağırın.</span><span class="sxs-lookup"><span data-stu-id="25388-112">Use your **IPartner.Invoices** collection and call the **ById()** method.</span></span>

2. <span data-ttu-id="25388-113">**Get() veya** **GetAsync() yöntemlerini** çağırma.</span><span class="sxs-lookup"><span data-stu-id="25388-113">Call the **Get()** or **GetAsync()** methods.</span></span>

``` csharp
// IPartner scopedPartnerOperations;
// string selectedInvoiceId;

var invoice = scopedPartnerOperations.Invoices.ById(selectedInvoiceId).Get();
```

<span data-ttu-id="25388-114">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="25388-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="25388-115">**Project:** PartnerSDK.FeatureSample **Sınıfı**: GetInvoice.cs</span><span class="sxs-lookup"><span data-stu-id="25388-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoice.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="25388-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="25388-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="25388-117">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="25388-117">Request syntax</span></span>

| <span data-ttu-id="25388-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="25388-118">Method</span></span>  | <span data-ttu-id="25388-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="25388-119">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="25388-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="25388-120">**GET**</span></span> | <span data-ttu-id="25388-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="25388-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/{invoice-id} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="25388-122">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="25388-122">URI parameter</span></span>

<span data-ttu-id="25388-123">Faturayı almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="25388-123">Use the following query parameter to get the invoice.</span></span>

| <span data-ttu-id="25388-124">Ad</span><span class="sxs-lookup"><span data-stu-id="25388-124">Name</span></span>           | <span data-ttu-id="25388-125">Tür</span><span class="sxs-lookup"><span data-stu-id="25388-125">Type</span></span>       | <span data-ttu-id="25388-126">Gerekli</span><span class="sxs-lookup"><span data-stu-id="25388-126">Required</span></span> | <span data-ttu-id="25388-127">Açıklama</span><span class="sxs-lookup"><span data-stu-id="25388-127">Description</span></span>                                                                                        |
|----------------|------------|----------|----------------------------------------------------------------------------------------------------|
| <span data-ttu-id="25388-128">**invoice-id**</span><span class="sxs-lookup"><span data-stu-id="25388-128">**invoice-id**</span></span> | <span data-ttu-id="25388-129">**string**</span><span class="sxs-lookup"><span data-stu-id="25388-129">**string**</span></span> | <span data-ttu-id="25388-130">Yes</span><span class="sxs-lookup"><span data-stu-id="25388-130">Yes</span></span>      | <span data-ttu-id="25388-131">Değer, kurumsal bayinin belirli bir faturanın sonuçlarını filtrelemesini sağlayan bir **invoice-id** değeridir.</span><span class="sxs-lookup"><span data-stu-id="25388-131">The value is an **invoice-id** that allows the reseller to filter the results for a given invoice.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="25388-132">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="25388-132">Request headers</span></span>

<span data-ttu-id="25388-133">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="25388-133">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="25388-134">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="25388-134">Request body</span></span>

<span data-ttu-id="25388-135">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="25388-135">None</span></span>

### <a name="request-example"></a><span data-ttu-id="25388-136">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="25388-136">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/<invoice-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 8ac25aa5-9537-4b6d-b782-aa0c8e979e99
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
```

## <a name="rest-response"></a><span data-ttu-id="25388-137">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="25388-137">REST response</span></span>

<span data-ttu-id="25388-138">Başarılı olursa, bu yöntem yanıt [gövdesinde](invoice-resources.md#invoice) bir Fatura kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="25388-138">If successful, this method returns an [Invoice](invoice-resources.md#invoice) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="25388-139">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="25388-139">Response success and error codes</span></span>

<span data-ttu-id="25388-140">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="25388-140">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="25388-141">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="25388-141">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="25388-142">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="25388-142">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="25388-143">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="25388-143">Response example</span></span>

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
