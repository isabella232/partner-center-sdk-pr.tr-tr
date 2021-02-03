---
title: Arama alanına göre filtrelenmiş bir müşteri listesini alma
description: Bir filtreyle eşleşen müşteri kaynakları koleksiyonunu alır. İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz. Şirket adına, etki alanına, dolaylı satıcıya veya dolaylı bulut çözümü sağlayıcısına (CSP) göre filtreleme yapabilirsiniz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: aad9524dbe2c9edbbd7c1d50da7a448f6872fcb9
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769376"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="11736-105">Arama alanına göre filtrelenmiş bir müşteri listesini alma</span><span class="sxs-lookup"><span data-stu-id="11736-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="11736-106">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="11736-106">**Applies To**</span></span>

- <span data-ttu-id="11736-107">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="11736-107">Partner Center</span></span>
- <span data-ttu-id="11736-108">21Vianet tarafından çalıştırılan iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="11736-108">Partner Center operated by 21Vianet</span></span>
- <span data-ttu-id="11736-109">Microsoft Bulut Almanya için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="11736-109">Partner Center for Microsoft Cloud Germany</span></span>
- <span data-ttu-id="11736-110">Microsoft Cloud for US Government için İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="11736-110">Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="11736-111">Bir filtreyle eşleşen [Müşteri](customer-resources.md#customer) kaynakları koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="11736-111">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="11736-112">İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11736-112">You can optionally set a page size.</span></span> <span data-ttu-id="11736-113">Şirket adına, etki alanına, dolaylı satıcıya veya dolaylı bulut çözümü sağlayıcısına (CSP) göre filtreleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="11736-113">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11736-114">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="11736-114">Prerequisites</span></span>

- <span data-ttu-id="11736-115">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="11736-115">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="11736-116">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="11736-116">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="11736-117">Kullanıcı tarafından oluşturulan bir filtre.</span><span class="sxs-lookup"><span data-stu-id="11736-117">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="11736-118">C\#</span><span class="sxs-lookup"><span data-stu-id="11736-118">C\#</span></span>

<span data-ttu-id="11736-119">Bir filtreyle eşleşen müşterilerin bir koleksiyonunu almak için ilk olarak filtreyi oluşturmak üzere bir [**Simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11736-119">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="11736-120">[**Customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)' ı içeren bir dize geçirmeniz ve filtre Işleminin türünü [**Fieldfilteroperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)olarak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="11736-120">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="11736-121">Bu, müşterilerin bitiş noktası tarafından desteklenen tek alan filtresi işlemidir.</span><span class="sxs-lookup"><span data-stu-id="11736-121">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="11736-122">Filtreleyecek dizeyi de sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="11736-122">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="11736-123">Sonra, [**Buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemini çağırarak ve filtre geçirerek sorguya geçirilecek bir [**ıquery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="11736-123">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="11736-124">BuildSimplyQuery, [**Queryfactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfının desteklediği sorgu türlerinden yalnızca biridir.</span><span class="sxs-lookup"><span data-stu-id="11736-124">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="11736-125">Son olarak, filtreyi yürütmek ve sonucu almak için, önce iş ortağının müşteri işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ' ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="11736-125">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="11736-126">Sonra [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) veya [**queryasync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="11736-126">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

``` csharp
IAggregatePartner partnerOperations;

// Specify the partial string to filter by (to match Contoso).
string searchPrefix = "cont"

// Create a simple field filter.
var fieldFilter = new SimpleFieldFilter(
    CustomerSearchField.CompanyName.ToString(),
    FieldFilterOperation.StartsWith,
    searchPrefix);

// Create an iQuery object to pass to the Query method.
var myQuery = QueryFactory.Instance.BuildSimpleQuery(fieldFilter);

// Get the collection of matching customers.
var customers = partnerOperations.Customers.Query(myQuery);
```

<span data-ttu-id="11736-127">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="11736-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="11736-128">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: FilterCustomers.cs</span><span class="sxs-lookup"><span data-stu-id="11736-128">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="11736-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="11736-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="11736-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="11736-130">Request syntax</span></span>

| <span data-ttu-id="11736-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="11736-131">Method</span></span>  | <span data-ttu-id="11736-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="11736-132">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="11736-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="11736-133">**GET**</span></span> | <span data-ttu-id="11736-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers? size = {size} &filtre = {FILTER} http/1.1</span><span class="sxs-lookup"><span data-stu-id="11736-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="11736-135">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="11736-135">URI parameters</span></span>

<span data-ttu-id="11736-136">Aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="11736-136">Use the following query parameters.</span></span>

| <span data-ttu-id="11736-137">Ad</span><span class="sxs-lookup"><span data-stu-id="11736-137">Name</span></span>   | <span data-ttu-id="11736-138">Tür</span><span class="sxs-lookup"><span data-stu-id="11736-138">Type</span></span>   | <span data-ttu-id="11736-139">Gerekli</span><span class="sxs-lookup"><span data-stu-id="11736-139">Required</span></span> | <span data-ttu-id="11736-140">Açıklama</span><span class="sxs-lookup"><span data-stu-id="11736-140">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="11736-141">boyut</span><span class="sxs-lookup"><span data-stu-id="11736-141">size</span></span>   | <span data-ttu-id="11736-142">int</span><span class="sxs-lookup"><span data-stu-id="11736-142">int</span></span>    | <span data-ttu-id="11736-143">No</span><span class="sxs-lookup"><span data-stu-id="11736-143">No</span></span>       | <span data-ttu-id="11736-144">Tek seferde görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="11736-144">The number of results to be displayed at one time.</span></span> <span data-ttu-id="11736-145">Bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="11736-145">This parameter is optional.</span></span> |
| <span data-ttu-id="11736-146">filtre</span><span class="sxs-lookup"><span data-stu-id="11736-146">filter</span></span> | <span data-ttu-id="11736-147">filtre</span><span class="sxs-lookup"><span data-stu-id="11736-147">filter</span></span> | <span data-ttu-id="11736-148">Yes</span><span class="sxs-lookup"><span data-stu-id="11736-148">Yes</span></span>      | <span data-ttu-id="11736-149">Müşterilere uygulanacak filtre.</span><span class="sxs-lookup"><span data-stu-id="11736-149">The filter to apply to customers.</span></span> <span data-ttu-id="11736-150">Bu, kodlanmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="11736-150">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="11736-151">Filtre sözdizimi</span><span class="sxs-lookup"><span data-stu-id="11736-151">Filter Syntax</span></span>

<span data-ttu-id="11736-152">Filtre parametresini bir dizi virgülle ayrılmış anahtar-değer çiftleri olarak oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="11736-152">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="11736-153">Her anahtar ve değer tek tek tırnak içine alınmalıdır ve iki nokta ile ayrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="11736-153">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="11736-154">Filtrenin tamamının kodlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="11736-154">The entire filter must be encoded.</span></span>

<span data-ttu-id="11736-155">Kodlanamayan bir örnek şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="11736-155">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="11736-156">Aşağıdaki tabloda gerekli anahtar-değer çiftleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="11736-156">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="11736-157">Anahtar</span><span class="sxs-lookup"><span data-stu-id="11736-157">Key</span></span>      | <span data-ttu-id="11736-158">Değer</span><span class="sxs-lookup"><span data-stu-id="11736-158">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="11736-159">Alan</span><span class="sxs-lookup"><span data-stu-id="11736-159">Field</span></span>    | <span data-ttu-id="11736-160">Filtrelenecek alan.</span><span class="sxs-lookup"><span data-stu-id="11736-160">The field to filter.</span></span> <span data-ttu-id="11736-161">Geçerli değerler [**Customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)içinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="11736-161">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="11736-162">Değer</span><span class="sxs-lookup"><span data-stu-id="11736-162">Value</span></span>    | <span data-ttu-id="11736-163">Filtrelenecek değer.</span><span class="sxs-lookup"><span data-stu-id="11736-163">The value to filter by.</span></span> <span data-ttu-id="11736-164">Değerin durumu yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="11736-164">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="11736-165">Operatör</span><span class="sxs-lookup"><span data-stu-id="11736-165">Operator</span></span> | <span data-ttu-id="11736-166">Uygulanacak işleç.</span><span class="sxs-lookup"><span data-stu-id="11736-166">The operator to apply.</span></span> <span data-ttu-id="11736-167">Bu müşteri senaryosu için desteklenen tek değer " \_ ile başlar".</span><span class="sxs-lookup"><span data-stu-id="11736-167">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="11736-168">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="11736-168">Request headers</span></span>

<span data-ttu-id="11736-169">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="11736-169">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="11736-170">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="11736-170">Request body</span></span>

<span data-ttu-id="11736-171">Yok.</span><span class="sxs-lookup"><span data-stu-id="11736-171">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="11736-172">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="11736-172">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers?size=0&filter=%7B%22Field%22%3A%22CompanyName%22%2C%22Value%22%3A%22Cont%22%2C%22Operator%22%3A%22starts_with%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 5ce66de5-eea9-486f-a11c-c852aa3d1502
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="11736-173">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="11736-173">REST response</span></span>

<span data-ttu-id="11736-174">Başarılı olursa, bu yöntem yanıt gövdesinde eşleşen [Müşteri](customer-resources.md#customer) kaynakları koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="11736-174">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="11736-175">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="11736-175">Response success and error codes</span></span>

<span data-ttu-id="11736-176">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="11736-176">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="11736-177">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="11736-177">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="11736-178">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="11736-178">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="11736-179">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="11736-179">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 1839
Content-Type: application/json; charset=utf-8
MS-CorrelationId: a2a912ee-d595-47e2-97ae-1b0ae1efa13d
MS-RequestId: dfeda56c-1af5-43fc-a9c0-346b9e85dc96
MS-CV: n0lMNyJtaUC802pO.0
MS-ServerId: 202010223
Date: Fri, 24 Feb 2017 22:08:20 GMT

{
    "totalCount": 3,
    "items": [{
            "id": "c5757d70-06f3-4f23-8367-5a9e55019f94",
            "companyProfile": {
                "tenantId": "c5757d70-06f3-4f23-8367-5a9e55019f94",
                "domain": "contoso190.onmicrosoft.com",
                "companyName": "Contoso190",
                "links": {
                    "self": {
                        "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94/profiles/company",
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
                    "uri": "/customers/c5757d70-06f3-4f23-8367-5a9e55019f94",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
            "companyProfile": {
                "tenantId": "7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                "domain": "ContosoCorpCo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d/profiles/company",
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
                    "uri": "/customers/7b26b357-9ca3-48b8-a58e-4febe2662a5d",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }, {
            "id": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
            "companyProfile": {
                "tenantId": "bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                "domain": "contosocorpdemo.onmicrosoft.com",
                "companyName": "Contoso",
                "links": {
                    "self": {
                        "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b/profiles/company",
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
                    "uri": "/customers/bfbd6ef0-311f-47ec-bbd7-0fcb7846661b",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "Customer"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers?size=0&filter=%7B%22Field%22%3A%22Domain%22%2C%22Value%22%3A%22cont%22%2C%22Operator%22%3A%22starts_with%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
