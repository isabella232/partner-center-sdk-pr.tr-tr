---
title: Kimliğe göre bir müşterinin yönetilen hizmetlerini alma
description: Müşterinin yönetilen hizmetlerini alır. Diğer bir deyişle, yönetici ayrıcalıklarına sahip olduğunuz tüm müşteri aboneliklerinin bağlantılarını alın. Bu bağlantıları, Microsoft ile destek ve dosya hizmeti istekleri sağlamak için kullanabilirsiniz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 4764fce6a80035ea4b9dcc6677a3da28fc863eb7
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769802"
---
# <a name="get-the-managed-services-for-a-customer-by-id"></a><span data-ttu-id="1e874-105">Kimliğe göre bir müşterinin yönetilen hizmetlerini alma</span><span class="sxs-lookup"><span data-stu-id="1e874-105">Get the managed services for a customer by ID</span></span>

<span data-ttu-id="1e874-106">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="1e874-106">**Applies To**</span></span>

- <span data-ttu-id="1e874-107">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1e874-107">Partner Center</span></span>
- <span data-ttu-id="1e874-108">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1e874-108">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="1e874-109">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1e874-109">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1e874-110">Müşterinin yönetilen hizmetlerini alır.</span><span class="sxs-lookup"><span data-stu-id="1e874-110">Gets the managed services for a customer.</span></span> <span data-ttu-id="1e874-111">Diğer bir deyişle, yönetici ayrıcalıklarına sahip olduğunuz tüm müşteri aboneliklerinin bağlantılarını alın.</span><span class="sxs-lookup"><span data-stu-id="1e874-111">In other words, get links to all of the customer's subscriptions for which you have delegated admin privileges.</span></span> <span data-ttu-id="1e874-112">Bu bağlantıları, Microsoft ile destek ve dosya hizmeti istekleri sağlamak için kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e874-112">You can use these links to provide support and file service requests with Microsoft.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1e874-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1e874-113">Prerequisites</span></span>

- <span data-ttu-id="1e874-114">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1e874-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1e874-115">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="1e874-115">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1e874-116">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1e874-116">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1e874-117">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1e874-117">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1e874-118">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1e874-118">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1e874-119">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1e874-119">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1e874-120">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="1e874-120">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1e874-121">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="1e874-121">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1e874-122">C\#</span><span class="sxs-lookup"><span data-stu-id="1e874-122">C\#</span></span>

<span data-ttu-id="1e874-123">Müşterinin tüm yönetilen hizmetlerinin listesini göstermek için **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1e874-123">To display a list of all the managed services for a customer, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="1e874-124">Ardından [**Managedservices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) özelliğini çağırın, ardından [**Get ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) yöntemleri gelir.</span><span class="sxs-lookup"><span data-stu-id="1e874-124">Then call the [**ManagedServices**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.managedservices) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.managedservices.imanagedservicecollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// var selectedCustomerID as Customer;

ResourceCollection<ManagedService> managedServices = partnerOperations.Customers.ById(selectedCustomerId).ManagedServices.Get();
```

<span data-ttu-id="1e874-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1e874-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1e874-126">**Proje**: partnercentersdk. FeaturesSamples **sınıfı**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="1e874-126">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1e874-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1e874-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1e874-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1e874-128">Request syntax</span></span>

| <span data-ttu-id="1e874-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1e874-129">Method</span></span>  | <span data-ttu-id="1e874-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1e874-130">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1e874-131">**Al**</span><span class="sxs-lookup"><span data-stu-id="1e874-131">**GET**</span></span> | <span data-ttu-id="1e874-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/managedservices http/1.1</span><span class="sxs-lookup"><span data-stu-id="1e874-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/managedservices HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1e874-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1e874-133">URI parameter</span></span>

<span data-ttu-id="1e874-134">Müşterinin yönetilen hizmetlerini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e874-134">Use the following query parameter to get the customer's managed services.</span></span>

| <span data-ttu-id="1e874-135">Ad</span><span class="sxs-lookup"><span data-stu-id="1e874-135">Name</span></span>                   | <span data-ttu-id="1e874-136">Tür</span><span class="sxs-lookup"><span data-stu-id="1e874-136">Type</span></span>     | <span data-ttu-id="1e874-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1e874-137">Required</span></span> | <span data-ttu-id="1e874-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1e874-138">Description</span></span>                           |
|------------------------|----------|----------|---------------------------------------|
| <span data-ttu-id="1e874-139">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="1e874-139">**customer-tenant-id**</span></span> | <span data-ttu-id="1e874-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="1e874-140">**guid**</span></span> | <span data-ttu-id="1e874-141">Y</span><span class="sxs-lookup"><span data-stu-id="1e874-141">Y</span></span>        | <span data-ttu-id="1e874-142">Müşteriye karşılık gelen bir GUID.</span><span class="sxs-lookup"><span data-stu-id="1e874-142">A GUID corresponding to the customer.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1e874-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1e874-143">Request headers</span></span>

<span data-ttu-id="1e874-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1e874-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1e874-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1e874-145">Request body</span></span>

<span data-ttu-id="1e874-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="1e874-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1e874-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1e874-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/managedservices HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 4ff57220-f17b-4d8f-8e09-78334c57ba00
MS-CorrelationId: 03d6064a-f048-4aee-8892-ed46dc5c8bee
```

## <a name="rest-response"></a><span data-ttu-id="1e874-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1e874-148">REST response</span></span>

<span data-ttu-id="1e874-149">Başarılı olursa, bu yöntem yanıt gövdesinde **yönetilen hizmet** nesnelerinin bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1e874-149">If successful, this method returns a collection of **Managed Service** objects in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1e874-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1e874-150">Response success and error codes</span></span>

<span data-ttu-id="1e874-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1e874-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1e874-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1e874-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1e874-153">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1e874-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1e874-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1e874-154">Response example</span></span>

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
