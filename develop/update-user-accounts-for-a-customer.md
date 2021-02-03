---
title: Müşteri için kullanıcı hesaplarını güncelleştirme
description: Müşteri için mevcut bir kullanıcı hesabındaki ayrıntıları güncelleştirin.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: 52a43341bf2c3ba64d8c232af01f3fbae6765d82
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97769184"
---
# <a name="update-user-accounts-for-a-customer"></a><span data-ttu-id="d8851-103">Müşteri için kullanıcı hesaplarını güncelleştirme</span><span class="sxs-lookup"><span data-stu-id="d8851-103">Update user accounts for a customer</span></span>

<span data-ttu-id="d8851-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="d8851-104">**Applies To**</span></span>

- <span data-ttu-id="d8851-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="d8851-105">Partner Center</span></span>

<span data-ttu-id="d8851-106">Müşteri için mevcut bir kullanıcı hesabındaki ayrıntıları güncelleştirin.</span><span class="sxs-lookup"><span data-stu-id="d8851-106">Update details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d8851-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="d8851-107">Prerequisites</span></span>

- <span data-ttu-id="d8851-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="d8851-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="d8851-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="d8851-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="d8851-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="d8851-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="d8851-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="d8851-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="d8851-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="d8851-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="d8851-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="d8851-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="d8851-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="d8851-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="d8851-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="d8851-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="d8851-116">C\#</span><span class="sxs-lookup"><span data-stu-id="d8851-116">C\#</span></span>

<span data-ttu-id="d8851-117">Belirtilen müşteri kullanıcısının ayrıntılarını güncelleştirmek için, önce belirtilen müşteri KIMLIĞINI ve kullanıcıyı güncelleştirmek üzere alın.</span><span class="sxs-lookup"><span data-stu-id="d8851-117">To update the details for a specified customer user, first retrieve the specified customer ID and user to update.</span></span> <span data-ttu-id="d8851-118">Ardından, yeni bir **customeruser** nesnesinde kullanıcının güncelleştirilmiş bir sürümünü oluşturun.</span><span class="sxs-lookup"><span data-stu-id="d8851-118">Then, create an updated version of the user in a new **CustomerUser** object.</span></span> <span data-ttu-id="d8851-119">Ardından, **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d8851-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="d8851-120">Ardından, **Byıd (** ) yöntemi ve ardından **Patch ()** yöntemiyle **Users** özelliğini çağırın.</span><span class="sxs-lookup"><span data-stu-id="d8851-120">Then call the **Users** property, the **ById()** method, followed by the **Patch()** method.</span></span>

``` csharp
// string selectedCustomerId;
// customerUser specifiedUser;
// IAggregatePartner partnerOperations;

// Updated information
var userToUpdate = new CustomerUser()
{
    PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "testPw@!122B" },
    DisplayName = "DisplayNameChange",
    FirstName = "FirstNameChange",
    LastName = "LastNameChange",
    UsageLocation = "US",
    UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
};

// Update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="d8851-121">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="d8851-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="d8851-122">**Proje**: partnersdk. Featuresamples **sınıfı**: CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="d8851-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="d8851-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="d8851-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="d8851-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="d8851-124">Request syntax</span></span>

| <span data-ttu-id="d8851-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="d8851-125">Method</span></span>    | <span data-ttu-id="d8851-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="d8851-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8851-127">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="d8851-127">**PATCH**</span></span> | <span data-ttu-id="d8851-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="d8851-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="d8851-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="d8851-129">URI parameter</span></span>

<span data-ttu-id="d8851-130">Doğru müşteriyi tanımlamak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8851-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="d8851-131">Ad</span><span class="sxs-lookup"><span data-stu-id="d8851-131">Name</span></span>                   | <span data-ttu-id="d8851-132">Tür</span><span class="sxs-lookup"><span data-stu-id="d8851-132">Type</span></span>     | <span data-ttu-id="d8851-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="d8851-133">Required</span></span> | <span data-ttu-id="d8851-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="d8851-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="d8851-135">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="d8851-135">**customer-tenant-id**</span></span> | <span data-ttu-id="d8851-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="d8851-136">**guid**</span></span> | <span data-ttu-id="d8851-137">Y</span><span class="sxs-lookup"><span data-stu-id="d8851-137">Y</span></span>        | <span data-ttu-id="d8851-138">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="d8851-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="d8851-139">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="d8851-139">**user-id**</span></span>            | <span data-ttu-id="d8851-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="d8851-140">**guid**</span></span> | <span data-ttu-id="d8851-141">Y</span><span class="sxs-lookup"><span data-stu-id="d8851-141">Y</span></span>        | <span data-ttu-id="d8851-142">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="d8851-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="d8851-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="d8851-143">Request headers</span></span>

<span data-ttu-id="d8851-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="d8851-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="d8851-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="d8851-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="d8851-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="d8851-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
      "usageLocation": "new country/region code",

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="d8851-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="d8851-147">REST response</span></span>

<span data-ttu-id="d8851-148">Başarılı olursa, bu yöntem güncelleştirilmiş bilgileri içeren bir kullanıcı hesabı döndürür.</span><span class="sxs-lookup"><span data-stu-id="d8851-148">If successful, this method returns a user account with the updated information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="d8851-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="d8851-149">Response success and error codes</span></span>

<span data-ttu-id="d8851-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="d8851-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="d8851-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="d8851-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="d8851-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="d8851-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="d8851-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="d8851-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "new country/region code",
  "id": "4b10bf41-ab11-40e3-8c53-cd67849b50de",
  "userPrincipalName": "emailidchange@abcdefgh1234.ccsctp.net",
  "firstName": "FirstNameChange",
  "lastName": "LastNameChange",
  "displayName": "DisplayNameChange",
  "userDomainType": "none",
  "state": "active",
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/4b10bf41-ab11-40e3-8c53-cd67849b50de",
      "method": "GET",
      "headers": [

      ]
    }
  },
  "attributes": {
    "objectType": "CustomerUser"
  }
}
```
