---
title: Silinen bir kullanıcıyı bir müşteri için geri yükleme
description: Silinen bir kullanıcıyı müşteri KIMLIĞINE ve Kullanıcı KIMLIĞINE göre geri yükleme.
ms.date: 07/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 9fd86a268c804a2fdd5efd67a8982afc043c95a6
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769797"
---
# <a name="restore-a-deleted-user-for-a-customer"></a><span data-ttu-id="3d788-103">Silinen bir kullanıcıyı bir müşteri için geri yükleme</span><span class="sxs-lookup"><span data-stu-id="3d788-103">Restore a deleted user for a customer</span></span>

<span data-ttu-id="3d788-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="3d788-104">**Applies To**</span></span>

- <span data-ttu-id="3d788-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="3d788-105">Partner Center</span></span>

<span data-ttu-id="3d788-106">Silinen bir **kullanıcıyı** müşteri kimliğine ve kullanıcı kimliğine göre geri yükleme.</span><span class="sxs-lookup"><span data-stu-id="3d788-106">How to restore a deleted **User** by customer ID and user ID.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="3d788-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="3d788-107">Prerequisites</span></span>

- <span data-ttu-id="3d788-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="3d788-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="3d788-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="3d788-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="3d788-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="3d788-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="3d788-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d788-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="3d788-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="3d788-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="3d788-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="3d788-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="3d788-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="3d788-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="3d788-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="3d788-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="3d788-116">Kullanıcı kimliği.</span><span class="sxs-lookup"><span data-stu-id="3d788-116">The user ID.</span></span> <span data-ttu-id="3d788-117">Kullanıcı KIMLIĞINIZ yoksa, bkz. [bir müşteri için silinen kullanıcıları görüntüleme](view-a-deleted-user.md).</span><span class="sxs-lookup"><span data-stu-id="3d788-117">If you do not have the user ID, see [View deleted users for a customer](view-a-deleted-user.md).</span></span>

## <a name="when-can-you-restore-a-deleted-user-account"></a><span data-ttu-id="3d788-118">Silinen bir kullanıcı hesabını geri yüklemek ne zaman olabilir?</span><span class="sxs-lookup"><span data-stu-id="3d788-118">When can you restore a deleted user account?</span></span>

<span data-ttu-id="3d788-119">Bir kullanıcı hesabını sildiğinizde Kullanıcı durumu "devre dışı" olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="3d788-119">The user state is set to "inactive" when you delete a user account.</span></span> <span data-ttu-id="3d788-120">Bu, otuz gün boyunca, Kullanıcı hesabının ve ilişkili verilerinin temizlenme ve kurtarılamaz hale getirilme yolunda kalır.</span><span class="sxs-lookup"><span data-stu-id="3d788-120">It remains that way for thirty days, after which the user account and its associated data are purged and made unrecoverable.</span></span> <span data-ttu-id="3d788-121">Silinen bir kullanıcı hesabını yalnızca bu otuz günlük pencere sırasında geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d788-121">You can only restore a deleted user account during this thirty-day window.</span></span> <span data-ttu-id="3d788-122">Silinen ve "etkin olmayan" olarak işaretlenen "etkin değil" Kullanıcı hesabı artık kullanıcı koleksiyonunun bir üyesi olarak döndürülmez (örneğin, [bir müşterinin tüm Kullanıcı hesaplarının listesini al](get-a-list-of-all-user-accounts-for-a-customer.md)' ı kullanarak).</span><span class="sxs-lookup"><span data-stu-id="3d788-122">Once deleted and marked "inactive" the user account is no longer returned as a member of the user collection (for example, using [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="3d788-123">C\#</span><span class="sxs-lookup"><span data-stu-id="3d788-123">C\#</span></span>

<span data-ttu-id="3d788-124">Bir kullanıcıyı geri yüklemek için [**customeruser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) sınıfının yeni bir örneğini oluşturun ve [**User. State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) özelliğinin değerini [**userState. Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate)olarak ayarlayın.</span><span class="sxs-lookup"><span data-stu-id="3d788-124">To restore a user, create a new instance of the [**CustomerUser**](/dotnet/api/microsoft.store.partnercenter.models.users.customeruser) class, and set the value of the [**User.State**](/dotnet/api/microsoft.store.partnercenter.models.users.user.state) property to [**UserState.Active**](/dotnet/api/microsoft.store.partnercenter.models.users.userstate).</span></span>

<span data-ttu-id="3d788-125">Silinen bir kullanıcıyı, kullanıcının durumunu etkin olarak ayarlayarak geri yükleyebilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="3d788-125">You restore a deleted user by setting the user's state to active.</span></span> <span data-ttu-id="3d788-126">Kullanıcı kaynağındaki kalan alanları yeniden doldurmanız gerekmez.</span><span class="sxs-lookup"><span data-stu-id="3d788-126">You do not have to repopulate the remaining fields in the user resource.</span></span> <span data-ttu-id="3d788-127">Bu değerler, silinen, etkin olmayan kullanıcı kaynağından otomatik olarak geri yüklenir.</span><span class="sxs-lookup"><span data-stu-id="3d788-127">Those values will automatically be restored from the deleted, inactive user resource.</span></span> <span data-ttu-id="3d788-128">Ardından, müşteriyi tanımlamak için müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini ve kullanıcıyı tanımlamak için [**Users. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d788-128">Next, use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer, and the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

<span data-ttu-id="3d788-129">Son olarak, [**yama**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) yöntemini çağırın ve kullanıcıyı geri yükleme isteğini göndermek Için **customeruser** örneğini geçirin.</span><span class="sxs-lookup"><span data-stu-id="3d788-129">Finally, call the [**Patch**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.patch) method and pass the **CustomerUser** instance to send the request to restore the user.</span></span>

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

<span data-ttu-id="3d788-130">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="3d788-130">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="3d788-131">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CustomerUserRestore.cs</span><span class="sxs-lookup"><span data-stu-id="3d788-131">**Project**: Partner Center SDK Samples **Class**: CustomerUserRestore.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="3d788-132">REST isteği</span><span class="sxs-lookup"><span data-stu-id="3d788-132">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="3d788-133">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="3d788-133">Request syntax</span></span>

| <span data-ttu-id="3d788-134">Yöntem</span><span class="sxs-lookup"><span data-stu-id="3d788-134">Method</span></span>    | <span data-ttu-id="3d788-135">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="3d788-135">Request URI</span></span>                                                                                            |
|-----------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3d788-136">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="3d788-136">**PATCH**</span></span> | <span data-ttu-id="3d788-137">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="3d788-137">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="3d788-138">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="3d788-138">URI parameter</span></span>

<span data-ttu-id="3d788-139">Müşteri kimliğini ve Kullanıcı kimliğini belirtmek için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d788-139">Use the following query parameters to specify the customer id and user id.</span></span>

| <span data-ttu-id="3d788-140">Ad</span><span class="sxs-lookup"><span data-stu-id="3d788-140">Name</span></span>                   | <span data-ttu-id="3d788-141">Tür</span><span class="sxs-lookup"><span data-stu-id="3d788-141">Type</span></span>     | <span data-ttu-id="3d788-142">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3d788-142">Required</span></span> | <span data-ttu-id="3d788-143">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3d788-143">Description</span></span>                                                                                                              |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="3d788-144">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="3d788-144">**customer-tenant-id**</span></span> | <span data-ttu-id="3d788-145">**guid**</span><span class="sxs-lookup"><span data-stu-id="3d788-145">**guid**</span></span> | <span data-ttu-id="3d788-146">Y</span><span class="sxs-lookup"><span data-stu-id="3d788-146">Y</span></span>        | <span data-ttu-id="3d788-147">Değer, satıcının sonuçları belirli bir müşteriye filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="3d788-147">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results to a given customer.</span></span> |
| <span data-ttu-id="3d788-148">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="3d788-148">**user-id**</span></span>            | <span data-ttu-id="3d788-149">**guid**</span><span class="sxs-lookup"><span data-stu-id="3d788-149">**guid**</span></span> | <span data-ttu-id="3d788-150">Y</span><span class="sxs-lookup"><span data-stu-id="3d788-150">Y</span></span>        | <span data-ttu-id="3d788-151">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="3d788-151">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                         |

### <a name="request-headers"></a><span data-ttu-id="3d788-152">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="3d788-152">Request headers</span></span>

<span data-ttu-id="3d788-153">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="3d788-153">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="3d788-154">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="3d788-154">Request body</span></span>

<span data-ttu-id="3d788-155">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="3d788-155">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="3d788-156">Ad</span><span class="sxs-lookup"><span data-stu-id="3d788-156">Name</span></span>       | <span data-ttu-id="3d788-157">Tür</span><span class="sxs-lookup"><span data-stu-id="3d788-157">Type</span></span>   | <span data-ttu-id="3d788-158">Gerekli</span><span class="sxs-lookup"><span data-stu-id="3d788-158">Required</span></span> | <span data-ttu-id="3d788-159">Açıklama</span><span class="sxs-lookup"><span data-stu-id="3d788-159">Description</span></span>                                                            |
|------------|--------|----------|------------------------------------------------------------------------|
| <span data-ttu-id="3d788-160">Durum</span><span class="sxs-lookup"><span data-stu-id="3d788-160">State</span></span>      | <span data-ttu-id="3d788-161">string</span><span class="sxs-lookup"><span data-stu-id="3d788-161">string</span></span> | <span data-ttu-id="3d788-162">Y</span><span class="sxs-lookup"><span data-stu-id="3d788-162">Y</span></span>        | <span data-ttu-id="3d788-163">Kullanıcı durumu.</span><span class="sxs-lookup"><span data-stu-id="3d788-163">The user state.</span></span> <span data-ttu-id="3d788-164">Silinen bir kullanıcıyı geri yüklemek için, bu dize "etkin" içermelidir.</span><span class="sxs-lookup"><span data-stu-id="3d788-164">To restore a deleted user, this string must contain "active".</span></span> |
| <span data-ttu-id="3d788-165">Öznitelikler</span><span class="sxs-lookup"><span data-stu-id="3d788-165">Attributes</span></span> | <span data-ttu-id="3d788-166">object</span><span class="sxs-lookup"><span data-stu-id="3d788-166">object</span></span> | <span data-ttu-id="3d788-167">N</span><span class="sxs-lookup"><span data-stu-id="3d788-167">N</span></span>        | <span data-ttu-id="3d788-168">"ObjectType": "CustomerUser" içerir.</span><span class="sxs-lookup"><span data-stu-id="3d788-168">Contains "ObjectType": "CustomerUser".</span></span>                                 |

### <a name="request-example"></a><span data-ttu-id="3d788-169">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="3d788-169">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="3d788-170">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="3d788-170">REST response</span></span>

<span data-ttu-id="3d788-171">Başarılı olursa yanıt, yanıt gövdesinde geri yüklenen Kullanıcı bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="3d788-171">If successful, the response returns the restored user information in the response body.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="3d788-172">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="3d788-172">Response success and error codes</span></span>

<span data-ttu-id="3d788-173">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="3d788-173">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="3d788-174">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="3d788-174">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="3d788-175">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="3d788-175">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="3d788-176">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="3d788-176">Response example</span></span>

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
