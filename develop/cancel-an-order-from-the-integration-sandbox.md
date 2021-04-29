---
title: Tümleştirme korumalı alanı 'ndan bir siparişi iptal etme
description: Iş Ortağı Merkezi API 'Lerini, tümleştirme korumalı alanı hesaplarından farklı türdeki abonelik siparişlerinin iptal etmek için nasıl kullanacağınızı öğrenin.
ms.date: 04/28/2021
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: c3bf862c62804a56e6f73dd3ec36d2e9eb65f997
ms.sourcegitcommit: f59a9311c8a37d45695caf74794ec1697426acc9
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 04/29/2021
ms.locfileid: "108210028"
---
# <a name="cancel-an-order-from-the-integration-sandbox-using-partner-center-apis"></a><span data-ttu-id="21e45-103">Iş Ortağı Merkezi API 'Lerini kullanarak tümleştirme korumalı alanından bir siparişi iptal etme</span><span class="sxs-lookup"><span data-stu-id="21e45-103">Cancel an order from the integration sandbox using Partner Center APIs</span></span>

<span data-ttu-id="21e45-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="21e45-104">**Applies to:**</span></span>

- <span data-ttu-id="21e45-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="21e45-105">Partner Center</span></span>
- <span data-ttu-id="21e45-106">21Vianet tarafından çalıştırılan İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="21e45-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="21e45-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="21e45-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="21e45-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="21e45-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="21e45-109">Bu makalede, Iş Ortağı Merkezi API 'Lerinin, tümleştirme korumalı alanı hesaplarından farklı abonelik siparişlerinin türlerini iptal etmek için nasıl kullanılacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="21e45-109">This article describes how to use Partner Center APIs to cancel different types of subscription orders from integration sandbox accounts.</span></span> <span data-ttu-id="21e45-110">Bu şekilde, ayrılmış örnekler, yazılımlar ve hizmet olarak satılan Market (SaaS) abonelik siparişleri bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="21e45-110">Such orders can include reserved instances, software, and commercial marketplace Software as a Service (SaaS) subscription orders.</span></span>

>[!NOTE] 
><span data-ttu-id="21e45-111">Lütfen ayrılmış örneğin iptalinin veya ticari Market SaaS Abonelik siparişlerinin yalnızca tümleştirme korumalı alanı hesaplarından yapılacağına dikkat edin.</span><span class="sxs-lookup"><span data-stu-id="21e45-111">Please be aware that the cancellations of reserved instance, or commercial marketplace SaaS subscription orders are only possible from integration sandbox accounts.</span></span> <span data-ttu-id="21e45-112">60 günden eski olan tüm korumalı alan siparişleri Iş Ortağı Merkezi 'nden iptal edilemez.</span><span class="sxs-lookup"><span data-stu-id="21e45-112">Any sandbox orders which are older than 60 days cannot be cancelled from Partner Center.</span></span> <span data-ttu-id="21e45-113">Yardıma ihtiyacınız varsa, Iş Ortağı Merkezi desteğine ulaşın.</span><span class="sxs-lookup"><span data-stu-id="21e45-113">If you need assistance, reach out to Partner Center Support.</span></span> 

<span data-ttu-id="21e45-114">API aracılığıyla yazılım üretim emirlerini iptal etmek için [iptal-yazılım-satın](cancel-software-purchases.md)alma kullanın.</span><span class="sxs-lookup"><span data-stu-id="21e45-114">To cancel production orders of software through API, use [cancel-software-purchases](cancel-software-purchases.md).</span></span>
<span data-ttu-id="21e45-115">Ayrıca, [satın alma işlemini iptal etmek](/partner-center/csp-software-subscriptions)için pano aracılığıyla yazılımın üretim emirlerini iptal edebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="21e45-115">You can also cancel production orders of software through dashboard using [cancel a purchase](/partner-center/csp-software-subscriptions).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="21e45-116">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="21e45-116">Prerequisites</span></span>

- <span data-ttu-id="21e45-117">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="21e45-117">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="21e45-118">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="21e45-118">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="21e45-119">Bir müşteriyle, etkin ayrılmış örnek/yazılım/üçüncü taraf SaaS Abonelik emirlerine sahip bir tümleştirme korumalı alan iş ortağı hesabı.</span><span class="sxs-lookup"><span data-stu-id="21e45-119">An integration sandbox partner account with a customer having active reserved instance / software / third-party SaaS subscription orders.</span></span>

## <a name="c"></a><span data-ttu-id="21e45-120">C\#</span><span class="sxs-lookup"><span data-stu-id="21e45-120">C\#</span></span>

<span data-ttu-id="21e45-121">Tümleştirme korumalı alanından bir siparişi iptal etmek için, [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) iş ortağı işlemlerini almak üzere bir arabirim almak üzere hesap kimlik bilgilerinizi metoduna geçirin.</span><span class="sxs-lookup"><span data-stu-id="21e45-121">To cancel an order from the integration sandbox, pass your account credentials to the [**`CreatePartnerOperations`**](/dotnet/api/microsoft.store.partnercenter.partnerservice.instance) method to get an [**`IPartner`**](/dotnet/api/microsoft.store.partnercenter.ipartner) interface to get partner operations.</span></span>

<span data-ttu-id="21e45-122">Belirli bir [siparişi](order-resources.md#order)seçmek için müşteri tanımlayıcısı ile iş ortağı işlemlerini ve çağrı [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın, ardından siparişi **`Orders.ById()`** ve son olarak **`Get`** ya da alma yöntemini belirtmek için Order Identifier ' ı seçin **`GetAsync`** .</span><span class="sxs-lookup"><span data-stu-id="21e45-122">To select a particular [Order](order-resources.md#order), use the partner operations and call [**`Customers.ById()`**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer identifier to specify the customer, followed by **`Orders.ById()`** with order identifier to specify the order and finally **`Get`** or **`GetAsync`** method to retrieve it.</span></span>

<span data-ttu-id="21e45-123">[**`Order.Status`**](order-resources.md#order)Özelliğini olarak ayarlayın `cancelled` ve **`Patch()`** sıralamayı güncelleştirmek için yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="21e45-123">Set the [**`Order.Status`**](order-resources.md#order) property to `cancelled` and use the **`Patch()`** method to update the order.</span></span>

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

## <a name="rest-request"></a><span data-ttu-id="21e45-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="21e45-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="21e45-125">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="21e45-125">Request syntax</span></span>

| <span data-ttu-id="21e45-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="21e45-126">Method</span></span>     | <span data-ttu-id="21e45-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="21e45-127">Request URI</span></span>                                                                            |
|------------|----------------------------------------------------------------------------------------|
| <span data-ttu-id="21e45-128">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="21e45-128">**PATCH**</span></span> | <span data-ttu-id="21e45-129">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-id}/Orders/{Order-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="21e45-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/orders/{order-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="21e45-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="21e45-130">URI parameter</span></span>

<span data-ttu-id="21e45-131">Bir müşteriyi silmek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="21e45-131">Use the following query parameter to delete a customer.</span></span>

| <span data-ttu-id="21e45-132">Ad</span><span class="sxs-lookup"><span data-stu-id="21e45-132">Name</span></span>                   | <span data-ttu-id="21e45-133">Tür</span><span class="sxs-lookup"><span data-stu-id="21e45-133">Type</span></span>     | <span data-ttu-id="21e45-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="21e45-134">Required</span></span> | <span data-ttu-id="21e45-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="21e45-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="21e45-136">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="21e45-136">**customer-tenant-id**</span></span> | <span data-ttu-id="21e45-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="21e45-137">**guid**</span></span> | <span data-ttu-id="21e45-138">Y</span><span class="sxs-lookup"><span data-stu-id="21e45-138">Y</span></span>        | <span data-ttu-id="21e45-139">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="21e45-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="21e45-140">**sıra kimliği**</span><span class="sxs-lookup"><span data-stu-id="21e45-140">**order-id**</span></span> | <span data-ttu-id="21e45-141">**string**</span><span class="sxs-lookup"><span data-stu-id="21e45-141">**string**</span></span> | <span data-ttu-id="21e45-142">Y</span><span class="sxs-lookup"><span data-stu-id="21e45-142">Y</span></span>        | <span data-ttu-id="21e45-143">Değer, iptal edilmesi gereken sıra kimliklerini belirten bir dizedir.</span><span class="sxs-lookup"><span data-stu-id="21e45-143">The value is a string denoting the order IDs that need to be canceled.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="21e45-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="21e45-144">Request headers</span></span>

<span data-ttu-id="21e45-145">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="21e45-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="21e45-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="21e45-146">Request body</span></span>

```http
{
    "id": "UKXASSO1dezh3HdxClHxSp5UEFXGbAnt1",
    "status": "cancelled",
}
```

### <a name="request-example"></a><span data-ttu-id="21e45-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="21e45-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="21e45-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="21e45-148">REST response</span></span>

<span data-ttu-id="21e45-149">Başarılı olursa, bu yöntem iptal edildi sırasını döndürür.</span><span class="sxs-lookup"><span data-stu-id="21e45-149">If successful, this method returns the canceled order.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="21e45-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="21e45-150">Response success and error codes</span></span>

<span data-ttu-id="21e45-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="21e45-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="21e45-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="21e45-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="21e45-153">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="21e45-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="21e45-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="21e45-154">Response example</span></span>

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
