---
title: Tümleştirme korumalı alanı 'ndan bir siparişi iptal etme
description: Iş Ortağı Merkezi API 'Lerini, tümleştirme korumalı alanı hesaplarından farklı türdeki abonelik siparişlerinin iptal etmek için nasıl kullanacağınızı öğrenin.
ms.date: 08/16/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 363bf209e27d5223259c8c533710a3b35bbef1e6
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770084"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="af127-103">Iş Ortağı Merkezi API 'Lerini kullanarak tümleştirme korumalı alanından bir siparişi iptal etme</span><span class="sxs-lookup"><span data-stu-id="af127-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="af127-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="af127-104">**Applies to:**</span></span>

- <span data-ttu-id="af127-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="af127-105">Partner Center</span></span>
- <span data-ttu-id="af127-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="af127-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="af127-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="af127-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="af127-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="af127-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="af127-109">Bu makalede, Iş Ortağı Merkezi API 'Lerinin, tümleştirme korumalı alanı hesaplarından farklı abonelik siparişlerinin türlerini iptal etmek için nasıl kullanılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="af127-109">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="af127-110">Bu şekilde, ayrılmış örnekler, yazılımlar ve hizmet olarak satılan Market (SaaS) abonelik siparişleri bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="af127-110">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

>[!NOTE]
><span data-ttu-id="af127-111">Lütfen ayrılmış örneğin iptalinin veya ticari Market SaaS Abonelik siparişlerinin yalnızca tümleştirme korumalı alanı hesaplarından yapılacağına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="af127-111">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span>  

<span data-ttu-id="af127-112">API aracılığıyla yazılım üretim emirlerini iptal etmek için [iptal-yazılım-satın](cancel-software-purchases.md)alma kullanın.</span><span class="sxs-lookup"><span data-stu-id="af127-112">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="af127-113">Ayrıca, [satın alma işlemini iptal etmek](/partner-center/csp-software-subscriptions)için pano aracılığıyla yazılımın üretim emirlerini iptal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="af127-113">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="af127-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="af127-114">Prerequisites</span></span>

- <span data-ttu-id="af127-115">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="af127-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="af127-116">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="af127-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="af127-117">Bir müşteriyle, etkin ayrılmış örnek/yazılım/üçüncü taraf SaaS Abonelik emirlerine sahip bir tümleştirme korumalı alan iş ortağı hesabı.</span><span class="sxs-lookup"><span data-stu-id="af127-117">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="af127-118">C\#</span><span class="sxs-lookup"><span data-stu-id="af127-118">C\#</span></span>

<span data-ttu-id="af127-119">Tümleştirme korumalı alanından bir siparişi iptal etmek için, [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) iş ortağı işlemlerini almak üzere bir arabirim almak üzere hesap kimlik bilgilerinizi metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="af127-119">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="af127-120">Belirli bir [siparişi](order-resources.md#order)seçmek için müşteri tanımlayıcısı ile iş ortağı işlemlerini ve çağrı [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın, ardından siparişi **`Orders.ById()`** ve son olarak **`Get`** ya da alma yöntemini belirtmek için Order Identifier ' ı seçin **`GetAsync`** .</span><span class="sxs-lookup"><span data-stu-id="af127-120">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="af127-121">[**`Order.Status`**](order-resources.md#order)Özelliğini olarak ayarlayın `cancelled` ve **`Patch()`** sıralamayı güncelleştirmek için yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="af127-121">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="af127-122">REST isteği</span><span class="sxs-lookup"><span data-stu-id="af127-122">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="af127-123">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="af127-123">Request syntax</span></span>

| <span data-ttu-id="af127-124">Yöntem</span><span class="sxs-lookup"><span data-stu-id="af127-124">Method</span></span>     | <span data-ttu-id="af127-125">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="af127-125">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="af127-126">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="af127-126">**PATCH**</span></span> | <span data-ttu-id="af127-127">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="af127-127">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="af127-128">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="af127-128">URI parameter</span></span>

<span data-ttu-id="af127-129">Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="af127-129">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="af127-130">Ad</span><span class="sxs-lookup"><span data-stu-id="af127-130">Name</span></span>                   | <span data-ttu-id="af127-131">Tür</span><span class="sxs-lookup"><span data-stu-id="af127-131">Type</span></span>     | <span data-ttu-id="af127-132">Gerekli</span><span class="sxs-lookup"><span data-stu-id="af127-132">Required</span></span> | <span data-ttu-id="af127-133">Açıklama</span><span class="sxs-lookup"><span data-stu-id="af127-133">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="af127-134">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="af127-134">**customer-tenant-id**</span></span> | <span data-ttu-id="af127-135">**guid**</span><span class="sxs-lookup"><span data-stu-id="af127-135">**guid**</span></span> | <span data-ttu-id="af127-136">Y</span><span class="sxs-lookup"><span data-stu-id="af127-136">Y</span></span>        | <span data-ttu-id="af127-137">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="af127-137">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="af127-138">**sıra kimliği**</span><span class="sxs-lookup"><span data-stu-id="af127-138">**order-id**</span></span> | <span data-ttu-id="af127-139">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="af127-139">**string**</span></span> | <span data-ttu-id="af127-140">Y</span><span class="sxs-lookup"><span data-stu-id="af127-140">Y</span></span>        | <span data-ttu-id="af127-141">Değer, iptal edilmesi gereken sıra kimliklerini belirten bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="af127-141">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="af127-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="af127-142">Request headers</span></span>

<span data-ttu-id="af127-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="af127-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="af127-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="af127-144">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="af127-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="af127-145">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="af127-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="af127-146">REST response</span></span>

<span data-ttu-id="af127-147">Başarılı olursa, bu yöntem iptal edildi sırasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="af127-147">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="af127-148">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="af127-148">Response success and error codes</span></span>

<span data-ttu-id="af127-149">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="af127-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="af127-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="af127-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="af127-151">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="af127-151">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="af127-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="af127-152">Response example</span></span>

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
