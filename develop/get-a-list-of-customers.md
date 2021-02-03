---
title: Müşterilerin bir listesini alma
description: Bir iş ortağının müşterilerinin tümünü temsil eden bir kaynak koleksiyonu alma.
ms.date: 09/17/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 2dd8469458809ab38b6d6081adc91d6d1184d2d0
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769629"
---
# <a name="get-a-list-of-customers"></a><span data-ttu-id="a9f8b-103">Müşterilerin bir listesini alma</span><span class="sxs-lookup"><span data-stu-id="a9f8b-103">Get a list of customers</span></span>

<span data-ttu-id="a9f8b-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="a9f8b-104">**Applies to:**</span></span>

- <span data-ttu-id="a9f8b-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a9f8b-105">Partner Center</span></span>
- <span data-ttu-id="a9f8b-106">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a9f8b-106">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="a9f8b-107">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a9f8b-107">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="a9f8b-108">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="a9f8b-108">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="a9f8b-109">Bu makalede, bir iş ortağının müşterilerinin tümünü temsil eden bir kaynak koleksiyonunun nasıl alınacağı açıklanır.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-109">This article describes how to get a collection of resources that represents all of a partner's customers.</span></span>

> [!TIP]
> <span data-ttu-id="a9f8b-110">Bu işlemi Iş Ortağı Merkezi panosunda da gerçekleştirebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-110">You can also perform this operation in the Partner Center dashboard.</span></span> <span data-ttu-id="a9f8b-111">Ana sayfada, **müşteri yönetimi** altında, **müşterileri görüntüle**' yi seçin.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-111">On the main page, under **Customer management**, select **View Customers**.</span></span> <span data-ttu-id="a9f8b-112">Ya da kenar çubuğunda **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-112">Or, on the sidebar, select **Customers**.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a9f8b-113">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="a9f8b-113">Prerequisites</span></span>

- <span data-ttu-id="a9f8b-114">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-114">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="a9f8b-115">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-115">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

## <a name="c"></a><span data-ttu-id="a9f8b-116">C\#</span><span class="sxs-lookup"><span data-stu-id="a9f8b-116">C\#</span></span>

<span data-ttu-id="a9f8b-117">Tüm müşterilerin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="a9f8b-117">To get a list of all customers:</span></span>

1. <span data-ttu-id="a9f8b-118">[**Iaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) koleksiyonunu kullanarak bir **ıpartner** nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-118">Use the [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) collection to create an **IPartner** object.</span></span>

2. <span data-ttu-id="a9f8b-119">[**Sorgu ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) veya [**queryasync ()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) yöntemlerini kullanarak müşteri listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-119">Retrieve the customer list using the [**Query()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync()**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) methods.</span></span> <span data-ttu-id="a9f8b-120">(Sorgu oluşturma yönergeleri için bkz. [**Queryfactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfı.)</span><span class="sxs-lookup"><span data-stu-id="a9f8b-120">(For instructions on creating a query, see the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.)</span></span>

``` csharp
// IAggregatePartner partnerOperations;

// All the operations executed on this partner operation instance will share the same correlation Id but will differ in request Id
IPartner scopedPartnerOperations = partnerOperations.With(RequestContextFactory.Instance.Create(Guid.NewGuid()));

// read customers into chunks of 40s
var customersBatch = scopedPartnerOperations.Customers.Query(QueryFactory.Instance.BuildIndexedQuery(40));
var customersEnumerator = scopedPartnerOperations.Enumerators.Customers.Create(customersBatch);
```

<span data-ttu-id="a9f8b-121">Bir örnek için aşağıdakilere bakın:</span><span class="sxs-lookup"><span data-stu-id="a9f8b-121">For an example, see the following:</span></span>

- <span data-ttu-id="a9f8b-122">Örnek: [konsol test uygulaması](console-test-app.md)</span><span class="sxs-lookup"><span data-stu-id="a9f8b-122">Sample: [Console test app](console-test-app.md)</span></span>
- <span data-ttu-id="a9f8b-123">Proje: **Partnersdk. FeatureSamples**</span><span class="sxs-lookup"><span data-stu-id="a9f8b-123">Project: **PartnerSDK.FeatureSamples**</span></span>
- <span data-ttu-id="a9f8b-124">Sınıf: **CustomerPaging.cs**</span><span class="sxs-lookup"><span data-stu-id="a9f8b-124">Class: **CustomerPaging.cs**</span></span>

## <a name="java"></a><span data-ttu-id="a9f8b-125">Java</span><span class="sxs-lookup"><span data-stu-id="a9f8b-125">Java</span></span>

[!INCLUDE [Partner Center Java SDK support details](../includes/java-sdk-support.md)]

<span data-ttu-id="a9f8b-126">Tüm müşterilerin bir listesini almak için:</span><span class="sxs-lookup"><span data-stu-id="a9f8b-126">To get a list of all customers:</span></span>

1. <span data-ttu-id="a9f8b-127">Müşteri işlemlerine bir başvuru almak için [**ıaggregatepartner. getCustomers**] işlevini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-127">Use the [**IAggregatePartner.getCustomers**] function to get a reference to the customer operations.</span></span>

2. <span data-ttu-id="a9f8b-128">**Sorgu ()** işlevini kullanarak müşteri listesini alın.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-128">Retrieve the customer list using the **query()** function.</span></span>

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

## <a name="powershell"></a><span data-ttu-id="a9f8b-129">PowerShell</span><span class="sxs-lookup"><span data-stu-id="a9f8b-129">PowerShell</span></span>

[!INCLUDE [Partner Center PowerShell module support details](../includes/powershell-module-support.md)]

<span data-ttu-id="a9f8b-130">Müşterilerin tam listesini almak için [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) komutunu parametresiz olarak yürütün.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-130">Execute the [**Get-PartnerCustomer**](https://github.com/Microsoft/Partner-Center-PowerShell/blob/master/docs/help/Get-PartnerCustomer.md) command with no parameters to get a complete list of customers.</span></span>

```powershell
Get-PartnerCustomer
```

## <a name="rest-request"></a><span data-ttu-id="a9f8b-131">REST isteği</span><span class="sxs-lookup"><span data-stu-id="a9f8b-131">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="a9f8b-132">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="a9f8b-132">Request syntax</span></span>

| <span data-ttu-id="a9f8b-133">Yöntem</span><span class="sxs-lookup"><span data-stu-id="a9f8b-133">Method</span></span>  | <span data-ttu-id="a9f8b-134">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="a9f8b-134">Request URI</span></span>                                                                   |
|---------|-------------------------------------------------------------------------------|
| <span data-ttu-id="a9f8b-135">**Al**</span><span class="sxs-lookup"><span data-stu-id="a9f8b-135">**GET**</span></span> | <span data-ttu-id="a9f8b-136">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers? boyut = {SIZE} http/1.1</span><span class="sxs-lookup"><span data-stu-id="a9f8b-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size} HTTP/1.1</span></span> |

#### <a name="uri-parameter"></a><span data-ttu-id="a9f8b-137">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="a9f8b-137">URI parameter</span></span>

<span data-ttu-id="a9f8b-138">Müşterilerin bir listesini almak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-138">Use the following query parameter to get a list of customers.</span></span>

| <span data-ttu-id="a9f8b-139">Ad</span><span class="sxs-lookup"><span data-stu-id="a9f8b-139">Name</span></span>     | <span data-ttu-id="a9f8b-140">Tür</span><span class="sxs-lookup"><span data-stu-id="a9f8b-140">Type</span></span>    | <span data-ttu-id="a9f8b-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="a9f8b-141">Required</span></span> | <span data-ttu-id="a9f8b-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="a9f8b-142">Description</span></span>                                        |
|----------|---------|----------|----------------------------------------------------|
| <span data-ttu-id="a9f8b-143">**boyutla**</span><span class="sxs-lookup"><span data-stu-id="a9f8b-143">**size**</span></span> | <span data-ttu-id="a9f8b-144">**int**</span><span class="sxs-lookup"><span data-stu-id="a9f8b-144">**int**</span></span> | <span data-ttu-id="a9f8b-145">Y</span><span class="sxs-lookup"><span data-stu-id="a9f8b-145">Y</span></span>        | <span data-ttu-id="a9f8b-146">Tek seferde görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-146">The number of results to be displayed at one time.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="a9f8b-147">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="a9f8b-147">Request headers</span></span>

<span data-ttu-id="a9f8b-148">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="a9f8b-148">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="a9f8b-149">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="a9f8b-149">Request body</span></span>

<span data-ttu-id="a9f8b-150">Yok.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-150">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="a9f8b-151">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="a9f8b-151">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=40 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 3705fc6d-4127-4a87-bdba-9658f73fe019
MS-CorrelationId: b12260fb-82de-4701-a25f-dcd367690645
```

## <a name="rest-response"></a><span data-ttu-id="a9f8b-152">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="a9f8b-152">REST response</span></span>

<span data-ttu-id="a9f8b-153">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Müşteri](customer-resources.md#customer) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-153">If successful, this method returns a collection of [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="a9f8b-154">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="a9f8b-154">Response success and error codes</span></span>

<span data-ttu-id="a9f8b-155">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-155">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="a9f8b-156">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="a9f8b-156">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="a9f8b-157">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="a9f8b-157">For a full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="a9f8b-158">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="a9f8b-158">Response example</span></span>

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
