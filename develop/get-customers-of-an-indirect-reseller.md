---
title: Dolaylı bir satıcının müşterilerini alma
description: Dolaylı bir satıcı müşterilerinin listesini alma.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e05248b16b803529258de806c25b117f3104ad2a
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446335"
---
# <a name="get-customers-of-an-indirect-reseller"></a><span data-ttu-id="7a507-103">Dolaylı bir satıcının müşterilerini alma</span><span class="sxs-lookup"><span data-stu-id="7a507-103">Get customers of an indirect reseller</span></span>

<span data-ttu-id="7a507-104">Dolaylı bir satıcı müşterilerinin listesini alma.</span><span class="sxs-lookup"><span data-stu-id="7a507-104">How to get a list of the customers of an indirect reseller.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7a507-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="7a507-105">Prerequisites</span></span>

- <span data-ttu-id="7a507-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="7a507-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="7a507-107">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="7a507-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="7a507-108">Dolaylı Bayi kiracı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="7a507-108">The tenant identifier of the indirect reseller.</span></span>

## <a name="c"></a><span data-ttu-id="7a507-109">C\#</span><span class="sxs-lookup"><span data-stu-id="7a507-109">C\#</span></span>

<span data-ttu-id="7a507-110">Belirtilen dolaylı satıcıyla ilişki olan müşterilerin bir koleksiyonunu almak için ilk olarak filtreyi oluşturmak üzere bir [**Simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7a507-110">To get a collection of customers that have a relationship with the specified indirect reseller, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="7a507-111">[**Customersearchfield. ındirectbayi**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) numaralandırma üyesini bir dizeye dönüştürmeniz ve [**Fieldfilteroperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) değerlerini filtre işleminin türü olarak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a507-111">You'll need to pass the [**CustomerSearchField.IndirectReseller**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield) enumeration member converted to a string, and indicate [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation) as the type of filter operation.</span></span> <span data-ttu-id="7a507-112">Ayrıca, filtrelemeye yönelik dolaylı satıcının kiracı tanımlayıcısını sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="7a507-112">You'll also need to provide the tenant identifier of the indirect reseller to filter by.</span></span>

<span data-ttu-id="7a507-113">Sonra, [**Buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemini çağırarak ve filtre geçirerek sorguya geçirilecek bir [**ıquery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="7a507-113">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="7a507-114">BuildSimplyQuery, [**Queryfactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfının desteklediği sorgu türlerinden yalnızca biridir.</span><span class="sxs-lookup"><span data-stu-id="7a507-114">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="7a507-115">Filtreyi yürütmek ve sonucu almak için önce iş ortağının müşteri işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ' ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a507-115">To execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="7a507-116">Sonra [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) veya [**queryasync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="7a507-116">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

<span data-ttu-id="7a507-117">Disk belleğine geçiş yapmak için bir Numaralandırıcı oluşturmak üzere [**ıaggregatepartner. Numaralandırıcılar. Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) özelliğinden müşteri koleksiyonu Numaralandırıcı fabrikası arabirimini alın ve sonra, aşağıdaki kodda gösterildiği gibi, müşteri koleksiyonunu tutan değişkeni geçirerek [**Oluştur**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create)'u çağırın.</span><span class="sxs-lookup"><span data-stu-id="7a507-117">To create an enumerator for traversing paged results, get the customer collection enumerator factory interface from the [**IAggregatePartner.Enumerators.Customers**](/dotnet/api/microsoft.store.partnercenter.enumerators.iresourcecollectionenumeratorcontainer.customers) property, and then call [**Create**](/dotnet/api/microsoft.store.partnercenter.factory.iresourcecollectionenumeratorfactory-1.create), as shown in the code below, passing the variable that holds the customer collection.</span></span>

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

<span data-ttu-id="7a507-118">**örnek**: [konsol test uygulaması](console-test-app.md)**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getcustomersofındirectbayi. cs</span><span class="sxs-lookup"><span data-stu-id="7a507-118">**Sample**: [Console test app](console-test-app.md)**Project**: Partner Center SDK Samples **Class**: GetCustomersOfIndirectReseller.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="7a507-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="7a507-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="7a507-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="7a507-120">Request syntax</span></span>

| <span data-ttu-id="7a507-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="7a507-121">Method</span></span>  | <span data-ttu-id="7a507-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="7a507-122">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="7a507-123">**Al**</span><span class="sxs-lookup"><span data-stu-id="7a507-123">**GET**</span></span> | <span data-ttu-id="7a507-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers? size = {size}? Filter = {FILTER} http/1.1</span><span class="sxs-lookup"><span data-stu-id="7a507-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}?filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="7a507-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="7a507-125">URI parameter</span></span>

<span data-ttu-id="7a507-126">İsteği oluşturmak için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a507-126">Use the following query parameters to create the request.</span></span>

| <span data-ttu-id="7a507-127">Ad</span><span class="sxs-lookup"><span data-stu-id="7a507-127">Name</span></span>   | <span data-ttu-id="7a507-128">Tür</span><span class="sxs-lookup"><span data-stu-id="7a507-128">Type</span></span>   | <span data-ttu-id="7a507-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="7a507-129">Required</span></span> | <span data-ttu-id="7a507-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="7a507-130">Description</span></span>                                                                                                                                                                                                                                                                                   |
|--------|--------|----------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="7a507-131">boyut</span><span class="sxs-lookup"><span data-stu-id="7a507-131">size</span></span>   | <span data-ttu-id="7a507-132">int</span><span class="sxs-lookup"><span data-stu-id="7a507-132">int</span></span>    | <span data-ttu-id="7a507-133">Hayır</span><span class="sxs-lookup"><span data-stu-id="7a507-133">No</span></span>       | <span data-ttu-id="7a507-134">Tek seferde görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="7a507-134">The number of results to be displayed at one time.</span></span> <span data-ttu-id="7a507-135">Bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="7a507-135">This parameter is optional.</span></span>                                                                                                                                                                                                                |
| <span data-ttu-id="7a507-136">filtre</span><span class="sxs-lookup"><span data-stu-id="7a507-136">filter</span></span> | <span data-ttu-id="7a507-137">filtre</span><span class="sxs-lookup"><span data-stu-id="7a507-137">filter</span></span> | <span data-ttu-id="7a507-138">Yes</span><span class="sxs-lookup"><span data-stu-id="7a507-138">Yes</span></span>      | <span data-ttu-id="7a507-139">Aramaya filtre uygulayan sorgu.</span><span class="sxs-lookup"><span data-stu-id="7a507-139">The query that filters the search.</span></span> <span data-ttu-id="7a507-140">Belirtilen bir dolaylı satıcı için müşterileri almak üzere, dolaylı satıcı tanımlayıcısını eklemeniz ve şu dizeyi içermelidir: {"Field": "ındirectbayi", "Value": "{dolaylı satıcı tanımlayıcısı}", "operator": " \_ ile başlar"}.</span><span class="sxs-lookup"><span data-stu-id="7a507-140">To retrieve customers for a specified indirect reseller, you must insert the indirect reseller identifier and include and encode the following string: {"Field":"IndirectReseller","Value":"{indirect reseller identifier}","Operator":"starts\_with"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="7a507-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="7a507-141">Request headers</span></span>

<span data-ttu-id="7a507-142">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="7a507-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="7a507-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="7a507-143">Request body</span></span>

<span data-ttu-id="7a507-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="7a507-144">None.</span></span>

### <a name="request-example-encoded"></a><span data-ttu-id="7a507-145">İstek örneği (kodlanmış)</span><span class="sxs-lookup"><span data-stu-id="7a507-145">Request example (encoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22IndirectReseller%22%2C%22Value%22%3A%22484e548c-f5f3-4528-93a9-c16c6373cb59%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

### <a name="request-example-decoded"></a><span data-ttu-id="7a507-146">İstek örneği (kodu çözüldü)</span><span class="sxs-lookup"><span data-stu-id="7a507-146">Request example (decoded)</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter={"Field":"IndirectReseller","Value":"484e548c-f5f3-4528-93a9-c16c6373cb59","Operator":"starts_with"} HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: aa04fb9d-c6b6-4754-8a6a-86e00cdd5ccb
MS-CorrelationId: b4e67a78-0692-45d1-b408-04b9178a8ac6
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="7a507-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="7a507-147">REST response</span></span>

<span data-ttu-id="7a507-148">Başarılı olursa, yanıt gövdesi satıcının müşterileri hakkındaki bilgileri içerir.</span><span class="sxs-lookup"><span data-stu-id="7a507-148">If successful, the response body contains information about the reseller's customers.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="7a507-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="7a507-149">Response success and error codes</span></span>

<span data-ttu-id="7a507-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="7a507-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="7a507-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="7a507-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="7a507-152">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="7a507-152">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="7a507-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="7a507-153">Response example</span></span>

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
