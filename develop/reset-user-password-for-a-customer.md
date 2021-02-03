---
title: Müşterinin kullanıcı parolasını sıfırlama
description: Parolayı sıfırlamak, müşterinizin mevcut bir kullanıcı hesabındaki diğer ayrıntıları güncelleştirmeye çok benzer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: e0df93c2db55ec0fe49fc0e3089b7e11928f32bb
ms.sourcegitcommit: cfedd76e573c5616cf006f826f4e27f08281f7b4
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 07/08/2020
ms.locfileid: "97768873"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="f9304-103">Müşterinin kullanıcı parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="f9304-103">Reset user password for a customer</span></span>

<span data-ttu-id="f9304-104">**Uygulama hedefi**</span><span class="sxs-lookup"><span data-stu-id="f9304-104">**Applies To**</span></span>

- <span data-ttu-id="f9304-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="f9304-105">Partner Center</span></span>

<span data-ttu-id="f9304-106">Parolayı sıfırlamak, müşterinizin mevcut bir kullanıcı hesabındaki diğer ayrıntıları güncelleştirmeye çok benzer.</span><span class="sxs-lookup"><span data-stu-id="f9304-106">Resetting a password is very similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9304-107">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="f9304-107">Prerequisites</span></span>

- <span data-ttu-id="f9304-108">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="f9304-108">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="f9304-109">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="f9304-109">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="f9304-110">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="f9304-110">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="f9304-111">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="f9304-111">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="f9304-112">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="f9304-112">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="f9304-113">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="f9304-113">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="f9304-114">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="f9304-114">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="f9304-115">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="f9304-115">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="f9304-116">C\#</span><span class="sxs-lookup"><span data-stu-id="f9304-116">C\#</span></span>

<span data-ttu-id="f9304-117">Belirtilen müşteri kullanıcısının parolasını sıfırlamak için, önce belirtilen müşteri KIMLIĞINI ve hedeflenen kullanıcıyı alın.</span><span class="sxs-lookup"><span data-stu-id="f9304-117">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="f9304-118">Ardından, mevcut müşteriyle ilgili bilgileri içeren, ancak yeni bir **Passwordprofile** nesnesi ile yeni bir **customeruser** nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="f9304-118">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="f9304-119">Ardından, **ıaggregatepartner. Customers** koleksiyonunuzu kullanın ve **byıd ()** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f9304-119">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="f9304-120">Ardından **Users** özelliğini, **byıd ()** yöntemini ve sonra **Patch** yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="f9304-120">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

``` csharp
// IAggregatePartner partnerOperations;
// string selectedCustomerId;
// CustomerUser specifiedUser;

var selectedCustomer = partnerOperations.Customers.ById(selectedCustomerId).Get();
var userToUpdate = new CustomerUser()
   {
      PasswordProfile = new PasswordProfile() { ForceChangePassword = true, Password = "newPassword" },
      DisplayName = "Roger Federer",
      FirstName = "Roger",
      LastName = "Federer",
      UsageLocation = "US",
      UserPrincipalName = Guid.NewGuid().ToString("N") + "@" + selectedCustomer.CompanyProfile.Domain.ToString()
   };

// update customer user information
User updatedCustomerUserInfo = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(specifiedUser.Id).Patch(userToUpdate);

```

<span data-ttu-id="f9304-121">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="f9304-121">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="f9304-122">**Proje**: partnersdk. Featuresamples **sınıfı**: CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="f9304-122">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="f9304-123">REST isteği</span><span class="sxs-lookup"><span data-stu-id="f9304-123">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="f9304-124">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="f9304-124">Request syntax</span></span>

| <span data-ttu-id="f9304-125">Yöntem</span><span class="sxs-lookup"><span data-stu-id="f9304-125">Method</span></span>    | <span data-ttu-id="f9304-126">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="f9304-126">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="f9304-127">**DÜZELTMESI**</span><span class="sxs-lookup"><span data-stu-id="f9304-127">**PATCH**</span></span> | <span data-ttu-id="f9304-128">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-Tenant-ID}/Users http/1.1</span><span class="sxs-lookup"><span data-stu-id="f9304-128">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="f9304-129">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="f9304-129">URI parameter</span></span>

<span data-ttu-id="f9304-130">Doğru müşteriyi tanımlamak için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9304-130">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="f9304-131">Ad</span><span class="sxs-lookup"><span data-stu-id="f9304-131">Name</span></span>                   | <span data-ttu-id="f9304-132">Tür</span><span class="sxs-lookup"><span data-stu-id="f9304-132">Type</span></span>     | <span data-ttu-id="f9304-133">Gerekli</span><span class="sxs-lookup"><span data-stu-id="f9304-133">Required</span></span> | <span data-ttu-id="f9304-134">Açıklama</span><span class="sxs-lookup"><span data-stu-id="f9304-134">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="f9304-135">**Müşteri-Kiracı kimliği**</span><span class="sxs-lookup"><span data-stu-id="f9304-135">**customer-tenant-id**</span></span> | <span data-ttu-id="f9304-136">**guid**</span><span class="sxs-lookup"><span data-stu-id="f9304-136">**guid**</span></span> | <span data-ttu-id="f9304-137">Y</span><span class="sxs-lookup"><span data-stu-id="f9304-137">Y</span></span>        | <span data-ttu-id="f9304-138">Değer, satıcının satıcıya ait olan belirli bir müşteriye ait sonuçları filtrelemesine olanak tanıyan bir GUID biçimli **Müşteri-Kiracı kimliği** ' dir.</span><span class="sxs-lookup"><span data-stu-id="f9304-138">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="f9304-139">**Kullanıcı kimliği**</span><span class="sxs-lookup"><span data-stu-id="f9304-139">**user-id**</span></span>            | <span data-ttu-id="f9304-140">**guid**</span><span class="sxs-lookup"><span data-stu-id="f9304-140">**guid**</span></span> | <span data-ttu-id="f9304-141">Y</span><span class="sxs-lookup"><span data-stu-id="f9304-141">Y</span></span>        | <span data-ttu-id="f9304-142">Değer, tek bir kullanıcı hesabına ait olan GUID biçimli bir **Kullanıcı kimliği** olur.</span><span class="sxs-lookup"><span data-stu-id="f9304-142">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="f9304-143">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="f9304-143">Request headers</span></span>

<span data-ttu-id="f9304-144">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="f9304-144">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="f9304-145">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="f9304-145">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="f9304-146">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="f9304-146">Request example</span></span>

```http
PATCH https://api.partnercenter.microsoft.com/v1/customers/<customer-tenant-id>/users/<user-id> HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
{
     "passwordProfile":{
        password: "Renew456*",
        forceChangePassword: true
      },

      "attributes": {
        "objectType": "CustomerUser"
      }
}
```

## <a name="rest-response"></a><span data-ttu-id="f9304-147">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="f9304-147">REST response</span></span>

<span data-ttu-id="f9304-148">Başarılı olursa, bu yöntem, güncelleştirilmiş parola bilgileriyle birlikte Kullanıcı bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="f9304-148">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="f9304-149">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="f9304-149">Response success and error codes</span></span>

<span data-ttu-id="f9304-150">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="f9304-150">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="f9304-151">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="f9304-151">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="f9304-152">Tam liste için bkz. [hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="f9304-152">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="f9304-153">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="f9304-153">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 31942
Content-Type: application/json
MS-CorrelationId: 8a53b025-d5be-4d98-ab20-229d1813de76
MS-RequestId: b1317092-f087-471e-a637-f66523b2b94c
Date: June 24 2016 22:00:25 PST
{
  "usageLocation": "AX",
  "id": "95794928-9abe-4548-8b43-50ffc20b9404",
  "userPrincipalName": "aaaa4@abcdefgh1234.ccsctp.net",
  "firstName": "aaaa4",
  "lastName": "aaaa4",
  "displayName": "aaaa4",
  "passwordProfile": {
    "forceChangePassword": false,
    "password": "Renew456*"
  },
  "lastDirectorySyncTime": null,
  "userDomainType": "none",
  "state": "active",
  "softDeletionTime": null,
  "links": {
    "self": {
      "uri": "/customers/eebd1b55-5360-4438-a11d-5c06918c3014/users/95794928-9abe-4548-8b43-50ffc20b9404",
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
