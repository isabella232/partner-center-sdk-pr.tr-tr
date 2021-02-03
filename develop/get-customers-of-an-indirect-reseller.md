---
title: Dolaylı bir satıcının müşterilerini alma
description: Dolaylı bir satıcı müşterilerinin listesini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e4219f544a74bb3f34ec3aefe08cf18eed77fd42
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769688"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="23cc5-103">Dolaylı bir satıcının müşterilerini alma</span><span class="sxs-lookup"><span data-stu-id="23cc5-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="23cc5-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="23cc5-104">**Applies To**</span></span>

- <span data-ttu-id="23cc5-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="23cc5-105">Partner Center</span></span>

<span data-ttu-id="23cc5-106">Dolaylı bir satıcı müşterilerinin listesini alma.</span><span class="sxs-lookup"><span data-stu-id="23cc5-106">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="23cc5-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="23cc5-107">Prerequisites</span></span>

- <span data-ttu-id="23cc5-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="23cc5-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="23cc5-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="23cc5-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="23cc5-110">Dolaylı Bayi kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="23cc5-110">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="23cc5-111">C\#</span><span class="sxs-lookup"><span data-stu-id="23cc5-111">C\#</span></span>

<span data-ttu-id="23cc5-112">Belirtilen dolaylı satıcıyla ilişki olan müşterilerin bir koleksiyonunu almak için ilk olarak filtreyi oluşturmak üzere bir [**Simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="23cc5-112">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="23cc5-113">[**Customersearchfield. ındirectbayi**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) numaralandırma üyesini bir dizeye dönüştürmeniz ve [**Fieldfilteroperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) değerlerini filtre işleminin türü olarak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="23cc5-113">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="23cc5-114">Ayrıca, filtrelemeye yönelik dolaylı satıcının kiracı tanımlayıcısını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="23cc5-114">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="23cc5-115">Sonra, [**Buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemini çağırarak ve filtre geçirerek sorguya geçirilecek bir [**ıquery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="23cc5-115">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="23cc5-116">BuildSimplyQuery, [**Queryfactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfının desteklediği sorgu türlerinden yalnızca biridir.</span><span class="sxs-lookup"><span data-stu-id="23cc5-116">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="23cc5-117">Filtreyi yürütmek ve sonucu almak için önce iş ortağının müşteri işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ' ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="23cc5-117">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="23cc5-118">Sonra [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) veya [**queryasync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="23cc5-118">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="23cc5-119">Disk belleğine geçiş yapmak için bir Numaralandırıcı oluşturmak üzere [**ıaggregatepartner. Numaralandırıcılar. Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) özelliğinden müşteri koleksiyonu Numaralandırıcı fabrikası arabirimini alın ve sonra, aşağıdaki kodda gösterildiği gibi, müşteri koleksiyonunu tutan değişkeni geçirerek [**Oluştur**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)'u çağırın.</span><span class="sxs-lookup"><span data-stu-id="23cc5-119">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

``` csharp
IAggregatePartner partnerOperations;
string indirectResellerId;

// Create a filter.
var filter = new SimpleFieldFilter(
    CustomerSearchField.IndirectReseller.ToString(),
    FieldFilterOperation.StartsWith,
    indirectResellerId);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(filter);

// Get the collection of matching customers.
var customersPage = partnerOperations.Customers.Query(myQuery);

// Create a customer enumerator for traversing the customer pages.
var customersEnumerator = partnerOperations.Enumerators.Customers.Create(customersPage);
int pageNumber = 1;

while (customersEnumerator.HasValue)
{
    // Work with the current page.
     foreach (var c in customersEnumerator.Current.Items)
    {
        // Display customer tenant identifier and company name.
        Console.WriteLine(string.Format("{0} - {1}.",c.Id,c.CompanyProfile.CompanyName));
    }
    // Get the next page of customers.
    customersEnumerator.Next();
}
```

<span data-ttu-id="23cc5-120">**Örnek**: [konsol test uygulaması](console-test-app.md)**PROJESI**: iş ortağı Merkezi SDK örnekleri **sınıfı**: GetCustomersOfIndirectReseller.cs</span><span class="sxs-lookup"><span data-stu-id="23cc5-120">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="23cc5-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="23cc5-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="23cc5-122">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="23cc5-122">Request syntax</span></span>

| <span data-ttu-id="23cc5-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="23cc5-123">Method</span></span>  | <span data-ttu-id="23cc5-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="23cc5-124">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="23cc5-125">**Al**</span><span class="sxs-lookup"><span data-stu-id="23cc5-125">**GET**</span></span> | <span data-ttu-id="23cc5-126">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers? size = {size}? Filter = {FILTER} http/1.1</span><span class="sxs-lookup"><span data-stu-id="23cc5-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="23cc5-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="23cc5-127">URI parameter</span></span>

<span data-ttu-id="23cc5-128">İsteği oluşturmak için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="23cc5-128">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="23cc5-129">Ad</span><span class="sxs-lookup"><span data-stu-id="23cc5-129">Name</span></span>   | <span data-ttu-id="23cc5-130">Tür</span><span class="sxs-lookup"><span data-stu-id="23cc5-130">Type</span></span>   | <span data-ttu-id="23cc5-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="23cc5-131">Required</span></span> | <span data-ttu-id="23cc5-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="23cc5-132">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="23cc5-133">boyut</span><span class="sxs-lookup"><span data-stu-id="23cc5-133">size</span></span>   | <span data-ttu-id="23cc5-134">int</span><span class="sxs-lookup"><span data-stu-id="23cc5-134">int</span></span>    | <span data-ttu-id="23cc5-135">No</span><span class="sxs-lookup"><span data-stu-id="23cc5-135">No</span></span>       | <span data-ttu-id="23cc5-136">Tek seferde görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="23cc5-136">The number of results to be displayed at one time.</span></span> <span data-ttu-id="23cc5-137">Bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="23cc5-137">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="23cc5-138">filtre</span><span class="sxs-lookup"><span data-stu-id="23cc5-138">filter</span></span> | <span data-ttu-id="23cc5-139">filtre</span><span class="sxs-lookup"><span data-stu-id="23cc5-139">filter</span></span> | <span data-ttu-id="23cc5-140">Yes</span><span class="sxs-lookup"><span data-stu-id="23cc5-140">Yes</span></span>      | <span data-ttu-id="23cc5-141">Aramaya filtre uygulayan sorgu.</span><span class="sxs-lookup"><span data-stu-id="23cc5-141">The query that filters the search.</span></span> <span data-ttu-id="23cc5-142">Belirtilen bir dolaylı satıcı için müşterileri almak üzere, dolaylı satıcı tanımlayıcısını eklemeniz ve şu dizeyi içermelidir: {"Field": "ındirectbayi", "Value": "{dolaylı satıcı tanımlayıcısı}", "operator": " \_ ile başlar"}.</span><span class="sxs-lookup"><span data-stu-id="23cc5-142">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="23cc5-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="23cc5-143">Request headers</span></span>

<span data-ttu-id="23cc5-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="23cc5-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="23cc5-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="23cc5-145">Request body</span></span>

<span data-ttu-id="23cc5-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="23cc5-146">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="23cc5-147">İstek örneği (kodlanmış)</span><span class="sxs-lookup"><span data-stu-id="23cc5-147">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="23cc5-148">İstek örneği (kodu çözüldü)</span><span class="sxs-lookup"><span data-stu-id="23cc5-148">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="23cc5-149">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="23cc5-149">REST response</span></span>

<span data-ttu-id="23cc5-150">Başarılı olursa, yanıt gövdesi satıcının müşterileri hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="23cc5-150">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="23cc5-151">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="23cc5-151">Response success and error codes</span></span>

<span data-ttu-id="23cc5-152">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="23cc5-152">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="23cc5-153">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="23cc5-153">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="23cc5-154">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="23cc5-154">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="23cc5-155">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="23cc5-155">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 2273
Content-Type: application/json; charset=utf-8
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CV: XI2/vIHmIEGVlGL9.0
MS-ServerId: 101112012
Date: Tue, 11 Apr 2017 23:31:28 GMT

{
    "totalCount": 2,
    "items": [{
            "id": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
            "companyProfile": {
                "tenantId": "53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                "domain": "FourthCoffee137.onmicrosoft.com",
                "companyName": "FourthCoffee137",
                "links": {
                    "self": {
                        "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/53eb21cb-6b2d-4ee5-9e92-27dfc927e93c",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
            "companyProfile": {
                "tenantId": "3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                "domain": "WingtipToys1254789149.onmicrosoft.com",
                "companyName": "Wingtip Toys1254789149",
                "links": {
                    "self": {
                        "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087/profiles/company",
                        "method": "GET",
                        "headers": []
                    }
                },
                "attributes": {
                    "objectType": "CustomerCompanyProfile"
                }
            },
            "relationshipToPartner": "reseller",
            "links": {
                "self": {
                    "uri": "/customers/3dfe847b-cad9-4fc1-86d3-cf16c2790087",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        },
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```
