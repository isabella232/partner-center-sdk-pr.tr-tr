---
title: Bir rolden bir müşteri kullanıcısını kaldırma
description: Bir kullanıcıyı bir müşteri hesabı içindeki dizin rolünden kaldırma.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 36dc742c4f713131b4996d7dc945b6dd008a3ef5
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445655"
---
# <a name="remove-a-customer-user-from-a-role"></a><span data-ttu-id="80c94-103">Bir rolden bir müşteri kullanıcısını kaldırma</span><span class="sxs-lookup"><span data-stu-id="80c94-103">Remove a customer user from a role</span></span>

<span data-ttu-id="80c94-104">Bir kullanıcıyı bir müşteri hesabı içindeki dizin rolünden kaldırma.</span><span class="sxs-lookup"><span data-stu-id="80c94-104">How to remove a user from a directory role within a customer account.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80c94-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="80c94-105">Prerequisites</span></span>

- <span data-ttu-id="80c94-106">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="80c94-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="80c94-107">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="80c94-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="80c94-108">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="80c94-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="80c94-109">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="80c94-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="80c94-110">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="80c94-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="80c94-111">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="80c94-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="80c94-112">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="80c94-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="80c94-113">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="80c94-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="80c94-114">C\#</span><span class="sxs-lookup"><span data-stu-id="80c94-114">C\#</span></span>

<span data-ttu-id="80c94-115">Bir kullanıcıyı bir dizin rolünden kaldırmak için, Kullanıcı tarafından değiştirilecek [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemine bir çağrı ile, DIZIN rolü kimliğiyle [**Directoryroles. byıd**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) metodunu kullanarak rolü belirtin.</span><span class="sxs-lookup"><span data-stu-id="80c94-115">To remove a user from a directory role, select the customer with the user to modify with a call to the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method, From there, specify the role using the [**DirectoryRoles.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.idirectoryrolecollection.byid) method with the directory role ID.</span></span> <span data-ttu-id="80c94-116">Ardından, kaldırılacak kullanıcıyı belirlemek için [**Usermembers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) yöntemine erişin ve kullanıcıyı rolden kaldırmak için silme yöntemini ve [**silin**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) .</span><span class="sxs-lookup"><span data-stu-id="80c94-116">Then, access the [**UserMembers.ById**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermembercollection.byid) method to identify the user to remove, and the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerdirectoryroles.iusermember.delete) method to remove the user from the role.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string selectedRoleId;
// string selectedUserMemberId;

partnerOperations.Customers.ById(selectedCustomerId).DirectoryRoles.ById(selectedRoleId).UserMembers.ById(selectedUserMemberId).Delete();
```

<span data-ttu-id="80c94-117">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="80c94-117">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="80c94-118">**Project**: iş ortağı merkezi SDK örnekleri **sınıfı**: removecustomerusermemberfromdirectoryrole. cs</span><span class="sxs-lookup"><span data-stu-id="80c94-118">**Project**: Partner Center SDK Samples **Class**: RemoveCustomerUserMemberFromDirectoryRole.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="80c94-119">REST isteği</span><span class="sxs-lookup"><span data-stu-id="80c94-119">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="80c94-120">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="80c94-120">Request syntax</span></span>

| <span data-ttu-id="80c94-121">Yöntem</span><span class="sxs-lookup"><span data-stu-id="80c94-121">Method</span></span>     | <span data-ttu-id="80c94-122">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="80c94-122">Request URI</span></span>                                                                                                                           |
|------------|---------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="80c94-123">**SILMELI**</span><span class="sxs-lookup"><span data-stu-id="80c94-123">**DELETE**</span></span> | <span data-ttu-id="80c94-124">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/directoryroles/{role-ID}/usermembers/{User-id} http/1.1</span><span class="sxs-lookup"><span data-stu-id="80c94-124">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/directoryroles/{role-ID}/usermembers/{user-ID} HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="80c94-125">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="80c94-125">URI parameter</span></span>

<span data-ttu-id="80c94-126">Doğru müşteri, rol ve kullanıcıyı tanımlamak için aşağıdaki URI parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="80c94-126">Use the following URI parameters to identify the correct customer, role, and user.</span></span>

| <span data-ttu-id="80c94-127">Ad</span><span class="sxs-lookup"><span data-stu-id="80c94-127">Name</span></span>                   | <span data-ttu-id="80c94-128">Tür</span><span class="sxs-lookup"><span data-stu-id="80c94-128">Type</span></span>     | <span data-ttu-id="80c94-129">Gerekli</span><span class="sxs-lookup"><span data-stu-id="80c94-129">Required</span></span> | <span data-ttu-id="80c94-130">Açıklama</span><span class="sxs-lookup"><span data-stu-id="80c94-130">Description</span></span>                                                                        |
|------------------------|----------|----------|------------------------------------------------------------------------------------|
| <span data-ttu-id="80c94-131">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="80c94-131">**customer-tenant-id**</span></span> | <span data-ttu-id="80c94-132">**guid**</span><span class="sxs-lookup"><span data-stu-id="80c94-132">**guid**</span></span> | <span data-ttu-id="80c94-133">Y</span><span class="sxs-lookup"><span data-stu-id="80c94-133">Y</span></span>        | <span data-ttu-id="80c94-134">Değer, müşteriyi tanımlayan bir GUID biçimli **Müşteri-Kiracı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="80c94-134">The value is a GUID formatted **customer-tenant-id** that identifies the customer.</span></span> |
| <span data-ttu-id="80c94-135">**rol kimliği**</span><span class="sxs-lookup"><span data-stu-id="80c94-135">**role-id**</span></span>            | <span data-ttu-id="80c94-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="80c94-136">**guid**</span></span> | <span data-ttu-id="80c94-137">Y</span><span class="sxs-lookup"><span data-stu-id="80c94-137">Y</span></span>        | <span data-ttu-id="80c94-138">Değer, rolü tanımlayan bir GUID biçimli **rol kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="80c94-138">The value is a GUID formatted **role-id** that identifies the role.</span></span>                |
| <span data-ttu-id="80c94-139">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="80c94-139">**user-id**</span></span>            | <span data-ttu-id="80c94-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="80c94-140">**guid**</span></span> | <span data-ttu-id="80c94-141">Y</span><span class="sxs-lookup"><span data-stu-id="80c94-141">Y</span></span>        | <span data-ttu-id="80c94-142">Değer, tek bir kullanıcı hesabını tanımlayan GUID biçimli bir **Kullanıcı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="80c94-142">The value is a GUID formatted **user-id** that identifies a single user account.</span></span>   |

### <a name="request-headers"></a><span data-ttu-id="80c94-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="80c94-143">Request headers</span></span>

<span data-ttu-id="80c94-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="80c94-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="80c94-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="80c94-145">Request body</span></span>

<span data-ttu-id="80c94-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="80c94-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="80c94-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="80c94-147">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20/directoryroles/729827e3-9c14-49f7-bb1b-9608f156bbb8/usermembers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04%20 HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 0a00ec08-6273-46bb-ab6f-14a13959b381
MS-CorrelationId: 87d18a45-81fc-40cf-921a-b91cb82d67fe
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
Connection: Keep-Alive
```

## <a name="rest-response"></a><span data-ttu-id="80c94-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="80c94-148">REST response</span></span>

<span data-ttu-id="80c94-149">Kullanıcı rolden başarıyla kaldırılırsa, yanıt gövdesi boştur.</span><span class="sxs-lookup"><span data-stu-id="80c94-149">If the user is removed from the role successfully, the response body is empty.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="80c94-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="80c94-150">Response success and error codes</span></span>

<span data-ttu-id="80c94-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="80c94-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="80c94-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="80c94-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="80c94-153">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="80c94-153">For the full list, see [Partner Center REST error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="80c94-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="80c94-154">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 90bda268-7929-4ad6-be01-89c5af5fc504
MS-RequestId: e784d7aa-8c8d-45ee-8f97-9e09823d7338
MS-CV: es01VX8do0u2aTXw.0
MS-ServerId: 101112616
Date: Tue, 20 Dec 2016 23:16:35 GMT
```
