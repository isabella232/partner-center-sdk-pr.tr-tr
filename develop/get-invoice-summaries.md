---
title: Fatura özetlerini alma
description: Hem yinelenen hem de tek seferlik ücretlerin bakiyesini ve toplam ücretlerini göstermek için her bir para birimi türü için bir fatura özetleri kaynağı kullanabilirsiniz.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: fb6ff839c56c7b0b77a9904abf05d95ca0500b00
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549119"
---
# <a name="get-invoice-summaries"></a><span data-ttu-id="8c553-103">Fatura özetlerini alma</span><span class="sxs-lookup"><span data-stu-id="8c553-103">Get invoice summaries</span></span>

<span data-ttu-id="8c553-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="8c553-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="8c553-105">Yinelenen ve tek seferlik ücretlerin bakiyesini ve toplam ücretlerini gösteren bir fatura Özeti almak için **InvoiceSummaries** kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="8c553-105">You can use the **InvoiceSummaries** to retrieve an invoice summary that shows the balance and total charges of both recurring and one-time charges.</span></span> <span data-ttu-id="8c553-106">**InvoiceSummaries** kaynağı her bir para birimi türü için bir fatura özeti içerir.</span><span class="sxs-lookup"><span data-stu-id="8c553-106">The **InvoiceSummaries** resource contains an invoice summary for each currency type.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8c553-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="8c553-107">Prerequisites</span></span>

- <span data-ttu-id="8c553-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="8c553-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="8c553-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="8c553-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="8c553-110">Geçerli bir fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="8c553-110">A valid invoice identifier.</span></span>

## <a name="c"></a><span data-ttu-id="8c553-111">C\#</span><span class="sxs-lookup"><span data-stu-id="8c553-111">C\#</span></span>

<span data-ttu-id="8c553-112">Her bir para birimi türü için bir [**Faturaüt**](invoice-resources.md#invoicesummary) Içeren bir [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) koleksiyonunu almak için:</span><span class="sxs-lookup"><span data-stu-id="8c553-112">To retrieve an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) collection that contains an [**InvoiceSummary**](invoice-resources.md#invoicesummary) for each currency type:</span></span>

1. <span data-ttu-id="8c553-113">**Özet** özelliğini çağırmak Için **ıaggregatepartner. faturalardaki** koleksiyonunuzu kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c553-113">Use your **IAggregatePartner.Invoices** collection to call the **Summaries** property.</span></span>

2. <span data-ttu-id="8c553-114">**Get ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="8c553-114">Call the **Get()** method.</span></span>
3. <span data-ttu-id="8c553-115">Tek bir [**faturaya**](invoice-resources.md#invoicesummary)ait bakiyeyi almak için, koleksiyonun bu üyesi için **BalanceAmount** özelliğine erişin.</span><span class="sxs-lookup"><span data-stu-id="8c553-115">To get the balance of an individual [**InvoiceSummary**](invoice-resources.md#invoicesummary), access the **BalanceAmount** property for that member of the collection.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

// Get the invoice summaries collection.
var invoiceSummaries = scopedPartnerOperations.Invoices.Summaries.Get();

// Display the balance on the first invoice summary in the collection.
Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummaries[0].BalanceAmount);
```

<span data-ttu-id="8c553-116">Daha fazla bilgi için aşağıdaki örnek koda bakın:</span><span class="sxs-lookup"><span data-stu-id="8c553-116">For more information, see the following example code:</span></span>

- <span data-ttu-id="8c553-117">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="8c553-117">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="8c553-118">Project: **partnersdk. featuresample**</span><span class="sxs-lookup"><span data-stu-id="8c553-118">Project: **PartnerSDK.FeatureSample**</span></span>
- <span data-ttu-id="8c553-119">Sınıf: **GetInvoiceSummaries. cs**</span><span class="sxs-lookup"><span data-stu-id="8c553-119">Class: **GetInvoiceSummaries.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="8c553-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="8c553-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="8c553-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="8c553-121">Request syntax</span></span>

| <span data-ttu-id="8c553-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="8c553-122">Method</span></span>  | <span data-ttu-id="8c553-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="8c553-123">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="8c553-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="8c553-124">**GET**</span></span> | <span data-ttu-id="8c553-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturalar/özetler http/1.1</span><span class="sxs-lookup"><span data-stu-id="8c553-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summaries HTTP/1.1</span></span>     |

#### <a name="uri-parameter"></a><span data-ttu-id="8c553-126">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="8c553-126">URI parameter</span></span>

<span data-ttu-id="8c553-127">Yok.</span><span class="sxs-lookup"><span data-stu-id="8c553-127">None.</span></span>

### <a name="request-headers"></a><span data-ttu-id="8c553-128">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="8c553-128">Request headers</span></span>

<span data-ttu-id="8c553-129">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="8c553-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="8c553-130">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="8c553-130">Request body</span></span>

<span data-ttu-id="8c553-131">Yok.</span><span class="sxs-lookup"><span data-stu-id="8c553-131">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="8c553-132">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="8c553-132">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summaries HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="8c553-133">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="8c553-133">REST response</span></span>

<span data-ttu-id="8c553-134">Başarılı olursa, bu yöntem yanıt gövdesinde bir [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="8c553-134">If successful, this method returns an [**InvoiceSummaries**](invoice-resources.md#invoicesummaries) resource in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="8c553-135">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="8c553-135">Response success and error codes</span></span>

<span data-ttu-id="8c553-136">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="8c553-136">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="8c553-137">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="8c553-137">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="8c553-138">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="8c553-138">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="8c553-139">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="8c553-139">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "totalCount": 3,
    "items": [
        {
            "balanceAmount": 751094.39,
            "currencyCode": "GBP",
            "currencySymbol": "£",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
            "lastPaymentDate": "2017-01-01T12:00:00Z",
            "lastPaymentAmount": 1000,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "Recurring",
                    "summary": {
                        "balanceAmount": 202955.87,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2017-02-27T00:00:00Z",
                        "firstInvoiceCreationDate": "2017-01-21T00:00:00Z",
                        "lastPaymentDate": "2017-01-01T12:00:00Z",
                        "lastPaymentAmount": 1000,
                        "latestInvoiceDate": "0001-01-01T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                },
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 548138.52,
                        "currencyCode": "GBP",
                        "currencySymbol": "£",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1230.33,
            "currencyCode": "CHF",
            "currencySymbol": "CHF",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1230.33,
                        "currencyCode": "CHF",
                        "currencySymbol": "CHF",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        },
        {
            "balanceAmount": 1001.12,
            "currencyCode": "EUR",
            "currencySymbol": "€",
            "accountingDate": "2018-03-16T00:00:00",
            "firstInvoiceCreationDate": "2018-03-16T00:00:00",
            "lastPaymentDate": "0001-01-01T00:00:00",
            "lastPaymentAmount": 0,
            "latestInvoiceDate": "2018-03-16T00:00:00",
            "details": [
                {
                    "invoiceType": "OneTime",
                    "summary": {
                        "balanceAmount": 1001.12,
                        "currencyCode": "EUR",
                        "currencySymbol": "€",
                        "accountingDate": "2018-03-16T00:00:00",
                        "firstInvoiceCreationDate": "2018-03-16T00:00:00",
                        "lastPaymentDate": "0001-01-01T00:00:00",
                        "lastPaymentAmount": 0,
                        "latestInvoiceDate": "2018-03-16T00:00:00",
                        "attributes": {
                            "objectType": "InvoiceSummary"
                        }
                    }
                }
            ],
            "links": {
                "self": {
                    "uri": "/invoices/summary",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "InvoiceSummary"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/invoices/summaries",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
