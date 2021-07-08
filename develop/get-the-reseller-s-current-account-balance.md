---
title: Ortağın geçerli hesap bakiyesini alma
description: Ortağın geçerli hesap bakiyesini alır. Hem yinelenen hem de tek seferlik ücretler için bir faturaya ait bakiye ve toplam ücretler Özeti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a04ab63482ec9d06e2fe47d2b6ce1bc6a5fd5f27
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548507"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="347ed-104">Ortağın geçerli hesap bakiyesini alma</span><span class="sxs-lookup"><span data-stu-id="347ed-104">Get the partner's current account balance</span></span>

<span data-ttu-id="347ed-105">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="347ed-105">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="347ed-106">Ortağın geçerli hesap bakiyesini alır.</span><span class="sxs-lookup"><span data-stu-id="347ed-106">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="347ed-107">Hem yinelenen hem de tek seferlik ücretler için bir faturaya ait bakiye ve toplam ücretler Özeti.</span><span class="sxs-lookup"><span data-stu-id="347ed-107">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="347ed-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="347ed-108">Prerequisites</span></span>

- <span data-ttu-id="347ed-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="347ed-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="347ed-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="347ed-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="347ed-111">C\#</span><span class="sxs-lookup"><span data-stu-id="347ed-111">C\#</span></span>

<span data-ttu-id="347ed-112">Hesap bakiyenizi almak için **ıaggregatepartner. faturalardaki** koleksiyonunuzu kullanın ve ardından **Summary** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="347ed-112">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="347ed-113">Sonra **Get** işlevini çağırın ve son olarak **BalanceAmount** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="347ed-113">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="347ed-114">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="347ed-114">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="347ed-115">**Project**: partnersdk. featuresample **sınıfı**: getınvomisi esummary. cs</span><span class="sxs-lookup"><span data-stu-id="347ed-115">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="347ed-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="347ed-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="347ed-117">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="347ed-117">Request syntax</span></span>

| <span data-ttu-id="347ed-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="347ed-118">Method</span></span>  | <span data-ttu-id="347ed-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="347ed-119">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="347ed-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="347ed-120">**GET**</span></span> | <span data-ttu-id="347ed-121">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturaes/Summary http/1.1</span><span class="sxs-lookup"><span data-stu-id="347ed-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="347ed-122">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="347ed-122">Request headers</span></span>

<span data-ttu-id="347ed-123">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="347ed-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="347ed-124">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="347ed-124">Request body</span></span>

<span data-ttu-id="347ed-125">Hiçbiri</span><span class="sxs-lookup"><span data-stu-id="347ed-125">None</span></span>

### <a name="request-example"></a><span data-ttu-id="347ed-126">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="347ed-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="347ed-127">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="347ed-127">REST response</span></span>

<span data-ttu-id="347ed-128">Başarılı olursa, bu yöntem yanıtta bir [Faturalaresummary](invoice-resources.md#invoicesummary) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="347ed-128">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="347ed-129">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="347ed-129">Response success and error codes</span></span>

<span data-ttu-id="347ed-130">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="347ed-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="347ed-131">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="347ed-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="347ed-132">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="347ed-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="347ed-133">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="347ed-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 256
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
Date: Thu, 24 Mar 2016 05:21:01 GMT

{
    "balanceAmount": 751094.39,
    "currencyCode": "USD",
    "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
                "currencyCode": "USD",
                "currencySymbol": "$",
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
```
