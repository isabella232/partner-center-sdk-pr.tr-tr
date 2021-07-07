---
title: Silinen bir kullanıcıyı bir müşteri için geri yükleme
description: Silinen bir Kullanıcının müşteri kimliğine ve kullanıcı kimliğine göre geri yükleme.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 23caf91c6b29b292c2638b4a1ad208c606c47492
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445723"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="d671a-103">Silinen bir kullanıcıyı bir müşteri için geri yükleme</span><span class="sxs-lookup"><span data-stu-id="d671a-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="d671a-104">Silinen bir Kullanıcının müşteri **kimliğine ve** kullanıcı kimliğine göre geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="d671a-104">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d671a-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d671a-105">Prerequisites</span></span>

- <span data-ttu-id="d671a-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="d671a-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d671a-107">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="d671a-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d671a-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d671a-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d671a-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="d671a-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d671a-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="d671a-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d671a-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="d671a-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d671a-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="d671a-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d671a-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="d671a-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="d671a-114">Kullanıcı kimliği.</span><span class="sxs-lookup"><span data-stu-id="d671a-114">The user ID.</span></span> <span data-ttu-id="d671a-115">Kullanıcı kimliğiniz yoksa bkz. [Müşteri için silinen kullanıcıları görüntüleme.](view-a-deleted-user.md)</span><span class="sxs-lookup"><span data-stu-id="d671a-115">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="d671a-116">Silinen bir kullanıcı hesabını ne zaman geri yükleyebilirsiniz?</span><span class="sxs-lookup"><span data-stu-id="d671a-116">When can you restore a deleted user account?</span></span>

<span data-ttu-id="d671a-117">Bir kullanıcı hesabını silebilirsiniz, kullanıcı durumu "etkin değil" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="d671a-117">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="d671a-118">30 gün boyunca bu şekilde kalır ve bu sürenin ardından kullanıcı hesabı ve ilişkili verileri temizlenebilir ve kurtarılamaz hale değiştirilebilir.</span><span class="sxs-lookup"><span data-stu-id="d671a-118">It remains that way for 30 days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="d671a-119">Silinen bir kullanıcı hesabını yalnızca bu 30 günlük süre boyunca geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d671a-119">You can only restore a deleted user account during this 30-day window.</span></span> <span data-ttu-id="d671a-120">Silinen ve "etkin olmayan" olarak işaretlenen kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak döndürülemez (örneğin, Bir müşteri için tüm kullanıcı hesaplarının listesini [al](get-a-list-of-all-user-accounts-for-a-customer.md)kullanılarak).</span><span class="sxs-lookup"><span data-stu-id="d671a-120">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="d671a-121">C\#</span><span class="sxs-lookup"><span data-stu-id="d671a-121">C\#</span></span>

<span data-ttu-id="d671a-122">Bir kullanıcı geri yüklemek için [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) sınıfının yeni bir örneğini oluşturun ve User.State özelliğinin değerini [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) [**olarak ayarlayın.**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)</span><span class="sxs-lookup"><span data-stu-id="d671a-122">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="d671a-123">Silinen bir kullanıcının durumunu etkin olarak ayarerek geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d671a-123">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="d671a-124">Kullanıcı kaynağında kalan alanları yeniden doldurmanız zorunda değildir.</span><span class="sxs-lookup"><span data-stu-id="d671a-124">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="d671a-125">Bu değerler silinen, etkin olmayan kullanıcı kaynağından otomatik olarak geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="d671a-125">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="d671a-126">Ardından [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini müşteri kimliğiyle birlikte kullanarak müşteriyi ve kullanıcıyı tanımlamak için [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d671a-126">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="d671a-127">Son olarak [**Patch yöntemini çağırarak**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) **CustomerUser örneğini** geçarak kullanıcıya geri yükleme isteği gönderin.</span><span class="sxs-lookup"><span data-stu-id="d671a-127">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedCustomerUserId;

var updatedCustomerUser = new CustomerUser()
{
    State = UserState.Active
};

// Restore customer user information.
var restoredCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Patch(updatedCustomerUser);
```

<span data-ttu-id="d671a-128">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d671a-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d671a-129">**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="d671a-129">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d671a-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d671a-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d671a-131">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="d671a-131">Request syntax</span></span>

| <span data-ttu-id="d671a-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d671a-132">Method</span></span>    | <span data-ttu-id="d671a-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d671a-133">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d671a-134">**Yama**</span><span class="sxs-lookup"><span data-stu-id="d671a-134">**PATCH**</span></span> | <span data-ttu-id="d671a-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="d671a-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d671a-136">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d671a-136">URI parameter</span></span>

<span data-ttu-id="d671a-137">Müşteri kimliğini ve kullanıcı kimliğini belirtmek için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d671a-137">Use the following query parameters to specify the customer ID and user ID.</span></span>

| <span data-ttu-id="d671a-138">Ad</span><span class="sxs-lookup"><span data-stu-id="d671a-138">Name</span></span>                   | <span data-ttu-id="d671a-139">Tür</span><span class="sxs-lookup"><span data-stu-id="d671a-139">Type</span></span>     | <span data-ttu-id="d671a-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d671a-140">Required</span></span> | <span data-ttu-id="d671a-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d671a-141">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d671a-142">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="d671a-142">**customer-tenant-id**</span></span> | <span data-ttu-id="d671a-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="d671a-143">**guid**</span></span> | <span data-ttu-id="d671a-144">Y</span><span class="sxs-lookup"><span data-stu-id="d671a-144">Y</span></span>        | <span data-ttu-id="d671a-145">Değer, kurumsal bayinin sonuçları belirli bir müşteriye filtrelemesini sağlayan GUID biçimli bir **customer-tenant-id** değeridir.</span><span class="sxs-lookup"><span data-stu-id="d671a-145">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="d671a-146">**user-id**</span><span class="sxs-lookup"><span data-stu-id="d671a-146">**user-id**</span></span>            | <span data-ttu-id="d671a-147">**guid**</span><span class="sxs-lookup"><span data-stu-id="d671a-147">**guid**</span></span> | <span data-ttu-id="d671a-148">Y</span><span class="sxs-lookup"><span data-stu-id="d671a-148">Y</span></span>        | <span data-ttu-id="d671a-149">Değer, tek bir kullanıcı hesabına ait OLAN GUID biçimli bir **user-id** değeridir.</span><span class="sxs-lookup"><span data-stu-id="d671a-149">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="d671a-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d671a-150">Request headers</span></span>

<span data-ttu-id="d671a-151">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="d671a-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d671a-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d671a-152">Request body</span></span>

<span data-ttu-id="d671a-153">Bu tablo, istek gövdesinde gerekli özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="d671a-153">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="d671a-154">Ad</span><span class="sxs-lookup"><span data-stu-id="d671a-154">Name</span></span>       | <span data-ttu-id="d671a-155">Tür</span><span class="sxs-lookup"><span data-stu-id="d671a-155">Type</span></span>   | <span data-ttu-id="d671a-156">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d671a-156">Required</span></span> | <span data-ttu-id="d671a-157">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d671a-157">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="d671a-158">Durum</span><span class="sxs-lookup"><span data-stu-id="d671a-158">State</span></span>      | <span data-ttu-id="d671a-159">string</span><span class="sxs-lookup"><span data-stu-id="d671a-159">string</span></span> | <span data-ttu-id="d671a-160">Y</span><span class="sxs-lookup"><span data-stu-id="d671a-160">Y</span></span>        | <span data-ttu-id="d671a-161">Kullanıcı durumu.</span><span class="sxs-lookup"><span data-stu-id="d671a-161">The user state.</span></span> <span data-ttu-id="d671a-162">Silinen bir kullanıcı geri yüklemek için bu dizenin "etkin" olması gerekir.</span><span class="sxs-lookup"><span data-stu-id="d671a-162">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="d671a-163">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="d671a-163">Attributes</span></span> | <span data-ttu-id="d671a-164">object</span><span class="sxs-lookup"><span data-stu-id="d671a-164">object</span></span> | <span data-ttu-id="d671a-165">N</span><span class="sxs-lookup"><span data-stu-id="d671a-165">N</span></span>        | <span data-ttu-id="d671a-166">"ObjectType": "CustomerUser" ifadesini içerir.</span><span class="sxs-lookup"><span data-stu-id="d671a-166">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="d671a-167">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d671a-167">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 269
Expect: 100-continue

{
    "State": "active",
    "Attributes": {
        "ObjectType": "CustomerUser"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="d671a-168">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d671a-168">REST response</span></span>

<span data-ttu-id="d671a-169">Başarılı olursa yanıt, yanıt gövdesinde geri yüklenen kullanıcı bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="d671a-169">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d671a-170">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d671a-170">Response success and error codes</span></span>

<span data-ttu-id="d671a-171">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="d671a-171">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d671a-172">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d671a-172">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d671a-173">Tam liste için bkz. [REST İş Ortağı Merkezi Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="d671a-173">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d671a-174">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d671a-174">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 465
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 32be760f-8282-4e01-a37b-829c8a700e8a
MS-RequestId: 6e668bc0-5bd7-44d6-b6fa-529d41ce9659
MS-CV: ZTeBriO7mEaiM13+.0
MS-ServerId: 101112616
Date: Fri, 20 Jan 2017 22:24:55 GMT

{
    "usageLocation": "US",
    "id": "a45f1416-3300-4f65-9e8d-f123b397a4ea",
    "userPrincipalName": "e83763f7f2204ac384cfcd49f79f2749@dtdemocspcustomer005.onmicrosoft.com",
    "firstName": "Ferdinand",
    "lastName": "Filibuster",
    "displayName": "Ferdinand",
    "userDomainType": "none",
    "state": "active",
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
```
