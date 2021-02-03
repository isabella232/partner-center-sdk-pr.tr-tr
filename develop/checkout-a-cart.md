---
title: Sepet sonuçlandırma
description: Iş Ortağı Merkezi API 'Lerini kullanarak bir sepetteki müşteriyi bir siparişi nasıl kullanıma alabileceğinizi öğrenin. Bunu bir müşteri siparişini tamamlayacak şekilde yapabilirsiniz.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 094817a34cd29bc96788fcfb6a16610a8192d784
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770079"
---
# <a name="checkout-an-order-for-a-customer-in-a-cart"></a><span data-ttu-id="4ef8b-104">Sepette müşteri için sipariş alma</span><span class="sxs-lookup"><span data-stu-id="4ef8b-104">Checkout an order for a customer in a cart</span></span>

<span data-ttu-id="4ef8b-105">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="4ef8b-105">**Applies to:**</span></span>

- <span data-ttu-id="4ef8b-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ef8b-106">Partner Center</span></span>
- <span data-ttu-id="4ef8b-107">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ef8b-107">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="4ef8b-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ef8b-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="4ef8b-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="4ef8b-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="4ef8b-110">Bir sepette müşteri için sipariş alma.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-110">How to checkout an order for a customer in a cart.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4ef8b-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="4ef8b-111">Prerequisites</span></span>

- <span data-ttu-id="4ef8b-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="4ef8b-113">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="4ef8b-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="4ef8b-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="4ef8b-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="4ef8b-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="4ef8b-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="4ef8b-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="4ef8b-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="4ef8b-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="4ef8b-120">Mevcut bir sepet için sepet KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-120">A Cart ID for an existing cart.</span></span>

## <a name="c"></a><span data-ttu-id="4ef8b-121">C\#</span><span class="sxs-lookup"><span data-stu-id="4ef8b-121">C\#</span></span>

<span data-ttu-id="4ef8b-122">Müşteriye yönelik bir siparişi kullanıma almak için sepet ve müşteri tanımlayıcısını kullanarak sepete bir başvuru alın.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-122">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="4ef8b-123">Son olarak, sıralamayı gerçekleştirmek için **Create** veya **createasync** işlevlerini çağırın.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-123">Finally, call the **Create** or **CreateAsync** functions to complete the order.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string cartId;

var cart = partnerOperations.Customers.ById(customerId).Cart.ById(cartId).Checkout();
```

## <a name="java"></a><span data-ttu-id="4ef8b-124">Java</span><span class="sxs-lookup"><span data-stu-id="4ef8b-124">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](<../includes/java-sdk-support.md>)]

<span data-ttu-id="4ef8b-125">Müşteriye yönelik bir siparişi kullanıma almak için sepet ve müşteri tanımlayıcısını kullanarak sepete bir başvuru alın.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-125">To checkout an order for a customer, get a reference to the cart using the cart and customer identifier.</span></span> <span data-ttu-id="4ef8b-126">Son olarak, sıralamayı gerçekleştirmek için **Create** işlevini çağırın.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-126">Finally, call the **create** function to complete the order.</span></span>

```java
// IAggregatePartner partnerOperations;
// String customerId;
// String cartId;

Cart cart = partnerOperations.getCustomers().byId(customerId).getCart().byId(cartId).checkout();
```

## <a name="powershell"></a><span data-ttu-id="4ef8b-127">PowerShell</span><span class="sxs-lookup"><span data-stu-id="4ef8b-127">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](<../includes/powershell-module-support.md>)]

<span data-ttu-id="4ef8b-128">Bir müşteriye yönelik bir siparişi kullanıma almak için, siparişi tamamladıktan sonra [**Gönder-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) ' i yürütün.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-128">To checkout an order for a customer, execute the [**Submit-PartnerCustomerCart**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Submit-PartnerCustomerCart.md) to complete the order.</span></span>

```powershell
# $customerId
# $cartId

Submit-PartnerCustomerCart -CartId $cartId -CustomerId $customerId
```

## <a name="rest-request"></a><span data-ttu-id="4ef8b-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="4ef8b-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="4ef8b-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="4ef8b-130">Request syntax</span></span>

| <span data-ttu-id="4ef8b-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="4ef8b-131">Method</span></span>   | <span data-ttu-id="4ef8b-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="4ef8b-132">Request URI</span></span>                                                                                                 |
|----------|-------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="4ef8b-133">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="4ef8b-133">**POST**</span></span> | <span data-ttu-id="4ef8b-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-id}/Carts/{cart-id}/Checkout http/1.1</span><span class="sxs-lookup"><span data-stu-id="4ef8b-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/carts/{cart-id}/checkout HTTP/1.1</span></span>     |

### <a name="uri-parameters"></a><span data-ttu-id="4ef8b-135">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="4ef8b-135">URI parameters</span></span>

<span data-ttu-id="4ef8b-136">Müşteriyi tanımlamak ve kullanıma almak istediğiniz sepeti belirtmek için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-136">Use the following path parameters to identify the customer and specify the cart to be checked out.</span></span>

| <span data-ttu-id="4ef8b-137">Ad</span><span class="sxs-lookup"><span data-stu-id="4ef8b-137">Name</span></span>            | <span data-ttu-id="4ef8b-138">Tür</span><span class="sxs-lookup"><span data-stu-id="4ef8b-138">Type</span></span>     | <span data-ttu-id="4ef8b-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="4ef8b-139">Required</span></span> | <span data-ttu-id="4ef8b-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="4ef8b-140">Description</span></span>                                                            |
|-----------------|----------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="4ef8b-141">**müşteri kimliği**</span><span class="sxs-lookup"><span data-stu-id="4ef8b-141">**customer-id**</span></span> | <span data-ttu-id="4ef8b-142">string</span><span class="sxs-lookup"><span data-stu-id="4ef8b-142">string</span></span>   | <span data-ttu-id="4ef8b-143">Yes</span><span class="sxs-lookup"><span data-stu-id="4ef8b-143">Yes</span></span>      | <span data-ttu-id="4ef8b-144">Müşteriyi tanımlayan bir GUID biçimli müşteri kimliği.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-144">A GUID formatted customer-id that identifies the customer.</span></span>             |
| <span data-ttu-id="4ef8b-145">**sepet kimliği**</span><span class="sxs-lookup"><span data-stu-id="4ef8b-145">**cart-id**</span></span>     | <span data-ttu-id="4ef8b-146">string</span><span class="sxs-lookup"><span data-stu-id="4ef8b-146">string</span></span>   | <span data-ttu-id="4ef8b-147">Yes</span><span class="sxs-lookup"><span data-stu-id="4ef8b-147">Yes</span></span>      | <span data-ttu-id="4ef8b-148">Sepeti tanımlayan bir GUID biçimli sepet kimliği.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-148">A GUID formatted cart-id that identifies the cart.</span></span>                     |

### <a name="request-headers"></a><span data-ttu-id="4ef8b-149">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="4ef8b-149">Request headers</span></span>

<span data-ttu-id="4ef8b-150">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="4ef8b-150">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="4ef8b-151">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="4ef8b-151">Request body</span></span>

<span data-ttu-id="4ef8b-152">Yok.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-152">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="4ef8b-153">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="4ef8b-153">Request example</span></span>

```http
POST /v1/customers/d6bf25b7-e0a8-4f2d-a31b-97b55cfc774d/carts/b4c8fdea-cbe4-4d17-9576-13fcacbf9605/checkout HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
X-Locale: en-US
MS-PartnerCenter-Client: Partner Center .NET SDK
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 0
Expect: 100-continue

No-Content-Body
```

## <a name="rest-response"></a><span data-ttu-id="4ef8b-154">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="4ef8b-154">REST response</span></span>

<span data-ttu-id="4ef8b-155">Başarılı olursa, yanıt gövdesi doldurulmuş [Cartcheckoutresult](cart-resources.md#cartcheckoutresult) kaynağını içerir.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-155">If successful, the response body contains the populated [CartCheckoutResult](cart-resources.md#cartcheckoutresult) resource.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="4ef8b-156">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="4ef8b-156">Response success and error codes</span></span>

<span data-ttu-id="4ef8b-157">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-157">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="4ef8b-158">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="4ef8b-158">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="4ef8b-159">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="4ef8b-159">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="4ef8b-160">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="4ef8b-160">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 764
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 0e93c70c-977a-4a88-9580-7cf084c73286
MS-RequestId: 4fa6dad6-a89f-4875-8247-8294a10ae1cf
X-Locale: en-US,en-US
MS-CV: sF/wRa2ih0CzbABc.0
MS-ServerId: 000001
Date: Thu, 15 Mar 2018 17:15:01 GMT
?{
  "orders": [
    {
      "id": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "alternateId": "3c6f2530-1e31-4088-8230-dd1c31a18bce",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "MS-AZR-0145P",
          "subscriptionId": "EF2E1307-86E6-40E3-A794-872403FBD31C",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Microsoft Azure",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.76+00:00",
      "status": "completed",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "311qiN8iFwkv-XARWMvXRYAwYKMACVqv1",
      "alternateId": "0a3624c6e47d",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "one_time",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BQ36:004G:DZH318Z08C0S",
          "termDuration": "P1Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 1 Year",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 1,
          "offerId": "DZH318Z0BQ36:004J:DZH318Z08B8X",
          "termDuration": "P3Y",
          "transactionType": "New",
          "friendlyName": "Reserved VM Instance, Standard_NV12, US East 2, 3 Years",
          "quantity": 1,
          "links": {...}
        },
        {
          "lineItemNumber": 2,
          "offerId": "DG7GMGF0DWM3:0002:DG7GMGF0DT1M",
          "transactionType": "New",
          "friendlyName": "BizTalk Server 2016 Branch",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:51.6578126Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    },
    {
      "id": "HVu_cO8Ea7fNRQP4ia1QTpZap-kg_7P71",
      "alternateId": "55a4e6854d54",
      "referenceCustomerId": "28045616-f6b9-462f-9701-0d89b5e65c44",
      "billingCycle": "monthly",
      "currencyCode": "USD",
      "currencySymbol": "$",
      "lineItems": [
        {
          "lineItemNumber": 0,
          "offerId": "DZH318Z0BXWC:0002:DZH318Z0BMRV",
          "termDuration": "P1M",
          "transactionType": "New",
          "friendlyName": "Barracuda WaaS - Medium Plan",
          "quantity": 1,
          "links": {...}
        }
      ],
      "creationDate": "2019-01-16T00:48:44.4514129Z",
      "status": "pending",
      "transactionType": "UserPurchase",
      "links": {...},
      ...
    }
  ],
  ...
}
```
