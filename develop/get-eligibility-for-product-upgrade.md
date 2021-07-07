---
title: Müşterinin bir Azure planına yükseltmeye uygunluğunu denetleme
description: bir müşterinin bir Microsoft Azure (MS-azr-0145p) aboneliğinden bir Azure planına yükseltme için uygun olup olmadığını öğrenmek üzere productyükselderequest kaynağını kullanarak bir ProductUpgradesEligibility kaynağı döndürebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 34a20611c7d92042b5432c5ffb3ba4702d77e0c2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446267"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="34a75-103">Müşterinin bir Azure planına yükseltmeye uygunluğunu denetleme</span><span class="sxs-lookup"><span data-stu-id="34a75-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="34a75-104">bir müşterinin bir Microsoft Azure (MS-azr-0145p) aboneliğinden bir Azure planına yükseltme için uygun olup olmadığını denetlemek için [**productyükseltileequest**](product-upgrade-resources.md#productupgraderequest) kaynağını kullanabilirsiniz. bu yöntem, müşterinin ürün yükseltme uygunluğuyla bir [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="34a75-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="34a75-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="34a75-105">Prerequisites</span></span>

- <span data-ttu-id="34a75-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="34a75-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="34a75-107">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="34a75-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="34a75-108">Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="34a75-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="34a75-109">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="34a75-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="34a75-110">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="34a75-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="34a75-111">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="34a75-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="34a75-112">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="34a75-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="34a75-113">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="34a75-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="34a75-114">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="34a75-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="34a75-115">Ürün ailesi.</span><span class="sxs-lookup"><span data-stu-id="34a75-115">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="34a75-116">C\#</span><span class="sxs-lookup"><span data-stu-id="34a75-116">C\#</span></span>

<span data-ttu-id="34a75-117">Müşterinin Azure planına yükseltmeye uygun olup olmadığını denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="34a75-117">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="34a75-118">**Productupgradesrequest** nesnesi oluşturun ve ürün ailesi olarak müşteri tanımlayıcısını ve "Azure" i belirtin.</span><span class="sxs-lookup"><span data-stu-id="34a75-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="34a75-119">**Iaggregatepartner. Productyükseltmeleri** koleksiyonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="34a75-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="34a75-120">**CheckEligibility** yöntemini çağırın ve bir **ProductUpgradesEligibility** nesnesi döndüren **productupgradesrequest** nesnesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="34a75-120">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesEligibility productUpgradeEligibility = partnerOperations.ProductUpgrades.CheckEligibility(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="34a75-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="34a75-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="34a75-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="34a75-122">Request syntax</span></span>

| <span data-ttu-id="34a75-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="34a75-123">Method</span></span>   | <span data-ttu-id="34a75-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="34a75-124">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="34a75-125">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="34a75-125">**POST**</span></span> | <span data-ttu-id="34a75-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/productupgrades/uygunluk http/1.1</span><span class="sxs-lookup"><span data-stu-id="34a75-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="34a75-127">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="34a75-127">Request headers</span></span>

<span data-ttu-id="34a75-128">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="34a75-128">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="34a75-129">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="34a75-129">Request body</span></span>

<span data-ttu-id="34a75-130">İstek gövdesi bir [**Productyükseltilebilir Derequest**](product-upgrade-resources.md#productupgraderequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="34a75-130">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="34a75-131">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="34a75-131">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/eligibility HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c245d5f2-1de3-4ae0-9e42-95e38e3cb8ff
MS-CorrelationId: e3f26e6a-044f-4371-ad52-0d91ce4200be
X-Locale: en-US
MS-PartnerCenter-Application: Partner Center .NET SDK Samples
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 340
Expect: 100-continue
Connection: Keep-Alive
{
        "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
        "productFamily": "azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="34a75-132">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="34a75-132">REST response</span></span>

<span data-ttu-id="34a75-133">Başarılı olursa, bu yöntem gövdede bir [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="34a75-133">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="34a75-134">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="34a75-134">Response success and error codes</span></span>

<span data-ttu-id="34a75-135">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="34a75-135">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="34a75-136">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="34a75-136">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="34a75-137">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="34a75-137">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="34a75-138">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="34a75-138">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "customerId": "c1958bc7-3284-4952-a257-de594ee64743",
    "isEligible": true,
    "productFamily": "azure"
}
```
