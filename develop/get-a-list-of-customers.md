---
title: Müşterilerin bir listesini alma
description: Bir iş ortağının müşterilerinin tümünü temsil eden bir kaynak koleksiyonu alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 840c9d1a61451763d37a19639f99b12f1deb7521
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874355"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="d6c77-103">Müşterilerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="d6c77-103">Get a list of customers</span></span>

<span data-ttu-id="d6c77-104">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d6c77-104">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="d6c77-105">Bu makalede, bir iş ortağının müşterilerinin tümünü temsil eden bir kaynak koleksiyonunun nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="d6c77-105">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="d6c77-106">Bu işlemi Iş Ortağı Merkezi panosunda da gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d6c77-106">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="d6c77-107">Ana sayfada, **müşteri yönetimi** altında, **müşterileri görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="d6c77-107">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="d6c77-108">Ya da kenar çubuğunda **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="d6c77-108">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d6c77-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d6c77-109">Prerequisites</span></span>

- <span data-ttu-id="d6c77-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d6c77-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d6c77-111">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="d6c77-111">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="d6c77-112">C\#</span><span class="sxs-lookup"><span data-stu-id="d6c77-112">C\#</span></span>

<span data-ttu-id="d6c77-113">Tüm müşterilerin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="d6c77-113">To get a list of all customers:</span></span>

1. <span data-ttu-id="d6c77-114">[**Iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunu kullanarak bir **ıpartner** nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d6c77-114">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="d6c77-115">[**Sorgu ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) veya [**queryasync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) yöntemlerini kullanarak müşteri listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d6c77-115">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="d6c77-116">(Sorgu oluşturma yönergeleri için bkz. [**Queryfactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfı.)</span><span class="sxs-lookup"><span data-stu-id="d6c77-116">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="d6c77-117">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="d6c77-117">For an example, see the following:</span></span>

- <span data-ttu-id="d6c77-118">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="d6c77-118">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="d6c77-119">Project: **partnersdk. featuresamples**</span><span class="sxs-lookup"><span data-stu-id="d6c77-119">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="d6c77-120">Sınıf: **Customerpaging. cs**</span><span class="sxs-lookup"><span data-stu-id="d6c77-120">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="d6c77-121">Java</span><span class="sxs-lookup"><span data-stu-id="d6c77-121">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="d6c77-122">Tüm müşterilerin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="d6c77-122">To get a list of all customers:</span></span>

1. <span data-ttu-id="d6c77-123">Müşteri işlemlerine bir başvuru almak için [**ıaggregatepartner. getCustomers**] işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6c77-123">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="d6c77-124">**Sorgu ()** işlevini kullanarak müşteri listesini alın.</span><span class="sxs-lookup"><span data-stu-id="d6c77-124">Retrieve the customer list using the **query()** function.</span></span>

```java
// Query the customers, get the first page if a page size was set, otherwise get all customers
SeekBasedResourceCollection<Customer> customersPage = partnerOperations.getCustomers().query(QueryFactory.getInstance().buildIndexedQuery(40));

// Create a customer enumerator which will aid us in traversing the customer pages
IResourceCollectionEnumerator<SeekBasedResourceCollection<Customer>> customersEnumerator =
    partnerOperations.getEnumerators().getCustomers().create( customersPage );

int pageNumber = 1;

while (customersEnumerator.hasValue())
{
    /*
     * Use the customersEnumerator.getCurrent() function to
     * access the current page of customers.
     */

    // Get the next page of customers
    customersEnumerator.next();
}
```

## <a name="powershell"></a><span data-ttu-id="d6c77-125">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d6c77-125">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="d6c77-126">Müşterilerin tam listesini almak için [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) komutunu parametresiz olarak yürütün.</span><span class="sxs-lookup"><span data-stu-id="d6c77-126">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="d6c77-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d6c77-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d6c77-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d6c77-128">Request syntax</span></span>

| <span data-ttu-id="d6c77-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d6c77-129">Method</span></span>  | <span data-ttu-id="d6c77-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d6c77-130">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="d6c77-131">**Al**</span><span class="sxs-lookup"><span data-stu-id="d6c77-131">**GET**</span></span> | <span data-ttu-id="d6c77-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers? boyut = {SIZE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="d6c77-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="d6c77-133">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d6c77-133">URI parameter</span></span>

<span data-ttu-id="d6c77-134">Müşterilerin bir listesini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6c77-134">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="d6c77-135">Ad</span><span class="sxs-lookup"><span data-stu-id="d6c77-135">Name</span></span>     | <span data-ttu-id="d6c77-136">Tür</span><span class="sxs-lookup"><span data-stu-id="d6c77-136">Type</span></span>    | <span data-ttu-id="d6c77-137">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d6c77-137">Required</span></span> | <span data-ttu-id="d6c77-138">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d6c77-138">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="d6c77-139">**boyutla**</span><span class="sxs-lookup"><span data-stu-id="d6c77-139">**size**</span></span> | <span data-ttu-id="d6c77-140">**int**</span><span class="sxs-lookup"><span data-stu-id="d6c77-140">**int**</span></span> | <span data-ttu-id="d6c77-141">Y</span><span class="sxs-lookup"><span data-stu-id="d6c77-141">Y</span></span>        | <span data-ttu-id="d6c77-142">Tek seferde görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="d6c77-142">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="d6c77-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d6c77-143">Request headers</span></span>

<span data-ttu-id="d6c77-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d6c77-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d6c77-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d6c77-145">Request body</span></span>

<span data-ttu-id="d6c77-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="d6c77-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="d6c77-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d6c77-147">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="d6c77-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d6c77-148">REST response</span></span>

<span data-ttu-id="d6c77-149">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Müşteri](customer-resources.md#customer) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="d6c77-149">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d6c77-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d6c77-150">Response success and error codes</span></span>

<span data-ttu-id="d6c77-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="d6c77-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d6c77-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d6c77-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d6c77-153">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d6c77-153">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d6c77-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d6c77-154">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 15650
Content-Type: application/json
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
Date: Fri, 20 Nov 2015 01:08:23 GMT

{
    "totalCount": 2,
    "items": [{
        "id": "b44bb1fb-c595-45b0-9e09-d657365580bf",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    },
    {
        "id": "45c44870-ef77-4fdd-b6fe-3dacb075cff2",
        "companyProfile": {
            "tenantId": "<guid>",
            "domain": "domain",
            "companyName": "companyName",
            "attributes": {
                "objectType": "CustomerCompanyProfile"
            }
        },
        "relationshipToPartner": "reseller",
        "attributes": {
            "objectType": "Customer"
        }
    }],
    "links": {
        "self": {
            "uri": "/v1/customers?size=40",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
