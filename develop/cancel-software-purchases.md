---
title: Yazılım satın alımlarını iptal etme
description: Iş Ortağı Merkezi API 'Lerini kullanarak yazılım aboneliklerini ve kalıcı yazılım satın alımlarını iptal etmek için Self Servis seçeneği.
ms.date: 12/19/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 25fd10a171fa6ca01f3442d49145443f2382cc18
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769328"
---
# <a name="cancel-software-purchases"></a><span data-ttu-id="c4823-103">Yazılım satın alımlarını iptal etme</span><span class="sxs-lookup"><span data-stu-id="c4823-103">Cancel software purchases</span></span>

<span data-ttu-id="c4823-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="c4823-104">**Applies to:**</span></span>

- <span data-ttu-id="c4823-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="c4823-105">Partner Center</span></span>

<span data-ttu-id="c4823-106">Iş Ortağı Merkezi API 'Lerini, yazılım aboneliklerini ve kalıcı yazılım satın alımlarını iptal etmek için kullanabilirsiniz (satın alma tarihinden itibaren iptal etme penceresinde yaptığınız sürece).</span><span class="sxs-lookup"><span data-stu-id="c4823-106">You can use the Partner Center APIs to cancel software subscriptions and perpetual software purchases (as long as those purchases were made within the cancellation window from the purchase date).</span></span> <span data-ttu-id="c4823-107">Bu tür iptallerini yapmak için bir destek bileti oluşturmanız gerekmez ve bunun yerine aşağıdaki self servis yöntemlerini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4823-107">You don't need to create a support ticket to make such cancellations, and can use the following self-service methods instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c4823-108">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="c4823-108">Prerequisites</span></span>

- <span data-ttu-id="c4823-109">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="c4823-109">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="c4823-110">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="c4823-110">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="c4823-111">C\#</span><span class="sxs-lookup"><span data-stu-id="c4823-111">C\#</span></span>

<span data-ttu-id="c4823-112">Yazılım sırasını iptal etmek için</span><span class="sxs-lookup"><span data-stu-id="c4823-112">To cancel a software order,</span></span>

1. <span data-ttu-id="c4823-113">İş ortağı işlemlerini almak üzere bir [**ıpartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) arabirimi almak için hesap kimlik bilgilerinizi [**createpartneroperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="c4823-113">Pass your account credentials to the [**CreatePartnerOperations**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**IPartner**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

2. <span data-ttu-id="c4823-114">İptal etmek istediğiniz belirli bir [sıra](order-resources.md#order) seçin.</span><span class="sxs-lookup"><span data-stu-id="c4823-114">Select a particular [Order](order-resources.md#order) you wish to cancel.</span></span> <span data-ttu-id="c4823-115">Customer [**. byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri tanımlayıcısıyla, ardından **Orders. byıd ()** ile Order Identifier ile çağırın.</span><span class="sxs-lookup"><span data-stu-id="c4823-115">Call the [**Customers.ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier, followed by **Orders.ById()** with order identifier.</span></span>

3. <span data-ttu-id="c4823-116">Siparişi almak için **Get** veya **GetAsync** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="c4823-116">Call the **Get** or **GetAsync** method to retrieve the order.</span></span>

4. <span data-ttu-id="c4823-117">[**Order. Status**](order-resources.md#order) özelliğini olarak ayarlayın `cancelled` .</span><span class="sxs-lookup"><span data-stu-id="c4823-117">Set the [**Order.Status**](order-resources.md#order) property to `cancelled`.</span></span>

5. <span data-ttu-id="c4823-118">Seçim İptal için belirli satır öğelerini belirtmek istiyorsanız [**Order. LineItems**](order-resources.md#order) öğesini iptal etmek istediğiniz satır öğeleri listesine ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="c4823-118">(Optional) If you want to specify certain line items for cancellation, set the [**Order.LineItems**](order-resources.md#order) to list of line items that you want to cancel.</span></span>

6. <span data-ttu-id="c4823-119">Sıralamayı güncelleştirmek için **Patch ()** metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4823-119">Use the **Patch()** method to update the order.</span></span>

``` csharp
// IPartnerCredentials accountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner accountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(accountCredentials);

// Cancel order
var order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order.LineItems = new List<OrderLineItem> {
    order.LineItems.First()
};
order = accountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="c4823-120">REST isteği</span><span class="sxs-lookup"><span data-stu-id="c4823-120">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="c4823-121">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="c4823-121">Request syntax</span></span>

| <span data-ttu-id="c4823-122">Yöntem</span><span class="sxs-lookup"><span data-stu-id="c4823-122">Method</span></span>     | <span data-ttu-id="c4823-123">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="c4823-123">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="c4823-124">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="c4823-124">**PATCH**</span></span> | <span data-ttu-id="c4823-125">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="c4823-125">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="c4823-126">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="c4823-126">URI parameters</span></span>

<span data-ttu-id="c4823-127">Bir müşteriyi silmek için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4823-127">Use the following query parameters to delete a customer.</span></span>

| <span data-ttu-id="c4823-128">Ad</span><span class="sxs-lookup"><span data-stu-id="c4823-128">Name</span></span>                   | <span data-ttu-id="c4823-129">Tür</span><span class="sxs-lookup"><span data-stu-id="c4823-129">Type</span></span>     | <span data-ttu-id="c4823-130">Gerekli</span><span class="sxs-lookup"><span data-stu-id="c4823-130">Required</span></span> | <span data-ttu-id="c4823-131">Açıklama</span><span class="sxs-lookup"><span data-stu-id="c4823-131">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="c4823-132">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="c4823-132">**customer-tenant-id**</span></span> | <span data-ttu-id="c4823-133">**guid**</span><span class="sxs-lookup"><span data-stu-id="c4823-133">**guid**</span></span> | <span data-ttu-id="c4823-134">Y</span><span class="sxs-lookup"><span data-stu-id="c4823-134">Y</span></span>        | <span data-ttu-id="c4823-135">Bu değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli müşteri kiracı tanımlayıcısıdır.</span><span class="sxs-lookup"><span data-stu-id="c4823-135">The value is a GUID formatted customer tenant identifier that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="c4823-136">**sıra kimliği**</span><span class="sxs-lookup"><span data-stu-id="c4823-136">**order-id**</span></span> | <span data-ttu-id="c4823-137">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="c4823-137">**string**</span></span> | <span data-ttu-id="c4823-138">Y</span><span class="sxs-lookup"><span data-stu-id="c4823-138">Y</span></span>        | <span data-ttu-id="c4823-139">Değer, iptal etmek istediğiniz sıranın tanımlayıcısını gösteren bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="c4823-139">The value is a string that denotes the identifier of the order that you want to cancel.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="c4823-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="c4823-140">Request headers</span></span>

<span data-ttu-id="c4823-141">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="c4823-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="c4823-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="c4823-142">Request body</span></span>

```http
{
    “id”: “2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

### <a name="request-example"></a><span data-ttu-id="c4823-143">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="c4823-143">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "status": "cancelled",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS"
        }
    ]
}
```

## <a name="rest-response"></a><span data-ttu-id="c4823-144">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="c4823-144">REST response</span></span>

<span data-ttu-id="c4823-145">Başarılı olursa, bu yöntem iptal edilen satır öğelerinin sırasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="c4823-145">If successful, this method returns the order with canceled line items.</span></span>

<span data-ttu-id="c4823-146">Sipariş durumu, siparişteki tüm satır öğeleri iptal edildiğinde iptal **edildi** olarak işaretlenir veya siparişteki tüm satır öğeleri iptal edilmediğinde **tamamlanacaktır** .</span><span class="sxs-lookup"><span data-stu-id="c4823-146">The order status will be marked as either **cancelled** if all the line items in the order are cancelled, or **completed** if not all line items in the order are canceled.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="c4823-147">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="c4823-147">Response success and error codes</span></span>

<span data-ttu-id="c4823-148">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="c4823-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="c4823-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="c4823-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="c4823-150">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="c4823-150">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="c4823-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="c4823-151">Response example</span></span>

<span data-ttu-id="c4823-152">Aşağıdaki örnek yanıtta, teklif tanımlayıcısına sahip olan satır öğesi miktarının **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** sıfır (0) hale geldiğini görebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="c4823-152">In the following example response, you can see that the quantity of line item with the offer identifier **`DG7GMGF0FKZV:0003:DG7GMGF0DWMS`** has become zero (0).</span></span> <span data-ttu-id="c4823-153">Bu değişiklik, iptal için işaretlenen satır öğesinin başarıyla iptal edildiği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c4823-153">This change means that the line item that was marked for cancellation has been canceled successfully.</span></span> <span data-ttu-id="c4823-154">Örnek sıra, iptal edilmemiş diğer satır öğelerini içerir, bu da genel siparişin durumunun **tamamlandı** olarak işaretleneceği, **iptal** edilmeyeceği anlamına gelir.</span><span class="sxs-lookup"><span data-stu-id="c4823-154">The example order contains other line items that weren't canceled, which means that the status of the overall order will be marked as **completed**, not **cancelled**.</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
    "alternateId": "c403d91b21d2",
    "referenceCustomerId": "45411344-b09d-47e7-9653-542006bf9766",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0FKZV:0003:DG7GMGF0DWMS",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "SQL Server Enterprise - 2 Core License Pack - 3 year",
            "quantity": 0,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0FKZV?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0FKZV/skus/0003/availabilities/DG7GMGF0DWMS?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        },
        {
            "lineItemNumber": 1,
            "offerId": "DG7GMGF0DVT7:000C:DG7GMGF0FVZM",
            "termDuration": "P3Y",
            "transactionType": "New",
            "friendlyName": "Windows Server CAL - 1 Device CAL - 3 year",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DVT7?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DVT7/skus/000C/availabilities/DG7GMGF0FVZM?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-12-12T17:33:56.1306495Z",
    "status": "completed",
    "transactionType": "UserPurchase",
    "links": {
        "self": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "GET",
            "headers": []
        },
        "provisioningStatus": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1/provisioningstatus",
            "method": "GET",
            "headers": []
        },
        "patchOperation": {
            "uri": "/customers/45411344-b09d-47e7-9653-542006bf9766/orders/2y6dF_rVgDAXMxypQPPnTquuXhKVK_3N1",
            "method": "PATCH",
            "headers": []
        }
    },
    "client": {
        "marketplaceCountry": "US",
        "deviceFamily": "UniversalStore-PartnerCenter",
        "name": "Partner Center API"
    },
    "attributes": {
        "objectType": "Order"
    }
}
```
