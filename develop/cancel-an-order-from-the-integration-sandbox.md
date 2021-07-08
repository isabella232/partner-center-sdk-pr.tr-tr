---
title: Tümleştirme korumalı alandan siparişi iptal etme
description: Tümleştirme korumalı alan hesaplarından İş Ortağı Merkezi abonelik siparişlerini iptal etmek için api'leri kullanmayı öğrenin.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4c4b658f406e420d8d3cd425688364fe3d440d3d
ms.sourcegitcommit: a3a78ec0f5078645b5a4f3b534165eef30f2c822
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/30/2021
ms.locfileid: "113104980"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="64b95-103">Api'leri kullanarak tümleştirme korumalı alandan İş Ortağı Merkezi iptal etme</span><span class="sxs-lookup"><span data-stu-id="64b95-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="64b95-104">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi 21Vianet | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="64b95-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="64b95-105">Bu makalede tümleştirme korumalı alan hesaplarından farklı İş Ortağı Merkezi sipariş türlerini iptal etmek için api'leri kullanma işlemi açıklanmıştır.</span><span class="sxs-lookup"><span data-stu-id="64b95-105">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="64b95-106">Bu tür siparişler ayrılmış örnekler, yazılımlar ve ticari market Hizmet Olarak Yazılım (SaaS) abonelik siparişlerini içerebilir.</span><span class="sxs-lookup"><span data-stu-id="64b95-106">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

> [!NOTE] 
> <span data-ttu-id="64b95-107">Ayrılmış örnek veya ticari market SaaS abonelik siparişlerinin iptallerinin yalnızca tümleştirme korumalı alan hesaplarından mümkün olduğunu unutmayın.</span><span class="sxs-lookup"><span data-stu-id="64b95-107">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span> <span data-ttu-id="64b95-108">60 günden eski olan tüm korumalı alan siparişleri, İş Ortağı Merkezi.</span><span class="sxs-lookup"><span data-stu-id="64b95-108">Any sandbox orders which are older than 60 days cannot be cancelled from Partner Center.</span></span>

<span data-ttu-id="64b95-109">API aracılığıyla yazılım üretim siparişlerini iptal etmek için [cancel-software-purchases kullanın.](cancel-software-purchases.md)</span><span class="sxs-lookup"><span data-stu-id="64b95-109">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="64b95-110">Ayrıca, satın alma işlemini iptal etmek için pano aracılığıyla yazılım üretim [siparişlerini iptal edebilirsiniz.](/partner-center/csp-software-subscriptions)</span><span class="sxs-lookup"><span data-stu-id="64b95-110">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="64b95-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="64b95-111">Prerequisites</span></span>

- <span data-ttu-id="64b95-112">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="64b95-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="64b95-113">Bu senaryo hem tek başına Uygulama hem de Uygulama+Kullanıcı kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="64b95-113">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="64b95-114">Etkin ayrılmış örnek / yazılım / üçüncü taraf SaaS abonelik siparişleri olan bir müşteriyle tümleştirme korumalı alan iş ortağı hesabı.</span><span class="sxs-lookup"><span data-stu-id="64b95-114">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="64b95-115">C\#</span><span class="sxs-lookup"><span data-stu-id="64b95-115">C\#</span></span>

<span data-ttu-id="64b95-116">Tümleştirme korumalı alandan bir siparişi iptal etmek için hesap kimlik bilgilerinizi yöntemine iletir ve iş ortağı [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) işlemlerini almak için bir arabirim elde [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) edin.</span><span class="sxs-lookup"><span data-stu-id="64b95-116">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="64b95-117">Belirli bir [Sipariş seçmek için](order-resources.md#order)iş ortağı işlemlerini kullanın ve müşteri tanımlayıcısını müşteri tanımlayıcısıyla birlikte çağırma yöntemini, ardından sipariş tanımlayıcısını kullanarak siparişi ve son olarak da alma [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini **`Orders.ById()`** **`Get`** **`GetAsync`** belirtin.</span><span class="sxs-lookup"><span data-stu-id="64b95-117">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="64b95-118">özelliğini [**`Order.Status`**](order-resources.md#order) olarak ayarlayın `cancelled` ve yöntemini kullanarak **`Patch()`** siparişi güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="64b95-118">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

``` csharp
// IPartnerCredentials tipAccountCredentials;
// Customer tenant Id to be deleted.
// string customerTenantId;

IPartner tipAccountPartnerOperations = PartnerService.Instance.CreatePartnerOperations(tipAccountCredentials);

// Cancel order
var order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Get();
order.Status = "cancelled";
order = tipAccountPartnerOperations.Customers.ById(customerTenantId).Orders.ById(orderId).Patch(order);

```

## <a name="rest-request"></a><span data-ttu-id="64b95-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="64b95-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="64b95-120">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="64b95-120">Request syntax</span></span>

| <span data-ttu-id="64b95-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="64b95-121">Method</span></span>     | <span data-ttu-id="64b95-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="64b95-122">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="64b95-123">**Yama**</span><span class="sxs-lookup"><span data-stu-id="64b95-123">**PATCH**</span></span> | <span data-ttu-id="64b95-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="64b95-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="64b95-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="64b95-125">URI parameter</span></span>

<span data-ttu-id="64b95-126">Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="64b95-126">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="64b95-127">Ad</span><span class="sxs-lookup"><span data-stu-id="64b95-127">Name</span></span>                   | <span data-ttu-id="64b95-128">Tür</span><span class="sxs-lookup"><span data-stu-id="64b95-128">Type</span></span>     | <span data-ttu-id="64b95-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="64b95-129">Required</span></span> | <span data-ttu-id="64b95-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="64b95-130">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="64b95-131">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="64b95-131">**customer-tenant-id**</span></span> | <span data-ttu-id="64b95-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="64b95-132">**guid**</span></span> | <span data-ttu-id="64b95-133">Y</span><span class="sxs-lookup"><span data-stu-id="64b95-133">Y</span></span>        | <span data-ttu-id="64b95-134">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="64b95-134">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="64b95-135">**order-id**</span><span class="sxs-lookup"><span data-stu-id="64b95-135">**order-id**</span></span> | <span data-ttu-id="64b95-136">**string**</span><span class="sxs-lookup"><span data-stu-id="64b95-136">**string**</span></span> | <span data-ttu-id="64b95-137">Y</span><span class="sxs-lookup"><span data-stu-id="64b95-137">Y</span></span>        | <span data-ttu-id="64b95-138">değeri, iptal edilmesi gereken sipariş kimliklerini not alan bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="64b95-138">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="64b95-139">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="64b95-139">Request headers</span></span>

<span data-ttu-id="64b95-140">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="64b95-140">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="64b95-141">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="64b95-141">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="64b95-142">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="64b95-142">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/orders/<order-id> HTTP/1.1
Accept: application/json
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

## <a name="rest-response"></a><span data-ttu-id="64b95-143">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="64b95-143">REST response</span></span>

<span data-ttu-id="64b95-144">Başarılı olursa, bu yöntem iptal edilen siparişi döndürür.</span><span class="sxs-lookup"><span data-stu-id="64b95-144">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="64b95-145">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="64b95-145">Response success and error codes</span></span>

<span data-ttu-id="64b95-146">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="64b95-146">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="64b95-147">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="64b95-147">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="64b95-148">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="64b95-148">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="64b95-149">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="64b95-149">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 866
MS-CorrelationId: 1438ea3d-b515-45c7-9ec1-27ee0cc8e6bd
MS-RequestId: 655890ba-4d2b-4d09-a95f-4ea1348686a5

{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "alternateId": "11fc4bdfd47a",
    "referenceCustomerId": "bd59b416-37f9-4d8f-8df3-5750111fc615",
    "billingCycle": "one_time",
    "currencyCode": "USD",
    "currencySymbol": "$",
    "lineItems": [
        {
            "lineItemNumber": 0,
            "offerId": "DG7GMGF0DWT0:0001:DG7GMGF0DSQR",
            "termDuration": "",
            "transactionType": "New",
            "friendlyName": "Microsoft Identity Manager 2016 - 1 User CAL",
            "quantity": 1,
            "links": {
                "product": {
                    "uri": "/products/DG7GMGF0DWT0?country=US",
                    "method": "GET",
                    "headers": []
                },
                "sku": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001?country=US",
                    "method": "GET",
                    "headers": []
                },
                "availability": {
                    "uri": "/products/DG7GMGF0DWT0/skus/0001/availabilities/DG7GMGF0DSQR?country=US",
                    "method": "GET",
                    "headers": []
                }
            }
        }
    ],
    "creationDate": "2019-02-21T17:56:21.1335741Z",
    "status": "cancelled",
    "transactionType": "UserPurchase",
    "attributes": {
        "objectType": "Order"
    }
}
```
