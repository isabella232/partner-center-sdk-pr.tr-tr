---
title: Müşteri için ürün yükseltme varlığı oluşturma
description: Bir müşteriyi belirli bir ürün ailesine yükseltmek üzere ürün yükseltme varlığı oluşturmak için Productyükselderequest kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 45830033d93e0906eafc169cf04b997e2ff7c3d8
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768813"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="96b49-103">Müşteri için ürün yükseltme varlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="96b49-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="96b49-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="96b49-104">**Applies to:**</span></span>

- <span data-ttu-id="96b49-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="96b49-105">Partner Center</span></span>

<span data-ttu-id="96b49-106">Bir müşteriyi, **Productyükselderequest** kaynağını kullanarak belirli bir ürün ailesine (örneğin, Azure planı) yükseltmek için bir ürün yükseltme varlığı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96b49-106">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96b49-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="96b49-107">Prerequisites</span></span>

- <span data-ttu-id="96b49-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="96b49-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="96b49-109">Bu senaryo, uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="96b49-109">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="96b49-110">Iş Ortağı Merkezi API 'Leriyle App + kullanıcı kimlik doğrulaması kullanırken [güvenli uygulama modelini](enable-secure-app-model.md) izleyin.</span><span class="sxs-lookup"><span data-stu-id="96b49-110">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="96b49-111">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="96b49-111">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="96b49-112">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="96b49-112">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="96b49-113">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="96b49-113">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="96b49-114">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="96b49-114">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="96b49-115">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="96b49-115">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="96b49-116">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="96b49-116">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="96b49-117">Müşteriyi yükseltmek istediğiniz ürün ailesi.</span><span class="sxs-lookup"><span data-stu-id="96b49-117">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="96b49-118">C\#</span><span class="sxs-lookup"><span data-stu-id="96b49-118">C\#</span></span>

<span data-ttu-id="96b49-119">Bir müşteriyi Azure planına yükseltmek için:</span><span class="sxs-lookup"><span data-stu-id="96b49-119">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="96b49-120">**Productupgradesrequest** nesnesi oluşturun ve ürün ailesi olarak müşteri tanımlayıcısını ve "Azure" i belirtin.</span><span class="sxs-lookup"><span data-stu-id="96b49-120">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="96b49-121">**Iaggregatepartner. Productyükseltmeleri** koleksiyonunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="96b49-121">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="96b49-122">**Create** metodunu çağırın ve bir **konum üst bilgi** dizesi döndürecek **productupgradesrequest** nesnesini geçirin.</span><span class="sxs-lookup"><span data-stu-id="96b49-122">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="96b49-123">Yükseltme [durumunu sorgulamak](get-product-upgrade-status.md)için kullanılabilecek konum üst bilgisi dizesinden **Upgrade-ID** ' i ayıklayın.</span><span class="sxs-lookup"><span data-stu-id="96b49-123">Extract the **upgrade-id** from the location header string which can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

```csharp
// IAggregatePartner partnerOperations;

string selectedCustomerId = "58e2af4f-0ad3-4688-8744-be2357cd939a";

string selectedProductFamily = "Azure";

var productUpgradeRequest = new ProductUpgradesRequest
{
    CustomerId = selectedCustomerId,
    ProductFamily = selectedProductFamily
};

var productUpgradeLocationHeader = partnerOperations.ProductUpgrades.Create(productUpgradeRequest);

var upgradeId = Regex.Split(productUpgradeLocationHeader, "/")[1];

```

## <a name="rest-request"></a><span data-ttu-id="96b49-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="96b49-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="96b49-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="96b49-125">Request syntax</span></span>

| <span data-ttu-id="96b49-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="96b49-126">Method</span></span>   | <span data-ttu-id="96b49-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="96b49-127">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="96b49-128">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="96b49-128">**POST**</span></span> | <span data-ttu-id="96b49-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/productyükseltmeleri http/1.1</span><span class="sxs-lookup"><span data-stu-id="96b49-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="96b49-130">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="96b49-130">Request headers</span></span>

<span data-ttu-id="96b49-131">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="96b49-131">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="96b49-132">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="96b49-132">Request body</span></span>

<span data-ttu-id="96b49-133">İstek gövdesi bir [Productyükseltilebilir Derequest](product-upgrade-resources.md#productupgraderequest) kaynağı içermelidir.</span><span class="sxs-lookup"><span data-stu-id="96b49-133">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="96b49-134">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="96b49-134">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/productupgrades HTTP/1.1
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
  "productFamily": "Azure"
}
```

## <a name="rest-response"></a><span data-ttu-id="96b49-135">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="96b49-135">REST response</span></span>

<span data-ttu-id="96b49-136">Başarılı olursa, yanıt ürün yükseltme durumunu almak için kullanılabilecek bir URI 'ye sahip bir **konum** üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="96b49-136">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="96b49-137">Bu URI 'yi diğer ilgili REST API 'Leri ile kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="96b49-137">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="96b49-138">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="96b49-138">Response success and error codes</span></span>

<span data-ttu-id="96b49-139">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="96b49-139">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="96b49-140">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="96b49-140">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="96b49-141">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="96b49-141">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="96b49-142">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="96b49-142">Response example</span></span>

```http
HTTP/1.1 202 Accepted
Content-Length: 0
Location: productUpgrades/42d075a4-bfe7-43e7-af6d-7c68a57edcb4
MS-CorrelationId: 772871a9-399b-4f3b-b8c7-38f550e4f22a
MS-RequestId: cb82f7d6-f0d9-44d4-82f9-f6eee6e68390
MS-CV: iqOqN0FnaE2y0HcD.0
MS-ServerId: 030020525
Date: Thu, 28 Sep 2019 20:35:35 GMT
```
