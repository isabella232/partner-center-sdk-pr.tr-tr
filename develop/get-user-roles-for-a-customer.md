---
title: Müşteri için kullanıcı rolleri alma
description: Bir kullanıcı hesabına bağlı tüm rollerin/izinlerin bir listesini alın. Çeşitlemeler, bir müşterinin tüm Kullanıcı hesapları genelinde tüm izinlerin listesini almayı ve belirli bir role sahip olan kullanıcıların bir listesini almayı içerir.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 8f58e8b7eae5bb47265bb1ac83fcdcd160f735d2
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445927"
---
# <a name="get-user-roles-for-a-customer"></a><span data-ttu-id="80d8f-104">Müşteri için kullanıcı rolleri alma</span><span class="sxs-lookup"><span data-stu-id="80d8f-104">Get user roles for a customer</span></span>

<span data-ttu-id="80d8f-105">Bir kullanıcı hesabına bağlı tüm rollerin/izinlerin bir listesini alın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-105">Get a list of all the roles/permissions attached to a user account.</span></span> <span data-ttu-id="80d8f-106">Çeşitlemeler, bir müşterinin tüm Kullanıcı hesapları genelinde tüm izinlerin listesini almayı ve belirli bir role sahip olan kullanıcıların bir listesini almayı içerir.</span><span class="sxs-lookup"><span data-stu-id="80d8f-106">Variations include getting a list of all permissions across all user accounts for a customer, and getting a list of users that have a given role.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80d8f-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="80d8f-107">Prerequisites</span></span>

- <span data-ttu-id="80d8f-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="80d8f-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80d8f-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="80d8f-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="80d8f-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80d8f-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80d8f-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80d8f-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80d8f-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="80d8f-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80d8f-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="80d8f-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80d8f-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80d8f-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="80d8f-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="80d8f-116">C\#</span><span class="sxs-lookup"><span data-stu-id="80d8f-116">C\#</span></span>

<span data-ttu-id="80d8f-117">Belirtilen bir müşterinin tüm dizin rollerini almak için, önce belirtilen müşteri KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-117">To retrieve all the directory roles for a specified customer, first retrieve the specified customer ID.</span></span> <span data-ttu-id="80d8f-118">Ardından, **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-118">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="80d8f-119">Ardından, **Get ()** veya **GetAsync ()** yöntemi tarafından ardından **directoryroles** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-119">Then call the **DirectoryRoles** property, followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var directoryRoles = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.Get();
```

<span data-ttu-id="80d8f-120">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80d8f-120">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80d8f-121">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: getcustomerdirectoryroles. cs</span><span class="sxs-lookup"><span data-stu-id="80d8f-121">**Project**: Partner Center SDK Samples **Class**: GetCustomerDirectoryRoles.cs</span></span>

<span data-ttu-id="80d8f-122">Belirli bir rolü olan müşteri kullanıcılarının listesini almak için, önce belirtilen müşteri KIMLIĞINI ve dizin rolü KIMLIĞINI alın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-122">To retrieve a list of customer users that have a given role, first retrieve the specified customer ID and the directory role ID.</span></span> <span data-ttu-id="80d8f-123">Ardından, **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-123">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="80d8f-124">Daha sonra **Directoryroles** özelliğini ve ardından **byıd ()** yöntemini çağırın, ardından **Usermembers** özelliği, ardından **Get ()** veya **GetAsync ()** yöntemi tarafından izlenir.</span><span class="sxs-lookup"><span data-stu-id="80d8f-124">Then call the **DirectoryRoles** property, then **ById()** method, then the **UserMembers** property, the followed by the **Get()** or **GetAsync()** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// string selectedDirectoryRoleId;

var userMembers = partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedDirectoryRoleId).UserMembers.Get();
```

<span data-ttu-id="80d8f-125">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80d8f-125">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80d8f-126">**Project**: partnersdk. featuresamples **sınıfı**: getcustomerdirectoryroleusermembers. cs</span><span class="sxs-lookup"><span data-stu-id="80d8f-126">**Project**: PartnerSDK.FeatureSamples **Class**: GetCustomerDirectoryRoleUserMembers.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="80d8f-127">REST isteği</span><span class="sxs-lookup"><span data-stu-id="80d8f-127">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80d8f-128">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="80d8f-128">Request syntax</span></span>

| <span data-ttu-id="80d8f-129">Yöntem</span><span class="sxs-lookup"><span data-stu-id="80d8f-129">Method</span></span>  | <span data-ttu-id="80d8f-130">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="80d8f-130">Request URI</span></span>                                                                                                           |
|---------|-----------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80d8f-131">**Al**</span><span class="sxs-lookup"><span data-stu-id="80d8f-131">**GET**</span></span> | <span data-ttu-id="80d8f-132">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="80d8f-132">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id}/directoryroles HTTP/1.1</span></span> |
| <span data-ttu-id="80d8f-133">**Al**</span><span class="sxs-lookup"><span data-stu-id="80d8f-133">**GET**</span></span> | <span data-ttu-id="80d8f-134">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles http/1.1</span><span class="sxs-lookup"><span data-stu-id="80d8f-134">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles HTTP/1.1</span></span>                 |
| <span data-ttu-id="80d8f-135">**Al**</span><span class="sxs-lookup"><span data-stu-id="80d8f-135">**GET**</span></span> | <span data-ttu-id="80d8f-136">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers</span><span class="sxs-lookup"><span data-stu-id="80d8f-136">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers</span></span>    |

### <a name="uri-parameter"></a><span data-ttu-id="80d8f-137">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="80d8f-137">URI parameter</span></span>

<span data-ttu-id="80d8f-138">Doğru müşteriyi tanımlamak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-138">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="80d8f-139">Ad</span><span class="sxs-lookup"><span data-stu-id="80d8f-139">Name</span></span>                   | <span data-ttu-id="80d8f-140">Tür</span><span class="sxs-lookup"><span data-stu-id="80d8f-140">Type</span></span>     | <span data-ttu-id="80d8f-141">Gerekli</span><span class="sxs-lookup"><span data-stu-id="80d8f-141">Required</span></span> | <span data-ttu-id="80d8f-142">Açıklama</span><span class="sxs-lookup"><span data-stu-id="80d8f-142">Description</span></span>                                                                                                                                                                                                 |
|------------------------|----------|----------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80d8f-143">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="80d8f-143">**customer-tenant-id**</span></span> | <span data-ttu-id="80d8f-144">**guid**</span><span class="sxs-lookup"><span data-stu-id="80d8f-144">**guid**</span></span> | <span data-ttu-id="80d8f-145">Y</span><span class="sxs-lookup"><span data-stu-id="80d8f-145">Y</span></span>        | <span data-ttu-id="80d8f-146">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="80d8f-146">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span>                                                      |
| <span data-ttu-id="80d8f-147">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="80d8f-147">**user-id**</span></span>            | <span data-ttu-id="80d8f-148">**guid**</span><span class="sxs-lookup"><span data-stu-id="80d8f-148">**guid**</span></span> | <span data-ttu-id="80d8f-149">N</span><span class="sxs-lookup"><span data-stu-id="80d8f-149">N</span></span>        | <span data-ttu-id="80d8f-150">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="80d8f-150">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                                                                            |
| <span data-ttu-id="80d8f-151">**rol kimliği**</span><span class="sxs-lookup"><span data-stu-id="80d8f-151">**role-id**</span></span>            | <span data-ttu-id="80d8f-152">**guid**</span><span class="sxs-lookup"><span data-stu-id="80d8f-152">**guid**</span></span> | <span data-ttu-id="80d8f-153">N</span><span class="sxs-lookup"><span data-stu-id="80d8f-153">N</span></span>        | <span data-ttu-id="80d8f-154">Değer, bir rol türüne ait olan GUID biçimli bir **rol kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="80d8f-154">The value is a GUID formatted **role-id** that belongs to a type of role.</span></span> <span data-ttu-id="80d8f-155">Tüm Kullanıcı hesaplarında bir müşterinin tüm dizin rollerini sorgulayarak bu kimlikleri alabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80d8f-155">You can get these IDs by querying all the directory roles for a customer, across all user accounts.</span></span> <span data-ttu-id="80d8f-156">(Yukarıdaki ikinci senaryo).</span><span class="sxs-lookup"><span data-stu-id="80d8f-156">(The second scenario, above).</span></span> |

### <a name="request-headers"></a><span data-ttu-id="80d8f-157">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="80d8f-157">Request headers</span></span>

<span data-ttu-id="80d8f-158">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="80d8f-158">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80d8f-159">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="80d8f-159">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="80d8f-160">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="80d8f-160">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id>/directoryroles HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
```

## <a name="rest-response"></a><span data-ttu-id="80d8f-161">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="80d8f-161">REST response</span></span>

<span data-ttu-id="80d8f-162">Başarılı olursa, bu yöntem verilen kullanıcı hesabıyla ilişkili rollerin bir listesini döndürür.</span><span class="sxs-lookup"><span data-stu-id="80d8f-162">If successful, this method returns a list of the roles associated with the given user account.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80d8f-163">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="80d8f-163">Response success and error codes</span></span>

<span data-ttu-id="80d8f-164">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="80d8f-164">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80d8f-165">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="80d8f-165">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80d8f-166">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="80d8f-166">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80d8f-167">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="80d8f-167">Response example</span></span>

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
