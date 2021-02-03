---
title: Bir kullanıcıya atanan lisansları alma
description: Bir müşteri hesabındaki bir kullanıcıya atanan lisansların listesini almak için Iş Ortağı Merkezi API 'Lerini nasıl kullanacağınızı öğrenin.
ms.date: 05/22/2019
ms.service: partner-dashboard
ms.subservice: partnercenter-sdk
ms.openlocfilehash: b754ba4ecba7067f78c6868b387bac0190bfd230
ms.sourcegitcommit: a25d4951f25502cdf90cfb974022c5e452205f42
ms.translationtype: MT
ms.contentlocale: tr-TR
ms.lasthandoff: 12/04/2020
ms.locfileid: "97770096"
---
# <a name="get-licenses-assigned-to-a-user-within-a-customer-account"></a><span data-ttu-id="5e792-103">Müşteri hesabı içindeki bir kullanıcıya atanan lisansları al</span><span class="sxs-lookup"><span data-stu-id="5e792-103">Get licenses assigned to a user within a customer account</span></span>

<span data-ttu-id="5e792-104">**Uygulama hedefi:**</span><span class="sxs-lookup"><span data-stu-id="5e792-104">**Applies to:**</span></span>

- <span data-ttu-id="5e792-105">İş Ortağı Merkezi</span><span class="sxs-lookup"><span data-stu-id="5e792-105">Partner Center</span></span>

<span data-ttu-id="5e792-106">Müşteri hesabı içindeki bir kullanıcıya atanan lisansların listesini alma.</span><span class="sxs-lookup"><span data-stu-id="5e792-106">How to get a list of licenses assigned to a user within a customer account.</span></span> <span data-ttu-id="5e792-107">Burada gösterilen örneklerde, Azure Active Directory tarafından yönetilen lisansları temsil eden varsayılan lisans grubu olan grup1 'ten atanan lisanslar döndürülür.</span><span class="sxs-lookup"><span data-stu-id="5e792-107">The examples shown here return licenses assigned from group1, the default license group that represents licenses managed by Azure Active Directory.</span></span> <span data-ttu-id="5e792-108">Belirtilen lisans gruplarından atanan lisansları almak için bkz. [lisans grubuna göre kullanıcıya atanan lisansları alın](get-licenses-assigned-to-a-user-by-license-group.md).</span><span class="sxs-lookup"><span data-stu-id="5e792-108">To get licenses assigned from specified license groups, see [Get licenses assigned to a user by license group](get-licenses-assigned-to-a-user-by-license-group.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="5e792-109">Önkoşullar</span><span class="sxs-lookup"><span data-stu-id="5e792-109">Prerequisites</span></span>

- <span data-ttu-id="5e792-110">[Iş ortağı merkezi kimlik doğrulamasında](partner-center-authentication.md)açıklandığı gibi kimlik bilgileri.</span><span class="sxs-lookup"><span data-stu-id="5e792-110">Credentials as described in [Partner Center authentication](partner-center-authentication.md).</span></span> <span data-ttu-id="5e792-111">Bu senaryo yalnızca uygulama + kullanıcı kimlik bilgileriyle kimlik doğrulamayı destekler.</span><span class="sxs-lookup"><span data-stu-id="5e792-111">This scenario supports authentication with App+User credentials only.</span></span>

- <span data-ttu-id="5e792-112">Bir müşteri KIMLIĞI ( `customer-tenant-id` ).</span><span class="sxs-lookup"><span data-stu-id="5e792-112">A customer ID (`customer-tenant-id`).</span></span> <span data-ttu-id="5e792-113">Müşterinin KIMLIĞINI bilmiyorsanız Iş Ortağı Merkezi [panosunda](https://partner.microsoft.com/dashboard)bulabilirsiniz.</span><span class="sxs-lookup"><span data-stu-id="5e792-113">If you don't know the customer's ID, you can look it up in the Partner Center [dashboard](https://partner.microsoft.com/dashboard).</span></span> <span data-ttu-id="5e792-114">Iş Ortağı Merkezi menüsünden **CSP** ' yi ve ardından **müşteriler**' i seçin.</span><span class="sxs-lookup"><span data-stu-id="5e792-114">Select **CSP** from the Partner Center menu, followed by **Customers**.</span></span> <span data-ttu-id="5e792-115">Müşteri listesinden müşteriyi seçin ve ardından **Hesap**' ı seçin.</span><span class="sxs-lookup"><span data-stu-id="5e792-115">Select the customer from the customer list, then select **Account**.</span></span> <span data-ttu-id="5e792-116">Müşterinin hesap sayfasında, **müşteri hesabı bilgileri** bölümünde **Microsoft kimliği** ' ni arayın.</span><span class="sxs-lookup"><span data-stu-id="5e792-116">On the customer’s Account page, look for the **Microsoft ID** in the **Customer Account Info** section.</span></span> <span data-ttu-id="5e792-117">Microsoft KIMLIĞI, müşteri KIMLIĞI () ile aynıdır `customer-tenant-id` .</span><span class="sxs-lookup"><span data-stu-id="5e792-117">The Microsoft ID is the same as the customer ID  (`customer-tenant-id`).</span></span>

- <span data-ttu-id="5e792-118">Kullanıcı tanımlayıcısı.</span><span class="sxs-lookup"><span data-stu-id="5e792-118">A user identifier.</span></span>

## <a name="c"></a><span data-ttu-id="5e792-119">C\#</span><span class="sxs-lookup"><span data-stu-id="5e792-119">C\#</span></span>

<span data-ttu-id="5e792-120">Varsayılan grup1 lisans grubundan bir kullanıcıya hangi lisansların atandığını denetlemek için, önce müşteriyi tanımlamak üzere müşteri KIMLIĞIYLE [**ıaggregatepartner. Customers. byıd**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) yöntemini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e792-120">To check which licenses are assigned to a user from the default group1 license group, first use the [**IAggregatePartner.Customers.ById**](/dotnet/api/microsoft.store.partnercenter.customers.icustomercollection.byid) method with the customer ID to identify the customer.</span></span> <span data-ttu-id="5e792-121">Ardından kullanıcıyı tanımlamak için Kullanıcı KIMLIĞIYLE [**Users. byıd**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5e792-121">Then call the [**Users.ById**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomerusercollection.byid) method with the user ID to identify the user.</span></span> <span data-ttu-id="5e792-122">Ardından, [**lisanslar**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) özelliğinden müşteri Kullanıcı Lisansı işlemlerine yönelik bir arabirim alın.</span><span class="sxs-lookup"><span data-stu-id="5e792-122">Next, get an interface to customer user license operations from the [**Licenses**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruser.licenses) property.</span></span> <span data-ttu-id="5e792-123">Son olarak, kullanıcıya atanan lisansların koleksiyonunu almak için [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) veya [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) yöntemini çağırın.</span><span class="sxs-lookup"><span data-stu-id="5e792-123">Finally, call the [**Get**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.get) or the [**GetAsync**](/dotnet/api/microsoft.store.partnercenter.customerusers.icustomeruserlicensecollection.getasync) method to retrieve the collection of licenses assigned to the user.</span></span>

``` csharp
// string selectedCustomerUserId;
// string selectedCustomerId;
// IAggregatePartner partnerOperations;

var customerUserAssignedLicenses = partnerOperations.Customers.ById(selectedCustomerId).Users.ById(selectedCustomerUserId).Licenses.Get();
```

<span data-ttu-id="5e792-124">**Örnek**: [konsol test uygulaması](console-test-app.md).</span><span class="sxs-lookup"><span data-stu-id="5e792-124">**Sample**: [Console test app](console-test-app.md).</span></span> <span data-ttu-id="5e792-125">**Proje**: Iş Ortağı Merkezi SDK örnekleri **sınıfı**: CustomerUserAssignedLicenses.cs</span><span class="sxs-lookup"><span data-stu-id="5e792-125">**Project**: Partner Center SDK Samples **Class**: CustomerUserAssignedLicenses.cs</span></span>

## <a name="rest-request"></a><span data-ttu-id="5e792-126">REST isteği</span><span class="sxs-lookup"><span data-stu-id="5e792-126">REST request</span></span>

### <a name="request-syntax"></a><span data-ttu-id="5e792-127">İstek sözdizimi</span><span class="sxs-lookup"><span data-stu-id="5e792-127">Request syntax</span></span>

| <span data-ttu-id="5e792-128">Yöntem</span><span class="sxs-lookup"><span data-stu-id="5e792-128">Method</span></span>  | <span data-ttu-id="5e792-129">İstek URI'si</span><span class="sxs-lookup"><span data-stu-id="5e792-129">Request URI</span></span>                                                                                              |
|---------|----------------------------------------------------------------------------------------------------------|
| <span data-ttu-id="5e792-130">**Al**</span><span class="sxs-lookup"><span data-stu-id="5e792-130">**GET**</span></span> | <span data-ttu-id="5e792-131">[*{BaseUrl}*](partner-center-rest-urls.md)/v1/Customers/{Customer-ID}/Users/{User-ID}/lisanslar http/1.1</span><span class="sxs-lookup"><span data-stu-id="5e792-131">[*{baseURL}*](partner-center-rest-urls.md)/v1/customers/{customer-id}/users/{user-id}/licenses HTTP/1.1</span></span> |

### <a name="uri-parameter"></a><span data-ttu-id="5e792-132">URI parametresi</span><span class="sxs-lookup"><span data-stu-id="5e792-132">URI parameter</span></span>

<span data-ttu-id="5e792-133">Müşteriyi ve kullanıcıyı tanımlamak için aşağıdaki yol parametrelerini kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e792-133">Use the following path parameters to identify the customer and user.</span></span>

| <span data-ttu-id="5e792-134">Ad</span><span class="sxs-lookup"><span data-stu-id="5e792-134">Name</span></span>        | <span data-ttu-id="5e792-135">Tür</span><span class="sxs-lookup"><span data-stu-id="5e792-135">Type</span></span>   | <span data-ttu-id="5e792-136">Gerekli</span><span class="sxs-lookup"><span data-stu-id="5e792-136">Required</span></span> | <span data-ttu-id="5e792-137">Açıklama</span><span class="sxs-lookup"><span data-stu-id="5e792-137">Description</span></span>                                           |
|-------------|--------|----------|-------------------------------------------------------|
| <span data-ttu-id="5e792-138">müşteri kimliği</span><span class="sxs-lookup"><span data-stu-id="5e792-138">customer-id</span></span> | <span data-ttu-id="5e792-139">string</span><span class="sxs-lookup"><span data-stu-id="5e792-139">string</span></span> | <span data-ttu-id="5e792-140">Yes</span><span class="sxs-lookup"><span data-stu-id="5e792-140">Yes</span></span>      | <span data-ttu-id="5e792-141">Müşteriyi tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="5e792-141">A GUID formatted string that identifies the customer.</span></span> |
| <span data-ttu-id="5e792-142">user-id</span><span class="sxs-lookup"><span data-stu-id="5e792-142">user-id</span></span>     | <span data-ttu-id="5e792-143">string</span><span class="sxs-lookup"><span data-stu-id="5e792-143">string</span></span> | <span data-ttu-id="5e792-144">Yes</span><span class="sxs-lookup"><span data-stu-id="5e792-144">Yes</span></span>      | <span data-ttu-id="5e792-145">Kullanıcıyı tanımlayan GUID biçimli dize.</span><span class="sxs-lookup"><span data-stu-id="5e792-145">A GUID formatted string that identifies the user.</span></span>     |

### <a name="request-headers"></a><span data-ttu-id="5e792-146">İstek üst bilgileri</span><span class="sxs-lookup"><span data-stu-id="5e792-146">Request headers</span></span>

<span data-ttu-id="5e792-147">Daha fazla bilgi için bkz. [Iş ortağı MERKEZI Rest üstbilgileri](headers.md).</span><span class="sxs-lookup"><span data-stu-id="5e792-147">For more information, see [Partner Center REST headers](headers.md).</span></span>

### <a name="request-body"></a><span data-ttu-id="5e792-148">İstek gövdesi</span><span class="sxs-lookup"><span data-stu-id="5e792-148">Request body</span></span>

<span data-ttu-id="5e792-149">Yok.</span><span class="sxs-lookup"><span data-stu-id="5e792-149">None.</span></span>

### <a name="request-example"></a><span data-ttu-id="5e792-150">İstek örneği</span><span class="sxs-lookup"><span data-stu-id="5e792-150">Request example</span></span>

```http
GET https://api.partnercenter.microsoft.com/v1/customers/0c39d6d5-c70d-4c55-bc02-f620844f3fd1/users/482e2152-4b49-48ec-b715-823365ce3d4c/licenses HTTP/1.1
Authorization: Bearer <token>
Accept: application/json
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
X-Locale: en-US
Host: api.partnercenter.microsoft.com
```

## <a name="rest-response"></a><span data-ttu-id="5e792-151">REST yanıtı</span><span class="sxs-lookup"><span data-stu-id="5e792-151">REST response</span></span>

<span data-ttu-id="5e792-152">Başarılı olursa, yanıt gövdesi [Lisans](license-resources.md#license) kaynakları koleksiyonunu içerir.</span><span class="sxs-lookup"><span data-stu-id="5e792-152">If successful, the response body contains the collection of [License](license-resources.md#license) resources.</span></span>

### <a name="response-success-and-error-codes"></a><span data-ttu-id="5e792-153">Yanıt başarısı ve hata kodları</span><span class="sxs-lookup"><span data-stu-id="5e792-153">Response success and error codes</span></span>

<span data-ttu-id="5e792-154">Her yanıt başarı veya başarısızlık ve ek hata ayıklama bilgilerini gösteren bir HTTP durum kodu ile gelir.</span><span class="sxs-lookup"><span data-stu-id="5e792-154">Each response comes with an HTTP status code that indicates success or failure and additional debugging information.</span></span> <span data-ttu-id="5e792-155">Bu kodu, hata türünü ve ek parametreleri okumak için bir ağ izleme aracı kullanın.</span><span class="sxs-lookup"><span data-stu-id="5e792-155">Use a network trace tool to read this code, error type, and additional parameters.</span></span> <span data-ttu-id="5e792-156">Tam liste için bkz. [Partner Center hata kodları](error-codes.md).</span><span class="sxs-lookup"><span data-stu-id="5e792-156">For the full list, see [Partner Center error codes](error-codes.md).</span></span>

### <a name="response-example"></a><span data-ttu-id="5e792-157">Yanıt örneği</span><span class="sxs-lookup"><span data-stu-id="5e792-157">Response example</span></span>

```http
HTTP/1.1 200 OK
Content-Length: 3883
Content-Type: application/json; charset=utf-8
MS-CorrelationId: 813f15b3-eb18-4709-b2f3-668d62babf91
MS-RequestId: 68e50b00-e1ff-422a-a293-158617463d41
MS-CV: WYkHYMfWTUajFosK.0
MS-ServerId: 020021921
Date: Fri, 09 Jun 2017 00:29:24 GMT

{
    "totalCount": 1,
    "items": [{
            "servicePlans": [{
                    "displayName": "Azure Information Protection Premium P1",
                    "serviceName": "RMS_S_PREMIUM",
                    "id": "6c57d4b6-3b23-47a5-9bc9-69f17b4947b3",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Intune A Direct",
                    "serviceName": "INTUNE_A",
                    "id": "c1ec4a95-1f05-45b3-a911-aa3fa01094f5",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Active Directory Rights",
                    "serviceName": "RMS_S_ENTERPRISE",
                    "id": "bea4c11e-220a-4e6d-8eb8-8ea15d019f90",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Azure Active Directory Premium P1",
                    "serviceName": "AAD_PREMIUM",
                    "id": "41781fb2-bc02-4b7c-bd55-b576c07bb09d",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }, {
                    "displayName": "Microsoft Azure Multi-Factor Authentication",
                    "serviceName": "MFA_PREMIUM",
                    "id": "8a256a2b-b617-496d-b51b-e76466e88db0",
                    "capabilityStatus": "Assigned",
                    "targetType": "User"
                }
            ],
            "productSku": {
                "id": "efccb6f7-5641-4e0e-bd10-b4976e1bf68e",
                "name": "Enterprise Mobility + Security E3",
                "skuPartNumber": "EMS",
                "licenseGroupId": "group1"
            },
            "attributes": {
                "objectType": "License"
            }
        }
    ],
    "attributes": {
        "objectType": "Collection"
    }
}
```