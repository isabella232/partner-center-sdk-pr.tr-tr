---
title: Müşteri için kullanıcı rolleri ayarlama
description: Bir müşteri hesabı içinde, bir dizi dizin rolü vardır. Bu rollere kullanıcı hesapları atayabilirsiniz.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: f42120e40e54ff8bd6242634d97268091abf8e1c
ms.sourcegitcommit: 30d1b9d48453c7697a2f42ee09138e507dcf9f2d
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 10/19/2020
ms.locfileid: "97769592"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="78b11-104">Müşteri için kullanıcı rolleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="78b11-104">Set user roles for a customer</span></span>

<span data-ttu-id="78b11-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="78b11-105">**Applies To**</span></span>

- <span data-ttu-id="78b11-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="78b11-106">Partner Center</span></span>

<span data-ttu-id="78b11-107">Bir müşteri hesabı içinde, bir dizi dizin rolü vardır.</span><span class="sxs-lookup"><span data-stu-id="78b11-107">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="78b11-108">Bu rollere kullanıcı hesapları atayabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78b11-108">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78b11-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="78b11-109">Prerequisites</span></span>

- <span data-ttu-id="78b11-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="78b11-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="78b11-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="78b11-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="78b11-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="78b11-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="78b11-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="78b11-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="78b11-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="78b11-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="78b11-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="78b11-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="78b11-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="78b11-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="78b11-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="78b11-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="78b11-118">C\#</span><span class="sxs-lookup"><span data-stu-id="78b11-118">C\#</span></span>

<span data-ttu-id="78b11-119">Bir müşteri kullanıcısına bir dizin rolü atamak için, ilgili kullanıcı ayrıntıları ile yeni bir [**Usermember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="78b11-119">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="78b11-120">Ardından, müşteriyi tanımlamak için belirtilen müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="78b11-120">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="78b11-121">Buradan, rolü belirtmek için dizin rolü KIMLIĞIYLE [**Directoryroles. byıd**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metodunu kullanın.</span><span class="sxs-lookup"><span data-stu-id="78b11-121">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="78b11-122">Ardından, **Usermembers** koleksiyonuna erişin ve [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) metodunu kullanarak yeni Kullanıcı üyesini bu role atanan kullanıcı üyeleri koleksiyonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="78b11-122">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

``` csharp
// UserMember createdUser;
// IAggregatePartner partnerOperations;
// Customer selectedCustomer;
// IDirectoryRole selectedRole;

// Create the new user member.
UserMember userMemberToAdd = new UserMember()
{
    UserPrincipalName = createdUser.UserPrincipalName,
    DisplayName = createdUser.DisplayName,
    Id = createdUser.Id
};

// Add the new user member to the role.
var userMemberAdded = partnerOperations.Customers.ById(selectedCustomer.Id).DirectoryRoles.ById(selectedRole.Id).UserMembers.Create(userMemberToAdd);
```

<span data-ttu-id="78b11-123">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="78b11-123">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="78b11-124">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="78b11-124">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="78b11-125">REST isteği</span><span class="sxs-lookup"><span data-stu-id="78b11-125">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="78b11-126">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="78b11-126">Request syntax</span></span>

| <span data-ttu-id="78b11-127">Yöntem</span><span class="sxs-lookup"><span data-stu-id="78b11-127">Method</span></span>   | <span data-ttu-id="78b11-128">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="78b11-128">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="78b11-129">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="78b11-129">**POST**</span></span> | <span data-ttu-id="78b11-130">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-id}/usermembers http/1.1</span><span class="sxs-lookup"><span data-stu-id="78b11-130">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="78b11-131">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="78b11-131">URI parameter</span></span>

<span data-ttu-id="78b11-132">Doğru müşteriyi ve rolü tanımlamak için aşağıdaki URI parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="78b11-132">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="78b11-133">Rolün atanacağı kullanıcıyı belirlemek için, istek gövdesinde tanımlama bilgilerini sağlayın.</span><span class="sxs-lookup"><span data-stu-id="78b11-133">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="78b11-134">Ad</span><span class="sxs-lookup"><span data-stu-id="78b11-134">Name</span></span>                   | <span data-ttu-id="78b11-135">Tür</span><span class="sxs-lookup"><span data-stu-id="78b11-135">Type</span></span>     | <span data-ttu-id="78b11-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="78b11-136">Required</span></span> | <span data-ttu-id="78b11-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78b11-137">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="78b11-138">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="78b11-138">**customer-tenant-id**</span></span> | <span data-ttu-id="78b11-139">**guid**</span><span class="sxs-lookup"><span data-stu-id="78b11-139">**guid**</span></span> | <span data-ttu-id="78b11-140">Y</span><span class="sxs-lookup"><span data-stu-id="78b11-140">Y</span></span>        | <span data-ttu-id="78b11-141">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="78b11-141">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="78b11-142">**rol kimliği**</span><span class="sxs-lookup"><span data-stu-id="78b11-142">**role-id**</span></span>            | <span data-ttu-id="78b11-143">**guid**</span><span class="sxs-lookup"><span data-stu-id="78b11-143">**guid**</span></span> | <span data-ttu-id="78b11-144">Y</span><span class="sxs-lookup"><span data-stu-id="78b11-144">Y</span></span>        | <span data-ttu-id="78b11-145">Değer, kullanıcıya atanacak rolü tanımlayan bir GUID biçimli **rol kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="78b11-145">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="78b11-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="78b11-146">Request headers</span></span>

<span data-ttu-id="78b11-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="78b11-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="78b11-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="78b11-148">Request body</span></span>

<span data-ttu-id="78b11-149">Bu tabloda, istek gövdesinde gereken özellikler açıklanmaktadır.</span><span class="sxs-lookup"><span data-stu-id="78b11-149">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="78b11-150">Ad</span><span class="sxs-lookup"><span data-stu-id="78b11-150">Name</span></span>                  | <span data-ttu-id="78b11-151">Tür</span><span class="sxs-lookup"><span data-stu-id="78b11-151">Type</span></span>       | <span data-ttu-id="78b11-152">Gerekli</span><span class="sxs-lookup"><span data-stu-id="78b11-152">Required</span></span> | <span data-ttu-id="78b11-153">Açıklama</span><span class="sxs-lookup"><span data-stu-id="78b11-153">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="78b11-154">**Numarasını**</span><span class="sxs-lookup"><span data-stu-id="78b11-154">**Id**</span></span>                | <span data-ttu-id="78b11-155">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="78b11-155">**string**</span></span> | <span data-ttu-id="78b11-156">Y</span><span class="sxs-lookup"><span data-stu-id="78b11-156">Y</span></span>        | <span data-ttu-id="78b11-157">Role eklenecek kullanıcının kimliği.</span><span class="sxs-lookup"><span data-stu-id="78b11-157">The Id of the user to add to the role.</span></span> |
| <span data-ttu-id="78b11-158">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="78b11-158">**DisplayName**</span></span>       | <span data-ttu-id="78b11-159">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="78b11-159">**string**</span></span> | <span data-ttu-id="78b11-160">Y</span><span class="sxs-lookup"><span data-stu-id="78b11-160">Y</span></span>        | <span data-ttu-id="78b11-161">Kullanıcının kolay görünen adı.</span><span class="sxs-lookup"><span data-stu-id="78b11-161">The friendly display name of the user.</span></span> |
| <span data-ttu-id="78b11-162">**UserPrincipalName**</span><span class="sxs-lookup"><span data-stu-id="78b11-162">**UserPrincipalName**</span></span> | <span data-ttu-id="78b11-163">**dizisinde**</span><span class="sxs-lookup"><span data-stu-id="78b11-163">**string**</span></span> | <span data-ttu-id="78b11-164">Y</span><span class="sxs-lookup"><span data-stu-id="78b11-164">Y</span></span>        | <span data-ttu-id="78b11-165">Kullanıcı sorumlusunun adı.</span><span class="sxs-lookup"><span data-stu-id="78b11-165">The name of the user principal.</span></span>        |
| <span data-ttu-id="78b11-166">**Öznitelikler**</span><span class="sxs-lookup"><span data-stu-id="78b11-166">**Attributes**</span></span>        | <span data-ttu-id="78b11-167">**nesne**</span><span class="sxs-lookup"><span data-stu-id="78b11-167">**object**</span></span> | <span data-ttu-id="78b11-168">Y</span><span class="sxs-lookup"><span data-stu-id="78b11-168">Y</span></span>        | <span data-ttu-id="78b11-169">"ObjectType" içerir: "UserMember"</span><span class="sxs-lookup"><span data-stu-id="78b11-169">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="78b11-170">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="78b11-170">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/directoryroles/f023fd81-a637-4b56-95fd-791ac0226033/usermembers HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
X-Locale: en-US
Content-Type: application/json
Host: api.partnercenter.microsoft.com
Content-Length: 180
Expect: 100-continue

{
    "Id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "DisplayName": "Daniel Tsai",
    "UserPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "Attributes": {
        "ObjectType": "UserMember"
    }
}
```

## <a name="rest-response"></a><span data-ttu-id="78b11-171">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="78b11-171">REST response</span></span>

<span data-ttu-id="78b11-172">Bu yöntem, Kullanıcı rolü başarıyla atandığında eklenen rol kimliğine sahip kullanıcı hesabını döndürür.</span><span class="sxs-lookup"><span data-stu-id="78b11-172">This method returns the user account with the role id attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="78b11-173">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="78b11-173">Response success and error codes</span></span>

<span data-ttu-id="78b11-174">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="78b11-174">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="78b11-175">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="78b11-175">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="78b11-176">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="78b11-176">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="78b11-177">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="78b11-177">Response example</span></span>

```http
HTTP/1.1 201 Created
Content-Length: 231
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: a56cb2e5-a156-4f68-9155-57ffe2b93d18
MS-CV: aia94+gnrEeQqkGr.0
MS-ServerId: 101112202
Date: Tue, 20 Dec 2016 23:36:55 GMT

{
    "displayName": "Daniel Tsai",
    "userPrincipalName": "Daniel@dtdemocspcustomer005.onmicrosoft.com",
    "roleId": "f023fd81-a637-4b56-95fd-791ac0226033",
    "id": "a9ef48bb-8758-4590-a312-d4a47bfaded4",
    "attributes": {
        "objectType": "UserMember"
    }
}
```
