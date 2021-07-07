---
title: Müşterinin kullanıcı parolasını sıfırlama
description: Parolayı sıfırlamak, mevcut bir kullanıcı hesabında müşteriniz için diğer ayrıntıları güncelleştirmeye benzer.
ms.date: 12/15/2017
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
author: dineshvu
ms.author: dineshvu
ms.openlocfilehash: f3661a588f566485cbd58035c63ae9f8e5d383af
ms.sourcegitcommit: 0b2a62af1765a447addd9c4340c28bc42fdc2747
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 06/04/2021
ms.locfileid: "111445689"
---
# <a name="reset-user-password-for-a-customer"></a><span data-ttu-id="041bb-103">Müşterinin kullanıcı parolasını sıfırlama</span><span class="sxs-lookup"><span data-stu-id="041bb-103">Reset user password for a customer</span></span>

<span data-ttu-id="041bb-104">Parolayı sıfırlamak, mevcut bir kullanıcı hesabında müşteriniz için diğer ayrıntıları güncelleştirmeye benzer.</span><span class="sxs-lookup"><span data-stu-id="041bb-104">Resetting a password is similar to updating other details in an existing user account for your customer.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="041bb-105">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="041bb-105">Prerequisites</span></span>

- <span data-ttu-id="041bb-106">kimlik doğrulamasında açıklandığı gibi [İş Ortağı Merkezi bilgileri.](partner-center-authentication.md)</span><span class="sxs-lookup"><span data-stu-id="041bb-106">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="041bb-107">Bu senaryo yalnızca App+User kimlik bilgileriyle kimlik doğrulamasını destekler.</span><span class="sxs-lookup"><span data-stu-id="041bb-107">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="041bb-108">Müşteri kimliği ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="041bb-108">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="041bb-109">Müşterinin kimliğini bilmiyorsanız bu kimliği panoda [İş Ortağı Merkezi.](https://partner.microsoft.com/dashboard)</span><span class="sxs-lookup"><span data-stu-id="041bb-109">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="041bb-110">İş Ortağı Merkezi **menüsünden CSP'yi** ve ardından **Müşteriler'i seçin.**</span><span class="sxs-lookup"><span data-stu-id="041bb-110">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="041bb-111">Müşteri listesinden müşteriyi ve ardından Hesap'ı **seçin.**</span><span class="sxs-lookup"><span data-stu-id="041bb-111">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="041bb-112">Müşterinin Hesap sayfasında Müşteri Hesabı Bilgileri **bölümünde Microsoft** **Kimliği'ne** bakın.</span><span class="sxs-lookup"><span data-stu-id="041bb-112">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="041bb-113">Microsoft Kimliği, müşteri kimliği () ile `customer-tenant-id` aynıdır.</span><span class="sxs-lookup"><span data-stu-id="041bb-113">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

## <a name="c"></a><span data-ttu-id="041bb-114">C\#</span><span class="sxs-lookup"><span data-stu-id="041bb-114">C\#</span></span>

<span data-ttu-id="041bb-115">Belirtilen bir müşteri kullanıcıya yönelik bir parolayı sıfırlamak için önce belirtilen müşteri kimliğini ve hedeflenen kullanıcıyı alın.</span><span class="sxs-lookup"><span data-stu-id="041bb-115">To reset a password for a specified customer user, first retrieve the specified customer ID and the targeted user.</span></span> <span data-ttu-id="041bb-116">Ardından, mevcut **müşteriyle ilgili bilgileri** içeren ancak yeni bir **PasswordProfile** nesnesi olan yeni bir CustomerUser nesnesi oluşturun.</span><span class="sxs-lookup"><span data-stu-id="041bb-116">Then, create a new **CustomerUser** object that contains the information for the existing customer, but with a new **PasswordProfile** object.</span></span> <span data-ttu-id="041bb-117">Ardından **IAggregatePartner.Customers koleksiyonu kullanın** ve **ById() yöntemini** çağırın.</span><span class="sxs-lookup"><span data-stu-id="041bb-117">Then, use your **IAggregatePartner.Customers** collection and call the **ById()** method.</span></span> <span data-ttu-id="041bb-118">Ardından **Users özelliğini,** **ById() yöntemini** ve patch yöntemini çağırabilirsiniz. </span><span class="sxs-lookup"><span data-stu-id="041bb-118">Then call the **Users** property, the **ById()** method, and then the **Patch** method.</span></span>

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

<span data-ttu-id="041bb-119">**Örnek:** [Konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="041bb-119">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="041bb-120">**Project:** PartnerSDK.FeatureSamples **Sınıfı:** CustomerUserUpdate.cs</span><span class="sxs-lookup"><span data-stu-id="041bb-120">**Project**: PartnerSDK.FeatureSamples **Class**: CustomerUserUpdate.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="041bb-121">REST isteği</span><span class="sxs-lookup"><span data-stu-id="041bb-121">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="041bb-122">İstek söz dizimi</span><span class="sxs-lookup"><span data-stu-id="041bb-122">Request syntax</span></span>

| <span data-ttu-id="041bb-123">Yöntem</span><span class="sxs-lookup"><span data-stu-id="041bb-123">Method</span></span>    | <span data-ttu-id="041bb-124">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="041bb-124">Request URI</span></span>                                                                                  |
|-----------|----------------------------------------------------------------------------------------------|
| <span data-ttu-id="041bb-125">**Yama**</span><span class="sxs-lookup"><span data-stu-id="041bb-125">**PATCH**</span></span> | <span data-ttu-id="041bb-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span><span class="sxs-lookup"><span data-stu-id="041bb-126">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-tenant-id}/users HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="041bb-127">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="041bb-127">URI parameter</span></span>

<span data-ttu-id="041bb-128">Doğru müşteriyi belirlemek için aşağıdaki sorgu parametresini kullanın.</span><span class="sxs-lookup"><span data-stu-id="041bb-128">Use the following query parameter to identify the correct customer.</span></span>

| <span data-ttu-id="041bb-129">Ad</span><span class="sxs-lookup"><span data-stu-id="041bb-129">Name</span></span>                   | <span data-ttu-id="041bb-130">Tür</span><span class="sxs-lookup"><span data-stu-id="041bb-130">Type</span></span>     | <span data-ttu-id="041bb-131">Gerekli</span><span class="sxs-lookup"><span data-stu-id="041bb-131">Required</span></span> | <span data-ttu-id="041bb-132">Açıklama</span><span class="sxs-lookup"><span data-stu-id="041bb-132">Description</span></span>                                                                                                                                            |
|------------------------|----------|----------|--------------------------------------------------------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="041bb-133">**customer-tenant-id**</span><span class="sxs-lookup"><span data-stu-id="041bb-133">**customer-tenant-id**</span></span> | <span data-ttu-id="041bb-134">**guid**</span><span class="sxs-lookup"><span data-stu-id="041bb-134">**guid**</span></span> | <span data-ttu-id="041bb-135">Y</span><span class="sxs-lookup"><span data-stu-id="041bb-135">Y</span></span>        | <span data-ttu-id="041bb-136">Değer, kurumsal bayinin kurumsal **bayiye** ait olan belirli bir müşteri için sonuçları filtrelemesini sağlayan GUID biçimli bir müşteri kiracı kimliğidir.</span><span class="sxs-lookup"><span data-stu-id="041bb-136">The value is a GUID formatted **customer-tenant-id** that allows the reseller to filter the results for a given customer that belongs to the reseller.</span></span> |
| <span data-ttu-id="041bb-137">**user-id**</span><span class="sxs-lookup"><span data-stu-id="041bb-137">**user-id**</span></span>            | <span data-ttu-id="041bb-138">**guid**</span><span class="sxs-lookup"><span data-stu-id="041bb-138">**guid**</span></span> | <span data-ttu-id="041bb-139">Y</span><span class="sxs-lookup"><span data-stu-id="041bb-139">Y</span></span>        | <span data-ttu-id="041bb-140">Değer, tek bir kullanıcı hesabına ait OLAN GUID biçimli bir **user-id** değeridir.</span><span class="sxs-lookup"><span data-stu-id="041bb-140">The value is a GUID formatted **user-id** that belongs to a single user account.</span></span>                                                                       |

### <a name="request-headers"></a><span data-ttu-id="041bb-141">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="041bb-141">Request headers</span></span>

<span data-ttu-id="041bb-142">Daha fazla bilgi için [bkz. İş Ortağı Merkezi REST üst bilgileri.](headers.md)</span><span class="sxs-lookup"><span data-stu-id="041bb-142">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="041bb-143">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="041bb-143">Request body</span></span>

### <a name="request-example"></a><span data-ttu-id="041bb-144">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="041bb-144">Request example</span></span>

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

## <a name="rest-response"></a><span data-ttu-id="041bb-145">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="041bb-145">REST response</span></span>

<span data-ttu-id="041bb-146">Başarılı olursa, bu yöntem güncelleştirilmiş parola bilgileriyle birlikte kullanıcı bilgilerini döndürür.</span><span class="sxs-lookup"><span data-stu-id="041bb-146">If successful, this method returns the user information, along with the updated password information.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="041bb-147">Yanıt başarı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="041bb-147">Response success and error codes</span></span>

<span data-ttu-id="041bb-148">Her yanıt, başarılı veya başarısız olduğunu belirten bir HTTP durum kodu ve ek hata ayıklama bilgileriyle birlikte gelir.</span><span class="sxs-lookup"><span data-stu-id="041bb-148">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="041bb-149">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="041bb-149">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="041bb-150">Tam liste için bkz. [Hata Kodları.](error-codes.md)</span><span class="sxs-lookup"><span data-stu-id="041bb-150">For the full list, see [Error Codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="041bb-151">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="041bb-151">Response example</span></span>

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
