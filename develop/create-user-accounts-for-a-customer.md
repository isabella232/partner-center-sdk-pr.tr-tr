---
title: Müşteri için kullanıcı hesapları oluşturma
description: Müşteriniz için yeni bir kullanıcı hesabı oluşturun.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: d086d7ba72c9d9e42dc88684ddeafc9a597bfd7c
ms.sourcegitcommit: ad8082bee01fb1f57da423b417ca1ca9c0df8e45
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/10/2021
ms.locfileid: "111973392"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="22ced-103">Müşteri için kullanıcı hesapları oluşturma</span><span class="sxs-lookup"><span data-stu-id="22ced-103">Create user accounts for a customer</span></span>

<span data-ttu-id="22ced-104">Müşteriniz için yeni bir kullanıcı hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22ced-104">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="22ced-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="22ced-105">Prerequisites</span></span>

- <span data-ttu-id="22ced-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="22ced-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="22ced-107">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="22ced-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="22ced-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="22ced-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="22ced-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="22ced-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="22ced-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="22ced-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="22ced-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="22ced-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="22ced-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="22ced-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="22ced-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="22ced-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="22ced-114">C\#</span><span class="sxs-lookup"><span data-stu-id="22ced-114">C\#</span></span>

<span data-ttu-id="22ced-115">Bir müşteriye yeni bir kullanıcı hesabı almak için:</span><span class="sxs-lookup"><span data-stu-id="22ced-115">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="22ced-116">İlgili kullanıcı **bilgileriyle yeni** bir CustomerUser nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="22ced-116">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="22ced-117">**IAggregatePartner.Customers koleksiyonu kullanın** ve **ById() yöntemini** çağırın.</span><span class="sxs-lookup"><span data-stu-id="22ced-117">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="22ced-118">Users **özelliğini ve** ardından **Create** yöntemini çağırma.</span><span class="sxs-lookup"><span data-stu-id="22ced-118">Call the **Users** property, followed by the **Create** method.</span></span>

``` csharp
// string selectedCustomerId;
// IAggregatePartner partnerOperations;
// var SelectedCustomer;

var userToCreate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "Password!1" },
    DisplayName = "TestDisplayName",
    FirstName = "TestFirstName",
    LastName = "TestLastName",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

User createdUser = partnerOperations.Customers.ById(selectedCustomerId).Users.Create(userToCreate);
```

<span data-ttu-id="22ced-119">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="22ced-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="22ced-120">**Project:** PartnerSDK.FeatureSamples **Sınıfı:** CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="22ced-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="22ced-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="22ced-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="22ced-122">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="22ced-122">Request syntax</span></span>

| <span data-ttu-id="22ced-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="22ced-123">Method</span></span>   | <span data-ttu-id="22ced-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="22ced-124">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="22ced-125">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="22ced-125">**POST**</span></span> | <span data-ttu-id="22ced-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="22ced-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="22ced-127">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="22ced-127">URI parameters</span></span>

<span data-ttu-id="22ced-128">Doğru müşteriyi belirlemek için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="22ced-128">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="22ced-129">Ad</span><span class="sxs-lookup"><span data-stu-id="22ced-129">Name</span></span> | <span data-ttu-id="22ced-130">Tür</span><span class="sxs-lookup"><span data-stu-id="22ced-130">Type</span></span> | <span data-ttu-id="22ced-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="22ced-131">Required</span></span> | <span data-ttu-id="22ced-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="22ced-132">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="22ced-133">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="22ced-133">**customer-tenant-id**</span></span> | <span data-ttu-id="22ced-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="22ced-134">**guid**</span></span> | <span data-ttu-id="22ced-135">Y</span><span class="sxs-lookup"><span data-stu-id="22ced-135">Y</span></span> | <span data-ttu-id="22ced-136">değeri GUID biçiminde bir **customer-tenant-id değeridir.** Kurumsal bayinin, kurumsal bayiye ait olan belirli bir müşteri için sonuçları filtrelemesini sağlar.</span><span class="sxs-lookup"><span data-stu-id="22ced-136">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="22ced-137">**user-id**</span><span class="sxs-lookup"><span data-stu-id="22ced-137">**user-id**</span></span> | <span data-ttu-id="22ced-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="22ced-138">**guid**</span></span> | <span data-ttu-id="22ced-139">N</span><span class="sxs-lookup"><span data-stu-id="22ced-139">N</span></span> | <span data-ttu-id="22ced-140">Değer, tek bir kullanıcı hesabına ait OLAN GUID biçimli bir **user-id** değeridir.</span><span class="sxs-lookup"><span data-stu-id="22ced-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="22ced-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="22ced-141">Request headers</span></span>

<span data-ttu-id="22ced-142">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="22ced-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="22ced-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="22ced-143">Request body</span></span>

<span data-ttu-id="22ced-144">Yok.</span><span class="sxs-lookup"><span data-stu-id="22ced-144">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="22ced-145">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="22ced-145">Request example</span></span>

```http
POST https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "country/region code",
      "userPrincipalName": "userid@domain.onmicrosoft.com",
      "firstName": "First",
      "lastName": "Last",
      "displayName": "User name",
      "immutableId": "Some unique ID",
      "passwordProfile":{
                 password: "abCD123*",
                 forceChangePassword: true
      },
      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="22ced-146">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="22ced-146">REST response</span></span>

<span data-ttu-id="22ced-147">Başarılı olursa, bu yöntem GUID dahil olmak üzere bir kullanıcı hesabı döndürür.</span><span class="sxs-lookup"><span data-stu-id="22ced-147">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="22ced-148">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="22ced-148">Response success and error codes</span></span>

<span data-ttu-id="22ced-149">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="22ced-149">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="22ced-150">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="22ced-150">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="22ced-151">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="22ced-151">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="22ced-152">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="22ced-152">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST

{
  "usageLocation": "country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "userid@domain.onmicrosoft.com",
  "firstName": "First",
  "lastName": "Last",
  "displayName": "User name",
  "immutableId": "Some unique ID",
  "passwordProfile": {
    "forceChangePassword": true,
    "password": "abCD123*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```