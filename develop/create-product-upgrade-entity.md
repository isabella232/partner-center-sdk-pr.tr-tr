---
title: Müşteri için ürün yükseltme varlığı oluşturma
description: Bir müşteriyi belirli bir ürün ailesine yükseltmek üzere ürün yükseltme varlığı oluşturmak için ProductUpgradeRequest kaynağını kullanabilirsiniz.
ms.date: 11/01/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4e346b7f5294a8847047c85115d8c80f34eaca84
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973426"
---
# <a name="create-a-product-upgrade-entity-for-a-customer"></a><span data-ttu-id="0caf7-103">Müşteri için ürün yükseltme varlığı oluşturma</span><span class="sxs-lookup"><span data-stu-id="0caf7-103">Create a product upgrade entity for a customer</span></span>

<span data-ttu-id="0caf7-104">**ProductUpgradeRequest** kaynağını kullanarak bir müşteriyi belirli bir ürün ailesine (örneğin, Azure planı) yükseltmek için bir ürün yükseltme varlığı oluşturabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0caf7-104">You can create a product upgrade entity to upgrade a customer to a given product family (for example, Azure plan) using the **ProductUpgradeRequest** resource.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0caf7-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0caf7-105">Prerequisites</span></span>

- <span data-ttu-id="0caf7-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="0caf7-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0caf7-107">Bu senaryo, App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="0caf7-107">This scenario supports authentication with App+User credentials.</span></span> <span data-ttu-id="0caf7-108">[Uygulama+Kullanıcı kimlik doğrulamasını](enable-secure-app-model.md) farklı API'lerle kullanırken güvenli İş Ortağı Merkezi izleyin.</span><span class="sxs-lookup"><span data-stu-id="0caf7-108">Follow the [secure app model](enable-secure-app-model.md) when using App+User authentication with Partner Center APIs.</span></span>

- <span data-ttu-id="0caf7-109">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0caf7-109">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0caf7-110">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="0caf7-110">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0caf7-111">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="0caf7-111">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0caf7-112">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="0caf7-112">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0caf7-113">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="0caf7-113">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0caf7-114">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="0caf7-114">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="0caf7-115">Müşteriyi yükseltmek istediğiniz ürün ailesi.</span><span class="sxs-lookup"><span data-stu-id="0caf7-115">The product family to which you want to upgrade the customer.</span></span>

## <a name="c"></a><span data-ttu-id="0caf7-116">C\#</span><span class="sxs-lookup"><span data-stu-id="0caf7-116">C\#</span></span>

<span data-ttu-id="0caf7-117">Bir müşteriyi Azure planına yükseltmek için:</span><span class="sxs-lookup"><span data-stu-id="0caf7-117">To upgrade a customer to Azure plan:</span></span>

1. <span data-ttu-id="0caf7-118">Bir **ProductUpgradesRequest nesnesi** oluşturun ve müşteri tanımlayıcısını ve ürün ailesi olarak "Azure" belirtin.</span><span class="sxs-lookup"><span data-stu-id="0caf7-118">Create a **ProductUpgradesRequest** object and specify the customer identifier and "Azure" as the product family.</span></span>

2. <span data-ttu-id="0caf7-119">**IAggregatePartner.ProductUpgrades koleksiyonunu** kullanın.</span><span class="sxs-lookup"><span data-stu-id="0caf7-119">Use the **IAggregatePartner.ProductUpgrades** collection.</span></span>

3. <span data-ttu-id="0caf7-120">**Create** yöntemini çağırarak **ProductUpgradesRequest nesnesini** iletin; bu nesne bir konum üst **bilgisi dizesi** döndürür.</span><span class="sxs-lookup"><span data-stu-id="0caf7-120">Call the **Create** method and pass in the **ProductUpgradesRequest** object, which will return a **location header** string.</span></span>

4. <span data-ttu-id="0caf7-121">Yükseltme **durumunu sorgulamak** için kullanılan konum üst bilgisi dizesinde [upgrade-id'sini ayıklar.](get-product-upgrade-status.md)</span><span class="sxs-lookup"><span data-stu-id="0caf7-121">Extract the **upgrade-id** from the location header string that can be used to [query the upgrade status](get-product-upgrade-status.md).</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="0caf7-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0caf7-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0caf7-123">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="0caf7-123">Request syntax</span></span>

| <span data-ttu-id="0caf7-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0caf7-124">Method</span></span>   | <span data-ttu-id="0caf7-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0caf7-125">Request URI</span></span>                                                                                   |
|----------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="0caf7-126">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="0caf7-126">**POST**</span></span> | <span data-ttu-id="0caf7-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="0caf7-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/productupgrades HTTP/1.1</span></span> |

#### <a name="request-headers"></a><span data-ttu-id="0caf7-128">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0caf7-128">Request headers</span></span>

<span data-ttu-id="0caf7-129">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="0caf7-129">For more information, see [Partner Center REST headers](headers.md).</span></span>

#### <a name="request-body"></a><span data-ttu-id="0caf7-130">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0caf7-130">Request body</span></span>

<span data-ttu-id="0caf7-131">İstek gövdesi bir [ProductUpgradeRequest kaynağı içermeli.](product-upgrade-resources.md#productupgraderequest)</span><span class="sxs-lookup"><span data-stu-id="0caf7-131">The request body must contain a [ProductUpgradeRequest](product-upgrade-resources.md#productupgraderequest) resource.</span></span>

#### <a name="request-example"></a><span data-ttu-id="0caf7-132">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0caf7-132">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="0caf7-133">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0caf7-133">REST response</span></span>

<span data-ttu-id="0caf7-134">Başarılı olursa yanıt, ürün yükseltme **durumunu** almak için URI'ye sahip bir Konum üst bilgisi içerir.</span><span class="sxs-lookup"><span data-stu-id="0caf7-134">If successful, the response contains a **Location** header that has a URI that can be used to retrieve product upgrade status.</span></span> <span data-ttu-id="0caf7-135">Bu URI'yi diğer ilgili REST API'leriyle kullanmak üzere kaydedin.</span><span class="sxs-lookup"><span data-stu-id="0caf7-135">Save this URI for use with other related REST APIs.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0caf7-136">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0caf7-136">Response success and error codes</span></span>

<span data-ttu-id="0caf7-137">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="0caf7-137">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0caf7-138">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0caf7-138">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0caf7-139">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="0caf7-139">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0caf7-140">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0caf7-140">Response example</span></span>

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
