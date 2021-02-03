---
title: Ortağın geçerli hesap bakiyesini alma
description: Ortağın geçerli hesap bakiyesini alır. Hem yinelenen hem de tek seferlik ücretler için bir faturaya ait bakiye ve toplam ücretler Özeti.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 110da433faa6ff4d3d068c6d68a6f497f4a2721a
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769046"
---
# <a name="get-the-partners-current-account-balance"></a><span data-ttu-id="2f9ff-104">Ortağın geçerli hesap bakiyesini alma</span><span class="sxs-lookup"><span data-stu-id="2f9ff-104">Get the partner's current account balance</span></span>

<span data-ttu-id="2f9ff-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="2f9ff-105">**Applies To**</span></span>

- <span data-ttu-id="2f9ff-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2f9ff-106">Partner Center</span></span>
- <span data-ttu-id="2f9ff-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2f9ff-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="2f9ff-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2f9ff-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="2f9ff-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="2f9ff-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="2f9ff-110">Ortağın geçerli hesap bakiyesini alır.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-110">Retrieves the partner's current account balance.</span></span> <span data-ttu-id="2f9ff-111">Hem yinelenen hem de tek seferlik ücretler için bir faturaya ait bakiye ve toplam ücretler Özeti.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-111">A summary of the balance and total charges of an invoice for both recurring and one-time charges.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2f9ff-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="2f9ff-112">Prerequisites</span></span>

- <span data-ttu-id="2f9ff-113">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="2f9ff-114">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-114">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="2f9ff-115">C\#</span><span class="sxs-lookup"><span data-stu-id="2f9ff-115">C\#</span></span>

<span data-ttu-id="2f9ff-116">Hesap bakiyenizi almak için **ıaggregatepartner. faturalardaki** koleksiyonunuzu kullanın ve ardından **Summary** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-116">To retrieve your account balance, use your **IAggregatePartner.Invoices** collection, and then call the **Summary** property.</span></span> <span data-ttu-id="2f9ff-117">Sonra **Get** işlevini çağırın ve son olarak **BalanceAmount** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-117">Then call the **Get** function, and finally call the **BalanceAmount** property.</span></span>

``` csharp
// IAggregatePartner scopedPartnerOperations;

var invoiceSummary = scopedPartnerOperations.Invoices.Summary.Get();

Console.Out.WriteLine("Current Account Balance:  {0:C}", invoiceSummary.BalanceAmount);
```

<span data-ttu-id="2f9ff-118">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="2f9ff-118">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="2f9ff-119">**Proje**: Partnersdk. Featuresample **sınıfı**: GetInvoiceSummary.cs</span><span class="sxs-lookup"><span data-stu-id="2f9ff-119">**Project**: PartnerSDK.FeatureSample **Class**: GetInvoiceSummary.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="2f9ff-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="2f9ff-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="2f9ff-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="2f9ff-121">Request syntax</span></span>

| <span data-ttu-id="2f9ff-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="2f9ff-122">Method</span></span>  | <span data-ttu-id="2f9ff-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="2f9ff-123">Request URI</span></span>                                                              |
|---------|--------------------------------------------------------------------------|
| <span data-ttu-id="2f9ff-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="2f9ff-124">**GET**</span></span> | <span data-ttu-id="2f9ff-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/faturaes/Summary http/1.1</span><span class="sxs-lookup"><span data-stu-id="2f9ff-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/summary HTTP/1.1</span></span>  |

### <a name="request-headers"></a><span data-ttu-id="2f9ff-126">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="2f9ff-126">Request headers</span></span>

<span data-ttu-id="2f9ff-127">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="2f9ff-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="2f9ff-128">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="2f9ff-128">Request body</span></span>

<span data-ttu-id="2f9ff-129">Yok</span><span class="sxs-lookup"><span data-stu-id="2f9ff-129">None</span></span>

### <a name="request-example"></a><span data-ttu-id="2f9ff-130">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="2f9ff-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/summary HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a45e6643-1caf-4429-8f90-07c03d85bc2b
MS-CorrelationId: 57eb2ca7-755f-450f-9187-eae1e75a0114
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="2f9ff-131">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="2f9ff-131">REST response</span></span>

<span data-ttu-id="2f9ff-132">Başarılı olursa, bu yöntem yanıtta bir [Faturalaresummary](invoice-resources.md#invoicesummary) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-132">If successful, this method returns an [InvoiceSummary](invoice-resources.md#invoicesummary) resource in the response.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="2f9ff-133">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="2f9ff-133">Response success and error codes</span></span>

<span data-ttu-id="2f9ff-134">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="2f9ff-135">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="2f9ff-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="2f9ff-136">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="2f9ff-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="2f9ff-137">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="2f9ff-137">Response example</span></span>

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
