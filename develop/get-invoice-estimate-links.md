---
title: Fatura tahmini bağlantılarını alma
description: Sorgu mutabakatı satır öğesi ayrıntılarına yönelik bir tahmin bağlantıları koleksiyonu edinebilirsiniz.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 719becd3fac5605c4ad48ab86d483ba7903d65d8
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111549153"
---
# <a name="get-invoice-estimate-links"></a><span data-ttu-id="7457c-103">Fatura tahmini bağlantılarını alma</span><span class="sxs-lookup"><span data-stu-id="7457c-103">Get invoice estimate links</span></span>

<span data-ttu-id="7457c-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="7457c-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="7457c-105">Faturalandırılmamış mutabakat satır öğelerinin ayrıntılarını sorgulama hakkında yardım almak için tahmin bağlantıları sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="7457c-105">You can get estimate links to help query details for unbilled reconciliation line items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7457c-106">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7457c-106">Prerequisites</span></span>

- <span data-ttu-id="7457c-107">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7457c-107">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7457c-108">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7457c-108">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="7457c-109">Bir fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7457c-109">An invoice identifier.</span></span> <span data-ttu-id="7457c-110">Bu, satır öğelerinin alınacağı faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="7457c-110">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="7457c-111">C\#</span><span class="sxs-lookup"><span data-stu-id="7457c-111">C\#</span></span>

<span data-ttu-id="7457c-112">Aşağıdaki örnek kod, belirli bir para birimi için faturalandırılmamış satır öğelerini sorgulamak için tahmin bağlantılarını nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="7457c-112">The following example code shows how you can get the estimate links to query unbilled line items for a given currency.</span></span> <span data-ttu-id="7457c-113">Yanıt, her dönemin tahmini bağlantılarını içerir (örneğin, geçerli ve önceki ay).</span><span class="sxs-lookup"><span data-stu-id="7457c-113">The response contains the estimate links for each period (for example, the current and previous month).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

<span data-ttu-id="7457c-114">Benzer bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="7457c-114">For a similar example, see the following:</span></span>

- <span data-ttu-id="7457c-115">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="7457c-115">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="7457c-116">Project: **iş ortağı merkezi SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="7457c-116">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="7457c-117">Sınıf: **Getestimateslinks. cs**</span><span class="sxs-lookup"><span data-stu-id="7457c-117">Class: **GetEstimatesLinks.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="7457c-118">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7457c-118">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7457c-119">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7457c-119">Request syntax</span></span>

| <span data-ttu-id="7457c-120">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7457c-120">Method</span></span>  | <span data-ttu-id="7457c-121">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7457c-121">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7457c-122">**Al**</span><span class="sxs-lookup"><span data-stu-id="7457c-122">**GET**</span></span> | <span data-ttu-id="7457c-123">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/ınvoes/estimates/Links? CurrencyCode = {CURRENCYCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7457c-123">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="7457c-124">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="7457c-124">URI parameters</span></span>

<span data-ttu-id="7457c-125">İsteği oluştururken aşağıdaki URI 'yi ve sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7457c-125">Use the following URI and query parameter when creating the request.</span></span>

| <span data-ttu-id="7457c-126">Ad</span><span class="sxs-lookup"><span data-stu-id="7457c-126">Name</span></span>                   | <span data-ttu-id="7457c-127">Tür</span><span class="sxs-lookup"><span data-stu-id="7457c-127">Type</span></span>   | <span data-ttu-id="7457c-128">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7457c-128">Required</span></span> | <span data-ttu-id="7457c-129">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7457c-129">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="7457c-130">currencyCode</span><span class="sxs-lookup"><span data-stu-id="7457c-130">currencyCode</span></span>           | <span data-ttu-id="7457c-131">string</span><span class="sxs-lookup"><span data-stu-id="7457c-131">string</span></span> | <span data-ttu-id="7457c-132">Yes</span><span class="sxs-lookup"><span data-stu-id="7457c-132">Yes</span></span>      | <span data-ttu-id="7457c-133">Faturalandırılmamış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="7457c-133">The currency code for the unbilled line items.</span></span>                    |

### <a name="request-headers"></a><span data-ttu-id="7457c-134">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7457c-134">Request headers</span></span>

<span data-ttu-id="7457c-135">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7457c-135">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7457c-136">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7457c-136">Request body</span></span>

<span data-ttu-id="7457c-137">Yok.</span><span class="sxs-lookup"><span data-stu-id="7457c-137">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="7457c-138">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="7457c-138">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7457c-139">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7457c-139">REST response</span></span>

<span data-ttu-id="7457c-140">Başarılı olursa, yanıt faturalandırılmamış tahminleri alma bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="7457c-140">If successful, the response contains the links to retrieve unbilled estimates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7457c-141">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7457c-141">Response success and error codes</span></span>

<span data-ttu-id="7457c-142">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7457c-142">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7457c-143">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7457c-143">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7457c-144">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7457c-144">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7457c-145">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7457c-145">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Type: application/json; charset=utf-8
Server: Microsoft-IIS/10.0
MS-CorrelationId: 80EAA055-B5D3-4D88-BFE8-924A3F706462
MS-RequestId: 1b18689e-3fe3-4fdb-d09e-39d13941390b
X-Locale: en-US
X-SourceFiles: =?UTF-8?B?RDpcU291cmNlc1xSUEUuUGFydG5lci5TZXJ2aWNlLkJpbGxpbmdTZXJ2aWNlXHYxLjFcV2ViQXBpc1xCaWxsaW5nU2VydmljZS5WMi5XZWJcdjFcaW52b2ljZXNcZXN0aW1hdGVzXGxpbmtz?=
X-Powered-By: ASP.NET
Date: Thu, 14 Mar 2019 18:15:06 GMT
Content-Length: 1857

{
  "totalCount": 4,
  "items": [
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "daily_rated_usage",
      "title": "Daily rated usage unbilled",
      "description": "This invoice line items includes unbilled consumption based data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=Marketplace&invoicelineitemtype=UsageLineItems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Current",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=current&size=2000",
        "method": "GET",
        "headers": []
      }
    },
    {
      "type": "non_consumption",
      "title": "Unbilled reconciliation line items",
      "description": "This includes reconciliation line items for unbilled data only.",
      "period": "Previous",
      "link": {
        "uri": "/invoices/unbilled/lineitems?provider=all&invoicelineitemtype=billinglineitems&currencycode=USD&period=previous&size=2000",
        "method": "GET",
        "headers": []
      }
    }
  ],
  "attributes": {
    "objectType": "Collection"
 }
}
```
