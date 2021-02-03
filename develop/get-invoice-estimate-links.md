---
title: Fatura tahmini bağlantılarını alma
description: Sorgu mutabakatı satır öğesi ayrıntılarına yönelik bir tahmin bağlantıları koleksiyonu edinebilirsiniz.
ms.date: 09/24/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.assetid: ''
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 10801cdb1f9d4f50a1f8fc86c2d0eaf8610ed68c
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769017"
---
# <a name="get-invoice-estimate-links"></a><span data-ttu-id="4fe4a-103">Fatura tahmini bağlantılarını alma</span><span class="sxs-lookup"><span data-stu-id="4fe4a-103">Get invoice estimate links</span></span>

<span data-ttu-id="4fe4a-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="4fe4a-104">**Applies to:**</span></span>

- <span data-ttu-id="4fe4a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4fe4a-105">Partner Center</span></span>
- <span data-ttu-id="4fe4a-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4fe4a-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4fe4a-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4fe4a-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4fe4a-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4fe4a-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4fe4a-109">Faturalandırılmamış mutabakat satır öğelerinin ayrıntılarını sorgulama hakkında yardım almak için tahmin bağlantıları sağlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-109">You can get estimate links to help query details for unbilled reconciliation line items.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4fe4a-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4fe4a-110">Prerequisites</span></span>

- <span data-ttu-id="4fe4a-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4fe4a-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4fe4a-113">Bir fatura tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-113">An invoice identifier.</span></span> <span data-ttu-id="4fe4a-114">Bu, satır öğelerinin alınacağı faturayı tanımlar.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-114">This identifies the invoice for which to retrieve the line items.</span></span>

## <a name="c"></a><span data-ttu-id="4fe4a-115">C\#</span><span class="sxs-lookup"><span data-stu-id="4fe4a-115">C\#</span></span>

<span data-ttu-id="4fe4a-116">Aşağıdaki örnek kod, belirli bir para birimi için faturalandırılmamış satır öğelerini sorgulamak için tahmin bağlantılarını nasıl kullanabileceğinizi gösterir.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-116">The following example code shows how you can get the estimate links to query unbilled line items for a given currency.</span></span> <span data-ttu-id="4fe4a-117">Yanıt, her dönemin tahmini bağlantılarını içerir (örneğin, geçerli ve önceki ay).</span><span class="sxs-lookup"><span data-stu-id="4fe4a-117">The response contains the estimate links for each period (for example, the current and previous month).</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string curencyCode;

 // all the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
 IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read estimate links for currencycode
var estimateLinks = scopedPartnerOperations.Invoices.Estimates.Links.ByCurrency(curencyCode).Get();
```

<span data-ttu-id="4fe4a-118">Benzer bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="4fe4a-118">For a similar example, see the following:</span></span>

- <span data-ttu-id="4fe4a-119">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="4fe4a-119">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="4fe4a-120">Proje: **Iş ortağı MERKEZI SDK örnekleri**</span><span class="sxs-lookup"><span data-stu-id="4fe4a-120">Project: **Partner Center SDK Samples**</span></span>
- <span data-ttu-id="4fe4a-121">Sınıf: **GetEstimatesLinks.cs**</span><span class="sxs-lookup"><span data-stu-id="4fe4a-121">Class: **GetEstimatesLinks.cs**</span></span>

## <a name="rest-request"></a><span data-ttu-id="4fe4a-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4fe4a-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4fe4a-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4fe4a-123">Request syntax</span></span>

| <span data-ttu-id="4fe4a-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4fe4a-124">Method</span></span>  | <span data-ttu-id="4fe4a-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4fe4a-125">Request URI</span></span>                                                                                                 |
|---------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4fe4a-126">**Al**</span><span class="sxs-lookup"><span data-stu-id="4fe4a-126">**GET**</span></span> | <span data-ttu-id="4fe4a-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/ınvoes/estimates/Links? CurrencyCode = {CURRENCYCODE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="4fe4a-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/invoices/estimates/links?currencycode={currencycode} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="4fe4a-128">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="4fe4a-128">URI parameters</span></span>

<span data-ttu-id="4fe4a-129">İsteği oluştururken aşağıdaki URI 'yi ve sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-129">Use the following URI and query parameter when creating the request.</span></span>

| <span data-ttu-id="4fe4a-130">Ad</span><span class="sxs-lookup"><span data-stu-id="4fe4a-130">Name</span></span>                   | <span data-ttu-id="4fe4a-131">Tür</span><span class="sxs-lookup"><span data-stu-id="4fe4a-131">Type</span></span>   | <span data-ttu-id="4fe4a-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4fe4a-132">Required</span></span> | <span data-ttu-id="4fe4a-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4fe4a-133">Description</span></span>                                                       |
|------------------------|--------|----------|-------------------------------------------------------------------|
| <span data-ttu-id="4fe4a-134">currencyCode</span><span class="sxs-lookup"><span data-stu-id="4fe4a-134">currencyCode</span></span>           | <span data-ttu-id="4fe4a-135">string</span><span class="sxs-lookup"><span data-stu-id="4fe4a-135">string</span></span> | <span data-ttu-id="4fe4a-136">Yes</span><span class="sxs-lookup"><span data-stu-id="4fe4a-136">Yes</span></span>      | <span data-ttu-id="4fe4a-137">Faturalandırılmamış satır öğelerinin para birimi kodu.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-137">The currency code for the unbilled line items.</span></span>                    |

### <a name="request-headers"></a><span data-ttu-id="4fe4a-138">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4fe4a-138">Request headers</span></span>

<span data-ttu-id="4fe4a-139">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4fe4a-139">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4fe4a-140">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4fe4a-140">Request body</span></span>

<span data-ttu-id="4fe4a-141">Yok.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-141">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4fe4a-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4fe4a-142">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/invoices/estimates/links?currencycode=usd HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 1234ecb8-37af-45f4-a1a1-358de3ca2b9e
MS-CorrelationId: 5e612512-4345-4bb0-866e-47aeda031234
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="4fe4a-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4fe4a-143">REST response</span></span>

<span data-ttu-id="4fe4a-144">Başarılı olursa, yanıt faturalandırılmamış tahminleri alma bağlantılarını içerir.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-144">If successful, the response contains the links to retrieve unbilled estimates.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4fe4a-145">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4fe4a-145">Response success and error codes</span></span>

<span data-ttu-id="4fe4a-146">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4fe4a-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4fe4a-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4fe4a-148">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4fe4a-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4fe4a-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4fe4a-149">Response example</span></span>

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
