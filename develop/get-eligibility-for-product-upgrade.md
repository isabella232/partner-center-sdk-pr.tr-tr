---
title: Müşterinin bir Azure planına yükseltmeye uygunluğunu denetleme
description: Bir müşterinin bir Microsoft Azure (MS-AZR-0145P) aboneliğinden bir Azure planına yükseltme için uygun olup olmadığını öğrenmek üzere Productyükselderequest kaynağını kullanarak bir ProductUpgradesEligibility kaynağı döndürebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: khpavan
ms.author: sakhanda
ms.openlocfilehash: 568ed3f4cff7d9cd520e608d43cb89bb78e00ccc
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768723"
---
# <a name="check-a-customers-eligibility-for-upgrading-to-an-azure-plan"></a><span data-ttu-id="d95a0-103">Müşterinin bir Azure planına yükseltmeye uygunluğunu denetleme</span><span class="sxs-lookup"><span data-stu-id="d95a0-103">Check a customer's eligibility for upgrading to an Azure plan</span></span>

<span data-ttu-id="d95a0-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="d95a0-104">**Applies to:**</span></span>

- <span data-ttu-id="d95a0-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d95a0-105">Partner Center</span></span>

<span data-ttu-id="d95a0-106">Bir müşterinin bir Microsoft Azure (MS-AZR-0145P) aboneliğinden bir Azure planına yükseltme için uygun olup olmadığını denetlemek için [**productyükseltileequest**](product-upgrade-resources.md#productupgraderequest) kaynağını kullanabilirsiniz. Bu yöntem, müşterinin ürün yükseltme uygunluğuyla bir [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="d95a0-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to check if a customer is eligible to upgrade to an Azure plan from a Microsoft Azure (MS-AZR-0145P) subscription This method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource with the customer's product upgrade eligibility.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d95a0-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d95a0-107">Prerequisites</span></span>

- <span data-ttu-id="d95a0-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d95a0-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d95a0-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d95a0-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="d95a0-110">Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="d95a0-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="d95a0-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d95a0-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d95a0-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d95a0-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d95a0-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="d95a0-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d95a0-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d95a0-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d95a0-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="d95a0-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d95a0-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="d95a0-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d95a0-117">Ürün ailesi.</span><span class="sxs-lookup"><span data-stu-id="d95a0-117">The product family.</span></span>

## <a name="c"></a><span data-ttu-id="d95a0-118">C\#</span><span class="sxs-lookup"><span data-stu-id="d95a0-118">C\#</span></span>

<span data-ttu-id="d95a0-119">Müşterinin Azure planına yükseltmeye uygun olup olmadığını denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="d95a0-119">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="d95a0-120">**Productupgradesrequest** nesnesi oluşturun ve ürün ailesi olarak müşteri tanımlayıcısını ve "Azure" i belirtin.</span><span class="sxs-lookup"><span data-stu-id="d95a0-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="d95a0-121">**Iaggregatepartner. Productyükseltmeleri** koleksiyonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="d95a0-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>
3. <span data-ttu-id="d95a0-122">**CheckEligibility** yöntemini çağırın ve bir **ProductUpgradesEligibility** nesnesi döndüren **productupgradesrequest** nesnesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="d95a0-122">Call the **CheckEligibility** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradesEligibility** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="d95a0-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d95a0-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d95a0-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d95a0-124">Request syntax</span></span>

| <span data-ttu-id="d95a0-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d95a0-125">Method</span></span>   | <span data-ttu-id="d95a0-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d95a0-126">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="d95a0-127">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="d95a0-127">**POST**</span></span> | <span data-ttu-id="d95a0-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/productupgrades/uygunluk http/1.1</span><span class="sxs-lookup"><span data-stu-id="d95a0-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/eligibility HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d95a0-129">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d95a0-129">Request headers</span></span>

<span data-ttu-id="d95a0-130">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d95a0-130">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d95a0-131">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d95a0-131">Request body</span></span>

<span data-ttu-id="d95a0-132">İstek gövdesi bir [**Productyükseltilebilir Derequest**](product-upgrade-resources.md#productupgraderequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="d95a0-132">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="d95a0-133">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d95a0-133">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="d95a0-134">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d95a0-134">REST response</span></span>

<span data-ttu-id="d95a0-135">Başarılı olursa, bu yöntem gövdede bir [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="d95a0-135">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d95a0-136">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d95a0-136">Response success and error codes</span></span>

<span data-ttu-id="d95a0-137">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="d95a0-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d95a0-138">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d95a0-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d95a0-139">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d95a0-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d95a0-140">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d95a0-140">Response example</span></span>

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
