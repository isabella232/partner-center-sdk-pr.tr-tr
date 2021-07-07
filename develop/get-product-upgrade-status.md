---
title: Müşterinin ürün yükseltme durumunu al
description: ProductUpgradeRequest kaynağını kullanarak müşterinin yeni bir ürün ailesine (örneğin, bir Microsoft Azure (MS-AZR-0145P) aboneliğinden Azure planına ürün yükseltme durumunu tespit edebilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 03d925dd0fae987226ad1f8e71fad380ba144b83
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445571"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="38e4e-103">Müşterinin ürün yükseltme durumunu al</span><span class="sxs-lookup"><span data-stu-id="38e4e-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="38e4e-104">Yeni bir ürün ailesine yükseltme durumunu almak için [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) kaynağını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38e4e-104">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="38e4e-105">Bu kaynak, bir müşteriyi Microsoft Azure (MS-AZR-0145P) aboneliğinden Azure planına yükseltirken geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="38e4e-105">This resource applies when you're upgrading a customer from a Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="38e4e-106">Başarılı bir istek [**ProductUpgradesEligibility kaynağını**](product-upgrade-resources.md#productupgradeseligibility) döndürür.</span><span class="sxs-lookup"><span data-stu-id="38e4e-106">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="38e4e-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="38e4e-107">Prerequisites</span></span>

- <span data-ttu-id="38e4e-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="38e4e-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="38e4e-109">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="38e4e-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="38e4e-110">[Uygulama+Kullanıcı kimlik doğrulamasını](enable-secure-app-model.md) farklı API'lerle kullanırken güvenli İş Ortağı Merkezi izleyin.</span><span class="sxs-lookup"><span data-stu-id="38e4e-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="38e4e-111">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="38e4e-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="38e4e-112">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="38e4e-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="38e4e-113">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="38e4e-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="38e4e-114">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="38e4e-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="38e4e-115">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="38e4e-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="38e4e-116">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="38e4e-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="38e4e-117">Ürün ailesi.</span><span class="sxs-lookup"><span data-stu-id="38e4e-117">The product family.</span></span>

- <span data-ttu-id="38e4e-118">Yükseltme isteğinin upgrade-id.</span><span class="sxs-lookup"><span data-stu-id="38e4e-118">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="38e4e-119">C\#</span><span class="sxs-lookup"><span data-stu-id="38e4e-119">C\#</span></span>

<span data-ttu-id="38e4e-120">Bir müşterinin Azure planına yükseltmeye uygun olup olduğunu kontrol etmek için:</span><span class="sxs-lookup"><span data-stu-id="38e4e-120">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="38e4e-121">Bir **ProductUpgradesRequest nesnesi** oluşturun ve müşteri tanımlayıcısını ve ürün ailesi olarak "Azure" belirtin.</span><span class="sxs-lookup"><span data-stu-id="38e4e-121">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="38e4e-122">**IAggregatePartner.ProductUpgrades koleksiyonunu** kullanın.</span><span class="sxs-lookup"><span data-stu-id="38e4e-122">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="38e4e-123">**ById yöntemini** çağırın ve **upgrade-id girin.**</span><span class="sxs-lookup"><span data-stu-id="38e4e-123">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="38e4e-124">**CheckStatus** yöntemini çağırarak **ProductUpgradesRequest** nesnesini **(productUpgradeStatus** nesnesi) iade eder.</span><span class="sxs-lookup"><span data-stu-id="38e4e-124">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

ProductUpgradesStatus productUpgradeStatus = partnerOperations.ProductUpgrades.ById(selectedUpgradeId).CheckStatus(productUpgradeRequest);

if (productUpgradeEligibility.IsEligibile)
{
    ....
}

```

## <a name="rest-request"></a><span data-ttu-id="38e4e-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="38e4e-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="38e4e-126">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="38e4e-126">Request syntax</span></span>

| <span data-ttu-id="38e4e-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="38e4e-127">Method</span></span>   | <span data-ttu-id="38e4e-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="38e4e-128">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="38e4e-129">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="38e4e-129">**POST**</span></span> | <span data-ttu-id="38e4e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="38e4e-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="38e4e-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="38e4e-131">URI parameter</span></span>

<span data-ttu-id="38e4e-132">Ürün yükseltme durumunu almak istediğiniz müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="38e4e-132">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="38e4e-133">Ad</span><span class="sxs-lookup"><span data-stu-id="38e4e-133">Name</span></span>               | <span data-ttu-id="38e4e-134">Tür</span><span class="sxs-lookup"><span data-stu-id="38e4e-134">Type</span></span> | <span data-ttu-id="38e4e-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="38e4e-135">Required</span></span> | <span data-ttu-id="38e4e-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="38e4e-136">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="38e4e-137">**upgrade-id**</span><span class="sxs-lookup"><span data-stu-id="38e4e-137">**upgrade-id**</span></span> | <span data-ttu-id="38e4e-138">GUID</span><span class="sxs-lookup"><span data-stu-id="38e4e-138">GUID</span></span> | <span data-ttu-id="38e4e-139">Yes</span><span class="sxs-lookup"><span data-stu-id="38e4e-139">Yes</span></span> | <span data-ttu-id="38e4e-140">Değer, GUID biçimli bir yükseltme tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="38e4e-140">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="38e4e-141">bu tanımlayıcıyı, izılacak bir yükseltme belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="38e4e-141">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="38e4e-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="38e4e-142">Request headers</span></span>

<span data-ttu-id="38e4e-143">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="38e4e-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="38e4e-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="38e4e-144">Request body</span></span>

<span data-ttu-id="38e4e-145">İstek gövdesi bir [**ProductUpgradeRequest kaynağı içermeli.**](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="38e4e-145">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="38e4e-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="38e4e-146">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4/status  HTTP/1.1
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
 {
    "customerId": "4c721420-72ad-4708-a0a7-371a2f7b0969",
    "productFamily": "azure"
  }
  "Attributes": {
  "ObjectType": "ProductUpgradeRequest"
  }
}
```

## <a name="rest-response"></a><span data-ttu-id="38e4e-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="38e4e-147">REST response</span></span>

<span data-ttu-id="38e4e-148">Başarılı olursa, bu yöntem gövdede [**bir ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="38e4e-148">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="38e4e-149">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="38e4e-149">Response success and error codes</span></span>

<span data-ttu-id="38e4e-150">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="38e4e-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="38e4e-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="38e4e-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="38e4e-152">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="38e4e-152">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="38e4e-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="38e4e-153">Response example</span></span>

```http
HTTP/1.1 200 Ok
Content-Length: 150
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 04 Oct 2019 20:35:35 GMT

{
    "id": "42d075a4-bfe7-43e7-af6d-7c68a57edcb4",
    "status": "Completed",
    "productFamily": "Azure",
    "lineItems": [
        {
            "sourceProduct": {
                "id": "b1beb621-3cad-4d7a-b360-62db33ce028e",
                "name": "AzureSubscription"
            },
            "targetProduct": {
                "id": "d231908e-31c1-de0e-027b-bc5ce11f09d9",
                "name": "Microsoft Azure plan"
            },
            "upgradedDate": "2019-08-29T23:47:28.8524555Z",
            "status": "Completed"
        }
    ]
}

```
