---
title: Kimliğe göre bir müşterinin yönetilen hizmetlerini alma
description: Müşteri için yönetilen hizmetleri alır. Başka bir deyişle, yönetici ayrıcalıkları için temsilci olarak seçen müşterinin tüm aboneliklerinin bağlantılarını edinin. Microsoft ile destek ve dosya hizmeti istekleri sağlamak için bu bağlantıları kullanabilirsiniz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 1cf7e7b62113bd96b00fdc2301e4e7ac4f5d4243
ms.sourcegitcommit: b307fd75e305e0a88cfd1182cc01d2c9a108ce45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/06/2021
ms.locfileid: "111548456"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="feb43-105">Kimliğe göre bir müşterinin yönetilen hizmetlerini alma</span><span class="sxs-lookup"><span data-stu-id="feb43-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="feb43-106">**Için geçerlidir:** İş Ortağı Merkezi | İş Ortağı Merkezi Microsoft Bulut Almanya için | İş Ortağı Merkezi için Microsoft Cloud for US Government</span><span class="sxs-lookup"><span data-stu-id="feb43-106">**Applies to**: Partner Center | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="feb43-107">Müşteri için yönetilen hizmetleri alır.</span><span class="sxs-lookup"><span data-stu-id="feb43-107">Gets the managed services for a customer.</span></span> <span data-ttu-id="feb43-108">Başka bir deyişle, yönetici ayrıcalıkları için temsilci olarak seçen müşterinin tüm aboneliklerinin bağlantılarını edinin.</span><span class="sxs-lookup"><span data-stu-id="feb43-108">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="feb43-109">Microsoft ile destek ve dosya hizmeti istekleri sağlamak için bu bağlantıları kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="feb43-109">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="feb43-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="feb43-110">Prerequisites</span></span>

- <span data-ttu-id="feb43-111">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="feb43-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="feb43-112">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="feb43-112">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="feb43-113">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="feb43-113">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="feb43-114">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="feb43-114">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="feb43-115">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="feb43-115">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="feb43-116">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="feb43-116">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="feb43-117">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="feb43-117">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="feb43-118">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="feb43-118">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="feb43-119">C\#</span><span class="sxs-lookup"><span data-stu-id="feb43-119">C\#</span></span>

<span data-ttu-id="feb43-120">Bir müşteri için tüm yönetilen hizmetlerin listesini görüntülemek için **IAggregatePartner.Customers** koleksiyonu kullanın ve [**ById() yöntemini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) arayın.</span><span class="sxs-lookup"><span data-stu-id="feb43-120">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="feb43-121">Ardından [**ManagedServices özelliğini**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) ve ardından [**Get() veya**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) yöntemlerini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="feb43-121">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="feb43-122">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="feb43-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="feb43-123">**Project:** PartnerCenterSDK.FeaturesSamples **Sınıfı:** CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="feb43-123">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="feb43-124">REST isteği</span><span class="sxs-lookup"><span data-stu-id="feb43-124">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="feb43-125">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="feb43-125">Request syntax</span></span>

| <span data-ttu-id="feb43-126">Yöntem</span><span class="sxs-lookup"><span data-stu-id="feb43-126">Method</span></span>  | <span data-ttu-id="feb43-127">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="feb43-127">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="feb43-128">**Al**</span><span class="sxs-lookup"><span data-stu-id="feb43-128">**GET**</span></span> | <span data-ttu-id="feb43-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="feb43-129">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="feb43-130">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="feb43-130">URI parameter</span></span>

<span data-ttu-id="feb43-131">Müşterinin yönetilen hizmetlerini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="feb43-131">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="feb43-132">Ad</span><span class="sxs-lookup"><span data-stu-id="feb43-132">Name</span></span>                   | <span data-ttu-id="feb43-133">Tür</span><span class="sxs-lookup"><span data-stu-id="feb43-133">Type</span></span>     | <span data-ttu-id="feb43-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="feb43-134">Required</span></span> | <span data-ttu-id="feb43-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="feb43-135">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="feb43-136">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="feb43-136">**customer-tenant-id**</span></span> | <span data-ttu-id="feb43-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="feb43-137">**guid**</span></span> | <span data-ttu-id="feb43-138">Y</span><span class="sxs-lookup"><span data-stu-id="feb43-138">Y</span></span>        | <span data-ttu-id="feb43-139">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="feb43-139">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="feb43-140">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="feb43-140">Request headers</span></span>

<span data-ttu-id="feb43-141">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="feb43-141">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="feb43-142">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="feb43-142">Request body</span></span>

<span data-ttu-id="feb43-143">Yok.</span><span class="sxs-lookup"><span data-stu-id="feb43-143">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="feb43-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="feb43-144">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="feb43-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="feb43-145">REST response</span></span>

<span data-ttu-id="feb43-146">Başarılı olursa, bu yöntem yanıt **gövdesinde Yönetilen Hizmet** nesnelerinin bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="feb43-146">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="feb43-147">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="feb43-147">Response success and error codes</span></span>

<span data-ttu-id="feb43-148">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="feb43-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="feb43-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="feb43-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="feb43-150">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="feb43-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="feb43-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="feb43-151">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 10588
Content-Type: application/json
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
Date: Mon, 23 Nov 2015 18:02:12 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "Exchange",
        "name": "Exchange",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Exchange&InitialDomain=<domain>&PrimaryDomain=<domain>",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    },
    {
        "id": "MicrosoftCommunicationsOnline",
        "name": "SkypeforBusiness",
        "groupName": "Office",
        "links": {
            "adminService": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=MicrosoftCommunicationsOnline",
                "method": "GET",
                "headers": []
            },
            "serviceHealth": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=ServiceStatus",
                "method": "GET",
                "headers": []
            },
            "serviceTicket": {
                "uri": "https://portal.office.com/Partner/BeginClientSession.aspx?CTID=<ctid>&CSDEST=Support",
                "method": "GET",
                "headers": []
            }
        },
        "attributes": {
            "objectType": "ManagedService"
        }
    }
```
