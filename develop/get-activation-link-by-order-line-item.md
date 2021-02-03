---
title: Sipariş satırı öğesine göre etkinleştirme bağlantısını alma
description: Sipariş satırı öğesine göre bir abonelik etkinleştirme bağlantısı alır.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: rbars
ms.author: rbars
ms.openlocfilehash: c0e84888870571cf6bd21306f527863f2aa7ee85
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769268"
---
# <a name="get-activation-link-by-order-line-item"></a><span data-ttu-id="5f7f0-103">Sipariş satırı öğesine göre etkinleştirme bağlantısını alma</span><span class="sxs-lookup"><span data-stu-id="5f7f0-103">Get activation link by order line item</span></span>

<span data-ttu-id="5f7f0-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="5f7f0-104">**Applies To**</span></span>

- <span data-ttu-id="5f7f0-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5f7f0-105">Partner Center</span></span>
- <span data-ttu-id="5f7f0-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5f7f0-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="5f7f0-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5f7f0-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="5f7f0-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5f7f0-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5f7f0-109">Sipariş satırı öğe numarasına göre ticari Market aboneliği etkinleştirme bağlantısını alır.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-109">Gets a commercial marketplace subscription activation link by the order line item number.</span></span>

<span data-ttu-id="5f7f0-110">Iş Ortağı Merkezi panosunda, ana sayfada **abonelik** bölümünde **belirli bir aboneliği** seçerek veya **abonelikler** sayfasında etkinleştirilecek aboneliğin yanındaki **yayımcının site bağlantısına git** ' i seçerek bu işlemi yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-110">In the Partner Center dashboard, you can do this operation by selecting either a **Specific Subscription** under **Subscription** on the main page, or selecting the **Go to Publisher's site** link next to the subscription to activate on the **Subscriptions** page.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5f7f0-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5f7f0-111">Prerequisites</span></span>

- <span data-ttu-id="5f7f0-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5f7f0-113">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5f7f0-114">Etkinleştirmesi gereken ürün ile tamamlanmış sıra.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-114">Completed order with product that needs activation.</span></span>

## <a name="c"></a><span data-ttu-id="5f7f0-115">C\#</span><span class="sxs-lookup"><span data-stu-id="5f7f0-115">C\#</span></span>

<span data-ttu-id="5f7f0-116">Bir satır öğesinin etkinleştirme bağlantısını almak için, [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini seçili müşteri kimliğiyle çağırın.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-116">To get a line item's activation link, use your [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the selected customer ID.</span></span> <span data-ttu-id="5f7f0-117">Ardından [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) özelliğini ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) yöntemini belirtilen  [**siparişkimliğiniz**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id)ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-117">Then call the [**Orders**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.orders) property and the [**ById()**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.byid) method with your specified  [**OrderId**](/dotnet/api/microsoft.store.partnercenter.models.orders.order.id).</span></span> <span data-ttu-id="5f7f0-118">Ardından, satır öğesi numara tanımlayıcısı ile **Byıd ()** yöntemi Ile [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) çağrısı yapın.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-118">Then, call the [**LineItems**](/dotnet/api/microsoft.store.partnercenter.orders.iordercollection.get) with **ById()** method with the line item number identifier.</span></span>  <span data-ttu-id="5f7f0-119">Son olarak, **Activationlinks ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-119">Finally, call the **ActivationLinks()** method.</span></span>

```csharp
// IAggregatePartner partnerOperations;
// string customerId;
// string orderId;
// string lineItemNumber

// get the activation link for the specific line item
var partnerOperations.Customers.ById(customerId).Orders.ById(orderId).OrderLineItems.ById(lineItemNumber).ActivationLinks();
```

## <a name="rest-request"></a><span data-ttu-id="5f7f0-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5f7f0-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5f7f0-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5f7f0-121">Request syntax</span></span>

| <span data-ttu-id="5f7f0-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5f7f0-122">Method</span></span>  | <span data-ttu-id="5f7f0-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5f7f0-123">Request URI</span></span>                                                                                                                               |
|---------|-------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5f7f0-124">**Al**</span><span class="sxs-lookup"><span data-stu-id="5f7f0-124">**GET**</span></span> | <span data-ttu-id="5f7f0-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{CustomerID}/Orders/{OrderID}/LineItem/{lineıtemnumber}/activationlinks http/1.1</span><span class="sxs-lookup"><span data-stu-id="5f7f0-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customerId}/orders/{orderId}/lineitems/{lineItemNumber}/activationlinks HTTP/1.1</span></span> |

### <a name="request-headers"></a><span data-ttu-id="5f7f0-126">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5f7f0-126">Request headers</span></span>

<span data-ttu-id="5f7f0-127">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5f7f0-127">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5f7f0-128">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5f7f0-128">Request body</span></span>

<span data-ttu-id="5f7f0-129">Yok.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-129">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5f7f0-130">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5f7f0-130">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/8c5b65fd-c725-4f50-8d9c-97ec9169fdd0/orders/03fb46b3-bf8c-49aa-b908-ca2e93bcc04a/lineitems/0/activationlinks HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="5f7f0-131">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5f7f0-131">REST response</span></span>

<span data-ttu-id="5f7f0-132">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Müşteri](customer-resources.md#customer) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-132">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5f7f0-133">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5f7f0-133">Response success and error codes</span></span>

<span data-ttu-id="5f7f0-134">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-134">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5f7f0-135">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5f7f0-135">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5f7f0-136">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5f7f0-136">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5f7f0-137">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5f7f0-137">Response example</span></span>

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
