---
title: Müşteri için kullanıcı rolleri alma
description: Bir kullanıcı hesabına bağlı tüm rollerin/izinlerin bir listesini alın. Çeşitlemeler, bir müşterinin tüm Kullanıcı hesapları genelinde tüm izinlerin listesini almayı ve belirli bir role sahip olan kullanıcıların bir listesini almayı içerir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8dad5c035c08905c3d39052de07ebb912452a16b
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768908"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="0adee-104">Müşteri için kullanıcı rolleri alma</span><span class="sxs-lookup"><span data-stu-id="0adee-104">Get user roles for a customer</span></span>

<span data-ttu-id="0adee-105">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="0adee-105">**Applies To**</span></span>

- <span data-ttu-id="0adee-106">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="0adee-106">Partner Center</span></span>

<span data-ttu-id="0adee-107">Bir kullanıcı hesabına bağlı tüm rollerin/izinlerin bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="0adee-107">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="0adee-108">Çeşitlemeler, bir müşterinin tüm Kullanıcı hesapları genelinde tüm izinlerin listesini almayı ve belirli bir role sahip olan kullanıcıların bir listesini almayı içerir.</span><span class="sxs-lookup"><span data-stu-id="0adee-108">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0adee-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="0adee-109">Prerequisites</span></span>

- <span data-ttu-id="0adee-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="0adee-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="0adee-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="0adee-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="0adee-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="0adee-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="0adee-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0adee-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="0adee-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="0adee-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="0adee-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="0adee-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="0adee-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="0adee-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="0adee-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="0adee-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="0adee-118">C\#</span><span class="sxs-lookup"><span data-stu-id="0adee-118">C\#</span></span>

<span data-ttu-id="0adee-119">Belirtilen bir müşterinin tüm dizin rollerini almak için, önce belirtilen müşteri KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="0adee-119">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="0adee-120">Ardından, **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0adee-120">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="0adee-121">Ardından, **Get ()** veya **GetAsync ()** yöntemi tarafından ardından **directoryroles** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0adee-121">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="0adee-122">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0adee-122">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0adee-123">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: GetCustomerDirectoryRoles.cs</span><span class="sxs-lookup"><span data-stu-id="0adee-123">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="0adee-124">Belirli bir rolü olan müşteri kullanıcılarının listesini almak için, önce belirtilen müşteri KIMLIĞINI ve dizin rolü KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="0adee-124">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="0adee-125">Ardından, **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="0adee-125">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="0adee-126">Daha sonra **Directoryroles** özelliğini ve ardından **byıd ()** yöntemini çağırın, ardından **Usermembers** özelliği, ardından **Get ()** veya **GetAsync ()** yöntemi tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="0adee-126">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="0adee-127">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="0adee-127">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="0adee-128">**Proje**: partnersdk. Featuresamples **sınıfı**: GetCustomerDirectoryRoleUserMembers.cs</span><span class="sxs-lookup"><span data-stu-id="0adee-128">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="0adee-129">REST isteği</span><span class="sxs-lookup"><span data-stu-id="0adee-129">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="0adee-130">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="0adee-130">Request syntax</span></span>

| <span data-ttu-id="0adee-131">Yöntem</span><span class="sxs-lookup"><span data-stu-id="0adee-131">Method</span></span>  | <span data-ttu-id="0adee-132">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="0adee-132">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0adee-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="0adee-133">**GET**</span></span> | <span data-ttu-id="0adee-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="0adee-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="0adee-135">**Al**</span><span class="sxs-lookup"><span data-stu-id="0adee-135">**GET**</span></span> | <span data-ttu-id="0adee-136">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="0adee-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="0adee-137">**Al**</span><span class="sxs-lookup"><span data-stu-id="0adee-137">**GET**</span></span> | <span data-ttu-id="0adee-138">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="0adee-138">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="0adee-139">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="0adee-139">URI parameter</span></span>

<span data-ttu-id="0adee-140">Doğru müşteriyi tanımlamak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="0adee-140">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="0adee-141">Ad</span><span class="sxs-lookup"><span data-stu-id="0adee-141">Name</span></span>                   | <span data-ttu-id="0adee-142">Tür</span><span class="sxs-lookup"><span data-stu-id="0adee-142">Type</span></span>     | <span data-ttu-id="0adee-143">Gerekli</span><span class="sxs-lookup"><span data-stu-id="0adee-143">Required</span></span> | <span data-ttu-id="0adee-144">Açıklama</span><span class="sxs-lookup"><span data-stu-id="0adee-144">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="0adee-145">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="0adee-145">**customer-tenant-id**</span></span> | <span data-ttu-id="0adee-146">**guid**</span><span class="sxs-lookup"><span data-stu-id="0adee-146">**guid**</span></span> | <span data-ttu-id="0adee-147">Y</span><span class="sxs-lookup"><span data-stu-id="0adee-147">Y</span></span>        | <span data-ttu-id="0adee-148">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="0adee-148">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="0adee-149">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="0adee-149">**user-id**</span></span>            | <span data-ttu-id="0adee-150">**guid**</span><span class="sxs-lookup"><span data-stu-id="0adee-150">**guid**</span></span> | <span data-ttu-id="0adee-151">N</span><span class="sxs-lookup"><span data-stu-id="0adee-151">N</span></span>        | <span data-ttu-id="0adee-152">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="0adee-152">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="0adee-153">**rol kimliği**</span><span class="sxs-lookup"><span data-stu-id="0adee-153">**role-id**</span></span>            | <span data-ttu-id="0adee-154">**guid**</span><span class="sxs-lookup"><span data-stu-id="0adee-154">**guid**</span></span> | <span data-ttu-id="0adee-155">N</span><span class="sxs-lookup"><span data-stu-id="0adee-155">N</span></span>        | <span data-ttu-id="0adee-156">Değer, bir rol türüne ait olan GUID biçimli bir **rol kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="0adee-156">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="0adee-157">Tüm Kullanıcı hesaplarında bir müşterinin tüm dizin rollerini sorgulayarak bu kimlikleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="0adee-157">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="0adee-158">(Yukarıdaki ikinci senaryo).</span><span class="sxs-lookup"><span data-stu-id="0adee-158">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="0adee-159">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="0adee-159">Request headers</span></span>

<span data-ttu-id="0adee-160">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="0adee-160">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="0adee-161">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="0adee-161">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="0adee-162">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="0adee-162">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="0adee-163">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="0adee-163">REST response</span></span>

<span data-ttu-id="0adee-164">Başarılı olursa, bu yöntem verilen kullanıcı hesabıyla ilişkili rollerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="0adee-164">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="0adee-165">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="0adee-165">Response success and error codes</span></span>

<span data-ttu-id="0adee-166">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="0adee-166">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="0adee-167">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="0adee-167">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="0adee-168">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="0adee-168">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="0adee-169">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="0adee-169">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
      "totalCount": 2,
      "items": [
        {
          "name": "Helpdesk Administrator",
          "id": "729827e3-9c14-49f7-bb1b-9608f156bbb8",
          "attributes": { "objectType": "DirectoryRole" }
        },
        {
          "name": "User Account Administrator",
          "id": "fe930be7-5e62-47db-91af-98c3a49a38b1",
          "attributes": { "objectType": "DirectoryRole" }
        }
      ],
      "attributes": { "objectType": "Collection" }
}
```
