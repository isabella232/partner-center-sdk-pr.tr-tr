---
title: Sipariş satırı öğesine göre etkinleştirme bağlantısını alma
description: Sipariş satırı öğesine göre abonelik etkinleştirme bağlantısını alır.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: aa02a5a5b4a281b96e32ee6d239cc440cf8af4ec
ms.sourcegitcommit: d4b0c80d81f1d5bdf3c4c03344ad639646ae6ab9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111760785"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="b8b9d-103">Sipariş satırı öğesine göre etkinleştirme bağlantısını alma</span><span class="sxs-lookup"><span data-stu-id="b8b9d-103">Get activation link by order line item</span></span>

<span data-ttu-id="b8b9d-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="b8b9d-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="b8b9d-105">Sipariş satırı öğe numarasına göre ticari market aboneliği etkinleştirme bağlantısını alır.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-105">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="b8b9d-106">İş Ortağı Merkezi panosunda, ana sayfada Abonelik altında Belirli bir  Abonelik seçerek veya Abonelikler sayfasında etkinleştirmek için aboneliğin yanındaki **Publisher'nin sitesine** git bağlantısını seçerek bu işlemi  **yapabilirsiniz.**</span><span class="sxs-lookup"><span data-stu-id="b8b9d-106">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b8b9d-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="b8b9d-107">Prerequisites</span></span>

- <span data-ttu-id="b8b9d-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="b8b9d-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="b8b9d-109">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-109">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="b8b9d-110">Etkinleştirmesi gereken ürünle sipariş tamamlandı.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-110">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="b8b9d-111">C\#</span><span class="sxs-lookup"><span data-stu-id="b8b9d-111">C\#</span></span>

<span data-ttu-id="b8b9d-112">Bir satır öğesinin etkinleştirme bağlantısını almak için [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonu kullanın ve seçilen müşteri kimliğiyle [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini arayın.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-112">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="b8b9d-113">Ardından Orders [**özelliğini ve**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) belirttiğiniz [**OrderId değeriyle çağırabilirsiniz.**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id)</span><span class="sxs-lookup"><span data-stu-id="b8b9d-113">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="b8b9d-114">Ardından satır öğesi numarası tanımlayıcısıyla **ById()** yöntemiyle [**LineItems'i**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-114">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="b8b9d-115">Son olarak **ActivationLinks() yöntemini** arayın.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-115">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="b8b9d-116">REST isteği</span><span class="sxs-lookup"><span data-stu-id="b8b9d-116">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="b8b9d-117">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="b8b9d-117">Request syntax</span></span>

| <span data-ttu-id="b8b9d-118">Yöntem</span><span class="sxs-lookup"><span data-stu-id="b8b9d-118">Method</span></span>  | <span data-ttu-id="b8b9d-119">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="b8b9d-119">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="b8b9d-120">**Al**</span><span class="sxs-lookup"><span data-stu-id="b8b9d-120">**GET**</span></span> | <span data-ttu-id="b8b9d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="b8b9d-121">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="b8b9d-122">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="b8b9d-122">Request headers</span></span>

<span data-ttu-id="b8b9d-123">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="b8b9d-123">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="b8b9d-124">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="b8b9d-124">Request body</span></span>

<span data-ttu-id="b8b9d-125">Yok.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-125">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="b8b9d-126">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="b8b9d-126">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="b8b9d-127">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="b8b9d-127">REST response</span></span>

<span data-ttu-id="b8b9d-128">Başarılı olursa, bu yöntem yanıt [gövdesinde bir](customer-resources.md#customer) Müşteri kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-128">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="b8b9d-129">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="b8b9d-129">Response success and error codes</span></span>

<span data-ttu-id="b8b9d-130">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-130">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="b8b9d-131">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="b8b9d-131">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="b8b9d-132">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="b8b9d-132">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="b8b9d-133">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="b8b9d-133">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 809
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT
{
  "totalCount": 1,
  "items": [
    {
      "lineItemNumber": 0,
      "link": {
        "uri": "<link populated here>",
        "method": "GET",
        "headers": [

        ]
      }
    }
  ],
  "links": {
    "self": {
      "uri": "/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "Collection"
  }
}
```
