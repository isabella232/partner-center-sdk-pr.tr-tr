---
title: Müşteri için tüm hizmet taleplerini alma
description: Müşterinin tüm hizmet isteklerini alır.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: amitravat
ms.author: amrava
ms.openlocfilehash: 6f473c7a7d43b1a3929d983fb23dae92fdafbc0f
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769898"
---
# <a name="get-all-service-requests-for-a-customer"></a><span data-ttu-id="1b56a-103">Müşteri için tüm hizmet taleplerini alma</span><span class="sxs-lookup"><span data-stu-id="1b56a-103">Get all service requests for a customer</span></span>

<span data-ttu-id="1b56a-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="1b56a-104">**Applies To**</span></span>

- <span data-ttu-id="1b56a-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1b56a-105">Partner Center</span></span>
- <span data-ttu-id="1b56a-106">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1b56a-106">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="1b56a-107">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="1b56a-107">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="1b56a-108">Müşterinin tüm hizmet isteklerini alır.</span><span class="sxs-lookup"><span data-stu-id="1b56a-108">Gets all of a customer's service requests.</span></span>

<span data-ttu-id="1b56a-109">Iş Ortağı Merkezi panosunda, bu işlem önce [bir müşteri seçilerek](get-a-customer-by-name.md)gerçekleştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="1b56a-109">In the Partner Center dashboard, this operation can be performed by first [selecting a customer](get-a-customer-by-name.md).</span></span> <span data-ttu-id="1b56a-110">Sonra sol kenar çubuğundan **hizmet yönetimi** ' ni seçin.</span><span class="sxs-lookup"><span data-stu-id="1b56a-110">Then, select **Service management** on the left sidebar.</span></span> <span data-ttu-id="1b56a-111">Müşterinin hizmet istekleri, **destek biletleri** altında görüntülenir.</span><span class="sxs-lookup"><span data-stu-id="1b56a-111">The customer's service requests are displayed under **Support tickets**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1b56a-112">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="1b56a-112">Prerequisites</span></span>

- <span data-ttu-id="1b56a-113">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="1b56a-113">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="1b56a-114">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="1b56a-114">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="1b56a-115">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="1b56a-115">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="1b56a-116">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="1b56a-116">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="1b56a-117">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="1b56a-117">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="1b56a-118">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="1b56a-118">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="1b56a-119">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="1b56a-119">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="1b56a-120">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="1b56a-120">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="1b56a-121">C\#</span><span class="sxs-lookup"><span data-stu-id="1b56a-121">C\#</span></span>

<span data-ttu-id="1b56a-122">Müşterinin hizmet isteklerinin tümünün listesini göstermek için, **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve [**byıd ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="1b56a-122">To display a list of all of a customer's service requests, use your **IAggregatePartner.Customers** collection and call the [**ById()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method.</span></span> <span data-ttu-id="1b56a-123">Ardından [**Servicerequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) özelliğini çağırın, ardından [**Get ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) veya [**GetAsync ()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) yöntemleri gelir.</span><span class="sxs-lookup"><span data-stu-id="1b56a-123">Then call the [**ServiceRequests**](/dotnet/api/microsoft.store.partnercenter.customers.icustomer.servicerequests) property, followed by the [**Get()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.get) or [**GetAsync()**](/dotnet/api/microsoft.store.partnercenter.servicerequests.iservicerequestcollection.getasync) methods.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string customerId as string;

ResourceCollection<ServiceRequest> serviceRequests = partnerOperations.Customers.ById(customerId).ServiceRequests.Get();
```

<span data-ttu-id="1b56a-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="1b56a-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="1b56a-125">**Proje**: partnercentersdk. FeaturesSamples **sınıfı**: CustomerManagedServices.cs</span><span class="sxs-lookup"><span data-stu-id="1b56a-125">**Project**: PartnerCenterSDK.FeaturesSamples **Class**: CustomerManagedServices.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="1b56a-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="1b56a-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="1b56a-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="1b56a-127">Request syntax</span></span>

| <span data-ttu-id="1b56a-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="1b56a-128">Method</span></span>  | <span data-ttu-id="1b56a-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="1b56a-129">Request URI</span></span>                                                                                            |
|---------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="1b56a-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="1b56a-130">**GET**</span></span> | <span data-ttu-id="1b56a-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/servicerequests http/1.1</span><span class="sxs-lookup"><span data-stu-id="1b56a-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/servicerequests HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="1b56a-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="1b56a-132">URI parameter</span></span>

<span data-ttu-id="1b56a-133">Müşterinin tüm hizmet isteklerini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b56a-133">Use the following query parameter to get all service requests for the customer.</span></span>

| <span data-ttu-id="1b56a-134">Ad</span><span class="sxs-lookup"><span data-stu-id="1b56a-134">Name</span></span>                   | <span data-ttu-id="1b56a-135">Tür</span><span class="sxs-lookup"><span data-stu-id="1b56a-135">Type</span></span>     | <span data-ttu-id="1b56a-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="1b56a-136">Required</span></span> | <span data-ttu-id="1b56a-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="1b56a-137">Description</span></span>                            |
|------------------------|----------|----------|----------------------------------------|
| <span data-ttu-id="1b56a-138">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="1b56a-138">**customer-tenant-id**</span></span> | <span data-ttu-id="1b56a-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="1b56a-139">**guid**</span></span> | <span data-ttu-id="1b56a-140">Y</span><span class="sxs-lookup"><span data-stu-id="1b56a-140">Y</span></span>        | <span data-ttu-id="1b56a-141">Müşteriye karşılık gelen bir GUID..</span><span class="sxs-lookup"><span data-stu-id="1b56a-141">A GUID corresponding to the customer..</span></span> |

### <a name="request-headers"></a><span data-ttu-id="1b56a-142">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="1b56a-142">Request headers</span></span>

<span data-ttu-id="1b56a-143">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="1b56a-143">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="1b56a-144">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="1b56a-144">Request body</span></span>

<span data-ttu-id="1b56a-145">Yok.</span><span class="sxs-lookup"><span data-stu-id="1b56a-145">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="1b56a-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="1b56a-146">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/servicerequests HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
```

## <a name="rest-response"></a><span data-ttu-id="1b56a-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="1b56a-147">REST response</span></span>

<span data-ttu-id="1b56a-148">Başarılı olursa, bu yöntem yanıt gövdesinde bir **hizmet isteği** kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="1b56a-148">If successful, this method returns a collection of **Service Request** resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="1b56a-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="1b56a-149">Response success and error codes</span></span>

<span data-ttu-id="1b56a-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="1b56a-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="1b56a-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="1b56a-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="1b56a-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="1b56a-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="1b56a-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="1b56a-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 742
Content-Type: application/json
MS-CorrelationId: 998e31a1-3f17-4471-a9ee-7678dd72e033
MS-RequestId: 53d5d48c-9693-46b6-8071-2eed07797d6c
Date: Tue, 24 Nov 2015 07:19:21 GMT

{
    "totalCount": 1,
    "items": [{
        "title": "Test",
        "severity": 0,
        "id": "615112491169010",
        "status": 1,
        "primaryContact": {
            "lastName": "LastName",
            "firstName": "FirstName"
        },
        "createdDate": "2015-11-24T01:07:00.863",
        "lastModifiedDate": "2015-11-24T01:17:10.61",
        "lastClosedDate": "0001-01-01T00:00:00",
        "attributes": {
            "objectType": "ServiceRequest"
        }
    }],
    "attributes": {
        "objectType": "Collection"
    }
}
```
