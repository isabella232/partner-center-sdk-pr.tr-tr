---
title: Müşteri için kullanıcı rolleri ayarlama
description: Bir müşteri hesabı içinde bir dizi dizin rolü vardır. Bu rollere kullanıcı hesapları atabilirsiniz.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: a035d711ffa91200fa7b479ed5ec53929aa4feaf
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111446709"
---
# <a name="set-user-roles-for-a-customer"></a><span data-ttu-id="53a7f-104">Müşteri için kullanıcı rolleri ayarlama</span><span class="sxs-lookup"><span data-stu-id="53a7f-104">Set user roles for a customer</span></span>

<span data-ttu-id="53a7f-105">Bir müşteri hesabı içinde bir dizi dizin rolü vardır.</span><span class="sxs-lookup"><span data-stu-id="53a7f-105">Within a customer account, there's a set of directory roles.</span></span> <span data-ttu-id="53a7f-106">Bu rollere kullanıcı hesapları atabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="53a7f-106">You can assign user accounts to those roles.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="53a7f-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="53a7f-107">Prerequisites</span></span>

- <span data-ttu-id="53a7f-108">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="53a7f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="53a7f-109">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="53a7f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="53a7f-110">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="53a7f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="53a7f-111">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="53a7f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="53a7f-112">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="53a7f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="53a7f-113">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="53a7f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="53a7f-114">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="53a7f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="53a7f-115">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="53a7f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="53a7f-116">C\#</span><span class="sxs-lookup"><span data-stu-id="53a7f-116">C\#</span></span>

<span data-ttu-id="53a7f-117">Bir müşteri kullanıcıya dizin rolü atamak için, ilgili kullanıcı ayrıntılarıyla [**yeni bir UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) oluşturun.</span><span class="sxs-lookup"><span data-stu-id="53a7f-117">To assign a directory role to a customer user, create a new [**UserMember**](/dotnet/api/microsoft.store.partnercenter.models.roles.usermember) with the relevant user details.</span></span> <span data-ttu-id="53a7f-118">Ardından, müşteriyi [**tanımlamak için belirtilen müşteri kimliğiyle IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="53a7f-118">Then, call the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the specified customer ID to identify the customer.</span></span> <span data-ttu-id="53a7f-119">Burada, rolü belirtmek için [**dizin rolü kimliğiyle DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="53a7f-119">From there, use the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID to specify the role.</span></span> <span data-ttu-id="53a7f-120">Ardından **UserMembers koleksiyonuna** erişin ve [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) yöntemini kullanarak yeni kullanıcı üyesini bu role atanan kullanıcı üyeleri koleksiyonuna ekleyin.</span><span class="sxs-lookup"><span data-stu-id="53a7f-120">Then, access the **UserMembers** collection, and use the [**Create**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.create) method to add the new user member to the collection of user members assigned to that role.</span></span>

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

<span data-ttu-id="53a7f-121">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="53a7f-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="53a7f-122">**Project:** İş Ortağı Merkezi SDK'sı Samples **Sınıfı:** AddUserMemberToDirectoryRole.cs</span><span class="sxs-lookup"><span data-stu-id="53a7f-122">**Project**: Partner Center SDK Samples **Class**: AddUserMemberToDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="53a7f-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="53a7f-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="53a7f-124">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="53a7f-124">Request syntax</span></span>

| <span data-ttu-id="53a7f-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="53a7f-125">Method</span></span>   | <span data-ttu-id="53a7f-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="53a7f-126">Request URI</span></span>                                                                                                                 |
|----------|-----------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="53a7f-127">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="53a7f-127">**POST**</span></span> | <span data-ttu-id="53a7f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="53a7f-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="53a7f-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="53a7f-129">URI parameter</span></span>

<span data-ttu-id="53a7f-130">Doğru müşteriyi ve rolü belirlemek için aşağıdaki URI parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="53a7f-130">Use the following URI parameters to identify the correct customer and role.</span></span> <span data-ttu-id="53a7f-131">Rolün atanacak kullanıcıyı belirlemek için, istek gövdesinde tanımlayıcı bilgileri sağlar.</span><span class="sxs-lookup"><span data-stu-id="53a7f-131">To identify the user to whom to assign the role, supply the identifying information in the request body.</span></span>

| <span data-ttu-id="53a7f-132">Ad</span><span class="sxs-lookup"><span data-stu-id="53a7f-132">Name</span></span>                   | <span data-ttu-id="53a7f-133">Tür</span><span class="sxs-lookup"><span data-stu-id="53a7f-133">Type</span></span>     | <span data-ttu-id="53a7f-134">Gerekli</span><span class="sxs-lookup"><span data-stu-id="53a7f-134">Required</span></span> | <span data-ttu-id="53a7f-135">Açıklama</span><span class="sxs-lookup"><span data-stu-id="53a7f-135">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="53a7f-136">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="53a7f-136">**customer-tenant-id**</span></span> | <span data-ttu-id="53a7f-137">**guid**</span><span class="sxs-lookup"><span data-stu-id="53a7f-137">**guid**</span></span> | <span data-ttu-id="53a7f-138">Y</span><span class="sxs-lookup"><span data-stu-id="53a7f-138">Y</span></span>        | <span data-ttu-id="53a7f-139">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="53a7f-139">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="53a7f-140">**role-id**</span><span class="sxs-lookup"><span data-stu-id="53a7f-140">**role-id**</span></span>            | <span data-ttu-id="53a7f-141">**guid**</span><span class="sxs-lookup"><span data-stu-id="53a7f-141">**guid**</span></span> | <span data-ttu-id="53a7f-142">Y</span><span class="sxs-lookup"><span data-stu-id="53a7f-142">Y</span></span>        | <span data-ttu-id="53a7f-143">Değer, kullanıcıya atanma **rolünü tanımlayan GUID** biçimli bir rol kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="53a7f-143">The value is a GUID formatted **role-id** that identifies the role to assign to the user.</span></span>                                                              |

### <a name="request-headers"></a><span data-ttu-id="53a7f-144">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="53a7f-144">Request headers</span></span>

<span data-ttu-id="53a7f-145">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="53a7f-145">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="53a7f-146">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="53a7f-146">Request body</span></span>

<span data-ttu-id="53a7f-147">Bu tablo, istek gövdesinde gerekli özellikleri açıklar.</span><span class="sxs-lookup"><span data-stu-id="53a7f-147">This table describes the required properties in the request body.</span></span>

| <span data-ttu-id="53a7f-148">Ad</span><span class="sxs-lookup"><span data-stu-id="53a7f-148">Name</span></span>                  | <span data-ttu-id="53a7f-149">Tür</span><span class="sxs-lookup"><span data-stu-id="53a7f-149">Type</span></span>       | <span data-ttu-id="53a7f-150">Gerekli</span><span class="sxs-lookup"><span data-stu-id="53a7f-150">Required</span></span> | <span data-ttu-id="53a7f-151">Açıklama</span><span class="sxs-lookup"><span data-stu-id="53a7f-151">Description</span></span>                            |
|-----------------------|------------|----------|----------------------------------------|
| <span data-ttu-id="53a7f-152">**Kimliği**</span><span class="sxs-lookup"><span data-stu-id="53a7f-152">**Id**</span></span>                | <span data-ttu-id="53a7f-153">**string**</span><span class="sxs-lookup"><span data-stu-id="53a7f-153">**string**</span></span> | <span data-ttu-id="53a7f-154">Y</span><span class="sxs-lookup"><span data-stu-id="53a7f-154">Y</span></span>        | <span data-ttu-id="53a7f-155">Role eklemek istediğiniz kullanıcının kimliği.</span><span class="sxs-lookup"><span data-stu-id="53a7f-155">The ID of the user to add to the role.</span></span> |
| <span data-ttu-id="53a7f-156">**DisplayName**</span><span class="sxs-lookup"><span data-stu-id="53a7f-156">**DisplayName**</span></span>       | <span data-ttu-id="53a7f-157">**string**</span><span class="sxs-lookup"><span data-stu-id="53a7f-157">**string**</span></span> | <span data-ttu-id="53a7f-158">Y</span><span class="sxs-lookup"><span data-stu-id="53a7f-158">Y</span></span>        | <span data-ttu-id="53a7f-159">Kullanıcının kolay görünen adı.</span><span class="sxs-lookup"><span data-stu-id="53a7f-159">The friendly display name of the user.</span></span> |
| <span data-ttu-id="53a7f-160">**Userprincipalname**</span><span class="sxs-lookup"><span data-stu-id="53a7f-160">**UserPrincipalName**</span></span> | <span data-ttu-id="53a7f-161">**string**</span><span class="sxs-lookup"><span data-stu-id="53a7f-161">**string**</span></span> | <span data-ttu-id="53a7f-162">Y</span><span class="sxs-lookup"><span data-stu-id="53a7f-162">Y</span></span>        | <span data-ttu-id="53a7f-163">Kullanıcı sorumlusu adı.</span><span class="sxs-lookup"><span data-stu-id="53a7f-163">The name of the user principal.</span></span>        |
| <span data-ttu-id="53a7f-164">**Öznitelikler**</span><span class="sxs-lookup"><span data-stu-id="53a7f-164">**Attributes**</span></span>        | <span data-ttu-id="53a7f-165">**Nesne**</span><span class="sxs-lookup"><span data-stu-id="53a7f-165">**object**</span></span> | <span data-ttu-id="53a7f-166">Y</span><span class="sxs-lookup"><span data-stu-id="53a7f-166">Y</span></span>        | <span data-ttu-id="53a7f-167">"ObjectType":"UserMember" içerir</span><span class="sxs-lookup"><span data-stu-id="53a7f-167">Contains "ObjectType":"UserMember"</span></span>     |

### <a name="request-example"></a><span data-ttu-id="53a7f-168">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="53a7f-168">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="53a7f-169">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="53a7f-169">REST response</span></span>

<span data-ttu-id="53a7f-170">Bu yöntem, kullanıcıya başarıyla rol atandığı zaman rol kimliği eklenmiş kullanıcı hesabını döndürür.</span><span class="sxs-lookup"><span data-stu-id="53a7f-170">This method returns the user account with the role ID attached when the user is successfully assigned the role.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="53a7f-171">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="53a7f-171">Response success and error codes</span></span>

<span data-ttu-id="53a7f-172">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="53a7f-172">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="53a7f-173">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="53a7f-173">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="53a7f-174">Tam liste için bkz. [İŞ ORTAĞı MERKEZI REST hata kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="53a7f-174">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="53a7f-175">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="53a7f-175">Response example</span></span>

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
