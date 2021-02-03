---
title: Müşteri için kullanıcı hesapları oluşturma
description: Müşteriniz için yeni bir kullanıcı hesabı oluşturun.
ms.date: 05/28/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: 9131a1c4c37d07b1994b67379ec8361fda13a371
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768807"
---
# <a name="create-user-accounts-for-a-customer"></a><span data-ttu-id="9caa2-103">Müşteri için kullanıcı hesapları oluşturma</span><span class="sxs-lookup"><span data-stu-id="9caa2-103">Create user accounts for a customer</span></span>

<span data-ttu-id="9caa2-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="9caa2-104">**Applies to:**</span></span>

- <span data-ttu-id="9caa2-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="9caa2-105">Partner Center</span></span>

<span data-ttu-id="9caa2-106">Müşteriniz için yeni bir kullanıcı hesabı oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9caa2-106">Create a new user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9caa2-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="9caa2-107">Prerequisites</span></span>

- <span data-ttu-id="9caa2-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="9caa2-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="9caa2-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="9caa2-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="9caa2-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="9caa2-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="9caa2-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="9caa2-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="9caa2-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="9caa2-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="9caa2-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="9caa2-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="9caa2-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="9caa2-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="9caa2-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="9caa2-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="9caa2-116">C\#</span><span class="sxs-lookup"><span data-stu-id="9caa2-116">C\#</span></span>

<span data-ttu-id="9caa2-117">Bir müşteri için yeni bir kullanıcı hesabı almak için:</span><span class="sxs-lookup"><span data-stu-id="9caa2-117">To obtain a new user account for a customer:</span></span>

1. <span data-ttu-id="9caa2-118">İlgili kullanıcı bilgileriyle yeni bir **Customeruser** nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="9caa2-118">Create a new **CustomerUser** object with the relevant user information.</span></span>

2. <span data-ttu-id="9caa2-119">**Iaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="9caa2-119">Use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span>

3. <span data-ttu-id="9caa2-120">**Users** özelliğini çağırın, ardından **Create** yöntemi.</span><span class="sxs-lookup"><span data-stu-id="9caa2-120">Call the **Users** property, followed by the **Create** method.</span></span>

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

<span data-ttu-id="9caa2-121">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="9caa2-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="9caa2-122">**Proje**: partnersdk. Featuresamples **sınıfı**: CustomerUserCreate.cs</span><span class="sxs-lookup"><span data-stu-id="9caa2-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserCreate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="9caa2-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="9caa2-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="9caa2-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="9caa2-124">Request syntax</span></span>

| <span data-ttu-id="9caa2-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="9caa2-125">Method</span></span>   | <span data-ttu-id="9caa2-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="9caa2-126">Request URI</span></span>                                                                                  |
|----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="9caa2-127">**Yayınla**</span><span class="sxs-lookup"><span data-stu-id="9caa2-127">**POST**</span></span> | <span data-ttu-id="9caa2-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="9caa2-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

#### <a name="uri-parameters"></a><span data-ttu-id="9caa2-129">URI parametreleri</span><span class="sxs-lookup"><span data-stu-id="9caa2-129">URI parameters</span></span>

<span data-ttu-id="9caa2-130">Doğru müşteriyi tanımlamak için aşağıdaki sorgu parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="9caa2-130">Use the following query parameters to identify the correct customer.</span></span>

| <span data-ttu-id="9caa2-131">Ad</span><span class="sxs-lookup"><span data-stu-id="9caa2-131">Name</span></span> | <span data-ttu-id="9caa2-132">Tür</span><span class="sxs-lookup"><span data-stu-id="9caa2-132">Type</span></span> | <span data-ttu-id="9caa2-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="9caa2-133">Required</span></span> | <span data-ttu-id="9caa2-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="9caa2-134">Description</span></span> |
|----- |----- | -------- |------------ |
| <span data-ttu-id="9caa2-135">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="9caa2-135">**customer-tenant-id**</span></span> | <span data-ttu-id="9caa2-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="9caa2-136">**guid**</span></span> | <span data-ttu-id="9caa2-137">Y</span><span class="sxs-lookup"><span data-stu-id="9caa2-137">Y</span></span> | <span data-ttu-id="9caa2-138">Değer, bir GUID biçimli **Müşteri-Kiracı kimliği** olur. Satıcının, satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanır.</span><span class="sxs-lookup"><span data-stu-id="9caa2-138">The value is a GUID formatted **customer-tenant-id**. It allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="9caa2-139">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="9caa2-139">**user-id**</span></span> | <span data-ttu-id="9caa2-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="9caa2-140">**guid**</span></span> | <span data-ttu-id="9caa2-141">N</span><span class="sxs-lookup"><span data-stu-id="9caa2-141">N</span></span> | <span data-ttu-id="9caa2-142">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="9caa2-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span> |

### <a name="request-headers"></a><span data-ttu-id="9caa2-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="9caa2-143">Request headers</span></span>

<span data-ttu-id="9caa2-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="9caa2-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="9caa2-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="9caa2-145">Request body</span></span>

<span data-ttu-id="9caa2-146">Yok.</span><span class="sxs-lookup"><span data-stu-id="9caa2-146">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="9caa2-147">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="9caa2-147">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="9caa2-148">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="9caa2-148">REST response</span></span>

<span data-ttu-id="9caa2-149">Başarılı olursa, bu yöntem GUID de dahil olmak üzere bir kullanıcı hesabı döndürür.</span><span class="sxs-lookup"><span data-stu-id="9caa2-149">If successful, this method returns a user account, including the GUID.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="9caa2-150">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="9caa2-150">Response success and error codes</span></span>

<span data-ttu-id="9caa2-151">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="9caa2-151">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="9caa2-152">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="9caa2-152">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="9caa2-153">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="9caa2-153">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="9caa2-154">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="9caa2-154">Response example</span></span>

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