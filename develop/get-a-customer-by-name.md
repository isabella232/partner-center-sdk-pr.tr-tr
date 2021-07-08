---
title: Arama alanına göre filtrelenmiş bir müşteri listesini alma
description: Bir filtreyle eşleşen müşteri kaynakları koleksiyonunu alır. İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz. Şirket adına, etki alanına, dolaylı satıcıya veya dolaylı bulut çözümü sağlayıcısına (CSP) göre filtreleme yapabilirsiniz.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 663b8509d8704f9c443796d9fbcf72fb9c5b7fb2
ms.sourcegitcommit: b1d6fd0ca93d8a3e30e970844d3164454415f553
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/09/2021
ms.locfileid: "111874967"
---
# <a name="get-a-list-of-customers-filtered-by-a-search-field"></a><span data-ttu-id="5aa43-105">Arama alanına göre filtrelenmiş bir müşteri listesini alma</span><span class="sxs-lookup"><span data-stu-id="5aa43-105">Get a list of customers filtered by a search field</span></span>

<span data-ttu-id="5aa43-106">**Uygulama hedefi**: Iş Ortağı Merkezi | 21Vianet tarafından işletilen iş ortağı Merkezi | Microsoft Bulut Almanya için iş ortağı Merkezi | Microsoft Cloud for US Government için iş ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5aa43-106">**Applies to**: Partner Center | Partner Center operated by 21Vianet | Partner Center for Microsoft Cloud Germany | Partner Center for Microsoft Cloud for US Government</span></span>

<span data-ttu-id="5aa43-107">Bir filtreyle eşleşen [Müşteri](customer-resources.md#customer) kaynakları koleksiyonunu alır.</span><span class="sxs-lookup"><span data-stu-id="5aa43-107">Gets a collection of [Customer](customer-resources.md#customer) resources that match a filter.</span></span> <span data-ttu-id="5aa43-108">İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa43-108">You can optionally set a page size.</span></span> <span data-ttu-id="5aa43-109">Şirket adına, etki alanına, dolaylı satıcıya veya dolaylı bulut çözümü sağlayıcısına (CSP) göre filtreleme yapabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5aa43-109">You can filter by company name, domain, indirect reseller, or indirect cloud solution provider (CSP).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5aa43-110">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5aa43-110">Prerequisites</span></span>

- <span data-ttu-id="5aa43-111">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5aa43-111">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5aa43-112">Bu senaryo, hem tek başına uygulama hem de uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5aa43-112">This scenario supports authentication with both standalone App and App+User credentials.</span></span>

- <span data-ttu-id="5aa43-113">Kullanıcı tarafından oluşturulan bir filtre.</span><span class="sxs-lookup"><span data-stu-id="5aa43-113">A user-constructed filter.</span></span>

## <a name="c"></a><span data-ttu-id="5aa43-114">C\#</span><span class="sxs-lookup"><span data-stu-id="5aa43-114">C\#</span></span>

<span data-ttu-id="5aa43-115">Bir filtreyle eşleşen müşterilerin bir koleksiyonunu almak için ilk olarak filtreyi oluşturmak üzere bir [**Simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5aa43-115">To get a collection of customers that match a filter, first instantiate a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object to create the filter.</span></span> <span data-ttu-id="5aa43-116">[**Customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)' ı içeren bir dize geçirmeniz ve filtre Işleminin türünü [**Fieldfilteroperation. StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation)olarak belirtmeniz gerekir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-116">You'll need to pass a string that contains the [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield), and indicate the type of filter operation as [**FieldFilterOperation.StartsWith**](/dotnet/api/microsoft.store.partnercenter.models.query.fieldfilteroperation).</span></span> <span data-ttu-id="5aa43-117">Bu, müşterilerin bitiş noktası tarafından desteklenen tek alan filtresi işlemidir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-117">That's the only field filter operation supported by the customers end point.</span></span> <span data-ttu-id="5aa43-118">Filtreleyecek dizeyi de sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-118">You'll also need to provide the string to filter by.</span></span>

<span data-ttu-id="5aa43-119">Sonra, [**Buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemini çağırarak ve filtre geçirerek sorguya geçirilecek bir [**ıquery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) nesnesi örneği oluşturun.</span><span class="sxs-lookup"><span data-stu-id="5aa43-119">Next, instantiate an [**iQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.iquery) object to pass to the query by calling the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method and passing it the filter.</span></span> <span data-ttu-id="5aa43-120">BuildSimplyQuery, [**Queryfactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) sınıfının desteklediği sorgu türlerinden yalnızca biridir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-120">BuildSimplyQuery is just one of the query types supported by the [**QueryFactory**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory) class.</span></span>

<span data-ttu-id="5aa43-121">Son olarak, filtreyi yürütmek ve sonucu almak için, önce iş ortağının müşteri işlemlerine bir arabirim almak üzere [**ıaggregatepartner. Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) ' ı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5aa43-121">Finally, to execute the filter and get the result, first use [**IAggregatePartner.Customers**](/dotnet/api/microsoft.store.partnercenter.ipartner.customers) to get an interface to the partner's customer operations.</span></span> <span data-ttu-id="5aa43-122">Sonra [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) veya [**queryasync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5aa43-122">Then call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.query) or [**QueryAsync**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.queryasync) method.</span></span>

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

<span data-ttu-id="5aa43-123">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5aa43-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5aa43-124">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: filtercustomers. cs</span><span class="sxs-lookup"><span data-stu-id="5aa43-124">**Project**: Partner Center SDK Samples **Class**: FilterCustomers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5aa43-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5aa43-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5aa43-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5aa43-126">Request syntax</span></span>

| <span data-ttu-id="5aa43-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5aa43-127">Method</span></span>  | <span data-ttu-id="5aa43-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5aa43-128">Request URI</span></span>                                                                                   |
|---------|-----------------------------------------------------------------------------------------------|
| <span data-ttu-id="5aa43-129">**Al**</span><span class="sxs-lookup"><span data-stu-id="5aa43-129">**GET**</span></span> | <span data-ttu-id="5aa43-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers? size = {size} &filtre = {FILTER} http/1.1</span><span class="sxs-lookup"><span data-stu-id="5aa43-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameters"></a><span data-ttu-id="5aa43-131">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="5aa43-131">URI parameters</span></span>

<span data-ttu-id="5aa43-132">Aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5aa43-132">Use the following query parameters.</span></span>

| <span data-ttu-id="5aa43-133">Ad</span><span class="sxs-lookup"><span data-stu-id="5aa43-133">Name</span></span>   | <span data-ttu-id="5aa43-134">Tür</span><span class="sxs-lookup"><span data-stu-id="5aa43-134">Type</span></span>   | <span data-ttu-id="5aa43-135">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5aa43-135">Required</span></span> | <span data-ttu-id="5aa43-136">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5aa43-136">Description</span></span>                                                                    |
|--------|--------|----------|--------------------------------------------------------------------------------|
| <span data-ttu-id="5aa43-137">boyut</span><span class="sxs-lookup"><span data-stu-id="5aa43-137">size</span></span>   | <span data-ttu-id="5aa43-138">int</span><span class="sxs-lookup"><span data-stu-id="5aa43-138">int</span></span>    | <span data-ttu-id="5aa43-139">Hayır</span><span class="sxs-lookup"><span data-stu-id="5aa43-139">No</span></span>       | <span data-ttu-id="5aa43-140">Tek seferde görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="5aa43-140">The number of results to be displayed at one time.</span></span> <span data-ttu-id="5aa43-141">Bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="5aa43-141">This parameter is optional.</span></span> |
| <span data-ttu-id="5aa43-142">filtre</span><span class="sxs-lookup"><span data-stu-id="5aa43-142">filter</span></span> | <span data-ttu-id="5aa43-143">filtre</span><span class="sxs-lookup"><span data-stu-id="5aa43-143">filter</span></span> | <span data-ttu-id="5aa43-144">Yes</span><span class="sxs-lookup"><span data-stu-id="5aa43-144">Yes</span></span>      | <span data-ttu-id="5aa43-145">Müşterilere uygulanacak filtre.</span><span class="sxs-lookup"><span data-stu-id="5aa43-145">The filter to apply to customers.</span></span> <span data-ttu-id="5aa43-146">Bu, kodlanmış bir dize olmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5aa43-146">This must be an encoded string.</span></span>              |

### <a name="filter-syntax"></a><span data-ttu-id="5aa43-147">Filtre sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5aa43-147">Filter Syntax</span></span>

<span data-ttu-id="5aa43-148">Filtre parametresini bir dizi virgülle ayrılmış anahtar-değer çiftleri olarak oluşturmanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-148">You must compose the filter parameter as a series of comma separated, key-value pairs.</span></span> <span data-ttu-id="5aa43-149">Her anahtar ve değer tek tek tırnak içine alınmalıdır ve iki nokta ile ayrılmalıdır.</span><span class="sxs-lookup"><span data-stu-id="5aa43-149">Each key and value must be individually quoted and separated by a colon.</span></span> <span data-ttu-id="5aa43-150">Filtrenin tamamının kodlanmış olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-150">The entire filter must be encoded.</span></span>

<span data-ttu-id="5aa43-151">Kodlanamayan bir örnek şuna benzer:</span><span class="sxs-lookup"><span data-stu-id="5aa43-151">An unencoded example looks like this:</span></span>

```http
?filter{"Field":"CompanyName","Value":"cont","Operator":"starts_with"}
```

<span data-ttu-id="5aa43-152">Aşağıdaki tabloda gerekli anahtar-değer çiftleri açıklanmaktadır:</span><span class="sxs-lookup"><span data-stu-id="5aa43-152">The following table describes the required key-value pairs:</span></span>

| <span data-ttu-id="5aa43-153">Anahtar</span><span class="sxs-lookup"><span data-stu-id="5aa43-153">Key</span></span>      | <span data-ttu-id="5aa43-154">Değer</span><span class="sxs-lookup"><span data-stu-id="5aa43-154">Value</span></span>                                                                                                                    |
|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5aa43-155">Alan</span><span class="sxs-lookup"><span data-stu-id="5aa43-155">Field</span></span>    | <span data-ttu-id="5aa43-156">Filtrelenecek alan.</span><span class="sxs-lookup"><span data-stu-id="5aa43-156">The field to filter.</span></span> <span data-ttu-id="5aa43-157">Geçerli değerler [**Customersearchfield**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield)içinde bulunabilir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-157">The valid values can be found in [**CustomerSearchField**](/dotnet/api/microsoft.store.partnercenter.models.customers.customersearchfield).</span></span> |
| <span data-ttu-id="5aa43-158">Değer</span><span class="sxs-lookup"><span data-stu-id="5aa43-158">Value</span></span>    | <span data-ttu-id="5aa43-159">Filtrelenecek değer.</span><span class="sxs-lookup"><span data-stu-id="5aa43-159">The value to filter by.</span></span> <span data-ttu-id="5aa43-160">Değerin durumu yok sayılır.</span><span class="sxs-lookup"><span data-stu-id="5aa43-160">The case of the value is ignored.</span></span>                                                                |
| <span data-ttu-id="5aa43-161">Operatör</span><span class="sxs-lookup"><span data-stu-id="5aa43-161">Operator</span></span> | <span data-ttu-id="5aa43-162">Uygulanacak işleç.</span><span class="sxs-lookup"><span data-stu-id="5aa43-162">The operator to apply.</span></span> <span data-ttu-id="5aa43-163">Bu müşteri senaryosu için desteklenen tek değer " \_ ile başlar".</span><span class="sxs-lookup"><span data-stu-id="5aa43-163">The only supported value for this customer scenario is "starts\_with".</span></span>                            |

### <a name="request-headers"></a><span data-ttu-id="5aa43-164">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5aa43-164">Request headers</span></span>

<span data-ttu-id="5aa43-165">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5aa43-165">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5aa43-166">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5aa43-166">Request body</span></span>

<span data-ttu-id="5aa43-167">Yok.</span><span class="sxs-lookup"><span data-stu-id="5aa43-167">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5aa43-168">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5aa43-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="5aa43-169">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5aa43-169">REST response</span></span>

<span data-ttu-id="5aa43-170">Başarılı olursa, bu yöntem yanıt gövdesinde eşleşen [Müşteri](customer-resources.md#customer) kaynakları koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="5aa43-170">If successful, this method returns a collection of matching [Customer](customer-resources.md#customer) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5aa43-171">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5aa43-171">Response success and error codes</span></span>

<span data-ttu-id="5aa43-172">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5aa43-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5aa43-173">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5aa43-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5aa43-174">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5aa43-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5aa43-175">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5aa43-175">Response example</span></span>

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
