---
title: Müşterinin kullanıcı hesabını silme
description: Bir müşterinin mevcut kullanıcı hesabını silme.
ms.date: 06/20/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 77fc1a1c7264779ca549be8d52798e90c91138bb
ms.sourcegitcommit: 58801b7a09c19ce57617ec4181a008a673b725f0
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 09/22/2020
ms.locfileid: "97769382"
---
# <a name="delete-a-user-account-for-a-customer"></a><span data-ttu-id="617fa-103">Müşterinin kullanıcı hesabını silme</span><span class="sxs-lookup"><span data-stu-id="617fa-103">Delete a user account for a customer</span></span>

<span data-ttu-id="617fa-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="617fa-104">**Applies to:**</span></span>

- <span data-ttu-id="617fa-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="617fa-105">Partner Center</span></span>

<span data-ttu-id="617fa-106">Bu makalede, bir müşterinin mevcut kullanıcı hesabının nasıl silineceği açıklanır.</span><span class="sxs-lookup"><span data-stu-id="617fa-106">This article explains how to delete an existing user account for a customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="617fa-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="617fa-107">Prerequisites</span></span>

- <span data-ttu-id="617fa-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="617fa-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="617fa-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="617fa-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="617fa-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="617fa-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="617fa-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="617fa-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="617fa-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="617fa-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="617fa-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="617fa-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="617fa-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="617fa-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="617fa-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="617fa-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="617fa-116">Bir kullanıcı KIMLIĞI.</span><span class="sxs-lookup"><span data-stu-id="617fa-116">A user ID.</span></span> <span data-ttu-id="617fa-117">Kullanıcı KIMLIĞINIZ yoksa, bkz. [bir müşterinin tüm Kullanıcı hesaplarının listesini alın](get-a-list-of-all-user-accounts-for-a-customer.md).</span><span class="sxs-lookup"><span data-stu-id="617fa-117">If you do not have the user ID, see [Get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md).</span></span>

## <a name="deleting-a-user-account"></a><span data-ttu-id="617fa-118">Kullanıcı hesabını silme</span><span class="sxs-lookup"><span data-stu-id="617fa-118">Deleting a user account</span></span>

<span data-ttu-id="617fa-119">Bir kullanıcı hesabını sildiğinizde, Kullanıcı durumu otuz gün boyunca **etkin değil** olarak ayarlanır.</span><span class="sxs-lookup"><span data-stu-id="617fa-119">When you delete a user account, the user state is set to **inactive** for thirty days.</span></span> <span data-ttu-id="617fa-120">Otuz gün sonra, Kullanıcı hesabı ve onunla ilişkili veriler temizlenir ve kurtarılamaz hale getirilir.</span><span class="sxs-lookup"><span data-stu-id="617fa-120">After thirty days, the user account and its associated data are purged and made unrecoverable.</span></span>

<span data-ttu-id="617fa-121">Etkin olmayan hesap otuz gün penceresinde yer alıyorsa, [bir müşterinin silinen kullanıcı hesabını geri yükleyebilirsiniz](restore-a-user-for-a-customer.md) .</span><span class="sxs-lookup"><span data-stu-id="617fa-121">You can [restore a deleted user account for a customer](restore-a-user-for-a-customer.md) if the inactive account is within the thirty day window.</span></span> <span data-ttu-id="617fa-122">Ancak, silinmiş ve devre dışı olarak işaretlenen bir hesabı geri yüklediğinizde, hesap artık kullanıcı koleksiyonunun bir üyesi olarak döndürülmez (örneğin, [bir müşterinin tüm Kullanıcı hesaplarının bir listesini](get-a-list-of-all-user-accounts-for-a-customer.md)aldığınızda).</span><span class="sxs-lookup"><span data-stu-id="617fa-122">However, when you restore an account that was deleted and marked as inactive, the account is no longer returned as a member of the user collection (for example, when you [get a list of all user accounts for a customer](get-a-list-of-all-user-accounts-for-a-customer.md)).</span></span>

## <a name="c"></a><span data-ttu-id="617fa-123">C\#</span><span class="sxs-lookup"><span data-stu-id="617fa-123">C\#</span></span>

<span data-ttu-id="617fa-124">Mevcut bir müşteri Kullanıcı hesabını silmek için:</span><span class="sxs-lookup"><span data-stu-id="617fa-124">To delete an existing customer user account:</span></span>

1. <span data-ttu-id="617fa-125">Müşteriyi tanımlamak için, müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. Byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="617fa-125">Use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span>

2. <span data-ttu-id="617fa-126">Kullanıcıyı tanımlamak için [**Users. Byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) metodunu çağırın.</span><span class="sxs-lookup"><span data-stu-id="617fa-126">Call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method to identify the user.</span></span>

3. <span data-ttu-id="617fa-127">Kullanıcıyı silmek ve Kullanıcı durumunu devre dışı olarak ayarlamak için [**silme**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="617fa-127">Call the [**Delete**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.delete) method to delete the user and set the user state to inactive.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// string customerUserIdToDelete;

partnerOperations.Customers.ById(selectedCustomerId).Users.ById(customerUserIdToDelete).Delete();
```

<span data-ttu-id="617fa-128">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="617fa-128">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="617fa-129">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: DeleteCustomerUser.cs</span><span class="sxs-lookup"><span data-stu-id="617fa-129">**Project**: Partner Center SDK Samples **Class**: DeleteCustomerUser.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="617fa-130">REST isteği</span><span class="sxs-lookup"><span data-stu-id="617fa-130">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="617fa-131">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="617fa-131">Request syntax</span></span>

| <span data-ttu-id="617fa-132">Yöntem</span><span class="sxs-lookup"><span data-stu-id="617fa-132">Method</span></span>     | <span data-ttu-id="617fa-133">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="617fa-133">Request URI</span></span>                                                                                            |
|------------|--------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="617fa-134">DELETE</span><span class="sxs-lookup"><span data-stu-id="617fa-134">DELETE</span></span>     | <span data-ttu-id="617fa-135">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users/{User-ID} http/1.1</span><span class="sxs-lookup"><span data-stu-id="617fa-135">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users/{user-id} HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="617fa-136">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="617fa-136">URI parameters</span></span>

<span data-ttu-id="617fa-137">Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="617fa-137">Use the following query parameters to identify the customer and user.</span></span>

| <span data-ttu-id="617fa-138">Ad</span><span class="sxs-lookup"><span data-stu-id="617fa-138">Name</span></span>                   | <span data-ttu-id="617fa-139">Tür</span><span class="sxs-lookup"><span data-stu-id="617fa-139">Type</span></span>     | <span data-ttu-id="617fa-140">Gerekli</span><span class="sxs-lookup"><span data-stu-id="617fa-140">Required</span></span> | <span data-ttu-id="617fa-141">Açıklama</span><span class="sxs-lookup"><span data-stu-id="617fa-141">Description</span></span>                                                                                                               |
|------------------------|----------|----------|---------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="617fa-142">Müşteri-Kiracı kimliği</span><span class="sxs-lookup"><span data-stu-id="617fa-142">customer-tenant-id</span></span>     | <span data-ttu-id="617fa-143">GUID</span><span class="sxs-lookup"><span data-stu-id="617fa-143">GUID</span></span>     | <span data-ttu-id="617fa-144">Y</span><span class="sxs-lookup"><span data-stu-id="617fa-144">Y</span></span>        | <span data-ttu-id="617fa-145">Değer, satıcının belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-kiracı kimliğidir** .</span><span class="sxs-lookup"><span data-stu-id="617fa-145">The value is a GUID-formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer.</span></span> |
| <span data-ttu-id="617fa-146">user-id</span><span class="sxs-lookup"><span data-stu-id="617fa-146">user-id</span></span>                | <span data-ttu-id="617fa-147">GUID</span><span class="sxs-lookup"><span data-stu-id="617fa-147">GUID</span></span>     | <span data-ttu-id="617fa-148">Y</span><span class="sxs-lookup"><span data-stu-id="617fa-148">Y</span></span>        | <span data-ttu-id="617fa-149">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliğidir** .</span><span class="sxs-lookup"><span data-stu-id="617fa-149">The value is a GUID-formatted **user-id** that belongs to a single user account.</span></span>                                          |

### <a name="request-headers"></a><span data-ttu-id="617fa-150">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="617fa-150">Request headers</span></span>

<span data-ttu-id="617fa-151">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="617fa-151">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="617fa-152">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="617fa-152">Request body</span></span>

<span data-ttu-id="617fa-153">Yok.</span><span class="sxs-lookup"><span data-stu-id="617fa-153">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="617fa-154">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="617fa-154">Request example</span></span>

```http
DELETE https://api.partnercenter.microsoft.com/v1/customers/4d3cf487-70f4-4e1e-9ff1-b2bfce8d9f04/users/a45f1416-3300-4f65-9e8d-f123b397a4ea HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
X-Locale: en-US
Host: api.partnercenter.microsoft.com
Content-Length: 0
```

## <a name="rest-response"></a><span data-ttu-id="617fa-155">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="617fa-155">REST response</span></span>

<span data-ttu-id="617fa-156">Başarılı olursa, bu yöntem bir **204 içerik** durum kodu döndürür.</span><span class="sxs-lookup"><span data-stu-id="617fa-156">If successful, this method returns a **204 No Content** status code.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="617fa-157">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="617fa-157">Response success and error codes</span></span>

<span data-ttu-id="617fa-158">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="617fa-158">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="617fa-159">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="617fa-159">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="617fa-160">Tam liste için bkz. [Iş ortağı MERKEZI Rest hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="617fa-160">For the full list, see [Partner Center REST Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="617fa-161">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="617fa-161">Response example</span></span>

```http
HTTP/1.1 204 No Content
Content-Length: 0
MS-CorrelationId: 709c0b80-016c-4662-b29f-697fdf03e87a
MS-RequestId: f113b126-ec13-4baa-ab4d-67c245244971
MS-CV: 90KUJA7HKEaG8wHu.0
MS-ServerId: 101112616
Date: Tue, 24 Jan 2017 23:27:18 GMT
```
