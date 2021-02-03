---
title: Müşteri için ürün yükseltme durumunu alın
description: Bir müşteri için ürün yükseltmenin durumunu bir Azure planına Microsoft Azure (MS-AZR-0145P) aboneliği gibi yeni bir ürün ailesine yönelik olarak öğrenmek için Productyükselderequest kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1819887d459ec72a48ea2b7a5a4121dc56718313
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769059"
---
# <a name="get-the-product-upgrade-status-for-a-customer"></a><span data-ttu-id="59096-103">Müşteri için ürün yükseltme durumunu alın</span><span class="sxs-lookup"><span data-stu-id="59096-103">Get the product upgrade status for a customer</span></span>

<span data-ttu-id="59096-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="59096-104">**Applies to:**</span></span>

- <span data-ttu-id="59096-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="59096-105">Partner Center</span></span>

<span data-ttu-id="59096-106">Yeni bir ürün ailesine yükseltmenin durumunu almak için [**Productyükseltiderequest**](product-upgrade-resources.md#productupgraderequest) kaynağını kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59096-106">You can use the [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource to get the status of an upgrade to a new product family.</span></span> <span data-ttu-id="59096-107">Bu kaynak, bir müşteriyi bir Microsoft Azure (MS-AZR-0145P) aboneliğinden bir Azure planına yükselttiğinizde geçerlidir.</span><span class="sxs-lookup"><span data-stu-id="59096-107">This resource applies when you're upgrading a customer from an Microsoft Azure (MS-AZR-0145P) subscription to an Azure plan.</span></span> <span data-ttu-id="59096-108">Başarılı bir istek [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağını döndürür.</span><span class="sxs-lookup"><span data-stu-id="59096-108">A successful request returns the [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="59096-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="59096-109">Prerequisites</span></span>

- <span data-ttu-id="59096-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="59096-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="59096-111">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="59096-111">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="59096-112">Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="59096-112">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="59096-113">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="59096-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="59096-114">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59096-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="59096-115">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="59096-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="59096-116">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="59096-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="59096-117">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="59096-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="59096-118">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="59096-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="59096-119">Ürün ailesi.</span><span class="sxs-lookup"><span data-stu-id="59096-119">The product family.</span></span>

- <span data-ttu-id="59096-120">Yükseltme isteğinin yükseltme kimliği.</span><span class="sxs-lookup"><span data-stu-id="59096-120">The upgrade-id of an upgrade request.</span></span>

## <a name="c"></a><span data-ttu-id="59096-121">C\#</span><span class="sxs-lookup"><span data-stu-id="59096-121">C\#</span></span>

<span data-ttu-id="59096-122">Müşterinin Azure planına yükseltmeye uygun olup olmadığını denetlemek için:</span><span class="sxs-lookup"><span data-stu-id="59096-122">To check if a customer is eligible to upgrade to Azure plan:</span></span>

1. <span data-ttu-id="59096-123">**Productupgradesrequest** nesnesi oluşturun ve ürün ailesi olarak müşteri tanımlayıcısını ve "Azure" i belirtin.</span><span class="sxs-lookup"><span data-stu-id="59096-123">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="59096-124">**Iaggregatepartner. Productyükseltmeleri** koleksiyonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="59096-124">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="59096-125">**Byıd** metodunu çağırın ve **yükseltme-kimliği**' ni geçirin.</span><span class="sxs-lookup"><span data-stu-id="59096-125">Call the **ById** method and pass in the **upgrade-id**.</span></span>

4. <span data-ttu-id="59096-126">**CheckStatus** metodunu çağırın ve **productupgradestatus** nesnesini döndürecek **productupgradesrequest** nesnesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="59096-126">Call the **CheckStatus** method and pass in the **ProductUpgradesRequest** object, which will return a **ProductUpgradeStatus** object.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="59096-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="59096-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="59096-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="59096-128">Request syntax</span></span>

| <span data-ttu-id="59096-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="59096-129">Method</span></span>   | <span data-ttu-id="59096-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="59096-130">Request URI</span></span> |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="59096-131">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="59096-131">**POST**</span></span> | <span data-ttu-id="59096-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/productupgrades/{Upgrade-id}/Status http/1.1</span><span class="sxs-lookup"><span data-stu-id="59096-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/productUpgrades/{upgrade-id}/status HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="59096-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="59096-133">URI parameter</span></span>

<span data-ttu-id="59096-134">Ürün yükseltme durumu almak istediğiniz müşteriyi belirtmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="59096-134">Use the following query parameter to specify the customer for whom you're getting a product upgrade status.</span></span>

| <span data-ttu-id="59096-135">Ad</span><span class="sxs-lookup"><span data-stu-id="59096-135">Name</span></span>               | <span data-ttu-id="59096-136">Tür</span><span class="sxs-lookup"><span data-stu-id="59096-136">Type</span></span> | <span data-ttu-id="59096-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="59096-137">Required</span></span> | <span data-ttu-id="59096-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="59096-138">Description</span></span>                                                                                 |
|--------------------|------|----------|---------------------------------------------------------------------------------------------|
| <span data-ttu-id="59096-139">**yükseltme kimliği**</span><span class="sxs-lookup"><span data-stu-id="59096-139">**upgrade-id**</span></span> | <span data-ttu-id="59096-140">GUID</span><span class="sxs-lookup"><span data-stu-id="59096-140">GUID</span></span> | <span data-ttu-id="59096-141">Yes</span><span class="sxs-lookup"><span data-stu-id="59096-141">Yes</span></span> | <span data-ttu-id="59096-142">Değer, GUID biçimli bir yükseltme tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="59096-142">The value is a GUID-formatted upgrade identifier.</span></span> <span data-ttu-id="59096-143">Bu tanımlayıcıyı, izlemek üzere bir yükseltme belirtmek için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="59096-143">You can use this identifier to specify an upgrade to track.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="59096-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="59096-144">Request headers</span></span>

<span data-ttu-id="59096-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="59096-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="59096-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="59096-146">Request body</span></span>

<span data-ttu-id="59096-147">İstek gövdesi bir [**Productyükseltilebilir Derequest**](product-upgrade-resources.md#productupgraderequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="59096-147">The request body must contain a [**ProductUpgradeRequest**](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

### <a name="request-example"></a><span data-ttu-id="59096-148">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="59096-148">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="59096-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="59096-149">REST response</span></span>

<span data-ttu-id="59096-150">Başarılı olursa, bu yöntem gövdede bir [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) kaynağı döndürür.</span><span class="sxs-lookup"><span data-stu-id="59096-150">If successful, this method returns a [**ProductUpgradesEligibility**](product-upgrade-resources.md#productupgradeseligibility) resource in the body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="59096-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="59096-151">Response success and error codes</span></span>

<span data-ttu-id="59096-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="59096-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="59096-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="59096-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="59096-154">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="59096-154">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="59096-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="59096-155">Response example</span></span>

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
