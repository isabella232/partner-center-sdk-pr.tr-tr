---
title: Müşteri için silinen kullanıcıları görüntüleme
description: Müşteri KIMLIĞINE göre bir müşterinin silinen CustomerUser kaynaklarının bir listesini alır. İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz. Bir filtre sağlamanız gerekir.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9b1a9b85e3eba7ae7ec1dab8e951134d03371604
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769533"
---
# <a name="view-deleted-users-for-a-customer"></a><span data-ttu-id="03d7a-105">Müşteri için silinen kullanıcıları görüntüleme</span><span class="sxs-lookup"><span data-stu-id="03d7a-105">View deleted users for a customer</span></span>

<span data-ttu-id="03d7a-106">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="03d7a-106">**Applies To**</span></span>

- <span data-ttu-id="03d7a-107">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="03d7a-107">Partner Center</span></span>

<span data-ttu-id="03d7a-108">Müşteri KIMLIĞINE göre bir müşterinin silinen CustomerUser kaynaklarının bir listesini alır.</span><span class="sxs-lookup"><span data-stu-id="03d7a-108">Gets a list of deleted CustomerUser resources for a customer by customer ID.</span></span> <span data-ttu-id="03d7a-109">İsteğe bağlı olarak bir sayfa boyutu ayarlayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03d7a-109">You can optionally set a page size.</span></span> <span data-ttu-id="03d7a-110">Bir filtre sağlamanız gerekir.</span><span class="sxs-lookup"><span data-stu-id="03d7a-110">You must supply a filter.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="03d7a-111">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="03d7a-111">Prerequisites</span></span>

- <span data-ttu-id="03d7a-112">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="03d7a-112">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="03d7a-113">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="03d7a-113">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="03d7a-114">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="03d7a-114">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="03d7a-115">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03d7a-115">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="03d7a-116">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="03d7a-116">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="03d7a-117">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="03d7a-117">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="03d7a-118">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="03d7a-118">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="03d7a-119">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="03d7a-119">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="what-happens-when-you-delete-a-user-account"></a><span data-ttu-id="03d7a-120">Bir kullanıcı hesabını sildiğinizde ne olur?</span><span class="sxs-lookup"><span data-stu-id="03d7a-120">What happens when you delete a user account?</span></span>

<span data-ttu-id="03d7a-121">Bir kullanıcı hesabını sildiğinizde Kullanıcı durumu "devre dışı" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="03d7a-121">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="03d7a-122">Bu, otuz gün boyunca, Kullanıcı hesabının ve ilişkili verilerinin temizlenme ve kurtarılamaz hale getirilme yolunda kalır.</span><span class="sxs-lookup"><span data-stu-id="03d7a-122">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="03d7a-123">Bir silinen kullanıcı hesabını otuz gün penceresinde geri yüklemek isterseniz, bkz. bir [müşteri için silinen bir kullanıcıyı geri yükleme](restore-a-user-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="03d7a-123">If you want to restore a deleted user account within the thirty day window, see [Restore a deleted user for a customer](restore-a-user-for-a-customer.md).</span></span> <span data-ttu-id="03d7a-124">Silinen ve "etkin olmayan" olarak işaretlenen Kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak döndürülmez (örneğin, [bir müşterinin tüm Kullanıcı hesaplarının listesini al](get-a-list-of-all-user-accounts-for-a-customer.md)' ı kullanarak).</span><span class="sxs-lookup"><span data-stu-id="03d7a-124">Once deleted and marked "inactive", the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span> <span data-ttu-id="03d7a-125">Henüz temizlenmemiş silinen kullanıcıların bir listesini almak için, etkin olmayan olarak ayarlanmış kullanıcı hesaplarını sorgumalısınız.</span><span class="sxs-lookup"><span data-stu-id="03d7a-125">To get a list of deleted users that have not yet been purged, you must query for user accounts that have been set to inactive.</span></span>

## <a name="c"></a><span data-ttu-id="03d7a-126">C\#</span><span class="sxs-lookup"><span data-stu-id="03d7a-126">C\#</span></span>

<span data-ttu-id="03d7a-127">Silinen kullanıcıların bir listesini almak için, durumu devre dışı olarak ayarlanan müşteri kullanıcıları için filtre uygulayan bir sorgu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03d7a-127">To retrieve a list of deleted users, construct a query that filters for customer users whose status is set to inactive.</span></span> <span data-ttu-id="03d7a-128">İlk olarak, aşağıdaki kod parçacığında gösterildiği gibi parametreleriyle bir [**Simplefieldfilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) nesnesini örnekleyerek filtre oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03d7a-128">First, create the filter by instantiating a [**SimpleFieldFilter**](/dotnet/api/microsoft.store.partnercenter.models.query.simplefieldfilter) object with the parameters as shown in the following code snippet.</span></span> <span data-ttu-id="03d7a-129">Sonra [**Buildındexedquery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) yöntemini kullanarak sorguyu oluşturun.</span><span class="sxs-lookup"><span data-stu-id="03d7a-129">Then create the query using the [**BuildIndexedQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildindexedquery) method.</span></span> <span data-ttu-id="03d7a-130">Disk belleğine alınmış sonuçları istemiyorsanız, bunun yerine [**Buildsimplequery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) yöntemini kullanabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="03d7a-130">If you do not want paged results, you can use the [**BuildSimpleQuery**](/dotnet/api/microsoft.store.partnercenter.models.query.queryfactory.buildsimplequery) method instead.</span></span> <span data-ttu-id="03d7a-131">Ardından, müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="03d7a-131">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="03d7a-132">Son olarak, isteği göndermek için [**sorgu**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="03d7a-132">Finally, call the [**Query**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.query) method to send the request.</span></span>

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

<span data-ttu-id="03d7a-133">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="03d7a-133">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="03d7a-134">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetCustomerInactiveUsers.cs</span><span class="sxs-lookup"><span data-stu-id="03d7a-134">**Project**: Partner Center SDK Samples **Class**: GetCustomerInactiveUsers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="03d7a-135">REST isteği</span><span class="sxs-lookup"><span data-stu-id="03d7a-135">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="03d7a-136">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="03d7a-136">Request syntax</span></span>

| <span data-ttu-id="03d7a-137">Yöntem</span><span class="sxs-lookup"><span data-stu-id="03d7a-137">Method</span></span>  | <span data-ttu-id="03d7a-138">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="03d7a-138">Request URI</span></span>                                                                                                       |
|---------|-------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="03d7a-139">**Al**</span><span class="sxs-lookup"><span data-stu-id="03d7a-139">**GET**</span></span> | <span data-ttu-id="03d7a-140">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users? size = {size} &filtre = {FILTER} http/1.1</span><span class="sxs-lookup"><span data-stu-id="03d7a-140">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users?size={size}&filter={filter} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="03d7a-141">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="03d7a-141">URI parameter</span></span>

<span data-ttu-id="03d7a-142">İsteği oluştururken aşağıdaki yolu ve sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="03d7a-142">Use the following path and query parameters when creating the request.</span></span>

| <span data-ttu-id="03d7a-143">Ad</span><span class="sxs-lookup"><span data-stu-id="03d7a-143">Name</span></span>        | <span data-ttu-id="03d7a-144">Tür</span><span class="sxs-lookup"><span data-stu-id="03d7a-144">Type</span></span>   | <span data-ttu-id="03d7a-145">Gerekli</span><span class="sxs-lookup"><span data-stu-id="03d7a-145">Required</span></span> | <span data-ttu-id="03d7a-146">Açıklama</span><span class="sxs-lookup"><span data-stu-id="03d7a-146">Description</span></span>                                                                                                                                                                        |
|-------------|--------|----------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="03d7a-147">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="03d7a-147">customer-id</span></span> | <span data-ttu-id="03d7a-148">guid</span><span class="sxs-lookup"><span data-stu-id="03d7a-148">guid</span></span>   | <span data-ttu-id="03d7a-149">Yes</span><span class="sxs-lookup"><span data-stu-id="03d7a-149">Yes</span></span>      | <span data-ttu-id="03d7a-150">Değer, müşteriyi tanımlayan bir GUID biçimli müşteri kimliği olur.</span><span class="sxs-lookup"><span data-stu-id="03d7a-150">The value is a GUID formatted customer-id that identifies the customer.</span></span>                                                                                                            |
| <span data-ttu-id="03d7a-151">boyut</span><span class="sxs-lookup"><span data-stu-id="03d7a-151">size</span></span>        | <span data-ttu-id="03d7a-152">int</span><span class="sxs-lookup"><span data-stu-id="03d7a-152">int</span></span>    | <span data-ttu-id="03d7a-153">No</span><span class="sxs-lookup"><span data-stu-id="03d7a-153">No</span></span>       | <span data-ttu-id="03d7a-154">Tek seferde görüntülenecek sonuç sayısı.</span><span class="sxs-lookup"><span data-stu-id="03d7a-154">The number of results to be displayed at one time.</span></span> <span data-ttu-id="03d7a-155">Bu parametre isteğe bağlıdır.</span><span class="sxs-lookup"><span data-stu-id="03d7a-155">This parameter is optional.</span></span>                                                                                                     |
| <span data-ttu-id="03d7a-156">filtre</span><span class="sxs-lookup"><span data-stu-id="03d7a-156">filter</span></span>      | <span data-ttu-id="03d7a-157">filtre</span><span class="sxs-lookup"><span data-stu-id="03d7a-157">filter</span></span> | <span data-ttu-id="03d7a-158">Yes</span><span class="sxs-lookup"><span data-stu-id="03d7a-158">Yes</span></span>      | <span data-ttu-id="03d7a-159">Kullanıcı aramasına filtre uygulayan sorgu.</span><span class="sxs-lookup"><span data-stu-id="03d7a-159">The query that filters the user search.</span></span> <span data-ttu-id="03d7a-160">Silinen kullanıcıları almak için şu dizeyi dahil etmeniz ve kodlamanız gerekir: {"alan": "UserState", "Value": "etkin olmayan", "Işleç": "Equals"}.</span><span class="sxs-lookup"><span data-stu-id="03d7a-160">To retrieve deleted users, you must include and encode the following string: {"Field":"UserState","Value":"Inactive","Operator":"equals"}.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="03d7a-161">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="03d7a-161">Request headers</span></span>

<span data-ttu-id="03d7a-162">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="03d7a-162">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="03d7a-163">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="03d7a-163">Request body</span></span>

<span data-ttu-id="03d7a-164">Yok.</span><span class="sxs-lookup"><span data-stu-id="03d7a-164">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="03d7a-165">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="03d7a-165">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users?size=500&filter=%7B%22Field%22%3A%22UserState%22%2C%22Value%22%3A%22Inactive%22%2C%22Operator%22%3A%22equals%22%7D HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: c11feb95-55d2-45b6-9d1b-74b55d2221fb
MS-CorrelationId: 2b4ab588-f48c-4874-b479-a61895e107b2
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="03d7a-166">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="03d7a-166">REST response</span></span>

<span data-ttu-id="03d7a-167">Başarılı olursa, bu yöntem yanıt gövdesinde bir [Customeruser](user-resources.md#customeruser) kaynakları koleksiyonu döndürür.</span><span class="sxs-lookup"><span data-stu-id="03d7a-167">If successful, this method returns a collection of [CustomerUser](user-resources.md#customeruser) resources in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="03d7a-168">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="03d7a-168">Response success and error codes</span></span>

<span data-ttu-id="03d7a-169">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="03d7a-169">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="03d7a-170">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="03d7a-170">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="03d7a-171">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="03d7a-171">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="03d7a-172">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="03d7a-172">Response example</span></span>

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
