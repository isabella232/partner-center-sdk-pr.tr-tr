---
title: Müşteri için silinen kullanıcıları görüntüleme
description: Müşteri kimliğine göre bir müşteri için silinen CustomerUser kaynaklarının listesini alır. İsteğe bağlı olarak bir sayfa boyutu da ayarlayabilirsiniz. Bir filtre sağlamak gerekir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f4fec958a9a6bb580d35de1cf3007e1db3b2b650
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445315"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="529a9-105">Müşteri için silinen kullanıcıları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="529a9-105">View deleted users for a customer</span></span>

<span data-ttu-id="529a9-106">Müşteri kimliğine göre bir müşteri için silinen CustomerUser kaynaklarının listesini alır.</span><span class="sxs-lookup"><span data-stu-id="529a9-106">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="529a9-107">İsteğe bağlı olarak bir sayfa boyutu da ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="529a9-107">You can optionally set a page size.</span></span> <span data-ttu-id="529a9-108">Bir filtre sağlamak gerekir.</span><span class="sxs-lookup"><span data-stu-id="529a9-108">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="529a9-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="529a9-109">Prerequisites</span></span>

- <span data-ttu-id="529a9-110">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="529a9-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="529a9-111">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="529a9-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="529a9-112">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="529a9-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="529a9-113">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="529a9-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="529a9-114">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="529a9-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="529a9-115">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="529a9-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="529a9-116">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="529a9-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="529a9-117">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="529a9-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="529a9-118">Bir kullanıcı hesabını silebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="529a9-118">What happens when you delete a user account?</span></span>

<span data-ttu-id="529a9-119">Bir kullanıcı hesabını silebilirsiniz, kullanıcı durumu "etkin değil" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="529a9-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="529a9-120">30 gün boyunca bu şekilde kalır ve bu sürenin ardından kullanıcı hesabı ve ilişkili verileri temizlenebilir ve kurtarılamaz hale değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="529a9-120">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="529a9-121">Silinen bir kullanıcı hesabını 30 günlük süre içinde geri yüklemek için bkz. Silinen bir [kullanıcıyı müşteri için geri yükleme.](restore-a-user-for-a-customer.md)</span><span class="sxs-lookup"><span data-stu-id="529a9-121">If you want to restore a deleted user account within the 30-day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="529a9-122">Silindikten ve "etkin değil" olarak işaretlendiktan sonra, kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak [döndürülemez](get-a-list-of-all-user-accounts-for-a-customer.md)(örneğin, Bir müşteri için tüm kullanıcı hesaplarının listesini al kullanılarak).</span><span class="sxs-lookup"><span data-stu-id="529a9-122">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="529a9-123">Henüz temizlenemeyen silinmiş kullanıcıların listesini almak için etkin değil olarak ayarlanmış kullanıcı hesaplarını sorgulamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="529a9-123">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="529a9-124">C\#</span><span class="sxs-lookup"><span data-stu-id="529a9-124">C\#</span></span>

<span data-ttu-id="529a9-125">Silinen kullanıcıların listesini almak için, durumu etkin olmayan olarak ayarlanmış müşteri kullanıcılarını filtreleten bir sorgu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="529a9-125">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="529a9-126">İlk olarak, aşağıdaki kod parçacığında gösterildiği gibi parametrelerle [**bir SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesi örneği başlatarak filtreyi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="529a9-126">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="529a9-127">Ardından [**BuildIndexedQuery yöntemini kullanarak sorguyu**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="529a9-127">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="529a9-128">Sayfalı sonuçları istemiyorsanız bunun yerine [**BuildSimpleQuery yöntemini kullanabilirsiniz.**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery)</span><span class="sxs-lookup"><span data-stu-id="529a9-128">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="529a9-129">Ardından, müşteriyi [**tanımlamak için IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanın.</span><span class="sxs-lookup"><span data-stu-id="529a9-129">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="529a9-130">Son olarak, isteği göndermek için [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) yöntemini çağırabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="529a9-130">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// int customerUserPageSize;

// Create a filter for users whose status is inactive (i.e. deleted).
var filter = new SimpleFieldFilter("UserState", FieldFilterOperation.Equals, "Inactive");

// Build a paged query.
var simpleQueryWithFilter = QueryFactory.Instance.BuildIndexedQuery(customerUserPageSize, 0, filter);

// Send the request.
var customerUsers = partnerOperations.Customers.ById(selectedCustomerId).Users.Query(simpleQueryWithFilter);
```

<span data-ttu-id="529a9-131">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="529a9-131">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="529a9-132">**Project:** İş Ortağı Merkezi SDK'sı **Örnekler Sınıfı:** GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="529a9-132">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="529a9-133">REST isteği</span><span class="sxs-lookup"><span data-stu-id="529a9-133">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="529a9-134">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="529a9-134">Request syntax</span></span>

| <span data-ttu-id="529a9-135">Yöntem</span><span class="sxs-lookup"><span data-stu-id="529a9-135">Method</span></span>  | <span data-ttu-id="529a9-136">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="529a9-136">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="529a9-137">**Al**</span><span class="sxs-lookup"><span data-stu-id="529a9-137">**GET**</span></span> | <span data-ttu-id="529a9-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="529a9-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="529a9-139">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="529a9-139">URI parameter</span></span>

<span data-ttu-id="529a9-140">İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="529a9-140">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="529a9-141">Ad</span><span class="sxs-lookup"><span data-stu-id="529a9-141">Name</span></span>        | <span data-ttu-id="529a9-142">Tür</span><span class="sxs-lookup"><span data-stu-id="529a9-142">Type</span></span>   | <span data-ttu-id="529a9-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="529a9-143">Required</span></span> | <span data-ttu-id="529a9-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="529a9-144">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="529a9-145">customer-id</span><span class="sxs-lookup"><span data-stu-id="529a9-145">customer-id</span></span> | <span data-ttu-id="529a9-146">guid</span><span class="sxs-lookup"><span data-stu-id="529a9-146">guid</span></span>   | <span data-ttu-id="529a9-147">Yes</span><span class="sxs-lookup"><span data-stu-id="529a9-147">Yes</span></span>      | <span data-ttu-id="529a9-148">Değer, müşteriyi tanımlayan GUID biçimli bir customer-id değeridir.</span><span class="sxs-lookup"><span data-stu-id="529a9-148">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="529a9-149">boyut</span><span class="sxs-lookup"><span data-stu-id="529a9-149">size</span></span>        | <span data-ttu-id="529a9-150">int</span><span class="sxs-lookup"><span data-stu-id="529a9-150">int</span></span>    | <span data-ttu-id="529a9-151">Hayır</span><span class="sxs-lookup"><span data-stu-id="529a9-151">No</span></span>       | <span data-ttu-id="529a9-152">Aynı anda görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="529a9-152">The number of results to be displayed at one time.</span></span> <span data-ttu-id="529a9-153">Bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="529a9-153">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="529a9-154">filtre</span><span class="sxs-lookup"><span data-stu-id="529a9-154">filter</span></span>      | <span data-ttu-id="529a9-155">filtre</span><span class="sxs-lookup"><span data-stu-id="529a9-155">filter</span></span> | <span data-ttu-id="529a9-156">Yes</span><span class="sxs-lookup"><span data-stu-id="529a9-156">Yes</span></span>      | <span data-ttu-id="529a9-157">Kullanıcı aramalarını filtreleen sorgu.</span><span class="sxs-lookup"><span data-stu-id="529a9-157">The query that filters the user search.</span></span> <span data-ttu-id="529a9-158">Silinen kullanıcıları almak için şu dizeyi dahil etmek ve kodlamanız gerekir: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span><span class="sxs-lookup"><span data-stu-id="529a9-158">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="529a9-159">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="529a9-159">Request headers</span></span>

<span data-ttu-id="529a9-160">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="529a9-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="529a9-161">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="529a9-161">Request body</span></span>

<span data-ttu-id="529a9-162">Yok.</span><span class="sxs-lookup"><span data-stu-id="529a9-162">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="529a9-163">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="529a9-163">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="529a9-164">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="529a9-164">REST response</span></span>

<span data-ttu-id="529a9-165">Başarılı olursa, bu yöntem yanıt gövdesinde [CustomerUser](user-resources.md#customeruser) kaynaklarının bir koleksiyonunu döndürür.</span><span class="sxs-lookup"><span data-stu-id="529a9-165">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="529a9-166">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="529a9-166">Response success and error codes</span></span>

<span data-ttu-id="529a9-167">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="529a9-167">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="529a9-168">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="529a9-168">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="529a9-169">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="529a9-169">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="529a9-170">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="529a9-170">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 802
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 690b34ca-07c8-4f8a-ab13-f22a50594a43
MS-RequestId: 1187f9ad-02b4-4d96-b668-7cf3d289467b
MS-CV: 3TLmR9gz6EaCVCjR.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 19:13:14 GMT

{
    "totalCount": 1,
    "items": [{
            "usageLocation": "US",
            "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
            "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
            "firstName": "Ferdinand",
            "lastName": "Filibuster",
            "displayName": "Ferdinand",
            "userDomainType": "none",
            "state": "inactive",
            "softDeletionTime": "2017-01-20T00:33:34Z",
            "links": {
                "self": {
                    "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea",
                    "method": "GET",
                    "headers": []
                }
            },
            "attributes": {
                "objectType": "CustomerUser"
            }
        }
    ],
    "links": {
        "self": {
            "uri": "/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserStatus%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D",
            "method": "GET",
            "headers": []
        }
    },
    "attributes": {
        "objectType": "Collection"
    }
}
```
